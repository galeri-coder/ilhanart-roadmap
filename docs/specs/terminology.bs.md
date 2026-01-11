# 📚 Rječnik Tehničkih Pojmova i Koncepata
> **"Razumjeti jezik ovog protokola znači razumjeti njegovu viziju."**

## ⚙️ PoArt Forenzički Motor (PFE) v1.0: Temeljna Arhitektura

**PoArt Forenzički Motor (PFE)** je centralni sloj koji predstavlja logiku i tehničku operaciju iza [PoArt] protokola. Ovo je "forenzički motor" koji uzima sirove podatke proizvodnje umjetnosti i pretvara ih u **digitalni dokaz** koji je provjerljiv i nepromjenjiv.

### 🧩 Zašto "PoArt Forensic"?

- **PoArt (Dokaz Umjetnosti):** Cilj motora je povezati vrijednost digitalnog kapitala ne sa procjenama, već sa **provjerljivim procesom proizvodnje**.
- **Forensic (Naučna Verifikacija):**
  - **Tehnička Definicija:** Algoritamski metod i niz zapisa za verifikaciju da podaci procesa proizvodnje (potezi četkom, video vremena, zapisi) nisu izmijenjeni.
  - **Filozofski Nivo:** Tvrdnja o pretvaranju **cijene ljudskog vremena, rada i odluka** u mjerljivu istinu, nasuprot AI-ovoj proizvodnji "trenutnog rezultata".

> Napomena: Blockchain integracija (npr. Solana) nije jezgro PFE-a; biće opisana odvojeno kao **Chain Anchor Layer** u svrhe verifikacije/registracije.

### 🛠️ Tehnički Opseg v1.0

**PoArt Forenzički Motor (PFE) v1.0** izgrađen je na sljedećim **3 glavna stuba** umjesto složenih finansijskih modela:

1. **Hashing & Sealing (Pečaćenje):**  
   PFE procesira sve elemente u paketu dokaza (fajl rada, video, JSON/zapisi, potpisi, itd.) na determinisan način i generiše jedinstvenu **NotarySeal** vrijednost.

   **Ključni Koncepti (v1.0):**
   - **FileHash (Digitalni Otisak Rada):** Hash generisan iz bajtova fajla rada.
   - **EvidenceRoot (Korijen Paketa Dokaza):** Korijen sažetka koji predstavlja integritet paketa dokaza (Merkle korijen ili hash kanonske reprezentacije).
   - **NotarySeal (Konačna Pečat / PFE Output):** Konačna pečat generisana iz kombinacije EvidenceRoot + vrijeme + potpis.

   **Formule (Jasno Prikazane Investitorima):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Definicije Kanonskog Opterećenja (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Napomena: Vrijednost citirana kao PFE output je **NotarySeal**. **SignerSignature** proces će biti aktiviran u fazi 2 (sa Solana Wallet Adapter); u trenutnoj v1.0, koriste se atestacioni potpisi sistema. Atestacioni javni ključ objavljuje se u registru pod poljem `issuer.attestation_pubkey`.

2. **Indexing (Skladištenje):**  
   Piše na jasnom i upitnom registarskom sloju koji novčanik, kojeg datuma, **dokaz rada** za koje djelo je poslao.  
   *(Ovaj sloj može biti baza podataka; chain integracija je odvojeno opisana kao "Chain Anchor Layer".)*

3. **Verification (Verifikacija):**  
   Kada se postave pitanja o valjanosti rada, PFE ponovo procesira sirove dokaze; matematički provjerava da li se izračunate **EvidenceRoot / NotarySeal** vrijednosti slažu sa sačuvanim zapisima.

---

### 🧮 PoArt Teorema Vrijednosti (The Value Theorem)

[PoArt] protokol ne povezuje vrijednost ($V$) digitalnog kapitala sa nejasnom tržišnom percepcijom, već sa **fizičkom realnošću procesa proizvodnje**.

Vještačka Inteligencija (AI) uništava proces pružajući trenutne rezultate ($t \to 0$). [PoArt], međutim, čuva vrijednost kao akumulaciju elemenata **vremena, rada i agencije**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definicije Varijabli

- **$\int dt$ (Akumulacija Procesa):**  
  Vrijednost nije "trenutni rezultat"; to je **proces** akumuliran između $t_{\text{start}}$ i $t_{\text{end}}$. Kada se period skuplja (AI produkcija), rezultat integracije se približava 0.

- **$P_{\text{labor}}(t)$ (Trenutna Snaga Rada):**  
  Predstavlja intenzitet mentalnog i fizičkog rada utrošenog tokom proizvodnje. Kako se provjerljivi rad povećava, integrand raste.  
  > Napomena: Ovaj termin može se praktično generalizovati "mjerljivim/provjerljivim signalom rada".

- **$I_{\text{agency}}(t)$ (Faktor Agencije):**  
  Sposobnost kreatora da preuzme rizike i donosi odluke. Uzima vrijednosti između $0$ i $1$.
  - **AI ($I \approx 0$):** Izvršava naredbe, ne preuzima rizike, ne plaća cijenu.
  - **Čovjek ($I \to 1$):** Mijenja odluke, okleva, preuzima rizike.

- **$U_{\text{irreversible}}$ (Nepovratna Jedinstvenost):**  
  Iako je u digitalnoj produkciji moguće poništiti (`Ctrl+Z`), u fizičkoj produkciji (boja nanesena na platno, isklesano kamenje, akcija u direktnom prenosu) nema puta nazad. Ova **nepovratna priroda** je dodatni član koji stvara "jedinstvenost" (nepromjenjive karakteristike) u djelu.

### 🔎 Analiza Slučaja: AI "Trenutni Rezultat" protiv Čovjeka "Provjereni Proces"

Sljedeća scena pokazuje kako **PoArt Teorema Vrijednosti** praktično funkcioniše i zašto AI produkcija dobija niži rezultat na [PoArt] skali.

#### Scena A: 10-Sekundna Produkcija Scene sa AI

- **Period ($\Delta t$):** $10$ sekundi (kratak proces)
- **Snaga Rada ($P_{\text{labor}}$):** $1$ jedinica (samo pisanje naredbe)
- **Faktor Agencije ($I_{\text{agency}}$):** $0.01$ (bez rizika, bez cijene)
- **Nepovratna Priroda ($U_{\text{irreversible}}$):** $0$ (reverzibilno / kopirljivo)

**Rezultat:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Komentar:** Iako je rezultat savršen; [PoArt] vrijednost se približava $0$ jer nikakav proces nije živio i nije bilo uključene agencije/rizika.

#### Scena B: 6-Satna Fizička Produkcija u Direktnom Prenosu

- **Period ($\Delta t$):** $6$ sati ($21{,}600$ sekundi)
- **Snaga Rada ($P_{\text{labor}}$):** $0.5$ jedinica (kontinuirani fizički i mentalni rad)
- **Faktor Agencije ($I_{\text{agency}}$):** $0.9$ (mijenjajuće odluke, preuzimanje rizika, nepovratni izbori)
- **Nepovratna Priroda ($U_{\text{irreversible}}$):** $>0$ (fizički signali se ne mogu vratiti)

**Rezultat:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Komentar:** Sa proširenjem procesa i povećanjem agencije (rizika), vrijednost se sakuplja u akumuliranoj formi. Član $U_{\text{irreversible}}$ je dodatni doprinos koji stvara "jedinstvenost" (nepromjenjive karakteristike) u djelu.

---

### ✅ Zaključak: Vrijednost Povezana sa Dokazom (Proof-Bound Value)

Ova teorema izvlači tvrdnju vrijednosti [PoArt] iz "preferencije" ili "tržišne priče" i povezuje je sa **provjerljivom realnošću proizvodnje**.

1. **Bez Procesa, Nema Vrijednosti:**  
   AI uništava proces trenutnim rezultatima ($t \to 0$). Kada se prozor procesa skuplja, rezultat integracije mora opadati:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Agencija i Rizik su Množitelji:**  
   [PoArt] ne mjeri samo "utrošeno vrijeme" već i stvarni nivo odluka, rizika i cijene u tom vremenu. Produkcija bez rizika (AI) ima manju vrijednost:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Jedinstvenost je Fizički Dokaz, ne Marketing:**  
   Nepovratni signali u fizičkoj produkciji (potezi na platnu, komad kamena) su izvan logike `Ctrl+Z` digitalnog. Ova nepovratna priroda ($U_{\text{irreversible}}$) čini djelo jedinstvenim kroz egzistenciju.

> **🔐 Suština:** Teorema vrijednosti može izgledati kao mjerenje neizvjesnosti (iako ekvivalent stvarnog svijeta ne može biti potpuno izmjeren), svrha ove formule je uspostaviti varijable i pokazati smjer. U AI eri, rijetka stvar nije "slika" već **provjerljivi rad, vrijeme i agencija**. [PoArt] mjeri ovu rijetkost i piše je sa **paketom dokaza**.

### 🏛️ Značaj Koncepta "Motora"

Tokeni koji dolaze sa Pump.fun ili sličnih platformi često su samo **"ulaznica"**. **PoArt Forenzički Motor (PFE)**, međutim, je **sloj ustavne logike** koji odlučuje koja prava ova ulaznica štiti, kako će se djelo pisati i kako će se umjetnost/nauka/tehnologija očuvati.

> **Napomena:** Razlog zašto smo započeli ovaj projekat na Pumpfun bio je nedostatak dovoljnih sredstava i nedostatak okruženja za dosezanje trenutne publike putem direktnog prenosa. Upotreba trenutnih podataka bila je strateški ispravan korak, iako nije bila najvišeg kvaliteta. Bez obzira na budžet i resurse, definisanje logike ovog motora na GitHub-u dokazuje da projekat nije samo finansijska procjena, već dugoročna vizija **softverske infrastrukture** i **nacionalne digitalne biblioteke**.

---

## 🎨 [PoArt] Protokol Dokaza Rada (Proof of Art Protocol v1.0)

> **"Pravi umjetnik, prava produkcija, prava vrijednost."**

Ovaj protokol je **proces biološke i intelektualne zaštite** razvijen protiv nepoznatih prevaranta koji okružuju kripto ekosistem, protiv AI slika napravljenih za 5 minuta, i protiv kulture "Pump & Dump".

---

## a) Šta je [PoArt]? (Filozofska i Tehnička Definicija)

**Dokaz Umjetnosti [PoArt];** je institucionalni standard atestacije koji osigurava da vrijednost iza kapitala na blockchain-u nije zasnovana na procjenama, već na **ljudskom radu**, **vremenu** i **provjerljivoj fizičkoj energiji**.

Bitcoin *"sa strujom i snagom procesora"* **(Dokaz Rada)** generiše vrijednost, na sličan način projekti povezani sa [PoArt] *"sa umjetničkom vještinom i ljudskim vremenom"* generišu vrijednost.

Ovo eliminiše rizik *"Developer je prodao, projekat je gotov"* na Pump.fun i DEX platformama; jer ovdje vrijednost nije u kodu već u **kontinuitetu proizvodnje**.

> **[PoArt] učesnicima ne govori "Vjerujte nam"; govori "Ovo je dokaz, vidite svojim očima, verificirajte svojom matematikom."**

---

## b) 5-Stub Standard [PoArt] (5 Stubova Istine)

Ovih 5 stavki su nepromjenjivi filteri kroz koje projekat mora proći da bi dobio [PoArt] pečat.

### 1) Dokaz Direktnog Identiteta

- **Problem:** Kripto svijet je pun nepoznatih osnivača (Devs) sa nejasnim identitetima koji prikupljaju novac i napuštaju projekte.
- **[PoArt] Rješenje:** Kreator ne samo da verificira identitet već i **prisustvo tokom proizvodnje**. Ovo uključuje sesije direktnog prenosa gdje se vodi razgovor sa zajednicom i specifični zahtjevi se implementiraju odmah, ne unaprijed snimljeni video.  
  (Na primjer, *"Napiši današnji datum i trenutni broj bloka u desnom uglu platna"*)
- **Slogan:** *"Botovi mogu slikati ali botovi ne znoje i ne mogu improvizovati."*

### 2) Dokaz Rada i Procesa

- **Problem:** AI (Vještačka Inteligencija) slike napravljene za 2 sekunde dobijaju jednako "jpeg" tretman u digitalnom svijetu kao uljana slika rađena 2 mjeseca.
- **[PoArt] Rješenje:** Proces "začeća i rođenja" djela se piše. Faza skice, faza slikanja, akumulirani sati utrošeni i fizički proces kroz koji je umjetnik prošao dok je stvarao djelo se piše. Ovo dodaje **"cijenu vremena"** tokenu. Proizvodnja kapitala teška, njegova vrijednost jaka.

### 3) Dokaz Estetske Vrijednosti

- **Problem:** "Meme" kultura koja se fokusira samo na trenutni smijeh dok se ljepota i umjetnička dubina zanemaruju, što uzrokuje kratkoročne "Hype" projekte.
- **[PoArt] Rješenje:** Projekat mora imati akademske umjetničke standarde, teoriju boja, pravila kompozicije i poznavanje materijala (Impasto, Texture, itd.). Sadržaj ne samo da treba da vas nasmije; trebao bi stvoriti divljenje u gledaocima i imati **kolekcionarsku vrijednost**.

### 4) Konceptualna Inovacija

- **Problem:** Hiljade kopija psa/mačke tokena bez kreativnosti.
- **[PoArt] Rješenje:** Projekat mora stvoriti novi most koji povezuje umjetnost, nauku, filozofiju ili tehnologiju u značajnoj strukturi.  
  (Na primjer, povezivanje antičke David statue sa kripto tržišnim podacima; procesiranje ideje "ljudske transformacije u kamen" kroz ovo i njeno zasnivanje na naučnim izvorima.)  
  Djelo ne bi trebalo biti samo vizuelni poziv već i **intelektualni izazov** koji stimuliše razmišljanja o nauci, filozofiji ili tehnologiji.

> [!IMPORTANT]
> **Memorabilan Primjer (Las Palmitas Efekat):** U Las Palmitas regionu u Meksiku, pogođenom kriminalom, više od 200 kuća je transformisano u ogromnu duga izložbu. Kao rezultat ove intervencije ljepote, stope kriminala u regionu su značajno pale, a mladi ljudi su počeli učestvovati u umjetnosti umjesto u kriminalnim gangovima. Transformacija ljepote je prepisala poštovanje ljudi prema svom okruženju i jedni drugima (socijalna integracija).
>
> **Očekivanje:** Projekat koji ulazi u [PoArt] listu mora, kao gornji primjer, imati društveni, naučni ili filozofski odnos uzroka i posljedice izvan vizuelne ljepote. Vrijeme je jedini kapital koji se ne može kupiti novcem stoga, u ovom protokolu treba verificovati stavljajući vrijeme kao garanciju. Konceptualna osnova projekta mora biti toliko jaka i univerzalna da, godinama kasnije u mogućoj CTO (Community Takeover) situaciji, zajednica može nastaviti kreativni kapacitet projekta samostalno naslijedivši ovo nasljeđe.

### 5) Ne Algoritamski već Agencija

- **Problem:** Savršena ali bezdušna ponavljajuća digitalna produkcija.
- **[PoArt] Rješenje:** Jedinstvena agencija čovjeka koji može griješiti, preuzeti rizike i osjetiti emocionalne promjene mora se osjetiti u djelu. Neizvjesnost u potezima četkom, iznenadne reakcije materijala i trenutne odluke umjetnika su **biološki potpisi** koji razlikuju djelo od "mehaničke proizvodnje".

---

## c) Proces Verifikacije i Prevencija Prevare

Ovaj sistem osigurava da projekat ostane pouzdan i živ ne samo "na početku" već "uvijek".

### 📦 Paket Dokaza - Digitalni Blizanac

Iza svakog djela odobrenog od [PoArt] postoji enkriptovan i vremenski označen paket podataka koji investitori mogu preuzeti:

- **RAW Video Zapis:** Sirovi kontinuirani film vremena proizvodnje.
- **Analiza Metapodataka:** Datum kreiranja fajla, informacije o korištenim instrumentima i podaci o lokaciji.
- **Fizička Referenca:** Dokaz da djelo postoji u fizičkom svijetu  
  (Na primjer, trenutne novine ili blockchain podaci tog vremena pored djela).

> *Napomena o Usklađenosti:* Termin "paket dokaza" u prethodnim dijelovima se povezuje sa lancem **Paket Dokaza → EvidenceRoot → NotarySeal**; tj., integritet paketa predstavlja se provjerljivim pečatom.

### 🔄 365-Dnevna Obnova (Protokol Održivosti)

- **Revolucionarna Karakteristika:** U kripto projektima "Dev" (Developer) obično objavi token i obično nestane nakon 1-2 mjeseca (soft rug). [PoArt] to čini nemogućim.
- **Pravilo:** Status "verificiranog umjetnika" nije doživotan. Samo **1 godina** je valjana.
- **Operacija:** Umjetnik/Developer mora predstaviti zajednici **novo značajno i provjerljivo djelo** svakih 365 dana.
- **Primjer Scene:** Započeli ste projekat 2026. U januaru 2027, sistem daje upozorenje "dokaz istekao". Ako umjetnik ne predstavi novu izložbu, novo fizičko djelo ili novu tehničku integraciju tada "oznaka povjerenja" projekta pada.
- **Rezultat:** Ovaj sistem osigurava **sadržaj nikada ne gubi relevantnost** i investitor nikad nema strah *"Je li Developer još tu?"*. Projekat postaje živi studio.

### 🚩 Protokol Crvene Zastave

**U bilo kojoj situaciji prevare otkrivene od strane zajednice ili algoritma (korištenje AI, ukradeno djelo, manipulirani video):**

1. Certifikat se odmah označava kao **"VOID" (ništavan)**.
2. Paketi dokaza se javno označavaju kao **"lažni"**.
3. Projekat se stavlja u [PoArt] crnu listu. Ovo u decentralizovanom svijetu, **reputacija je valuta** jača.

---

## d) Zaključak: Ne Kazino, već Muzej

**Pump.fun i Decentralizovane Berze (DEX) nažalost su sada kazina; svjetla trepere, svi jure za brzim profitima, i kuća (prevarant) uvijek pobjeđuje. Razlog zašto smo započeli projekat ovdje bio je nedostatak dovoljnih sredstava i nepostojanje okruženja za dosezanje trenutne publike putem direktnog prenosa.**

**[PoArt] je tvrđava izgrađena usred ovog kazina.**

- 🎰 Kazino je zasnovan na igrama karata; mi smo **zasnovani na fizičkoj realnosti**.
- 🃏 Kazino je otvoren za prevaru; mi smo **otvoreni za jasne dokaze**.
- ⏳ Kazino je privremen; mi smo **fokusirani na vječnost umjetnosti i nauke**.

**Token koji koristi ovaj protokol nije samo "novčić"; to je digitalni kapital sa znojem, bojom, kodom i vizijom.**

---

## 🗳️ 6) Upravljanje i Javni Registar

**Svrha ovog dijela: Transformisati [PoArt] standard iz nivoa "povjerenja u osobe" u održivu javnu infrastrukturu sa registar + verifikacija + nadzor zajednice.**

### 6.1 Javni Registar

- **Javni Registar:** Svi odobreni podaci se pišu u `ilhanart.org/registry` (ili GitHub Registry).

**Logika Registra (Predloženi Standard - u JSON Path Formatu):**

Svaki unos koji ulazi u registar ima ova minimalna provjerljiva jezgra polja:

- **Identitet i Status:**
  - `certificate_id` (čitljiva referenca)
  - `status` (active / void)
  - `void_reason` (ako je primjenjivo)
  - `visibility` (private / masked / public)
  - `created_at` (vremenski žig)

- **Izdavački Autoritet:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informacije o Djelu:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (ako je moguće; za identifikaciju sa token vratom)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Forenzički Podaci:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Kriptografski Dokaz:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Upravljanje:**
  - `governance.decision`
  - `governance.veto_threshold`

Registar može imati dva nivoa:
- **1)** Čovjeku-čitljiv indeks (web lista / pretraga / filter)
- **2)** Mašini-čitljiva reprezentacija (JSON zapis; za PFE verifikaciju)

**Ova "registracija" postaje provjerljiva putem PFE lanca paketa dokaza → EvidenceRoot → NotarySeal. Registar pruža ciljeve verifikacije, ne "tvrdnje".**

---

### 6.2 40% Veto Zajednice (Token-Gated Upravljanje)

- **40% Veto Zajednice:** Glasanje počinje mjesec dana prije davanja statusa; **40% zajednice token-gated (verificirane sa Solana)** veto poništava prijavu.

**Tok Glasanja (Predloženi Jasan Proces):**
- **Prozor Prijave:** Kandidat projekat otvara "PoArt Kandidat Registraciju" (zapisi kandidata se pojavljuju u "pending" statusu).
- **Period Revizije:** Zajednica ispituje dokaze do 30 dana (paket dokaza + zapisi direktnog prenosa + metapodaci).
- **Token-Gated Verifikacija:** Glasanje se vrši sa verificiranim Solana novčanicima (npr. specifično token/NFT vlasništvo + potpis novčanika).
- **Pravilo Veta:** Ako 40% glasova bude **opozicija (ne / veto)** tada se prijava poništava.
- **Transparentnost:** Rezultati glasanja se čuvaju u registru kao "zapis odluke" (datum, omjer, ID slike).

---

### 6.3 Sinhronizacija Metapodataka (Usklađivanje sa Fizičkim Svijetom)

- **Sinhronizacija Metapodataka:** Tehnički podaci u registru moraju 100% odgovarati fizičkom entitetu.

**Tehnička Definicija "100% Usklađivanja" (Predložena Transparentnost):**
- **Minimalno Usklađivanje (Obavezno):**
  - `asset.fingerprints.sha256/sha512` u registru mora biti **identičan** sa hash-om diskutovanog fajla.
  - `proof.notary_seal` u registru ponovo kreirano (ako je paket dokaza prisutan), mora biti **identičan**.
- **Usklađivanje Fizičke Reference (Tip Dokaza):**
  - Fizičko djelo + datum/blok referenca prikazana u direktnom prenosu i isti dokaz moraju se slagati sa paketom dokaza.
- **Usklađenost Privatnosti:**
  - Polja kao IP/lokacija u `masked` vidljivosti se objavljuju **prema standardima maskiranja**.

---

### 6.4 Spor i Opoziv

Registar nije samo proces "odobrenja"; to je **živi proces revizije** protiv prevare.

- Kada počne spor, unos se može staviti u **"review" (revizija)** status.
- Kada se otkrije prevara, označava se kao `status: void` i dodaje se razlog:
  - `void_reason` (korištenje AI / krađa / manipulacija, itd.)
  - `revoked_at` (vrijeme opoziva)
- Izvor odluke opoziva je jasan u registru:
  - Glasanje zajednice / Zvanični Komitet / Napomena Naučne Istrage (primjenjivo)

> **Ovaj dio je registarski blizanac VOID koncepta u dijelu "Protokol Crvene Zastave".**

---

### 6.5 Primjer Unosa u Registar (Mašinski Čitljiv)
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
> *Napomena: `asset.fingerprints.sha512` i druge hash vrijednosti su skraćene u svrhe prikaza; u stvarnoj implementaciji, koriste se heksadecimalni stringovi pune dužine.*

---

## 7) 🔐 Tehnički Pečat (NOTARY SEAL)

**Algoritam nepromjenjivog pečata generisan od PoArt Forenzičkog Motora (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Protokol Digitalnog Notara i Naučnog Dokaza (Beta v1.0)

> **"Kultura je veća od Kapitala. Zaštiti svoja djela danas, prenesi sutra."**

---

## Zašto Javno?

Prava sigurnost dolazi iz transparentnosti. Zahvaljujući našem **Javnom Registru** sistemu, bilo ko bilo gdje u svijetu može u sekundama verificirati da li je fajl pravi, bez potrebe za autoritetom.

---

## 🧩 Zašto Više "Modula Vidljivosti"?

Ovo je najvažniji dio koda (meni opcije vidljivosti). Ove opcije omogućavaju korisnicima da naprave balans u **"Privatnost protiv Transparentnost"**:

### 🔒 Privatno

- **Scena:** Umjetnik još ne želi objaviti djelo, ali želi vremenski označiti da dokaže "Ovo sam napravio ovog datuma".
- **Šta Kod Radi:** Piše podatke u bazu podataka ali označava pečat kao `visibility: "private"`. Kasnije kada pišeš politiku "javnog čitanja", možeš sakriti ove zapise od ljudi sa `WHERE visibility = 'public'`.

### 🕶️ Maskirano

- **Scena:** Umjetnik želi transparentnost ali se boji da će se adresa njegove kuće (IP lokacija) saznati.
- **Šta Kod Radi:** Funkcije `maskIP` i `maskLoc` rade na JavaScript strani. Ovo mijenja IP adresu u `88.241.***.***` format, lokaciju u `***/TR` format, i šalje cenzurisanu verziju u bazu podataka.
- **Istina o Privatnosti:** Maskiranje se vrši u pretraživaču, Supabase ne vidi stvarnu lokaciju. **Ali:** Ako se koriste API-ji treće strane kao ipapi.co za podatke o lokaciji, ovi provajderi vide IP adresu tokom zahtjeva.
- **Pečaćenje u Maskiranom Modu:** EvidenceRoot i NotarySeal kalkulacija se vrši sa maskiranim forenzičkim podacima; stoga verifikacija ostaje deterministička.

### 🌍 Javno

- **Scena:** Potpuna transparentnost. Prema [PoArt] standardima, gdje, kada, iz koje mreže je djelo kreirano se javno objavljuje.

---

## 💡 Tehnička Inovacija

PoArt nije samo sistem uploadovanja fajlova. Ovo je **"lanac naučne njege"** motor koji miješa tri različita tehnička nivoa u jednom kotlu da donese novi standard.

**Sloj opisan kao "motor" u ovom dijelu odgovara jezgru PoArt Forenzičkog Motora (PFE) u prethodnim uslovima.**

### 1) Client-Side Hashing (Maksimalna Privatnost)

Fajlovi vaših umjetničkih komada se ne uploaduju na server. Naš baziran-na-pretraživaču (client-side) motor kalkuliše hash fajla (digitalni sažetak) na vašem vlastitom računaru. Samo ovaj digitalni otisak i metapodaci se šalju na server.

> **Istina o Privatnosti:** Fajl djela se ne uploaduje na server i tako je siguran. Međutim, forenzički podaci (IP/lokacija) se dijele prema odabranom modu vidljivosti (privatno/maskirano/javno).

### 2) Forenzička Fuzija Podataka (Naučna Snaga)

Više od običnog vremenskog žiga. Sistem povezuje ove podatke u "korijen pečata":

- **Digitalni Sažetak (SHA-512):** Digitalni otisak koristeći kriptografski sažetak standard (SHA-512) koji će se slomiti ako se jedan pixel djela promijeni.
- **Lokacija i Vrijeme:** Kodiranje podataka o datumu, zemlji, gradu i okrugu sa milisekundnom preciznošću.
- **Identifikacija Uređaja:** Operativni sistem, pretraživač i tip uređaja (User-Agent analiza).

---

## 🛡️ Slučajevi Korištenja i Prednosti

Ako ste umjetnik, pisac ili dizajner, reći "Ja sam ovo prvi napravio" nije dovoljno; morate dokazati.

**Vaše djelo pečatirano sa PoArt:**

- **Matematički Dokaz:** Ako se promijeni čak i jedan pixel vašeg fajla, sistem zna. Manipulacija je nemoguća.
- **Pravna Osnova:** Napisano je kojeg datuma, kojeg grada, sa kojeg uređaja je djelo pečatirano.
- **Trenutni Certifikat:** U sekundama generiše za vas specijalan **"Certifikat Identiteta Kapitala"**, QR kod i pečatirano.

---

## ⚙️ Arhitektura Sistema i Tehničke Karakteristike

Sistem je dizajniran na "serverless" arhitekturi, fokusirajući se na visoke performanse i skalabilnost.

| Sloj | Tehnologija | Opis |
|--------|-----------|-------------|
| **Enkripcija** | SHA-256 & SHA-512 | Dva-slojna kriptografska sažetak |
| **Baza Podataka** | Supabase (PostgreSQL) | JSONB struktura podataka, RLS politike |
| **Forenzički Podaci** | ipapi.co API | IP/lokacija/vrijeme trokut |
| **Prezentacija** | html2canvas + jsPDF | Client-side PNG/PDF kreacija |
| **Frontend** | Vanilla JavaScript | Nula framework zavisnost |
| **Sigurnost** | Client-Side Hashing | Fajl nikad ne ide na server |

### Značajne Karakteristike

| Karakteristika | Opis | U Konkurentima? |
|---------|-------|-----------------|
| **UI Povuci i Spusti** | Povuci i spusti fajl, trenutni pregled | ❌ U većini nema |
| **Multi-Format Izvoz** | PNG, JSON, PDF - jednim klikom | ⚠️ Ograničeno |
| **Real-Time Pregled** | Pregled certifikata direktno | ❌ Niko |
| **Kontrola Privatnosti** | Privatno/maskirano/javno opcije | ❌ Niko |
| **Client-Side Hash** | Fajl nikad ne ide na server | ✅ Samo u nekima |
| **Forenzički Metapodaci** | IP, lokacija, uređaj, vrijeme - svi zajedno | ❌ Podijeljeno |
| **QR Verifikacija** | Trenutna verifikacija QR kod | ⚠️ Ograničeno |
| **Ograničenje Brzine** | Spam zaštita (RLS + klijent) | ❌ U većini nema |

---

## 🗺️ Put Naprijed: Budućnost "Bez Povjerenja"

Trenutna verzija **(Beta v1.0)** dizajnirana je da pruži krajnjim korisnicima maksimalnu brzinu, lak interfejs i besplatan pristup. Naša konačna vizija, međutim, je transformacija u strukturu gdje administrator baze podataka (mi) čak ne može ni intervenisati.

### Faza 1: Beta (Sada Direktno)

- **Infrastruktura:** Cloud Baza Podataka (Supabase).
- **Svrha:** Brzina, uklanjanje UX (korisničko iskustvo) prepreka i usklađenost. Pružanje "bez-trenja" sigurnosti.

### 🚀 Faza 2: (Backend / Edge Funkcija Potrebe)

Ova faza uključuje transformaciju iz "client-side" pune administracije strukture u "server-side authority" strukturu koja je sigurnija i kontrolabilnija.

| Stavka | Šta Donosi? | Tehnički Stek | Prioritet |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Funkcija** | Sprečavanje spam-a + API ključ sigurnost | Supabase Edge (Deno) | 🔴 Visok |
| **Wallet Potpis** | Kriptografska verifikacija | Solana Wallet Adapter | 🟡 Srednji |
| **IPFS/Arweave Backup** | Decentralizovana nepromjenjivost | IPFS SDK + Pinata | 🟢 Nizak |
| **Proces Opoziva** | Opozovi lažne certifikate | DB schema update | 🔴 Visok |
| **Revizijski Logovi** | Zapisi naučne istrage | Specijalni zapis tabele | 🟡 Srednji |
| **OpenTimestamps** | Bitcoin sidro | OTS JavaScript | 🟢 Nizak |
| **DID Integracija** | Decentralizovani identitet | ION/Ceramic | 🟢 Nizak |

### Faza 3: Potpuna Decentralizacija (Dugoročno)

| Karakteristika | Cilj | ETA |
|---------|------|-----|
| **Blockchain Registar** | On-chain Ethereum/Solana registracija | Q4 2026 |
| **DAO Upravljanje** | Upravljanje zajednice | Q1 2027 |
| **Multi-Chain Podrška** | Polygon, Arbitrum, Base | Q2 2027 |
| **Pravno Priznanje** | Valjanost u turskim sudovima | 2027-2028 |
| **API za Developere** | Javne API krajnje tačke | Q3 2026 |

---

## 📊 Analiza Konkurencije (Ažurirano)

PoArt stoji u "Sweet Spot" popunjavajući praznine trenutnih rješenja.

| Karakteristika | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Cijena** | 🆓 Besplatno | 🆓 | 💰 Plaćeno | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI Povuci i Spusti** | ✅ Vrlo lako | ❌ CLI | ⚠️ Srednje | ⚠️ Srednje | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Izvoz** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Pregled** | ✅ Direktno | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Kontrola Privatnosti** | ✅ 3 Moda | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privatnost | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forenzički Metapodaci** | ✅ Potpuno | ❌ | ❌ | ⚠️ Ograničeno | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verifikacija** | ✅ Trenutno | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Ograničenje Brzine** | ✅ RLS+Klijent | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Sidro** | 🔄 Put Naprijed | ✅ Bitcoin | ✅ Ethereum | ✅ Više | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Bosanska Podrška** | ✅ Nativna | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Ključ:**
- ✅ : Potpuna podrška / Dostupno
- ⚠️ : Ograničeno / U plaćenim planovima
- ❌ : Nijedno / Nije podržano
- 🔄 : U putu naprijed (u razvoju)
- 🆓 : Potpuno besplatno
- 💰 : Plaćeno / Registracija potrebna

---

**[PoArt] Protokol Dokaza Umjetnosti v1.0**  
*"Kultura > Kapital"*

## 🧾 Licenca

MIT Licenca © 2026 Ilhan Art Gallery Initiative

Za potpune uslove vidi [![Licenca](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE).

---

## 💬 Priznanja

![Verzija](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Sigurnost](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platforma](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![Licenca](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Ovaj projekat je razvijen od strane [Ilhan Art Gallery] inicijative, i njegov izvorni kod je javno dostupan za transparentnost.**

**Protokol V1.0 // Pečatirano sa SHA-512**

*© 2026 İLHAN ART | Sva prava zadržana za umjetnička djela, slike i ideje.*

---
