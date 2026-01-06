# 📜 Protocol Terminology & Technical Lexicon
> **Protocol Version:** 1.0 (Stable)  
> **Network Vision:** 2025 - 3000 Archive  
> **Ecosystem:** [PoArt] & [FPP]  
> **Status:** Active Documentation

---

## 🏛️ 1. Pillars of the Protocol (Temel Protokoller)

### **[PoArt] Proof of Art (v1.0)**
* **Tanım:** Bir sanat eserinin sadece nihai sonucunu değil, tüm **yaratım sürecini (process)** teknik verilerle doğrulayan ana protokoldür. 
* **Çözdüğü Sorun:** Günümüzde üretken yapay zeka (Generative AI) araçlarının artışıyla birlikte, gerçek insan emeğinin dijital ortamda kanıtlanamaz hale gelmesi ve sanatın "meta" değerinin düşmesi.
* **Nasıl Çalışır?** Sanatçı, eseri oluştururken her aşamayı kapsayan "Evidence Pack" (Kanıt Paketi) verilerini sisteme sunar. Protokol, bu verileri zaman damgalı olarak blokzincir üzerinde mühürler.
* **Örnek Senaryo:** Bir sanatçı 40 saatlik bir Impasto tablo yapıyorsa, bu 40 saatin yayın logları, fırça darbelerinin timelapse kayıtları ve dijital parmak izleri [PoArt] filtresinden geçer. Sadece "bitmiş resim" değil, o resmin arkasındaki "40 saatlik insan emeği" tescillenir.

### **[FPP] Foundational Pillar Protocol (v1.0)**
* **Tanım:** Ekosistemin ekonomik, yönetimsel ve toplumsal "taşıyıcı kolonlarını" (pillars) inşa eden, sadakati ve uzun vadeli katılımı ödüllendiren ana sistemdir.
* **Çözdüğü Sorun:** Kripto ekosistemindeki "parayı basan düdüğü çalar" mantığının yarattığı adaletsizlik ve projeyi terk eden spekülatörlerin ekosisteme zarar vermesi.
* **Nasıl Çalışır?** Kullanıcıların ekosistem içindeki karar verme ve yönetim ağırlığı, cüzdanlarındaki varlık miktarından ziyade, bu varlığı ne kadar "sağlam" (pillar) ve uzun süreli tuttuklarına göre belirlenir.
* **Örnek Senaryo:** Sisteme bugün 1 milyon token ile giren bir "balina", 1 yıldır sistemde 100 token tutan sadık bir "patron"dan daha düşük bir yönetim ağırlığına (voting power) sahip olabilir.

---

## 📊 2. Economic & Governance Metrics (Ekonomik Metrikler)

### **TWAB (Time-Weighted Average Balance)**
* **Tanım:** Zaman-Ağırlıklı Ortalama Bakiye. Bir cüzdanın ekosistem içindeki gerçek "ağırlığını" hesaplayan matematiksel formüldür.
* **Matematiksel Model:**
    $$TWAB = \sum (Bakiye \times Zaman)$$
* **Çözdüğü Sorun:** "Whale Manipulation" (Balina Manipülasyonu). Varlıklı birinin kritik bir oylamadan hemen önce borsadan yüklü miktarda alım yaparak kararı kendi lehine manipüle etmesini engeller.
* **Örnek Hesaplama:** * **A Şahsı:** 1.000.000 tokenı oylamadan 1 saat önce aldı. ($Zaman \approx 0$). Gücü: **Düşük.**
    * **B Şahsı:** 100 tokenı 365 gündür cüzdanında tutuyor. ($Zaman = 365$). Gücü: **Yüksek.**
    * **Sonuç:** Sistem, B şahsının sadakatini A şahsının parasına tercih eder.

### **Logarithmic Power Scoring (Logaritmik Skor)**
* **Tanım:** Güç artışını doğrusal (lineer) değil, logaritmik olarak hesaplayan matematiksel adalet mekanizmasıdır.
* **Matematiksel Model:**
    $$Score = \log_{10}(TWAB + 1)$$
* **Çözdüğü Sorun:** Kapitalist güç yoğunlaşması. Çok büyük varlık sahiplerinin topluluğun sesini tamamen bastırmasını engeller.
* **Örnek Hesaplama:** * 10 tokenı olanın gücü $log_{10}(10) = \mathbf{1}$ ise,
    * 1.000.000 tokenı olanın gücü $log_{10}(1,000,000) = \mathbf{6}$ olur.
    * **Adalet Notu:** Bir kişi diğerinden 100.000 kat daha zengin olsa bile, yönetimde sadece 6 kat daha güçlü olabilir. Bu, küçük yatırımcıların birleşerek devleri dengelemesini sağlar.

---

## 🛡️ 3. Security & Validation (Güvenlik ve Doğrulama)

### **Millennium Vault (10-Year Epochs)**
* **Tanım:** Varlıkların 10 yıllık periyotlarla (Epoch) kilitlendiği, ekosistemin en üst düzey "itibar kasası"dır.
* **Çözdüğü Sorun:** Kısa vadeli kâr maksimizasyonu hedefleyen spekülatörlerin, projenin 2025-3000 arasındaki uzun vadeli vizyonuna zarar verecek kararlar alması.
* **Cevap:** Projenin geleceğine dair en kritik kararları ancak varlığını 10 yıl boyunca kilitleyen ve "Founding Patron" statüsü kazanan kişiler verebilir. Bu, projenin kurucu iradesini yüzyıllar boyunca korur.

### **Evidence Pack (Kanıt Paketi)**
* **Tanım:** Bir sanat eserinin [PoArt] protokolü tarafından onaylanması için gereken zorunlu teknik veri setidir.
* **Zorunlu İçerik:**
    1.  **Live Logs:** Üretim anındaki 7/24 canlı yayın ve sunucu kayıtları.
    2.  **Process Timelapse:** Eserin ilk fırça darbesinden son haline kadar olan kare kare hızlandırılmış videosu.
    3.  **Digital Fingerprint:** Sanatçının cüzdanıyla imzalanmış, verinin manipüle edilmediğini kanıtlayan hash kodu.
* **Çözdüğü Sorun:** "Bu eser gerçekten bir insan eliyle ve büyük bir emekle mi yapıldı?" sorusuna verilen teknik, reddedilemez ve şeffaf yanıttır.

### **Sybil & Flash-loan Protection**
* **Tanım:** Blokzincir üzerindeki anlık saldırı ve sahte hesap (bot) manipülasyonlarına karşı kurulan matematiksel barikattır.
* **Çözdüğü Sorun:** Bir saldırganın binlerce bot hesap açarak sistemi ele geçirmeye çalışması (Sybil) veya anlık kredi (Flash-loan) çekerek geçici bir güç oluşturması.
* **Cevap:** [FPP] içindeki TWAB filtresi, anlık hareketlerin zaman ağırlığını "sıfır" gördüğü için bu saldırganların sistemde hiçbir hükmü kalmaz. Zaman satın alınamaz tek metadır.

---

## 🗳️ 4. Governance (Yönetim)

### **Veto Threshold (%40)**
* **Tanım:** Bir sanat eserinin veya protokol değişikliğinin reddedilmesi için gereken minimum topluluk "Hayır" oyu oranıdır.
* **Çözdüğü Sorun:** Çoğunluğun diktatörlüğü ve sisteme düşük kaliteli veya şüpheli içeriklerin sızması.
* **Cevap:** Topluluğun %40'ı bir kayıt için "Bu [PoArt] standartlarına uymuyor" derse, o kayıt mühürlenmez. Bu, kalitenin ve şeffaflığın topluluk tarafından korunmasıdır.

### **Digital Notary (Dijital Noter)**
* **Tanım:** [PoArt] verilerini süzgeçten geçiren, doğruluğunu onaylayan ve Public Registry'ye (Kamu Arşivi) mühürleyen akıllı kontrat mekanizmasıdır.
* **Çözdüğü Sorun:** Onay sürecinde "insan" faktöründen kaynaklanan taraflılık, rüşvet veya hata riskini ortadan kaldırır.
* **Sonuç:** Bir sanat eseri Dijital Noter tarafından onaylandığı an, 3000 yılına kadar silinmeyecek ve değiştirilemeyecek olan evrensel sanat arşivindeki yerini alır.

## 🏛️ 5. Validation & Persistence (Doğrulama ve Süreklilik)

### **365 Günlük Kesintisiz Cold Wallet Doğrulaması**
* **Tanım:** Bir sanat eserinin veya [FPP] kapsamındaki varlığın, mülkiyet güvenliğinin en üst seviyesi olan "Soğuk Cüzdanlarda" (Cold Wallet) tam bir takvim yılı (365 gün) boyunca hiçbir transfer işlemi görmeden tutulması zorunluluğudur.
* **Çözdüğü Sorun:** 1. **Wash Trading:** Varlıkların sürekli el değiştirerek suni fiyat ve hacim oluşturması.
    2. **Spekülatif Baskı:** Sanatın bir yatırım aracından ziyade "kültürel bir miras" olarak konumlanmasını sağlamak.
    3. **Güvenlik Zafiyeti:** Sıcak cüzdanların (Hot Wallet) hacklenme riskine karşı ekosistemi korumak.
* **Nasıl Çalışır? (Teknik İşleyiş):** Akıllı kontrat (Smart Contract), varlığın cüzdana girdiği blok numarasını ve zaman damgasını mühürler. Sistem 7/24 zincir üstü (on-chain) izleme yapar. Eğer varlık 365 gün dolmadan tek bir transfer işlemi dahi görürse, bağlı olduğu [PoArt] doğrulama statüsü anında "Verified" (Doğrulanmış) durumundan "Revoked" (İptal) durumuna çekilir.
* **Örnek Senaryo:** Bir koleksiyoner, "Founding Patron" ünvanını korumak istiyorsa, varlığını Ledger veya Trezor gibi bir donanım cüzdana çeker. Eğer 200. günde nakit paraya sıkışıp varlığın bir kısmını satarsa, o güne kadar biriktirdiği tüm "Zaman Ağırlıklı Ortalama Bakiye" (TWAB) puanları sıfırlanır ve "yeşil ışığı" söner.

### **Evidence Pack: Trinity of Proof (Üçlü Kanıt Mekanizması)**
* **Tanım:** [PoArt] v1.0 standartları çerçevesinde, bir eserin yapay zeka tarafından değil, bir insan tarafından, belirli bir zaman diliminde ve fiziksel/dijital bir emekle üretildiğini kanıtlayan sarsılmaz veri kümesidir.
* **Bileşenler ve Teknik Detaylar:**
    1. **Canlı Yayın (Live Stream Logs):** Sanatçının üretim sürecini topluluğa açık ve kesintisiz şekilde gerçekleştirdiğini kanıtlayan ham video kayıtlarıdır. (Örn: YouTube veya Twitch platformlarında yapılan "İlhan Art Live" yayınlarının sunucu taraflı kayıtları).
    2. **Process Timelapse (Evrim Videosu):** Eserin "hiçlikten" varoluşa giden yolculuğunun kare kare kaydıdır. Bu, eserin katman katman nasıl inşa edildiğini teknik olarak analiz etmeyi sağlar. (Örn: 100 saatlik bir Impasto dokusunun 3 dakikalık yüksek çözünürlüklü teknik özeti).
    3. **Technical Logs (İşlem Günlükleri):** Dijital fırça darbelerinin koordinatları, baskı şiddeti, kullanılan araçların zaman çizelgesi ve dosya meta-verilerinin (metadata) blokzincir hashleri.
* **Çözdüğü Sorun:** Yapay zekanın (AI) saniyeler içinde "sanat" taklidi yaptığı bir dünyada, gerçek sanatçının "yıllar süren eğitimini" ve "günler süren emeğini" teknik olarak ayırt edilemez olmaktan kurtarır.

### **Yıllık Yenileme Zorunluluğu (365-Day Renewal)**
* **Tanım:** Public Registry'de yer alan her kaydın, güncelliğini ve meşruiyetini koruması için her yıl yapılması gereken "Dijital Kalp Atışı" (Heartbeat) onay işlemidir.
* **Çözdüğü Sorun:** 1. **Ölü Veri:** Sahibi tarafından terk edilmiş veya erişimi kaybedilmiş cüzdanların arşivi kirletmesi.
    2. **Pasif Koleksiyonculuk:** Sanatın sadece "alınan ve unutulan" bir nesneye dönüşmesini engelleyerek, sanatçı ile hami (patron) arasındaki bağı dinamik tutmak.
* **Nasıl Çalışır?** Her bir [PoArt] sertifikasının bir "Valid Until" (Geçerlilik Tarihi) vardır. Bu süre dolmadan 30 gün önce sistem uyarı verir. Sanatçı veya mülkiyet sahibi, eserin hala elinde olduğunu ve [PoArt] standartlarına uygunluğun devam ettiğini yeni bir dijital imza ile tescil etmek zorundadır.
* **Örnek Senaryo:** 2025'te tescil edilen "İlhan Art" serisi bir eser, 2026'da sahibi tarafından "Renewal" işlemine tabi tutulmazsa, Public Registry'de statüsü "Legacy Archive" (Eski Arşiv) olarak güncellenir. Bu, eserin sahte olduğu anlamına gelmez ancak "aktif olarak doğrulanan" statüsünü ve buna bağlı yönetim haklarını kaybetmesi demektir.

---

## 🗳️ 6. Decentralized Supervision (Merkeziyetsiz Denetim)

### **Topluluk Veto Mekanizması (%40 Eşik)**
* **Tanım:** [PoArt] sistemine dahil edilmek istenen yeni bir kaydın veya protokol değişikliğinin, topluluğun nitelikli azınlığı tarafından durdurulabilmesini sağlayan demokratik güvenlik bariyeridir.
* **Neden %40 Eşiği Belirlendi?**
    - Geleneksel sistemlerdeki %51 (mutlak çoğunluk) kuralı, "çoğunluğun diktatörlüğüne" ve ufak bir oy farkıyla manipülasyona açıktır. 
    - %40 eşiği, topluluğun neredeyse yarısına yakınının "Burada bir şüphe var" demesini ciddiye alır. Eğer topluluğun %40'ı "Hayır" diyorsa, sistem o eseri şüpheli olarak işaretler ve "Digital Notary" mühürleme işlemini kalıcı olarak durdurur.
* **Çözdüğü Sorun:** 1. **Sybil Attacks:** Saldırganların bot hesaplarla oylamaları ele geçirmesi.
    2. **Collusion (Anlaşmalı Oylama):** Bir grup insanın bir araya gelerek sahte bir eseri "Verified" yapmaya çalışması.
* **Örnek Senaryo:** Bir kullanıcı, yapay zeka ile ürettiği bir görseli "kendi emeğim" diyerek [PoArt] için başvuruda bulundu. Ancak topluluk, sunulan "Evidence Pack" içinde tutarsızlıklar fark etti. Elinde [FPP] tutan gerçek sanat destekçileri (Patrons), oylama güçlerini kullanarak %40 barajını geçerlerse, o görsel sisteme asla "Sanat Eseri" olarak mühürlenemez. Logaritmik skorlama (log10) sayesinde, bir balinanın bu %40'lık barajı tek başına parayla aşması matematiksel olarak imkansız hale getirilmiştir.

---
## 🏛️ 7. The Michelangelo Framework (Meritocracy Engine)

### **Michelangelo // The Meritocracy Philosophy**
* **Tanım:** İlhan Art ekosisteminin sıralama ve itibar motorudur. Sistemin bir "Zenginler Listesi" (Rich List) olmasını engelleyen, liyakat tabanlı bir hiyerarşi modelidir.
* **Çözdüğü Sorun:** Geleneksel kripto projelerinde cüzdanında en çok para olanın en tepede yer alması adaletsizliği.
* **Cevap:** Michelangelo motoru şu sloganla çalışır: *"You cannot buy your way to the top."* (Zirveyi satın alamazsın; inşa etmeli, çevirmeli ve küratörlük yapmalısın).
* **Örnek:** Milyonlarca dolarlık bir balina, sisteme sadece para koyduğu için asla 1 numaralı "Patron" olamaz. Zirve, yıllarca sisteme kültürel katkı sunan (Translation, Curation, Building) ve zamanını veren kişilere aittir.

### **Status Formula: Time x Contribution**
* **Tanım:** Bir "Patron"un nihai skorunu (Final Score) belirleyen temel çarpan mekanizmasıdır.
* **Matematiksel Model:**
  $$\text{Status} = \text{Holding Time} \times \text{Cultural Contribution}$$
* **Bileşenler:**
    1. **Holding Time:** Varlığın soğuk cüzdanda (Cold Wallet) bozulmadan durduğu toplam gün sayısı. (Örn: Görseldeki gibi 1,420 Gün).
    2. **Cultural Contribution:** Sanatçının veya hamisinin ekosisteme kattığı somut değer (Çeviriler, teknik geliştirmeler, sergi destekleri).
* **Çözdüğü Sorun:** Sadece cüzdanda para tutmanın "pasif" bir eylem olması. Sistem, "hem tutan hem de üreten" kişiyi ödüllendirir.

---

## 📊 8. Cultural Multipliers & Ranking Levels

### **Cultural Multiplier (Kültürel Çarpanlar)**
* **Tanım:** Patronların final skoruna eklenen, belirli görevlerin tamamlanmasıyla kazanılan bonus puan sistemidir.
* **Uygulama Alanları:**
    - **Translation (JP/TR/EN):** Bilimsel, felsefi veya sanatsal metinlerin İlhan Art standartlarında çevrilmesi (Örn: +4,500 Pts).
    - **Curation:** Registry üzerindeki eserlerin kalite kontrolü ve veto süreçlerine aktif katılım.
    - **Infrastructure:** Ekosistemin teknik dökümantasyonuna veya kod altyapısına yapılan katkılar.
* **Örnek:** Bir Patron 1000 gün boyunca varlık tuttuysa (Base Score), buna ek olarak yaptığı bir çeviriyle +4,500 Pts "Kültürel Çarpan" alarak sıralamada binlerce kişinin önüne geçebilir.

### **Tier Classifications (Rütbe Seviyeleri)**
Sistem, topluluk içindeki ağırlığı 3 ana elit seviyeye ayırır:
1. **Legendary (Top 10):** Ekosistemin en üst düzey kurucu iradesi. Sadece en yüksek puanlı 10 cüzdan bu unvana ve en yüksek "Veto" gücüne sahiptir.
2. **Senior (Top 50):** Sistemin ana taşıyıcı kolonları (Pillars). Karar alma mekanizmalarında kritik söz hakkına sahiptirler.
3. **Veteran (Top 100):** Ekosistemin uzun vadeli ve güvenilir doğrulayıcıları.
* **Önemli Kural:** Bu rütbeler statik değildir; bir Patron katkıyı bırakırsa veya varlığını cüzdandan çıkarırsa, alttan gelen aktif Patronlar tarafından rütbesi elinden alınır.

---

## 🛡️ 9. Cut-off Thresholds (Eşik Bariyerleri)

### **Entry Thresholds (Giriş Barajları)**
* **Tanım:** Belirli bir rütbeye veya Global Registry listesine girebilmek için aşılması gereken matematiksel puan sınırlarıdır.
    - **Legendary Threshold:** 92,500 Pts (Bu puanın altındakiler ne kadar parası olursa olsun Top 10'a giremez).
    - **Top 100 Entry:** 45,000 Pts (Global listeye adını yazdırmak için gereken minimum liyakat puanı).
* **Çözdüğü Sorun:** Sistemin "kalabalıklaşmasını" ve kalitesizleşmesini engeller. Zirveye giden yol, her geçen gün zorlaşan bir matematiksel bariyerle korunur.

### **Network TWAB (Global Zaman Ağırlığı)**
* **Tanım:** Tüm ekosistemin toplam zaman-ağırlıklı bakiyesidir (Örn: 4.2M Network TWAB).
* **Fonksiyonu:** Sistemin toplam "güven hacmini" gösterir. Bu rakam ne kadar yüksekse, [PoArt] protokolü o kadar saldırılamaz ve manipüle edilemez hale gelir.
* **24h New Entries:** Sisteme son 24 saatte dahil edilen yeni [PoArt] kayıtlarını gösteren canlı veri akışıdır.
---

## 🏛️ 10. Intellectual Framework (Entelektüel Yapı)

### **IPOW: Intellectual Proof of Work (Emek Stake Etme)**
* **Tanım:** Sadece maddi varlık tutmanın ötesinde, sisteme "yüksek nitelikli insan emeği" (çeviri, sanat üretimi, teknik dökümantasyon, eğitim) katmayı zorunlu kılan itibar motorudur.
* **Çözdüğü Sorun:** "Pasif Stake" sorunu. Diğer projelerde kullanıcılar sadece token tutarak (passive holding) ödül kazanırken, [FPP] ekosisteminde pasiflik bir dezavantajdır.
* **Nasıl Çalışır?** Kullanıcının temel skoru (TWAB), yaptığı somut kültürel katkılarla çarpılır. Sisteme "emek" enjekte edilmediği sürece, sadece para tutarak "Legendary" statüsüne ulaşmak matematiksel olarak imkansız hale getirilir.
* **Örnek:** Bir kullanıcı 1 milyon token tutsa bile, eğer tek bir çeviri yapmamış veya sanatsal kanıt (PoArt) sunmamışsa; 100 token tutan ama aktif olarak döküman çeviren bir "Emekçi" (Worker) tarafından yönetimde saf dışı bırakılabilir.

### **Intellectual Honesty Filter (Entelektüel Dürüstlük ve Quiz Mekanizması)**
* **Tanım:** Herhangi bir hak talebinde (claim) veya yönetim oylamasında, kullanıcının konuyu gerçekten anlayıp anlamadığını ölçen "Zorunlu Entelektüel Emek Kanıtı" aşamasıdır.
* **Çözdüğü Sorun:** 1. **Copy-Paste Kültürü:** Kullanıcıların neyi oyladığını bilmeden sadece "Evet" veya "Hayır" demesi.
    2. **AI Spam:** Yapay zekanın otomatik olarak claim işlemlerini gerçekleştirmesi.
* **Nasıl Çalışır?** Sistem, claim öncesi kullanıcıya dökümantasyon veya protokol kuralları hakkında rastgele, dinamik sorular yöneltir. Bu soruları doğru yanıtlayamayan kullanıcı, oylama veya ödül haklarını o dönem için kaybeder. Amaç "kopyalamayı" değil, "anlamayı" ödüllendirmektir.

---

## 🛡️ 11. Advanced Sybil Resistance (Gelişmiş Saldırı Koruması)

### **The Turnstile Mechanism (Turnike Sistemi)**
* **Tanım:** Ekosisteme giriş için belirlenen "Minimum Katılım Eşiği"dir (Örn: 250 ILHAN Token).
* **Felsefesi:** *"Duvar değil, turnike."* Bu sistem, gerçek kullanıcıların içeri girmesini engellemek için değil, sıfır maliyetli bot saldırılarını (Sybil Attack) ekonomik olarak verimsiz hale getirmek için kurulmuştur.
* **Çözdüğü Sorun:** Bir saldırganın milyonlarca boş cüzdan açarak sistemi "zombi cüzdanlarla" doldurması ve oylamaları manipüle etmesi.
* **Örnek:** 10,000 sahte hesap açmak isteyen bir bot operatörü, her hesap için 250 token tutmak zorunda kaldığında, bu saldırının maliyeti saldırganın elde edeceği faydadan çok daha yüksek bir seviyeye çıkar ve saldırı matematiksel olarak durur.

### **Zombie Wallet Filter (Aktif Claim Zorunluluğu)**
* **Tanım:** Belirli periyotlarla (aylık/yıllık) cüzdanın "hayatta ve aktif" olduğunu kanıtlamasını gerektiren filtreleme sistemidir.
* **Çözdüğü Sorun:** Arşivin ve yönetim listelerinin (Top 100), anahtarı kaybolmuş veya terk edilmiş "ölü" adreslerle dolması.
* **Cevap:** Aktif claim yapmayan adresler, skorları ne kadar yüksek olursa olsun "Global Registry" listesinden otomatik olarak düşürülür. Bu sayede sistem, sadece "yaşayan ve üreten" bireylerden oluşan dinamik bir yapı olarak kalır.

---

## 🧬 12. Generational Legacy & Governance (Nesiller Arası Miras ve Yönetim)

### **Generational Inheritance (Nesiller Arası Miras/Varis Belirleme)**
* **Tanım:** 4 yıl (1460 gün) boyunca kesintisiz "Legendary" statüsünü koruyan üyelerin, kazandıkları itibar skorunu ve haklarını bir sonraki nesle (varise) devretme yetkisidir.
* **Vizyon:** İlhanArt'ın "Bin Yıllık Vizyon" (2026-3000) hedefini gerçekleştiren köprüdür.
* **Çözdüğü Sorun:** Bir kişinin ölümü veya aktifliğini yitirmesiyle, on yıllar boyunca biriktirdiği "kültürel değerin" ekosistemden silinip gitmesi.
* **Uygulama:** Sadece 4 yıllık sadakatini kanıtlamış olanlar "Varis Belirleme" ekranına erişebilir. Bu işlem on-chain olarak mühürlenir ve bir "itibar mirası" oluşturulur.

### **Parliamentary Governance Rights (Parlamenter Söz Hakkı)**
* **Tanım:** Skor seviyesine göre (Legendary, Patron, Member) cüzdanlara atanan kademeli yönetim ve denetim yetkileridir.
* **Hiyerarşi Detayları:**
    1. **Legendary (100k+ Skor):** "Tam Parlamenter Söz Hakkı". Sistemin anayasası, fee yapıları ve stratejik vizyon üzerinde doğrudan "Kurucu İrade" yetkisine sahiptirler.
    2. **Patron (50k-99k Skor):** "Küratör ve Denetçi". Eser listeleme onayları, oylamalar ve topluluk önerileri üzerinde aktif rol oynarlar.
    3. **Member (<50k Skor):** Topluluk önerileri sunma ve küçük ölçekli kararlara katılım hakkı.
* **Çözdüğü Sorun:** Kaotik ve kontrolsüz oylamalar yerine, ekosisteme en çok emek vermiş olanların en kritik kararları aldığı "Liyakate Dayalı Demokrasi" modelini getirir.

## 🌍 13. Cultural Privilege Layers & Real-World Integration
> **Not:** Bu bölümde belirtilen ayrıcalıklar, 2026-2030 yol haritası kapsamında kademeli olarak hayata geçirilecek olan "Gelecek Vizyonu" (Future Roadmap) bileşenleridir.

### **The Annual Exhibition Right (Yıllık Galeri Hakkı)**
* **Tanım:** [PoArt] üzerinden doğrulanmış yüksek skorlu sanatçıların ve patronların, fiziksel **İlhan Art Gallery** mekanında yılda bir kez, bir hafta süreyle kendi kürasyonlarını veya eserlerini sergileme hakkıdır.
* **Çözdüğü Sorun:** Bağımsız sanatçıların fiziksel galeri alanlarına erişim zorluğu ve yüksek sergileme maliyetleri.
* **Nasıl Çalışır?** Skor bazlı sıralamada belirli bir eşiği (Threshold) geçen kullanıcılar, takvim üzerinden rezervasyon yaparak galeri alanını "itibar puanları" ile kullanabilirler. Bu, sanatın demokratikleşmesidir.

### **Dynamic Art Pricing (JSON-Linked Discounts)**
* **Tanım:** Fiziksel veya dijital sanat eserlerinin satın alım sürecinde, cüzdanınızdaki [FPP] statüsünün bir indirim anahtarı (JSON Metadata) olarak çalışmasıdır.
* **Teknik Detay:** Eserlerin satış kontratı, alıcının cüzdanındaki "Status" verisini JSON kodu üzerinden okur.
* **Uygulama:** - **Legendary:** %50+ indirim.
    - **Patron:** %30 indirim.
    - **Member:** %10 indirim.
* **Önemli Felsefe:** Bu sistemde bir eseri ucuza almanın yolu "pazarlık" değil, ekosisteme sunulan "kanıtlanmış emek"tir.

### **Physical Ecosystem Integration (Mağaza ve Partner Entegrasyonu)**
* **Tanım:** Sıralamadaki statünün, fiziksel dünyadaki anlaşmalı işletmelerle (Kitabevleri, Kafeler, Kültür Merkezleri) dijital olarak entegre edilmesidir.
* **Örnek Ortaklıklar:**
    - **Kitabevleri:** FPP dökümantasyonunu ve felsefesini destekleyen yayınevlerinden, statüye göre özel indirim kodları (Claimable Codes).
    - **Kafeler & Sosyal Alanlar:** Anlaşmalı mekanlarda QR kod okutularak statüye özel "Patron Kahvesi" veya indirimli hizmet erişimi.
* **Çözdüğü Sorun:** Dijital itibarın gerçek hayatta bir karşılığının olmaması. Bu sistemle, İlhan Art kartvizitiniz değil, cüzdanınızdaki emeğinizdir.

### **Labor Over Capital: Meritocratic Access (Emek > Sermaye)**
* **Tanım:** Sistemin ana adalet formülüdür. Maddi imkanları kısıtlı olan ancak "Kültürel Katkı" (Translation, Code, Art, Education) üreten bireylerin, çok fazla token tutan pasif balinalardan daha fazla avantaja sahip olmasıdır.
* **Matematiksel Mantık:** $$\text{Hak Talebi (Claim Right)} \propto \text{Kültürel Puan} + \log_{10}(\text{Bakiye})$$
* **Sonuç:** Bu sistemde, 250 token (Turnstile limit) tutup yoğun çeviri ve sanat katkısı sağlayan bir öğrenci, 100.000 token tutup hiçbir şey üretmeyen birinden çok daha fazla indirim, sergi hakkı ve ücretsiz kahve/kitap erişimine sahip olacaktır.
* **Felsefe:** *"Emek, en büyük sermayedir."*

---

## 📅 14. Roadmap & Future Notes
Bu dökümantasyonda yer alan tüm maddeler, İlhan Art ekosisteminin 2026'dan 3000 yılına doğru uzanan vizyonunun birer yapı taşıdır. Her sürüm güncellemesi (v1.1, v1.2 vb.) bu ayrıcalıkların teknik entegrasyon süreçlerini (API bağlantıları, fiziksel POS entegrasyonları vb.) içerecektir.

---
