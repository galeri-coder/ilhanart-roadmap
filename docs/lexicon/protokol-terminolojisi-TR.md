# 📜 Protokol Terminolojisi ve Teknik Sözlük 🇹🇷
> **Protocol Version:** 1.0 (Stable)  
> **Network Vision:** 2025 → 3000 Archive  
> **Ecosystem:** [PoArt] + [FPP] + [Michelangelo] + [Cultural Layers]  
> **Status:** **HARD_LOCKED** (Active Documentation)  
> **Integrity:** SHA-512 Sealed (Digital Notary Compatible)

---

**İçindekiler**

**1. Pillars of the Protocol (Temel Protokoller)  
2. Roles & Entities (Roller ve Varlıklar)  
3. Economic & Governance Metrics (Ekonomik & Yönetişim Metrikleri)  
4. Security & Validation (Güvenlik & Doğrulama)  
5. Validation & Persistence (Doğrulama & Süreklilik)  
6. Decentralized Supervision (Merkeziyetsiz Denetim)  
7. The Michelangelo Framework (Meritocracy Engine)  
8. Cultural Multipliers & Ranking Levels (Kültürel Çarpanlar & Rütbeler)  
9. Cut-off Thresholds & Network Metrics (Eşikler & Ağ Metrikleri)  
10. Intellectual Framework (Entelektüel Yapı)  
11. Advanced Sybil Resistance (Gelişmiş Saldırı Koruması)  
12. Generational Legacy & Governance (Nesiller Arası Miras & Yönetim)  
13. Cultural Privilege Layers & Real-World Integration (Fiziksel Entegrasyon)  
14. State Machine (Kayıt Yaşam Döngüsü)  
15. Minimal On-chain / Maximal Off-chain (Zincir Üstü / Zincir Dışı Model)  
16. Appeals / Mercii & İtiraz Mekanizması (Kurumsal Güven Katmanı)  
17. Threat Model (Saldırı Kataloğu ve Karşı Katmanlar)  
18. Final Word: A Blueprint for Global Governance (Manifesto)  
19. Roadmap & Future Notes (Yol Haritası Notu)**

---

## 🔰 Katmanlı Mimariye Genel Bakış

| Katman | Amaç | Protokol |
|:--|:--|:--|
| **L1** | Emek doğrulama | **PoArt (Proof of Art)** |
| **L2** | Sadakat / ekonomi | **FPP (Foundational Pillar Protocol)** |
| **L3** | Yönetim | **Michelangelo Framework (Meritocracy Engine)** |
| **L4** | Kültürel entegrasyon | **Cultural Layers & Privileges** |

Bu yapı, ekosistemin teknik ve felsefi bütünlüğünü dört temel seviyede özetler.  
Yeni katılan bir kullanıcı bu tablo üzerinden tüm protokol mimarisini 2 dakikada kavrayabilir.

---

## 🔐 Kriptografik Primitifler (v1.0 Sabitleri)

- Bu dokümanda **Hash(x)** ifadesi **SHA-512(x)** anlamındadır.
- **MerkleRoot(AllFiles):** Yaprak ve iç düğüm hash’leri **SHA-512** ile üretilir.
- **SignerSignature:** Bir cüzdanın özel anahtarıyla üretilen, doğrulamada kullanılan imzadır (hash değildir).
- Tüm “seal / root / signature-ref” hesapları deterministik ve doğrulanabilir olacak şekilde tanımlanır.

- **SignatureScheme (v1.0): Ed25519 (RFC 8032)**
  - **SignerPublicKey:** 32-byte raw (hex string değil)
  - **SignerSignature:** 64-byte raw (hex/base64 sadece gösterim; protokol bytes kabul eder)
  - **VoterId (v1.0 normu):** `VoterId = SignerPublicKey` (32-byte raw, length-prefixed field içinde taşınır)
  - **Signature Domain Separation (v1.0):**
    - Her imza mutlaka 1-byte `DomainTag` ile ayrıştırılır (cross-protocol replay önlenir).
    - Örn:
      - `0x01` = VoteReceiptBody imzası
      - `0x48` = Heartbeat Light Proof / StateDigest (dokümanda tanımlı)
      - (Genişletmeler v1.1+ ile eklenebilir)
  - **Signing kuralı (v1.0):**
    - İmza mesajı: `SigMsg = SHA-512( DomainTag || PayloadBytes )`
    - İmza: `SignerSignature = Ed25519.Sign( sk, SigMsg )`
  - **Verification kuralı (v1.0):**
    - `Ed25519.Verify( pk=VoterId, msg=SigMsg, sig=SignerSignature ) == TRUE`
  - **Canonical signature kuralları (v1.0):**
    - `SignerSignature` uzunluğu **tam 64 byte** olmak zorundadır; aksi reddedilir.
    - Non-canonical/invalid Ed25519 encoding reddedilir.


- **Canonical Encoding (v1.0):** Dokümanda `A || B || C` ifadesi; alanların **byte düzeyinde** deterministik encode edilip birleştirilmesi demektir.  
  - `field(X)` tanımı:
    - **Sabit uzunluklu** alanlar: `field(X)=enc(X)` (**length prefix yok**)
    - **Değişken uzunluklu** alanlar (ör. string/bytes): `field(X)=u32be(len(enc(X))) || enc(X)`
      - `len(...)` = **encode edilmiş verinin byte uzunluğu** (UTF-8 string ise UTF-8 byte sayısı)
  - `A || B || C = field(A) || field(B) || field(C)`
  - **Sabit tip/uzunluk standartları (v1.0):**
    - **SHA-512 digest** = **64-byte raw** (hex string değil)
    - **TimeStamp** = `u64be` (**8 byte**, UTC Unix seconds)
    - **VoteChoice** = `u8` (0=Abstain, 1=Yes, 2=No, 3=Veto)
    - **Weight** = `u128be` (unsigned 128-bit, big-endian)
  - **Amaç:** `A||B` birleştirmelerinde sınırların karışmasını önlemek ve **ambiguous concatenation** riskini sıfırlamak.

- **VoterConsensusRoot (v1.0):** Bir oylamanın/kararın çıktısını ve oy setini tek bir 64-byte köke bağlayan değer.  
  - `VoteLeaf_i = SHA-512( 0x00 || VoteReceiptBytes_i )`
  - `VoteSetRoot = MerkleRoot( sort_lex( VoteLeaf_1..n ) )`  *(SHA-512 ile; yapraklar lexicographic sıralanır)*
  - `ConsensusEnvelopeBytes = (`
    `ProposalRef || SnapshotTime || YesWeight || NoWeight || AbstainWeight ||`
    `QuorumWeight || VetoWeight || ResultCode || VoteSetRoot`
    `)`  *(hepsi `||` = Canonical Encoding’e göre)*
  - `VoterConsensusRoot = SHA-512( ConsensusEnvelopeBytes )`
  - **Alan tipleri:**
    - `ProposalRef` = bytes (değişken; `field(ProposalRef)` length-prefixed)
    - `SnapshotTime` = `u64be`
    - `YesWeight/NoWeight/AbstainWeight/QuorumWeight/VetoWeight` = `u128be`
    - `ResultCode` = `u8` (0=Rejected, 1=Accepted, 2=Revoked, 3=Timeout)
    - `VoteSetRoot` = 64-byte raw (SHA-512 digest)

---

## 🧩 Üyelik Seviyeleri — “Primer → Texture → Impasto” (TWAB Tier)

Tier, yalnızca TWAB’dan türetilen **logaritmik skor** üzerinden belirlenir:

$$
\text{ScoreTWAB}=\log_{10}(\text{TWAB}_{30d}+1)
$$

| Seviye | Tanım | Teknik Temel (v1.0) |
|:--|:--|:--|
| **Primer (Astar)** | Giriş seviyesi. | `0 < ScoreTWAB ≤ 3` |
| **Texture (Doku)** | Aktif katılımcı. | `3 < ScoreTWAB ≤ 5` |
| **Impasto (Katman)** | Üst çekirdek seviye. | `ScoreTWAB > 5` |

Formül:

$$
\text{Tier}(u)=
\begin{cases}
\text{Primer},&0<\text{ScoreTWAB}_u\le3\\
\text{Texture},&3<\text{ScoreTWAB}_u\le5\\
\text{Impasto},&\text{ScoreTWAB}_u>5
\end{cases}
$$

> **Cooldown kuralı (v1.0):** Adres `CooldownWindow` içindeyse Tier belirlemede
> `ScoreTWAB = log10(EffectiveTWAB_{30d}+1)` kullanılır.

> Not: ScoreTWAB, TWAB’dan deterministik türediği için Tier hâlâ “TWAB tabanlıdır”.  
> Bu eşikler **Turnstile** gibi giriş barajlarıyla ölçek uyumunu korur.


> **Not (isim çakışması giderildi):**  
> “Primer/Texture/Impasto” **Üyelik Seviyesi (Tier)** olarak yalnızca **TWAB**’a göre belirlenir.  
> **Rütbe Sınıfı (Rank)** ise **Pts** üzerinden belirlenir ve **Rank-I / Rank-II / Rank-III** olarak adlandırılır.  
> **Pts**, TWAB + kültürel katkı + denetim/oylama katılımı gibi bileşenlerden türetilen birleşik bir skordur.

---

## 🏛️ 1) Pillars of the Protocol (Temel Protokoller)

### **[PoArt] Proof of Art (v1.0)**
* **Tanım:** Bir sanat eserinin sadece nihai sonucunu değil, tüm **yaratım sürecini (process)** teknik verilerle doğrulayan ana protokoldür.  
* **Çözdüğü Sorun:** Üretken yapay zeka (Generative AI) araçlarının artışıyla birlikte, gerçek insan emeğinin dijital ortamda kanıtlanamaz hale gelmesi ve sanatın “meta” değerinin düşmesi.  
* **Nasıl Çalışır?** Sanatçı, eseri oluştururken her aşamayı kapsayan **Evidence Pack** (Kanıt Paketi) verilerini sisteme sunar. Protokol, bu verileri zaman damgalı olarak blokzincir üzerinde mühürler.  
* **Örnek Senaryo:** Bir sanatçı 40 saatlik bir impasto tablo yapıyorsa, bu 40 saatin yayın logları, fırça darbelerinin timelapse kayıtları ve dijital parmak izleri [PoArt] filtresinden geçer. Sadece “bitmiş resim” değil, o resmin arkasındaki “40 saatlik insan emeği” tescillenir.

---

### **[FPP] Foundational Pillar Protocol (v1.0)**
* **Tanım:** Ekosistemin ekonomik, yönetimsel ve toplumsal “taşıyıcı kolonlarını” (pillars) inşa eden; sadakati, sürekliliği ve uzun vadeli katılımı ödüllendiren ana sistemdir.  
* **Çözdüğü Sorun:** Kripto ekosistemindeki “parayı basan düdüğü çalar” mantığının yarattığı adaletsizlik ve projeyi terk eden spekülatörlerin ekosisteme zarar vermesi.  
* **Nasıl Çalışır?** Kullanıcıların ekosistem içindeki karar verme ve yönetim ağırlığı, cüzdanlarındaki varlık miktarından ziyade, bu varlığı ne kadar “sağlam” (pillar) ve uzun süreli tuttuklarına göre belirlenir.  
* **Örnek Senaryo:** Sisteme bugün 1 milyon token ile giren bir “balina”, 1 yıldır sistemde 100 token tutan sadık bir “patron”dan daha düşük bir yönetim ağırlığına (voting power) sahip olabilir.

---

## 👥 2) Roles & Entities (Roller ve Varlıklar)

Bu protokol, “kim ne yapar, ne yapamaz?” sorusunu netleştirerek yanlış anlaşılmaları ve suistimali azaltır.

- **Artist (Sanatçı):** [PoArt] için Evidence Pack üretir, kayıt başlatır, yıllık yenileme için **Heartbeat Signature** imza atar.  
- **Patron (Hami / Destekçi):** [FPP] içinde süreklilik ve katkı ile statü kazanır; veto, denetim ve kürasyon süreçlerinde ağırlık taşır.  
- **Validator (Doğrulayıcı Topluluk):** Evidence Pack inceleme, tutarsızlık işaretleme, veto/itiraz süreçlerinde aktif rol alır.  
- **Digital Notary (Dijital Noter / Self-Executing Contract):** Kanıt + konsensüs + zaman damgasını deterministik şekilde doğrular ve Public Registry’ye mühürler.  
- **Public Registry (Kamu Arşivi):** “Onaylı kayıtların” kalıcı kimlik katmanı. Kayıt statüleri burada görünür (Verified/Legacy/Revoked vs).  
- **Evidence Storage (IPFS/Arweave/Archive):** Ham verinin saklandığı zincir dışı katman; zincire yalnızca kriptografik kökler yazılır.

---

## 📊 3) Economic & Governance Metrics (Ekonomik & Yönetişim Metrikleri)

Bu bölüm, ekosistemin sürdürülebilirliği ve yönetimde adaleti sağlamak için kullanılan temel matematiksel modelleri ve zaman tabanlı kısıtlamaları tanımlar.  
Amaç; sermaye ile anlık güç satın alma girişimlerini (**whale / flash-in / pump-dump / oy satın alma**) zaman sürtünmesi ile etkisizleştirirken, uzun vadeli sadakati ölçülebilir ve denetlenebilir hale getirmektir.

---

### 3.1) Time Windows (Zaman Pencereleri) ve “Epoch” Netliği

Bu protokolde **“epoch” terimi yalnızca Operational Epoch’u (7 gün)** ifade eder.  
Diğer zaman parametreleri, amaçları karışmaması için **Guard Window (30 gün)** ve **Integrity Cycle (365 gün)** olarak ayrı isimlerle tanımlanır.

> **Terminoloji Notu (v1.0):**  
> **Evidence Pack** kayıt/doğrulama/itiraz süreçlerinde kullanılan “heavy proof” paketidir.  
> **Heartbeat Signature** ise yalnızca **yıllık sahiplik/aktiflik yenilemesi** için kullanılan “light renewal” imzasıdır.

#### 3.1.1) Operational Epoch (Standart Operasyonel Döngü)
Yönetim raporlarının, doğrulama loglarının ve rutin skor güncellemelerinin çalıştığı temel periyottur.

- **Default Operational Epoch:** **7 Gün**  
- **Fonksiyon:** Rutin metrik güncellemeleri, kayıt/log akışları, periyodik raporlama.

#### 3.1.2) Critical Vote Guard Window (Kritik Oylama Koruma Penceresi)
Kritik oylamalarda, oylama gücünün hangi geçmiş zaman aralığına bakılarak hesaplanacağını belirleyen güvenlik penceresidir.

- **Critical Vote Guard Window (Lookback):** **30 Gün**  
- **Fonksiyon:** Oylama öncesi yapılan yüklü ve kısa vadeli sermaye girişlerini etkisizleştirir.

> **Kural Netliği:** Kritik oylamalarda oy gücü hesaplanırken **Operational Epoch (7 gün)** yerine **Guard Window (30 gün)** baz alınır.

#### 3.1.3) Integrity Cycle (365-Day Renewal)

- **Integrity Cycle:** **365 Gün**  
- **Fonksiyon:** Yıllık yenilemede (**Heartbeat Signature**) üzerinden doğrulama.  
> **v1.0 Varsayılanları:** 7 gün / 30 gün / 365 gün. Parametre değişimi yalnızca yönetişim kararı + sürüm etiketi ile yapılır.


---

### 3.2) TWAB (Time-Weighted Average Balance)

TWAB, bir cüzdanın belirli bir **sabit lookback penceresi (W)** boyunca tuttuğu bakiyenin **zaman-ağırlıklı ortalamasıdır**.

> **Kritik (v1.0):** TWAB hesabında payda, “cüzdanın aktif olduğu süre” değil, **sabit pencere uzunluğu W**’dur.  
> Böylece yeni giren bir adres “ilk dakikadan” tam TWAB’a ulaşamaz; TWAB, pencere doldukça doğal olarak yükselir.

Sürekli zaman formu:

$$
\text{TWAB}_{W}(t)=\frac{1}{W}\int_{t-W}^{t}\text{Balance}(\tau)\,d\tau
$$

Diskret (epoch bazlı) form:

$$
\text{TWAB}_{W}=\frac{\sum_{i=1}^{n}(\text{Balance}_i\times\Delta t_i)}{W}
\quad\text{ve}\quad
\sum \Delta t_i = W
$$

- Varsayılan pencereler (v1.0):
  - **Operational TWAB:** \(W=7\) gün
  - **Critical Vote TWAB:** \(W=30\) gün (Guard Window)
  - **Integrity TWAB:** \(W=365\) gün (Integrity Cycle)

**Opsiyonel ham alan metrik (birim: Token×Zaman):**

$$
\text{TWA}_{W}=\int_{t-W}^{t}\text{Balance}(\tau)\,d\tau
\approx \sum_{i=1}^{n}(\text{Balance}_i\times\Delta t_i)
$$


---

### 3.3) Voting Power (Oy Gücü)

$$
\text{VotingPower}=f(\text{TWAB},\text{TimeRules},\text{Tier})
$$

> **Normatif kural (v1.0):** Eğer adres `CooldownWindow` içindeyse (transfer sonrası 30 gün),
> `VotingPower` hesaplarında `TWAB_W` yerine `EffectiveTWAB_W` kullanılır.
> Aksi halde `EffectiveTWAB_W = TWAB_W` kabul edilir.


**Guard Window Etkisi:** kritik oylamada 30 günlük lookback kullanılır.

---

### 3.4) Logarithmic Power Scoring (Logaritmik Skorlama)

$$
\text{Score}_{W}=\log_{10}(\text{TWAB}_{W}+1)
$$

- Rutin metriklerde: \(W=7\) gün  
- Kritik oylamalarda: \(W=30\) gün (Guard Window)

$$
\text{VotingPower}=\text{Score}_{W}\times g(\text{TimeRules},\text{Tier})
$$


| Bakiye (TWAB) | Skor ($\log_{10}(\text{TWAB}+1)$) | Güç Analizi |
|:--|:--|:--|
| 10 | 1.04 | Başlangıç seviyesi etki |
| 1,000 | 3.00 | 100 kat varlık artışı → ~3 skor |
| 1,000,000 | 6.00 | 100 000 kat artış → ~6 skor |

> **Simülasyon:**  
> Gerçek zamanlı olarak logaritmik oy gücü hesaplamasını görmek veya kendi TWAB senaryonuzu test etmek için  
> [PoArt Simulation Console](https://galeri-coder.github.io/ilhanart-protocol/%5BPoArt%5D/) bağlantısına gidin.

---

### 3.5) FPP v1.0 Uyumluluğu

- **Operational Epoch:** 7 Gün  
- **Guard Window:** 30 Gün  
- **Integrity Cycle:** 365 Gün  

Her yıl (**Heartbeat Signature**) ile yenileme zorunludur.

---

## 🛡️ 4) Security & Validation (Güvenlik ve Doğrulama)

### 4.1) Foundational Vault (1-Year Lock Cycles)
* **Tanım:** Varlıkların **1 yıllık kilit döngüleri** ile tutulduğu, ekosistemin en üst düzey “itibar kasası”.  
* **Çözdüğü Sorun:** Kısa vadeli kâr hedefleyen spekülatörlerin 2025–3000 vizyona zarar vermesi.  
* **Cevap:** En kritik kararları yalnızca varlığını **1 yıl** kilitleyen ve [FPP] içinde “Foundational Pillar” statüsü kazanan kişiler verebilir.

> Not: Bu dokümanda “epoch” terimi yalnızca **Operational Epoch (7 gün)** için kullanılır. Vault kilitleri “Lock Cycle” olarak anılır.

---

### 4.2) Evidence Pack (Kanıt Paketi)

**Tanım:**  
Bir eserin [PoArt] tarafından onaylanması için gereken zorunlu teknik veri seti.

#### 4.2.A) Live Identity Proof (Algoritma Dışı İrade Kanıtı) — PoArt Güçlendirmesi *(Opsiyonel, ama güçlü)*

Bu modül, üretimin bir bot veya yapay zekâ simülasyonu değil, **gerçek bir insan iradesinden** doğduğunu kanıtlayan **canlılık doğrulaması + süreç odaklı** güçlendirme katmanıdır.

Bu modülü dökümantasyona ve sisteme şu teknik adımlarla entegre ediyoruz:

1) **Canlı Kimlik Katmanı (Live Identity Proof)**  
   Sürekli doğrulama: Sanatçı, üretim anında anonimlik maskesinin ardına saklanmak yerine, canlı stüdyo seansları aracılığıyla sürekli bir doğrulama katmanı sunar.  
   > **Üretim Çıpası:** Kimlik, nihai esere değil; üretim anının gerçekliğine ve fiziksel dünyadaki varlığa çıpalanır.

2) **Süreç ve Emek Kaydı (Labor & Process Proof)**  
   “Üretim sancısı”: Saniyeler içinde üretilen yapay zekâ çıktılarının aksine, teknik kararlar ve emek (fırça darbeleri, teknik metadata) kayıt altına alınır.  
   > **Zaman Kümülatifi:** Değer, bitmiş görselden ziyade, o görsele ulaşmak için harcanan kümülatif zamanda gizlidir.

3) **Kanıt Paketi (Evidence Pack) ve Mühürleme**  
   Video kayıtları, zaman damgaları ve teknik metadata bir araya getirilerek bir paket oluşturulur.  
   > **SHA-512 Bütünlüğü:** AllFiles hash’leri alınır → MerkleRoot üretilir → EvidenceRoot zincire yazılır.  
   > **Kamu Sicili:** Mühürlenen veriler Public Registry’ye işlenir; fiziksel varlık ile metadata senkronizasyonu sağlanır.

4) **İrade ve Anti-Sahtecilik Denetimi**  
   > **Algoritmik Olmayan İrade:** Otomasyonun kusursuzluğu yerine, insanın hata yapabilen ve risk alan özgün iradesi esas alınır.  
   > **Kırmızı Bayrak (Red Flag):** Sahtecilik/yanıltıcı beyan şüphesinde sistem “Red Flag” üretir ve statüyü incelemeye alır.

> **⚠️ Önemli Not:** Bu “Live Identity Proof” modülü bir rütbe değildir.  
> Yıllık sahiplik/aktiflik yenilemesi **Heartbeat Signature** ile yapılır ve 365 günlük döngüye tabidir.

#### Zorunlu İçerik (Trinity of Proof)
1. **Live Logs:** Üretim anındaki canlı yayın + platform/sunucu log uyumu  
2. **Process Timelapse:** İlk darbeden son hale kadar hızlandırılmış süreç videosu  
3. **Digital Fingerprint:** `SHA-512(EvidencePack)` hash’i + bu hash’in cüzdan tarafından imzalanmış hali (**SignerSignature**).


#### v1.0 Güçlendirmesi (Bütünlük Katmanı)
Trinity tek başına yetmez; aralarındaki bağ da mühürlenmelidir:

4. **Capture Manifest:**  
   Kamera/cihaz bilgisi, çözünürlük, kare sayısı, süre, dosya listesi, checksum’lar.

5. **Merkle Root / Hash Chain:**  

$$
\text{EvidenceRoot} = \text{MerkleRoot}(\text{AllFiles})
$$

Tüm kanıt dosyalarının tek kök değeri: zincire yazılan **“tek gerçek”**.

6. **Random Challenge Frames (Opsiyonel ama güçlü):**  
   Yayın sırasında rastgele anlarda düşük sürtünmeli “insan kanıtı” görevleri  
   (ör: belirli kartı göster, belirli kelimeyi yaz, belirli nesneyi kadraja al).  
   Bu, AI reenact / deepfake taklit maliyetini dramatik şekilde yükseltir.

---

**Çözdüğü Sorun:**  
“Bu eser gerçekten insan eliyle mi yapıldı?” sorusuna reddedilemez teknik yanıt.

---

### 4.3) Sybil & Flash-loan Protection
* **Tanım:** Bot hesap (Sybil) ve anlık kredi (Flash-loan) saldırılarına karşı matematiksel barikat.  
* **Cevap:** [FPP] içindeki TWAB + Guard Window, anlık sermaye hareketlerini “yönetim etkisi” açısından önemsizleştirir.

---

### 4.4) Digital Notary (Dijital Noter: Protokolün Sarsılmaz Mührü)

* **Tanım:** [PoArt] ve [FPP] verilerini teknik süzgeçten geçiren, doğruluğunu matematiksel olarak onaylayan ve nihai veriyi **Public Registry** üzerine geri dönülemez şekilde mühürleyen self-executing mekanizma.

#### Çözdüğü Sorunlar
1) **Merkezi Otorite ve Bias:** Subjektif “elit onayı” riskini azaltır.  
2) **Veri Manipülasyonu:** Onaylanmış kaydın geriye dönük değişmesini teknik olarak imkansızlaştırır.  
3) **Gatekeeping:** Sanatçının küresel arşive girişi “zevk” ile değil “kanıt” ile olur.

#### Doğrulama Döngüsü (Üçlü Filtre)
- **Evidence Pack Completeness:** Trinity + Manifest + EvidenceRoot  
- **Demokratik Denetim:** Quorum + Veto kurallarını aşmamak  
- **Kriptografik Doğrulama:** **SignerSignature** doğrulaması + **SHA-512** bütünlük kontrolü

#### VoterConsensusRoot (v1.0) — Oylama Konsensüs Kökü (Deterministik)

Bu bölümde geçen `VoterConsensusRoot`, oylamanın **sonuç özetini** ve **oy setini** tek bir köke bağlar.

**1) Vote Receipt (tek oy kaydı) — canonical bytes**

Önce imzasız gövde oluşturulur:

`VoteReceiptBody = (`
`ProposalRef || VoterId || VoteChoice || Weight || VoteTime`
`)`

Ardından oy veren, aşağıdaki mesajı imzalar:

- `SignerSignature = Sign( SHA-512( 0x01 || VoteReceiptBody ) )`

Son olarak kayıt bytes’ı:

`VoteReceiptBytes = (`
`VoteReceiptBody || SignerSignature`
`)`


**2) Vote leaf ve VoteSetRoot**
- `VoteLeaf = SHA-512( 0x00 || VoteReceiptBytes )`
- Tüm `VoteLeaf` değerleri **lexicographic** (byte-wise) sıralanır.
- `VoteSetRoot = MerkleRoot( sorted VoteLeaf list )` *(MerkleRoot, SHA-512 ile)*

**3) ConsensusEnvelope ve VoterConsensusRoot**
`ConsensusEnvelopeBytes = (`
`ProposalRef || SnapshotTime || YesWeight || NoWeight || AbstainWeight ||`
`QuorumWeight || VetoWeight || ResultCode || VoteSetRoot`
`)`

- `SnapshotTime`: `u64be`
- `YesWeight/NoWeight/AbstainWeight/QuorumWeight/VetoWeight`: `u128be`
- `ResultCode`: `u8` (0=Rejected, 1=Accepted, 2=Revoked, 3=Timeout)
- `VoteSetRoot`: 64-byte raw

`VoterConsensusRoot = SHA-512( ConsensusEnvelopeBytes )`

> Not: Bu dokümandaki tüm `||` birleştirmeleri **Canonical Encoding (v1.0)** kurallarıyla yapılır (bkz. Kriptografik Primitifler).


#### Matematiksel Onay Mührü
> Not: Bu dokümanda Hash(x) ifadesi SHA-512(x) anlamındadır.

> Not: `||` birleştirmesi **Canonical Encoding (v1.0)** kurallarına göre yapılır (bkz. Kriptografik Primitifler).

$$
\text{NotarySeal}=\text{SHA-512}\!\left(\text{EvidenceRoot}\,\|\,\text{VoterConsensusRoot}\,\|\,\text{TimeStamp}\right)
$$



#### Sonuç (2026–3000)
Dijital Noter mührünü alan eser, tekil bir kurumun malı olmaktan çıkar;  
insanlığın uzun vadeli kültürel mirasının bir parçası haline gelir.  
Mühür; “kim, ne zaman, hangi emekle” sorusunu yüzyıllar sonra bile doğrulanabilir kılar.

---

## 💾 5) Validation & Persistence (Doğrulama ve Süreklilik)

### 5.1) 365 Günlük Kesintisiz Cold Wallet Doğrulaması

**Tanım:**  
Varlığın cold wallet’ta (Ledger/Trezor vb.) 365 gün boyunca **istikrarlı** tutulması.

**Çözdüğü Sorunlar:**
1. Wash Trading  
2. Spekülatif baskı  
3. Sıcak cüzdan güvenlik zafiyeti  

---

#### v1.0 Güncellemesi: “Hard Reset” yerine “Penalty Ladder”

> **Netlik (v1.0): Penalty Ladder neyi etkiler?**

>**Strike sayımı (v1.0):**
- `StrikeCount`, son **365 gün** içinde gerçekleşen cold-wallet bütünlük ihlallerinin sayısıdır.
- Her yeni ihlal `StrikeCount = StrikeCount + 1` yapar.
- Eğer adres **365 gün** boyunca yeni ihlal yapmazsa `StrikeCount` sıfırlanır.
- `StrikeCount ≥ 3` olduğunda statü **Revoked** olur.

> Cold-wallet bütünlüğü bozulduğunda iki ayrı şey vardır:
> 1) **HoldingDays** doğal olarak sıfırlanır (zaman bileşeni kaybolur).
> 2) **Penalty Ladder**, bunun üstüne “kalıcı” ikinci bir ceza bindirmemek için yalnızca
>    **kısa süreli bir cooldown penceresinde** oy gücü / skor hesaplarında uygulanır.
>
> Bu nedenle v1.0’da Penalty çarpanı:
> - **VotingPower** hesaplarında kullanılan `TWAB_{30d}` için,
> - ve **Pts** içindeki `log10(TWAB_{30d}+1)` bileşeni için
> **CooldownWindow = 30 gün** boyunca uygulanır.

>
> HoldingDays zaten sıfırlandığı için, Penalty’nin “kalıcı” olması **double slashing** yaratır.
> v1.0 standardı: **Penalti geçici, HoldingDays sıfırlaması kalıcıdır.**
- Uygulama kuralı: Transfer olayından sonra `CooldownWindow` süresi bitince `EffectiveTWAB_{30d} = TWAB_{30d}` olur.



Tek transfer ile her şeyi sıfırlamak çok güçlü ama insan hatasını da yakabilir.  
Bu yüzden v1.0’da sistem hem sert hem yaşanabilir olmalı:

**1. İhlal (365 dolmadan transfer):** *(CooldownWindow = 30 gün boyunca)*

$$
\text{EffectiveTWAB}_{30d} = \text{TWAB}_{30d} \times 0.20
$$

**2. İhlal:** *(CooldownWindow = 30 gün boyunca)*

$$
\text{EffectiveTWAB}_{30d} = \text{TWAB}_{30d} \times 0.05
$$

**3. İhlal:**  
Statü **Revoked** (iptal).

> Bu merdiven: gerçek kullanıcıyı tamamen yakmadan “hızlı gir-çık” manipülasyonunu ekonomik olarak anlamsızlaştırır.

---

#### Güvenli Taşıma İstisnası (Move Permit, Time-Lock)

Cüzdan taşıma veya güvenlik upgrade gibi durumlar için:

- **Move Permit** talebi açılır  
- Kısa bir **time-lock** uygulanır  
- Topluluk denetimi (Quorum + Veto) devrededir  
- Zincire yalnızca “permit” kaydı ve yeni adres bağlanması yazılır

---

### 5.2) Evidence Pack: Zorunlu Trinity + Bütünlük Katmanı

#### Zorunlu İçerik (Trinity of Proof)
1) **Live Logs:** Canlı yayın + platform/sunucu log uyumu  
2) **Process Timelapse:** Sürecin baştan sona hızlandırılmış kaydı  
3) **Digital Fingerprint:** `SHA-512(EvidencePack)` hash’i + bu hash’in cüzdan tarafından imzalanmış hali (**SignerSignature**).

#### Bütünlük Katmanı (Trinity’yi güçlendirir)
- **Capture Manifest** + **Technical Logs** + **EvidenceRoot**
$$
\text{EvidenceRoot}=\text{MerkleRoot}(\text{AllFiles})
$$

* **Çözdüğü Sorun:** AI taklidinin saniyeler içinde “sonuç” üretmesine karşı, insan emeğinin “süreç” kanıtını korur.

---

### 5.3) Yıllık Yenileme Zorunluluğu (365-Day Heartbeat)
* **Tanım:** Public Registry’deki her kaydın “aktif ve sahipli” kaldığını gösteren yıllık imza (**Heartbeat Signature**).  
* **Çözdüğü Sorunlar:** Ölü veri, terk edilmiş cüzdanlar, pasif koleksiyonculuk.

* **Nasıl Çalışır?**
  - Her kaydın **Valid Until** tarihi vardır.  
  - Süre dolmadan **30 gün önce** uyarı.  
  - Sahip, yeni imza ile “hala bende ve standartlara uyuyor” der.  
  - Aksi halde kayıt **Legacy Archive** statüsüne iner.

> Opsiyonel hızlandırma: Eğer proje “yıllık arşiv + düzenli denetim” altyapısına daha önceden sahipse **365 günden 30 güne** teknik olarak indirilebilir.  
> v1.0 varsayılanı 365 gündür.

- **Heartbeat Light Proof (v1.0 — opsiyonel ama önerilir):**
  - Sahip, Heartbeat Signature ile birlikte küçük bir “durum kanıtı” üretir:
    - `StateDigest = SHA-512( 0x48 || RecordId || TimeStamp || PhotoHash || NoteHash )`
  - `PhotoHash/NoteHash` zincire ham veri olarak yazılmaz; yalnızca hash yazılır (off-chain saklanır).
  - Amaç: Heartbeat’i “sadece imza” olmaktan çıkarıp **Proof of Existence** seviyesine taşımak.


---

## 🗳️ 6) Decentralized Supervision (Merkeziyetsiz Denetim)

### 6.1) Topluluk Veto Mekanizması (Quorum + Veto Çift Kilit)
* **Tanım:** Yeni kayıt veya protokol değişikliğinin, nitelikli azınlık tarafından durdurulabilmesini sağlayan demokratik güvenlik bariyeri.

**v1.0 Kuralı (Matematiksel olarak çalışır):**
- **Quorum (Minimum Katılım):** Katılan oy ağırlığı ≥ toplam aktif oy ağırlığının **%25’i**  
- **Veto Threshold:** Quorum sağlandıktan sonra, **katılan oy ağırlığının %40’ı** “veto” verirse öneri reddedilir.

* **Çözdüğü Sorunlar:**
  1) Sybil Attacks  
  2) Collusion (anlaşmalı oylama)  
  3) Bribery (rüşvetle oylama satın alma)

* **Örnek Senaryo:** AI ile üretilmiş bir görsel, “emeğim” diye başvurur.  
Evidence Pack tutarsızdır. Topluluk, logaritmik skorlama ve TWAB etkisi ile veto barajını geçerse kayıt asla mühürlenemez.

---

### 6.2) Emergency Governance / Fallback Council *(Ek Madde)*



**Amaç:** Katılım oranı düşük olduğunda yönetişimin tıkanmasını (*decision deadlock*) önlemek.

$$
\text{Deadlock}=(\text{QuorumNotMet})\land(\text{ProposalTimeout}>7\text{ days})
$$

Durum `Deadlock = TRUE` olduğunda:

1. **Fallback Council**, aşağıdaki hiyerarşik seçimle kurulur:
   - (A) Eğer **Rank-III** havuzunda yeterli üye varsa: Rank-III ilk %10 (Pts’e göre)
   - (B) Eğer Rank-III **boş** veya yetersizse: mevcut **en yüksek Rank-II** ilk %10 (Pts’e göre)
   - (C) Eğer Rank-II de yetersizse: **Validator** havuzunda “minimum stake + minimum katılım” şartını geçen ilk %N


Bu mekanizma, demokratik karar ilkesini bozmadan sistemin operasyonel sürekliliğini garanti eder.

2. **Konsey kararı,** `CouncilConsensus ≥ ⅔` oranıyla alınır.  
3. İlk fırsatta (≥30 gün) topluluk referandumu ile onaylanmazsa **otomatik** feshedilir.  
4. Tüm karar kayıtları **`Emergency Ledger`** üzerinde SHA-512 hash’iyle mühürlenir.

---

## ⚙️ 7) The Michelangelo Framework (Meritocracy Engine)

### 7.1) Michelangelo // The Meritocracy Philosophy
* **Tanım:** Ekosistemin sıralama ve itibar motoru. “Zenginler listesi”ne dönüşmeyi engelleyen liyakat tabanlı hiyerarşi.  
* **Slogan:** *“You cannot buy your way to the top.”*  
* **Örnek:** Milyonlarca dolarlık balina, sadece para koyduğu için 1 numara olamaz. Zirve; yıllarca kültürel katkı sunanlara aittir.

### 7.2) Status Formula: Time × Contribution
$$
\text{Status}=\text{HoldingTime}\times\text{CulturalContribution}
$$

* **HoldingTime:** cold wallet’ta bozulmadan duran gün sayısı (örn. 1420 gün)  
* **CulturalContribution:** çeviri, kürasyon, altyapı, sergi desteği vb. somut katkı  
* **Çözdüğü Sorun:** Sadece token tutmanın pasif bir eylem olması. Sistem “hem tutan hem üreten”i ödüllendirir.

---

## 📊 8) Cultural Multipliers & Ranking Levels

### 8.1) Cultural Multiplier (Kültürel Çarpanlar)
* **Tanım:** Final skora eklenen bonus sistem.  
* **Uygulama Alanları:**
  - **JP/TR/EN büyük çeviri (örnek):** bilim/felsefe/sanat metinleri (+4,500 Pts örnek)  
  - **Denetim/Kalite:** registry kalite kontrol + veto katılımı  
  - **Infrastructure:** kod, dokümantasyon, indexer katkısı  

* **Örnek:** 1000 gün holding + 1 büyük çeviri = sıralamada binlerce kişiyi geçebilir.

### 8.2) Rütbe Sınıfları (Pts Bazlı Rank)

### 8.X) Pts (v1.0) — Rank Skoru (Log + Time + Cultural)

Pts, sermaye dominasyonunu engellemek için **logaritmik** ve **zaman bileşenli** tanımlanır:

$$
\text{Pts}=
\Big\lfloor
\alpha\cdot\log_{10}(\text{TWAB}_{30d}+1)
+\beta\cdot\log_{10}(\text{HoldingDays}+1)
\Big\rfloor
+\text{CulturalPts}
+\text{GovernancePts}
$$

> **Normatif kural (v1.0):** `CooldownWindow` sırasında Pts içindeki
> `log10(TWAB_{30d}+1)` bileşeni `log10(EffectiveTWAB_{30d}+1)` olarak hesaplanır.


- Varsayılan katsayılar (v1.0):
  - \(\alpha = 10{,}000\)
  - \(\beta = 10{,}000\)

- `HoldingDays`: **kesintisiz** cold-wallet doğrulamasının bozulmadığı gün sayısı  
  (Move Permit ile taşınan durumlar “kesinti” sayılmaz).

Bu yapı ile:
- Büyük bakiye **Pts’i** artırır ama **logaritmik** sınır içinde kalır.
- Uzun süreli sadakat (HoldingDays) Pts’e gerçek ağırlık ekler.
- CulturalPts/GovernancePts, “emek > sermaye” ilkesini pratikte taşır.


| Rütbe | Aralık / Puan | Rol & Yetkiler |
|:--|:--|:--|
| **Rank-III (≥100k Pts)** | Anayasal Düzey | Strateji, fee, ve uzun vadeli yön belirleme |
| **Rank-II (50k–99k Pts)** | Küratoryal Düzey | Denetim, kürasyon, oylama koordinasyonu |
| **Rank-I (<50k Pts)** | Üye Düzeyi | Öneri sunma ve küçük karar süreçlerine katılım |

> Rütbeler, [FPP] çerçevesinde katkı akışı ve zamansal düşüş oranına göre dinamik biçimde güncellenir.  
> **Kural:** Statik değil. Katkı bırakılırsa veya istikrar bozulursa rütbe düşer.

---

## 📈 9) Cut-off Thresholds & Network Metrics

### 9.1) Entry Thresholds (Giriş Barajları)
Eşikler “stable” olduğunda tek olmalı:

- **Rank-III Threshold:** **≥ 100,000 Pts**  
- **Top 100 Entry:** **≥ 45,000 Pts**

* **Çözdüğü Sorun:** Sistem kalabalıklaşıp kalitesizleşmesin. Zirveye giden yol matematiksel bariyerle korunur.

### 9.2) Network TWAB (Global Zaman Ağırlığı)
* **Tanım:** Ekosistemin toplam TWAB kapasitesi. (Örn: 4.2M Network TWAB)  
* **Fonksiyonu:** Bu rakam yükseldikçe sistem manipüle edilemez hale gelir.  
* **24h New Entries:** Son 24 saatte sisteme giren yeni [PoArt] kayıt akışı.

---

## 🎨 10) Intellectual Framework (Entelektüel Yapı)

### 10.1) IPOW: Intellectual Proof of Work (Emek Stake Etme)
* **Tanım:** Para tutmanın ötesinde yüksek nitelikli insan emeği (çeviri, sanat, eğitim, teknik) gerektiren itibar motoru.  
* **Çözdüğü Sorun:** “Pasif stake” kültürü.  
* **Örnek:** 1M token tutup katkı yapmayan bir adres, 100 token tutup döküman çeviren bir emekçi tarafından yönetimde geriye düşebilir.

### 10.2) Intellectual Honesty Filter (Entelektüel Dürüstlük)
* **Tanım:** Claim veya kritik oylamalarda, kullanıcının konuyu anlayıp anlamadığını ölçen aşama.  
* **Çözdüğü Sorunlar:** copy-paste oylama, AI spam, “neyi oyladığını bilmeden” evet/hayır.

#### v1.0 Güncellemesi: Quiz yerine “Anlama Kanıtı” (Erişilebilir)
Klasik quiz, dil ve erişilebilirlik açısından kullanıcıyı yakabilir. Bu yüzden:

**Seçenek A (Kısa Özet):** 100 kelime ile öneriyi özetle  
**Seçenek B (Risk Seçimi):** 2 risk işaretle + 1 gerekçe yaz  
**Seçenek C (İtiraz Girdisi):** Varsa 1 itiraz gerekçesi sun  

Bu modüller, “ezberi” değil “anlamayı” ölçer ve bot otomasyonunu zorlaştırır.

---

## 🛡️ 11) Advanced Sybil Resistance (Gelişmiş Saldırı Koruması)

### 11.1) The Turnstile Mechanism (Turnike Sistemi)
* **Tanım:** Ekosisteme giriş için minimum katılım eşiği (Örn: 250 ILHAN Token).  
* **Felsefe:** “Duvar değil, turnike.”  
* **Çözdüğü Sorun:** Milyonlarca boş cüzdan ile “zombi” doldurma.  
* **Örnek:** 10,000 sahte hesap açmak isteyen bot, her birinde 250 token tutmak zorunda kalınca saldırı ekonomik olarak verimsizleşir.

### 11.2) Zombie Wallet Filter (Aktif Claim Zorunluluğu)
* **Tanım:** Belirli periyotlarla cüzdanın “hayatta ve aktif” olduğunu kanıtlaması.  
* **Kural:** Aktif claim yapmayan adresler, skorları yüksek olsa bile Public Registry’den düşer.  
* **Amaç:** Sistem “yaşayan ve üreten” bireylerden oluşsun.

---

## 🧬 12) Generational Legacy & Governance (Nesiller Arası Miras & Yönetim)

### 12.1) Generational Legacy Transfer (Varis Mekanizması)
Impasto (Tier) statüsünü uzun süre koruyanların itibar ve haklarını varise devredebilmesi.  
* **Çözdüğü Sorun:** Bir kişinin ölümü/aktifliği yitirmesiyle kültürel değerin kaybolması.  
* **Uygulama:** Varis ekranı yalnızca 4 yıllık sadakati kanıtlayanlara açılır ve on-chain mühürlenir.

### 12.2) Parliamentary Governance Rights (Parlamenter Söz Hakkı)
1) **Rank-III (≥100k Pts):** anayasa, fee, strateji  
2) **Rank-II (50k–99k Pts):** kürasyon, denetim, oylamalar  
3) **Rank-I (<50k Pts):** öneriler, küçük ölçekli kararlar  

* **Çözdüğü Sorun:** Kaotik oylamalar yerine “liyakate dayalı demokrasi”.

---

## 🌍 13) Cultural Privilege Layers & Real-World Integration

> Not: Bu bölümdeki ayrıcalıklar, 2026–2030 kapsamında kademeli uygulanacak “Future Roadmap” bileşenleridir.

### 13.1) The Annual Exhibition Right (Yıllık Galeri Hakkı)
* **Tanım:** [PoArt] doğrulanmış yüksek skorlu sanatçı/patronların İlhan Art Gallery’de yılda 1 kez, 1 hafta sergileme hakkı.  
* **Çözdüğü Sorun:** Bağımsız sanatçının fiziksel alana erişim maliyeti.  
* **Nasıl Çalışır?** Threshold geçenler takvim üzerinden rezervasyon yapar; galeri “itibar puanları” ile kullanılır.

### 13.2) Dinamik Sanat Fiyatlandırması (JSON Bağlantılı İndirimler)
* **Tanım:** Kültürel statüye göre indirim oranını belirleyen dinamik fiyatlandırma API’si.  
* **Yapı:**  
  - **Rank-III (≥100k Pts)** → %50+ indirim  
  - **Rank-II (50k–99k Pts)** → %30 indirim  
  - **Rank-I (<50k Pts)** → %10 indirim  
* **Felsefe:** “Pazarlık yok — yalnızca doğrulanmış emek değer belirler.”  
* **Amaç:** Kültürel katkıyı ödüllendirirken, algoritmik şeffaflık ve adalet sağlamak.

### 13.3) Physical Ecosystem Integration (Partner Entegrasyonu)
- Kitabevleri, kafeler, kültür merkezleri  
- QR ile statü okuma, claimable codes

### 13.4) Labor Over Capital: Meritocratic Access (Emek > Sermaye)

**Tanım:**  
Sistemde gerçek ayrıcalık, salt sermaye miktarına değil; kültürel katkı + zaman istikrarına göre tanımlanır.

**Matematiksel Model:**

$$
\text{ClaimRight} \propto \text{CulturalScore} + \log_{10}(\text{Balance})
$$

Yani, bir kullanıcının “hak kazanımı” kültürel emeğiyle birlikte artar;  
varlık miktarı ise yalnızca logaritmik katkı sağlar — böylece **emek**, **sermayeden** baskın hale gelir.

**Örnek:**  
250 token tutup yoğun katkı üreten biri,  
100 000 token tutup pasif kalan birinden daha fazla avantaja sahip olabilir.

---

## 🧩 14) State Machine (Kayıt Yaşam Döngüsü)

Bir [PoArt] kaydı ve [FPP] statüsü aşağıdaki deterministik akıştan geçer:

1) **Draft** (hazırlık)  
2) **Submitted** (başvuru)  
3) **Under Review** (inceleme)  
4) **Challenged** (itiraz açıldı)  
5) **Verified** (NotarySeal basıldı)  
6) **Renew Due** (Heartbeat zamanı yaklaştı)  
7) **Legacy Archive** (yenilenmedi, pasif arşiv)  
8) **Revoked** (ihlal/kanıt çökmesi/veto/çoklu ihlal)

> Bu akış; “ne zaman hangi statüdeyim?” sorusunu tek bakışta çözer.

---

## 🔗 15) Minimal On-chain / Maximal Off-chain

### Zincir Üstüne (On-chain) Yazılanlar
- EvidenceRoot (Merkle Root)  
- NotarySeal  
- TimeStamp  
- Signer (artist/owner)  
- Status (Verified/Legacy/Revoked)  
- Permit Records (Move Permit gibi istisnalar)

### Zincir Dışında (Off-chain) Tutulanlar
- Ham video dosyaları  
- Timelapse  
- Teknik log dosyaları  
- Manifest detayları  
- Büyük arşiv setleri (IPFS/Arweave)

**Amaç:** Zinciri şişirmeden, doğrulanabilirliği maksimum yapmak.

---

## 🏛️ 16) Appeals / Mercii & İtiraz Mekanizması (Kurumsal Güven Katmanı)

İtiraz mekanizması “güvenin kurumsal teminatıdır”.

- **Strategic Filter:** İtirazlar “kanıt tabanlı” olmalı (sadece duygu/iftira değil).  
- **Community Veto (v1.0):**  
  - **Quorum:** katılan ağırlık ≥ toplam aktif ağırlığın **%25’i**  
  - **Veto:** quorum sağlandıktan sonra, **katılan ağırlığın %40’ı** “veto” verirse öneri reddedilir.  
- **Anti-Bot / Anti-Sybil:** (uygulama katmanı) stake-gated doğrulama  
- **Evidence Pack Freezing:** İtiraz açıldığında ilgili kanıt paketi “freeze” olur (time-lock).  
- **Transparency / Time-Lock:** Her itiraz olayı kamuya açık zaman çizelgesinde görünür; ani sansür veya manipülasyon engellenir.

---

## 🧨 17) Threat Model (Saldırı Kataloğu ve Karşı Katmanlar)

| Tehdit | Karşı Katman |
|:--|:--|
| **Sybil Attack** | Turnstile + Zombie Filter + Quorum |
| **Flash-loan** | TWAB + Guard Window + Log Scoring |
| **Whale Domination** | Logarithmic Power Scoring + TWAB |
| **Wash Trading** | Cold Wallet Verification + Penalty Ladder |
| **Collusion** | Veto + Evidence Pack scrutiny + Transparency |
| **Data Tampering** | `NotarySeal = SHA-512(EvidenceRoot || VoterConsensusRoot || TimeStamp)` (EvidenceRoot = MerkleRoot(AllFiles)) |
| **Bribery / Vote Buying** | Time-lock + Quorum + Contribution-weighted Legitimacy |
| **Deepfake Process Forgery** | Random Challenge Frames + Manifest + Hash Chain |

---

## ⚖️ 18) Final Word: A Blueprint for Global Governance (Manifesto)

> **Vizyon Notu:** [FPP] ve [PoArt] tarafından inşa edilen bu matematiksel zırh, sadece bir sanat galerisini değil; yozlaşmış parlamenter sistemleri ve manipüle edilen seçimleri de iyileştirebilecek bir “yönetim modeli” sunar.

### 18.1) The End of Plotokrasi (Sermaye Despotizminin Sonu)
* **Tanım:** Plütokrasi — yönetimin en zengin azınlığın elinde olması.  
* **Protokolün Yanıtı:** Logaritmik skorlama ile paranın gücü sınıra çekilir; “zaman” ve “emek” otorite olur.  
* **Gerekçe:** Gelecek, cüzdanı şişkin olanın değil; entelektüel değer katanın elinde olmalıdır.

### 18.2) The Meritocratic Parliament (Liyakate Dayalı Parlamento)
Popülizm ve sermaye odaklı siyasetin yerine; dökümantasyonu özümsemiş, IPOW sunmuş liyakat sahiplerinin söz hakkı kazandığı bir yapı hedeflenir.

### 18.3) Security Against Vote Rigging (SHA-512 Seçim Güvencesi)
- **Turnstile:** bot manipülasyonunu ekonomik olarak boğar  
- **TWAB:** son dakika vatandaşlık/oy satın almayı etkisizleştirir  
- **Quorum + Veto:** azınlığın sesini ezdirmeden denetim sağlar

### 18.4) The Conclusion: Saving the Future (Geleceği Kurtarmak)
Bu sistem; hilenin değil kanıtlanmış emeğin, anlık heveslerin değil bin yıllık vizyonun kazandığı bir “yeni düzen” tasarımıdır.  
Yanlış yönetilmeye mahkum edilmiş bir toplumu kurtarmanın yolu; insan hatasını azaltan, matematiksel olarak adil olduğu ispatlanmış bir protokol mimarisi kurmaktır.

---

## 📅 19) Roadmap & Future Notes

Bu dökümantasyonda yer alan tüm maddeler, İlhan Art ekosisteminin 2026’dan 3000 yılına uzanan vizyonunun yapı taşlarıdır.  
Her sürüm güncellemesi (v1.1, v1.2 vb.) bu ayrıcalıkların teknik entegrasyon süreçlerini (API bağlantıları, fiziksel POS entegrasyonları vb.) içerecektir.

---

## 🔐 Hash Signature (v1.0 Hard-Locked)

- **Hash Primitive:** SHA-512

- **EvidenceRoot:** `MerkleRoot(AllFiles)` (SHA-512)
  - `EvidenceRoot` çıktısı **64-byte raw** digest’tir (hex string değil).

- **VoterConsensusRoot:** `SHA-512(ConsensusEnvelopeBytes)` (64-byte raw)
  - Detaylar: **🔐 Kriptografik Primitifler** ve **4.4 Digital Notary / VoterConsensusRoot** bölümüne bakınız.

- **NotarySeal (v1.0):**
  - `NotarySealBytes = EvidenceRoot || VoterConsensusRoot || TimeStamp`
  - Burada `||` birleştirmesi **Canonical Encoding (v1.0)** kurallarıyla yapılır:
    - `EvidenceRoot` = 64-byte raw (length prefix yok)
    - `VoterConsensusRoot` = 64-byte raw (length prefix yok)
    - `TimeStamp` = `u64be` (8 byte, UTC Unix seconds)
  - Matematiksel tanım:
    $$
    \text{NotarySeal}=\text{SHA-512}\!\left(\text{EvidenceRoot}\,\|\,\text{VoterConsensusRoot}\,\|\,\text{TimeStamp}\right)
    $$


