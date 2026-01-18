# 📚 KAMUS TERMINOLOGI & KONSEP - Bahagian 1
> **"Memahami bahasa protokol ini adalah memahami visinya."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Infrastruktur Teras

**PoArt Forensic Engine (PFE)** adalah lapisan utama yang mewakili logik teras dan operasi teknikal di sebalik protokol [PoArt]. Inilah "enjin forensik" yang mengambil data pengeluaran mentah karya seni dan mengubahnya menjadi **bukti digital** yang boleh disahkan dan tidak boleh diubah.

### 🧩 Mengapa "PoArt Forensic"?

- **PoArt (Proof of Art):** Fokus enjin adalah menghubungkan nilai aset digital bukan kepada spekulasi; tetapi kepada **proses pengeluaran yang boleh dibuktikan**.
- **Forensic (Pengesahan Forensik):**
  - **Definisi Teknikal:** Pendekatan algoritma dan rantai rekod untuk mengesahkan bahawa data yang berkaitan dengan proses pengeluaran (sapuan berus, timelapse, log) tidak dimanipulasi.
  - **Lapisan Falsafah:** Menentang pengeluaran "output segera" AI; tuntutan bahawa pengeluaran manusia yang mengandungi **masa, usaha, dan harga keputusan** boleh menjadi ukuran realiti.

> Nota: Integrasi blockchain (cth. Solana) bukan teras PFE; ia ditakrifkan secara berasingan sebagai **Chain Anchor Layer** untuk pengesahan/registry.

### 🛠️ Skop Teknikal v1.0

**PoArt Forensic Engine (PFE) v1.0** dibina atas **3 tiang utama** dan bukannya model kewangan yang kompleks:

1. **Hashing & Sealing (Penyegelan):**  
   PFE memproses semua elemen dalam Evidence Pack (fail karya seni, video, JSON/log, tandatangan dll.) secara deterministik untuk menghasilkan nilai **NotarySeal** yang unik.

   **Konsep teras (v1.0):**
   - **FileHash (cap jari karya seni):** Hash yang dijana daripada byte fail karya seni.
   - **EvidenceRoot (punca pakej bukti):** Ringkasan punca yang mewakili integriti Evidence Pack (Merkle root atau canonical manifest hash).
   - **NotarySeal (meterai akhir / PFE Output):** Meterai akhir yang dijana daripada gabungan EvidenceRoot + masa + tandatangan.

   **Formula (jelas kelihatan kepada pelabur):**
   
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
   
   > Nota: Nilai yang dimaksudkan sebagai PFE output adalah **NotarySeal**. Mekanisme **SignerSignature** akan diaktifkan dalam Fasa 2 (dengan Solana Wallet Adapter); dalam v1.0 semasa, tandatangan attestation sistem sendiri digunakan. Kunci awam attestation diterbitkan dalam medan `issuer.attestation_pubkey` registry.

2. **Indexing (Pengarkiban):**  
   Merekod dompet mana, tarikh apa, untuk karya seni apa yang mengemukakan **Labor Proof (Bukti Buruh)**; ke dalam lapisan rekod yang telus dan boleh dicari.  
   *(Lapisan ini boleh menjadi pangkalan data; integrasi rantai ditakrifkan secara berasingan sebagai "Chain Anchor Layer".)*

3. **Verification (Pengesahan):**  
   Apabila keaslian karya seni dipersoalkan, PFE memproses semula bukti mentah; menguji dengan kepastian matematik sama ada nilai **EvidenceRoot / NotarySeal** yang dikira sepadan dengan rekod dalam arkib.

---

### 🧮 Teorem Nilai PoArt (The Value Theorem)

Protokol [PoArt] menghubungkan nilai ($V$) aset digital bukan dengan persepsi pasaran subjektif; tetapi dengan **realiti fizikal proses pengeluaran**.

Kecerdasan Buatan (AI) memusnahkan proses dengan memberikan hasil segera ($t \to 0$). [PoArt] menerima nilai sebagai; pengumpulan **masa, usaha, dan kehendak**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definisi Pembolehubah

- **$\int dt$ (Pengumpulan Proses):**  
  Nilai bukan "output" segera; ia adalah **proses** yang terkumpul antara $t_{\text{start}}$ dan $t_{\text{end}}$. Apabila tempoh berkurang (pengeluaran AI), hasil kamiran menghampiri 0.

- **$P_{\text{labor}}(t)$ (Kuasa Buruh Seketika):**  
  Mewakili intensiti usaha mental dan fizikal yang dibelanjakan pada masa pengeluaran. Apabila usaha yang boleh dibuktikan meningkat, integrand berkembang.  
  > Nota: Istilah ini boleh dinormalisasi secara praktikal melalui "isyarat buruh yang boleh diukur/dibuktikan".

- **$I_{\text{agency}}(t)$ (Pekali Kehendak):**  
  Keupayaan pengeluar untuk mengambil risiko dan membuat keputusan. Mengambil nilai antara $0$ dan $1$.
  - **AI ($I \approx 0$):** Mengikut arahan, tidak mengambil risiko, tidak membayar harga.
  - **Manusia ($I \to 1$):** Mengubah keputusan, teragak-agak, mengambil risiko.

- **$U_{\text{irreversible}}$ (Keunikan Tidak Boleh Dikembalikan):**  
  Walaupun pembatalan (`Ctrl+Z`) boleh dilakukan dalam pengeluaran digital; dalam pengeluaran fizikal (cat yang disapu di kanvas, marmar yang diukir, gerak isyarat dalam siaran langsung) tidak ada jalan kembali. **Ketidakbolehkembalian ini** adalah istilah tambahan yang mencipta "keunikan" (watak non-fungible) dalam karya.

### 🔎 Analisis Kes: AI "Output Segera" vs. Manusia "Proses Terbukti"

Senario berikut menunjukkan bagaimana **Teorem Nilai PoArt** berfungsi secara praktikal dan mengapa pengeluaran AI mendapat skor rendah dalam piawaian [PoArt].

#### Senario A: Pengeluaran Visual dalam 10 Saat menggunakan AI

- **Tempoh ($\Delta t$):** $10$ saat (hampir tiada proses)
- **Kuasa Buruh ($P_{\text{labor}}$):** $1$ unit (hanya menulis arahan)
- **Pekali Kehendak ($I_{\text{agency}}$):** $0.01$ (tiada risiko, tiada harga)
- **Ketidakbolehkembalian ($U_{\text{irreversible}}$):** $0$ (boleh dikembalikan / boleh disalin)

**Hasil:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Komen:** Walaupun output sempurna; kerana tiada proses yang dialami dan tiada kehendak/risiko, nilai [PoArt] menghampiri $0$.

#### Senario B: Pengeluaran Fizikal 6 Jam dalam Siaran Langsung

- **Tempoh ($\Delta t$):** $6$ jam ($21{,}600$ saat)
- **Kuasa Buruh ($P_{\text{labor}}$):** $0.5$ unit (kesinambungan usaha fizikal dan mental)
- **Pekali Kehendak ($I_{\text{agency}}$):** $0.9$ (perubahan keputusan, mengambil risiko, pilihan tidak boleh dikembalikan)
- **Ketidakbolehkembalian ($U_{\text{irreversible}}$):** $>0$ (jejak fizikal tidak boleh diambil semula)

**Hasil:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Komen:** Apabila proses berpanjangan dan kehendak (risiko) meningkat, nilai berkumpul secara kumulatif. Istilah $U_{\text{irreversible}}$ adalah sumbangan tambahan yang mencipta "keunikan" (watak non-fungible) dalam karya.

---

### ✅ Kesimpulan: Nilai Terkunci dengan Bukti (Proof-Bound Value)

Teorem ini mengeluarkan tuntutan nilai [PoArt] daripada menjadi "keutamaan" atau "naratif pasaran" dan menghubungkannya dengan **realiti pengeluaran yang boleh dibuktikan**.

1. **Tiada Proses, Tiada Nilai:**  
   AI memusnahkan proses dalam output segera ($t \to 0$). Apabila tingkap proses menyempit, hasil kamiran semestinya mengecil dengan keperluan matematik:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Kehendak dan Risiko adalah Pengganda:**  
   [PoArt] mengukur bukan sahaja "masa yang dibelanjakan"; tetapi juga lapisan keputusan sebenar, risiko, dan harga dalam masa itu. Pengeluaran yang tidak mengambil risiko (AI) mempunyai nilai rendah:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Keunikan adalah Bukti Fizikal, Bukan Pemasaran:**  
   Jejak yang tidak boleh dikembalikan dalam pengeluaran fizikal (sapuan kanvas, retakan marmar) berada di luar logik `Ctrl+Z` digital. Ketidakbolehkembalian ini ($U_{\text{irreversible}}$) menjadikan karya unik secara ontologi.

> **🔐 RINGKASAN:** Walaupun teorem nilai kelihatan tidak pasti sebagai ukuran (walaupun dalam kehidupan sebenar tidak boleh diukur 100%), tujuan formula ini adalah; menunjukkan struktur dan arah pembolehubah. Dalam zaman AI, perkara yang jarang bukan "imej"; tetapi **usaha, masa, dan kehendak yang boleh dibuktikan.** [PoArt] mengukur kekurangan ini dan mendaftarkan dengan **Evidence Pack**.

### 🏛️ Kepentingan Konsep "Engine" (Enjin)

Token yang keluar dari platform seperti Pump.fun atau seumpamanya kebanyakannya hanyalah **"tiket akses"**. **PoArt Forensic Engine (PFE)** adalah **lapisan logik perlembagaan** yang menentukan hak apa yang dilindungi oleh tiket itu, bagaimana usaha akan direkodkan, dan bagaimana seni/sains/teknologi akan diabadikan.

> **Nota:** Sebab kami memulakan projek ini di Pump.fun adalah kerana kami tidak mempunyai kecairan dan bilangan pengikut yang mencukupi. Menggunakan data yang ada adalah langkah yang paling betul secara strategik walaupun bukan kualiti tertinggi. Mentakrifkan logik enjin ini di GitHub tanpa mengira bajet dan keupayaan membuktikan bahawa projek bukan sekadar spekulasi kewangan, tetapi visi **infrastruktur perisian** jangka panjang dan **perpustakaan negara digital**.

---

## 🎨 [PoArt] PROTOKOL BUKTI BURUH (Proof of Art Protocol v1.0)

> **"Artis Sebenar, Pengeluaran Sebenar, Nilai Sebenar."**

Protokol ini; adalah **mekanisme pertahanan biologi dan intelektual** yang dibangunkan menentang penipu tanpa nama yang merangkumi ekosistem kripto, visual AI yang dihasilkan dalam 5 minit, dan budaya "Pump & Dump".

---

## a) Apakah [PoArt]? (Definisi Falsafah dan Teknikal)

**Proof of Art [PoArt];** adalah piawaian pengesahan institusi yang menjamin bahawa nilai di sebalik aset di blockchain tidak berdasarkan spekulasi; tetapi berdasarkan **buruh manusia**, **masa**, dan **tenaga fizikal** yang boleh disahkan.

Seperti Bitcoin menghasilkan nilai dengan *"Elektrik dan Kuasa Pemproses"* **(Proof of Work)**; projek yang mematuhi [PoArt] juga menghasilkan nilai dengan *"Bakat dan Masa Manusia yang Dibelanjakan"*. Mempertaruhkan masa.

Menghapuskan risiko *"Pembangun (Dev) menjual, projek selesai"* di platform Pump.fun dan DEX; kerana di sini nilai tidak disimpan dalam kod, tetapi dalam **kesinambungan pengeluaran**.

> **[PoArt] tidak berkata kepada peserta "Percayalah kepada kami"; tetapi berkata "Inilah buktinya, lihat dengan mata anda, sahkan dengan matematik anda."**

---

## b) Piawaian 5 Tiang [PoArt] (The 5 Pillars of Truth)

5 perkara ini adalah penapis yang tidak boleh dimanipulasi yang mesti dilalui oleh projek untuk menerima meterai [PoArt].

### 1) Bukti Identiti Langsung (Live Identity Proof)

- **Masalah:** Dunia kripto penuh dengan pengasas tanpa nama (Dev) yang tidak jelas identiti mereka mengumpul wang dan meninggalkan projek.
- **[PoArt] Penyelesaian:** Pengeluar membuktikan bukan sahaja kad pengenalan, tetapi **kehadiran mereka pada masa pengeluaran**. Ini bukan video pra-rakam, tetapi sesi siaran langsung yang berinteraksi dengan komuniti dan melaksanakan permintaan khusus segera.  
  (Cth: *"Tulis tarikh hari ini dan nombor blok semasa di sudut kanan kanvas"*)
- **Moto:** *"Bot boleh membuat gambar tetapi bot tidak berpeluh dan tidak boleh berimprovisasi."*

### 2) Bukti Buruh dan Proses (Labor & Process Proof)

- **Masalah:** Visual AI yang dihasilkan dalam 2 saat dan lukisan minyak yang dibuat dalam 2 bulan menerima layanan "jpeg" yang sama di dunia digital.
- **[PoArt] Penyelesaian:** Proses "kehamilan dan kelahiran" karya seni direkodkan. Peringkat lakaran, lapisan cat, jam terkumpul yang dibelanjakan, dan proses fizikal yang dialami oleh artis semasa mencipta karya itu didokumentasikan. Ini menambah **"Kos Masa" (Time Cost)** kepada token. Semakin sukar pengeluaran aset, semakin kukuh nilainya.

### 3) Bukti Nilai Estetik (Aesthetic Value Proof)

- **Masalah:** Budaya "Meme" yang mengabaikan estetika dan kedalaman artistik, hanya fokus pada komedi segera, dan menghasilkan projek "Hype" jangka pendek.
- **[PoArt] Penyelesaian:** Projek mesti mempunyai piawaian seni akademik, teori warna, peraturan komposisi, dan pengetahuan bahan (Impasto, Tekstur dll.). Kandungan tidak sepatutnya hanya membuat ketawa; mesti menimbulkan kagum pada penonton dan mempunyai **nilai koleksi**.

### 4) Inovasi Konseptual (Conceptual Novelty)

- **Masalah:** Beribu-ribu syiling anjing/kucing yang menyalin antara satu sama lain, jauh dari kreativiti.
- **[PoArt] Penyelesaian:** Projek mesti membina jambatan baru yang menggabungkan seni, sains, falsafah, atau teknologi dalam struktur yang bermakna.  
  (Cth: Menggabungkan arca David klasik dengan data pasaran kripto; melalui ini memproses idea "menjadi batu" persepsi manusia dan boleh diasaskan dengan sumber saintifik.)  
  Karya bukan sekadar jamuan visual; tetapi juga cabaran intelektual yang membuatkan orang berfikir tentang **Sains, Falsafah, atau Teknologi**.

> [!IMPORTANT]
> **Contoh Rujukan (Kesan Las Palmitas):**  
> Di kawasan Las Palmitas Mexico yang bergelut dengan jenayah, lebih 200 rumah telah diubah menjadi jamuan pelangi besar. Hasil daripada campur tangan estetik ini, kadar jenayah di kawasan itu menurun pada tahap tertentu, remaja mula fokus kepada seni bukannya kumpulan. Perubahan estetik mengekod semula rasa hormat orang terhadap persekitaran mereka dan antara satu sama lain (Social Cohesion).
>
> **Jangkaan:** Projek yang akan masuk ke senarai [PoArt]; seperti contoh di atas, mesti mempunyai hubungan sebab-akibat sosiologi, saintifik, atau falsafah melebihi estetika visual semata-mata. Kerana satu-satunya perkara yang tidak boleh dibeli dengan wang adalah "Masa", dalam protokol ini masa mesti dipertaruhkan sebagai cagaran dan dibuktikan. Asas intelektual projek mesti sangat kuat dan universal sehingga; walaupun dalam senario CTO (Community Take Over) yang mungkin bertahun-tahun kemudian, komuniti boleh mewarisi legasi ini dan secara autonomi meneruskan potensi inovatif projek.

### 5) Kehendak Bukan Algoritma (Non-Algorithmic Agency)

- **Masalah:** Pengeluaran digital yang sempurna tetapi tanpa jiwa, berulang-ulang.
- **[PoArt] Penyelesaian:** Kehendak asal manusia yang boleh membuat kesilapan, mengambil risiko, dan mengalami turun naik emosi mesti dirasakan dalam karya. Ketidakpastian dalam sapuan berus, tindak balas bahan yang tidak dijangka, dan keputusan segera artis adalah **Tandatangan Biologi** yang memisahkan karya daripada "Pengeluaran Mesin".

---

**(Tamat Bahagian 1 - Bahagian 2 akan diteruskan...)**
# Protokol PoArt - Bahagian 2

## c) Mekanisme Pengesahan & Anti-Penipuan

Sistem ini menjamin bahawa projek bukan sahaja "pada permulaan" tetapi "selamanya" boleh dipercayai dan hidup.

### 📦 Pakej Bukti (Evidence Pack - The Digital Twin)

Di sebalik setiap karya seni yang diperakui [PoArt], terdapat pakej data yang disulitkan dan dicap masa yang boleh dimuat turun oleh pelabur:

- **Rakaman Video RAW:** Rakaman mentah berterusan bagi detik pengeluaran.
- **Analisis Metadata:** Tarikh penciptaan fail, maklumat peranti yang digunakan, dan data lokasi (Bandar-Negara).
- **Rujukan Fizikal:** Bukti bahawa karya seni wujud di dunia fizikal  
  (Cth: Akhbar semasa yang berdiri di sebelah karya seni atau data blockchain pada masa itu).

> *Nota ketekalan:* Ungkapan "pakej bukti" disambungkan kepada garis **Evidence Pack → EvidenceRoot → NotarySeal** di bahagian sebelumnya; iaitu integriti pakej diwakili oleh meterai yang boleh disahkan.

### 🔄 Pembaharuan 365 Hari (The Sustainability Protocol)

- **Ciri Revolusioner:** Dalam projek kripto, "Dev" (Pembangun) mengeluarkan token ke pasaran dan biasanya hilang selepas 1-2 bulan (Soft Rug). [PoArt] menjadikan ini mustahil.
- **Peraturan:** Status "Verified Artist" (Artis Disahkan) bukan seumur hidup. Hanya sah untuk **1 tahun**.
- **Operasi:** Artis/Pembangun mesti mempersembahkan **karya seni baru, besar, dan boleh dibuktikan** kepada komuniti setiap 365 hari.
- **Senario Contoh:** Anda memulakan projek pada 2026. Pada Januari 2027, sistem memberi amaran "Tempoh Bukti Tamat". Jika artis tidak mempersembahkan pameran baru, karya fizikal baru, atau integrasi teknologi baru, "Lencana Kepercayaan" projek akan jatuh.
- **Hasil:** Sistem ini menjamin bahawa **kandungan tidak akan pernah lapuk** dan pelabur tidak perlu risau *"Adakah pembangun masih di sini?"* Projek menjadi studio yang hidup.

### 🚩 Protokol Bendera Merah (Red Flag Protocol)

**Dalam kes sebarang penipuan (penggunaan AI, karya curi, video dimanipulasi) yang dikesan oleh komuniti atau algoritma:**

1. Sijil segera ditanda sebagai **"BATAL" (VOID)**.
2. Pakej bukti ditanda sebagai **"Palsu"** secara terbuka.
3. Projek dimasukkan ke dalam senarai hitam [PoArt]. Ini mengukuhkan hakikat bahawa **reputasi adalah satu-satunya mata wang** di dunia terdesentralisasi.
4. Tidak boleh menggunakan ungkapan [PoArt] dalam sebarang penerbitan, sumber sah tunggal ialah https://www.ilhanart.org/public-registry

---

## d) Kesimpulan: Bukan Kasino, Tetapi Muzium

**Pump.fun dan Pertukaran Terdesentralisasi (DEX) pada masa ini malangnya adalah kasino; lampu berkelip, semua orang mengejar keuntungan cepat, dan rumah (penipu) sentiasa menang. Sebab kami memulakan projek di sini adalah kerana kami juga cuba memperbaikinya dan kerana dengan data sedia ada dan siaran langsung kami mempunyai persekitaran yang boleh mencapai penonton semasa.**

**[PoArt] adalah kubu yang dibina di tengah kasino ini.**

- 🎰 Kasino bergantung kepada permainan kad; kami bergantung kepada **realiti fizikal**
- 🃏 Kasino terbuka kepada penipuan; kami terbuka kepada **bukti telus**
- ⏳ Kasino sementara; kami fokus kepada **keabadian seni dan sains**

**Token yang menggunakan protokol ini bukan sekadar "syiling"; ia adalah saham digital dengan peluh, cat, kod, dan falsafah di belakangnya.**

---

## 🗳️ 6) TADBIR URUS DAN DAFTAR AWAM (Governance & Public Registry)

**Tujuan bahagian ini adalah: mengeluarkan piawaian [PoArt] dari tahap "kepercayaan kepada orang" dan menjadikannya infrastruktur awam yang mampan dengan rekod + pengesahan + pengawasan komuniti.**

### 6.1 Daftar Awam (Public Registry)

- **Public Registry:** Semua data yang diluluskan direkodkan di `ilhanart.org/registry` (atau GitHub Registry).

**Logik rekod (piawaian yang disyorkan - format laluan JSON):**

Setiap rekod yang memasuki daftar mempunyai medan teras yang boleh disahkan minimum ini:

- **Identiti & Status:**
  - `certificate_id` (rujukan boleh dibaca)
  - `status` (active / void)
  - `void_reason` (jika ada)
  - `visibility` (private / masked / public)
  - `created_at` (cap masa)

- **Institusi Penerbit:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Maklumat Karya Seni:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet`
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
  - `governance.review_notes`

---

### 6.2 Proses Permohonan PoArt Verified

**Permohonan PoArt Verified disemak oleh İlhanArt Gallery mengikut 5 piawaian PoArt. Maklum balas komuniti diambil kira, tetapi keputusan muktamad bergantung kepada pasukan kurator. Keputusan dijelaskan secara telus dan direkodkan di ilhanart.org/registry.**

#### Proses Permohonan

**Permohonan:**
- Artis/projek memohon PoArt Verified
- Evidence Pack disediakan (rakaman video, metadata, pautan siaran langsung)
- Permohonan dihantar ke İlhanArt Gallery

**Semakan (30 Hari):**
- Pasukan galeri menyemak Evidence Pack secara terperinci
- Semua 5 piawaian PoArt disemak:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Temu bual dengan artis (pilihan)

**Perundingan Komuniti:**
- Evidence Pack dikongsi secara terbuka semasa proses permohonan
- Komuniti boleh memberikan maklum balas melalui ilhanart.org
- Pemegang token (minimum 10,000 $CULTURE) boleh membuat cadangan
- **Semua maklum balas diambil kira dalam proses semakan**
- **Tetapi keputusan muktamad bergantung kepada penilaian kurator**

**Keputusan:**
- Galeri meluluskan atau menolak permohonan
- Rasional keputusan dijelaskan secara telus
- Jika diluluskan → PoArt Verified badge
- Jika ditolak → boleh memohon semula selepas 6 bulan

**Ketelusan:**
- Semua permohonan dan keputusan direkodkan di ilhanart.org/registry
- Rekod keputusan diterbitkan secara terbuka:
  - Tarikh permohonan
  - Ringkasan proses semakan
  - Keputusan (Approved / Rejected)
  - Rasional keputusan (penjelasan ringkas)
  - Ringkasan maklum balas komuniti (tanpa nama)

#### Mengapa Keputusan Kurator?

**Kawalan Kualiti:**  
Status PoArt Verified adalah lencana berstandar tinggi. Penilaian kurator menjamin pemeliharaan piawaian ini.

**Pencegahan Manipulasi Spekulatif:**  
Dengan token Pump.fun, tadbir urus on-chain penuh (cth: Realms, DAO voting) secara teknikal tidak mungkin. Sistem pengundian off-chain terbuka kepada manipulasi whale dan serangan yang diselaraskan. Keputusan kurator menghapuskan risiko ini.

**Kecekapan Operasi:**  
Proses keputusan yang cepat dan jelas berbanding mekanisme pengundian yang kompleks. Artis mendapat hasil dalam 30 hari.

**Penyertaan Komuniti:**  
Maklum balas komuniti diambil kira sepenuhnya dan mempengaruhi proses keputusan. Tetapi keputusan muktamad adalah dengan pasukan kurator yang dilindungi daripada manipulasi.

**Masa Depan:**  
Apabila projek matang (2027+), mekanisme perundingan komuniti boleh diperkukuh. Tetapi perlindungan piawaian kurator kekal tetap.

---

### 6.3 Utiliti Token (Kegunaan Token)

**Manfaat yang diberikan kepada pemegang token $CULTURE:**

**1. Akses Keutamaan Acara Galeri:**
- Hak untuk mengadakan pameran 1 minggu setahun di İlhanArt Gallery (hak boleh dipindahkan)
- Diskaun drop painting
- Hak diskaun 10% hingga 30% untuk lukisan di galeri

**2. Akses Penuh PoArt Registry:**
- Rekod terperinci semua authenticated artworks
- Versi penuh Evidence Packs
- Alat pengesahan forensik

**3. Advisory Voting:**
- Hak perundingan dalam permohonan PoArt Verified
- Akses kepada saluran maklum balas komuniti
- Penyertaan dalam perbincangan tadbir urus

**4. Exclusive Content:**
- Kandungan behind-the-scenes studio
- Temu bual artis dan video proses
- Akses dokumentasi teknikal

**Nota:**  
Pemegang token memberikan undi penasihat (advisory vote). Keputusan muktamad adalah dengan pasukan kurator. Struktur ini dipilih untuk mengelakkan manipulasi whale dan serangan spekulatif. Tiada ganjaran staking kerana kami mencari peserta budaya jangka panjang, bukan modal mercenary jangka pendek.

---

### 6.4 Metadata Sync (Penyegerakan dengan Dunia Fizikal)

**Mentakrifkan "padanan 100%" secara teknikal:**

- **Padanan minimum (wajib):**
  - `asset.fingerprints.sha256/sha512` dalam daftar dan hash fail yang dipegang mesti **betul-betul sama**.
  - `proof.notary_seal` dalam daftar apabila dijana semula (jika ada Evidence Pack) mesti **betul-betul sama**.

---

### 6.5 Pertikaian, Semakan, dan Pembatalan

Daftar bukan sahaja mekanisme "kelulusan"; tetapi **mekanisme pengawasan hidup terhadap penipuan**.

- Apabila pertikaian dimulakan, rekod boleh dimasukkan ke dalam mod **"review"**.
- Jika penipuan dikesan, ditanda sebagai `status: void` dan rasional ditambah:
  - `void_reason` (penggunaan AI / curi / manipulasi dll.)
  - `revoked_at` (masa pembatalan)
- Sumber keputusan pembatalan jelas kelihatan dalam daftar:
  - semakan kurator / pertikaian komuniti / nota analisis forensik (yang mana berkenaan)

---

### 6.6 Contoh Rekod Daftar (Machine-readable)

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
      "sha512": "41e5e0d007a2a77b6e0e3ebc548fbaa2788ea265193434f58d23e8c0f5bb20a0..."
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
    "review_notes": "Met all 5 PoArt standards."
  }
}
```

---

## 7) 🔐 METERAI TEKNIKAL (NOTARY SEAL)

**Algoritma meterai tidak bergerak yang dihasilkan oleh PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

## 🗺️ Roadmap: Masa Depan "Trustless"

### Fasa 1: Beta v1.0 (Langsung Sekarang)

**Infrastruktur:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + IPFS backup)
- Gallery self-attestation (berpusat tetapi telus)

**Token:**
- Platform: Pump.fun
- Liquidity: Raydium (automatic)
- Governance: Advisory only (perundingan komuniti)

**Tujuan:**
- Kelajuan, hapuskan halangan UX
- Keselamatan "tanpa geseran"
- Pembinaan komuniti

**Token Utility (v1.0):**
- Akses keutamaan acara galeri
- Paparan PoArt Registry
- Hak advisory voting

---

### 🚀 Fasa 2: Decentralized Authority (2026 Q2-Q4)

| Ciri | Apa yang Diperoleh? | Tech Stack | ETA |
|---------|---------------|------------|-----|
| **Edge Function INSERT** | Pencegahan spam + keselamatan API Key | Supabase Edge (Deno) | Q2 2026 |
| **Tandatangan Wallet** | Decentralized identity | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | Arkib terdesentralisasi | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | Pembatalan sijil palsu | DB Schema Update | Q2 2026 |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain voting (x/web) + wallet signature
- Pemilihan wakil komuniti
- Kawalan operasi multi-sig
- Weighted advisory voting (dengan whale cap)

---

### Fasa 3: Desentralisasi Penuh (2027+)

| Ciri | Sasaran | ETA |
|---------|-------|-----|
| **On-Chain Registry** | Rekod Solana on-chain | Q1 2027 |
| **Enhanced Token Utility** | NFT mint, ciri lanjutan | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **Legal Recognition** | Kesahihan di mahkamah Turki | 2027-2028 |

---

## 🔬 Kedalaman Teknikal: Algoritma Meterai

### Fungsi Hash Deterministik

```javascript
// Pengiraan FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// Penciptaan EvidenceRoot
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// Pengeluaran NotarySeal
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}
```

### Aliran Pengesahan (Dua Tahap)

#### Quick Verify (Pengesahan Pantas)

```javascript
// Semak hash fail sahaja (bendera merah pantas)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  if (userFileHash === originalHash) {
    return { valid: true, message: "✅ Asal - Hash fail sepadan" };
  } else {
    return { valid: false, message: "❌ Palsu - Fail dimanipulasi" };
  }
}
```

#### Full Verify (Pengesahan Penuh)

```javascript
// Jana semula EvidenceRoot dan NotarySeal dan sahkan
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  const cert = await fetchFromRegistry(certificateId);

  // 1) Semakan FileHash
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Palsu - Hash fail tidak sepadan" };
  }

  // 2) Jana semula EvidenceRoot
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Tidak sepadan - EvidenceRoot" };
  }

  // 3) Jana semula NotarySeal
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Tidak sepadan - NotarySeal" };
  }

  return { valid: true, message: "✅ Asal - Full Verify lulus" };
}
```

---

## 💬 Nota Terakhir

### Pump.fun dan Realiti

Projek ini dimulakan di Pump.fun kerana:
- ✅ Akses kecairan (Raydium automatic migration)
- ✅ Akses komuniti sedia ada
- ✅ Kos permulaan rendah

Tetapi mari kita jelaskan:
- **Harga token** bukan petunjuk kejayaan artistik
- **Bajet operasi** nilai token penting (galeri, pameran, infrastruktur)
- **Metrik kejayaan:** Authenticated artworks + community engagement + pelawat fizikal

### Tadbir Urus dan Desentralisasi

**Realiti v1.0 (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (berpusat tetapi telus)
- Governance: Advisory only (keputusan muktamad kurator)

**Visi v2.0+ (2027+):**
- Registry: On-chain (Solana)
- Signatures: Wallet-based (decentralized)
- Governance: Hybrid (community advisory + curatorial quality)

Struktur ini memberikan **kecekapan operasi** dan **kawalan kualiti** pada peringkat awal, sambil membuka jalan untuk **penyertaan komuniti** meningkat pada masa hadapan.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Budaya, Lebih Besar daripada Modal*

## 🧾 License

MIT License © 2026 İlhan Art Gallery Initiative

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) 
![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) 
![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) 
![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Projek ini dibangunkan dengan inisiatif [İlhan Art Gallery], kod sumber dibuka kepada orang ramai untuk ketelusan.**

**PROTOKOL V1.0 // DIMETERAI DENGAN SHA-512**

*© 2026 İLHAN ART | Hak Cipta Terpelihara untuk Karya Seni, Visual, dan Idea.*

---

**(Tamat Bahagian 2)**
