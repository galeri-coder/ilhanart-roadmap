
---

```markdown
# 🏛️ [PoArt] Araştırma Sentezi & Protokol Mantığı (TR)
> **Doküman Kimliği:** `REF-LOGIC-2026-V2.3`  
> **Durum:** `ARŞİVLENDİ & GÜVENLİ`  
> **Depo:** `galeri-coder/ilhanart-roadmap`  
> **Son Bağlantı Kontrolü:** `2026-01-06`  
> **Özet (SHA-512):** `<BU_DOSYANIN_SHA512_DEĞERİNİ_BURAYA_EKLE>`

---

## 0) Bu doküman neden var?
[PoArt], sanat-merkezli (art-first) bir protokoldür: kültürel değerin kıt altyapısı olarak **dikkati** (attention) ele alır.

Bu araştırma sentezi “bakın ne kadar zekiyiz” türü bir bibliyografya değildir.  
Bu metin; aşağıdaki üç alanı:

- **İnsan bilişi** (zaman algısı, bilişsel yük, dikkat kontrolü)
- **Dijital dikkat ekonomisi** (anti-scroll mimarisi, derin çalışma teşvikleri)
- **Davranışsal piyasa mekanikleri** (dikkat-çeken varlıklar, zihinsel muhasebe, istikrarsızlık dinamikleri)

[PoArt] içindeki belirli mekanizmalara bağlayan bir **tasarım mantığı defteri** (design logic ledger) niteliğindedir:

- **Minimalist Terminal**
- **Katkı Gücü (CP)**
- **365 Gün Kuralı**
- **Anti-Hype Filtresi**
- **Deterministik Kıtlık Eğrileri**
- **Michelangelo Denetimi**
- **Dijital Noter / Kanıt Paketleri**

---

## 1) Bağlantı Bütünlüğü Politikası (DOI-öncelikli)

### 1.1 İstikrar kuralları
Aşağıdaki öncelik hiyerarşisi kullanılır:

1) **DOI** (tercih edilir, kalıcı çözücü)  
2) **Resmî kurumsal arşiv** (üniversite, devlet, tanınmış arşiv)  
3) **Yayınevi kayıt sayfası** (DOI yoksa resmî kitap/sayfa kaydı)  
4) **İkincil indeksler** (yalnızca üsttekiler yoksa)

### 1.2 İddia sınıflandırması (kritik)
Her kaynak aşağıdaki üç etiketten biriyle işaretlenir:

- **Kanıt (Hakemli / Ampirik):** ölçülebilir etkileri doğrudan test eder  
- **Çerçeve (Kavramsal / Açıklayıcı):** mekanizmaları açıklar; UI reçetesi değildir  
- **Tasarım Gerekçesi (Kitap / Sentez):** niyet ve tehdit modellemesini destekler; “ispat” değildir  

Bu sınıflandırma, protokol yazımındaki yaygın bir hatayı önler:
> iyi fikirleri, deneysel kanıt varmış gibi sunmak.

---

## 2) Değişiklik Kaydı (Changelog)

### 2.1 V2.1 → V2.2
- Flaherty (1999) için kırık NYU Press kayıt bağlantısı düzeltildi.
- Carr (2010) için hatalı W. W. Norton ISBN bağlantısı düzeltildi.
- Cal Newport “/books/” yönlendirmesi yerine daha stabil, doğrudan Deep Work sayfasına geçildi.

### 2.2 V2.2 → V2.3 (tutarlılık & izlenebilirlik)
- Zakay & Block (1995) “kanonik atfı”, kurumsal PDF dayanak metaverisiyle (sempozyum/proceedings bağlamı) eşleştirildi.
- Kaynak listesinden sonraki bölümler yeniden numaralandırıldı ve başlık seviyeleri GitHub TOC için standartlaştırıldı.
- Son diff kod bloğu GitHub render’ı bozmayacak şekilde doğru kapatıldı.

---

## 🧬 Yürütücü Özet
Bu 10 sütun tek bir birleşik tezi destekler:

**Bir sistem hızı ve yeniliği ödüllendirirse, yüzeysel davranışı üretir.  
Bir sistem doğrulanmış emeği ve sürdürülebilir dikkati ödüllendirirse, kültürel emeği geliştirebilir.**

[PoArt], “yavaş protokol” olarak tasarlanmıştır:
- hype ve botlara direnebilecek kadar yavaş,  
- katkıyı ölçebilecek kadar yapısal,  
- etkileşimde bir sanat eseri hissi yaratacak kadar estetik.

---

## 🧪 Faz I: Zaman Algısı & Bilişsel Yük

### 1) Zakay & Block (1995) - Dikkat Kapısı Modeli (Çerçeve)
**Kategori:** Çerçeve (ampirik zamanlama sonuçlarını yorumlamak için yaygın kullanılan yaklaşım)  
**DOI:** *(mevcut değil / bu proceedings bölümü için güvenilir şekilde atanmış değil; Son Bağlantı Kontrolü 2026-01-06 itibarıyla çözümlenebilir DOI bulunamadı; DOI-öncelikli politika gereği kurumsal arşiv dayanağına düşülür)*  

**Kanonik atıf (dayanakla eşleşen):**  
Zakay, D., & Block, R. A. (1995). *An attentional-gate model of prospective time estimation.*  
Proceedings, **I.P.A. Symposium (Liège, 7–8 November 1994)**, ss. 167–178.

**Stabil kurumsal PDF (önerilen dayanak):**  
https://www.montana.edu/rblock/documents/papers/ZakayBlock1995.pdf

#### Bu kaynak ne söylüyor? (açık dil)
- Prospektif zaman tahmini, **dikkatin nasıl dağıtıldığına** bağlıdır.
- Bilişsel bir “kapı”, zamanlama darbelerinin birikime girişini modüle eder.
- Dikkat dağılımındaki kaymalar, öznel süre yargılarını değiştirir.

#### [PoArt] yorumu (tasarım çerçevesi)
**Yüksek odaklı, görev tanımlı arayüzler; otomatik pilot kaydırmayı kesebilir ve zamanı bilinçli olarak “hissedilen” bir deneyime çevirebilir.**  
[PoArt] Terminalinde dikkat, yenilik kovalamaktan bilinçli incelemeye yönlendirilir: kullanıcı okur, doğrular, karşılaştırır ve kanıt bağlantılı adımlarla taahhütte bulunur. Bu, **zamansal ayrıştırmayı** artırır: oturum “kalınlaşır”, daha bölümlü ve daha bilinçli takip edilir.

Bu, makalenin tek bir UI seçimini “kanıtladığı” iddiası değildir.  
Bu, çerçeveden tasarıma çeviri kuralıdır: *dikkat dağılımı hissedilen süreyi etkiler; bu nedenle yüksek sürtünmeli doğrulama akışları düşük sürtünmeli dürtü davranışını kırmak için kullanılabilir.*

#### Uygulama eşlemesi
- **Bileşen:** `Sol Ate Engine` (UI yoğunluğu + görev segmentasyonu)
- **Mekanizma:** adım adım doğrulama akışı, dikkat tahsisini zorunlu kılar
- **Metrikler (öneri):**
  - doğrulama adımı başına görevde kalma süresi
  - kanıt kontrolü tamamlanma oranı
  - “adıma geri dönüş” davranışı (yeniden okuma = müzakere/tefekkür vekili)

---

### 2) Kahneman (2011) - Sistem 1 / Sistem 2 (Çerçeve)
**Kategori:** Çerçeve (ikili süreç bilişi); UI reçetesi değildir  
**Birincil referans (Kitap):**  
Kahneman, D. (2011). *Thinking, Fast and Slow.*

**Resmî Nobel biyografisi (stabil):**  
https://www.nobelprize.org/prizes/economic-sciences/2002/kahneman/biographical/

#### Bu kaynak ne söylüyor? (açık dil)
- İnsanlar iki genel modda çalışır:
  - **Sistem 1:** hızlı, sezgisel, dürtüsel
  - **Sistem 2:** yavaş, yansıtıcı, emek isteyen
- Birçok hata, Sistem 1 baskınken Sistem 2 devreye girmediğinde ortaya çıkar.

#### Yöntemsel uyarı (çerçeve, ispat değil)
Kahneman burada **kavramsal bir mercek** olarak kullanılır; “[PoArt] UI = X sonucu üretir” gibi doğrudan deneysel ispat olarak değil.  
[PoArt] bu modeli tasarım niyetine çevirir: hype ticaretinde yaygın olan refleks eylemleri azaltmak ve sürtünme, netlik ve doğrulama adımlarıyla bilinçli değerlendirmeyi artırmak.

**Çeviri kuralı:**  
Kahneman *başarısızlık modunu* açıklar.  
[PoArt], ona direnmek üzere *mimari bir karşı-tasarım* tanımlar.

#### Uygulama eşlemesi
- **Bileşen:** `Anti-Hype Filter` + `Minimalist Terminal`
- **Mekanizma:** dürtü tetiklerini azalt, kanıt bağlantılı eylemi zorunlu kıl
- **Metrikler (öneri):**
  - “oku-sonra-eylem” / “okumadan-eylem” olay oranı
  - yönetişim eyleminden önce kanıt paketi inceleme tamamlanması

---

### 3) Flaherty (1999) - Yaşantılanan Zaman & Anlam Yoğunluğu (Tasarım Gerekçesi / Fenomenoloji)
**Kategori:** Tasarım Gerekçesi (sosyoloji/deneyim; anlam-yoğunluğu temeli)  
**Yayınevi kayıt sayfası (stabil):**  
https://nyupress.org/9780814726877/a-watched-pot/

**Referans:**  
Flaherty, M. G. (1999). *A Watched Pot: How We Experience Time.* NYU Press.

#### Bu kaynak ne söylüyor? (açık dil)
- Zaman, yalnızca saat ölçümü değil, yaşantılanan bir fenomendir.
- Anlam, dikkat ve bağlam, sürenin hissedilen dokusunu biçimlendirir.

#### [PoArt] bu kaynağı neden kullanır? (CP konumlandırması)
Flaherty, Katkı Gücü’nün (CP) matematik temeli olarak değil, **fenomenolojik zemini** olarak konumlanır.  
Sanat-merkezli duruşu destekler: kültürel değer, hız metriklerinden değil, sürdürülebilir bilinçli etkileşimden doğar.

CP bir protokol değişkeni olarak işletilecekse, Flaherty mutlaka şu katmanlarla eşleşmelidir:
- ampirik ölçüm seçimleri,
- denetim mantığı,
- kanıt paketi doğrulaması,
- yenileme döngüleri.

[PoArt] yığınında:
- Flaherty, anlam-yoğunluğunun **neden** önemli olduğunu açıklar.
- [PoArt] denetimleri, bu yoğunluğun **nasıl** doğrulanıp ödüllendirileceğini tanımlar.

#### Uygulama eşlemesi
- **Bileşen:** `Katkı Gücü (CP)`
- **Mekanizma:** CP, ham zamandan çok kanıtlanmış katkıyı ağırlıklar
- **Metrikler (öneri):**
  - döngü başına doğrulanmış üretim/artefakt sayısı
  - kanıt paketi bütünlük puanı
  - 365 günlük döngülerde yenileme tutarlılığı

---

## 📱 Faz II: Dijital Dikkat & Bilişsel Kapasite

### 4) Ward ve ark. (2017) - “Brain Drain” (Kanıt)
**Kategori:** Kanıt (hakemli ampirik)  
**DOI:** https://doi.org/10.1086/691462

Ward, A. F., Duke, K., Gneezy, A., & Bos, M. W. (2017). *Brain Drain: The Mere Presence of One’s Own Smartphone Reduces Available Cognitive Capacity.* Journal of the Association for Consumer Research.

#### Bu kaynak ne söylüyor? (açık dil)
- Telefon kullanılmasa bile, yalnızca varlığı bilişsel kapasiteyi azaltabilir.

#### [PoArt] eşlemesi
- **Bileşen:** `Minimalist Terminal`
- **Mekanizma:** “dikkat parazitlerini” azalt; sonsuz kaydırma teşviklerini kaldır
- **Dil notu (aşırı iddiadan kaçın):**
  - “bilişsel kapasite / performans” de; “IQ geri getirir” deme.

---

### 5) Carr (2010) - The Shallows (Tasarım Gerekçesi)
**Kategori:** Tasarım Gerekçesi (sentez kitap; tehdit modelleme)  
**Yayınevi kayıt sayfası (stabil):**  
https://wwnorton.com/books/9780393357820

Carr, N. (2010). *The Shallows: What the Internet Is Doing to Our Brains.* W. W. Norton.

#### [PoArt] eşlemesi
- **Bileşen:** `Statik Blok Mimarisi`
- **Mekanizma:** sonsuz kaydırmayı kaldır; bilinçli okuma akışını maksimize et
- **Protokol niyeti:** yenilik bağımlılığı döngülerine karşı derin dikkati savun

---

### 6) Newport (2016) - Deep Work (Tasarım Gerekçesi)
**Kategori:** Tasarım Gerekçesi (strateji kitap; sürdürülebilir odak teşvikleri)  
**Resmî sayfa (stabil):**  
https://calnewport.com/deep-work-rules-for-focused-success-in-a-distracted-world/

Newport, C. (2016). *Deep Work: Rules for Focused Success in a Distracted World.*

#### [PoArt] eşlemesi
- **Bileşen:** `365 Gün Kuralı`
- **Mekanizma:** sürdürülebilir derinliği ödüllendir; kısa vadeli “turistleri” filtrele
- **Denetim davranışı:** uzun ufuklu döngüler yüzeyselliği caydırır

---

## 📈 Faz III: Davranışsal Piyasa Mekanikleri

### 7) Barber & Odean (2008) - Dikkat-Çeken Varlıklar (Kanıt)
**Kategori:** Kanıt (hakemli ampirik)  
**DOI:** https://doi.org/10.1093/rfs/hhm079

Barber, B. M., & Odean, T. (2008). *All That Glitters: Individual Investors and Attention-Grabbing Stocks.* Review of Financial Studies.

#### Bu kaynak ne söylüyor? (açık dil)
- Bireysel yatırımcılar “dikkat çeken” varlıklara çekilir (haber, aşırı hareket, anormal hacim).

#### [PoArt] eşlemesi
- **Bileşen:** `Anti-Hype Filtresi`
- **Mekanizma:** dikkat gürültüsünü bastır; doğrulanmış katkı sinyallerini yükselt
- **Tasarım kuralı:** dikkat bir değer metriği değil, saldırı yüzeyidir

---

### 8) Thaler (1985) - Zihinsel Muhasebe (Çerçeve)
**Kategori:** Çerçeve (davranışsal iktisat; daha geniş literatürde ampirik olarak temellenmiş)  
**DOI:** https://doi.org/10.1287/mksc.4.3.199

Thaler, R. H. (1985). *Mental Accounting and Consumer Choice.* Marketing Science.

#### [PoArt] eşlemesi
- **Bileşen:** `Miras Sermayesi` çerçevesi
- **Mekanizma:** zihinsel kovayı “hızlı kazanç”tan “kültürel koruma”ya kaydır
- **Tasarım kuralı:** adlandırma, UI ritüelleri ve denetim yapısı aktif zihinsel hesabı şekillendirir

---

### 9) Minsky (1992) - Finansal İstikrarsızlık Hipotezi (Çerçeve)
**Kategori:** Çerçeve (makro istikrarsızlık dinamikleri)  
**Resmî enstitü arşivi (stabil):**  
https://www.levyinstitute.org/publications/the-financial-instability-hypothesis/

Minsky, H. P. (1992). *The Financial Instability Hypothesis.* Levy Economics Institute (Working Paper No. 74).

#### Bu kaynak ne söylüyor? (açık dil)
- İstikrar, risk almayı teşvik edebilir ve kırılgan yapılar doğurabilir (hedge → spekülatif → ponzi kayması).

#### [PoArt] eşlemesi (kapsam sınırlı iddia)
[PoArt], “tüm piyasaları stabilize eder” iddiasında değildir.  
[PoArt], kendi kültürel ekonomisi içinde ponzi-benzeri kaymayı azaltmayı hedefler; bunu şu araçlarla yapar:
- meşruiyet altyapısı olarak doğrulanmış kültürel emek,
- deterministik kıtlık eğrileri,
- yavaş yönetişim döngüleri ve denetim yenilemeleri.

---

### 10) Wu (2016) - Dikkat Tacirleri (Tasarım Gerekçesi)
**Kategori:** Tasarım Gerekçesi (tarihsel sentez)  
**Yayınevi kayıt sayfası (stabil):**  
https://www.penguinrandomhouse.com/books/234876/the-attention-merchants-by-tim-wu/

Wu, T. (2016). *The Attention Merchants.* Penguin Random House.

#### [PoArt] eşlemesi
- **Bileşen:** `Michelangelo Denetimi` + `Dijital Noter`
- **Mekanizma:** dikkati platformlardan geri al; değeri doğrulanmış artefaktlara yeniden sabitle
- **Tasarım kuralı:** dikkat, kiralanan değil; üreticiler ve topluluklarca “sahip olunan” olmalıdır

---

## 3) [PoArt] Protokol Mantığı Özeti (Neden İşler? Taslak)

### 3.1 Başarısızlık modu
- Dijital sistemler dikkati yenilik döngüleriyle hasatlar.
- Piyasalar dikkati refleksif fiyat davranışına dönüştürür.
- Otorite kiralanabilir olduğunda (sermaye, bot, sybil) yönetişim çöker.

### 3.2 [PoArt] karşı-tasarımı
- Yenilik döngülerini **doğrulama ritüelleri** ile değiştir.
- Hız metriklerini **kanıt taşıyan artefaktlar** ile değiştir.
- Anlık otoriteyi **zaman + katkı** ile değiştir.

### 3.3 Estetik katman (sanat-merkezli)
Protokolle etkileşim “trading” gibi değil, daha çok şuna benzemelidir:
- bir galeriye girmek,
- eser etiketini okumak,
- provenance’ı doğrulamak,
- bir deftere imza atmak.

### 3.4 Uygulama Eşleme Matrisi (alıntı)
> Not: Bu matris hızlı yön bulma için **alıntıdır**.  
> İstenirse 10 sütunun tamamını kapsayacak şekilde bire bir tablo genişletilebilir.

| Araştırma Sütunu | PoArt Mekanizması | Tasarım Kuralı |
| :--- | :--- | :--- |
| **Dikkat Kapısı Modeli** (Zakay & Block) | **Sol Ate Engine** | Dikkat, bilinçli ve yaşantılanan deneyime dönüştürülmelidir. |
| **Sistem 2** (Kahneman) | **Minimalist Terminal** | Dürtüsel eylemler, kasıtlı analitik sürtünme ile caydırılmalıdır. |
| **Deep Work** (Newport) | **365 Gün Kuralı** | Kültürel değer, süreklilik ve sürdürülebilir derin odakla ölçülür. |
| **Zihinsel Muhasebe** (Thaler) | **Miras Sermayesi** | Varlıklar “harcanabilir nakit” değil “kültürel miras” olarak kodlanmalıdır. |

Bu, kültürel duruştur:  
**kullanıcının dikkati tüketilmez; kürate edilir.**

---

## 4) Kopyala-Yapıştır Modülleri (diğer dokümanlarda kullanım için)

### 4.1 “Çerçeve, ispat değil” feragati
Kahneman ve benzeri bilişsel modeller açıklayıcı çerçeveler olarak kullanılır. [PoArt]’ın direnç tasarladığı başarısızlık modlarını tanımlarlar. Tek başlarına herhangi bir spesifik UI seçiminin spesifik bir sonucu doğurduğunu ispatlamazlar.

### 4.2 “Fenomenoloji katmanı” feragati
Flaherty, CP için yaşantı-temelli gerekçeyi kurar. Matematiksel CP, ek ölçüm ve denetim mantığı gerektirir; fenomenoloji değişkenin neden önemli olduğunu açıklar, nasıl hesaplandığını değil.

### 4.3 “DOI yok” politika satırı
DOI yoksa (özellikle eski proceedings veya kitap bölümlerinde yaygın), [PoArt] stabil dayanak olarak resmî kurumsal arşiv bağlantısını kullanır ve son bağlantı kontrol tarihini kaydeder.

---

## 5) ✅ Doğrulama Kontrol Listesi (bakımcılar)
- [ ] Her DOI doğru işe çözülüyor.
- [ ] DOI yoksa kurumsal arşiv veya yayınevi kayıt bağlantısı veriliyor.
- [ ] Her kaynak etiketlendi: Kanıt / Çerçeve / Tasarım Gerekçesi.
- [ ] Aşırı iddialar ayıklandı (“UI X’i ispatlar” gibi, doğrudan ampirik destek yoksa).
- [ ] Değişiklik olduğunda Son Bağlantı Kontrolü güncelleniyor.

---

```diff
+ Zakay & Block (1995) atfı, kurumsal dayanak metaverisiyle (sempozyum/proceedings) eşleştirildi
+ GitHub TOC için başlık seviyeleri standartlaştırıldı (karışık # / ## sıçraması yok)
+ Yayınevi bağlantıları güncellendi ve teyit edildi (NYU Press / Norton / Cal Newport / Levy Institute)
+ Son diff bloğu doğru kapatıldı (GitHub render düzeltmesi)

---
