# 📚 TERMINOLOGI & GLOSARIUM KONSEP
> **"Memahami bahasa protokol ini berarti memahami visinya."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Infrastruktur Inti

**PoArt Forensic Engine (PFE)** mewakili lapisan inti logika dan operasi teknis di balik protokol [PoArt]. Ini adalah "mesin forensik" yang mengambil data produksi mentah karya seni dan mengubahnya menjadi **bukti digital** yang dapat diverifikasi dan tidak dapat diubah.

### 🧩 Mengapa "PoArt Forensic"?

- **PoArt (Proof of Art):** Fokus mesin adalah menghubungkan nilai aset digital bukan dengan spekulasi tetapi dengan **proses produksi yang dapat dibuktikan**.
- **Forensic (Verifikasi Forensik):**
  - **Definisi Teknis:** Pendekatan algoritma dan rantai pencatatan untuk memverifikasi bahwa data yang berkaitan dengan proses produksi (sapuan kuas, timelapse, log) tidak dimanipulasi.
  - **Lapisan Filosofis:** Klaim untuk mengubah produksi manusia yang mengandung **waktu, usaha, dan biaya keputusan** menjadi realitas terukur, berlawanan dengan "output instan" kecerdasan buatan.

> Catatan: Integrasi blockchain (misalnya Solana) bukan inti dari PFE; ini ditangani secara terpisah sebagai **Chain Anchor Layer** untuk verifikasi/registri.

### 🛠️ Cakupan Teknis v1.0

**PoArt Forensic Engine (PFE) v1.0** dibangun di atas **3 pilar utama** alih-alih model keuangan yang kompleks:

1. **Hashing & Sealing (Penyegelan):**  
   PFE memproses semua elemen dalam Evidence Pack (file karya, video, JSON/log, tanda tangan, dll.) secara deterministik dan menghasilkan nilai **NotarySeal** yang unik.

   **Konsep inti (v1.0):**
   - **FileHash (sidik jari karya):** Hash yang dihasilkan dari byte file karya.
   - **EvidenceRoot (akar paket bukti):** Ringkasan akar yang mewakili integritas Evidence Pack (Merkle root atau canonical manifest hash).
   - **NotarySeal (segel akhir / Output PFE):** Segel akhir yang dihasilkan dari kombinasi EvidenceRoot + waktu + tanda tangan.

   **Rumus (disajikan dengan jelas untuk investor):**
   
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
   
   > Catatan: Nilai yang dimaksud sebagai output PFE adalah **NotarySeal**. Mekanisme **SignerSignature** akan diaktifkan di Fase 2 (dengan Solana Wallet Adapter); v1.0 saat ini menggunakan tanda tangan attestation sistem. Kunci publik attestation dipublikasikan di field `issuer.attestation_pubkey` dalam registri.

2. **Indexing (Pengarsipan):**  
   Mencatat wallet mana yang mengirimkan **Labor Proof (Bukti Kerja)** untuk karya mana pada tanggal berapa ke dalam lapisan pencatatan yang transparan dan dapat dicari.  
   *(Lapisan ini bisa berupa database; integrasi rantai didefinisikan secara terpisah sebagai "Chain Anchor Layer".)*

3. **Verification (Verifikasi):**  
   Ketika keaslian karya ditanyakan, PFE memproses ulang bukti mentah; menguji dengan kepastian matematis apakah nilai **EvidenceRoot / NotarySeal** yang dihitung cocok dengan catatan dalam arsip.

---

### 🧮 Teorema Nilai PoArt (The Value Theorem)

Protokol [PoArt] menghubungkan nilai ($V$) aset digital bukan dengan persepsi pasar subjektif tetapi dengan **realitas fisik proses produksi**.

Kecerdasan Buatan (AI) menghancurkan proses dengan memberikan hasil instan ($t \to 0$). [PoArt] mempertimbangkan nilai sebagai akumulasi komponen **waktu, tenaga kerja, dan kehendak**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definisi Variabel

- **$\int dt$ (Akumulasi Proses):**  
  Nilai bukan "output" instan; ini adalah **proses** yang terakumulasi antara $t_{\text{start}}$ dan $t_{\text{end}}$. Ketika waktu berkurang (produksi AI), hasil integral mendekati 0.

- **$P_{\text{labor}}(t)$ (Intensitas Tenaga Kerja Instan):**  
  Mewakili intensitas usaha mental dan fisik yang dihabiskan pada saat produksi. Ketika usaha yang dapat dibuktikan meningkat, integrand meningkat.  
  > Catatan: Istilah ini dapat dinormalisasi secara praktis melalui "sinyal tenaga kerja yang dapat diukur/dibuktikan".

- **$I_{\text{agency}}(t)$ (Koefisien Kehendak):**  
  Kapasitas pengambilan risiko dan pengambilan keputusan produsen. Mengambil nilai antara $0$ dan $1$.
  - **AI ($I \approx 0$):** Menjalankan perintah, tidak mengambil risiko, tidak membayar harga.
  - **Manusia ($I \to 1$):** Mengubah keputusan, ragu-ragu, mengambil risiko.

- **$U_{\text{irreversible}}$ (Keunikan Tidak Dapat Dibalik):**  
  Dalam produksi digital, undo (`Ctrl+Z`) dimungkinkan; tetapi dalam produksi fisik (cat di kanvas, marmer yang dipahat, gestur dalam siaran langsung), tidak ada jalan kembali. **Ketidakreversibilitasan** ini adalah istilah tambahan yang menciptakan "keunikan" (karakter non-fungible) dalam karya.

### 🔎 Analisis Kasus: AI "Output Instan" vs. "Proses Terbukti" Manusia

Skenario berikut menunjukkan bagaimana **Teorema Nilai PoArt** bekerja dalam praktik dan mengapa produksi AI mendapat skor rendah dalam standar [PoArt].

#### Skenario A: Produksi Gambar AI dalam 10 Detik

- **Waktu ($\Delta t$):** $10$ detik (hampir tidak ada proses)
- **Intensitas Tenaga Kerja ($P_{\text{labor}}$):** $1$ unit (hanya menulis perintah)
- **Koefisien Kehendak ($I_{\text{agency}}$):** $0.01$ (tidak ada risiko, tidak ada harga)
- **Ketidakreversibilitasan ($U_{\text{irreversible}}$):** $0$ (dapat di-undo / disalin)

**Hasil:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Komentar:** Bahkan jika output sempurna; karena proses tidak dialami dan tidak mengandung kehendak/risiko, nilai [PoArt] mendekati $0$.

#### Skenario B: Produksi Fisik 6 Jam di Livestream

- **Waktu ($\Delta t$):** $6$ jam ($21{,}600$ detik)
- **Intensitas Tenaga Kerja ($P_{\text{labor}}$):** $0.5$ unit (kontinuitas usaha fisik dan mental)
- **Koefisien Kehendak ($I_{\text{agency}}$):** $0.9$ (mengubah keputusan, mengambil risiko, pilihan tidak dapat dibalik)
- **Ketidakreversibilitasan ($U_{\text{irreversible}}$):** $>0$ (jejak fisik tidak dapat di-undo)

**Hasil:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Komentar:** Ketika proses memanjang dan kehendak (risiko) meningkat, nilai meningkat secara kumulatif. Istilah $U_{\text{irreversible}}$ adalah kontribusi tambahan yang menciptakan "keunikan" (karakter non-fungible) dalam karya.

---

### ✅ Kesimpulan: Mengunci Nilai dengan Bukti (Proof-Bound Value)

Teorema ini mengubah klaim nilai [PoArt] dari "suka" atau "narasi pasar" menjadi **fakta produksi yang dapat dibuktikan**.

1. **Tanpa Proses, Tidak Ada Nilai:**  
   AI menghancurkan proses dengan output instan ($t \to 0$). Ketika jendela proses menyempit, hasil integral berkurang sebagai keharusan matematis:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Kehendak dan Risiko adalah Pengali:**  
   [PoArt] mengukur tidak hanya "waktu yang dihabiskan" tetapi juga lapisan keputusan, risiko, dan biaya nyata dalam waktu itu. Nilai produksi yang tidak mengambil risiko (AI) rendah:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Keunikan adalah Bukti Fisik, Bukan Marketing:**  
   Dalam produksi fisik, jejak yang tidak dapat dibalik (goresan kanvas, retakan marmer) berada di luar logika `Ctrl+Z` digital. Ketidakreversibilitasan ini ($U_{\text{irreversible}}$) membuat karya menjadi unik secara ontologis.

> **🔐 RINGKASAN:** Meskipun teorema nilai tampak tidak pasti sebagai pengukuran (bahkan jika tidak dapat diukur 100% dalam kehidupan nyata), tujuan rumus ini adalah menunjukkan konstruksi dan arah variabel. Yang langka di era AI bukan "gambar" tetapi **tenaga kerja, waktu, dan kehendak yang dapat dibuktikan**. [PoArt] mengukur kelangkaan ini dan mendaftarkannya dengan **Evidence Pack**.

### 🏛️ Pentingnya Konsep "Engine" (Mesin)

Token yang diluncurkan dari Pump.fun atau platform serupa seringkali hanya **"tiket masuk"**. **PoArt Forensic Engine (PFE)** adalah **lapisan logika konstitusional** yang menentukan hak apa yang dilindungi tiket itu, bagaimana tenaga kerja akan dicatat, dan bagaimana seni/sains/teknologi akan dilestarikan.

> **Catatan:** Alasan kami memulai proyek ini di Pump.fun adalah karena kami tidak memiliki likuiditas dan jumlah pengikut yang cukup. Menggunakan data yang ada mungkin bukan strategi berkualitas tertinggi tetapi merupakan langkah yang paling tepat. Terlepas dari anggaran dan sumber daya, mendefinisikan logika mesin ini di GitHub membuktikan bahwa proyek ini bukan hanya spekulasi keuangan tetapi **infrastruktur perangkat lunak** jangka panjang dan visi **perpustakaan digital nasional**.

---

## 🎨 PROTOKOL [PoArt] BUKTI KERJA SENI (Proof of Art Protocol v1.0)

> **"Seniman Nyata, Produksi Nyata, Nilai Nyata."**

Protokol ini adalah **mekanisme pertahanan biologis dan intelektual** yang dikembangkan melawan penipu anonim yang merajalela di ekosistem kripto, gambar AI yang diproduksi dalam 5 menit, dan budaya "Pump & Dump".

---

## a) Apa itu [PoArt]? (Definisi Filosofis dan Teknis)

**Proof of Art [PoArt];** adalah standar verifikasi institusional yang menjamin bahwa nilai di balik aset di blockchain dijamin bukan oleh spekulasi tetapi oleh **tenaga kerja manusia** yang dapat diverifikasi, **waktu**, dan **energi fisik**.

Seperti Bitcoin menciptakan nilai melalui *"Listrik dan Kekuatan Pemrosesan"* **(Proof of Work)**; proyek yang sesuai [PoArt] menciptakan nilai melalui *"Bakat dan Waktu Manusia yang Dihabiskan"*. Ini "Stake" Waktu.

Ini menghilangkan risiko *"Developer (Dev) menjual, proyek selesai"* di Pump.fun dan platform DEX; karena di sini nilai tidak ada dalam kode tetapi dalam **kontinuitas produksi**.

> **[PoArt] tidak berkata kepada peserta "Percayalah pada kami"; ia berkata "Ini buktinya, lihat dengan matamu, verifikasi dengan matematikamu."**

---

## b) Standar 5 Pilar [PoArt] (The 5 Pillars of Truth)

5 item ini adalah filter yang tidak dapat dimanipulasi yang harus dilewati proyek untuk menerima segel [PoArt].

### 1) Bukti Identitas Langsung (Live Identity Proof)

- **Masalah:** Dunia kripto penuh dengan pendiri anonim (Dev) yang mengumpulkan uang dan meninggalkan proyek.
- **Solusi [PoArt]:** Produsen membuktikan tidak hanya kartu identitas tetapi juga **kehadiran pada saat produksi**. Ini mencakup sesi livestream di mana mereka berinteraksi dengan komunitas dan memenuhi permintaan spesifik instan, bukan video yang direkam sebelumnya.  
  (Contoh: *"Tulis tanggal hari ini dan nomor blok saat ini di sudut kanan kanvas"*)
- **Motto:** *"Bot bisa melukis tetapi bot tidak bisa berkeringat dan berimprovisasi."*

### 2) Bukti Tenaga Kerja dan Proses (Labor & Process Proof)

- **Masalah:** Gambar AI yang diproduksi dalam 2 detik dan lukisan minyak yang dibuat dalam 2 bulan menerima perlakuan "jpeg" yang sama di dunia digital.
- **Solusi [PoArt]:** "Proses kehamilan dan kelahiran" karya dicatat. Tahap sketsa, lapisan cat, jam kumulatif yang dihabiskan, dan proses fisik yang dialami seniman saat membuat karya didokumentasikan. Ini menambahkan **"Biaya Waktu" (Time Cost)** ke token. Semakin sulit memproduksi aset, semakin kokoh nilainya.

### 3) Bukti Nilai Estetika (Aesthetic Value Proof)

- **Masalah:** Budaya "Meme" mengabaikan estetika dan kedalaman artistik, hanya fokus pada komedi instan, menghasilkan proyek "Hype" berumur pendek.
- **Solusi [PoArt]:** Proyek harus memiliki standar seni akademis, teori warna, aturan komposisi, dan pengetahuan material (Impasto, Tekstur, dll.). Konten tidak hanya harus membuat tertawa; harus membangkitkan kekaguman pada penonton dan memiliki **nilai koleksi**.

### 4) Inovasi Konseptual (Conceptual Novelty)

- **Masalah:** Ribuan koin anjing/kucing yang saling menyalin, tanpa kreativitas.
- **Solusi [PoArt]:** Proyek harus membangun jembatan baru yang menggabungkan seni, sains, filosofi, atau teknologi dengan cara yang bermakna.  
  (Contoh: Menggabungkan patung David klasik dengan data pasar kripto; memproses ide persepsi manusia "membatu" dan mampu membuktikannya dengan sumber ilmiah.)  
  Karya tidak hanya harus menjadi pesta visual; juga harus menjadi tantangan intelektual yang membuat orang berpikir tentang **Sains, Filosofi, atau Teknologi**.

> [!IMPORTANT]
> **Contoh Referensi (Efek Las Palmitas):**  
> Di lingkungan Las Palmitas di Meksiko yang bergulat dengan kejahatan, lebih dari 200 rumah diubah menjadi pesta pelangi raksasa. Setelah intervensi estetika ini, tingkat kejahatan di lingkungan tersebut menurun hingga tingkat tertentu, kaum muda mulai tertarik pada seni daripada geng. Perubahan estetika memprogram ulang rasa hormat orang terhadap lingkungan dan satu sama lain (Kohesi Sosial).
>
> **Harapan:** Proyek yang ingin masuk daftar [PoArt] harus mengandung hubungan sebab-akibat sosiologis, ilmiah, atau filosofis di luar estetika visual murni, seperti contoh di atas. Karena "Waktu" adalah satu-satunya aset yang tidak dapat dibeli dengan uang, dalam protokol ini, waktu harus di-stake sebagai jaminan dan dibuktikan. Fondasi konseptual proyek harus begitu kuat dan universal sehingga, bahkan dalam skenario CTO (Community Take Over) yang mungkin terjadi bertahun-tahun kemudian, komunitas dapat mewarisi warisan ini dan melanjutkan potensi inovatif proyek secara otonom.

### 5) Kehendak Non-Algoritmik (Non-Algorithmic Agency)

- **Masalah:** Produksi digital yang sempurna tetapi tanpa jiwa, berulang.
- **Solusi [PoArt]:** Kehendak unik manusia yang dapat membuat kesalahan, mengambil risiko, dan mengalami fluktuasi emosional harus terasa dalam karya. Ketidakpastian dalam sapuan kuas, reaksi material yang tidak terduga, dan keputusan instan seniman adalah **Tanda Tangan Biologis** yang membedakan karya dari "Produksi Mesin".

---

## c) Mekanisme Verifikasi & Anti-Pemalsuan

Sistem ini memastikan proyek tetap dapat dipercaya dan hidup tidak hanya "di awal" tetapi "selamanya".

### 📦 Paket Bukti (Evidence Pack - The Digital Twin)

Di balik setiap karya bersertifikat [PoArt] ada paket data terenkripsi dan bertanda waktu yang dapat diunduh investor:

- **Rekaman Video RAW:** Rekaman mentah tanpa gangguan dari momen produksi.
- **Analisis Metadata:** Tanggal pembuatan file, informasi perangkat yang digunakan, dan data lokasi (Kota-Negara).
- **Referensi Fisik:** Bukti bahwa karya ada di dunia fisik  
  (Contoh: Koran saat ini yang diletakkan di samping karya atau data blockchain pada saat itu).

> *Catatan konsistensi:* Istilah "paket bukti" terhubung ke rantai **Evidence Pack → EvidenceRoot → NotarySeal** di bagian sebelumnya; yaitu integritas paket diwakili oleh segel yang dapat diverifikasi.

### 🔄 Pembaruan 365 Hari (The Sustainability Protocol)

- **Fitur Revolusioner:** Dalam proyek kripto, "Dev" (Developer) meluncurkan token ke pasar dan biasanya menghilang setelah 1-2 bulan (Soft Rug). [PoArt] membuat ini tidak mungkin.
- **Aturan:** Status "Verified Artist" (Seniman Terverifikasi) tidak permanen. Hanya berlaku **1 tahun**.
- **Operasi:** Seniman/Developer harus menyajikan kepada komunitas **karya baru, besar, dan dapat dibuktikan** setiap 365 hari.
- **Skenario Contoh:** Anda memulai proyek pada tahun 2026. Pada Januari 2027, sistem memberikan peringatan "Periode Bukti Berakhir". Jika seniman tidak menyajikan pameran baru, karya fisik baru, atau integrasi teknologi baru, "Lencana Kepercayaan" proyek akan turun.
- **Hasil:** Sistem ini memastikan **konten tidak pernah usang** dan investor tidak mengalami ketakutan *"Apakah developer masih di sini?"*. Proyek menjadi studio yang hidup.

### 🚩 Protokol Bendera Merah (Red Flag Protocol)

**Jika ada pemalsuan (penggunaan AI, karya curian, video yang dimanipulasi) terdeteksi oleh komunitas atau algoritma:**

1. Sertifikat segera ditandai sebagai **"BATAL" (VOID)**.
2. Paket bukti diberi label publik sebagai **"Palsu"**.
3. Proyek dimasukkan ke daftar hitam [PoArt]. Ini memperkuat fakta bahwa di dunia terdesentralisasi, **reputasi adalah satu-satunya mata uang**.
4. Pernyataan [PoArt] tidak dapat dimasukkan dalam publikasi apa pun; satu-satunya sumber yang valid adalah https://www.ilhanart.org/public-registry

---

## d) Kesimpulan: Bukan Kasino, Tapi Museum

**Pump.fun dan Bursa Terdesentralisasi (DEX) saat ini sayangnya adalah kasino; lampu berkedip, semua orang mengejar keuntungan cepat, dan rumah (penipu) selalu menang. Alasan kami memulai proyek di sini juga untuk mencoba memperbaiki tempat ini, dan karena kami memiliki data yang ada dan lingkungan untuk menjangkau audiens yang ada melalui livestream.**

**[PoArt] adalah benteng yang dibangun di tengah kasino ini.**

- 🎰 Kasino bergantung pada permainan kertas; kami bergantung pada **realitas fisik**.
- 🃏 Kasino terbuka untuk kecurangan; kami terbuka untuk **bukti transparan**.
- ⏳ Kasino bersifat sementara; kami fokus pada **keabadian seni dan sains**.

**Token yang menggunakan protokol ini bukan hanya "koin"; ini adalah saham digital yang mengandung keringat, cat, kode, dan filosofi di belakangnya.**

---

## 🗳️ 6) TATA KELOLA DAN REGISTRI PUBLIK (Governance & Public Registry)

**Tujuan bagian ini: Mengubah standar [PoArt] dari bidang "kepercayaan pada individu" menjadi infrastruktur publik berkelanjutan dengan registrasi + verifikasi + pengawasan komunitas.**

### 6.1 Public Registry (Registri Publik)

- **Public Registry:** Semua data yang disetujui dicatat di `ilhanart.org/registry` (atau GitHub Registry).

**Logika registrasi (standar yang disarankan - format path JSON):**

Setiap catatan yang masuk ke registri membawa field inti yang dapat diverifikasi minimal berikut:

- **Identitas & Status:**
  - `certificate_id` (referensi yang dapat dibaca)
  - `status` (active / void)
  - `void_reason` (jika ada)
  - `visibility` (private / masked / public)
  - `created_at` (timestamp)

- **Organisasi Penerbit:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informasi Karya:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (jika memungkinkan; untuk identitas pemegang token)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Data Forensik:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Bukti Kriptografis:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Tata Kelola:**
  - `governance.decision`
  - `governance.review_notes`

Registri dapat memiliki dua lapisan:
- **1)** Indeks yang dapat dibaca manusia (daftar web / pencarian / filter)
- **2)** Manifest yang dapat dibaca mesin (catatan JSON; untuk verifikasi PFE)

**"Catatan" di sini dapat diverifikasi dengan rantai Evidence Pack → EvidenceRoot → NotarySeal dari PFE. Registri menyediakan target verifikasi, bukan "klaim".**

---

### 6.2 Proses Pendaftaran PoArt Verified

**Pendaftaran PoArt Verified dievaluasi oleh İlhanArt Gallery sesuai dengan 5 standar PoArt. Umpan balik komunitas dipertimbangkan, tetapi keputusan akhir ada pada tim kuratorial. Keputusan diumumkan secara transparan dan dicatat di ilhanart.org/registry.**

#### Proses Pendaftaran

**Pendaftaran:**
- Seniman/proyek mengajukan pendaftaran PoArt Verified
- Evidence Pack disiapkan (rekaman video, metadata, tautan livestream)
- Pendaftaran dikirim ke İlhanArt Gallery

**Peninjauan (30 Hari):**
- Tim galeri meninjau Evidence Pack secara detail
- Semua 5 standar PoArt diperiksa:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Wawancara dengan seniman (opsional)

**Konsultasi Komunitas:**
- Evidence Pack dibagikan secara publik selama proses pendaftaran
- Komunitas dapat memberikan umpan balik melalui ilhanart.org
- Pemegang token (minimum 10,000 $CULTURE) khususnya dapat memberikan saran
- **Semua umpan balik dipertimbangkan dalam proses peninjauan**
- **Namun, keputusan akhir bergantung pada evaluasi kuratorial**

**Keputusan:**
- Galeri menyetujui atau menolak pendaftaran
- Alasan keputusan diumumkan secara transparan
- Jika disetujui → Lencana PoArt Verified
- Jika ditolak → Dapat mendaftar ulang setelah 6 bulan

**Transparansi:**
- Semua pendaftaran dan keputusan dicatat di ilhanart.org/registry
- Catatan keputusan dipublikasikan secara publik:
  - Tanggal pendaftaran
  - Ringkasan proses peninjauan
  - Keputusan (Approved / Rejected)
  - Alasan keputusan (penjelasan singkat)
  - Ringkasan umpan balik komunitas (anonim)

#### Mengapa Keputusan Kuratorial?

**Kontrol Kualitas:**  
Status PoArt Verified adalah lencana dengan standar tinggi. Evaluasi kuratorial menjamin standar-standar ini dipertahankan.

**Pencegahan Manipulasi Spekulatif:**  
Tata kelola on-chain penuh (misalnya: Realms, DAO voting) tidak layak secara teknis dengan token Pump.fun. Sistem voting off-chain rentan terhadap manipulasi whale dan serangan terkoordinasi. Keputusan kuratorial menghilangkan risiko ini.

**Efisiensi Operasional:**  
Proses keputusan yang cepat dan jelas alih-alih mekanisme voting yang kompleks. Seniman mendapatkan hasil dalam 30 hari.

**Partisipasi Komunitas:**  
Umpan balik komunitas sepenuhnya dipertimbangkan dan mempengaruhi proses keputusan. Namun, keputusan akhir ada pada tim kuratorial yang dilindungi dari manipulasi.

**Masa Depan:**  
Ketika proyek matang (2027+), mekanisme konsultasi komunitas dapat diperkuat. Namun, perlindungan standar kuratorial bersifat permanen.

---

### 6.3 Token Utility (Kegunaan Token)

**Manfaat yang diberikan kepada pemegang token $CULTURE:**

**1. Akses Prioritas Acara Galeri:**
- Hak untuk mengadakan pameran 1 minggu per tahun di İlhanArt Gallery (hak dapat dipindahtangankan)
- Diskon drop painting
- Diskon 10% hingga 30% untuk lukisan di galeri

**2. Akses Penuh PoArt Registry:**
- Catatan detail semua karya yang diautentikasi
- Versi lengkap Evidence Pack
- Alat verifikasi forensik


**3. Advisory Voting:**
- Hak konsultasi dalam pendaftaran PoArt Verified
- Akses ke saluran umpan balik komunitas
- Partisipasi dalam diskusi tata kelola

**4. Konten Eksklusif:**
- Konten behind-the-scenes studio
- Wawancara seniman dan video proses
- Akses dokumentasi teknis

**Catatan:**  
Pemegang token memberikan advisory vote (suara konsultasi). Keputusan akhir ada pada tim kuratorial. Struktur ini dipilih untuk mencegah manipulasi whale dan serangan spekulatif. Tidak ada staking reward karena kami mencari peserta budaya jangka panjang, bukan modal tentara bayaran jangka pendek.

---

### 6.4 Metadata Sync (Sinkronisasi dengan Dunia Fisik)

- **Metadata Sync:** Data teknis dalam registri harus 100% cocok dengan aset fisik.

**Mendefinisikan "100% cocok" secara teknis (kejelasan yang disarankan):**

- **Kecocokan minimum (wajib):**
  - `asset.fingerprints.sha256/sha512` dalam registri harus **persis sama** dengan hash file yang ada di tangan.
  - `proof.notary_seal` dalam registri ketika diregenerasi (jika Evidence Pack ada) harus **persis sama**.

- **Kecocokan referensi fisik (jenis bukti):**
  - Bukti seperti karya fisik yang ditampilkan dalam livestream + referensi tanggal/blok harus konsisten dengan Evidence Pack.

- **Kepatuhan privasi:**
  - Field seperti IP/lokasi dalam visibilitas `masked` dipublikasikan **sesuai standar masking**.

---

### 6.5 Sengketa, Peninjauan, dan Pencabutan (Dispute & Revocation)

Registri bukan hanya mekanisme "persetujuan"; ini adalah **mekanisme pengawasan hidup terhadap pemalsuan**.

- Ketika sengketa dimulai, catatan dapat dimasukkan ke mode **"review"**.
- Jika pemalsuan terdeteksi, ditandai sebagai `status: void` dan alasan ditambahkan:
  - `void_reason` (penggunaan AI / dicuri / manipulasi, dll.)
  - `revoked_at` (waktu pencabutan)
- Sumber keputusan pencabutan terlihat jelas dalam registri:
  - peninjauan kuratorial / sengketa komunitas / catatan analisis forensik (mana yang berlaku)

> **Bagian ini adalah padanan konsep VOID di bagian "Red Flag Protocol" pada registri.**

---

### 6.6 Contoh Catatan Registri (Dapat Dibaca Mesin)
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
    "review_notes": "Met all 5 PoArt standards. Community feedback positive."
  }
}
```

> *Catatan: `asset.fingerprints.sha512` dan nilai hash lainnya disingkat untuk tujuan presentasi; dalam implementasi nyata, string karakter hexadecimal panjang penuh digunakan.*

---

## 7) 🔐 SEGEL TEKNIS (NOTARY SEAL)

**Algoritma segel tak tergoyahkan yang dihasilkan oleh PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Protokol [PoArt] Notaris Digital & Bukti Forensik (Beta v1.0)

> **"Budaya lebih besar dari modal. Lindungi karya Anda dari hari ini, bawa ke hari esok."**

---

## Mengapa Terbuka untuk Publik?

Keamanan sejati berasal dari transparansi. Dengan sistem **Public Registry (Registri Publik)** kami, siapa pun di mana pun di dunia dapat memverifikasi dalam hitungan detik apakah file di tangan mereka asli atau tidak, tanpa memerlukan otoritas apa pun.

---

## 🧩 Mengapa Ada Banyak "Modul Visibilitas"?

Ini adalah bagian paling kritis dari kode (menu pilih visibility). Opsi-opsi ini memungkinkan pengguna menyeimbangkan **"Privasi vs. Transparansi"**:

### 🔒 Pribadi (Private)

- **Skenario:** Seniman belum ingin mempublikasikan karya tetapi ingin mencap tanggal untuk membuktikan "saya membuat ini pada tanggal ini".
- **Apa yang Dilakukan Kode:** Menulis data ke database tetapi memberi label `visibility: "private"`. Nanti ketika menulis kebijakan "Public Read", Anda dapat menyembunyikan catatan ini dari publik dengan menggunakan `WHERE visibility = 'public'`.

### 🕶️ Tersamar (Masked)

- **Skenario:** Seniman ingin transparansi tetapi khawatir tentang menemukan alamat rumah (lokasi IP).
- **Apa yang Dilakukan Kode:** Fungsi `maskIP` dan `maskLoc` berjalan di sisi JavaScript. Mengubah alamat IP menjadi format `88.241.***.***`, lokasi menjadi format `***/TR` dan mengirim versi yang disensor ke database.
- **Catatan Privasi:** Masking dilakukan di browser, Supabase tidak melihat lokasi asli. **Namun:** Jika API pihak ketiga seperti ipapi.co digunakan untuk data lokasi, penyedia ini melihat alamat IP pada saat permintaan.
- **Penyegelan di Mode Masked:** Perhitungan EvidenceRoot dan NotarySeal dilakukan dengan data forensik yang di-mask; dengan demikian verifikasi tetap deterministik.

### 🌍 Publik (Public)

- **Skenario:** Transparansi penuh. Sesuai standar [PoArt], di mana, kapan, dan dari jaringan mana karya diproduksi dinyatakan secara terbuka.

---

## 💡 Inovasi Teknologi

PoArt bukan hanya sistem unggah file. Ini adalah mesin **"Rantai Penjagaan Bukti Forensik" (Forensic Chain of Custody)** yang membawa standar baru dengan meleburkan tiga lapisan teknologi berbeda dalam satu pot.

**Lapisan yang dijelaskan sebagai "mesin" di bagian ini sesuai dengan inti PoArt Forensic Engine (PFE) dari terminologi sebelumnya.**

### 1) Client-Side Hashing (Privasi Maksimum)

File karya Anda tidak pernah diunggah ke server. Mesin berbasis browser (Client-side) kami menghitung hash (ringkasan digital) file di komputer Anda. Hanya sidik jari ini dan metadata yang dikirim ke server.

> **Catatan Privasi:** File karya tidak diunggah ke server dan dilindungi dengan cara ini. Namun, data forensik (IP/lokasi) dibagikan sesuai dengan mode visibilitas yang dipilih (private/masked/public).

### 2) Forensic Data Fusion (Kekuatan Forensik)

Ini lebih dari sekadar timestamp biasa. Sistem menggabungkan data berikut dalam satu "Genesis Seal":

- **Ringkasan Digital (SHA-512):** Sidik jari digital yang akan rusak jika bahkan satu piksel karya berubah, menggunakan standar ringkasan kriptografi (SHA-512).
- **Lokasi & Waktu:** Tanggal dengan presisi milidetik saat transaksi dilakukan, data negara, kota, dan distrik.
- **Identitas Perangkat:** Sistem operasi, browser, dan jenis perangkat (analisis User-Agent).

---

## 🛡️ Kasus Penggunaan dan Manfaat

Jika Anda seorang seniman, penulis, atau desainer, mengatakan "Saya sudah membuat ini sebelumnya" tidak cukup, Anda perlu membuktikannya.

**Karya yang disegel dengan PoArt:**

- **Bukti Matematis:** Sistem mendeteksi jika bahkan satu piksel file Anda berubah. Manipulasi tidak mungkin.
- **Dasar Hukum:** Tanggal, kota, dan perangkat dari mana karya disegel dicatat.
- **Sertifikat Instan:** Menghasilkan **"Sertifikat Identitas Aset"** dengan kode QR dan segel yang unik untuk Anda dalam hitungan detik.

---

## ⚙️ Arsitektur Sistem dan Spesifikasi Teknis

Sistem dirancang pada arsitektur "Serverless", berfokus pada kinerja tinggi dan skalabilitas.

| Lapisan | Teknologi | Deskripsi |
|---------|-----------|-----------|
| **Kriptografi** | SHA-256 & SHA-512 | Ringkasan kriptografi dua lapis |
| **Database** | Supabase (PostgreSQL) | Struktur data JSONB, kebijakan RLS |
| **Data Forensik** | ipapi.co API | Trio IP/Lokasi/Waktu |
| **Rendering** | html2canvas + jsPDF | Produksi PNG/PDF sisi klien |
| **Frontend** | Vanilla JavaScript | Tanpa ketergantungan framework |
| **Keamanan** | Client-side hashing | File tidak pernah diunggah ke server |

### Fitur Unggulan

| Fitur | Detail | Di Pesaing? |
|-------|--------|-------------|
| **Drag & Drop UI** | Seret-lepas file, pratinjau instan | ❌ Kebanyakan tidak ada |
| **Multi-Format Export** | PNG, JSON, PDF - satu klik | ⚠️ Terbatas |
| **Real-Time Preview** | Pratinjau sertifikat langsung | ❌ Tidak |
| **Privacy Controls** | Opsi Private/Masked/Public | ❌ Tidak |
| **Client-Side Hashing** | File tidak pernah pergi ke server | ✅ Hanya beberapa |
| **Forensic Metadata** | IP, lokasi, perangkat, waktu - semua dalam satu | ❌ Terpisah |
| **QR Verification** | Kode QR verifikasi instan | ⚠️ Terbatas |
| **Rate Limiting** | Perlindungan spam (RLS + Client) | ❌ Kebanyakan tidak ada |

---

## 🗺️ Peta Jalan: Masa Depan "Trustless"

Versi saat ini **(Beta v1.0)** dioptimalkan untuk memberikan kecepatan maksimum, antarmuka mudah, dan akses gratis kepada pengguna akhir. Namun, visi akhir kami adalah beralih ke struktur di mana bahkan administrator database (kami) tidak dapat campur tangan.

### Fase 1: Beta v1.0 (Saat Ini Aktif)

**Infrastruktur:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + IPFS backup)
- Gallery self-attestation (terpusat tetapi transparan)

**Token:**
- Platform: Pump.fun
- Liquidity: Raydium (otomatis)
- Governance: Advisory only (konsultasi komunitas)

**Tujuan:**
- Kecepatan, menghilangkan hambatan UX
- Memberikan keamanan "tanpa gesekan"
- Membangun komunitas

**Token Utility (v1.0):**
- Akses prioritas acara galeri
- Melihat PoArt Registry
- Hak advisory voting

---

### 🚀 Fase 2: Decentralized Authority (2026 Q2-Q4)

Fase ini mencakup transisi dari struktur yang sepenuhnya "Client-Side" ke struktur yang lebih aman dan terdesentralisasi.

| Fitur | Apa yang Diperoleh? | Tech Stack | ETA |
|-------|---------------------|------------|-----|
| **Edge Function INSERT** | Pemblokiran spam + keamanan API Key | Supabase Edge (Deno) | Q2 2026 |
| **Wallet Signature** | Identitas terdesentralisasi | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | Arsip terdesentralisasi | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | Pembatalan sertifikat palsu | DB Schema Update | Q2 2026 |
| **Audit Log** | Catatan kueri forensik | Tabel log kustom | Q3 2026 |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain voting (x/web) + wallet signature
- Pemilihan perwakilan komunitas (90 hari pertama)
- Kontrol wallet operasi multi-sig
- Weighted advisory voting (dengan whale cap)

**Immutability:**
- Backup registri dengan hash IPFS
- Bitcoin timestamp anchoring
- Persiapan verifikasi cross-chain

---

### Fase 3: Desentralisasi Penuh (2027+)

| Fitur | Target | ETA |
|-------|--------|-----|
| **On-Chain Registry** | Pencatatan on-chain Solana | Q1 2027 |
| **Enhanced Token Utility** | NFT mint, fitur lanjutan | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **DID Integration** | Identitas Terdesentralisasi | Q3 2027 |
| **Community Governance** | Sistem advisory yang diperkuat | Q4 2027 |
| **Legal Recognition** | Validitas di pengadilan Turki | 2027-2028 |
| **API for Developers** | Public API endpoint | Q3 2027 |

**Governance Evolution:**
- v3.0: Model hybrid (kuratorial + community weighted)
- 2028+: Full community governance (opsional)
- Kontrol kualitas kuratorial selalu dipertahankan

---

## 🧬 Struktur Data Protokol (JSON Schema)

**Setiap sertifikat [PoArt] memiliki kartu identitas JSON yang portabel dan dapat diverifikasi yang diproduksi sesuai standar berikut.**

> **Catatan:** Format Identity JSON ini adalah format sertifikat yang disajikan kepada pengguna. Dalam catatan registri, `registry.asset` digunakan sebagai pengganti `identity.asset_data` (pemetaan: `identity.asset_data` == `registry.asset`).
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

## 🔬 Kedalaman Teknis: Algoritma Penyegelan

### Fungsi Hash Deterministik
```javascript
// Fungsi Pembantu: Konversi Digest ke string hex
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Konversi String ke byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Produksi string forensics canonical (v1.0: urutan field tetap + UTF-8 + delimiter \n)
// Catatan Fase 2: Akan beralih ke canonical JSON dengan RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Proses Produksi NotarySeal (Sepenuhnya Deterministik)
```javascript
// 1. Menghitung FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Mengumpulkan data Forensic (menggunakan satu timestamp)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Produksi satu timestamp
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Timestamp yang sama
  };
  
  return { forensics, timestamp };
}

// 3. Membuat EvidenceRoot (dengan canonical encoding)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Produksi NotarySeal (menggunakan timestamp yang sama)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Fungsi pembantu masking (dukungan IPv4 dan IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Periksa IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 atau format tidak dikenal
  return "***";
}
```

### Alur Verifikasi (Dua Tingkat)

#### Quick Verify (Verifikasi Cepat)
```javascript
// Hanya memeriksa hash file (bendera merah cepat)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Ambil dari Registry
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Perbandingan Hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Asli - Hash file cocok"
    };
  } else {
    return {
      valid: false,
      message: "❌ Palsu - File telah dimanipulasi"
    };
  }
}
```

#### Full Verify (Verifikasi Penuh)
```javascript
// Regenerasi EvidenceRoot dan NotarySeal untuk verifikasi
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Ambil dari Registry
  const cert = await fetchFromRegistry(certificateId);

  // 1) Periksa FileHash (bendera merah cepat)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Palsu - Hash file tidak cocok" };
  }

  // 2) Regenerasi EvidenceRoot (dengan forensics yang disimpan di registry)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Tidak cocok - EvidenceRoot tidak benar" };
  }

  // 3) Regenerasi NotarySeal (dengan timestamp + signer_sig yang sama)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Tidak cocok - NotarySeal tidak benar" };
  }

  // Opsional: Di Fase 2, verifikasi juga signer_sig dengan attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Tanda tangan tidak valid" };

  return { valid: true, message: "✅ Asli - Full Verify berhasil" };
}
```

> **Catatan Penting:**
> - **Quick Verify:** Hanya memeriksa hash file untuk penggunaan cepat.
> - **Full Verify:** Memverifikasi semua lapisan protokol (EvidenceRoot + NotarySeal).
> - Semua operasi hash dilakukan secara deterministik dengan encoding dan delimiter tetap.
> - **Standar kanonisasi v1.0:** Urutan field tetap + encoding UTF-8 + delimiter `\n`.
> - **Rencana Fase 2:** Transisi ke canonical JSON dengan RFC 8785 (JCS - JSON Canonicalization Scheme).
> - Di mode Masked, perhitungan EvidenceRoot dan NotarySeal dilakukan dengan forensics yang di-mask.
> - Satu timestamp digunakan di seluruh proses (forensics + NotarySeal); determinisme dijamin.
> - **Nama field Forensics:** `ip_masked`, `location`, `device`, `timestamp` (kode dan registry sepenuhnya kompatibel).
> - **Path Registry:** `certificate.asset.fingerprints` (sepenuhnya kompatibel dengan kode verify).
> - **signer_sig di Registry:** Field `proof.signer_sig` diperlukan untuk Full Verify.
> - Mekanisme SignerSignature akan diaktifkan di Fase 2 dengan Solana Wallet Adapter; di v1.0, verifikasi dapat dilakukan dengan `attestation_pubkey`.

---

## 📊 Analisis Pesaing (Diperbarui)

PoArt diposisikan pada "Sweet Spot" yang melengkapi kekurangan solusi yang ada.

| Fitur | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|-------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Biaya** | 🆓 Gratis | 🆓 | 💰 Berbayar | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Sangat Mudah | ❌ CLI | ⚠️ Sedang | ⚠️ Sedang | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Langsung | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Mode | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privasi | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Lengkap | ❌ | ❌ | ⚠️ Terbatas | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Instan | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Dukungan Turki** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Keterangan:**
- ✅ : Dukungan penuh / tersedia
- ⚠️ : Terbatas / dalam paket berbayar
- ❌ : Tidak / tidak didukung
- 🔄 : Dalam roadmap (sedang dikembangkan)
- 🆓 : Sepenuhnya gratis
- 💰 : Berbayar / langganan diperlukan

### Kekurangan Pesaing, Kekuatan PoArt

| Kekurangan | Pesaing | PoArt |
|------------|---------|-------|
| **Kesulitan Penggunaan** | CLI, perlu pengetahuan API, perlu wallet | Seret-lepas, selesai dalam 3 klik |
| **Hambatan Biaya** | Langganan $50-500/bulan | 100% gratis |
| **Privasi** | File diunggah ke server | Client-side, file tidak pernah pergi |
| **Data Forensik** | Hanya timestamp | IP, lokasi, perangkat, waktu - semua |
| **Dukungan Turki** | Tidak ada atau sangat terbatas | Dukungan bahasa native |
| **Open Source** | Kotak hitam | Semua kode terbuka di GitHub |

---

## 📈 Statistik Penggunaan (Target Q1 2026)

| Metrik | Target | Status |
|--------|--------|--------|
| **Total Sertifikat** | 1,000 | 🔄 Berlangsung |
| **Pengguna Aktif** | 500 | 🔄 Berlangsung |
| **Jumlah Verifikasi** | 5,000 | 🔄 Berlangsung |
| **Uptime** | %99.9 | ✅ Aktif |
| **Avg Response Time** | <200ms | ✅ Optimal |

---

## 🌍 Komunitas & Dukungan

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Kontributor

Protokol PoArt terus berkembang dengan kontribusi komunitas open source.

**Untuk berkontribusi:**
1. Fork repo
2. Buat feature branch (`git checkout -b feature/amazing-feature`)
3. Commit (`git commit -m 'Add amazing feature'`)
4. Push (`git push origin feature/amazing-feature`)
5. Buka Pull Request

### 🛠️ Apa yang Kami Butuhkan Sekarang? (Panggilan Bantuan)

Protokol PoArt menunggu kontribusi dari pengembang berpengalaman di bidang berikut untuk pengembangan **Fase 2**:

* **Supabase Edge Functions:** Memindahkan perlindungan spam ke sisi server.
* **Solana Web3.js:** Integrasi Wallet Signing.
* **IPFS / Arweave:** Integrasi layanan penyimpanan dan pinning.
* **Community Tools:** Voting X, sistem voting, analytics dashboard.

> Silakan mulai diskusi di tab "Issues" sebelum menambahkan fitur.

---

## 💬 Catatan Akhir

### Pump.fun dan Realitas

Proyek ini dimulai di Pump.fun karena:
- ✅ Akses likuiditas (Raydium automatic migration)
- ✅ Akses komunitas yang ada
- ✅ Biaya awal rendah

Namun, mari kita perjelas:
- **Harga token** bukan indikator keberhasilan artistik
- **Anggaran operasional** membutuhkan nilai token (galeri, pameran, infrastruktur)
- **Metrik keberhasilan:** Authenticated artworks + community engagement + pengunjung fisik

### Governance dan Desentralisasi

**Realitas v1.0 (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (terpusat tetapi transparan)
- Governance: Advisory only (keputusan akhir kuratorial)
- Token utility: Gallery access + registry + NFT priority

**Visi v2.0+ (2027+):**
- Registry: On-chain (Solana)
- Signatures: Wallet-based (terdesentralisasi)
- Governance: Hybrid (community advisory + curatorial quality)
- Token utility: Enhanced features + advanced access

Struktur ini memberikan **efisiensi operasional** dan **kontrol kualitas** di tahap awal, sambil menjaga jalur terbuka untuk meningkatkan **partisipasi komunitas** di masa depan.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Budaya Lebih Besar dari Modal*

## 🧾 Lisensi

MIT License © 2026 İlhan Art Gallery Initiative

Lihat [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) untuk ketentuan lengkap.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Proyek ini dikembangkan dengan inisiatif [İlhan Art Gallery], kode sumber dibuka untuk publik demi transparansi.**

**PROTOCOL V1.0 // DISEGEL DENGAN SHA-512.**

*© 2026 İLHAN ART | SEMUA HAK ATAS KARYA, GAMBAR, DAN IDE DILINDUNGI.*

---
