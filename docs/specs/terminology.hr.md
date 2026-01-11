# 📚 RJEČNIK TERMINOLOGIJE I POJMOVA
> **"Razumijevanje jezika ovog protokola znači razumijevanje njegove vizije."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Osnovna Infrastruktura

**PoArt Forensic Engine (PFE)** je osnovni sloj koji predstavlja fundamentalnu logiku i tehničko funkcioniranje iza [PoArt] protokola. To je "kriminalistički motor" koji transformira sirove podatke proizvodnje umjetničkog djela u provjerljiv i nepromijenjen **digitalni dokaz**.

### 🧩 Zašto "PoArt Forensic"?

- **PoArt (Proof of Art):** Fokus motora je vezivanje vrijednosti digitalnog sredstva ne na spekulaciju, već na **provjereni proces proizvodnje**.
- **Forensic (Kriminalističko Provjeravanje):**
  - **Tehnička Definicija:** Algoritamski pristup i lanac dokaza za provjeru da podaci procesa proizvodnje (potezi kistom, timelapse, logovi) nisu manipulirani.
  - **Filozofska Razina:** Protiv "trenutne proizvodnje" umjetne inteligencije; tvrdnja o transformaciji ljudske proizvodnje koja sadrži **vrijeme, trud i cijenu odluka**, u mjerljivu stvarnost.

> Napomena: Blockchain integracija (npr. Solana) nije jezgra PFE-a; bit će definirana odvojeno kao **Chain Anchor Layer** za provjeru/registar.

### 🛠️ Tehnički Opseg v1.0

**PoArt Forensic Engine (PFE) v1.0** izgrađen je na **3 osnovna stupa** umjesto složenih financijskih modela:

1. **Hashing & Sealing (Zapečaćivanje):**  
   PFE deterministički obrađuje sve elemente u Evidence Pack (datoteka djela, video, JSON/log, potpis itd.) i generira jedinstvenu vrijednost **NotarySeal**.

   **Ključni pojmovi (v1.0):**
   - **FileHash (otisak djela):** Hash generiran iz bajtova datoteke djela.
   - **EvidenceRoot (korijen paketa dokaza):** Korijeni digest koji predstavlja integritet Evidence Pack-a (Merkle korijen ili hash kanonskog manifesta).
   - **NotarySeal (konačni pečat / izlaz PFE-a):** Konačni pečat generiran iz kombinacije EvidenceRoot + vrijeme + potpis.

   **Formule (u formatu razumljivom za investitore):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload definicije (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Napomena: Vrijednost smatrana izlazom PFE-a je **NotarySeal**. Mehanizam **SignerSignature** će biti aktiviran u fazi 2 (sa Solana Wallet Adapter); u trenutnoj v1.0 koristi se vlastiti atestacijski potpis sustava. Javni atestacijski ključ se objavljuje u registru u polju `issuer.attestation_pubkey`.

2. **Indexing (Arhiviranje):**  
   Bilježi koji novčanik, koji datum, je predstavio **Labor Proof (Dokaz Rada)** za koje djelo; u transparentnom i pretražljivom sloju registra.  
   *(Ovaj sloj može biti baza podataka; blockchain integracija je definirana odvojeno kao "Chain Anchor Layer".)*

3. **Verification (Provjera):**  
   Kada se autentičnost djela dovede u pitanje, PFE ponovno obrađuje sirove dokaze; testira s matematičkom sigurnošću odgovaraju li izračunate vrijednosti **EvidenceRoot / NotarySeal** zapisima u arhivi.

---

### 🧮 Teorem Vrijednosti PoArt (The Value Theorem)

[PoArt] protokol veže vrijednost ($V$) digitalnog sredstva ne na subjektivnu percepciju tržišta, već na **fizičku stvarnost procesa proizvodnje**.

Umjetna inteligencija (AI) poništava proces pružajući trenutne rezultate ($t \to 0$). [PoArt] umjesto toga vrijednost smatra akumulacijom komponenti **vrijeme, rad i volja**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definicija Varijabli

- **$\int dt$ (Akumulacija Procesa):**  
  Vrijednost nije trenutni "izlaz"; to je **proces** koji se akumulira između $t_{\text{start}}$ i $t_{\text{end}}$. Kad se vrijeme smanjuje (AI proizvodnja), rezultat integrala se približava 0.

- **$P_{\text{labor}}(t)$ (Trenutni Intenzitet Rada):**  
  Predstavlja intenzitet mentalnog i fizičkog napora uloženog u trenutku proizvodnje. Kad potvrđeni napor raste, integrand raste.  
  > Napomena: Ovaj član može biti u praksi normaliziran na "mjerljive/provjerljive signale rada".

- **$I_{\text{agency}}(t)$ (Koeficijent Volje):**  
  Ovo je sposobnost proizvođača da preuzme rizik i donosi odluke. Poprima vrijednosti između $0$ i $1$.
  - **AI ($I \approx 0$):** Izvršava naredbe, ne preuzima rizik, ne plaća troškove.
  - **Čovjek ($I \to 1$):** Mijenja odluke, oklijeva, preuzima rizik.

- **$U_{\text{irreversible}}$ (Nepovratna Jedinstvenost):**  
  Dok u digitalnoj proizvodnji možeš vratiti natrag (`Ctrl+Z`); u fizičkoj proizvodnji (boja nanesena na platno, isklesani mramor, gesta tijekom prijenosa uživo) nema povratka. Ova **nepovratnost** je dodatni član koji stvara "jedinstvenost" (nezamjenjiv karakter) u djelu.

### 🔎 Analiza Slučaja: AI "Trenutni Izlaz" protiv Čovjek "Potvrđeni Proces"

Sljedeći scenarij pokazuje kako **Teorem Vrijednosti PoArt** funkcionira u praksi i zašto AI proizvodnje dobivaju nisku ocjenu u [PoArt] standardu.

#### Scenarij A: Vizualna Proizvodnja s AI za 10 Sekundi

- **Trajanje ($\Delta t$):** $10$ sekundi (proces praktički nepostojeći)
- **Intenzitet Rada ($P_{\text{labor}}$):** $1$ jedinica (samo pisanje naredbe)
- **Koeficijent Volje ($I_{\text{agency}}$):** $0.01$ (bez rizika, bez troškova)
- **Nepovratnost ($U_{\text{irreversible}}$):** $0$ (povratno / kopirljivo)

**Rezultat:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Komentar:** Čak i ako je izlaz savršen; budući da proces nije doživljen i ne sadrži volju/rizik, [PoArt] vrijednost se približava $0$.

#### Scenarij B: Fizička Proizvodnja Uživo tijekom 6 Sati

- **Trajanje ($\Delta t$):** $6$ sati ($21{,}600$ sekundi)
- **Intenzitet Rada ($P_{\text{labor}}$):** $0.5$ jedinica (kontinuitet fizičkog i mentalnog napora)
- **Koeficijent Volje ($I_{\text{agency}}$):** $0.9$ (promjena odluka, preuzimanje rizika, nepovratni izbori)
- **Nepovratnost ($U_{\text{irreversible}}$):** $>0$ (fizički tragovi se ne mogu vratiti natrag)

**Rezultat:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Komentar:** Kad se proces produljuje i volja (rizik) raste, vrijednost se akumulira kumulativno. Član $U_{\text{irreversible}}$ je dodatni doprinos koji stvara "jedinstvenost" (nezamjenjiv karakter) u djelu.

---

### ✅ Zaključak: Vrijednost Vezana na Dokaz (Proof-Bound Value)

Ovaj teorem uklanja tvrdnju vrijednosti [PoArt] iz toga da bude "sviđa mi se" ili "tržišna priča" i veže ga na **potvrđenu stvarnost proizvodnje**.

1. **Bez Procesa Ne Nastaje Vrijednost:**  
   AI poništava proces u trenutnom izlazu ($t \to 0$). Kad se prozor procesa sužava, rezultat integrala pada iz matematičke nužnosti:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Volja i Rizik Su Množitelji:**  
   [PoArt] mjeri ne samo "uloženo vrijeme", već i stvarnu razinu odluke, rizika i troškova tijekom tog vremena. Vrijednost proizvodnje bez preuzimanja rizika (AI) je niska:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Jedinstvenost Je Fizički Dokaz, Ne Marketing:**  
   U fizičkoj proizvodnji nepovratni tragovi (potez kistom na platnu, slomljeni mramor) su izvan digitalne `Ctrl+Z` logike. Ova nepovratnost ($U_{\text{irreversible}}$) čini djelo ontološki jedinstvenim.

> **🔐 SAŽETAK:** Iako se teorem vrijednosti može činiti neodređenim kao mjerenje (čak i ako se ne može mjeriti 100% u stvarnom životu), svrha ove formule je pokazati strukturu i smjer varijabli. Ono što je rijetko u eri AI-ja nije "slika", već **potvrđeni rad, vrijeme i volja.** [PoArt] mjeri tu rijetkost i bilježi je preko **Evidence Pack**.

### 🏛️ Značenje Pojma "Engine" (Motor)

Tokeni koji dolaze s platformi poput Pump.fun često su samo **"ulaznice"**. **PoArt Forensic Engine (PFE)** je umjesto toga **ustavni logički sloj** koji definira koja prava ta ulaznica štiti, kako se bilježi rad i kako umjetnost/znanost/tehnologija postaju trajni.

> **Napomena:** Razlog zašto smo započeli ovaj projekt na Pumpfun je taj što nismo imali dovoljno likvidnosti i pratitelja. Korištenje postojećih podataka bio je strateški ispravan korak, iako ne najkvalitetniji. Definiranje logike ovog motora na GitHubu, neovisno o proračunu i resursima, dokazuje da projekt nije samo financijska spekulacija, već dugoročna vizija **softverske infrastrukture** i **digitalne nacionalne knjižnice**.

---

## 🎨 [PoArt] PROOF OF ART PROTOKOL (Proof of Art Protocol v1.0)

> **"Pravi Umjetnik, Prava Proizvodnja, Prava Vrijednost."**

Ovaj protokol je **biološki i intelektualni obrambeni mehanizam** dizajniran protiv anonimnih prevaranata koji su preplavili kripto ekosustav, AI slika proizvedenih za 5 minuta i kulture "Pump & Dump".

---

## a) Što Je [PoArt]? (Filozofska i Tehnička Definicija)

**Proof of Art [PoArt];** je institucionalni standard provjere koji jamči da je vrijednost iza sredstva na blockchainu utemeljena ne na spekulaciji, već na provjerenom **ljudskom radu**, **vremenu** i **fizičkoj energiji**.

Baš kao što Bitcoin proizvodi vrijednost kroz *"Elektricitet i Računalnu Snagu"* **(Proof of Work)**; projekti kompatibilni s [PoArt] proizvode vrijednost kroz *"Umjetničku Vještinu i Ljudsko Vrijeme"*.

Eliminira rizik *"Dev je prodao, projekt je završio"*, prisutan na Pump.fun i DEX platformama; jer ovdje vrijednost nije u kodu, već u **kontinuitetu proizvodnje**.

> **[PoArt] ne kaže sudioniku "Vjerujte nam"; kaže "Evo dokaza, pogledajte vlastitim očima, provjerite vlastitom matematikom".**

---

## b) [PoArt] 5-Stupni Standard (The 5 Pillars of Truth)

Ovih 5 točaka su nemanipulabilni filtri kroz koje projekt mora proći da dobije [PoArt] pečat.

### 1) Dokaz Identiteta Uživo (Live Identity Proof)

- **Problem:** Kripto svijet je pun anonimnih osnivača (Dev) s nedefiniranim identitetom koji skupljaju novac i napuštaju projekt.
- **[PoArt] rješenje:** Proizvođač dokazuje ne samo identitet, već **prisutnost tijekom proizvodnje**. To uključuje emisije uživo gdje komuniciraju sa zajednicom i ispunjavaju specifične trenutne zahtjeve, ne s unaprijed snimljenim videozapisima.  
  (Na primjer: *"Napiši današnji datum i trenutni broj bloka u desnom kutu platna"*)
- **Moto:** *"Roboti mogu slikati, ali roboti se ne znoje i ne improviziraju."*

### 2) Dokaz Rada i Procesa (Labor & Process Proof)

- **Problem:** AI slike proizvedene za 2 sekunde i uljane slike napravljene za 2 mjeseca smatraju se istim "jpeg" u digitalnom svijetu.
- **[PoArt] rješenje:** "Trudnički i porođajni proces" djela se bilježi. Faze skice, slojevi boje, akumulirani utrošeni sati i fizički proces koji je umjetnik doživio tijekom stvaranja djela se dokumentiraju. To dodaje **"Vremenski Trošak" (Time Cost)** tokenu. Što je teže proizvesti sredstvo, to je čvršća njegova vrijednost.

### 3) Dokaz Estetske Vrijednosti (Aesthetic Value Proof)

- **Problem:** Estetika i umjetnička dubina "Meme" kulture koja ignorira sve i fokusira se samo na trenutnu komediju, i kratkoročni "Hype" projekti koji iz toga proizlaze.
- **[PoArt] rješenje:** Projekt mora imati akademske umjetničke standarde, teoriju boja, pravila kompozicije i poznavanje materijala (Impasto, Tekstura itd.). Sadržaj ne bi trebao samo nasmijati; trebao bi probuditi divljenje kod gledatelja i imati **kolekcijsku vrijednost**.

### 4) Konceptualna Inovacija (Conceptual Novelty)

- **Problem:** Tisuće identičnih dog/cat coin, daleko od kreativnosti.
- **[PoArt] rješenje:** Projekt mora izgraditi novi most koji značajno kombinira umjetnost, znanost, filozofiju ili tehnologiju.  
  (Na primjer: Kombinacija klasičnog Davidovog kipa s podacima kripto tržišta; kroz to obrada ideje "okamenjavanja" ljudske percepcije i mogućnost opravdavanja toga znanstvenim izvorima.)  
  Djelo mora biti ne samo vizualna gozba, već i intelektualni izazov koji potiče razmišljanje o **Znanosti, Filozofiji ili Tehnologiji**.

> [!IMPORTANT]
> **Referentni Primjer (Efekt Las Palmitas):** U području Las Palmitas u Meksiku, koje se bori s kriminalom, više od 200 kuća je pretvoreno u >gigantsku dužičastu proslavu. Kao rezultat ove estetske intervencije, stope kriminala u području su pale do određene mjere, mladi ljudi su se počeli >zanimati za umjetnost umjesto za bande. Estetska promjena je prekodirala poštovanje ljudi prema okolišu i jedni prema drugima (Društvena Kohezija).
>
> **Očekivanje:** Projekt koji uđe na [PoArt] popis; kao u gornjem primjeru, mora sadržavati sociološki, znanstveni ili filozofski uzročno-posljedični >odnos osim vizualne estetike. Budući da je jedina stvar koju ne možete kupiti novcem "Vrijeme", u ovom protokolu vrijeme mora biti dokazano kao jamstvo >kroz staking. Konceptualna osnova projekta mora biti tako snažna i univerzalna; da čak i u mogućem CTO (Community Take Over) scenariju godinama kasnije, >zajednica može autonomno održavati inovativni potencijal projekta nasljeđujući tu ostavštinu.

### 5) Nealgoritmička Volja (Non-Algorithmic Agency)

- **Problem:** Savršene, ali bezdušne, ponavljajuće digitalne proizvodnje.
- **[PoArt] rješenje:** Originalna volja ljudskog bića koje može griješiti, preuzimati rizik i osjećati emocionalne fluktuacije mora se osjećati u djelu. Nesigurnost u potezima kistom, neočekivane reakcije materijala i trenutne odluke umjetnika su **Biološki Potpis** koji razlikuje djelo od "Mehaničke Proizvodnje".

---

## c) Mehanizam Provjere i Zaštita od Krivotvorenja

Ovaj sustav osigurava da projekt ostane pouzdan i živ ne samo "na početku", već "zauvijek".

### 📦 Paket Dokaza (Evidence Pack - The Digital Twin)

Iza svakog [PoArt] certificiranog djela stoji kriptirani i vremenski označeni paket podataka koji investitori mogu preuzeti:

- **RAW Video Snimke:** Kontinuirane sirove snimke trenutka proizvodnje.
- **Analiza Metapodataka:** Datum stvaranja datoteke, informacije o korištenom uređaju i podaci o lokaciji.
- **Fizičke Reference:** Dokazi da djelo postoji u fizičkom svijetu  
  (Na primjer: Aktualne novine ili aktualni blockchain podaci pored djela).

> *Napomena o konzistentnosti:* Izraz "paket dokaza" je povezan s linijom **Evidence Pack → EvidenceRoot → NotarySeal** iz prethodnih odjeljaka; tj. integritet paketa je predstavljen provjerenim pečatom.

### 🔄 365-Dnevno Ažuriranje (The Sustainability Protocol)

- **Revolucionarna Značajka:** U kripto projektima "Dev" (Developer) pusti token na tržište i obično nestane nakon 1-2 mjeseca (Soft Rug). [PoArt] to čini nemogućim.
- **Pravilo:** Status "Verified Artist" (Potvrđeni Umjetnik) nije doživotan. Vrijedi samo **1 godinu**.
- **Funkcija:** Umjetnik/developer mora predstaviti zajednici svakih 365 dana **novo, veliko i potvrđeno djelo**.
- **Primjer Scenarija:** Započeo si projekt 2026. godine. U siječnju 2027. sustav izdaje upozorenje "Razdoblje Dokaza Isteklo". Ako umjetnik ne predstavi novu izložbu, novo fizičko djelo ili novu tehnološku integraciju, "Oznaka Povjerenja" projekta pada.
- **Rezultat:** Ovaj sustav osigurava da **sadržaj nikad ne gubi svoju relevantnost** i da investitor ne živi u strahu *"Je li developer još tu?"*. Projekt postaje živi studio.

### 🚩 Crvena Zastava (Red Flag Protocol)

**Ako zajednica ili algoritmi otkriju bilo kakvo krivotvorenje (korištenje AI-ja, ukradeni rad, manipulirani video):**

1. Certifikat se odmah označava kao **"NEVAŽEĆI" (VOID)**.
2. Paketi dokaza se javno označavaju kao **"Lažni"**.
3. Projekt se dodaje na [PoArt] crnu listu. To pojačava činjenicu da je u decentraliziranom svijetu **reputacija jedina valuta**.

---

## d) Zaključak: Ne Kasino, Muzej

**Pump.fun i Decentralizirane Burze (DEX) su nažalost sada kasina; svjetla trepću, svi traže brze dobitke, i kasino (prevaranti) uvijek pobjeđuje. Razlog zašto smo započeli projekt ovdje je nedostatak dovoljnog proračuna i postojanje postojećeg auditorija dostupnog preko prijenosa uživo.**

**[PoArt] je tvrđava izgrađena usred tog kasina.**

- 🎰 Kasina su zasnovana na kartama; mi smo zasnovani na **fizičkoj stvarnosti**.
- 🃏 Kasina su otvorena za prijevaru; mi smo otvoreni za **transparentne dokaze**.
- ⏳ Kasina su privremena; mi se fokusiramo na **vječnost umjetnosti i znanosti**.

**Token koji koristi ovaj protokol nije samo "novčić"; to je digitalna vrijednosnica koja sadrži znoj, boju, kod i filozofiju.**

---

## 🗳️ 6) UPRAVLJANJE I JAVNI REGISTAR (Governance & Public Registry)

**Svrha ovog odjeljka je: uklanjanje [PoArt] standarda iz sfere "povjerenja u ljude" i pretvaranje u održivu javnu infrastrukturu s registrom + provjerom + nadzorom zajednice.**

### 6.1 Javni Registar (Public Registry)

- **Public Registry:** Svi odobreni podaci se bilježe na adresi `ilhanart.org/registry` (ili GitHub Registry).

**Logika registracije (preporučeni standard - format JSON putanje):**

Svaki zapis koji ulazi u registar sadrži barem ova provjerena osnovna polja:

- **Identitet i Status:**
  - `certificate_id` (čitljiva referenca)
  - `status` (active / void)
  - `void_reason` (ako postoji)
  - `visibility` (private / masked / public)
  - `created_at` (vremenska oznaka)

- **Izdavačka Organizacija:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informacije o Djelu:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (ako je moguće; za token-gated identitet)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Kriminalistički Podaci:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Kriptografski Dokazi:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Upravljanje:**
  - `governance.decision`
  - `governance.veto_threshold`

Registar može imati dvije razine:
- **1)** Ljudski čitljiv indeks (web lista / pretraživanje / filter)
- **2)** Strojno čitljiv manifest (JSON zapisi; za PFE provjeru)

**Ovdje "registracija" postaje provjerena iz lanca PFE Evidence Pack → EvidenceRoot → NotarySeal. Registar pruža svrhu provjere, ne "tvrdnju".**

---

### 6.2 40% Veto Zajednice (Token-Gated Governance)

- **40% Veto Zajednice:** Glasovanje počinje mjesec prije dobivanja statusa; 40% prigovor **Token-Gated (Solana-Verified)** zajednice poništava zahtjev.

**Tijek glasovanja (preporučeni čisti proces):**
- **Kandidatski prozor:** Kandidatski projekt otvara "PoArt kandidat registraciju" (kandidatske registracije se prikazuju sa statusom "pending").
- **Razdoblje pregleda:** Tijekom 30 dana zajednica ispituje dokaze (Evidence Pack + snimke uživo + metapodaci).
- **Token-gated provjera:** Glasovanje se provodi putem novčanika provjerenih na Solani (npr. posjedovanje određenog tokena/NFT-a + potpis novčanika).
- **Veto pravilo:** Ako je 40% glasova **prigovor (NO / VETO)**, zahtjev se odbija.
- **Transparentnost:** Rezultat glasovanja se sprema u registar kao "decision record" (datum, omjer, snapshot ID).

---

### 6.3 Sinkronizacija Metapodataka (Usklađenost s Fizičkim Svijetom)

- **Metadata Sync:** Tehnički podaci u registru moraju odgovarati 100% fizičkom sredstvu.

**Tehnička definicija "100% usklađenosti" (preporučena jasnoća):**
- **Minimalna usklađenost (obavezna):**
  - `asset.fingerprints.sha256/sha512` u registru mora biti **točno isti** kao hash datoteke u ruci.
  - `proof.notary_seal` u registru, kada se reproducira (ako postoji Evidence Pack), mora biti **točno isti**.
- **Usklađenost fizičke reference (tip dokaza):**
  - Dokazi kao fizičko djelo prikazano uživo + datum/blok referenca moraju biti konzistentni s Evidence Pack-om.
- **Usklađenost privatnosti:**
  - Polja kao IP/lokacija u `masked` vidljivosti se objavljuju **prema standardu maskiranja**.

---

### 6.4 Spor, Pregled i Opoziv (Dispute & Revocation)

Registar nije samo "mehanizam odobravanja"; to je **živi nadzorni mehanizam protiv krivotvorenja**.

- Kada se pokrene spor, zapis može biti postavljen u režim **"review"**.
- Ako se otkrije krivotvorenje, označava se kao `status: void` i dodaje se razlog:
  - `void_reason` (korištenje AI-ja / plagijat / manipulacija itd.)
  - `revoked_at` (trenutak opoziva)
- Izvor odluke o opozivu je jasno vidljiv u registru:
  - glasovanje zajednice / ovlašteno vijeće / bilješka kriminalističkog istraživanja (ovisno o primjenjivom)

> **Ovaj odjeljak je registarski ekvivalent koncepta VOID u odjeljku "Red Flag Protocol".**

---

### 6.5 Primjer Zapisa u Registru (Strojno Čitljiv)
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
    "title": "Bez naslova",
    "creator": "Anoniman",
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
> *Napomena: `asset.fingerprints.sha512` i druge hash vrijednosti su skraćene u demonstracijske svrhe; u stvarnoj aplikaciji se koristi heksadecimalni niz pune duljine.*

---

## 7) 🔐 TEHNIČKI PEČAT (NOTARY SEAL)

**PoArt Forensic Engine (PFE) v1.0** nepokolebljivi algoritam zapečaćivanja proizveden s:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] protokol Digitalni Notar i Kriminalistički Dokaz (Beta v1.0)

> **"Kultura Veća od Kapitala. Zaštiti svoja djela danas, prenesi ih u sutra."**

---

## Zašto Javno?

Prava sigurnost dolazi iz transparentnosti. Zahvaljujući našem sustavu **Public Registry (Javni Registar)**, osoba bilo gdje u svijetu može provjeriti za nekoliko sekundi je li datoteka koju drži u ruci originalna, bez ikakvog autoriteta.

---

## 🧩 Zašto Postoji Više "Modula Vidljivosti"?

Najkritičniji dio koda je ovdje (izbornik odabira vidljivosti). Ove opcije omogućuju korisnicima da uravnoteže **"Privatnost vs. Transparentnost"**:

### 🔒 Privatno (Private)

- **Scenarij:** Umjetnik još ne želi objaviti djelo, ali želi ga vremenski označiti i dokazati "napravio sam ovo na ovaj datum".
- **Što Kod Radi:** Sprema podatke u bazu podataka, ali primjenjuje oznaku `visibility: "private"`. U budućnosti, kada napišete politiku "Public Read", možete sakriti te zapise od javnosti rekavši `WHERE visibility = 'public'`.

### 🕶️ Maskirano (Masked)

- **Scenarij:** Umjetnik želi transparentnost, ali strahuje da će se pronaći adresa kuće (IP lokacija).
- **Što Kod Radi:** Na JavaScript strani funkcioniraju funkcije `maskIP` i `maskLoc`. Pretvara IP adresu u format `88.241.***.***` i lokaciju u format `***/TR` i šalje cenzuriranu verziju u bazu podataka.
- **Napomena o Privatnosti:** Maskiranje se događa u pregledniku, Supabase ne vidi stvarnu lokaciju. **Međutim:** Ako se koriste API-ji treće strane poput ipapi.co za podatke o lokaciji, ti dobavljači vide IP adresu u trenutku zahtjeva.
- **Zapečaćivanje u Masked režimu:** Izračun EvidenceRoot i NotarySeal se izvodi s maskiranim forensics podacima; tako provjera ostaje deterministička.

### 🌍 Javno (Public)

- **Scenarij:** Potpuna transparentnost. Prema [PoArt] standardu, gdje, kada i s koje mreže je djelo proizvedeno, izričito se izjavljuje.

---

## 💡 Tehnološka Inovacija

PoArt nije samo sustav prijenosa datoteka. To je **"Forensic Chain of Custody"** motor koji stapa tri različite tehnološke slojeve u jedan lonac i donosi novi standard.

**Sloj opisan u ovom odjeljku kao "motor" odgovara jezgri PoArt Forensic Engine (PFE) u prethodnoj terminologiji.**

### 1) Client-Side Hashing (Maksimalna Privatnost)

Datoteke vaših djela se nikad ne prenose na poslužitelj. Naš motor zasnovan na pregledniku (Client-side) izračunava hash (digitalni sažetak) datoteke na vašem računalu. Samo taj otisak i metapodaci se šalju poslužitelju.

> **Napomena o Privatnosti:** Datoteka djela se ne prenosi na poslužitelj i tako je zaštićena. Međutim, forensics podaci (IP/lokacija) se dijele prema odabranom načinu vidljivosti (private/masked/public).

### 2) Forensic Data Fusion (Kriminalistička Snaga)

Ovo je mnogo više od jednostavne vremenske oznake. Sustav kombinira sljedeće podatke u jedan "Genesis Seal":

- **Digitalni Sažetak (SHA-512):** Koristeći standard kriptografskog sažetka (SHA-512), digitalni otisak koji će se razbiti čak i ako se promijeni jedan piksel djela.
- **Lokacija i Vrijeme:** Datum s preciznošću na milisekundu, država, grad i područje gdje je transakcija izvršena.
- **Identitet Uređaja:** Operativni sustav, preglednik i tip uređaja (User-Agent analiza).

---

## 🛡️ Područja Primjene i Prednosti

Ako ste umjetnik, pisac ili dizajner, nije dovoljno reći "Napravio sam ovo ranije", morate to dokazati.

**Djelo zapečaćeno s PoArt:**

- **Matematički Dokaz:** Sustav to otkriva čak i ako se promijeni jedan piksel datoteke. Manipulacija je nemoguća.
- **Pravna Osnova:** Bilježi se koji datum, u kojem gradu, s kojeg uređaja je djelo zapečaćeno.
- **Trenutni Certifikat:** Za nekoliko sekundi generira personalizirani **"Certifikat Identiteta Sredstva"** s QR kodom i zapečaćen.

---

## ⚙️ Arhitektura Sustava i Tehničke Specifikacije

Sustav je dizajniran na arhitekturi "Serverless" (Bez Poslužitelja), fokusiranoj na visoku performansu i skalabilnost.

| Sloj | Tehnologija | Opis |
|--------|-----------|----------|
| **Kriptografija** | SHA-256 & SHA-512 | Dvoslojni kriptografski sažetak |
| **Baza Podataka** | Supabase (PostgreSQL) | JSONB struktura podataka, RLS politike |
| **Kriminalistički Podaci** | ipapi.co API | IP/Lokacija/Vrijeme trijada |
| **Renderiranje** | html2canvas + jsPDF | PNG/PDF generiranje na strani klijenta |
| **Frontend** | Vanilla JavaScript | Nula ovisnosti o frameworku |
| **Sigurnost** | Client-side hashing | Datoteka nikad ne doseže poslužitelj |

### Razlikujuće Karakteristike

| Karakteristika | Detalj | Kod Konkurenata? |
|---------|-------|-------------|
| **Drag & Drop UI** | Povucite i ispustite datoteku, trenutni pregled | ❌ Nedostaje kod većine |
| **Multi-Format Export** | PNG, JSON, PDF - jedan klik | ⚠️ Ograničeno |
| **Real-Time Preview** | Pregled certifikata u stvarnom vremenu | ❌ Nedostaje |
| **Privacy Controls** | Private/Masked/Public opcije | ❌ Nedostaje |
| **Client-Side Hashing** | Datoteka nikad ne doseže poslužitelj | ✅ Samo kod nekih |
| **Forensic Metadata** | IP, lokacija, uređaj, vrijeme - sve zajedno | ❌ Fragmentirano |
| **QR Verification** | QR kod za trenutnu provjeru | ⚠️ Ograničeno |
| **Rate Limiting** | Zaštita od spama (RLS + Client) | ❌ Nedostaje kod većine |

---

## 🗺️ Putokaz: "Trustless" Budućnost

Trenutna verzija **(Beta v1.0)** optimizirana je za pružanje krajnjem korisniku maksimalne brzine, jednostavnog sučelja i besplatnog pristupa. Međutim, naša konačna vizija je prelazak na strukturu gdje čak ni administrator baze podataka (mi) ne može intervenirati.

### Faza 1: Beta (Sada Dostupna)

- **Infrastruktura:** Cloud Database (Supabase).
- **Svrha:** Brzina, eliminacija UX (Korisničko Iskustvo) barijera i prilagodba. Osiguravanje "bez trenja" sigurnosti.

### 🚀 Faza 2: (Što Zahtijeva Backend / Edge Function)

Ova faza pokriva prelazak iz potpuno "Client-Side" funkcionirajuće strukture sustava na sigurniju i upravljanu "Server-Side Authority" strukturu.

| Element | Što Donosi? | Tech Stack | Prioritet |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Function** | Blokiranje spama + sigurnost API ključa | Supabase Edge (Deno) | 🔴 Visok |
| **Potpis Novčanika** | Kriptografska provjera identiteta | Solana Wallet Adapter | 🟡 Srednji |
| **IPFS/Arweave Sigurnosna Kopija** | Decentralizirana nepromjenjivost | IPFS SDK + Pinata | 🟢 Nizak |
| **Mehanizam Opoziva** | Poništavanje lažnih certifikata | DB Schema ažuriranje | 🔴 Visok |
| **Audit Log** | Kriminalistička istraga bilježenje | Prilagođena log tablica | 🟡 Srednji |
| **OpenTimestamps** | Bitcoin sidrenje | OTS JavaScript | 🟢 Nizak |
| **DID integracija** | Decentralized Identity | ION/Ceramic | 🟢 Nizak |

### Faza 3: Potpuna Decentralizacija (Dugoročno)

| Karakteristika | Svrha | ETA |
|---------|-------|-----|
| **Blockchain Registry** | On-chain registracija Ethereum/Solana | Q4 2026 |
| **DAO Governance** | Upravljanje zajednice | Q1 2027 |
| **Multi-Chain Support** | Polygon, Arbitrum, Base | Q2 2027 |
| **Legal Recognition** | Valjanost u turskim sudovima | 2027-2028 |
| **API for Developers** | Javna API krajnja točka | Q3 2026 |

---

## 📊 Analiza Konkurenata (Ažurirana)

PoArt je pozicioniran na "Sweet Spot" (Optimalna Idealna Točka) koja nadopunjuje praznine u postojećim rješenjima.

| Karakteristika | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 証 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Cijena** | 🆓 Besplatno | 🆓 | 💰 Plaćeno | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Vrlo Jednostavno | ❌ CLI | ⚠️ Srednje | ⚠️ Srednje | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ U Stvarnom Vremenu | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Režima | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privatnost | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Potpuno | ❌ | ❌ | ⚠️ Ograničeno | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Trenutna | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Putokaz | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Hrvatska Podrška** | 🔄 U razvoju | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Legenda:**
- ✅ : Potpuna podrška / dostupno
- ⚠️ : Ograničeno / u plaćenim planovima
- ❌ : Nedostaje / nije podržano
- 🔄 : Na Putokazu (u razvoju)
- 🆓 : Potpuno besplatno
- 💰 : Plaćeno / zahtijeva pretplatu

### Nedostaci Konkurenata, Snage PoArt

| Minus | Konkurenti | PoArt |
|------|----------|-------|
| **Složenost Korištenja** | CLI, API znanje, novčanik potreban | Povucite i ispustite, završava za 3 klika |
| **Cjenovna Barijera** | Pretplata $50-500/mjesec | 100% besplatno |
| **Privatnost** | Datoteka se prenosi na poslužitelj | Client-side, datoteka nikad ne napušta |
| **Kriminalistički Podaci** | Samo vremenska oznaka | IP, lokacija, uređaj, vrijeme - sve |
| **Hrvatska Podrška** | Nedostaje ili vrlo ograničena | Nativna jezična podrška |
| **Open Source** | Zatvorena kutija | Sav kod otvoren na GitHub |

---

## 🧬 Struktura Podataka Protokola (JSON Schema)

**Svaki [PoArt] certifikat ima prenosivi i provjerljiv JSON identitet proizveden prema sljedećem standardu.**

> **Napomena:** Ovaj Identity JSON format je format certifikata predstavljen korisniku. U registarskim zapisima se umjesto `identity.asset_data` koristi `registry.asset` (mapiranje: `identity.asset_data` == `registry.asset`).
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
    "title": "Službeni Whitepaper",
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

## 🔬 Tehnička Dubina: Algoritam Zapečaćivanja

### Deterministične Hash Funkcije
```javascript
// Pomoćne Funkcije: Pretvaranje digesta u hex niz
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Pretvaranje niza u polje bajtova
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Generiranje kanoničkog forensics niza (v1.0: fiksni redoslijed polja + UTF-8 + razdvajač \n)
// Napomena Faza 2: Prelazak na kanonički JSON s RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal Proces Proizvodnje (Potpuno Deterministički)
```javascript
// 1. FileHash izračun (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Prikupljanje kriminalističkih podataka (korištenje jedne vremenske oznake)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Generiranje jedne vremenske oznake
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Ista vremenska oznaka
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot stvaranje (s kanoničkim kodiranjem)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal proizvodnja (korištenje iste vremenske oznake)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Pomoćne funkcije maskiranja (IPv4 i IPv6 podrška)
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4 provjera
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 ili nepoznati format
  return "***";
}
```

### Tijek Provjere (Dvije Razine)

#### Quick Verify (Brza Provjera)
```javascript
// Provjerava samo hash datoteke (brza crvena zastava)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Dohvaćanje iz Registra
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Hash usporedba
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Original - Hash datoteke se podudara"
    };
  } else {
    return {
      valid: false,
      message: "❌ Lažno - Datoteka je manipulirana"
    };
  }
}
```

#### Full Verify (Potpuna Provjera)
```javascript
// Reproducira i provjerava EvidenceRoot i NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Dohvaćanje iz Registra
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash provjera (brza crvena zastava)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Lažno - Hash datoteke se ne podudara" };
  }

  // 2) EvidenceRoot reprodukcija (s forensics podacima pohranjenima u registru)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Ne podudara se - EvidenceRoot nevažeći" };
  }

  // 3) NotarySeal reprodukcija (s istom vremenskom oznakom + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Ne podudara se - NotarySeal nevažeći" };
  }

  // Opcionalno: U fazi 2 provjerite također signer_sig s attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Potpis nevažeći" };

  return { valid: true, message: "✅ Original - Full Verify odobren" };
}
```

> **Važne Napomene:**
> - **Quick Verify:** Provjerava samo hash datoteke za brzu upotrebu.
> - **Full Verify:** Provjerava sve slojeve protokola (EvidenceRoot + NotarySeal).
> - Sve hash operacije se izvode deterministički, s fiksnim kodiranjem i razdvajačima.
> - **v1.0 standard kanonizacije:** Fiksni redoslijed polja + UTF-8 kodiranje + `\n` razdvajač.
> - **Plan Faza 2:** Prelazak na kanonički JSON s RFC 8785 (JCS - JSON Canonicalization Scheme).
> - U Masked režimu izračun EvidenceRoot i NotarySeal se izvodi s maskiranim forensics podacima.
> - Koristi se jedna vremenska oznaka u cijelom procesu (forensics + NotarySeal); determinizam zajamčen.
> - **Forensics nazivi polja:** `ip_masked`, `location`, `device`, `timestamp` (kod i registar potpuno kompatibilni).
> - **Put Registra:** `certificate.asset.fingerprints` (potpuno kompatibilan s kodom provjere).
> - **signer_sig u Registru:** Polje `proof.signer_sig` je potrebno za Full Verify.
> - Mehanizam SignerSignature će biti aktiviran u fazi 2 sa Solana Wallet Adapter; u v1.0 može se izvršiti provjera s `attestation_pubkey`.

---

## 📈 Statistika Korištenja (Q1 2026 Ciljevi)

| Metrika | Cilj | Status |
|--------|-------|-------|
| **Ukupni Certifikati** | 1,000 | 🔄 U tijeku |
| **Aktivni Korisnici** | 500 | 🔄 U tijeku |
| **Broj Provjera** | 5,000 | 🔄 U tijeku |
| **Uptime** | %99.9 | ✅ Aktivan |
| **Prosječno Vrijeme Odgovora** | <200ms | ✅ Optimalno |

---

## 🌍 Zajednica i Podrška

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 Suradnici

PoArt protokol se razvija zahvaljujući doprinosima zajednice s otvorenim kodom.

**Za doprinos:**
1. Napravite fork
2. Stvorite granu značajke (`git checkout -b feature/amazing-feature`)
3. Napravite commit (`git commit -m 'Add amazing feature'`)
4. Napravite push (`git push origin feature/amazing-feature`)
5. Otvorite Pull Request

### 🛠️ Što Trebamo Sada? (Poziv za Pomoć)

Tražimo doprinose od iskusnih razvijača u sljedećim temama za razvoj **Faze 2** PoArt protokola:

* **Supabase Edge Functions:** Premještanje zaštite od spama na stranu poslužitelja.
* **Solana Web3.js:** Integracija potpisivanja novčanika (Wallet Signing).
* **IPFS / Arweave:** Integracija usluga arhiviranja i sidrenja.

> Prije dodavanja značajke, molimo započnite raspravu u odjeljku "Issues".

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Kultura Veća od Kapitala*

## 🧾 Licenca

MIT License © 2026 İlhan Art Gallery Initiative

Pogledajte [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) za potpune uvjete.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Ovaj projekt je razvijen s inicijativom [İlhan Art Gallery] i izvorni kod je javno dostupan radi transparentnosti.**

**PROTOKOL V1.0 // ZAPEČAĆENO SA SHA-512.**

*© 2026 İLHAN ART | SVA PRAVA NA DJELA, SLIKE I IDEJE SU ZAŠTIĆENA.*

---
