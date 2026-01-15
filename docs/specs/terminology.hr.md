# 📚 TERMINOLOGIJA I RJEČNIK POJMOVA
> **„Razumjeti jezik ovog protokola znači razumjeti njegovu viziju."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Temeljna infrastruktura

**PoArt Forensic Engine (PFE)** predstavlja temeljni logički sloj i tehničko funkcioniranje iza [PoArt] protokola. Ovo je „forenzički motor" koji uzima sirove proizvodne podatke umjetničkog djela i pretvara ih u provjerljiv i nepromjenjiv **digitalni dokaz**.

### 🧩 Zašto „PoArt Forensic"?

- **PoArt (Proof of Art):** Fokus motora je povezati vrijednost digitalnog sredstva ne sa spekulacijom, već s **dokazivim proizvodnim procesom**.
- **Forensic (Forenzička verifikacija):**
  - **Tehnička definicija:** Algoritam i pristup lanca zapisa za provjeru da podaci iz proizvodnog procesa (potezi kista, timelapse, logovi) nisu manipulirani.
  - **Filozofski sloj:** Tvrdnja da se ljudska proizvodnja koja sadrži **vrijeme, trud i cijenu odluka** transformira u mjerljivu stvarnost, za razliku od „trenutnog izlaza" umjetne inteligencije.

> Napomena: Integracija s blockchainom (npr. Solana) nije jezgra PFE-a; tretira se kao zasebni **Chain Anchor Layer** za verifikaciju/registraciju.

### 🛠️ v1.0 Tehnički opseg

**PoArt Forensic Engine (PFE) v1.0** izgrađen je na **3 glavna stupa** umjesto složenih financijskih modela:

1. **Hashing & Sealing (Pečaćenje):**  
   PFE deterministički obrađuje sve elemente u Evidence Pack-u (datoteka djela, video, JSON/log, potpis itd.) i proizvodi jedinstvenu **NotarySeal** vrijednost.

   **Temeljni pojmovi (v1.0):**
   - **FileHash (otisak djela):** Hash generiran iz bajtova datoteke djela.
   - **EvidenceRoot (korijen paketa dokaza):** Korijenski sažetak koji predstavlja integritet Evidence Pack-a (Merkle root ili kanonski manifest hash).
   - **NotarySeal (konačni pečat / PFE izlaz):** Konačni pečat generiran iz kombinacije EvidenceRoot + vrijeme + potpis.

   **Formule (jasno vidljive investitorima):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Definicije Canonical Payload-a (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Napomena: Vrijednost koja se podrazumijeva kao PFE izlaz je **NotarySeal**. Mehanizam **SignerSignature** bit će aktiviran u Fazi 2 (sa Solana Wallet Adapterom); u trenutnoj v1.0 koristi se vlastiti attestation potpis sustava. Javni ključ za attestation objavljuje se u registru u polju `issuer.attestation_pubkey`.

2. **Indexing (Arhiviranje):**  
   Bilježi koji je novčanik predstavio **Labor Proof (Dokaz o radu)** za koje djelo, na koji datum; u transparentni i pretraživi sloj registracije.  
   *(Ovaj sloj može biti baza podataka; integracija s lancem definira se zasebno kao „Chain Anchor Layer".)*

3. **Verification (Verifikacija):**  
   Kada se ospori izvornost djela, PFE ponovno obrađuje sirove dokaze; s matematičkom preciznošću testira odgovaraju li izračunate vrijednosti **EvidenceRoot / NotarySeal** zapisu u arhivi.

---

### 🧮 PoArt Teorem vrijednosti (The Value Theorem)

[PoArt] protokol povezuje vrijednost ($V$) digitalnog sredstva ne sa subjektivnom percepcijom tržišta, već s **fizičkom stvarnošću proizvodnog procesa**.

Umjetna inteligencija (AI) eliminira proces dajući rezultat trenutno ($t \to 0$). [PoArt] tretira vrijednost kao akumulaciju komponenti **vremena, rada i volje**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definicije varijabli

- **$\int dt$ (Akumulacija procesa):**  
  Vrijednost nije trenutni „izlaz"; to je **proces** koji se akumulira između $t_{\text{start}}$ i $t_{\text{end}}$. Kako se vrijeme smanjuje (AI proizvodnja), rezultat integrala se približava 0.

- **$P_{\text{labor}}(t)$ (Trenutna radna snaga):**  
  Predstavlja intenzitet mentalnog i fizičkog napora utrošenog u trenutku proizvodnje. Kako dokazivi napor raste, integrand raste.  
  > Napomena: Ovaj pojam može se u praksi normalizirati kroz „mjerljive/dokazive signale rada".

- **$I_{\text{agency}}(t)$ (Koeficijent volje):**  
  Kapacitet proizvođača za preuzimanje rizika i donošenje odluka. Prima vrijednost između $0$ i $1$.
  - **AI ($I \approx 0$):** Izvršava naredbe, ne preuzima rizike, ne plaća cijenu.
  - **Čovjek ($I \to 1$):** Mijenja odluke, oklijevao, preuzima rizike.

- **$U_{\text{irreversible}}$ (Nepovratna singularnost):**  
  Dok je poništavanje (`Ctrl+Z`) moguće u digitalnoj proizvodnji, u fizičkoj proizvodnji (boja na platnu, isklesani mramor, gesta u live prijenosu) nema povratka. Ova **nepovratnost** je dodatni pojam koji stvara „singularnost" (non-fungible karakter) u djelu.

### 🔎 Studija slučaja: AI „Trenutni izlaz" vs. Čovjek „Dokazani proces"

Sljedeći scenarij pokazuje kako **PoArt Teorem vrijednosti** funkcionira u praksi i zašto AI proizvodnje dobivaju niske rezultate prema [PoArt] standardu.

#### Scenarij A: Proizvodnja slike s AI za 10 sekundi

- **Vrijeme ($\Delta t$):** $10$ sekundi (gotovo nikakav proces)
- **Radna snaga ($P_{\text{labor}}$):** $1$ jedinica (samo pisanje naredbe)
- **Koeficijent volje ($I_{\text{agency}}$):** $0.01$ (bez rizika, bez cijene)
- **Nepovratnost ($U_{\text{irreversible}}$):** $0$ (može se poništiti / kopirati)

**Rezultat:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Tumačenje:** Čak i ako je izlaz besprijekoran; budući da proces nije doživljen i ne sadrži volju/rizik, [PoArt] vrijednost se približava $0$.

#### Scenarij B: 6 sati fizičke proizvodnje u live prijenosu

- **Vrijeme ($\Delta t$):** $6$ sati ($21{,}600$ sekundi)
- **Radna snaga ($P_{\text{labor}}$):** $0.5$ jedinica (kontinuirani fizički i mentalni napor)
- **Koeficijent volje ($I_{\text{agency}}$):** $0.9$ (promjene odluka, preuzimanje rizika, nepovratni izbori)
- **Nepovratnost ($U_{\text{irreversible}}$):** $>0$ (fizički tragovi ne mogu se poništiti)

**Rezultat:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Tumačenje:** Kako se proces produžuje i volja (rizik) raste, vrijednost kumulativno raste. Pojam $U_{\text{irreversible}}$ je dodatni doprinos koji stvara „singularnost" (non-fungible karakter) u djelu.

---

### ✅ Zaključak: Zaključavanje vrijednosti dokazom (Proof-Bound Value)

Ovaj teorem uzima tvrdnju o vrijednosti [PoArt]-a iz „sviđanja" ili „tržišnog narativa" i povezuje je s **dokazivom proizvodnom stvarnošću**.

1. **Nema vrijednosti bez procesa:**  
   AI eliminira proces u trenutnom izlazu ($t \to 0$). Kako se prozor procesa sužava, rezultat integrala se smanjuje kao matematička nužnost:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Volja i rizik su multiplikatori:**  
   [PoArt] mjeri ne samo „utrošeno vrijeme"; već i sloj stvarne odluke, rizika i cijene tijekom tog vremena. Proizvodnja bez rizika (AI) ima nisku vrijednost:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Singularnost je fizički dokaz, ne marketing:**  
   U fizičkoj proizvodnji nepovratni tragovi (udarac na platno, pukotina u mramoru) su izvan logike `Ctrl+Z` u digitalnom. Ova nepovratnost ($U_{\text{irreversible}}$) čini djelo ontološki jedinstvenim.

> **🔐 SAŽETAK:** Čak i ako teorem vrijednosti izgleda neodređeno kao mjerenje (čak i ako se ne može 100% izmjeriti u stvarnom životu), svrha ove formule je pokazati konstrukciju i smjer varijabli. U eri AI-ja rijetka stvar nije „slika"; to je **dokazivi rad, vrijeme i volja.** [PoArt] mjeri tu oskudicu i registrira je s **Evidence Pack**-om.

### 🏛️ Značaj koncepta „Engine" (Motor)

Tokeni s Pump.fun ili sličnih platformi često su samo **„ulaznice za pristup"**. **PoArt Forensic Engine (PFE)** je **ustavni logički sloj** koji određuje koja prava ta ulaznica štiti, kako će rad biti zabilježen i kako će umjetnost/znanost/tehnologija biti sačuvana.

> **Napomena:** Razlog zašto smo pokrenuli ovaj projekt na Pump.fun je taj što je naš cilj također poboljšati to mjesto, a imamo postojeće podatke i krug koji će doseći postojeću publiku putem live prijenosa.

---

## 🎨 [PoArt] PROTOKOL DOKAZA O RADU (Proof of Art Protocol v1.0)

> **„Pravi umjetnik, prava proizvodnja, prava vrijednost."**

Ovaj protokol je **biološki i intelektualni obrambeni mehanizam** razvijen protiv anonimnih prevaranata koji okružuju kripto ekosustav, AI slika proizvedenih za 5 minuta i „Pump & Dump" kulture.

---

## a) Što je [PoArt]? (Filozofska i tehnička definicija)

**Proof of Art [PoArt];** je institucionalni standard verifikacije koji jamči da se vrijednost iza sredstva na blockchainu temelji na provjerljivom **ljudskom radu**, **vremenu** i **fizičkoj energiji**, a ne na spekulaciji.

Baš kao što Bitcoin proizvodi vrijednost s *„Električnom i procesorskom snagom"* **(Proof of Work)**; projekti kompatibilni s [PoArt] proizvode vrijednost s *„Utrošenim talentom i ljudskim vremenom"*. „Stake-aju" vrijeme.

Eliminira rizik *„Programer (Dev) prodao, projekt završio"* na platformama Pump.fun i DEX; jer ovdje vrijednost nije skrivena u kodu, već u **kontinuitetu proizvodnje**.

> **[PoArt] ne kaže svom sudioniku „Vjerujte nam"; kaže „Evo dokaza, vidi svojim očima, provjeri svojom matematikom".**

---

## b) [PoArt] 5 standarda (The 5 Pillars of Truth)

Ovih 5 točaka su nemanipulirajući filteri kroz koje projekt mora proći da bi dobio [PoArt] pečat.

### 1) Dokaz o živom identitetu (Live Identity Proof)

- **Problem:** Kripto svijet je pun anonimnih osnivača (Dev-ova) s nejasnim identitetom koji prikupe novac i napuste projekt.
- **[PoArt] Rješenje:** Proizvođač dokazuje ne samo svoju osobnu iskaznicu, već i **svoju prisutnost u trenutku proizvodnje**. Ovo uključuje sesije live prijenosa u kojima se interagira sa zajednicom i ispunjavaju se trenutni specifični zahtjevi, a ne unaprijed snimljeni videozapisi.  
  (Npr.: *„Napiši današnji datum i trenutni broj bloka u desni kut platna"*)
- **Moto:** *„Botovi mogu slikati, ali botovi se ne znoje i ne improviziraju."*

### 2) Dokaz o radu i procesu (Labor & Process Proof)

- **Problem:** AI slike proizvedene za 2 sekunde tretiraju se kao isti „jpeg" u digitalnom svijetu kao i uljana slika napravljena za 2 mjeseca.
- **[PoArt] Rješenje:** „Trudnoća i porod" djela se bilježi. Faze skice, slojevi boje, kumulativni utrošeni sati i fizički proces koji je umjetnik doživio dok je stvarao djelo se dokumentiraju. Ovo dodaje **„Vremenski trošak" (Time Cost)** tokenu. Što je teže proizvesti sredstvo, to je njegova vrijednost čvršća.

### 3) Dokaz o estetskoj vrijednosti (Aesthetic Value Proof)

- **Problem:** Ignoriranje estetike i umjetničke dubine od strane „Meme" kulture za fokusiranje samo na trenutnu komediju i rezultirajući kratkotrajni „Hype" projekti.
- **[PoArt] Rješenje:** Projekt mora imati akademske umjetničke standarde, teoriju boja, pravila kompozicije i poznavanje materijala (Impasto, Tekstura itd.). Sadržaj ne smije samo zabavljati; mora izazivati divljenje kod gledatelja i nositi **kolekcionarsku vrijednost**.

### 4) Konceptualna inovacija (Conceptual Novelty)

- **Problem:** Tisuće novčića psa/mačke koji kopiraju jedni druge, bez kreativnosti.
- **[PoArt] Rješenje:** Projekt mora izgraditi novi most koji objedinjuje umjetnost, znanost, filozofiju ili tehnologiju u smislenu strukturu.  
  (Npr.: Kombiniranje klasičnog kipa Davida s podacima s kripto tržišta; obrada ideje o „pretvaranju u kamen" ljudske percepcije i utemeljenje na znanstvenim izvorima.)  
  Djelo mora biti ne samo vizualna gozba; već i intelektualni izazov koji tjera na razmišljanje o **Znanosti, Filozofiji ili Tehnologiji**.

> [!IMPORTANT]
> **Referentni primjer (Las Palmitas efekt):**  
> U četvrti Las Palmitas u Meksiku, koja se borila s kriminalom, više od 200 kuća pretvoreno je u ogromnu duginsku proslavu. Kao rezultat ove estetske intervencije, stopa kriminala u četvrti je u određenoj mjeri pala, a mladi su se počeli zanimati za umjetnost umjesto za bande. Estetska promjena rekodirala je poštovanje ljudi prema njihovoj okolini i jednih prema drugima (Social Cohesion).
>
> **Očekivanje:** Projekt koji ulazi na [PoArt] listu mora, baš kao u gornjem primjeru, sadržavati sociološki, znanstveni ili filozofski uzročno-posljedični odnos izvan čiste vizualne estetike. Budući da je jedino sredstvo koje se ne može kupiti novcem „Vrijeme", u ovom protokolu vrijeme se mora stake-ati kao kolateral i dokazati. Konceptualna osnova projekta mora biti toliko snažna i univerzalna da čak i u scenariju mogućeg CTO-a (Community Take Over) godinama kasnije, zajednica može preuzeti to nasljeđe i autonomno nastaviti inovativni potencijal projekta.

### 5) Ne-algoritamska volja (Non-Algorithmic Agency)

- **Problem:** Besprijekorne, ali bezdušne, ponavljajuće digitalne produkcije.
- **[PoArt] Rješenje:** Jedinstvena volja čovjeka koji može griješiti, preuzimati rizike i doživljavati emocionalne fluktuacije mora se osjećati u djelu. Nesigurnost u potezima kista, neočekivane reakcije materijala i trenutne odluke umjetnika su **Biološki potpis** koji razlikuje djelo od „Strojne proizvodnje".

---

## c) Mehanizam verifikacije i borbe protiv krivotvorenja

Ovaj sustav osigurava da projekt ostane pouzdan i živ ne samo „na početku", već „zauvijek".

### 📦 Paket dokaza (Evidence Pack - The Digital Twin)

Iza svakog [PoArt] certificiranog djela nalazi se kriptirani i vremenski označeni paket podataka koji investitori mogu preuzeti:

- **RAW video snimke:** Neprekidni sirovi snimci iz trenutka proizvodnje.
- **Analiza metapodataka:** Datum stvaranja datoteke, informacije o korištenom uređaju i podaci o lokaciji (Grad-Država).
- **Fizičke reference:** Dokazi da djelo postoji u fizičkom svijetu  
  (Npr.: Aktualne novine pored djela ili blockchain podaci iz tog trenutka).

> *Napomena o dosljednosti:* Izraz „paket dokaza" povezuje se s linijom **Evidence Pack → EvidenceRoot → NotarySeal** iz prethodnih odjeljaka; tj. integritet paketa predstavljen je provjerljivim pečatom.

### 🔄 365-dnevna obnova (The Sustainability Protocol)

- **Revolucionarna značajka:** U kripto projektima „Dev" (Programer) pušta token na tržište i obično nestaje nakon 1-2 mjeseca (Soft Rug). [PoArt] to čini nemogućim.
- **Pravilo:** Status „Verified Artist" (Verificirani umjetnik) nije doživotan. Vrijedi samo **1 godinu**.
- **Mehanizam:** Umjetnik/Programer mora svakih 365 dana predstaviti zajednici **novo, veliko i dokazivo djelo**.
- **Primjer scenarija:** Pokrenuli ste projekt 2026. U siječnju 2027. sustav daje upozorenje „Rok dokaza istekao". Ako umjetnik ne predstavi novu izložbu, novo fizičko djelo ili novu tehnološku integraciju, „Značka povjerenja" projekta pada.
- **Rezultat:** Ovaj sustav osigurava da **sadržaj nikada ne izgubi aktualnost** i da investitor ne doživi strah *„Je li programer još uvijek tu?"*. Projekt se pretvara u živi studio.

### 🚩 Crvena zastava (Red Flag Protocol)

**U slučaju otkrivanja bilo kakve krivotvorine (korištenje AI-ja, ukradeno djelo, manipulirani video) od strane zajednice ili algoritama:**

1. Certifikat se odmah označava kao **„PONIŠTEN" (VOID)**.
2. Paketi dokaza se javno označavaju kao **„Lažni"**.
3. Projekt se stavlja na crnu listu [PoArt]. Ovo učvršćuje stvarnost da je **reputacija jedina valuta** u decentraliziranom svijetu.
4. Nikakve [PoArt] izjave ne mogu se koristiti u bilo kojoj objavi, jedini valjani izvor je https://www.ilhanart.org/public-registry

---

## d) Zaključak: Muzej, ne kasino

**Pump.fun i decentralizirane burze (DEX) su nažalost trenutno kasina; svjetla bljeskaju, svi jure za brzom zaradom i kuća (prevaranti) uvijek pobjeđuje. Razlog zašto smo pokrenuli projekt ovdje je također naš pokušaj da poboljšamo ovo mjesto, a imamo postojeće podatke i krug koji će doseći postojeću publiku putem live prijenosa.**

**[PoArt] je tvrđava izgrađena usred tog kasina.**

- 🎰 Kasino se oslanja na igre s kartama; mi se oslanjamo na **fizičku stvarnost**.
- 🃏 Kasino je otvoren za varanje; mi smo otvoreni za **transparentne dokaze**.
- ⏳ Kasino je privremeno; mi se fokusiramo na **vječnost umjetnosti i znanosti**.

**Token koji koristi ovaj protokol nije samo „coin"; to je digitalna dionica s znojem, bojom, kodom i filozofijom iza sebe.**

---

## 🗳️ 6) UPRAVLJANJE I JAVNI REGISTAR (Governance & Public Registry)

**Svrha ovog odjeljka je: Izvesti [PoArt] standard iz ravnine „povjerenja u ljude" i transformirati ga u održivu javnu infrastrukturu s registracijom + verifikacijom + nadzorom zajednice.**

### 6.1 Public Registry (Javni registar)

- **Public Registry:** Svi odobreni podaci bilježe se na `ilhanart.org/registry` (ili GitHub Registry).

**Logika registracije (predloženi standard - u JSON path formatu):**

Svaki zapis koji ulazi u registar nosi minimalno sljedeća provjerljiva temeljna polja:

- **Identitet i status:**
  - `certificate_id` (čitljiva referenca)
  - `status` (active / void)
  - `void_reason` (ako je primjenjivo)
  - `visibility` (private / masked / public)
  - `created_at` (vremenska oznaka)

- **Institucija izdavatelj:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informacije o djelu:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (ako je moguće; za identitet vlasnika tokena)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Forenzički podaci:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Kriptografski dokazi:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Upravljanje:**
  - `governance.decision`
  - `governance.review_notes`

Registar može imati dva sloja:
- **1)** Indeks čitljiv za ljude (web popis / pretraga / filter)
- **2)** Manifest čitljiv za strojeve (JSON zapisi; za PFE verifikaciju)

**„Registracija" ovdje postaje provjerljiva s lancem Evidence Pack → EvidenceRoot → NotarySeal PFE-a. Registar predstavlja cilj verifikacije, a ne „tvrdnju".**

---

### 6.2 Proces prijave za PoArt Verified

**Prijave za PoArt Verified ocjenjuje İlhanArt Gallery prema 5 PoArt standarda. Povratne informacije zajednice se uzimaju u obzir, ali konačna odluka ovisi o kuratorskom timu. Odluke se transparentno objavljuju i bilježe u ilhanart.org/registry.**

#### Proces prijave

**Prijava:**
- Umjetnik/projekt podnosi prijavu za PoArt Verified
- Evidence Pack se priprema (video snimke, metapodaci, linkovi na live prijenos)
- Prijava se šalje İlhanArt Gallery

**Pregled (30 dana):**
- Tim galerije detaljno pregledava Evidence Pack
- Provjeravaju se svih 5 PoArt standarda:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Intervju s umjetnikom (opcionalno)

**Konzultacija sa zajednicom:**
- Evidence Pack se javno dijeli tijekom procesa prijave
- Zajednica može davati povratne informacije putem ilhanart.org
- Vlasnici tokena (minimalno 10,000 $CULTURE) mogu posebno davati prijedloge
- **Sve povratne informacije uzimaju se u obzir tijekom procesa pregleda**
- **Ali konačna odluka temelji se na kuratorskoj procjeni**

**Odluka:**
- Galerija odobrava ili odbija prijavu
- Obrazloženje odluke se transparentno objavljuje
- Ako je odobrena → PoArt Verified značka
- Ako je odbijena → Može se ponovno prijaviti nakon 6 mjeseci

**Transparentnost:**
- Sve prijave i odluke bilježe se u ilhanart.org/registry
- Decision record se javno objavljuje:
  - Datum prijave
  - Sažetak procesa pregleda
  - Odluka (Approved / Rejected)
  - Obrazloženje odluke (kratko objašnjenje)
  - Sažetak povratnih informacija zajednice (anonimno)

#### Zašto kuratorska odluka?

**Kontrola kvalitete:**  
Status PoArt Verified je značka s visokim standardima. Kuratorska procjena jamči održavanje tih standarda.

**Sprječavanje spekulativne manipulacije:**  
Potpuno on-chain upravljanje (npr. Realms, DAO voting) s Pump.fun tokenima tehnički nije moguće. Off-chain sustavi glasovanja su otvoreni za manipulaciju kitova i koordinirane napade. Kuratorska odluka eliminira ovaj rizik.

**Operativna učinkovitost:**  
Brz i jasan proces donošenja odluka umjesto složenih mehanizama glasovanja. Umjetnici dobivaju rezultat u roku od 30 dana.

**Sudjelovanje zajednice:**  
Povratne informacije zajednice se u potpunosti uzimaju u obzir i utječu na proces donošenja odluka. Ali konačna odluka pripada kuratorskom timu zaštićenom od manipulacije.

**Budućnost:**  
Kada projekt sazrije (2027+), mehanizam konzultacija sa zajednicom može se ojačati. Ali kuratorska zaštita standarda ostaje trajna.

---

### 6.3 Token Utility (Područja korištenja tokena)

**Pogodnosti koje se pružaju vlasnicima $CULTURE tokena:**

**1. Prioritetni pristup događanjima u galeriji:**
- Pravo na izložbu od 1 tjedna godišnje u İlhanArt Gallery (pravo se može prenijeti)
- Popusti na drop painting
- Pravo na popust od 10% do 30% na slike u galeriji

**2. Puni pristup PoArt Registry:**
- Detaljni zapisi svih autentificiranih umjetničkih djela
- Pune verzije Evidence Pack-ova
- Alati za forenzičku verifikaciju

**3. Advisory Voting:**
- Pravo na savjetovanje u prijavama za PoArt Verified
- Pristup kanalima za povratne informacije zajednice
- Sudjelovanje u raspravama o upravljanju

**4. Exclusive Content:**
- Behind-the-scenes sadržaj iz studija
- Intervjui s umjetnicima i procesni videozapisi
- Pristup tehničkoj dokumentaciji

**Napomena:**  
Vlasnici tokena daju advisory vote (savjetodavni glas). Konačna odluka pripada kuratorskom timu. Ova struktura je odabrana kako bi se spriječila manipulacija kitova i spekulativni napadi. Nema staking nagrada jer tražimo dugoročne kulturne sudionike, a ne kratkoročni plaćenički kapital.

---

### 6.4 Metadata Sync (Usklađivanje s fizičkim svijetom)

- **Metadata Sync:** Tehnički podaci u registru moraju 100% odgovarati fizičkom sredstvu.

**Tehnička definicija „100% podudaranja" (predložena jasnoća):**

- **Minimalno podudaranje (obavezno):**
  - `asset.fingerprints.sha256/sha512` u registru mora biti **potpuno isto** kao hash datoteke u ruci.
  - `proof.notary_seal` u registru mora biti **potpuno isto** kada se regenerira (ako postoji Evidence Pack).

- **Podudaranje fizičke reference (tip dokaza):**
  - Dokazi poput fizičkog djela + referenca datuma/bloka prikazani u live prijenosu moraju biti dosljedni s Evidence Pack-om.

- **Usklađenost s privatnošću:**
  - Polja poput IP/lokacije u `masked` vidljivosti objavljuju se **prema standardu maskiranja**.

---

### 6.5 Osporavanje, pregled i poništenje (Dispute & Revocation)

Registar nije samo mehanizam „odobrenja"; to je **živi mehanizam nadzora protiv krivotvorenja**.

- Kada se pokrene osporavanje, zapis se može staviti u način **„review"**.
- Ako se otkrije krivotvorina, označava se kao `status: void` i dodaje se obrazloženje:
  - `void_reason` (korištenje AI-ja / ukradeno / manipulacija itd.)
  - `revoked_at` (vrijeme poništenja)
- Izvor odluke o poništenju jasno se prikazuje u registru:
  - kuratorski pregled / osporavanje zajednice / bilješka forenzičke analize (što je primjenjivo)

> **Ovaj dio je ekvivalent u registru koncepta VOID iz odjeljka „Red Flag Protocol".**

---

### 6.6 Primjer zapisa u registru (čitljiv za strojeve)
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

> *Napomena: `asset.fingerprints.sha512` i druge hash vrijednosti su skraćene u svrhu prikaza; u stvarnoj primjeni koriste se heksadecimalni znakovni nizovi pune duljine.*

---

## 7) 🔐 TEHNIČKI PEČAT (NOTARY SEAL)

**Nepokolebljiv algoritam pečata proizveden od strane PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Digitalni notar i protokol forenzičkih dokaza (Beta v1.0)

> **„Kultura je veća od kapitala. Zaštitite svoja djela od danas, prenesite ih u sutra."**

---

## Zašto je javno?

Prava sigurnost dolazi iz transparentnosti. Zahvaljujući našem sustavu **Public Registry (Javni registar)**, osoba bilo gdje u svijetu može u sekundama provjeriti je li datoteka u njenim rukama izvorna, bez potrebe za bilo kakvim autoritetom.

---

## 🧩 Zašto postoji više „modula vidljivosti"?

Najkritičniji dio koda je ovdje (izbornik za odabir vidljivosti). Ove opcije omogućuju korisnicima da balansiraju **„Privatnost vs. Transparentnost"**:

### 🔒 Privatno (Private)

- **Scenarij:** Umjetnik još ne želi objaviti djelo, ali želi staviti vremensku oznaku i dokazati „napravio sam ovo na ovaj datum".
- **Što kod radi:** Zapisuje podatke u bazu podataka, ali stavlja oznaku `visibility: "private"`. Kada kasnije napišeš „Public Read" politiku, možeš sakriti te zapise od javnosti govoreći `WHERE visibility = 'public'`.

### 🕶️ Maskirano (Masked)

- **Scenarij:** Umjetnik želi transparentnost, ali se boji da će kućna adresa (IP lokacija) biti otkrivena.
- **Što kod radi:** Funkcije `maskIP` i `maskLoc` rade na JavaScript strani. Pretvara IP adresu u format `88.241.***.***`, lokaciju u format `***/TR` i šalje cenzuriranu verziju u bazu podataka.
- **Napomena o privatnosti:** Maskiranje se vrši u pregledniku, Supabase ne vidi stvarnu lokaciju. **Međutim:** Ako se koriste API-ji trećih strana poput ipapi.co za podatke o lokaciji, ti pružatelji vide IP adresu u trenutku zahtjeva.
- **Pečaćenje u Masked načinu:** Izračun EvidenceRoot i NotarySeal vrši se s maskiranim forenzičkim podacima; tako verifikacija ostaje deterministička.

### 🌍 Javno (Public)

- **Scenarij:** Potpuna transparentnost. Prema [PoArt] standardu, otvoreno se izjavljuje gdje, kada i s koje mreže je djelo proizvedeno.

---

## 💡 Tehnološka inovacija

PoArt nije samo sustav za učitavanje datoteka. To je motor **„Forenzičkog lanca skrbništva" (Forensic Chain of Custody)** koji spaja tri različita tehnološka sloja u jedan lonac i uvodi novi standard.

**Sloj opisan kao „motor" u ovom odjeljku odgovara jezgri PoArt Forensic Engine (PFE) u prethodnoj terminologiji.**

### 1) Client-Side Hashing (Maksimalna privatnost)

Datoteke vaših djela nikada se ne učitavaju na poslužitelj. Naš motor koji radi u pregledniku (Client-side) izračunava hash (digitalni sažetak) datoteke na vašem vlastitom računalu. Na poslužitelj se šalje samo ovaj otisak i metapodaci.

> **Napomena o privatnosti:** Datoteka djela ne učitava se na poslužitelj i tako je zaštićena. Međutim, forenzički podaci (IP/lokacija) dijele se prema odabranom načinu vidljivosti (private/masked/public).

### 2) Forensic Data Fusion (Forenzička snaga)

Ovo je mnogo više od obične vremenske oznake (Timestamp). Sustav kombinira sljedeće podatke u jedan „Genesis pečat":

- **Digitalni sažetak (SHA-512):** Digitalni otisak koji koristi kriptografski standard sažetka (SHA-512), koji se kvari ako se promijeni čak i jedan piksel djela.
- **Lokacija i vrijeme:** Datum s milisekundnom preciznošću, država, grad i okrug kada je transakcija obavljena.
- **Identitet uređaja:** Operativni sustav, preglednik i tip uređaja (User-Agent analiza).

---

## 🛡️ Područja korištenja i prednosti

Ako ste umjetnik, pisac ili dizajner, nije dovoljno reći „Ja sam to već napravio", morate to dokazati.

**Djelo zapečaćeno s PoArt:**

- **Matematički dokaz:** Ako se promijeni čak i jedan piksel vaše datoteke, sustav to razumije. Manipulacija je nemoguća.
- **Pravna osnova:** Zabilježeno je na koji datum, u kojem gradu, s kojeg uređaja je djelo zapečaćeno.
- **Trenutni certifikat:** Proizvodi u sekundama jedinstveni za vas, s QR kodom i zapečaćeni **„Certifikat identiteta sredstva"**.

---

## ⚙️ Arhitektura sustava i tehničke specifikacije

Sustav je dizajniran na „Serverless" (Bez poslužitelja) arhitekturi, fokusirano na visoke performanse i skalabilnost.

| Sloj | Tehnologija | Opis |
|------|-------------|------|
| **Kriptografija** | SHA-256 & SHA-512 | Dvoslojni kriptografski sažetak |
| **Baza podataka** | Supabase (PostgreSQL) | JSONB struktura podataka, RLS politike |
| **Forenzički podaci** | ipapi.co API | IP/Lokacija/Vrijeme trojka |
| **Renderiranje** | html2canvas + jsPDF | Client-side PNG/PDF proizvodnja |
| **Frontend** | Vanilla JavaScript | Nula framework ovisnosti |
| **Sigurnost** | Client-side hashiranje | Datoteka se nikada ne učitava na poslužitelj |

### Istaknute značajke

| Značajka | Detalj | Kod konkurenata? |
|----------|--------|------------------|
| **Drag & Drop UI** | Povuci i ispusti datoteku, trenutni pregled | ❌ Nedostaje u većini |
| **Multi-Format Export** | PNG, JSON, PDF - jednim klikom | ⚠️ Ograničeno |
| **Real-Time Preview** | Pregled certifikata uživo | ❌ Nedostaje |
| **Privacy Controls** | Private/Masked/Public opcije | ❌ Nedostaje |
| **Client-Side Hashing** | Datoteka nikada ne ide na poslužitelj | ✅ Samo u nekoliko |
| **Forensic Metadata** | IP, lokacija, uređaj, vrijeme - sve zajedno | ❌ Djelomično |
| **QR Verification** | Trenutni QR kod za verifikaciju | ⚠️ Ograničeno |
| **Rate Limiting** | Zaštita od spama (RLS + Client) | ❌ Nedostaje u većini |

---

## 🗺️ Putokaz: „Trustless" budućnost

Trenutna verzija **(Beta v1.0)** optimizirana je za pružanje krajnjem korisniku maksimalne brzine, jednostavnog sučelja i besplatnog pristupa. Međutim, naša krajnja vizija je prijelaz na strukturu u kojoj čak ni administrator baze podataka (mi) ne može intervenirati.

### Faza 1: Beta v1.0 (Trenutno uživo)

**Infrastruktura:**
- Cloud Database (Supabase)
- Off-chain registar (PostgreSQL + IPFS backup)
- Gallery self-attestation (centralizirano ali transparentno)

**Token:**
- Platforma: Pump.fun
- Likvidnost: Raydium (automatska)
- Upravljanje: Samo savjetodavno (konzultacija zajednice)

**Cilj:**
- Brzina, uklanjanje UX barijera
- Pružanje „beskontaktne" sigurnosti
- Izgradnja zajednice

**Token Utility (v1.0):**
- Prioritetni pristup događanjima u galeriji
- Pregled PoArt Registry
- Pravo savjetodavnog glasovanja

---

### 🚀 Faza 2: Decentralized Authority (2026 Q2-Q4)

Ova faza pokriva prijelaz sustava iz potpuno „Client-Side" radne strukture u sigurniju i decentraliziraniju strukturu.

| Značajka | Što dobivamo? | Tech Stack | Rok |
|----------|---------------|------------|-----|
| **Edge Function INSERT** | Blokiranje spama + sigurnost API Key-a | Supabase Edge (Deno) | Q2 2026 |
| **Wallet potpis** | Decentralizirani identitet | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | Decentralizirani arhiv | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | Poništenje lažnog certifikata | DB Schema Update | Q2 2026 |
| **Audit Log** | Forenzički log upita | Custom logs tablica | Q3 2026 |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain glasovanje (x/web) + wallet potpis
- Izbor predstavnika zajednice (prvih 90 dana)
- Multi-sig kontrola operativnog novčanika
- Ponderirano savjetodavno glasovanje (s whale ograničenjem)

**Nepromjenjivost:**
- Registry backup s IPFS hashevima
- Bitcoin timestamp anchoring
- Priprema za cross-chain verifikaciju

---

### Faza 3: Potpuna decentralizacija (2027+)

| Značajka | Cilj | Rok |
|----------|------|-----|
| **On-Chain Registry** | Solana on-chain registracija | Q1 2027 |
| **Enhanced Token Utility** | NFT mint, napredne značajke | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **DID Integration** | Decentralizirani identitet | Q3 2027 |
| **Community Governance** | Ojačani savjetodavni sustav | Q4 2027 |
| **Legal Recognition** | Valjanost na turskim sudovima | 2027-2028 |
| **API for Developers** | Javna API krajnja točka | Q3 2027 |

**Evolucija upravljanja:**
- v3.0: Hibridni model (kuratorski + ponderiran od zajednice)
- 2028+: Potpuno upravljanje zajednice (opcionalno)
- Kuratorska kontrola kvalitete uvijek se čuva

---

## 🧬 Struktura podataka protokola (JSON Schema)

**Svaki [PoArt] certifikat ima prenosivu i provjerljivu JSON identifikacijsku karticu proizvedenu prema standardu ispod.**

> **Napomena:** Ovaj Identity JSON format je format certifikata predstavljen korisniku. U zapisima registra koristi se `registry.asset` umjesto `identity.asset_data` (mapiranje: `identity.asset_data` == `registry.asset`).
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

## 🔬 Tehnička dubina: Algoritam pečata

### Determinističke hash funkcije
```javascript
// Pomoćne funkcije: Pretvori digest u hex string
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Pretvori string u byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Proizvodnja kanoničkog forensics stringa (v1.0: fiksni redoslijed polja + UTF-8 + \n delimiter)
// Napomena za Fazu 2: Prijelaz na kanonički JSON s RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Proces proizvodnje NotarySeal (Potpuno deterministički)
```javascript
// 1. Izračun FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Prikupljanje forensic podataka (korištenje jedne vremenske oznake)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Proizvodnja jedne vremenske oznake
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

// 3. Kreiranje EvidenceRoot (s canonical encoding-om)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Proizvodnja NotarySeal (korištenje iste vremenske oznake)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Pomoćne funkcije za maskiranje (podrška za IPv4 i IPv6)
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

### Tok verifikacije (Dvije razine)

#### Quick Verify (Brza verifikacija)
```javascript
// Provjerava samo hash datoteke (brza crvena zastava)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Dohvati iz Registry-ja
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Usporedba hasheva
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

#### Full Verify (Potpuna verifikacija)
```javascript
// Ponovno stvara i verificira EvidenceRoot i NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Dohvati iz Registry-ja
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash provjera (brza crvena zastava)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Lažno - Hash datoteke se ne podudara" };
  }

  // 2) Ponovno stvori EvidenceRoot (s forensics pohranjenim u registry)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Ne podudara se - EvidenceRoot ne odgovara" };
  }

  // 3) Ponovno stvori NotarySeal (s istom vremenskom oznakom + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Ne podudara se - NotarySeal ne odgovara" };
  }

  // Opcionalno: U Fazi 2 verificiraj signer_sig i s attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Nevažeći potpis" };

  return { valid: true, message: "✅ Original - Full Verify prošao" };
}
```

> **Važne napomene:**
> - **Quick Verify:** Provjerava samo hash datoteke za brzu upotrebu.
> - **Full Verify:** Verificira sve slojeve protokola (EvidenceRoot + NotarySeal).
> - Sve hash operacije izvode se deterministički s fiksnim kodiranjem i delimiterima.
> - **v1.0 standard kanonizacije:** Fiksni redoslijed polja + UTF-8 kodiranje + `\n` delimiter.
> - **Plan za Fazu 2:** Prijelaz na kanonički JSON s RFC 8785 (JCS - JSON Canonicalization Scheme).
> - U masked načinu, izračun EvidenceRoot i NotarySeal vrši se s maskiranim forensics.
> - Jedna vremenska oznaka koristi se kroz cijeli proces (forensics + NotarySeal); determinizam je zajamčen.
> - **Nazivi forensics polja:** `ip_masked`, `location`, `device`, `timestamp` (kod i registry potpuno kompatibilni).
> - **Putanja u Registry:** `certificate.asset.fingerprints` (potpuno kompatibilna s kodom za verifikaciju).
> - **signer_sig u Registry:** Polje `proof.signer_sig` potrebno je za Full Verify.
> - Mehanizam SignerSignature bit će aktiviran u Fazi 2 sa Solana Wallet Adapterom; u v1.0 verifikacija se može izvršiti s `attestation_pubkey`.

---

## 📊 Analiza konkurencije (Ažurirano)

PoArt se pozicionira na „Sweet Spot" (Naidealnija točka) koji nadopunjuje nedostatke postojećih rješenja.

| Značajka | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|----------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Cijena** | 🆓 Besplatno | 🆓 | 💰 Plaćeno | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Vrlo lako | ❌ CLI | ⚠️ Srednje | ⚠️ Srednje | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Uživo | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 načina | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privatnost | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Potpuno | ❌ | ❌ | ⚠️ Ograničeno | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Trenutno | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Putokaz | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Turkish Support** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Legenda:**
- ✅ : Puna podrška / dostupno
- ⚠️ : Ograničeno / u plaćenim planovima
- ❌ : Nedostaje / nije podržano
- 🔄 : U putokazu (u razvoju)
- 🆓 : Potpuno besplatno
- 💰 : Plaćeno / potrebna pretplata

### Nedostaci konkurenata, snage PoArt-a

| Nedostatak | Konkurenti | PoArt |
|------------|-----------|-------|
| **Poteškoće u korištenju** | CLI, potrebno API znanje, novčanik | Povuci i ispusti, gotovo s 3 klika |
| **Barijera cijene** | $50-500/mjesec pretplata | 100% besplatno |
| **Privatnost** | Datoteka se učitava na poslužitelj | Client-side, datoteka nikada ne ide |
| **Forensic podaci** | Samo vremenska oznaka | IP, lokacija, uređaj, vrijeme - sve |
| **Hrvatski Support** | Nedostaje ili vrlo ograničeno | Profesionalna lokalizacija |
| **Otvoreni kod** | Zatvorena kutija | Sav kod otvoren na GitHub-u |

---

## 📈 Statistika korištenja (Ciljevi za 2026 Q1)

| Metrika | Cilj | Status |
|---------|------|--------|
| **Ukupno certifikata** | 1,000 | 🔄 U tijeku |
| **Aktivni korisnici** | 500 | 🔄 U tijeku |
| **Broj verifikacija** | 5,000 | 🔄 U tijeku |
| **Uptime** | 99.9% | ✅ Aktivno |
| **Avg Response Time** | <200ms | ✅ Optimalno |

---

## 🌍 Zajednica i podrška

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Suradnici

PoArt protokol nastavlja se razvijati s doprinosima zajednice otvorenog koda.

**Za doprinos:**
1. Napravi fork
2. Kreiraj feature branch (`git checkout -b feature/amazing-feature`)
3. Napravi commit (`git commit -m 'Add amazing feature'`)
4. Napravi push (`git push origin feature/amazing-feature`)
5. Otvori Pull Request

### 🛠️ Što nam trenutno treba? (Poziv za pomoć)

Razvoj PoArt Protocol **Faze 2** očekuje doprinose iskusnih programera u sljedećim područjima:

* **Supabase Edge Functions:** Premještanje zaštite od spama na stranu poslužitelja.
* **Solana Web3.js:** Integracija Wallet Signing.
* **IPFS / Arweave:** Integracija usluga arhiviranja i pinning.
* **Community Tools:** X glasovanje, voting systems, analytics dashboard.

> Molimo započnite raspravu u kartici „Issues" prije dodavanja značajke.

---

## 💬 Završne napomene

### Pump.fun i stvarnost

Ovaj projekt je pokrenut na Pump.fun jer:
- ✅ Pristup likvidnosti (Raydium automatic migration)
- ✅ Pristup postojećoj zajednici
- ✅ Niski početni troškovi

Ali razjasnimo ovo:
- **Cijena tokena** nije pokazatelj umjetničkog uspjeha
- **Operativni budžet** zahtijeva vrijednost tokena (galerija, izložbe, infrastruktura)
- **Metrike uspjeha:** Authenticated artworks + community engagement + fizički posjetitelji

### Upravljanje i decentralizacija

**v1.0 Stvarnost (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (centralizirano ali transparentno)
- Governance: Samo savjetodavno (kuratorska konačna odluka)
- Token utility: Gallery access + registry + NFT priority

**v2.0+ Vizija (2027+):**
- Registry: On-chain (Solana)
- Potpisi: Bazirani na Wallet-u (decentralizirano)
- Governance: Hibridno (community advisory + curatorial quality)
- Token utility: Poboljšane značajke + napredni pristup

Ova struktura pruža **operativnu učinkovitost** i **kontrolu kvalitete** u ranoj fazi, dok drži put otvoren za **povećanje sudjelovanja zajednice** u budućnosti.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Kultura je veća od kapitala*

## 🧾 Licenca

MIT License © 2026 İlhan Art Gallery Initiative

Vidi [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) za potpune uvjete.

---

## 💬 Zahvale

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Ovaj projekt je razvijen od strane inicijative [İlhan Art Gallery], a izvorni kodovi su otvoreni javnosti u ime transparentnosti.**

**PROTOKOL V1.0 // ZAPEČAĆENO S SHA-512.**

*© 2026 İLHAN ART | SVA PRAVA NA DJELA, SLIKE I IDEJE SU ZADRŽANA.*

---
