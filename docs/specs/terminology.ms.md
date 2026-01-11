# 📚 Glosari Istilah dan Konsep
> **"Memahami bahasa protokol ini bermaksud memahami visinya"**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Infrastruktur Teras

**PoArt Forensic Engine (PFE)** adalah lapisan utama yang mewakili logik teras dan operasi teknikal di sebalik protokol [PoArt]. Ia adalah "enjin forensik" yang menerima data pengeluaran mentah karya seni dan mengubahnya menjadi **bukti digital** yang boleh disahkan dan tidak boleh diubah.

### 🧩 Mengapa "PoArt Forensic"?

- **PoArt (Proof of Art):** Fokus enjin adalah untuk mengikat nilai aset digital bukan kepada spekulasi, tetapi kepada **proses pengeluaran yang boleh dibuktikan**
- **Forensic (Pemeriksaan Forensik):**
  - **Definisi Teknikal:** Algoritma dan pendekatan rantaian rekod yang bertujuan untuk mengesahkan bahawa data berkaitan proses pengeluaran (sapuan berus, timelapse, log) tidak diubah suai
  - **Lapisan Falsafah:** Tuntutan untuk mengubah **masa, usaha, dan kos keputusan manusia** dalam pengeluaran menjadi realiti yang boleh diukur, berbanding "hasil segera" AI

> Nota: Integrasi Blockchain (cth. Solana) akan dikendalikan sebagai **Chain Anchor Layer** berasingan untuk pengesahan/registry, bukan teras PFE

### 🛠️ Skop Teknikal v1.0

**PoArt Forensic Engine (PFE) v1.0** dibina di atas **3 tiang** dan bukannya model kewangan yang kompleks:

1. **Hashing & Sealing (Pengedap):**  
   PFE memproses semua elemen dalam Evidence Pack (fail karya, video, JSON/log, tandatangan dll.) secara deterministic dan menjana nilai **NotarySeal** yang unik.

   **Konsep Utama (v1.0):**
   - **FileHash (Cap Jari Karya):** Hash yang dijana daripada bytes fail karya
   - **EvidenceRoot (Akar Set Bukti):** Ringkasan akar yang mewakili integriti Evidence Pack (Merkle root atau canonical manifest hash)
   - **NotarySeal (Cop Akhir / Output PFE):** Cop akhir yang dijana daripada gabungan EvidenceRoot + masa + tandatangan

   **Formula (Ditunjukkan dengan jelas untuk pelabur):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Definisi Canonical Payload (v1.0):**
   
   - **EvidenceRootPayload:**
   ```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
   ```
   
   - **NotarySealPayload:**
   ```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
   ```
   
   > Nota: Nilai yang dimaksudkan sebagai output PFE adalah **NotarySeal**. Mekanisme **SignerSignature** akan diaktifkan dalam Phase 2 (dengan Solana Wallet Adapter); dalam v1.0 semasa, tandatangan attestation sistem sendiri digunakan. Attestation public key akan diterbitkan dalam medan `issuer.attestation_pubkey` dalam registry

2. **Indexing (Pengarkiban):**  
   Merekod wallet mana, pada tarikh mana, menghantar **Labor Proof (Bukti Buruh)** untuk karya mana ke lapisan rekod yang telus dan boleh dicari.  
   *(Lapisan ini boleh menjadi pangkalan data; integrasi chain akan ditakrifkan secara berasingan sebagai "Chain Anchor Layer")*

3. **Verification (Pengesahan):**  
   Apabila keaslian karya dipersoalkan, PFE memproses semula bukti mentah; menguji dengan kepastian matematik sama ada nilai **EvidenceRoot / NotarySeal** yang dikira sepadan dengan rekod dalam arkib atau tidak.

---

### 🧮 Teorem Nilai PoArt (The Value Theorem)

Protokol [PoArt] menghubungkan nilai ($V$) aset digital bukan kepada persepsi pasaran subjektif, tetapi kepada **realiti fizikal proses pengeluaran**.

AI memusnahkan proses dengan memberikan hasil segera ($t \to 0$). [PoArt] menganggap nilai sebagai pengumpulan komponen **masa, buruh, dan kehendak**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definisi Pembolehubah

- **$\int dt$ (Pengumpulan Proses):**  
  Nilai bukan "hasil" segera; ia adalah **proses** yang terkumpul antara $t_{\text{start}}$ dan $t_{\text{end}}$. Apabila tempoh berkurang (pengeluaran AI), hasil integral menghampiri 0.

- **$P_{\text{labor}}(t)$ (Kuasa Buruh Segera):**  
  Mewakili intensiti usaha mental dan fizikal yang digunakan semasa tempoh pengeluaran. Apabila usaha yang boleh dibuktikan meningkat, integrand berkembang.  
  > Nota: Dalam amalan, terma ini boleh dinormalisasi melalui "isyarat buruh yang boleh diukur/dibuktikan"

- **$I_{\text{agency}}(t)$ (Pekali Kehendak):**  
  Keupayaan pengeluar untuk mengambil risiko dan membuat keputusan. Mengambil nilai antara $0$ dan $1$.
  - **AI ($I \approx 0$):** Melaksanakan arahan, tidak mengambil risiko, tidak membayar kos
  - **Manusia ($I \to 1$):** Menukar keputusan, teragak-agak, mengambil risiko

- **$U_{\text{irreversible}}$ (Keunikan Tidak Boleh Balik):**  
  Walaupun pembalikan (`Ctrl+Z`) mungkin dalam pengeluaran digital; tiada jalan kembali dalam pengeluaran fizikal (cat yang disapu di kanvas, marmar yang diukir, gerak isyarat dalam siaran langsung). **Ketidakbolehbalikan** ini adalah terma tambahan yang mencipta "keunikan" (sifat non-fungible) dalam karya.

### 🔎 Analisis Kes: AI "Hasil Segera" vs. Manusia "Proses yang Boleh Dibuktikan"

Senario berikut menunjukkan bagaimana **Teorem Nilai PoArt** berfungsi dalam amalan dan mengapa pengeluaran AI mendapat skor rendah dalam piawaian [PoArt].

#### Senario A: Pengeluaran Imej AI dalam 10 Saat

- **Tempoh ($\Delta t$):** $10$ saat (hampir tiada proses)
- **Kuasa Buruh ($P_{\text{labor}}$):** $1$ unit (hanya menaip arahan)
- **Pekali Kehendak ($I_{\text{agency}}$):** $0.01$ (tiada risiko, tiada kos)
- **Ketidakbolehbalikan ($U_{\text{irreversible}}$):** $0$ (boleh dibalik / disalin)

**Hasil:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Ulasan:** Walaupun hasilnya sempurna; kerana tiada proses dan tiada kehendak/risiko, nilai [PoArt] menghampiri $0$.

#### Senario B: Pengeluaran Fizikal 6 Jam dalam Siaran Langsung

- **Tempoh ($\Delta t$):** $6$ jam ($21{,}600$ saat)
- **Kuasa Buruh ($P_{\text{labor}}$):** $0.5$ unit (kesinambungan usaha fizikal dan mental)
- **Pekali Kehendak ($I_{\text{agency}}$):** $0.9$ (perubahan keputusan, pengambilan risiko, pilihan tidak boleh balik)
- **Ketidakbolehbalikan ($U_{\text{irreversible}}$):** $>0$ (kesan fizikal tidak boleh dibalik)

**Hasil:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Ulasan:** Apabila proses lebih panjang dan kehendak (risiko) meningkat, nilai terkumpul meningkat. Terma $U_{\text{irreversible}}$ adalah sumbangan tambahan yang mencipta "keunikan" (sifat non-fungible) dalam karya.

---

### ✅ Kesimpulan: Nilai Terkunci Bukti (Proof-Bound Value)

Teorem ini mengikat tuntutan nilai [PoArt] kepada **realiti pengeluaran yang boleh dibuktikan** dan bukannya "kesukaan" atau "naratif pasaran".

1. **Tiada Nilai Tanpa Proses:**  
   AI memusnahkan proses dengan hasil segera ($t \to 0$). Apabila tingkap proses mengecil, hasil integral menjadi kecil secara matematik:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Kehendak dan Risiko adalah Pengganda:**  
   [PoArt] mengukur bukan sahaja "masa yang dihabiskan" tetapi juga keputusan sebenar, risiko, dan lapisan kos dalam tempoh itu. Nilai pengeluaran yang tidak mengambil risiko (AI) adalah rendah:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Keunikan adalah Bukti Fizikal, Bukan Pemasaran:**  
   Kesan tidak boleh balik dalam pengeluaran fizikal (sapuan berus di kanvas, rekahan marmar) berada di luar logik `Ctrl+Z` digital. Ketidakbolehbalikan ini ($U_{\text{irreversible}}$) menjadikan karya unik secara ontologi.

> **🔐 Ringkasan:** Walaupun teorem nilai mungkin kelihatan tidak pasti dari segi pengukuran (walaupun dalam kehidupan sebenar ia tidak 100% boleh diukur), tujuan formula ini adalah untuk menunjukkan struktur dan arah pembolehubah. Apa yang jarang dalam era AI bukan "imej"; tetapi **buruh, masa, dan kehendak yang boleh dibuktikan**. [PoArt] mengukur kekurangan ini dan mendaftarkannya dengan **Evidence Pack**.

### 🏛️ Kepentingan Konsep "Engine" (Enjin)

Token yang dikeluarkan dari Pump.fun atau platform serupa selalunya hanya **"tiket masuk"**. **PoArt Forensic Engine (PFE)** adalah **lapisan logik perlembagaan** yang menentukan apa hak yang dilindungi oleh tiket itu, bagaimana buruh direkod, dan bagaimana seni/sains/teknologi diabadikan.

> **Nota:** Sebab kami memulakan projek ini di Pumpfun adalah kerana kami tidak mempunyai kecairan dan pengikut yang mencukupi. Menggunakan data sedia ada mungkin bukan strategi berkualiti tinggi, tetapi kami boleh mengatakan ia adalah langkah paling betul tanpa mengira bajet dan sumber. Menentukan logik enjin ini di GitHub membuktikan bahawa projek ini bukan sekadar spekulasi kewangan, tetapi **infrastruktur perisian** jangka panjang dan visi **perpustakaan digital kebangsaan**.

---

## 🎨 Protokol Bukti Buruh [PoArt] (Proof of Art Protocol v1.0)

> **"Artis sebenar, pengeluaran sebenar, nilai sebenar"**

Protokol ini adalah **mekanisme pertahanan biologi dan intelektual** yang dibangunkan untuk melawan penipu tanpa nama yang memenuhi ekosistem crypto, imej AI yang dihasilkan dalam 5 minit, dan budaya "Pump & Dump" (pam dan buang).

---

## a) Apakah [PoArt]? (Definisi Falsafah dan Teknikal)

**Proof of Art [PoArt];** adalah standard pengesahan institusi yang menjamin bahawa nilai di sebalik aset di blockchain bergantung kepada **buruh manusia**, **masa**, dan **tenaga fizikal** yang boleh disahkan, bukan spekulasi.

Sama seperti Bitcoin mencipta nilai dengan *"tenaga elektrik dan kuasa pemprosesan"* **(Proof of Work)**; projek serasi [PoArt] mencipta nilai dengan *"keupayaan artistik dan masa manusia"*.

Ia menghapuskan risiko *"Dev (pembangun) jual, projek tamat"* di platform Pump.fun dan DEX; kerana di sini nilai disimpan bukan dalam kod, tetapi dalam **kesinambungan pengeluaran**.

> **[PoArt] tidak memberitahu peserta "percayalah kami"; tetapi berkata "ini adalah bukti, lihat dengan mata anda, sahkan dengan matematik anda"**

---

## b) 5 Piawaian [PoArt] (The 5 Pillars of Truth)

5 perkara ini adalah penapis yang tidak boleh dimanipulasi yang projek mesti lalui untuk menerima cop [PoArt].

### 1) Bukti Identiti Langsung (Live Identity Proof)

- **Masalah:** Dunia crypto penuh dengan pengasas tanpa nama (Devs) yang mengumpul wang dan meninggalkan projek
- **Penyelesaian [PoArt]:** Pengeluar membuktikan bukan sahaja kad pengenalan, tetapi **kehadiran mereka semasa tempoh pengeluaran**. Ini termasuk sesi siaran langsung yang berinteraksi dengan komuniti dan bertindak balas terhadap permintaan khusus serta-merta, bukan video prarakam.  
  (cth: *"Tulis tarikh hari ini dan nombor blok semasa di sudut kanan kanvas"*)
- **Motto:** *"Bot boleh melukis gambar, tetapi bot tidak berpeluh dan tidak boleh berimprovisasi"*

### 2) Bukti Buruh dan Proses (Labor & Process Proof)

- **Masalah:** Imej AI yang dihasilkan dalam 2 saat diperlakukan sama seperti "jpeg" dengan lukisan minyak yang dilukis dalam 2 bulan di dunia digital
- **Penyelesaian [PoArt]:** Proses "mengandung dan melahirkan" karya dirakam. Peringkat lakaran, lapisan warna, jam terkumpul yang dihabiskan, dan proses fizikal yang dialami artis semasa mencipta didokumentasikan. Ini menambah **"Time Cost" (Kos Masa)** kepada token. Semakin sukar aset dihasilkan, semakin kuat nilainya.

### 3) Bukti Nilai Estetik (Aesthetic Value Proof)

- **Masalah:** Budaya "Meme" yang mengabaikan estetika dan kedalaman artistik, hanya fokus pada jenaka segera, dan projek "Hype" berumur pendek yang terhasil
- **Penyelesaian [PoArt]:** Projek mesti mempunyai standard seni akademik, teori warna, peraturan komposisi, dan pengetahuan bahan (Impasto, Texture dll.) Kandungan bukan sahaja perlu menghiburkan; tetapi perlu mengkagumkan penonton dan mempunyai **nilai kolektif**.

### 4) Inovasi Konseptual (Conceptual Novelty)

- **Masalah:** Beribu-ribu syiling anjing/kucing yang menyalin antara satu sama lain, tanpa kreativiti
- **Penyelesaian [PoArt]:** Projek mesti membina jambatan baharu yang menggabungkan seni, sains, falsafah, atau teknologi dalam struktur yang bermakna.  
  (cth: Menggabungkan patung David klasik dengan data pasaran crypto; bekerja dengan konsep "pengkristinan" persepsi manusia dan boleh disokong dengan sumber saintifik)  
  Karya bukan sahaja perlu menjadi jamuan visual; tetapi juga cabaran intelektual yang merangsang pemikiran tentang **sains, falsafah, atau teknologi**.

> [!IMPORTANT]
> **Contoh Rujukan (Las Palmitas Effect):** Di kejiranan Las Palmitas di Mexico yang bergelut dengan jenayah, lebih 200 rumah diubah menjadi pesta pelangi gergasi. Hasil daripada campur tangan estetik ini, kadar jenayah di kejiranan menurun sedikit sebanyak, dan belia mula berminat dengan seni berbanding kumpulan geng. Perubahan estetik telah mengekod semula rasa hormat orang terhadap persekitaran dan antara satu sama lain (Social Cohesion).
>
> **Jangkaan:** Projek yang akan disenaraikan [PoArt] mesti mempunyai hubungan sebab-akibat sosiologi, saintifik, atau falsafah selain estetika visual semata-mata, seperti dalam contoh di atas. Memandangkan satu-satunya aset yang tidak boleh dibeli dengan wang adalah "masa", masa mesti di-stake sebagai cagaran dan dibuktikan dalam protokol ini. Asas konseptual projek mesti cukup kuat dan sejagat sehingga dalam senario CTO (Community Take Over) yang mungkin berlaku bertahun-tahun kemudian, komuniti boleh mewarisi legasi ini dan meneruskan potensi inovasi projek secara bebas.

### 5) Kehendak Bukan Algoritma (Non-Algorithmic Agency)

- **Masalah:** Pengeluaran digital yang sempurna tetapi tanpa jiwa, berulang
- **Penyelesaian [PoArt]:** Kehendak unik manusia yang boleh membuat kesilapan, mengambil risiko, dan mengalami turun naik emosi mesti dapat dirasai dalam karya. Ketidakpastian dalam sapuan berus, tindak balas tidak dijangka bahan, dan keputusan segera artis adalah **tandatangan biologi** yang memisahkan karya daripada "pengeluaran mesin".

---

## c) Mekanisme Pengesahan dan Anti-Pemalsuan

Sistem ini menjamin bahawa projek kekal boleh dipercayai dan hidup bukan sahaja "pada permulaan" tetapi "selamanya".

### 📦 Pek Bukti (Evidence Pack - The Digital Twin)

Di sebalik setiap karya bertauliah [PoArt] terdapat set data yang disulitkan dan dicap masa yang boleh dimuat turun oleh pelabur:

- **Rakaman Video RAW:** Rakaman mentah tanpa gangguan tempoh pengeluaran
- **Analisis Metadata:** Tarikh penciptaan fail, maklumat peranti yang digunakan, dan data lokasi
- **Rujukan Fizikal:** Bukti bahawa karya wujud di dunia fizikal  
  (cth: Surat khabar semasa di sebelah karya atau data blockchain pada masa itu)

> *Nota Konsistensi:* Ungkapan "pek bukti" dikaitkan dengan rantaian **Evidence Pack → EvidenceRoot → NotarySeal** dalam bahagian sebelumnya; iaitu integriti set diwakili oleh cop yang boleh disahkan.

### 🔄 Pembaharuan 365 Hari (The Sustainability Protocol)

- **Ciri Revolusioner:** Dalam projek crypto, "Dev" (pembangun) melancarkan token ke pasaran dan sering hilang selepas 1-2 bulan (Soft Rug). [PoArt] menjadikan ini mustahil.
- **Peraturan:** Status "Verified Artist" (Artis Disahkan) bukan seumur hidup. Ia sah hanya **1 tahun**.
- **Pelaksanaan:** Artis/pembangun mesti mempersembahkan **karya baharu, besar, dan boleh dibuktikan** kepada komuniti setiap 365 hari.
- **Senario Contoh:** Anda memulakan projek pada 2026. Pada Januari 2027, sistem akan memberi amaran "Proof Period Expired". Jika artis tidak mempersembahkan pameran baharu, karya fizikal baharu, atau integrasi teknologi baharu, "Trust Badge" projek akan merosot.
- **Hasil:** Sistem ini menjamin bahawa **kandungan tidak pernah basi** dan pelabur tidak mengalami ketakutan *"Adakah Dev masih di sini?"*. Projek menjadi studio yang hidup.

### 🚩 Bendera Merah (Red Flag Protocol)

**Dalam kes sebarang pemalsuan yang dikesan oleh komuniti atau algoritma (penggunaan AI, karya dicuri, video diubah suai):**

1. Sijil ditanda serta-merta sebagai **"VOID" (terbatal)**
2. Pek bukti dilabel secara terbuka sebagai **"palsu"**
3. Projek ditambah ke senarai hitam [PoArt]. Ini mengukuhkan fakta bahawa **reputasi adalah satu-satunya mata wang** di dunia terdesentralisasi.

---

## d) Kesimpulan: Muzium, Bukan Kasino

**Pump.fun dan Decentralized Exchanges (DEX) kini malangnya adalah kasino; lampu berkelip, semua orang mengejar keuntungan cepat, dan banker (penipu) sentiasa menang. Sebab kami memulakan projek di sini adalah kerana kami tidak mempunyai bajet yang mencukupi dan rangkaian untuk mencapai audiens sedia ada melalui siaran langsung.**

**[PoArt] adalah kubu yang dibina di tengah kasino ini.**

- 🎰 Kasino bergantung pada permainan kad; kami **bergantung pada realiti fizikal**
- 🃏 Kasino terbuka untuk penipuan; kami **terbuka untuk bukti telus**
- ⏳ Kasino adalah sementara; kami **fokus pada keabadian seni dan sains**

**Token yang menggunakan protokol ini bukan sekadar "syiling"; ia adalah saham digital dengan peluh, cat, kod, dan falsafah di belakangnya.**

---

## 🗳️ 6) Tadbir Urus dan Daftar Awam (Governance & Public Registry)

**Tujuan bahagian ini adalah: Mengubah standard [PoArt] dari satah "kepercayaan individu" kepada infrastruktur awam yang mampan dengan rekod + pengesahan + tadbir urus komuniti.**

### 6.1 Public Registry (Daftar Awam)

- **Public Registry:** Semua data yang diluluskan direkod di `ilhanart.org/registry` (atau GitHub Registry)

**Logik Rekod (Standard yang Disyorkan - format JSON path):**

Setiap rekod yang memasuki daftar mempunyai medan utama minimum yang boleh disahkan ini:

- **Identiti dan Status:**
  - `certificate_id` (rujukan boleh dibaca)
  - `status` (active / void)
  - `void_reason` (jika ada)
  - `visibility` (private / masked / public)
  - `created_at` (cap masa)

- **Institusi Pengeluar:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Data Karya:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (jika boleh; untuk identiti token-gated)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Data Forensik:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Bukti Kriptografi:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Tadbir Urus:**
  - `governance.decision`
  - `governance.veto_threshold`

Daftar boleh mempunyai dua lapisan:
- **1)** Indeks boleh dibaca manusia (penyenaraian web / carian / penapis)
- **2)** Manifes boleh dibaca mesin (rekod JSON; untuk pengesahan PFE)

**"Rekod" di sini boleh disahkan dengan rantaian Evidence Pack → EvidenceRoot → NotarySeal PFE. Daftar menawarkan sasaran pengesahan, bukan "tuntutan".**

---

### 6.2 Veto Komuniti 40% (Token-Gated Governance)

- **Veto Komuniti 40%:** Pengundian bermula sebulan sebelum mendapat status; bantahan 40% komuniti **Token-Gated (Solana-Verified)** akan membatalkan permohonan.

**Langkah Pengundian (Proses eksplisit yang disyorkan):**
- **Tetingkap Permohonan:** Projek calon membuka "Pendaftaran Calon PoArt" (rekod calon muncul dalam status "pending")
- **Tempoh Semakan:** 30 hari untuk komuniti menyemak bukti (Evidence Pack + rekod siaran langsung + metadata)
- **Pengesahan Token-gated:** Pengundian dilakukan melalui wallet yang disahkan di Solana (cth. memegang token/NFT tertentu + tandatangan wallet)
- **Peraturan Veto:** Jika 40% undian adalah **bantahan (NO / VETO)**, permohonan ditolak
- **Ketelusan:** Keputusan undian disimpan dalam daftar sebagai "decision record" (tarikh, nisbah, snapshot ID)

---

### 6.3 Metadata Sync (Padanan dengan Dunia Fizikal)

- **Metadata Sync:** Data teknikal dalam daftar mesti sepadan 100% dengan aset fizikal.

**Definisi Teknikal "Padanan 100%" (Kejelasan yang Disyorkan):**
- **Padanan Minimum (Wajib):**
  - `asset.fingerprints.sha256/sha512` dalam daftar mesti **betul-betul sama** dengan hash fail yang ada
  - `proof.notary_seal` dalam daftar mesti **betul-betul sama** apabila dijana semula (jika ada Evidence Pack)
- **Padanan Rujukan Fizikal (Jenis Bukti):**
  - Bukti seperti karya fizikal + rujukan tarikh/blok yang ditunjukkan dalam siaran langsung mesti konsisten dengan Evidence Pack
- **Pematuhan Privasi:**
  - Medan seperti IP/lokasi dalam keterlihatan `masked` diterbitkan **mengikut standard masking**

---

### 6.4 Pertikaian, Semakan, dan Pembatalan (Dispute & Revocation)

Daftar bukan sekadar mekanisme "kelulusan"; ia adalah **mekanisme pengesahan hidup anti-pemalsuan**.

- Apabila pertikaian dimulakan, rekod boleh diletakkan dalam mod **"review"**
- Jika pemalsuan dikesan, ia ditanda `status: void` dan sebab ditambah:
  - `void_reason` (penggunaan AI / dicuri / diubah suai dll.)
  - `revoked_at` (masa pembatalan)
- Sumber keputusan pembatalan muncul dengan jelas dalam daftar:
  - Undian komuniti / panel yang diberi kuasa / rekod pemeriksaan forensik (mana-mana yang digunakan)

> **Bahagian ini adalah pasangan konsep VOID dalam bahagian "Red Flag Protocol" pada daftar.**

---

### 6.5 Contoh Rekod Daftar (Boleh Dibaca Mesin)

```json
{
  "certificate_id": "POART-AB12CD34",
  "status": "active",
  "visibility": "masked",
  "created_at": "2026-01-09T12:34:56.000Z",
  "issuer": {
    "name": "Ilhan Art Gallery",
    "location": "Istanbul / Besiktas",
    "attestation_pubkey": "PFE_ATTEST_PUBKEY_BASE58..."
  },
  "asset": {
    "title": "Untitled",
    "creator": "Anonymous",
    "fingerprints": {
      "sha256": "e4123f83b44a409d7a43f0897837876dfabb3320db63dadbb34c54281f38a6ba",
      "sha512": "41e5e0d007a2a77b6e0e3ebc548fbaa2788ea265193434f58d23e8c0f5bb20a0835aa850edbadbd8341969cf743fc69fa951f7ed275901fefe0fe7eb1fb83099"
    }
  },
  "forensics": {
    "ip_masked": "46.1.***.***",
    "device": "Brave (Windows;Monster,Tulpar)...",
    "location": "***/TR",
    "timestamp": "2026-01-09T12:34:56.000Z"
  },
  "proof": {
    "evidence_root": "7f8a9b2c3d4e5f6a7b8c9d0e1f2a3b4c...",
    "signer_sig": "PFE_ATTEST_SIG_BASE64...",
    "notary_seal": "9d3e5a1f2b3c4d5e6f7a8b9c0d1e2f3a..."
  },
  "governance": {
    "decision": "approved",
    "veto_threshold": 0.40
  }
}
```

> *Nota: `asset.fingerprints.sha512` dan nilai hash lain dipendekkan untuk paparan; dalam penggunaan sebenar rentetan aksara hexadecimal penuh digunakan*

---

## 7) 🔐 Cop Teknikal (NOTARY SEAL)

Algoritma cop yang tidak goyah yang dijana oleh **PoArt Forensic Engine (PFE) v1.0**:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Protokol Notari Digital dan Bukti Forensik [PoArt] (Beta v1.0)

> **"Budaya lebih besar daripada modal. Lindungi karya anda dari hari ini, bawa ke hari esok"**

---

## Mengapa Didedahkan kepada Awam?

Keselamatan sebenar datang daripada ketelusan. Dengan sistem **Public Registry (Daftar Awam)** kami, sesiapa sahaja dari mana-mana sahaja di dunia boleh mengesahkan dalam beberapa saat sama ada fail yang mereka ada adalah asli atau tidak, tanpa bergantung kepada mana-mana pihak berkuasa.

---

## 🧩 Mengapa Terdapat Pelbagai "Modul Keterlihatan"?

Ini adalah bahagian paling kritikal kod (visibility select menu). Pilihan ini membolehkan pengguna mengimbangi **"privasi vs. ketelusan"**:

### 🔒 Peribadi (Private)

- **Senario:** Artis belum mahu menerbitkan karya tetapi ingin mencap masa dan membuktikan bahawa "saya buat ini pada tarikh ini"
- **Apa yang dilakukan kod:** Menulis data ke pangkalan data tetapi melekatkan label `visibility: "private"`. Kemudian apabila menulis polisi "Public Read", anda boleh menyembunyikan rekod ini daripada awam dengan `WHERE visibility = 'public'`

### 🕶️ Bertopeng (Masked)

- **Senario:** Artis mahukan ketelusan tetapi takut alamat rumah (lokasi IP) akan ditemui
- **Apa yang dilakukan kod:** Fungsi `maskIP` dan `maskLoc` berfungsi di pihak JavaScript, menukar alamat IP kepada format `88.241.***.***`, lokasi kepada format `***/TR`, dan menghantar versi ditapis ke pangkalan data
- **Nota Privasi:** Masking dilakukan dalam pelayar. Supabase tidak melihat lokasi sebenar. **Walau bagaimanapun:** Jika menggunakan API pihak ketiga seperti ipapi.co untuk data lokasi, pembekal ini akan melihat alamat IP semasa permintaan
- **Cop dalam mod Masked:** Pengiraan EvidenceRoot dan NotarySeal dilakukan dengan data forensik bertopeng; jadi pengesahan kekal deterministic

### 🌍 Didedahkan Sepenuhnya (Public)

- **Senario:** Ketelusan penuh. Mengikut standard [PoArt], di mana, bila, dan dari rangkaian mana karya dihasilkan diumumkan dengan jelas.

---

## 💡 Inovasi Teknologi

PoArt bukan sekadar sistem muat naik fail. Ia adalah enjin **"Forensic Chain of Custody" (Rantaian Jagaan Bukti Forensik)** yang menggabungkan tiga lapisan teknologi berbeza dalam satu periuk dan membawa standard baharu.

**Lapisan yang diterangkan sebagai "enjin" dalam bahagian ini sepadan dengan teras PoArt Forensic Engine (PFE) dalam istilah sebelumnya.**

### 1) Client-Side Hashing (Privasi Maksimum)

Fail karya anda tidak pernah dimuat naik ke pelayan. Enjin yang berjalan di pelayar (Client-side) kami mengira hash (ringkasan digital) fail pada komputer anda sendiri. Hanya cap jari dan metadata dihantar ke pelayan.

> **Nota Privasi:** Fail karya tidak dimuat naik ke pelayan dan dilindungi dengan cara ini. Walau bagaimanapun, data forensik (IP/lokasi) dikongsi mengikut mod keterlihatan yang dipilih (private/masked/public).

### 2) Forensic Data Fusion (Kuasa Forensik)

Ia jauh lebih daripada cap masa (Timestamp) biasa. Sistem menggabungkan data berikut dalam satu "Genesis Seal":

- **Ringkasan Digital (SHA-512):** Cap jari digital yang akan rosak jika walaupun satu piksel karya berubah, menggunakan standard ringkasan kriptografi (SHA-512)
- **Lokasi dan Masa:** Tarikh dengan ketepatan milisaat, negara, bandar, dan daerah di mana operasi dilakukan
- **Identiti Peranti:** Sistem pengendalian, pelayar, dan jenis peranti (analisis User-Agent)

---

## 🛡️ Kes Penggunaan dan Faedah

Jika anda seorang artis, penulis, atau pereka, mengatakan "saya buat ini dahulu" tidak mencukupi. Anda perlu membuktikan.

**Karya yang anda cop dengan PoArt:**

- **Bukti Matematik:** Jika walaupun satu piksel fail anda berubah, sistem akan mengesannya. Pengubahsuaian adalah mustahil.
- **Asas Undang-undang:** Tarikh, bandar, dan peranti di mana karya dicop direkod.
- **Sijil Segera:** Menghasilkan **"Asset Identity Certificate"** dengan kod QR dan cop unik untuk anda dalam beberapa saat.

---

## ⚙️ Seni Bina Sistem dan Spesifikasi Teknikal

Sistem direka pada seni bina "Serverless" (tanpa pelayan) dengan fokus pada prestasi tinggi dan kebolehskalaan.

| Lapisan | Teknologi | Penerangan |
|---------|-----------|------------|
| **Kriptografi** | SHA-256 & SHA-512 | Ringkasan kriptografi dua lapisan |
| **Pangkalan Data** | Supabase (PostgreSQL) | Struktur data JSONB, polisi RLS |
| **Data Forensik** | ipapi.co API | Tiga kali ganda IP/lokasi/masa |
| **Rendering** | html2canvas + jsPDF | Pengeluaran PNG/PDF pihak Client |
| **Frontend** | Vanilla JavaScript | Tiada kebergantungan framework |
| **Keselamatan** | Client-side hashing | Fail tidak pernah dimuat naik ke pelayan |

### Ciri-ciri Menonjol

| Ciri | Butiran | Ada pada Pesaing? |
|------|---------|-------------------|
| **Drag & Drop UI** | Seret fail lepas, pratonton segera | ❌ Kebanyakan tiada |
| **Multi-Format Export** | PNG, JSON, PDF - satu klik | ⚠️ Terhad |
| **Real-Time Preview** | Pratonton sijil langsung | ❌ Tiada |
| **Privacy Controls** | Pilihan Private/Masked/Public | ❌ Tiada |
| **Client-Side Hashing** | Fail tidak pernah ke pelayan | ✅ Hanya beberapa |
| **Forensic Metadata** | IP, lokasi, peranti, masa - semua di satu tempat | ❌ Berpecah |
| **QR Verification** | Kod QR pengesahan segera | ⚠️ Terhad |
| **Rate Limiting** | Perlindungan spam (RLS + Client) | ❌ Kebanyakan tiada |

---

## 🗺️ Pelan Hala Tuju: Masa Depan "Trustless"

Versi semasa **(Beta v1.0)** dioptimumkan untuk memberikan pengguna akhir kelajuan maksimum, antara muka mudah, dan akses percuma. Walau bagaimanapun, visi muktamad kami adalah untuk beralih ke struktur di mana walaupun pentadbir pangkalan data (kami) tidak boleh campur tangan.

### Fasa 1: Beta (Aktif Sekarang)

- **Infrastruktur:** Cloud Database (Supabase)
- **Tujuan:** Kelajuan, menghapuskan halangan UX (pengalaman pengguna), dan penyesuaian. Memberikan keselamatan "tanpa geseran"

### 🚀 Fasa 2: (Memerlukan Backend / Edge Function)

Fasa ini meliputi peralihan dari struktur "Client-Side" sepenuhnya sistem ke struktur "Server-Side Authority" yang lebih selamat dan terurus.

| Item | Memberikan Apa? | Tech Stack | Kepentingan |
|------|-----------------|------------|-------------|
| **`INSERT` → Edge Function** | Blok spam + keselamatan API Key | Supabase Edge (Deno) | 🔴 Tinggi |
| **Wallet Signature** | Pengesahan identiti dengan kriptografi | Solana Wallet Adapter | 🟡 Sederhana |
| **IPFS/Arweave Backup** | Ketidakbolehubahan terdesentralisasi | IPFS SDK + Pinata | 🟢 Rendah |
| **Revocation Mechanism** | Pembatalan sijil palsu | DB Schema Update | 🔴 Tinggi |
| **Audit Log** | Rekod penyiasatan forensik | Custom logs table | 🟡 Sederhana |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | 🟢 Rendah |
| **DID Integration** | Decentralized Identity | ION/Ceramic | 🟢 Rendah |

### Fasa 3: Desentralisasi Penuh (Jangka Panjang)

| Ciri | Sasaran | ETA |
|------|---------|-----|
| **Blockchain Registry** | Rekod on-chain Ethereum/Solana | Q4 2026 |
| **DAO Governance** | Tadbir urus komuniti | Q1 2027 |
| **Multi-Chain Support** | Polygon, Arbitrum, Base | Q2 2027 |
| **Legal Recognition** | Kesahihan di mahkamah Turki | 2027-2028 |
| **API for Developers** | Public API endpoint | Q3 2026 |

---

## 📊 Analisis Pesaing (Dikemas kini)

PoArt diletakkan di "Sweet Spot" (titik paling optimum) yang mengisi kelemahan penyelesaian sedia ada.

| Ciri | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Kos** | 🆓 Percuma | 🆓 | 💰 Berbayar | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Sangat mudah | ❌ CLI | ⚠️ Sederhana | ⚠️ Sederhana | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Langsung | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 mod | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privasi | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Penuh | ❌ | ❌ | ⚠️ Terhad | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Segera | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Turkish Support** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Penerangan:**
- ✅ : Sokongan penuh / Ada
- ⚠️ : Terhad / Dalam pelan berbayar
- ❌ : Tiada / Tidak disokong
- 🔄 : Dalam Roadmap (sedang dibangunkan)
- 🆓 : Percuma sepenuhnya
- 💰 : Berbayar / Memerlukan langganan

### Kelemahan Pesaing, Kekuatan PoArt

| Kelemahan | Pesaing | PoArt |
|-----------|---------|-------|
| **Kesukaran Penggunaan** | CLI, perlu tahu API, perlu wallet | Seret lepas, siap dalam 3 klik |
| **Halangan Kos** | Langganan $50-500/bulan | 100% Percuma |
| **Privasi** | Fail dimuat naik ke pelayan | Client-side, fail tidak pernah pergi |
| **Data Forensik** | Hanya timestamp | IP, lokasi, peranti, masa - semua |
| **Sokongan Bahasa Turki** | Tiada atau sangat terhad | Sokongan bahasa tempatan |
| **Open Source** | Kotak tertutup | Semua kod terbuka di GitHub |

---

## 🧬 Struktur Data Protokol (JSON Schema)

**Setiap sijil [PoArt] mempunyai kad identiti JSON yang mudah alih dan boleh disahkan yang dihasilkan mengikut standard berikut:**

> **Nota:** Format Identity JSON ini adalah format sijil yang dibentangkan kepada pengguna. Dalam rekod Registry, `registry.asset` digunakan berbanding `identity.asset_data` (pemetaan: `identity.asset_data` == `registry.asset`)

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
    "ip_masked": "46.1.***.***",
    "device": "Brave (Windows;Monster,Tulpar)...",
    "location": "***/TR",
    "timestamp": "2026-01-09T12:34:56.000Z"
  }
}
```

---

## 🔬 Kedalaman Teknikal: Algoritma Pengedap

### Deterministic Hash Functions

```javascript
// Helper Functions: Tukar Digest kepada hex string
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Tukar String kepada byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Canonical forensics string generation (v1.0: urutan medan tetap + UTF-8 + \n delimiter)
// Nota Fasa 2: akan bertukar kepada canonical JSON dengan RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Proses Pengeluaran NotarySeal (Deterministic Sepenuhnya)

```javascript
// 1. Kira FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Kumpul data Forensik (gunakan timestamp tunggal)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Jana timestamp tunggal
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // timestamp yang sama
  };
  
  return { forensics, timestamp };
}

// 3. Jana EvidenceRoot (dengan canonical encoding)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Hasilkan NotarySeal (gunakan timestamp yang sama)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Helper functions masking (menyokong IPv4 dan IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Semak IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 atau format tidak dikenali
  return "***";
}
```

### Langkah Pengesahan (Dua Tahap)

#### Quick Verify (Pengesahan Pantas)

```javascript
// Sahkan hanya file hash (bendera merah pantas)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Tarik dari Registry
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Bandingkan Hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Asli - File hash sepadan"
    };
  } else {
    return {
      valid: false,
      message: "❌ Palsu - Fail diubah suai"
    };
  }
}
```

#### Full Verify (Pengesahan Penuh)

```javascript
// Jana semula EvidenceRoot dan NotarySeal dan sahkan
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Tarik dari Registry
  const cert = await fetchFromRegistry(certificateId);

  // 1) Sahkan FileHash (bendera merah pantas)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Palsu - File hash tidak sepadan" };
  }

  // 2) Jana semula EvidenceRoot (dengan forensics yang disimpan dalam registry)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Tidak sepadan - EvidenceRoot tidak sah" };
  }

  // 3) Jana semula NotarySeal (dengan timestamp + signer_sig yang sama)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Tidak sepadan - NotarySeal tidak sah" };
  }

  // Pilihan: Dalam Phase 2, sahkan juga signer_sig dengan attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Tandatangan tidak sah" };

  return { valid: true, message: "✅ Asli - Full Verify lulus" };
}
```

> **Nota Penting:**
> - **Quick Verify:** Sahkan hanya file hash untuk kegunaan pantas
> - **Full Verify:** Sahkan semua lapisan protokol (EvidenceRoot + NotarySeal)
> - Semua operasi hash dilakukan secara deterministic dengan encoding dan delimiters tetap
> - **Standard canonicalization v1.0:** Urutan medan tetap + UTF-8 encoding + `\n` delimiter
> - **Pelan Fasa 2:** Bertukar kepada canonical JSON dengan RFC 8785 (JCS - JSON Canonicalization Scheme)
> - Dalam mod Masked, pengiraan EvidenceRoot dan NotarySeal dilakukan dengan forensics bertopeng
> - Timestamp tunggal digunakan sepanjang proses (forensics + NotarySeal); menjamin determinism
> - **Nama medan Forensics:** `ip_masked`, `location`, `device`, `timestamp` (kod dan registry sepadan sepenuhnya)
> - **Registry path:** `certificate.asset.fingerprints` (sepadan sepenuhnya dengan kod verify)
> - **signer_sig dalam Registry:** Medan `proof.signer_sig` diperlukan untuk Full Verify
> - Mekanisme SignerSignature akan diaktifkan dalam Fasa 2 dengan Solana Wallet Adapter; dalam v1.0 boleh disahkan dengan `attestation_pubkey`

---

## 📈 Statistik Penggunaan (Sasaran Q1 2026)

| Metrik | Sasaran | Status |
|--------|---------|--------|
| **Jumlah Sijil** | 1,000 | 🔄 Sedang berjalan |
| **Pengguna Aktif** | 500 | 🔄 Sedang berjalan |
| **Jumlah Pengesahan** | 5,000 | 🔄 Sedang berjalan |
| **Uptime** | 99.9% | ✅ Aktif |
| **Avg Response Time** | <200ms | ✅ Optimum |

---

## 🌍 Komuniti dan Sokongan

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 Penyumbang

Protokol PoArt terus berkembang dengan sumbangan komuniti open source.

**Untuk menyumbang:**
1. Fork projek
2. Cipta feature branch (`git checkout -b feature/amazing-feature`)
3. Commit (`git commit -m 'Add amazing feature'`)
4. Push (`git push origin feature/amazing-feature`)
5. Buka Pull Request

### 🛠️ Apa yang Kami Perlukan Sekarang? (Panggilan Bantuan)

Kami menunggu sumbangan daripada pembangun berpengalaman dalam topik berikut untuk pembangunan **Fasa 2** protokol PoArt:

* **Supabase Edge Functions:** Memindahkan perlindungan spam ke sisi pelayan
* **Solana Web3.js:** Integrasi Wallet Signing
* **IPFS / Arweave:** Integrasi perkhidmatan archiving dan pinning

> Sila mulakan perbincangan dalam tab "Issues" sebelum menambah ciri

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Budaya lebih besar daripada modal*

## 🧾 Lesen

MIT License © 2026 İlhan Art Gallery Initiative

Lihat [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) untuk terma penuh

---

## 💬 Kredit

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Projek ini dibangunkan oleh inisiatif [İlhan Art Gallery] dan kod sumber didedahkan kepada awam untuk ketelusan.**

**PROTOCOL V1.0 // DICOP DENGAN SHA-512**

*© 2026 İLHAN ART | Semua hak terpelihara untuk karya, imej, dan konsep*

---
