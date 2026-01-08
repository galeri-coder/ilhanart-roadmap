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

# [PoArt] Dijital Noter & Adli Kanıt Protokolü (Beta v1.0)

> **"Kültür, sermayeden büyüktür. Eserlerinizi bugünden koruyun, yarına taşıyın."**

# [PoArt] Dijital Noter & Adli Kanıt Protokolü (v1.0 Beta)

> **"Kültür, sermayeden büyüktür. Eserlerinizi bugünden koruyun, yarına taşıyın."**

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

---

## 📑 İçindekiler

1. [Proje Hakkında ve Vizyon](#-proje-hakkında-ve-vizyon)
2. [Neyi İcat Ettik? (Teknolojik İnovasyon)](#-neyi-icat-ettik-teknolojik-inovasyon)
3. [Kullanım Alanları ve Fayda](#-kullanım-alanları-ve-fayda)
4. [Sistem Mimarisi ve Teknik Özellikler](#-sistem-mimarisi-ve-teknik-özellikler)
5. [Yol Haritası: "Trustless" Gelecek](#-yol-haritası-trustless-gelecek)
6. [Rakip Analizi](#-rakip-analizi)
7. [Basın ve Topluluk Kiti](#-basın-ve-topluluk-kiti)

---

## 📖 Proje Hakkında ve Vizyon

**[PoArt] Dijital Noter**, dijital varlıkların (sanat eseri, belge, tasarım, kod vb.) mülkiyetini ve varoluş anını kanıtlamak için geliştirilmiş, **Adli Bilişim (Forensic)** prensiplerine dayalı çalışan, merkeziyetsizliğe geçiş sürecindeki bir kanıt protokolüdür.

Bu sistem, "Gizlilik üzerinden güvenlik" (Security through obscurity) ilkesini reddeder. Bunun yerine, şeffaflık ve kriptografik matematiğin gücüne inanır. 

**Neden Halka Açık?**
Gerçek güvenlik şeffaflıktan gelir. **Public Registry (Halka Açık Kayıt)** sistemimiz sayesinde, dünyanın herhangi bir yerindeki bir kişi, elindeki dosyanın orijinal olup olmadığını, herhangi bir otoriteye ihtiyaç duymadan saniyeler içinde doğrulayabilir.

---

## 💡 Neyi İcat Ettik? (Teknolojik İnovasyon)

PoArt, sadece bir dosya yükleme sistemi değildir. Üç farklı teknoloji katmanını tek bir potada eriterek yeni bir standart getiren bir **"Adli Kanıt Zinciri" (Forensic Chain of Custody)** motorudur.

### 1. Client-Side Hashing (Maksimum Gizlilik)
Dosyalarınız asla sunucuya yüklenmez. Tarayıcı tabanlı (Client-side) çalışan motorumuz, dosyanın hash'ini (dijital özetini) kendi bilgisayarınızda hesaplar. Sunucuya sadece bu parmak izi ve meta veriler gönderilir. **Gizliliğiniz %100 korunur.**

### 2. Forensic Data Fusion (Adli Güç)
Sıradan bir zaman damgasından (Timestamp) çok daha fazlasıdır. Sistem şu verileri tek bir "Genesis Mühür" içinde birleştirir:
* **Dijital DNA (SHA-512):** Eserin tek bir pikseli değişse bile bozulacak askeri standartta kriptografik imza.
* **Konum & Zaman:** İşlemin yapıldığı milisaniye hassasiyetinde tarih, ülke, şehir ve ilçe verisi.
* **Cihaz Kimliği:** İşletim sistemi, tarayıcı ve cihaz tipi (User-Agent analizi).
* **IP Adresi:** Hukuki süreçler için saklanan (ancak halka açık alanda maskelenen) bağlantı noktası.

### 3. Privacy Guard (Şeffaflık Dengesi)
Halka açık kayıtlarda kişisel verileri (IP gibi) maskeleyerek (Örn: `46.1.***.***`) gösterirken, arka planda ham veriyi (Raw Data) hukuki delil niteliği taşıması için şifreli olarak saklayan hibrit bir yapı kullanır.

---

## 🛡️ Kullanım Alanları ve Fayda

Bir sanatçı, yazar veya tasarımcıysanız, "Bunu ben daha önce yapmıştım" demek yetmez, kanıtlamanız gerekir.

**PoArt ile mühürlediğiniz bir eser:**
* **Matematiksel Kanıt:** Dosyanızın tek bir pikseli bile değişse sistem bunu anlar. Manipülasyon imkansızdır.
* **Hukuki Dayanak:** Eserin hangi tarihte, hangi şehirde, hangi cihazdan mühürlendiği kayıt altındadır.
* **Anında Sertifika:** Saniyeler içinde size özel, QR kodlu ve mühürlü bir "Varlık Kimlik Sertifikası" üretir.

---

## ⚙️ Sistem Mimarisi ve Teknik Özellikler

Sistem, "Serverless" (Sunucusuz) bir mimari üzerinde, yüksek performans ve ölçeklenebilirlik odaklı tasarlanmıştır.

* **Kriptografi:** SHA-256 & SHA-512 (Çift katmanlı özetleme).
* **Veri Tabanı:** Supabase (PostgreSQL) - JSONB veri yapısı.
* **Adli Veri:** `ipapi` entegrasyonu ile IP/Konum üçlemesi.
* **Rendering:** `html2canvas` ve DOM manipülasyonu ile sunucu yükü olmadan anlık PNG sertifika üretimi.

---

## 🗺️ Yol Haritası: "Trustless" Gelecek

Şu anki sürüm **(Beta v1.0)**, son kullanıcıya maksimum hız, kolay arayüz ve ücretsiz erişim sağlamak için optimize edilmiştir. Ancak nihai vizyonumuz, veritabanı yöneticisinin (bizim) bile müdahale edemeyeceği bir yapıya geçmektir.

### Faz 1: Beta (Şu An Yayında)
* **Altyapı:** Cloud Database (Supabase).
* **Amaç:** Hız, UX (Kullanıcı Deneyimi) bariyerlerini kaldırmak ve adaptasyon. "Sürtünmesiz" güvenlik sağlamak.

### Faz 2: Permaweb Geçişi (Gelecek Vizyonu)
* **Altyapı:** IPFS (InterPlanetary File System) ve Arweave.
* **Hedef:** **Immutable Storage (Değiştirilemez Depolama).**
* **Vizyon:** Veriler merkezi sunuculardan çıkarılarak dağıtık ağlara taşınacaktır. Bu geçiş tamamlandığında, oluşturulan kayıtlar sistem yöneticisi olarak **bizim bile silemeyeceğimiz**, sansürlenemez ve sonsuza dek yaşayan blokzincir tabanlı kanıtlara dönüşecektir.
* **Sonuç:** Tamamen "Trustless" (Güvene dayalı olmayan, matematiğe dayalı) bir sistem.

---

## 📊 Rakip Analizi

PoArt, mevcut çözümlerin eksiklerini tamamlayan "Sweet Spot" (En ideal nokta) üzerine konumlanmıştır.

| Özellik | **PoArt Notary** | OpenTimestamps | Verisart / Artory | OriginStamp |
| :--- | :---: | :---: | :---: | :---: |
| **Maliyet** | **Ücretsiz** | Ücretsiz | Ücretli / Abonelik | Freemium |
| **Kullanım Kolaylığı** | **Çok Kolay (Sürükle-Bırak)** | Zor (Teknik Bilgi İster) | Orta (Cüzdan İster) | Orta |
| **Adli Veri (Konum/IP)** | **✅ Var** | ❌ Yok | ❌ Yok | ⚠️ Kısıtlı |
| **Sertifika Çıktısı** | **✅ Anlık PNG** | ❌ Yok | ✅ Var | ✅ Var |
| **Gizlilik** | **✅ Client-Side Hash** | ✅ Client-Side Hash | ⚠️ Server Upload | ⚠️ Server Upload |

---

## 📜 Lisans

Bu proje **[İlhan Art Gallery]** inisiyatifi ile geliştirilmiş olup, kaynak kodları şeffaflık adına halka açıktır.


**PROTOKOL V1.0 // SHA-512 İLE MÜHÜRLENMİŞTİR.** *© 2025 İLHAN ART | ESERLERİN, GÖRSELLERİN VE FİKİRLERİN TÜM HAKLARI SAKLIDIR.*
