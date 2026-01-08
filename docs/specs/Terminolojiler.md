# ⚙️ Sol Ate Engine v1.0: Core Infrastructure

**Sol Ate Engine**, [PoArt] protokolünün arkasında yatan çekirdek mantığı ve teknik işleyişi temsil eden ana katmandır. Sanat eserinin ham üretim verisini alıp, onu sarsılmaz bir dijital kanıta dönüştüren "akıl" burasıdır.

---

### 🧩 Neden "Sol Ate"?

* **Sol (Solana):** Protokolün Solana ağını (veya Solana tabanlı varlıkları) bir kimlik ve sahiplik katmanı olarak kullandığını belirtir.
* **Ate (Artistic/Authenticated Trust Engine):**
    * **Teknik Tanım:** Sanatsal Güven Motoru. Üretim sürecine ait verilerin (fırça darbeleri, timelapse, loglar) sahte olmadığını doğrulayan algoritma seti.
    * **Felsefi Derinlik (Atē):** Yunan mitolojisinde *Atē*, insanın içine düşebildiği "hata" veya "anlık dürtü" anlamına gelir. Bu isim, yapay zekanın ruhsuz ve hesaplanmış kusursuzluğuna karşı; **insanın hata yapabilen, ter döken ve gerçek olan iradesini** kutsayan bir ironidir.

---

### 🛠️ v1.0 Teknik Kapsamı (Fonksiyonel Görevler)

Sol Ate Engine, karmaşık finansal modeller yerine şu 3 ana sütun üzerine inşa edilmiştir:

1.  **Hashing & Sealing (Mühürleme):**
    Evidence Pack içindeki tüm dosyaları (video, JSON, imza) işleyerek dökümantasyonda tanımlanan tekil **NotarySeal** değerini üretir.
    $$\text{Sol Ate Output} = \text{SHA-512}(\text{Input Data})$$

2.  **Indexing (Arşivleme):**
    Hangi cüzdanın, hangi tarihte, hangi sanat eseri için "Labor Proof" (Emek Kanıtı) sunduğunu şeffaf ve sorgulanabilir bir veritabanına işler.

3.  **Verification (Doğrulama):**
    Bir eserin orijinalliği sorgulandığında, ham dosyaları tekrar motor süzgecinden geçirerek orijinal mühürle eşleşip eşleşmediğini matematiksel kesinlikle test eder.

---

### 🏛️ "Engine" (Motor) Kavramının Önemi

Pump.fun veya benzeri platformlardan çıkan token'lar sadece birer **"erişim bileti"** niteliğindedir. **Sol Ate Engine** ise o biletin hangi hakları koruduğunu, emeğin nasıl tescilleneceğini ve sanatın nasıl ebedileşeceğini belirleyen **anayasal mantık katmanıdır.**

> **Not:** Bütçe ve imkanlardan bağımsız olarak bu motorun mantığını GitHub üzerinde tanımlamak, projenin sadece bir finansal spekülasyon değil, uzun vadeli bir **yazılım altyapısı** ve **dijital bir milli kütüphane** vizyonu olduğunu kanıtlar.

---


## 🎨 [PoArt] EMEK KANITI PROTOKOLÜ
**Gerçek Sanatçı, Gerçek Üretim, Gerçek Değer**

### a) [PoArt] Nedir?
**Proof of Art [PoArt];** bir projenin arkasındaki emeğin, doğrudan gerçek zamanlı insan iradesinden doğduğunu kanıtlarla görünür kılan kurumsal bir doğrulama yaklaşımıdır. Katılımcıya “İnan” demez; **“Bak ve doğrula”** der.

### b) [PoArt] 5'li Standart (The 5 Standards)
1.  **Canlı Kimlik Kanıtı (Live Identity Proof):** Üretim anının gerçekliğine çıpalanmış canlı doğrulama.
2.  **Emek ve Süreç Kanıtı (Labor & Process Proof):** Harcanan kümülatif zamanın ve "üretim sancısının" kaydı.
3.  **Estetik Değer Kanıtı (Aesthetic Value Proof):** Akademik ve sanatsal derinliğe sahip estetik standart.
4.  **Fikirsel İnovasyon (Conceptual Novelty):** Sanat ve teknoloji arasında yeni felsefi köprüler.
5.  **Algoritmik Olmayan İrade (Non-Algorithmic Agency):** İnsanın hata yapabilen ve risk alan özgün iradesi.

### c) Doğrulama & Anti-Sahtecilik
* **Kanıt Paketi (Evidence Pack):** Video kayıtları, zaman damgaları ve teknik metadatadan oluşan dijital ikiz.
* **365 Günlük Yenileme:** "Verified" statüsü kalıcı değildir; her yıl üretim döngüsünün kanıtlanmasıyla yenilenir.
* **Kırmızı Bayrak (Red Flag):** Sahtecilik veya ihlal durumunda statü derhal askıya alınır.

---

## 🗳️ YÖNETİŞİM VE KAMU SİCİLİ

* **Public Registry:** Tüm onaylı veriler `ilhanart.org/registry` (veya GitHub Registry) adresinde kaydedilir.
* **%40 Topluluk Vetosu:** Statü kazanılmadan bir ay önce oylama başlar; **Token-Gated (Solana-Verified)** topluluğun %40 itirazı başvuruyu geçersiz kılar.
* **Metadata Sync:** Sicildeki teknik veriler fiziksel varlıkla %100 eşleşmek zorundadır.

---

## 🔐 TEKNİK MÜHÜR (NOTARY SEAL)

Sol Ate Engine v1.0 tarafından üretilen sarsılmaz mühür algoritması:

$$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$

---
**PROTOKOL V1.0 // SHA-512 İLE MÜHÜRLENMİŞTİR.** *© 2025 İLHAN ART | ESERLERİN, GÖRSELLERİN VE FİKİRLERİN TÜM HAKLARI SAKLIDIR.*
