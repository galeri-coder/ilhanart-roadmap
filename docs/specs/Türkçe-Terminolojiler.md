# 📚 TERMINOLOJİ & KAVRAMLAR SÖZLÜĞÜ
> **"Bu protokolün dilini anlamak, vizyonunu anlamaktır."**

## ⚙️ Sol Ate Engine v1.0: Core Infrastructure

**Sol Ate Engine**, [PoArt] protokolünün arkasında yatan çekirdek mantığı ve teknik işleyişi temsil eden ana katmandır. Sanat eserinin ham üretim verisini alıp, onu sarsılmaz bir dijital kanıta dönüştüren "akıl" burasıdır.

### 🧩 Neden "Sol Ate"?

* **Sol (Solana):** Protokolün Solana ağını (veya Solana tabanlı varlıkları) bir kimlik ve sahiplik katmanı olarak kullandığını belirtir.
* **Ate (Artistic/Authenticated Trust Engine):**
    * **Teknik Tanım:** Sanatsal Güven Motoru. Üretim sürecine ait verilerin (fırça darbeleri, timelapse, loglar) sahte olmadığını doğrulayan algoritma seti.
    * **Felsefi Derinlik (Atē):** Yunan mitolojisinde *Atē*, insanın içine düşebildiği "hata" veya "anlık dürtü" anlamına gelir. Bu isim, yapay zekanın ruhsuz ve hesaplanmış kusursuzluğuna karşı; **insanın hata yapabilen, ter döken ve gerçek olan iradesini** kutsayan bir ironidir.

### 🛠️ v1.0 Teknik Kapsamı

Sol Ate Engine, karmaşık finansal modeller yerine şu 3 ana sütun üzerine inşa edilmiştir:

1.  **Hashing & Sealing (Mühürleme):**
    Evidence Pack içindeki tüm dosyaları (video, JSON, imza) işleyerek dökümantasyonda tanımlanan tekil **NotarySeal** değerini üretir.
    
    $$\text{Sol Ate Output} = \text{SHA-512}(\text{Input Data})$$

2.  **Indexing (Arşivleme):**
    Hangi cüzdanın, hangi tarihte, hangi sanat eseri için "Labor Proof" (Emek Kanıtı) sunduğunu şeffaf ve sorgulanabilir bir veritabanına işler.

3.  **Verification (Doğrulama):**
    Bir eserin orijinalliği sorgulandığında, ham dosyaları tekrar motor süzgecinden geçirerek orijinal mühürle eşleşip eşleşmediğini matematiksel kesinlikle test eder.

---

### 🧮 Sol Ate Değer Teoremi (The Value Theorem)

PoArt protokolü, bir dijital varlığın değerini ($V$) sübjektif piyasa algısıyla değil; **üretim sürecinin fiziksel gerçekliğiyle** hesaplar.

Yapay Zeka (AI), sonucu anında ($t \to 0$) vererek süreci yok eder. [PoArt] ise değeri, zaman ve irade fonksiyonunun bir türevi olarak kabul eder.

$$
V_{PoArt} = \int_{t_{start}}^{t_{end}} \left( P_{labor}(t) \cdot I_{agency}(t) \right) \, dt + U_{irreversible}
$$

#### Değişkenlerin Tanımı:

* **$\int dt$ (Süreç Birikimi):**
    Değer anlık bir "çıktı" (output) değildir; $t_{start}$ ve $t_{end}$ arasında biriken bir **süreçtir**. Süre azaldıkça (AI üretimi), entegralin sonucu 0'a yakınsar.

* **$P_{labor}(t)$ (Anlık Emek Gücü):**
    Fizikteki "Güç" ($P = W/t$) tanımıdır. Sanatçının üretim anında harcadığı zihinsel ve fiziksel enerjinin (Joule/saniye) yoğunluğudur. Kanıtlanabilir efor ne kadar yüksekse, çarpan o kadar büyür.

* **$I_{agency}(t)$ (İrade Katsayısı):**
    Üreticinin risk alma ve karar verme kapasitesidir. $0$ ile $1$ arasında bir değer alır.
    * **AI ($I \approx 0$):** Komutları uygular, risk almaz, bedel ödemez.
    * **İnsan ($I \to 1$):** Karar değiştirir, tereddüt eder, risk alır.

* **$U_{irreversible}$ (Geri Döndürülemez Tekillik):**
    Eskiden "hata" denilen, aslında eseri benzersiz kılan **kaotik imza**dır.
    * Dijitalde `Ctrl+Z` vardır.
    * PoArt'ta ise tuvale sürülen boya, yontulan mermer veya canlı yayındaki bir jest geri alınamaz. Bu **entropik kesinlik**, eseri kopyalanamaz (Non-Fungible) kılar.

### 🔎 Vaka Analizi: AI "Anlık Çıktı" vs. İnsan "Kanıtlı Süreç"

Aşağıdaki senaryo, **Sol Ate Değer Teoremi**'nin pratikte nasıl işlediğini ve neden AI üretimlerinin [PoArt] standardında düşük skor aldığını kanıtlar.

#### Senaryo A: AI ile 10 Saniyede Görsel Üretimi
* **Süre ($\Delta t$):** $10$ saniye (Süreç yok denecek kadar az).
* **Emek Gücü ($P_{labor}$):** $1$ birim (Sadece komut yazma).
* **İrade Katsayısı ($I_{agency}$):** $0.01$ (Risk yok, bedel yok, sadece komut).
* **Geri Döndürülemezlik ($U_{irreversible}$):** $0$ (Ctrl+Z mümkün, sonsuz kopyalanabilir).

**Sonuç:**
$$V_{AI} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$
> **Yorum:** Çıktı kusursuz olsa bile; süreç yaşanmadığı ve irade/risk barındırmadığı için [PoArt] değeri $0$'a yakınsar.

#### Senaryo B: Canlı Yayında 6 Saatlik Fiziksel Üretim
* **Süre ($\Delta t$):** $6$ saat ($21,600$ saniye).
* **Emek Gücü ($P_{labor}$):** $0.5$ birim (Fiziksel ve zihinsel eforun sürekliliği).
* **İrade Katsayısı ($I_{agency}$):** $0.9$ (Karar değiştirme, risk alma, geri dönüşsüz seçimler).
* **Geri Döndürülemezlik ($U_{irreversible}$):** $>0$ (Tuvale sürülen boya, yontulan mermer, canlı yayındaki jest geri alınamaz).

**Sonuç:**
$$V_{Human} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{irreversible} \approx 9,720 + U_{irreversible}$$
> **Yorum:** Süreç uzadıkça ve irade (risk) arttıkça değer kümülatif olarak artar. $U_{irreversible}$ terimi ise eseri **"Kopyalanamaz" (Non-Fungible)** kılarak ontolojik bir tekillik sağlar.

---

### ✅ Sonuç: Değerin İspatla Kilitlenmesi (Proof-Bound Value)

Bu teorem, [PoArt]'ın değer iddiasını bir "beğeni" veya "piyasa anlatısı" olmaktan çıkarıp **ispatlanabilir bir üretim gerçeğine** bağlar.

1.  **Süreç Olmadan Değer Oluşmaz:**
    AI anlık çıktıda ($t \to 0$) süreci yok eder. Süreç penceresi daraldıkça entegralin sonucu matematiksel bir zorunlulukla küçülür:
    $$\Delta t \downarrow \implies \int (P \cdot I) \, dt \to 0$$

2.  **İrade ve Risk Çarpandır:**
    [PoArt], sadece "harcanan süreyi" değil, o süredeki gerçek karar, risk ve bedel katmanını ölçer. Risk almayan (AI) bir üretimin değeri düşüktür.
    $$V_{PoArt} \propto \int (P_{labor} \cdot I_{agency}) \, dt$$

3.  **Tekillik, Pazarlama Değil Fiziksel Bir Kanıttır:**
    Fiziksel üretimde geri alınamaz izler (tuval darbesi, mermer kırığı), dijitaldeki `Ctrl+Z` mantığının dışındadır. Bu geri döndürülemezlik ($U_{irreversible}$), eseri ontolojik olarak tekilleştirir.

> **🔐 ÖZET:** Değer teoremi ölçüm olarak belirsiz gözüksede bu formülün amacı yapmaya çalıştığımız amacın temellerinin değişkenlerinin kurgularını gösterebilmektir. AI çağında nadir olan şey "görüntü" değil; **kanıtlanabilir emek, zaman ve iradedir.** [PoArt], bu kıtlığı ölçer ve **Evidence Pack** ile tesciller.

### 🏛️ "Engine" (Motor) Kavramının Önemi

Pump.fun veya benzeri platformlardan çıkan token'lar sadece birer **"erişim bileti"** niteliğindedir. **Sol Ate Engine** ise o biletin hangi hakları koruduğunu, emeğin nasıl tescilleneceğini ve sanatın nasıl ebedileşeceğini belirleyen **anayasal mantık katmanıdır.**

> **Not:** Bütçe ve imkanlardan bağımsız olarak bu motorun mantığını GitHub üzerinde tanımlamak, projenin sadece bir finansal spekülasyon değil, uzun vadeli bir **yazılım altyapısı** ve **dijital bir milli kütüphane** vizyonu olduğunu kanıtlar.

---


## 🎨 # [PoArt] EMEK KANITI PROTOKOLÜ (Proof of Art Protocol v1.0)

> **"Gerçek Sanatçı, Gerçek Üretim, Gerçek Değer."**

Bu protokol; kripto ekosistemini saran anonim dolandırıcılara, 5 dakikada üretilen yapay zeka görsellerine ve "Pump & Dump" (Pompala ve Boşalt) kültürüne karşı geliştirilmiş **biyolojik ve entelektüel bir savunma mekanizmasıdır.**

---

## a) [PoArt] Nedir? (Felsefi ve Teknik Tanım)

**Proof of Art [PoArt];** blokzincir üzerindeki bir varlığın arkasındaki değerin, spekülasyona değil; doğrulanabilir **insan emeğine**, **zamana** ve **fiziksel enerjiye** dayandığını garanti altına alan kurumsal bir doğrulama standardıdır.

Bitcoin nasıl *"Elektrik ve İşlemci Gücü"* **(Proof of Work)** ile değer üretiyorsa; [PoArt] uyumlu projeler de *"Sanatsal Yetenek ve İnsan Zamanı"* ile değer üretir.

Pump.fun ve DEX platformlarındaki *"Yazılımcı (Dev) sattı, proje bitti"* riskini ortadan kaldırır; çünkü burada değer kodda değil, **üretimin sürekliliğinde** saklıdır.

> **[PoArt], katılımcısına "Bize güvenin" demez; "İşte kanıtlar, gözlerinle gör, matematiğinle doğrula" der.**

---

## b) [PoArt] 5'li Standart (The 5 Pillars of Truth)

Bu 5 madde, bir projenin [PoArt] mührünü alabilmesi için geçmesi gereken, manipüle edilemez filtrelerdir.

### 1. Canlı Kimlik Kanıtı (Live Identity Proof)
* **Sorun:** Kripto dünyası, kimliği belirsiz anonim kurucuların (Dev'lerin) parayı toplayıp projeyi terk etmesiyle doludur.
* **[PoArt] Çözümü:** Üretici, sadece kimlik kartını değil, **üretim anındaki varlığını** kanıtlar. Bu, önceden kaydedilmiş videolarla değil; toplulukla etkileşime girilen, anlık spesifik taleplerin (Örneğin: *"Tuvalin sağ köşesine bugünün tarihini ve güncel blok numarasını yaz"*) yerine getirildiği canlı yayın seanslarını içerir.
* **Motto:** *"Botlar resim yapabilir ama botlar terlemez ve doğaçlama yapamaz."*

### 2. Emek ve Süreç Kanıtı (Labor & Process Proof)
* **Sorun:** 2 saniyede üretilen AI (Yapay Zeka) görselleri ile 2 ayda yapılan yağlı boya tablonun dijital dünyada aynı "jpeg" muamelesi görmesi.
* **[PoArt] Çözümü:** Eserin "hamilelik ve doğum" süreci kayıt altına alınır. Eskiz aşamaları, boya katmanları, harcanan kümülatif saatler ve sanatçının o eseri yaratırken yaşadığı fiziksel süreç belgelenir. Bu, tokene **"Zaman Maliyeti" (Time Cost)** ekler. Bir varlığın üretimi ne kadar zorsa, değeri o kadar sağlamdır.

### 3. Estetik Değer Kanıtı (Aesthetic Value Proof)
* **Sorun:** "Meme" kültürünün, estetiği ve sanatsal derinliği yok sayarak sadece anlık komediye odaklanması ve bunun sonucunda oluşan kısa ömürlü "Hype" projeler.
* **[PoArt] Çözümü:** Proje, akademik sanat standartlarına, renk teorisine, kompozisyon kurallarına ve malzeme bilgisine (Impasto, Doku vb.) sahip olmalıdır. İçerik sadece güldürmemeli; izleyicide hayranlık uyandırmalı ve **koleksiyon değeri** taşımalıdır.

### 4. Fikirsel İnovasyon (Conceptual Novelty)
* **Sorun:** Birbirinin kopyası olan, yaratıcılıktan uzak binlerce köpek/kedi coin'i.
* **[PoArt] Çözümü:** Proje, sanat; bilim, felsefe veya teknolojiyi bir şekilde fazla yapıda birleştiren yeni bir köprü kurmalıdır. (Örn: Klasik Davud heykeli ile Kripto Piyasa verilerini birleştirmek bunun üzerinden insan algısının taşa dönüşmesine dem vurmak ve bunları bilimsel kaynaklar ile delillendirebilmek). Eser, sadece görsel bir şölen değil, aynı zamanda **Bilim, Felsefe veya Teknoloji** üzerine düşündüren bir entelektüel meydan okuma olmalıdır.

> [!IMPORTANT]
>**Referans Örnek (Las Palmitas Etkisi): Meksika'nın suçla boğuşan Las Palmitas mahallesinde, 200'den fazla ev devasa bir "Gökkuşağı Muralı"na dönüştürülmüştür. Bu >estetik müdahale sonucunda mahalledeki suç oranları belirli ölçüde düşmüş, gençler çeteler yerine sanatla ilgilenmeye başlamıştır. Estetik değişim, insanların çevrelerine ve >birbirlerine olan saygısını (Social Cohesion) yeniden kodlamıştır.**
>
>**Beklenti: [PoArt] listesine girecek bir proje; tıpkı yukarıdaki örnekte olduğu gibi, salt görsel estetikten öte sosyolojik, bilimsel veya felsefi bir neden-sonuç >ilişkisi barındırmalıdır.
>Para ile satın alınamayacak yegâne varlık "Zaman" olduğu için, bu protokolde zaman bir teminat olarak stake edilerek kanıtlanmalıdır. Projenin fikirsel temeli o >kadar güçlü ve evrensel olmalıdır ki; seneler sonra olası bir CTO (Community Take Over) senaryosunda bile, topluluk bu mirası devralarak projenin yenilikçi >potansiyelini otonom bir şekilde sürdürebilmelidir.**

### 5. Algoritmik Olmayan İrade (Non-Algorithmic Agency)
* **Sorun:** Kusursuz ama ruhsuz, birbirini tekrar eden dijital üretimler.
* **[PoArt] Çözümü:** İnsanın hata yapabilen, risk alan ve duygusal dalgalanmalar yaşayan özgün iradesi eserde hissedilmelidir. Fırça darbelerindeki belirsizlik, malzemenin beklenmedik tepkileri ve sanatçının anlık kararları, eseri "Makine Üretimi"nden ayıran **Biyolojik İmza**dır.

---

## c) Doğrulama & Anti-Sahtecilik Mekanizması

Bu sistem, projenin sadece "başlangıçta" değil, "sonsuza kadar" güvenilir ve canlı kalmasını sağlar.

### 📦 Kanıt Paketi (Evidence Pack - The Digital Twin)
Her [PoArt] sertifikalı eserin arkasında, yatırımcıların indirebileceği şifreli ve zaman damgalı bir veri paketi bulunur:
* **RAW Video Kayıtları:** Üretim anının kesintisiz ham görüntüleri.
* **Metadata Analizi:** Dosyanın oluşturulma tarihi, kullanılan cihaz bilgileri ve konum verileri.
* **Fiziksel Referanslar:** Eserin fiziksel dünyada var olduğuna dair kanıtlar (Örn: Eserin yanında duran güncel gazete veya o anki blokzincir verisi).

### 🔄 365 Günlük Yenileme (The Sustainability Protocol)
* **Devrimsel Özellik:** Kripto projelerinde "Dev" (Geliştirici), tokeni piyasaya sürer ve genelde 1-2 ay sonra ortadan kaybolur (Soft Rug). [PoArt] bunu imkansız kılar.
* **Kural:** "Verified Artist" (Doğrulanmış Sanatçı) statüsü ömür boyu değildir. Sadece **1 yıl** geçerlidir.
* **İşleyiş:** Sanatçı/Geliştirici, her 365 günde bir, topluluğa **yeni, büyük ve kanıtlanabilir bir eser** sunmak zorundadır.
* **Örnek Senaryo:** 2026'da projeyi başlattınız. 2027 Ocak ayında sistem "Kanıt Süresi Doldu" uyarısı verir. Eğer sanatçı yeni bir sergi, yeni bir fiziksel eser veya yeni bir teknolojik entegrasyon sunmazsa, projenin "Güven Rozeti" düşer.
* **Sonuç:** Bu sistem, **içeriğin asla güncelliğini yitirmemesini** ve yatırımcının *"Geliştirici hala burada mı?"* korkusu yaşamamasını sağlar. Proje, yaşayan bir stüdyoya dönüşür.

### 🚩 Kırmızı Bayrak (Red Flag Protocol)
Topluluk veya algoritmalar tarafından tespit edilen herhangi bir sahtecilik (AI kullanımı, çalıntı eser, manipüle edilmiş video) durumunda:
1.  Sertifika derhal **"İPTAL" (VOID)** olarak işaretlenir.
2.  Kanıt paketleri halka açık şekilde **"Sahte"** olarak etiketlenir.
3.  Proje, [PoArt] kara listesine alınır. Bu, merkeziyetsiz bir dünyada **itibarın tek para birimi** olduğu gerçeğini pekiştirir.

---

## d) Sonuç: Kumarhane Değil, Müze.

**Pump.fun ve Merkeziyetsiz Borsalar (DEX) şu an malesef birer kumarhanedir; ışıklar yanıp söner, herkes hızlı kazanç peşindedir ve kasa (dolandırıcılar) her zaman kazanır. Projeyi burada başlatma sebebimiz yeterli bütçemizin olamaması ve canlı yayınlar ile mevcut kitleye ulaşacak çevremizin olmasından kaynaklıdır.* 

**[PoArt], bu kumarhanenin ortasına inşa edilmiş bir kaledir.**

* 🎰 Kumarhane kağıt oyunlarına dayanır; biz **fiziksel gerçekliğe** dayanıyoruz.
* 🃏 Kumarhane hileye açıktır; biz **şeffaf kanıtlara** açığız.
* ⏳ Kumarhane geçicidir; biz **sanat ve bilimin sonsuzluğuna** odaklıyız.

Bu protokolü kullanan token, sadece bir "coin" değil; arkasında ter, boya, kod ve felsefe barındıran **dijital bir hisse senedidir.**
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


![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

---

## 📑 İçindekiler

1. [Proje Hakkında ve Vizyon](#-proje-hakkında-ve-vizyon)
2. [(Teknolojik İnovasyon)](#-neyi-icat-ettik-teknolojik-inovasyon)
3. [Kullanım Alanları ve Fayda](#-kullanım-alanları-ve-fayda)
4. [Sistem Mimarisi ve Teknik Özellikler](#-sistem-mimarisi-ve-teknik-özellikler)
5. [Yol Haritası: "Trustless" Gelecek](#-yol-haritası-trustless-gelecek)
6. [Rakip Analizi](#-rakip-analizi)
7. [Basın ve Topluluk Kiti](#-basın-ve-topluluk-kiti)

---

**Neden Halka Açık?**
Gerçek güvenlik şeffaflıktan gelir. **Public Registry (Halka Açık Kayıt)** sistemimiz sayesinde, dünyanın herhangi bir yerindeki bir kişi, elindeki dosyanın orijinal olup olmadığını, herhangi bir otoriteye ihtiyaç duymadan saniyeler içinde doğrulayabilir.

---

## 💡 (Teknolojik İnovasyon)

PoArt, sadece bir dosya yükleme sistemi değildir. Üç farklı teknoloji katmanını tek bir potada eriterek yeni bir standart getiren bir **"Adli Kanıt Zinciri" (Forensic Chain of Custody)** motorudur.

### 1. Client-Side Hashing (Maksimum Gizlilik)
Dosyalarınız asla sunucuya yüklenmez. Tarayıcı tabanlı (Client-side) çalışan motorumuz, dosyanın hash'ini (dijital özetini) kendi bilgisayarınızda hesaplar. Sunucuya sadece bu parmak izi ve meta veriler gönderilir. **Gizliliğiniz %100 korunur.**

### 2. Forensic Data Fusion (Adli Güç)
Sıradan bir zaman damgasından (Timestamp) çok daha fazlasıdır. Sistem şu verileri tek bir "Genesis Mühür" içinde birleştirir:
* **Dijital DNA (SHA-512):** Eserin tek bir pikseli değişse bile bozulacak askeri standartta kriptografik imza.
* **Konum & Zaman:** İşlemin yapıldığı milisaniye hassasiyetinde tarih, ülke, şehir ve ilçe verisi.
* **Cihaz Kimliği:** İşletim sistemi, tarayıcı ve cihaz tipi (User-Agent analizi).


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

**Bu proje **[İlhan Art Gallery]** inisiyatifi ile geliştirilmiş olup, kaynak kodları şeffaflık adına halka açıktır.**


**PROTOKOL V1.0 // SHA-512 İLE MÜHÜRLENMİŞTİR.** *© 2025 İLHAN ART | ESERLERİN, GÖRSELLERİN VE FİKİRLERİN TÜM HAKLARI SAKLIDIR.

## 🧬 Protokol Veri Yapısı (JSON Schema)

**Her [PoArt] sertifikası, aşağıdaki standartta üretilen, taşınabilir ve doğrulanabilir bir JSON kimlik kartına sahiptir.**

```json
{
  "$schema": "https://raw.githubusercontent.com/galeri-coder/ilhanart-core/main/protocols/poart-identity-v1.json]"https://raw.githubusercontent.com/galeri-coder/ilhanart-core/main/protocols/poart-identity-v1.json",
  "manifest": {
    "protocol": "[PoArt] Proof of Art",
    "version": "1.0",
    "status": "Production-Ready"
  },
  "identity": {
    "issuer": "Ilhan Art Gallery",
    "location": "Istanbul / Besiktas",
    "archive_vision": "2025 - 3000"
  },
  "asset_data": {
    "title": "Official Whitepaper",
    "fingerprints": {
      "sha256": "e4123f83b44a409d7a43f0897837876dfabb3320db63dadbb34c54281f38a6ba",
      "sha512": "41e5e0d007a2a77b6e0e3ebc548fbaa2788ea265193434f58d23e8c0f5bb20a0835aa850edbadbd8341969cf743fc69fa951f7ed275901fefe0fe7eb1fb83099"
    }
  },
  "official_links": {
    "registry": "[https://www.ilhanart.org/public-registry](https://www.ilhanart.org/public-registry)",
    "evidence": "[https://www.ilhanart.org/identity](https://www.ilhanart.org/identity)"
  },
  "forensics": {
    "origin_ip_masked": "46.1.***.***",
    "device_signature": "Brave (Windows;Monster,Tulpar)...",
    "location": "Istanbul, TR"
  }
}
