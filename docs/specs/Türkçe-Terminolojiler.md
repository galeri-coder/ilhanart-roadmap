# 📚 TERMINOLOJİ & KAVRAMLAR SÖZLÜĞÜ
> **"Bu protokolün dilini anlamak, vizyonunu anlamaktır."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Core Infrastructure

**PoArt Forensic Engine (PFE)**, [PoArt] protokolünün arkasında yatan çekirdek mantığı ve teknik işleyişi temsil eden ana katmandır. Sanat eserinin ham üretim verisini alıp, onu doğrulanabilir ve değiştirilemez bir **dijital kanıta** dönüştüren "adli motor" burasıdır.

### 🧩 Neden "PoArt Forensic"?

- **PoArt (Proof of Art):** Motorun odağı, bir dijital varlığın değerini spekülasyona değil; **kanıtlanabilir üretim sürecine** bağlamaktır.
- **Forensic (Adli Doğrulama):**
  - **Teknik Tanım:** Üretim sürecine ait verilerin (fırça darbeleri, timelapse, loglar) manipüle edilmediğini doğrulamaya yönelik algoritma ve kayıt zinciri yaklaşımı.
  - **Felsefi Katman:** Yapay zekanın "anlık çıktı" üretimine karşı; **insanın zaman, efor ve karar bedeli** içeren üretimini ölçülebilir bir gerçekliğe dönüştürme iddiası.

> Not: Blokzincir (örn. Solana) entegrasyonu, PFE'nin çekirdeği değil; doğrulama/registry için ayrıca tanımlanacak bir **Chain Anchor Layer** olarak ele alınır.

### 🛠️ v1.0 Teknik Kapsamı

**PoArt Forensic Engine (PFE) v1.0**, karmaşık finansal modeller yerine şu **3 ana sütun** üzerine inşa edilmiştir:

1. **Hashing & Sealing (Mühürleme):**  
   PFE, Evidence Pack içindeki tüm öğeleri (eser dosyası, video, JSON/log, imza vb.) deterministik olarak işleyip tekil **NotarySeal** değerini üretir.

   **Çekirdek kavramlar (v1.0):**
   - **FileHash (eser parmak izi):** Eser dosyasının baytlarından üretilen hash.
   - **EvidenceRoot (kanıt paketi kökü):** Evidence Pack'in bütünlüğünü temsil eden kök özet (Merkle root veya kanonik manifest hash).
   - **NotarySeal (nihai mühür / PFE Output):** EvidenceRoot + zaman + imza birleşiminden üretilen son mühür.

   **Formüller (yatırımcıya net görünür biçimde):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   > Not: PFE çıktısı olarak kastedilen değer **NotarySeal**'dir. (Önceki isimlendirmedeki "Sol Ate Output" burada **NotarySeal** ile eşlenmiştir.)

2. **Indexing (Arşivleme):**  
   Hangi cüzdanın, hangi tarihte, hangi eser için **Labor Proof (Emek Kanıtı)** sunduğunu; şeffaf ve sorgulanabilir bir kayıt katmanına işler.  
   *(Bu katman veritabanı olabilir; zincir entegrasyonu ise ayrıca "Chain Anchor Layer" olarak tanımlanır.)*

3. **Verification (Doğrulama):**  
   Bir eserin orijinalliği sorgulandığında PFE, ham kanıtları yeniden işler; hesaplanan **EvidenceRoot / NotarySeal** değerlerinin arşivdeki kayıtla eşleşip eşleşmediğini matematiksel kesinlikle test eder.

---

### 🧮 PoArt Değer Teoremi (The Value Theorem)

[PoArt] protokolü, bir dijital varlığın değerini ($V$) sübjektif piyasa algısıyla değil; **üretim sürecinin fiziksel gerçekliğiyle** ilişkilendirir.

Yapay Zeka (AI), sonucu anında vererek ($t \to 0$) süreci yok eder. [PoArt] ise değeri; **zaman, emek ve irade** bileşenlerinin birikimi olarak ele alır.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Değişkenlerin Tanımı

- **$\int dt$ (Süreç Birikimi):**  
  Değer, anlık bir "çıktı" (output) değildir; $t_{\text{start}}$ ve $t_{\text{end}}$ arasında biriken bir **süreçtir**. Süre azaldıkça (AI üretimi), entegralin sonucu 0'a yakınsar.

- **$P_{\text{labor}}(t)$ (Anlık Emek Gücü):**  
  Üretim anında harcanan zihinsel ve fiziksel efor yoğunluğunu temsil eder. Kanıtlanabilir efor arttıkça, integrand büyür.  
  > Not: Bu terim, pratikte "ölçülebilir/kanıtlanabilir emek sinyalleri" üzerinden normalize edilebilir.

- **$I_{\text{agency}}(t)$ (İrade Katsayısı):**  
  Üreticinin risk alma ve karar verme kapasitesidir. $0$ ile $1$ arasında bir değer alır.
  - **AI ($I \approx 0$):** Komutları uygular, risk almaz, bedel ödemez.
  - **İnsan ($I \to 1$):** Karar değiştirir, tereddüt eder, risk alır.

- **$U_{\text{irreversible}}$ (Geri Döndürülemez Tekillik):**  
  Dijital üretimde geri alma (`Ctrl+Z`) mümkünken; fiziksel üretimde (tuvale sürülen boya, yontulan mermer, canlı yayındaki jest) geri dönüş yoktur. Bu **geri döndürülemezlik**, eserde "tekillik" (non-fungible karakter) yaratan ek bir terimdir.


### 🔎 Vaka Analizi: AI "Anlık Çıktı" vs. İnsan "Kanıtlı Süreç"

Aşağıdaki senaryo, **PoArt Değer Teoremi**'nin pratikte nasıl işlediğini ve neden AI üretimlerinin [PoArt] standardında düşük skor aldığını gösterir.

#### Senaryo A: AI ile 10 Saniyede Görsel Üretimi

- **Süre ($\Delta t$):** $10$ saniye (süreç yok denecek kadar az)
- **Emek Gücü ($P_{\text{labor}}$):** $1$ birim (sadece komut yazma)
- **İrade Katsayısı ($I_{\text{agency}}$):** $0.01$ (risk yok, bedel yok)
- **Geri Döndürülemezlik ($U_{\text{irreversible}}$):** $0$ (geri alınabilir / kopyalanabilir)

**Sonuç:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Yorum:** Çıktı kusursuz olsa bile; süreç yaşanmadığı ve irade/risk barındırmadığı için [PoArt] değeri $0$'a yakınsar.

#### Senaryo B: Canlı Yayında 6 Saatlik Fiziksel Üretim

- **Süre ($\Delta t$):** $6$ saat ($21{,}600$ saniye)
- **Emek Gücü ($P_{\text{labor}}$):** $0.5$ birim (fiziksel ve zihinsel eforun sürekliliği)
- **İrade Katsayısı ($I_{\text{agency}}$):** $0.9$ (karar değiştirme, risk alma, geri dönüşsüz seçimler)
- **Geri Döndürülemezlik ($U_{\text{irreversible}}$):** $>0$ (fiziksel izler geri alınamaz)

**Sonuç:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Yorum:** Süreç uzadıkça ve irade (risk) arttıkça değer kümülatif olarak artar. $U_{\text{irreversible}}$ terimi ise eserde "tekillik" (non-fungible karakter) yaratan ek bir katkıdır.

---

### ✅ Sonuç: Değerin İspatla Kilitlenmesi (Proof-Bound Value)

Bu teorem, [PoArt]'ın değer iddiasını bir "beğeni" veya "piyasa anlatısı" olmaktan çıkarıp **ispatlanabilir bir üretim gerçeğine** bağlar.

1. **Süreç Olmadan Değer Oluşmaz:**  
   AI, anlık çıktıda ($t \to 0$) süreci yok eder. Süreç penceresi daraldıkça integralin sonucu matematiksel bir zorunlulukla küçülür:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **İrade ve Risk Çarpandır:**  
   [PoArt], yalnızca "harcanan süreyi" değil; o süredeki gerçek karar, risk ve bedel katmanını da ölçer. Risk almayan (AI) bir üretimin değeri düşüktür:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Tekillik, Pazarlama Değil Fiziksel Bir Kanıttır:**  
   Fiziksel üretimde geri alınamaz izler (tuval darbesi, mermer kırığı), dijitaldeki `Ctrl+Z` mantığının dışındadır. Bu geri döndürülemezlik ($U_{\text{irreversible}}$), eseri ontolojik olarak tekilleştirir.

> **🔐 ÖZET:** Değer teoremi ölçüm olarak belirsiz gözükse de (gerçek hayatta %100 karşılığı tam ölçülemese bile) bu formülün amacı; değişkenlerin kurgusunu ve yönünü göstermektir. AI çağında nadir olan şey "görüntü" değil; **kanıtlanabilir emek, zaman ve iradedir.** [PoArt], bu kıtlığı ölçer ve **Evidence Pack** ile tesciller.

### 🏛️ "Engine" (Motor) Kavramının Önemi

Pump.fun veya benzeri platformlardan çıkan token'lar, çoğu zaman yalnızca birer **"erişim bileti"** niteliğindedir. **PoArt Forensic Engine (PFE)** ise o biletin hangi hakları koruduğunu, emeğin nasıl kayıt altına alınacağını ve sanatın/bilimin/teknolojinin nasıl kalıcılaştırılacağını belirleyen **anayasal mantık katmanıdır.**

> **Not:** Bizim bu projeyi Pumpfun'da başlatmamızın sebebi yeterli likidite ve yeterli takipçi sayısına sahip olamadığımız içindir. Mevcut datayı kullanmak stratejik olarak en kaliteli olmasa da en doğru hamleydi diyebiliriz. Bütçe ve imkanlardan bağımsız olarak bu motorun mantığını GitHub üzerinde tanımlamak, projenin sadece bir finansal spekülasyon değil, uzun vadeli bir **yazılım altyapısı** ve **dijital bir milli kütüphane** vizyonu olduğunu kanıtlar.

---

## 🎨 [PoArt] EMEK KANITI PROTOKOLÜ (Proof of Art Protocol v1.0)

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

### 1) Canlı Kimlik Kanıtı (Live Identity Proof)

- **Sorun:** Kripto dünyası, kimliği belirsiz anonim kurucuların (Dev'lerin) parayı toplayıp projeyi terk etmesiyle doludur.
- **[PoArt] Çözümü:** Üretici, sadece kimlik kartını değil, **üretim anındaki varlığını** kanıtlar. Bu; önceden kaydedilmiş videolarla değil, toplulukla etkileşime girilen ve anlık spesifik taleplerin yerine getirildiği canlı yayın seanslarını içerir.  
  (Örn: *"Tuvalin sağ köşesine bugünün tarihini ve güncel blok numarasını yaz"*)
- **Motto:** *"Botlar resim yapabilir ama botlar terlemez ve doğaçlama yapamaz."*

### 2) Emek ve Süreç Kanıtı (Labor & Process Proof)

- **Sorun:** 2 saniyede üretilen AI (Yapay Zeka) görselleri ile 2 ayda yapılan yağlı boya tablonun dijital dünyada aynı "jpeg" muamelesi görmesi.
- **[PoArt] Çözümü:** Eserin "hamilelik ve doğum" süreci kayıt altına alınır. Eskiz aşamaları, boya katmanları, harcanan kümülatif saatler ve sanatçının o eseri yaratırken yaşadığı fiziksel süreç belgelenir. Bu, tokene **"Zaman Maliyeti" (Time Cost)** ekler. Bir varlığın üretimi ne kadar zorsa, değeri o kadar sağlamdır.

### 3) Estetik Değer Kanıtı (Aesthetic Value Proof)

- **Sorun:** "Meme" kültürünün estetiği ve sanatsal derinliği yok sayarak sadece anlık komediye odaklanması ve bunun sonucunda oluşan kısa ömürlü "Hype" projeler.
- **[PoArt] Çözümü:** Proje, akademik sanat standartlarına, renk teorisine, kompozisyon kurallarına ve malzeme bilgisine (Impasto, Doku vb.) sahip olmalıdır. İçerik sadece güldürmemeli; izleyicide hayranlık uyandırmalı ve **koleksiyon değeri** taşımalıdır.

### 4) Fikirsel İnovasyon (Conceptual Novelty)

- **Sorun:** Birbirinin kopyası olan, yaratıcılıktan uzak binlerce köpek/kedi coin'i.
- **[PoArt] Çözümü:** Proje; sanat, bilim, felsefe veya teknolojiyi anlamlı bir yapıda birleştiren yeni bir köprü kurmalıdır.  
  (Örn: Klasik Davud heykeli ile kripto piyasa verilerini birleştirmek; bunun üzerinden insan algısının "taşa dönüşmesi" fikrini işlemek ve bunu bilimsel kaynaklarla temellendirebilmek.)  
  Eser, sadece görsel bir şölen değil; aynı zamanda **Bilim, Felsefe veya Teknoloji** üzerine düşündüren entelektüel bir meydan okuma olmalıdır.

> [!ÖNEMLİ]
> **Referans Örnek (Las Palmitas Etkisi):** Meksika'nın suçla boğuşan Las Palmitas mahallesinde, 200'den fazla ev devasa bir gökkuşağı şölenine dönüştürülmüştür. Bu estetik müdahale sonucunda mahalledeki suç oranları belirli ölçüde düşmüş, gençler çeteler yerine sanatla ilgilenmeye başlamıştır. Estetik değişim, insanların çevrelerine ve birbirlerine olan saygısını (Social Cohesion) yeniden kodlamıştır.
>
> **Beklenti:** [PoArt] listesine girecek bir proje; tıpkı yukarıdaki örnekte olduğu gibi, salt görsel estetikten öte sosyolojik, bilimsel veya felsefi bir neden-sonuç ilişkisi barındırmalıdır. Para ile satın alınamayacak yegâne varlık "Zaman" olduğu için, bu protokolde zaman bir teminat olarak stake edilerek kanıtlanmalıdır. Projenin fikirsel temeli o kadar güçlü ve evrensel olmalıdır ki; seneler sonra olası bir CTO (Community Take Over) senaryosunda bile, topluluk bu mirası devralarak projenin yenilikçi potansiyelini otonom bir şekilde sürdürebilmelidir.

### 5) Algoritmik Olmayan İrade (Non-Algorithmic Agency)

- **Sorun:** Kusursuz ama ruhsuz, birbirini tekrar eden dijital üretimler.
- **[PoArt] Çözümü:** İnsanın hata yapabilen, risk alan ve duygusal dalgalanmalar yaşayan özgün iradesi eserde hissedilmelidir. Fırça darbelerindeki belirsizlik, malzemenin beklenmedik tepkileri ve sanatçının anlık kararları, eseri "Makine Üretimi"nden ayıran **Biyolojik İmza**dır.

---

## c) Doğrulama & Anti-Sahtecilik Mekanizması

Bu sistem, projenin sadece "başlangıçta" değil, "sonsuza kadar" güvenilir ve canlı kalmasını sağlar.

### 📦 Kanıt Paketi (Evidence Pack - The Digital Twin)

Her [PoArt] sertifikalı eserin arkasında, yatırımcıların indirebileceği şifreli ve zaman damgalı bir veri paketi bulunur:

- **RAW Video Kayıtları:** Üretim anının kesintisiz ham görüntüleri.
- **Metadata Analizi:** Dosyanın oluşturulma tarihi, kullanılan cihaz bilgileri ve konum verileri.
- **Fiziksel Referanslar:** Eserin fiziksel dünyada var olduğuna dair kanıtlar  
  (Örn: Eserin yanında duran güncel gazete veya o anki blokzincir verisi).

> *Tutarlılık notu:* "kanıt paketi" ifadesi, önceki bölümlerdeki **Evidence Pack → EvidenceRoot → NotarySeal** hattına bağlanır; yani paketin bütünlüğü doğrulanabilir bir mühürle temsil edilir.

### 🔄 365 Günlük Yenileme (The Sustainability Protocol)

- **Devrimsel Özellik:** Kripto projelerinde "Dev" (Geliştirici), tokeni piyasaya sürer ve genelde 1-2 ay sonra ortadan kaybolur (Soft Rug). [PoArt] bunu imkansız kılar.
- **Kural:** "Verified Artist" (Doğrulanmış Sanatçı) statüsü ömür boyu değildir. Sadece **1 yıl** geçerlidir.
- **İşleyiş:** Sanatçı/Geliştirici, her 365 günde bir, topluluğa **yeni, büyük ve kanıtlanabilir bir eser** sunmak zorundadır.
- **Örnek Senaryo:** 2026'da projeyi başlattınız. 2027 Ocak ayında sistem "Kanıt Süresi Doldu" uyarısı verir. Eğer sanatçı yeni bir sergi, yeni bir fiziksel eser veya yeni bir teknolojik entegrasyon sunmazsa, projenin "Güven Rozeti" düşer.
- **Sonuç:** Bu sistem, **içeriğin asla güncelliğini yitirmemesini** ve yatırımcının *"Geliştirici hala burada mı?"* korkusu yaşamamasını sağlar. Proje, yaşayan bir stüdyoya dönüşür.

### 🚩 Kırmızı Bayrak (Red Flag Protocol)

**Topluluk veya algoritmalar tarafından tespit edilen herhangi bir sahtecilik (AI kullanımı, çalıntı eser, manipüle edilmiş video) durumunda:**

1. Sertifika derhal **"İPTAL" (VOID)** olarak işaretlenir.
2. Kanıt paketleri halka açık şekilde **"Sahte"** olarak etiketlenir.
3. Proje, [PoArt] kara listesine alınır. Bu, merkeziyetsiz bir dünyada **itibarın tek para birimi** olduğu gerçeğini pekiştirir.

---

## d) Sonuç: Kumarhane Değil, Müze

**Pump.fun ve Merkeziyetsiz Borsalar (DEX) şu an malesef birer kumarhanedir; ışıklar yanıp söner, herkes hızlı kazanç peşindedir ve kasa (dolandırıcılar) her zaman kazanır. Projeyi burada başlatma sebebimiz yeterli bütçemizin olmaması ve canlı yayınlar ile mevcut kitleye ulaşacak çevremizin olmasından kaynaklıdır.**

**[PoArt], bu kumarhanenin ortasına inşa edilmiş bir kaledir.**

- 🎰 Kumarhane kağıt oyunlarına dayanır; biz **fiziksel gerçekliğe** dayanıyoruz.
- 🃏 Kumarhane hileye açıktır; biz **şeffaf kanıtlara** açığız.
- ⏳ Kumarhane geçicidir; biz **sanat ve bilimin sonsuzluğuna** odaklıyız.

**Bu protokolü kullanan token, sadece bir "coin" değil; arkasında ter, boya, kod ve felsefe barındıran dijital bir hisse senedidir.**

---

## 🗳️ 6) YÖNETİŞİM VE KAMU SİCİLİ (Governance & Public Registry)

**Bu bölümün amacı şudur: [PoArt] standardını "kişilere güven" düzleminden çıkarıp, kayıt + doğrulama + topluluk denetimi ile sürdürülebilir bir kamu altyapısına dönüştürmek.**

### 6.1 Public Registry (Kamu Sicili)

- **Public Registry:** Tüm onaylı veriler `ilhanart.org/registry` (veya GitHub Registry) adresinde kaydedilir.

**Kayıt mantığı (önerilen standart):**
- Sicile giren her kayıt, minimum şu doğrulanabilir çekirdek alanları taşır:
  - `certificate_id` (okunabilir referans)
  - `notary_seal` (nihai mühür; PFE çıktısı)
  - `evidence_root` (kanıt paketi kökü)
  - `file_sha256` / `file_sha512` (eser dosyası parmak izi)
  - `creator` (metin adı) + mümkünse `creator_wallet` (token-gated kimlik için)
  - `created_at` (zaman damgası)
  - `status` (active / void) + `void_reason` (varsa)
  - `visibility` (private / masked / public)
- Sicilin iki katmanı bulunabilir:
  - **1)** İnsan-okur indeks (web listeleme / arama / filtre)
  - **2)** Makine-okur manifest (JSON kayıtları; PFE doğrulaması için)

**Buradaki "kayıt", PFE'nin Evidence Pack → EvidenceRoot → NotarySeal zinciriyle doğrulanabilir hale gelir. Sicil, "iddia" değil doğrulama hedefi sunar.**

---

### 6.2 %40 Topluluk Vetosu (Token-Gated Governance)

- **%40 Topluluk Vetosu:** Statü kazanılmadan bir ay önce oylama başlar; **Token-Gated (Solana-Verified)** topluluğun %40 itirazı başvuruyu geçersiz kılar.

**Oylama akışı (önerilen net süreç):**
- **Başvuru penceresi:** Aday proje "PoArt aday kaydı" açar (aday kayıtları "pending" statüsünde görünür).
- **İnceleme süresi:** 30 gün boyunca topluluk delilleri inceler (Evidence Pack + canlı yayın kayıtları + metadata).
- **Token-gated doğrulama:** Oy kullanımı, Solana üzerinde doğrulanmış cüzdanlar ile yapılır (ör. belirli token/NFT sahipliği + wallet signature).
- **Veto kuralı:** Oyların %40'ı **itiraz (NO / VETO)** ise başvuru reddedilir.
- **Şeffaflık:** Oylama sonucu sicilde "decision record" olarak saklanır (tarih, oran, snapshot kimliği).

---

### 6.3 Metadata Sync (Fiziksel Dünya ile Eşleşme)

- **Metadata Sync:** Sicildeki teknik veriler fiziksel varlıkla %100 eşleşmek zorundadır.

**"%100 eşleşme"yi teknik olarak tanımlamak (önerilen açıklık):**
- **Minimum eşleşme (zorunlu):**
  - Sicildeki `file_sha256/sha512` ile eldeki dosyanın hash'i **birebir aynı** olmalıdır.
  - Sicildeki `notary_seal` yeniden üretildiğinde (Evidence Pack varsa) **birebir aynı** olmalıdır.
- **Fiziksel referans eşleşmesi (kanıt türü):**
  - Canlı yayında gösterilen fiziksel eser + tarih/blok referansı gibi kanıtlar, Evidence Pack ile tutarlı olmalıdır.
- **Gizlilik uyumu:**
  - `masked` görünürlükte IP/konum gibi alanlar **maskeleme standardına uygun** yayımlanır.

---

### 6.4 İtiraz, İnceleme ve İptal (Dispute & Revocation)

Sicil, yalnızca "onay" mekanizması değil; **sahteciliğe karşı yaşayan bir denetim** mekanizmasıdır.

- İtiraz başlatıldığında kayıt **"review"** moduna alınabilir.
- Sahtecilik tespit edilirse `status: void` olarak işaretlenir ve gerekçe eklenir:
  - `void_reason` (AI kullanımı / çalıntı / manipülasyon vb.)
  - `revoked_at` (iptal zamanı)
- İptal kararının kaynağı sicilde açıkça görünür:
  - topluluk oylaması / yetkili kurul / adli inceleme notu (hangisi uygulanıyorsa)

> **Bu kısım, "Red Flag Protocol" bölümündeki VOID kavramının sicil üzerindeki karşılığıdır.**

---

### 6.5 Örnek Sicil Kaydı (Makine-okur)

```json
{
  "certificate_id": "POART-AB12CD34",
  "status": "active",
  "visibility": "masked",
  "created_at": "2026-01-09T12:34:56.000Z",
  "asset": {
    "title": "Untitled",
    "creator": "Anonymous",
    "file_sha256": "e4123f83b44a409d7a43f0897837876dfabb3320db63dadbb34c54281f38a6ba",
    "file_sha512": "41e5e0d007a2a77b6e0e3ebc548fbaa2788ea265193434f58d23e8c0f5bb20a0..."
  },
  "proof": {
    "evidence_root": "7f8a9b2c...",
    "notary_seal": "9d3e5a1f..."
  },
  "governance": {
    "decision": "approved",
    "veto_threshold": 0.40
  }
}
```

---

## 7) 🔐 TEKNİK MÜHÜR (NOTARY SEAL)

**PoArt Forensic Engine (PFE) v1.0** tarafından üretilen sarsılmaz mühür algoritması:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Dijital Noter & Adli Kanıt Protokolü (Beta v1.0)

> **"Kültür, sermayeden büyüktür. Eserlerinizi bugünden koruyun, yarına taşıyın."**

---

## Neden Halka Açık?

Gerçek güvenlik şeffaflıktan gelir. **Public Registry (Halka Açık Kayıt)** sistemimiz sayesinde, dünyanın herhangi bir yerindeki bir kişi; elindeki dosyanın orijinal olup olmadığını, herhangi bir otoriteye ihtiyaç duymadan saniyeler içinde doğrulayabilir.

---

## 🧩 Neden Birden Fazla "Görünürlük Modülü" Var?

Kodun en kritik kısmı burası (visibility select menüsü). Bu seçenekler, kullanıcıların **"Mahremiyet vs. Şeffaflık"** dengesini kurmasını sağlıyor:

### 🔒 Özel (Private)

- **Senaryo:** Sanatçı henüz eseri yayınlamak istemiyor ama tarih damgası vurup "ben bunu bu tarihte yapmıştım" diye kanıtlamak istiyor.
- **Kodun Yaptığı:** Veriyi veritabanına yazar ama `visibility: "private"` etiketi basar. İleride "Public Read" politikası yazarken `WHERE visibility = 'public'` diyerek bu kayıtları halktan gizleyebilirsin.

### 🕶️ Maskeli (Masked)

- **Senaryo:** Sanatçı şeffaflık istiyor ama ev adresinin (IP konumu) bulunmasından korkuyor.
- **Kodun Yaptığı:** JavaScript tarafında `maskIP` ve `maskLoc` fonksiyonları çalışır. IP adresini `88.241.***.***` şekline, konumu `***/Turkey` şekline çevirir ve veritabanına sansürlenmiş halini gönderir.
- **Güvenlik:** Bu çok zekice, çünkü sansür sunucuda değil, kullanıcının tarayıcısında yapılır. Yani Supabase bile gerçek konumu göremez.

### 🌍 Herkese Açık (Public)

- **Senaryo:** Tam şeffaflık. [PoArt] standardı gereği, eserin nerede, ne zaman, hangi ağdan üretildiği açıkça beyan edilir.

---

## 💡 Teknolojik İnovasyon

PoArt, sadece bir dosya yükleme sistemi değildir. Üç farklı teknoloji katmanını tek bir potada eriterek yeni bir standart getiren bir **"Adli Kanıt Zinciri" (Forensic Chain of Custody)** motorudur.

**Bu bölümde "motor" olarak anlatılan katman, önceki terminolojiyle PoArt Forensic Engine (PFE) çekirdeğine karşılık gelir.**

### 1) Client-Side Hashing (Maksimum Gizlilik)

Dosyalarınız asla sunucuya yüklenmez. Tarayıcı tabanlı (Client-side) çalışan motorumuz, dosyanın hash'ini (dijital özetini) kendi bilgisayarınızda hesaplar. Sunucuya sadece bu parmak izi ve meta veriler gönderilir. **Gizliliğiniz %100 korunur.**

> **"asla sunucuya yüklenmez" ifadesi, eser dosyası için geçerlidir; sistemin doğrulama/registry ihtiyacı olan alanlar (hash + metadata) ayrı değerlendirilir.**

### 2) Forensic Data Fusion (Adli Güç)

Sıradan bir zaman damgasından (Timestamp) çok daha fazlasıdır. Sistem şu verileri tek bir "Genesis Mühür" içinde birleştirir:

- **Dijital DNA (SHA-512):** Eserin tek bir pikseli değişse bile bozulacak askeri standartta kriptografik imza.
- **Konum & Zaman:** İşlemin yapıldığı milisaniye hassasiyetinde tarih, ülke, şehir ve ilçe verisi.
- **Cihaz Kimliği:** İşletim sistemi, tarayıcı ve cihaz tipi (User-Agent analizi).

---

## 🛡️ Kullanım Alanları ve Fayda

Bir sanatçı, yazar veya tasarımcıysanız, "Bunu ben daha önce yapmıştım" demek yetmez, kanıtlamanız gerekir.

**PoArt ile mühürlediğiniz bir eser:**

- **Matematiksel Kanıt:** Dosyanızın tek bir pikseli bile değişse sistem bunu anlar. Manipülasyon imkansızdır.
- **Hukuki Dayanak:** Eserin hangi tarihte, hangi şehirde, hangi cihazdan mühürlendiği kayıt altındadır.
- **Anında Sertifika:** Saniyeler içinde size özel, QR kodlu ve mühürlü bir **"Varlık Kimlik Sertifikası"** üretir.

---

## ⚙️ Sistem Mimarisi ve Teknik Özellikler

Sistem, "Serverless" (Sunucusuz) bir mimari üzerinde, yüksek performans ve ölçeklenebilirlik odaklı tasarlanmıştır.

| Katman | Teknoloji | Açıklama |
|--------|-----------|----------|
| **Kriptografi** | SHA-256 & SHA-512 | Çift katmanlı özetleme - askeri standart |
| **Veri Tabanı** | Supabase (PostgreSQL) | JSONB veri yapısı, RLS policies |
| **Adli Veri** | ipapi.co API | IP/Konum/Zaman üçlemesi |
| **Rendering** | html2canvas + jsPDF | Client-side PNG/PDF üretimi |
| **Frontend** | Vanilla JavaScript | Sıfır framework dependency |
| **Güvenlik** | Client-side hashing | Dosya asla sunucuya yüklenm ez |

### Öne Çıkan Özellikler

| Özellik | Detay | Rakiplerde? |
|---------|-------|-------------|
| **Drag & Drop UI** | Dosya sürükle-bırak, anında önizleme | ❌ Çoğunda yok |
| **Multi-Format Export** | PNG, JSON, PDF - tek tıkla | ⚠️ Sınırlı |
| **Real-Time Preview** | Sertifika canlı önizleme | ❌ Yok |
| **Privacy Controls** | Private/Masked/Public seçenekleri | ❌ Yok |
| **Client-Side Hashing** | Dosya asla sunucuya gitmiyor | ✅ Sadece birkaçında |
| **Forensic Metadata** | IP, konum, cihaz, zaman - hepsi bir arada | ❌ Parçalı |
| **QR Verification** | Anında doğrulama QR kodu | ⚠️ Kısıtlı |
| **Rate Limiting** | Spam koruması (RLS + Client) | ❌ Çoğunda yok |

---

## 🗺️ Yol Haritası: "Trustless" Gelecek

Şu anki sürüm **(Beta v1.0)**, son kullanıcıya maksimum hız, kolay arayüz ve ücretsiz erişim sağlamak için optimize edilmiştir. Ancak nihai vizyonumuz, veritabanı yöneticisinin (bizim) bile müdahale edemeyeceği bir yapıya geçmektir.

### Faz 1: Beta (Şu An Yayında)

- **Altyapı:** Cloud Database (Supabase).
- **Amaç:** Hız, UX (Kullanıcı Deneyimi) bariyerlerini kaldırmak ve adaptasyon. "Sürtünmesiz" güvenlik sağlamak.

### 🚀 Faz 2: (Backend / Edge Function Gerektirenler)

Bu faz, sistemin tamamen "Client-Side" çalışan yapısından, daha güvenli ve yönetilebilir bir "Server-Side Authority" yapısına geçişini kapsar.

| Madde | Ne Kazandırır? | Tech Stack | Öncelik |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Function** | Spam engeli + API Key güvenliği | Supabase Edge (Deno) | 🔴 Yüksek |
| **Wallet İmzası** | Kriptografik kimlik doğrulama | Solana Wallet Adapter | 🟡 Orta |
| **IPFS/Arweave Yedekleme** | Merkeziyetsiz değişmezlik | IPFS SDK + Pinata | 🟢 Düşük |
| **Revocation Mekanizması** | Sahte sertifika iptali | DB Schema Update | 🔴 Yüksek |
| **Audit Log** | Adli sorgulama kaydı | Custom logs tablosu | 🟡 Orta |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | 🟢 Düşük |
| **DID Integration** | Decentralized Identity | ION/Ceramic | 🟢 Düşük |

### Faz 3: Tam Merkeziyetsizlik (Uzun Vade)

| Özellik | Hedef | ETA |
|---------|-------|-----|
| **Blockchain Registry** | Ethereum/Solana on-chain kayıt | Q4 2026 |
| **DAO Governance** | Topluluk yönetimi | Q1 2027 |
| **Multi-Chain Support** | Polygon, Arbitrum, Base | Q2 2027 |
| **Legal Recognition** | Türk mahkemelerinde geçerlilik | 2027-2028 |
| **API for Developers** | Public API endpoint | Q3 2026 |

---

## 📊 Rakip Analizi (Güncellenmiş)

PoArt, mevcut çözümlerin eksiklerini tamamlayan "Sweet Spot" (En ideal nokta) üzerine konumlanmıştır.

| Özellik | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Maliyet** | 🆓 Ücretsiz | 🆓 | 💰 Ücretli | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Çok Kolay | ❌ CLI | ⚠️ Orta | ⚠️ Orta | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Canlı | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Mod | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Gizlilik | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Tam | ❌ | ❌ | ⚠️ Kısıtlı | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Anlık | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Turkish Support** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Açıklama:**
- ✅ : Tam destek / mevcut
- ⚠️ : Kısıtlı / ücretli planlarda
- ❌ : Yok / desteklenmiyor
- 🔄 : Roadmap'te (geliştirilmekte)
- 🆓 : Tamamen ücretsiz
- 💰 : Ücretli / abonelik gerekli

### Rakiplerin Eksikleri, PoArt'ın Güçlü Yönleri

| Eksi | Rakipler | PoArt |
|------|----------|-------|
| **Kullanım Zorluğu** | CLI, API bilgisi, cüzdan gerekli | Sürükle-bırak, 3 tıkla biter |
| **Maliyet Bariyeri** | $50-500/ay abonelik | %100 ücretsiz |
| **Gizlilik** | Dosya sunucuya yüklenir | Client-side, dosya asla gitmiyor |
| **Forensic Veri** | Sadece timestamp | IP, konum, cihaz, zaman - hepsi |
| **Türkçe Destek** | Yok veya çok kısıtlı | Native dil desteği |
| **Açık Kaynak** | Kapalı kutu | GitHub'da tüm kod açık |

---

## 🧬 Protokol Veri Yapısı (JSON Schema)

**Her [PoArt] sertifikası, aşağıdaki standartta üretilen, taşınabilir ve doğrulanabilir bir JSON kimlik kartına sahiptir.**

```json
{
  "$schema": "https://raw.githubusercontent.com/galeri-coder/ilhanart-core/main/protocols/poart-identity-v1.json",
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
    "registry": "https://www.ilhanart.org/public-registry",
    "evidence": "https://www.ilhanart.org/identity"
  },
  "forensics": {
    "origin_ip_masked": "46.1.***.***",
    "device_signature": "Brave (Windows;Monster,Tulpar)...",
    "location": "Istanbul, TR"
  }
}
```

---

## 🔬 Teknik Derinlik: Mühür Algoritması

### NotarySeal Üretim Süreci

```javascript
// 1. FileHash hesaplama (client-side)
const fileBuffer = await file.arrayBuffer();
const sha256 = await crypto.subtle.digest('SHA-256', fileBuffer);
const sha512 = await crypto.subtle.digest('SHA-512', fileBuffer);

// 2. Forensic data toplama
const forensics = {
  ip: await fetch('https://ipapi.co/json/').then(r => r.json()),
  device: navigator.userAgent,
  timestamp: new Date().toISOString()
};

// 3. EvidenceRoot oluşturma
const evidenceRoot = sha512(
  fileHash + forensics.ip + forensics.timestamp
);

// 4. NotarySeal üretimi
const notarySeal = sha512(
  evidenceRoot + signerSignature + timestamp
);
```

### Doğrulama Akışı

```javascript
// 1. Kullanıcı dosyayı yeniden hash'ler
const userFileHash = sha512(file);

// 2. Sistemden orijinal hash çekilir
const { sha512: originalHash } = await fetchFromRegistry(certId);

// 3. Matematiksel karşılaştırma
if (userFileHash === originalHash) {
  return "✅ Orijinal - Değiştirilmemiş";
} else {
  return "❌ Sahte - Dosya manipüle edilmiş";
}
```

---

## 📈 Kullanım İstatistikleri (2026 Q1 Hedefleri)

| Metrik | Hedef | Durum |
|--------|-------|-------|
| **Toplam Sertifika** | 1,000 | 🔄 İlerleme |
| **Aktif Kullanıcı** | 500 | 🔄 İlerleme |
| **Doğrulama Sayısı** | 5,000 | 🔄 İlerleme |
| **Uptime** | %99.9 | ✅ Aktif |
| **Avg Response Time** | <200ms | ✅ Optimal |

---

## 🌍 Topluluk & Destek

- **GitHub:** [github.com/galeri-coder/ilhanart-core](https://github.com/galeri-coder/ilhanart-core)
- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** info@ilhanart.org

---

## 🙏 Katkıda Bulunanlar

PoArt protokolü, açık kaynak topluluğunun katkılarıyla gelişmeye devam ediyor.

**Katkı yapmak için:**
1. Fork yapın
2. Feature branch oluşturun (`git checkout -b feature/amazing-feature`)
3. Commit atın (`git commit -m 'Add amazing feature'`)
4. Push yapın (`git push origin feature/amazing-feature`)
5. Pull Request açın

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Kültür, Sermayeden Büyüktür*

## 🧾 License

MIT License © 2026 İlhan Art Gallery Initiative  
See [LICENSE](LICENSE) for full terms.

---

## 💬 Credits


![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Bu proje [İlhan Art Gallery] inisiyatifi ile geliştirilmiş olup, kaynak kodları şeffaflık adına halka açıktır.**

**PROTOKOL V1.0 // SHA-512 İLE MÜHÜRLENMİŞTİR.**

*© 2026 İLHAN ART | ESERLERİN, GÖRSELLERİN VE FİKİRLERİN TÜM HAKLARI SAKLIDIR.*
---
