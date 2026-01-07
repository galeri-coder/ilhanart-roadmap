# 📜 Protocol Terminology & Technical Lexicon
> **Protocol Version:** 1.0 (Stable)  
> **Network Vision:** 2025 → 3000 Archive  
> **Ecosystem:** [PoArt] + [FPP]  
> **Status:** **HARD_LOCKED** (Active Documentation)  
> **Integrity:** SHA-512 Sealed (Digital Notary Compatible)

---

## İçindekiler
1. Pillars of the Protocol (Temel Protokoller)  
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
19. Roadmap & Future Notes (Yol Haritası Notu)

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

- **Artist (Sanatçı):**  
  [PoArt] için Evidence Pack üretir, kayıt başlatır, yıllık doğrulama (heartbeat) imzasını atar.

- **Patron (Hami / Destekçi):**  
  [FPP] içinde süreklilik ve katkı ile statü kazanır; veto, denetim ve kürasyon süreçlerinde ağırlık taşır.

- **Validator (Doğrulayıcı Topluluk):**  
  Evidence Pack inceleme, tutarsızlık işaretleme, veto/itiraz süreçlerinde aktif rol alır.

- **Digital Notary (Dijital Noter / Self-Executing Contract):**  
  Kanıt + konsensüs + zaman damgasını deterministik şekilde doğrular ve Public Registry’ye mühürler.

- **Public Registry (Kamu Arşivi):**  
  “Onaylı kayıtların” kalıcı kimlik katmanı. Kayıt statüleri burada görünür (Verified/Legacy/Revoked vs).

- **Evidence Storage (IPFS/Arweave/Archive):**  
  Ham verinin saklandığı zincir dışı katman; zincire yalnızca kriptografik kökler yazılır.

---

## 📊 3) Economic & Governance Metrics (Ekonomik & Yönetişim Metrikleri)

Bu bölüm, ekosistemin sürdürülebilirliği ve yönetimde adaleti sağlamak için kullanılan temel matematiksel modelleri ve zaman tabanlı kısıtlamaları tanımlar. Amaç; sermaye ile anlık güç satın alma girişimlerini (**whale / flash-in / pump-dump / oy satın alma**) zaman sürtünmesi ile etkisizleştirirken, uzun vadeli sadakati ölçülebilir ve denetlenebilir hale getirmektir.

---

### 3.1) Time Windows (Zaman Pencereleri) ve Epoch Tanımı

Bu protokolde zaman, tek bir “epoch” kelimesiyle değil; farklı amaçlara hizmet eden **üç ayrı pencere** ile tanımlanır. Böylece operasyonel ölçüm ile kritik oylama güvenliği birbirine karışmaz.

#### 3.1.1) Operational Epoch (Standart Operasyonel Döngü)

Yönetim raporlarının, doğrulama loglarının ve rutin skor güncellemelerinin çalıştığı temel periyottur.

- **Default Operational Epoch:** **7 Gün** (standart operasyonel döngü)
- **Fonksiyon:** Rutin metrik güncellemeleri, kayıt/log akışları, periyodik raporlama.

#### 3.1.2) Critical Vote Guard Window (Kritik Oylama Koruma Penceresi)

Kritik oylamalarda, oylama gücünün hangi geçmiş zaman aralığına bakılarak hesaplanacağını belirleyen güvenlik penceresidir.

- **Critical Vote Guard Window (Lookback):** **30 Gün**
- **Fonksiyon:** Oylama öncesi yapılan yüklü ve kısa vadeli sermaye girişlerini (oy satın alma girişimlerini) etkisizleştirir.

> **Kural Netliği (Önemli):**  
> Kritik oylamalarda oy gücü hesaplanırken **Operational Epoch (7 gün)** yerine **Guard Window (30 gün)** “lookback window” olarak baz alınır.  
> Yani kritik oylamada ölçüm penceresi **30 gündür**; **7 gün** sadece operasyonel raporlama döngüsüdür.

#### 3.1.3) Integrity Cycle (365-Day Renewal) ile İlişki

- **Integrity Cycle:** **365 Gün**
- **Fonksiyon:** Her yıllık yenileme döneminde (365-Day Renewal) metriklerin kanıtları (Evidence Pack) üzerinden doğrulanması zorunludur. Bu bir “hesaplama penceresi” değil; doğrulama ve denetim döngüsüdür.

> **⚠️ v1.0 Değişmezlik Notu (Hard-Coded / Parametreleme)**  
> - v1.0’da **Operational Epoch = 7 gün** ve **Guard Window = 30 gün** **hard-coded** kabul edilir (v1.0 içinde değişmez).  
> - Gelecekte “parametrelenebilir” ifadesi, v1.0 içinde anlık ayarlanabilirlik anlamına gelmez; yalnızca protokol sürüm yükseltmesi (ör. v1.1+) ve buna bağlı yönetişim onayı ile mümkün olacak bir değişiklik sınıfını ifade eder.

---

### 3.2) TWAB (Time-Weighted Average Balance)

TWAB, bir cüzdanın ekosistem içindeki **"sadakat"** ve **"istikrar"** katsayısını hesaplayan temel metriktir. Sadece bakiye miktarını değil, bu varlığa ne kadar süre sahip çıkıldığını ölçer.

**Hangi pencerede hesaplanır?**
- Rutin raporlarda TWAB, **Operational Epoch (7 gün)** boyunca hesaplanabilir.
- Kritik oylamalarda TWAB, **Critical Vote Guard Window (30 gün)** boyunca hesaplanır (lookback).

#### 3.2.1) Matematiksel Model (Normalize Edilmiş Ortalama)

Bir zaman penceresi içindeki ortalama sadakat puanı şu formülle hesaplanır:

$$
\text{TWAB} = \frac{\sum_{i=1}^{n} (\text{Bakiye}_i \times \Delta t_i)}{\sum_{i=1}^{n} \Delta t_i}
$$

- Burada $\Delta t_i$ ilgili bakiyenin taşındığı süreyi temsil eder.
- Bu formül, “anlık bakiye” yerine “zaman ağırlıklı denge” üretir.

#### 3.2.2) Ham Alan Metrik (TWA - Opsiyonel)

Bazı özel skorlama motorlarında "ortalama" yerine kümülatif bakiye-zaman alanı (integral) kullanılır:

$$
\text{TWA} = \sum_{i=1}^{n} (\text{Bakiye}_i \times \Delta t_i)
$$

- **Not:** TWA, normalize edilmemiş “alan” metriğidir. Aynı pencere için TWAB ile birlikte ya da alternatif motorlarda tek başına kullanılabilir.

**Çözülen Sorun:** **Whale Manipulation (Balina Manipülasyonu).**  
Oylama duyurulduğu an yüklü alım yapıp, oylama biter bitmez satış yapan (*pump-dump*) aktörlerin gücü, zaman sürtünmesi ile nötralize edilir.

---

### 3.3) Voting Power (Oy Gücü) Tanımı

Sistemde oy gücü, sadece cüzdan bakiyesine değil; zamana, kurallara ve kullanıcı statüsüne bağlı bir fonksiyondur:

$$
\text{VotingPower} = f(\text{TWAB}, \text{EpochRules}, \text{StatusTier})
$$

Bu dokümanın amacı, $f(\cdot)$ fonksiyonunun en kritik iki bileşenini standartlaştırmaktır:

1. **Zaman tabanlı ölçüm (TWAB + Guard Window)**
2. **Gücün yoğunlaşmasını engelleme (logaritmik skorlama)**

#### 3.3.1) Guard Window Etkisi (Kural Netliği)

Kritik oylamalarda:
- $\text{TWAB}$ hesaplaması **30 günlük Guard Window** üzerinden yapılır.
- Böylece oylamadan hemen önce yapılan alımlar, pencerenin çok küçük bir kısmını temsil ettiği için oy gücüne etkisi yakınsayan şekilde azalır.

**Örnek Senaryo (Mantıksal Kıyas):**
- **A Kullanıcısı:** 1.000.000 tokenı oylamadan 1 saat önce aldı.  
  (Kritik oylama ölçümü 30 gün lookback ile yapıldığı için, 1 saatlik katkı toplam pencerenin çok küçük kısmıdır; etkisi ihmal edilebilir düzeye iner.)
- **B Kullanıcısı:** 100 tokenı 365 gündür soğuk cüzdanda (Cold Wallet) tutuyor.  
  (Kritik oylamada son 30 günün TWAB’ı istikrarlı ve tam taşındığı için etkisi yüksek olur. Ayrıca yıllık Integrity Cycle doğrulamasında B’nin sürekliliği Evidence Pack ile desteklenir.)

**Sonuç:** Matematiksel model, B kullanıcısının uzun vadeli sadakatini, A kullanıcısının son dakika sermaye üstünlüğüne tercih eder.

---

### 3.4) Logarithmic Power Scoring (Logaritmik Skorlama)

Sermayenin yönetimde doğrusal (lineer) bir güç kazanmasını engelleyen adalet mekanizmasıdır. Güç artışını azalarak artan (logaritmik) bir eğriye oturtarak topluluğun sesini korur.

#### 3.4.1) Matematiksel Model

Kullanıcının yönetim ağırlığına temel olan skor şu formülle hesaplanır:

$$
\text{Score} = \log_{10}(\text{TWAB} + 1)
$$

> **Bağlayıcı Not (Tutarlılık):**  
> Bu dokümanda $\text{Score}$, 3.3’teki $\text{VotingPower}$ fonksiyonunun çekirdek bileşeni olarak kabul edilir.  
> Pratikte tipik bir birleşim şu mantığa oturur:

$$
\text{VotingPower} = \text{Score} \times g(\text{EpochRules}, \text{StatusTier})
$$

Burada $g(\cdot)$; statü tier çarpanları, oylama türüne özel filtreler ve guard kuralları gibi protokol kurallarını temsil eder.

#### 3.4.2) Adalet Notu (Neden Logaritmik?)

Bu model, **Kapitalist Güç Yoğunlaşmasını (Plutokrasi)** engellemek için tasarlanmıştır. Dev varlıkların topluluğun sesini boğmasını sınırlar ve küçük seslerin birleşerek denge kurmasına izin verir.

| Bakiye (TWAB) | Skor ($\log_{10}$) | Güç Analizi |
| :--- | :--- | :--- |
| 10 | 1.04 | Başlangıç seviyesi etki. |
| 1,000 | 3.00 | 100 kat varlık artışına karşılık ~3 seviyelik skor. |
| 1,000,000 | 6.00 | 100.000 kat varlık artışına karşılık ~6 seviyelik skor. |

**Özet:** Bir kişi diğerinden 100.000 kat daha zengin olsa bile, yönetimde 100.000 kat daha güçlü olamaz.

---

### 3.5) FPP v1.0 Uyumluluğu

Bu metrikler, **Foundational Pillar Protocol (FPP)** v1.0 standartlarına göre v1.0 içinde **“değişmez”** kabul edilir:

- **Operational Epoch:** 7 Gün
- **Critical Vote Guard Window:** 30 Gün
- **Integrity Cycle / 365-Day Renewal:** her yıl kanıt bazlı doğrulama

Her yıllık yenileme (365-Day Renewal) döneminde bu metriklerin kanıtları (Evidence Pack) üzerinden doğrulama yapılması zorunludur. Bu doğrulama; manipülasyon risklerini azaltır, metriklerin tutarlılığını korur ve sistemin uzun vadeli güvenilirliğini kurumsallaştırır.


## 🛡️ 4) Security & Validation (Güvenlik ve Doğrulama)

### 4.1) Millennium Vault (10-Year Epochs)
* **Tanım:** Varlıkların 1 yıllık periyotlarla (Epoch) kilitlendiği, ekosistemin en üst düzey “itibar kasası”.  
* **Çözdüğü Sorun:** Kısa vadeli kâr hedefleyen spekülatörlerin 2025–3000 vizyona zarar vermesi.  
* **Cevap:** En kritik kararları yalnızca varlığını 10 yıl kilitleyen ve [FPP] içinde “Foundational Pillar” statüsü kazanan kişiler verebilir.

---

### 4.2) Evidence Pack (Kanıt Paketi)
* **Tanım:** Bir eserin [PoArt] tarafından onaylanması için gereken zorunlu teknik veri seti.

#### Zorunlu İçerik (Trinity of Proof)
1) **Live Logs:** Üretim anındaki 7/24 canlı yayın ve sunucu kayıtları  
2) **Process Timelapse:** İlk darbeden son hale kadar hızlandırılmış süreç videosu  
3) **Digital Fingerprint:** Sanatçının cüzdanıyla imzalanmış hash (manipülasyon yok kanıtı)

#### v1.0 Güçlendirmesi (Zincirleme Bütünlük Katmanı)
Trinity tek başına yetmez; aralarındaki bağ da mühürlenmelidir:
4) **Capture Manifest (Manifesto):**  
   Kamera/cihaz bilgisi, çözünürlük, kare sayısı, süre, dosya listesi, checksum’lar.
5) **Merkle Root / Hash Chain:**  
\[
\text{EvidenceRoot} = \text{MerkleRoot}(\text{AllFiles})
\]
   Tüm kanıt dosyalarının tek kök değeri: zincire yazılan “tek gerçek”.
6) **Random Challenge Frames (Opsiyonel ama güçlü):**  
   Yayın sırasında rastgele anlarda düşük sürtünmeli “insan kanıtı” görevleri  
   (ör: belirli kartı göster, belirli kelimeyi yaz, belirli nesneyi kadraja al).  
   Bu, AI reenact / deepfake taklit maliyetini dramatik şekilde yükseltir.

* **Çözdüğü Sorun:** “Bu eser gerçekten insan eliyle mi yapıldı?” sorusuna reddedilemez teknik yanıt.

---

### 4.3) Sybil & Flash-loan Protection
* **Tanım:** Bot hesap (Sybil) ve anlık kredi (Flash-loan) saldırılarına karşı matematiksel barikat.  
* **Cevap:** [FPP] içindeki TWAB + Guard Window, anlık sermaye hareketlerini “yönetim etkisi” açısından önemsizleştirir.

---

## 💾 4.4) Digital Notary (Dijital Noter: Protokolün Sarsılmaz Mührü)
* **Tanım:** [PoArt] ve [FPP] verilerini teknik süzgeçten geçiren, doğruluğunu matematiksel olarak onaylayan ve nihai veriyi **Public Registry** üzerine geri dönülemez şekilde mühürleyen self-executing mekanizma.

### Çözdüğü Sorunlar
1) **Merkezi Otorite ve Bias:** Subjektif “elit onayı” riskini azaltır.  
2) **Veri Manipülasyonu:** Onaylanmış kaydın geriye dönük değişmesini teknik olarak imkansızlaştırır.  
3) **Gatekeeping:** Sanatçının küresel arşive girişi “zevk” ile değil “kanıt” ile olur.

### Doğrulama Döngüsü (Üçlü Filtre)
- **Evidence Pack Completeness:** Trinity + Manifest + EvidenceRoot  
- **Demokratik Denetim:** Veto/Quorum kurallarını aşmamak  
- **Kriptografik İmza:** SHA-512 imza doğrulaması

### Matematiksel Onay Mührü
\[
\text{NotarySeal} = \text{Hash}(\text{EvidenceRoot} + \text{VoterConsensus} + \text{TimeStamp})
\]

### Sonuç (2026–3000)
Dijital Noter mührünü alan eser, tekil bir kurumun malı olmaktan çıkar; insanlığın uzun vadeli kültürel mirasının bir parçası haline gelir. Mühür; “kim, ne zaman, hangi emekle” sorusunu yüzyıllar sonra bile doğrulanabilir kılar.

---

## 🏛️ 5) Validation & Persistence (Doğrulama ve Süreklilik)

### 5.1) 365 Günlük Kesintisiz Cold Wallet Doğrulaması
* **Tanım:** Varlığın cold wallet’ta (Ledger/Trezor vb.) 365 gün boyunca **istikrarlı** tutulması.

* **Çözdüğü Sorunlar:**
  1) Wash Trading  
  2) Spekülatif baskı  
  3) Sıcak cüzdan güvenlik zafiyeti

#### v1.0 Güncellemesi: “Hard Reset” yerine “Penalty Ladder”
Tek transfer ile her şeyi sıfırlamak çok güçlü ama insan hatasını da yakabilir. Bu yüzden v1.0’da sistem hem sert hem yaşanabilir olmalı:

- **1. İhlal (365 dolmadan transfer):**  
  TWAB tamamen silinmez, ama yönetim etkisi **Penalty Multiplier** ile düşer:  
\[
\text{EffectiveTWAB} = \text{TWAB} \times 0.20
\]

- **2. İhlal:**  
\[
\text{EffectiveTWAB} = \text{TWAB} \times 0.05
\]

- **3. İhlal:**  
  Statü **Revoked** (iptal).

> Bu merdiven: gerçek kullanıcıyı tamamen yakmadan “hızlı gir-çık” manipülasyonunu ekonomik olarak anlamsızlaştırır.

#### Güvenli Taşıma İstisnası (Move Permit, Time-Lock)
Cüzdan taşıma veya güvenlik upgrade gibi durumlar için:
- **Move Permit** talebi açılır  
- Kısa bir **time-lock** uygulanır  
- Topluluk denetimi (veto/quorum) devrededir  
- Zincire yalnızca “permit” kaydı ve yeni adres bağlanması yazılır

---

### 5.2) Evidence Pack: Trinity of Proof (Üçlü Kanıt Mekanizması)
* **Bileşenler ve Teknik Detaylar:**
  1) **Canlı Yayın (Live Stream Logs):** ham kayıtlar + platform server log uyumu  
  2) **Process Timelapse (Evrim Videosu):** katman katman inşanın teknik özeti  
  3) **Technical Logs (İşlem Günlükleri):** metadata, koordinatlar, araç zaman çizelgesi  
  4) **EvidenceRoot:** tüm dosyaların tek kripto kökü (Merkle Root)

* **Çözdüğü Sorun:** AI taklidinin saniyeler içinde “sonuç” üretmesine karşı, insan emeğinin “süreç” kanıtını korur.

---

### 5.3) Yıllık Yenileme Zorunluluğu (365-Day Heartbeat)
* **Tanım:** Public Registry’deki her kaydın “aktif ve sahipli” kaldığını gösteren yıllık imza.  
* **Çözdüğü Sorunlar:** Ölü veri, terk edilmiş cüzdanlar, pasif koleksiyonculuk.

* **Nasıl Çalışır?**
  - Her kaydın **Valid Until** tarihi vardır.  
  - Süre dolmadan **30 gün önce** uyarı.  
  - Sahip, yeni imza ile “hala bende ve standartlara uyuyor” der.  
  - Aksi halde kayıt **Legacy Archive** statüsüne iner.

> Opsiyonel hızlandırma: Eğer proje “yıllık arşiv + düzenli denetim” altyapısına sahipse heartbeat periyodu (ör. 30 gün) teknik olarak düşürülebilir. v1.0 varsayılanı 365 gündür.

---

## 🗳️ 6) Decentralized Supervision (Merkeziyetsiz Denetim)

### 6.1) Topluluk Veto Mekanizması (%40 Eşik)
* **Tanım:** Yeni kayıt veya protokol değişikliğinin, nitelikli azınlık tarafından durdurulabilmesini sağlayan demokratik güvenlik bariyeri.

#### v1.0 Güncellemesi: “Quorum + Veto” Çift Kilit
Sadece %40 veto demek, katılım düşükse manipüle edilebilir. Bu yüzden:

- **Quorum (Minimum Katılım):**  
  Toplam aktif oy ağırlığının en az **%25’i** katılmalı.  
- **Veto Threshold:**  
  Veto, yalnızca katılanların %40’ı değil; tercihen **toplam aktif ağırlığın %40’ına** ulaşınca çalışır.  
  (Bu protokolün “zırh” niyetine uygundur.)

* **Çözdüğü Sorunlar:**
  1) Sybil Attacks  
  2) Collusion (anlaşmalı oylama)  
  3) Bribery (rüşvetle oylama satın alma)

* **Örnek Senaryo:** AI ile üretilmiş bir görsel, “emeğim” diye başvurur. Evidence Pack tutarsızdır. Topluluk, logaritmik skorlama ve TWAB etkisi ile %40 veto barajını geçerse kayıt asla mühürlenemez.

---

## ⚙️ 7) The Michelangelo Framework (Meritocracy Engine)

### 7.1) Michelangelo // The Meritocracy Philosophy
* **Tanım:** İlhan Art ekosisteminin sıralama ve itibar motoru. “Zenginler listesi”ne dönüşmeyi engelleyen liyakat tabanlı hiyerarşi.  
* **Slogan:** *“You cannot buy your way to the top.”*  
* **Örnek:** Milyonlarca dolarlık balina, sadece para koyduğu için 1 numara olamaz. Zirve; yıllarca kültürel katkı sunanlara aittir.

### 7.2) Status Formula: Time × Contribution
\[
\text{Status} = \text{HoldingTime} \times \text{CulturalContribution}
\]

* **HoldingTime:** cold wallet’ta bozulmadan duran gün sayısı (örn. 1420 gün)  
* **CulturalContribution:** çeviri, kürasyon, altyapı, sergi desteği vb. somut katkı

* **Çözdüğü Sorun:** Sadece token tutmanın pasif bir eylem olması. Sistem “hem tutan hem üreten”i ödüllendirir.

---

## 📊 8) Cultural Multipliers & Ranking Levels

### 8.1) Cultural Multiplier (Kültürel Çarpanlar)
* **Tanım:** Final skora eklenen bonus sistem.  
* **Uygulama Alanları:**
  - **Translation (JP/TR/EN):** bilim/felsefe/sanat metinleri (+4,500 Pts örnek)  
  - **Curation:** registry kalite kontrol + veto katılımı  
  - **Infrastructure:** kod, dokümantasyon, indexer katkısı

* **Örnek:** 1000 gün holding + 1 büyük çeviri = sıralamada binlerce kişiyi geçebilir.

### 8.2) Tier Classifications (Rütbe Seviyeleri)
1) **Legendary (Top 10):** en yüksek veto/stratejik söz  
2) **Senior (Top 50):** ana kolonlar, kritik söz  
3) **Veteran (Top 100):** uzun vadeli doğrulayıcılar

* **Kural:** Statik değil. Katkı bırakılırsa veya istikrar bozulursa rütbe düşer.

---

## 📈 9) Cut-off Thresholds & Network Metrics

### 9.1) Entry Thresholds (Giriş Barajları)
Eşikler “stable” olduğunda tek olmalı:

- **Legendary Threshold:** **≥ 100,000 Pts**  
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
* **Kural:** Aktif claim yapmayan adresler, skorları yüksek olsa bile Global Registry’den düşer.  
* **Amaç:** Sistem “yaşayan ve üreten” bireylerden oluşsun.

---

## 🧬 12) Generational Legacy & Governance (Nesiller Arası Miras ve Yönetim)

### 12.1) Generational Inheritance (Varis Belirleme)
* **Tanım:** 4 yıl (1460 gün) boyunca kesintisiz Legendary statüsünü koruyanların itibar ve haklarını varise devredebilmesi.  
* **Çözdüğü Sorun:** Bir kişinin ölümü/aktifliği yitirmesiyle kültürel değerin kaybolması.  
* **Uygulama:** Varis ekranı yalnızca 4 yıllık sadakati kanıtlayanlara açılır ve on-chain mühürlenir.

### 12.2) Parliamentary Governance Rights (Parlamenter Söz Hakkı)
1) **Legendary (≥ 100k):** anayasa, fee, strateji  
2) **Patron (50k–99k):** kürasyon, denetim, oylamalar  
3) **Member (< 50k):** öneriler, küçük ölçekli kararlar

* **Çözdüğü Sorun:** Kaotik oylamalar yerine “liyakate dayalı demokrasi”.

---

## 🌍 13) Cultural Privilege Layers & Real-World Integration

> Not: Bu bölümdeki ayrıcalıklar, 2026–2030 kapsamında kademeli uygulanacak “Future Roadmap” bileşenleridir.

### 13.1) The Annual Exhibition Right (Yıllık Galeri Hakkı)
* **Tanım:** [PoArt] doğrulanmış yüksek skorlu sanatçı/patronların İlhan Art Gallery’de yılda 1 kez, 1 hafta sergileme hakkı.  
* **Çözdüğü Sorun:** Bağımsız sanatçının fiziksel alana erişim maliyeti.  
* **Nasıl Çalışır?** Threshold geçenler takvim üzerinden rezervasyon yapar; galeri “itibar puanları” ile kullanılır.

### 13.2) Dynamic Art Pricing (JSON-Linked Discounts)
* **Tanım:** Statünün indirim anahtarı olarak çalışması.  
* **Uygulama:**
  - Legendary: %50+  
  - Patron: %30  
  - Member: %10  
* **Felsefe:** Pazarlık değil, kanıtlanmış emek.

### 13.3) Physical Ecosystem Integration (Partner Entegrasyonu)
- Kitabevleri, kafeler, kültür merkezleri  
- QR ile statü okuma, claimable codes

### 13.4) Labor Over Capital: Meritocratic Access (Emek > Sermaye)
\[
\text{ClaimRight} \propto \text{CulturalScore} + \log_{10}(\text{Balance})
\]
250 token tutup yoğun katkı üreten biri, 100k token tutup pasif kalan birinden daha fazla avantaja sahip olabilir.

---

## 🧩 14) State Machine (Kayıt Yaşam Döngüsü)

Bir [PoArt] kaydı ve [FPP] statüsü aşağıdaki deterministik akıştan geçer:

1) **Draft** (hazırlık)  
2) **Submitted** (başvuru)  
3) **Under Review** (inceleme)  
4) **Challenged** (itiraz açıldı)  
5) **Verified** (NotarySeal basıldı)  
6) **Renew Due** (heartbeat zamanı yaklaştı)  
7) **Legacy Archive** (yenilenmedi, pasif arşiv)  
8) **Revoked** (ihlal/kanıt çökmesi/veto/çoklu ihlal)

> Bu akış; “ne zaman hangi statüdeyim?” sorusunu tek bakışta çözer.

---

## 🔗 15) Minimal On-chain / Maximal Off-chain

### Zincir Üstüne (On-chain) Yazılanlar
- `EvidenceRoot` (Merkle Root)  
- `NotarySeal`  
- `TimeStamp`  
- `Signer` (artist/owner)  
- `Status` (Verified/Legacy/Revoked)  
- `Permit Records` (Move Permit gibi istisnalar)

### Zincir Dışında (Off-chain) Tutulanlar
- ham video dosyaları  
- timelapse  
- teknik log dosyaları  
- manifest detayları  
- büyük arşiv setleri (IPFS/Arweave)

**Amaç:** Zinciri şişirmeden, doğrulanabilirliği maksimum yapmak.

---

## 🏛️ 16) Appeals / Mercii & İtiraz Mekanizması (Kurumsal Güven Katmanı)

İtiraz mekanizması “güvenin kurumsal teminatıdır”.

- **Strategic Filter:** İtirazlar “kanıt tabanlı” olmalı (sadece duygu/iftira değil).  
- **Community Veto:** %40 veto + quorum çift kilit  
- **Anti-Bot / Anti-Sybil:** (uygulama katmanı) Solana-gated / stake-gated doğrulama ile bot akışını boğma  
- **Evidence Pack Freezing:** İtiraz açıldığında ilgili kanıt paketi “freeze” olur (zaman kilidi)  
- **Transparency / Time-Lock:** Her itiraz olayı kamuya açık zaman çizelgesinde görünür; ani sansür veya manipülasyon engellenir.

---

## 🧨 17) Threat Model (Saldırı Kataloğu ve Karşı Katmanlar)

- **Sybil Attack:** Turnstile + Zombie Filter + Quorum  
- **Flash-loan:** TWAB + Guard Window + Log Scoring  
- **Whale Domination:** Logarithmic Power Scoring + TWAB  
- **Wash Trading:** Cold Wallet Verification + Penalty Ladder  
- **Collusion:** Veto + Evidence Pack scrutiny + transparency  
- **Data Tampering:** EvidenceRoot + SHA-512 signatures + NotarySeal  
- **Bribery / Vote Buying:** Time-lock + quorum + contribution-weighted legitimacy  
- **Deepfake Process Forgery:** Random Challenge Frames + manifest + hash chain

---

## ⚖️ 18) Final Word: A Blueprint for Global Governance (Manifesto)

> **Vizyon Notu:** [FPP] ve [PoArt] tarafından inşa edilen bu matematiksel zırh, sadece bir sanat galerisini değil; yozlaşmış parlamenter sistemleri ve manipüle edilen seçimleri de iyileştirebilecek bir “yönetim modeli” sunar.

### 18.1) The End of Plotokrasi (Sermaye Despotizminin Sonu)
* **Tanım:** Plütokrasi: yönetimin en zengin azınlığın elinde olması.  
* **Protokolün Yanıtı:** Logaritmik skorlama ile paranın gücü sınıra çekilir; “zaman” ve “emek” otorite olur.  
* **Gerekçe:** Gelecek, cüzdanı şişkin olanın değil; entelektüel değer katanın elinde olmalıdır.

### 18.2) The Meritocratic Parliament (Liyakate Dayalı Parlamento)
Popülizm ve sermaye odaklı siyasetin yerine; dökümantasyonu özümsemiş, IPOW sunmuş liyakat sahiplerinin söz hakkı kazandığı bir yapı hedeflenir.

### 18.3) Security Against Vote Rigging (SHA-512 Seçim Güvencesi)
- Turnstile: bot manipülasyonunu ekonomik olarak boğar  
- TWAB: son dakika vatandaşlık/oy satın almayı etkisizleştirir  
- %40 Veto + Quorum: azınlığın sesini ezdirmeden denetim sağlar

### 18.4) The Conclusion: Saving the Future (Geleceği Kurtarmak)
Bu sistem; hilenin değil kanıtlanmış emeğin, anlık heveslerin değil bin yıllık vizyonun kazandığı bir “yeni düzen” tasarımıdır. Yanlış yönetilmeye mahkum edilmiş bir toplumu kurtarmanın yolu; insan hatasını azaltan, matematiksel olarak adil olduğu ispatlanmış bir protokol mimarisi kurmaktır.

---

## 📅 19) Roadmap & Future Notes
Bu dökümantasyonda yer alan tüm maddeler, İlhan Art ekosisteminin 2026’dan 3000 yılına uzanan vizyonunun yapı taşlarıdır. Her sürüm güncellemesi (v1.1, v1.2 vb.) bu ayrıcalıkların teknik entegrasyon süreçlerini (API bağlantıları, fiziksel POS entegrasyonları vb.) içerecektir.

---
