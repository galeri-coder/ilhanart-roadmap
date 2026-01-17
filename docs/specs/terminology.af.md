# 📚 TERMINOLOGIE & KONSEPTE WOORDELYS
> **"Om die taal van hierdie protokol te verstaan, is om sy visie te verstaan."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Kern-infrastruktuur

**PoArt Forensic Engine (PFE)** is die hooflaag wat die kernlogika en tegniese werking agter die [PoArt]-protokol verteenwoordig. Dit is die "forensiese enjin" wat die rou produksiedata van 'n kunswerk neem en dit omskep in **digitale bewyse** wat verifieerbaar en onveranderlik is.

### 🧩 Waarom "PoArt Forensic"?

- **PoArt (Proof of Art / Bewys van Kuns):** Die fokus van die enjin is om die waarde van 'n digitale bate nie aan spekulasie te koppel nie; maar aan 'n **verifieerbare produksieproses**.
- **Forensic (Forensiese Verifikasie):**
  - **Tegniese Definisie:** 'n Algoritme en rekordkettingbenadering wat verifieer dat data wat verband hou met die produksieproses (kwasstrepe, timelapse, logs) nie gemanipuleer is nie.
  - **Filosofiese Laag:** Teen die "onmiddellike uitset" produksie van kunsmatige intelligensie; die aanspraak om **menslike tyd, inspanning en besluitnemingskoste** om te skakel na 'n meetbare werklikheid.

> Let wel: Blockchain-integrasie (bv. Solana) is nie die kern van PFE nie; dit word as 'n aparte **Chain Anchor Layer** vir verifikasie/registrasie hanteer.

### 🛠️ v1.0 Tegniese Omvang

**PoArt Forensic Engine (PFE) v1.0** is gebou op die volgende **3 hoofpilare** in plaas van komplekse finansiële modelle:

1. **Hashing & Sealing (Verseëling):**  
   PFE verwerk alle items in die Evidence Pack (kunswerkslêer, video, JSON/log, handtekening, ens.) deterministies en produseer 'n unieke **NotarySeal**-waarde.

   **Kernkonsepte (v1.0):**
   - **FileHash (kunswerk vingerafdruk):** Hash gegenereer uit die bytes van die kunswerkslêer.
   - **EvidenceRoot (bewyspakketwortel):** Wortelopsomming wat die integriteit van die Evidence Pack verteenwoordig (Merkle-wortel of kanonieke manifest-hash).
   - **NotarySeal (finale seël / PFE Uitset):** Finale seël geproduseer uit die kombinasie van EvidenceRoot + tyd + handtekening.

   **Formules (duidelik sigbaar vir beleggers):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload Definisies (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Let wel: Die waarde wat as PFE-uitset bedoel word, is **NotarySeal**. Die **SignerSignature**-meganisme sal in Fase 2 (met Solana Wallet Adapter) geaktiveer word; in die huidige v1.0 word die stelsel se eie attestasie-handtekening gebruik. Die attestasie publieke sleutel word in die register gepubliseer in die `issuer.attestation_pubkey`-veld.

2. **Indexing (Argivering):**  
   Rekordeer watter beursie, op watter datum, **Labor Proof (Arbeidsbewys)** vir watter kunswerk voorgelê het; in 'n deursigtige en navraagbare rekordlaag.  
   *(Hierdie laag kan 'n databasis wees; kettingintegrasie word apart as "Chain Anchor Layer" gedefinieer.)*

3. **Verification (Verifikasie):**  
   Wanneer die oorspronklikheid van 'n kunswerk bevraagteken word, herverwerk PFE die rou bewyse; toets met wiskundige sekerheid of die berekende **EvidenceRoot / NotarySeal**-waardes ooreenstem met die rekord in die argief.

---

### 🧮 PoArt Waarde Stelling (The Value Theorem)

Die [PoArt]-protokol koppel die waarde van 'n digitale bate ($V$) nie aan subjektiewe markpersepsie nie; maar aan die **fisiese werklikheid van die produksieproses**.

Kunsmatige Intelligensie (AI), deur die resultaat onmiddellik te lewer ($t \to 0$), vernietig die proses. [PoArt] hanteer waarde as; die akkumulasie van **tyd, arbeid en wil** komponente.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definisie van Veranderlikes

- **$\int dt$ (Prosesakkumulasie):**  
  Waarde is nie 'n onmiddellike "uitset" (output) nie; dit is 'n **proses** wat tussen $t_{\text{start}}$ en $t_{\text{end}}$ akkumuleer. Soos die tyd afneem (AI-produksie), nader die resultaat van die integraal 0.

- **$P_{\text{labor}}(t)$ (Oombliklike Arbeidskrag):**  
  Verteenwoordig die intensiteit van geestelike en fisiese inspanning wat tydens produksie spandeer word. Soos bewysbare inspanning toeneem, groei die integrand.  
  > Let wel: Hierdie term kan in die praktyk genormaliseer word deur "meetbare/bewysbare arbeidseine".

- **$I_{\text{agency}}(t)$ (Wilskoëffisiënt):**  
  Die produsent se vermoë om risiko te neem en besluite te neem. Dit neem 'n waarde tussen $0$ en $1$ aan.
  - **AI ($I \approx 0$):** Voer opdragte uit, neem nie risiko nie, betaal nie 'n prys nie.
  - **Mens ($I \to 1$):** Verander besluite, huiwer, neem risiko.

- **$U_{\text{irreversible}}$ (Onomkeerbare Uniekheid):**  
  In digitale produksie is terugdraai (`Ctrl+Z`) moontlik; maar in fisiese produksie (verf op doek, gebeeldhoupte marmer, gebare in lewende uitsending) is daar geen terugkeer nie. Hierdie **onomkeerbaarheid** is 'n bykomende term wat "uniekheid" (nie-fungibele karakter) in die kunswerk skep.

### 🔎 Gevallestudie: AI "Onmiddellike Uitset" vs. Mens "Bewese Proses"

Die volgende scenario toon hoe die **PoArt Waarde Stelling** in die praktyk werk en waarom AI-produksies lae tellings in die [PoArt]-standaard kry.

#### Scenario A: Beeldproduksie met AI in 10 Sekondes

- **Tyd ($\Delta t$):** $10$ sekondes (feitlik geen proses nie)
- **Arbeidskrag ($P_{\text{labor}}$):** $1$ eenheid (slegs opdrag skryf)
- **Wilskoëffisiënt ($I_{\text{agency}}$):** $0.01$ (geen risiko, geen prys)
- **Onomkeerbaarheid ($U_{\text{irreversible}}$):** $0$ (omkeerbaar / kopieerbaar)

**Resultaat:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Kommentaar:** Selfs al is die uitset perfek; omdat die proses nie beleef is nie en dit nie wil/risiko bevat nie, nader die [PoArt]-waarde $0$.

#### Scenario B: 6-Uur Fisiese Produksie in Lewende Uitsending

- **Tyd ($\Delta t$):** $6$ ure ($21{,}600$ sekondes)
- **Arbeidskrag ($P_{\text{labor}}$):** $0.5$ eenhede (kontinuïteit van fisiese en geestelike inspanning)
- **Wilskoëffisiënt ($I_{\text{agency}}$):** $0.9$ (besluitverandering, risiko-neming, onomkeerbare keuses)
- **Onomkeerbaarheid ($U_{\text{irreversible}}$):** $>0$ (fisiese spore kan nie teruggedraai word nie)

**Resultaat:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Kommentaar:** Soos die proses langer word en wil (risiko) toeneem, neem waarde kumulatief toe. Die $U_{\text{irreversible}}$-term is 'n bykomende bydrae wat "uniekheid" (nie-fungibele karakter) in die kunswerk skep.

---

### ✅ Gevolgtrekking: Waarde Gesluit met Bewys (Proof-Bound Value)

Hierdie stelling neem die [PoArt] waarde-aanspraak uit 'n "voorkeur" of "marknarratief" en koppel dit aan 'n **bewysbare produksiewerklikheid**.

1. **Geen Waarde Sonder Proses:**  
   AI vernietig die proses in onmiddellike uitset ($t \to 0$). Soos die prosesvenster vernou, verklein die resultaat van die integraal met wiskundige noodsaaklikheid:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Wil en Risiko is Vermenigvuldigers:**  
   [PoArt] meet nie net "tyd spandeer" nie; dit meet ook die werklike besluit, risiko en pryslaag in daardie tyd. Die waarde van produksie wat nie risiko neem nie (AI) is laag:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Uniekheid is nie Bemarking nie, maar Fisiese Bewys:**  
   In fisiese produksie is onomkeerbare spore (doekslag, marmerbreuk) buite die `Ctrl+Z`-logika van digitaal. Hierdie onomkeerbaarheid ($U_{\text{irreversible}}$) maak die kunswerk ontologies uniek.

> **🔐 OPSOMMING:** Selfs al lyk die waardestelling onduidelik as meting (selfs al kan dit nie 100% in werklike lewe gemeet word nie), is die doel van hierdie formule om die konstruksie en rigting van veranderlikes te wys. Wat skaars is in die AI-era is nie "beeld" nie; **bewysbare arbeid, tyd en wil**. [PoArt] meet hierdie skaarsheid en registreer dit met **Evidence Pack**.

### 🏛️ Die Belangrikheid van die "Engine" (Enjin) Konsep

Tokens wat uit Pump.fun of soortgelyke platforms kom, is dikwels net **"toegangskaartjies"**. **PoArt Forensic Engine (PFE)** is egter die **konstitusionele logiese laag** wat bepaal watter regte daardie kaartjie beskerm, hoe arbeid geregistreer word en hoe kuns/wetenskap/tegnologie permanent gemaak word.

> **Let wel:** Die rede waarom ons hierdie projek op Pump.fun begin het, is omdat ons nie genoeg likiditeit en volgelinge gehad het nie. Alhoewel die gebruik van bestaande data strategies nie die beste kwaliteit was nie, kan ons sê dit was die regte skuif. Ongeag begroting en geleenthede, die definisie van die logika van hierdie enjin op GitHub bewys dat die projek nie net finansiële spekulasie is nie, maar 'n langtermyn **sagteware-infrastruktuur** en visie van 'n **digitale nasionale biblioteek**.

---

## 🎨 [PoArt] ARBEIDSBEWYS PROTOKOL (Proof of Art Protocol v1.0)

> **"Werklike Kunstenaar, Werklike Produksie, Werklike Waarde."**

Hierdie protokol is 'n **biologiese en intellektuele verdedigingsmeganisme** ontwikkel teen anonieme bedrieërs wat die kripto-ekosisteem omring, kunsmatige intelligensie-beelde wat in 5 minute geproduseer word en die "Pump & Dump"-kultuur.

---

## a) Wat is [PoArt]? (Filosofiese en Tegniese Definisie)

**Proof of Art [PoArt];** is 'n institusionele verifikasiestandaard wat waarborg dat die waarde agter 'n bate op die blockchain gebaseer is op verifieerbare **menslike arbeid**, **tyd** en **fisiese energie**, nie spekulasie nie.

Net soos Bitcoin waarde produseer met *"Elektrisiteit en Verwerkerkrag"* **(Proof of Work)**; produseer [PoArt]-verenigbare projekte ook waarde met *"Gespandeerde Talent en Menslike Tyd"*. Dit "Stake" tyd.

Dit elimineer die *"Ontwikkelaar (Dev) het verkoop, projek is verby"* risiko op Pump.fun en DEX-platforms; omdat waarde hier nie in kode is nie, dit is versteek in die **kontinuïteit van produksie**.

> **[PoArt] sê nie aan sy deelnemer "Vertrou ons" nie; dit sê "Hier is die bewyse, sien met jou oë, verifieer met jou wiskunde".**

---

## b) [PoArt] 5-Pilaar Standaard (The 5 Pillars of Truth)

Hierdie 5 items is onmanipuleerbare filters wat 'n projek moet deurgaan om die [PoArt]-seël te ontvang.

### 1) Lewende Identiteitsbewys (Live Identity Proof)

- **Probleem:** Die kripto-wêreld is vol anonieme stigters (Devs) wat geld insamel en die projek verlaat.
- **[PoArt] Oplossing:** Die produsent bewys nie net sy identiteitskaart nie, maar ook **sy teenwoordigheid tydens produksie**. Dit sluit lewende uitsendingsessies in waar daar interaksie met die gemeenskap is en oombliklike spesifieke versoeke vervul word, nie vooraf opgenome video's nie.  
  (Bv: *"Skryf vandag se datum en huidige bloknommer in die regterhoek van die doek"*)
- **Leuse:** *"Bots kan skilder maar bots sweet nie en kan nie improviseer nie."*

### 2) Arbeids- en Prosesbewys (Labor & Process Proof)

- **Probleem:** AI-beelde wat in 2 sekondes geproduseer word en olieverfskilderye wat in 2 maande gemaak word, word dieselfde "jpeg"-behandeling in die digitale wêreld gegee.
- **[PoArt] Oplossing:** Die "swangerskap en geboorte" proses van die kunswerk word geregistreer. Skets fases, verflaë, kumulatiewe ure spandeer en die fisiese proses wat die kunstenaar deurgegaan het tydens die skepping van daardie kunswerk word gedokumenteer. Dit voeg **"Tydkoste" (Time Cost)** by die token. Hoe moeiliker die produksie van 'n bate, hoe stewiger sy waarde.

### 3) Estetiese Waardebewys (Aesthetic Value Proof)

- **Probleem:** Die "Meme"-kultuur wat estetika en artistieke diepte ignoreer en net op oombliklike komedie fokus en die kortstondige "Hype"-projekte wat daaruit voortspruit.
- **[PoArt] Oplossing:** Die projek moet akademiese kunsstandaarde, kleurteorie, komposisiereëls en materiaalkennis (Impasto, Tekstuur, ens.) hê. Inhoud moet nie net lag maak nie; dit moet bewondering by die kyker wek en **versamelingwaarde** hê.

### 4) Konseptuele Innovasie (Conceptual Novelty)

- **Probleem:** Duisende hond/kat-munte wat mekaar kopieer, ver van kreatiwiteit.
- **[PoArt] Oplossing:** Die projek moet 'n nuwe brug bou wat kuns, wetenskap, filosofie of tegnologie in 'n betekenisvolle struktuur kombineer.  
  (Bv: Die klassieke Dawid-beeld met kripto-markdata kombineer; die idee van menslike persepsie wat "in klip verander" daaruit werk en dit met wetenskaplike bronne kan begrond.)  
  Die kunswerk moet nie net 'n visuele fees wees nie; dit moet ook 'n intellektuele uitdaging wees wat laat nadink oor **Wetenskap, Filosofie of Tegnologie**.

> [!IMPORTANT]
> **Verwysingsvoorbeeld (Las Palmitas Effek):**  
> In die Las Palmitas-woonbuurt in Mexiko wat met misdaad gesukkel het, is meer as 200 huise omskep in 'n reuse reënboogfees. As gevolg van hierdie estetiese ingryping het misdaadsyfers in die woonbuurt tot 'n sekere mate gedaal, en jongmense het begin belangstel in kuns in plaas van bendes. Die estetiese verandering het mense se respek vir hul omgewing en mekaar (Social Cohesion) herkodeer.
>
> **Verwagting:** 'n Projek wat op die [PoArt]-lys wil kom; moet, soos die voorbeeld hierbo, 'n sosiologiese, wetenskaplike of filosofiese oorsaak-gevolg-verhouding bevat bo en behalwe blote visuele estetika. Omdat "Tyd" die enigste bate is wat nie met geld gekoop kan word nie, moet tyd in hierdie protokol as waarborg gestake word en bewys word. Die intellektuele basis van die projek moet so sterk en universeel wees dat; selfs in 'n moontlike CTO (Community Take Over) scenario jare later, die gemeenskap hierdie erfenis kan oorneem en die projek se innoverende potensiaal outonoom kan voortsit.

### 5) Nie-Algoritmiese Wil (Non-Algorithmic Agency)

- **Probleem:** Perfekte maar siellose, herhalende digitale produksies.
- **[PoArt] Oplossing:** Die unieke wil van die mens wat foute kan maak, risiko neem en emosionele skommelinge ervaar, moet in die kunswerk gevoel word. Die onsekerheid in kwasstrepe, die onverwagte reaksies van materiaal en die oombliklike besluite van die kunstenaar is die **Biologiese Handtekening** wat die kunswerk van "Masjien Produksie" onderskei.

---

## c) Verifikasie & Anti-Vervalsing Meganisme

Hierdie stelsel verseker dat die projek nie net "aan die begin" nie, maar "vir ewig" betroubaar en lewend bly.

### 📦 Bewyspakket (Evidence Pack - The Digital Twin)

Agter elke [PoArt]-gesertifiseerde kunswerk is daar 'n geënkripteerde en tydgestempelde datapakket wat beleggers kan aflaai:

- **RAW Video-opnames:** Ononderbroke rou beelde van die produksieoomblik.
- **Metadata-analise:** Lêerskeppingsdatum, gebruikte toestelinligting en liggingdata (Stad-Land).
- **Fisiese Verwysings:** Bewyse dat die kunswerk in die fisiese wêreld bestaan  
  (Bv: Huidige koerant of daardie oomblik se blockchain-data langs die kunswerk).

> *Konsekwentheidsnota:* Die uitdrukking "bewyspakket" koppel aan die **Evidence Pack → EvidenceRoot → NotarySeal**-lyn in vorige afdelings; dit wil sê die integriteit van die pakket word verteenwoordig deur 'n verifieerbare seël.

### 🔄 365-Dae Hernuwing (The Sustainability Protocol)

- **Revolusionêre Kenmerk:** In kripto-projekte stel die "Dev" (Ontwikkelaar) die token in die mark bekend en verdwyn gewoonlik 1-2 maande later (Soft Rug). [PoArt] maak dit onmoontlik.
- **Reël:** "Verified Artist" (Geverifieerde Kunstenaar) status is nie lewenslank nie. Dit is slegs vir **1 jaar** geldig.
- **Werking:** Die kunstenaar/ontwikkelaar moet elke 365 dae 'n **nuwe, groot en bewysbare kunswerk** aan die gemeenskap voorlê.
- **Voorbeeldscenario:** Jy het die projek in 2026 begin. In Januarie 2027 gee die stelsel 'n "Bewystydperk Verstreke" waarskuwing. As die kunstenaar nie 'n nuwe uitstalling, nuwe fisiese kunswerk of nuwe tegnologiese integrasie aanbied nie, val die projek se "Vertrouenswapen" af.
- **Resultaat:** Hierdie stelsel verseker dat **inhoud nooit verouderd raak nie** en dat die belegger nie die vrees van *"Is die ontwikkelaar nog hier?"* ervaar nie. Die projek word 'n lewende ateljee.

### 🚩 Rooi Vlag (Red Flag Protocol)

**In die geval van enige vervalsing (AI-gebruik, gesteelde kunswerk, gemanipuleerde video) wat deur die gemeenskap of algoritmes opgespoor word:**

1. Die sertifikaat word onmiddellik gemerk as **"NIETIG" (VOID)**.
2. Bewyspakkette word openlik gemerk as **"Vals"**.
3. Die projek word op die [PoArt]-swartlys geplaas. Dit versterk die werklikheid dat **reputasie die enigste geldeenheid** in 'n gedesentraliseerde wêreld is.
4. [PoArt]-uitdrukkings kan nie in enige publikasie ingesluit word nie, die enigste geldige bron is https://www.ilhanart.org/public-registry

---

## d) Gevolgtrekking: Museum, Nie Casino Nie

**Pump.fun en Gedesentraliseerde Beurse (DEX) is ongelukkig tans casino's; ligte flikker, almal jaag vinnige wins na en die huis (bedrieërs) wen altyd. Die rede waarom ons die projek hier begin het, is ook omdat ons probeer om dit hier te verbeter en omdat ons die data en lewende uitsendings het om die huidige gehoor te bereik.**

**[PoArt] is 'n kasteel gebou in die middel van hierdie casino.**

- 🎰 Die casino is gebaseer op kaartspeletjies; ons is gebaseer op **fisiese werklikheid**.
- 🃏 Die casino is oop vir bedrog; ons is oop vir **deursigtige bewyse**.
- ⏳ Die casino is tydelik; ons fokus op die **ewigheid van kuns en wetenskap**.

**'n Token wat hierdie protokol gebruik, is nie net 'n "munt" nie; dit is 'n digitale aandeel met sweet, verf, kode en filosofie daaragter.**

---

## 🗳️ 6) BESTUUR & OPENBARE REGISTER (Governance & Public Registry)

**Die doel van hierdie afdeling is: Om die [PoArt]-standaard uit die vlak van "vertrou mense" te neem en dit om te skakel na 'n volhoubare openbare infrastruktuur met registrasie + verifikasie + gemeenskapstoesig.**

### 6.1 Public Registry (Openbare Register)

- **Public Registry:** Alle goedgekeurde data word geregistreer by `ilhanart.org/registry` (of GitHub Registry).

**Registrasielogika (voorgestelde standaard - in JSON-padformaat):**

Elke rekord wat die register binnegaan, dra ten minste die volgende verifieerbare kernvelde:

- **Identiteit & Status:**
  - `certificate_id` (leesbare verwysing)
  - `status` (active / void)
  - `void_reason` (indien enige)
  - `visibility` (private / masked / public)
  - `created_at` (tydstempel)

- **Uitreikende Instelling:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Kunswerkinligting:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (indien moontlik; vir token-houer identifikasie)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Forensiese Data:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Kriptografiese Bewyse:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Bestuur:**
  - `governance.decision`
  - `governance.review_notes`

Die register kan twee lae hê:
- **1)** Mens-leesbare indeks (weblys / soek / filter)
- **2)** Masjien-leesbare manifest (JSON-rekords; vir PFE-verifikasie)

**Die "registrasie" hier word verifieerbaar met PFE se Evidence Pack → EvidenceRoot → NotarySeal-ketting. Die register bied nie 'n "aanspraak" nie, maar 'n verifikasiedoelwit.**

---

### 6.2 PoArt Verified Aansoekproses

**PoArt Verified-aansoeke word deur İlhanArt Gallery geëvalueer volgens die 5 PoArt-standaarde. Gemeenskapsterugvoer word in ag geneem, maar die finale besluit berus by die kuratorspan. Besluite word deursigtig aangekondig en geregistreer by ilhanart.org/registry.**

#### Aansoekproses

**Aansoek:**
- Kunstenaar/projek dien PoArt Verified-aansoek in
- Evidence Pack word voorberei (video-opnames, metadata, lewende uitsendingskakels)
- Aansoek word aan İlhanArt Gallery gestuur

**Hersiening (30 Dae):**
- Galeryspan hersien Evidence Pack in detail
- Alle 5 PoArt-standaarde word nagegaan:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Onderhoud met kunstenaar (opsioneel)

**Gemeenskapskonsultasie:**
- Evidence Pack word openlik gedeel tydens die aansoekproses
- Gemeenskap kan terugvoer gee via ilhanart.org
- Token-houers (minimum 10,000 $CULTURE) kan veral voorstelle maak
- **Alle terugvoer word tydens die hersieningsproses in ag geneem**
- **Die finale besluit berus egter op kuratoriale evaluering**

**Besluit:**
- Galery keur die aansoek goed of keur dit af
- Besluitrede word deursigtig aangekondig
- Indien goedgekeur → PoArt Verified badge
- Indien afgekeur → Kan ná 6 maande weer aansoek doen

**Deursigtigheid:**
- Alle aansoeke en besluite word by ilhanart.org/registry geregistreer
- Besluitrekord word openlik gepubliseer:
  - Aansoekdatum
  - Opsomming van hersieningsproses
  - Besluit (Approved / Rejected)
  - Besluitrede (kort verduideliking)
  - Opsomming van gemeenskapsterugvoer (anoniem)

#### Waarom Kuratoriale Besluit?

**Kwaliteitsbeheer:**  
PoArt Verified-status is 'n kenteken met hoë standaarde. Kuratoriale evaluering waarborg die behoud van hierdie standaarde.

**Voorkoming van Spekulatiewe Manipulasie:**  
Volledige on-chain bestuur (bv: Realms, DAO-stemming) is tegnies nie moontlik met Pump.fun-tokens nie. Off-chain stemstelsels is ook oop vir walvismanipulasie en gekoördineerde aanvalle. Kuratoriale besluit elimineer hierdie risiko.

**Operasionele Doeltreffendheid:**  
In plaas van komplekse stemmeganismes, 'n vinnige en duidelike besluitproses. Kunstenaars kry binne 30 dae 'n resultaat.

**Gemeenskapsdeelname:**  
Gemeenskapsterugvoer word ten volle in ag geneem en beïnvloed die besluitproses. Die finale besluit berus egter by die kuratorspan wat teen manipulasie beskerm word.

**Toekoms:**  
Wanneer die projek volwasse is (2027+), kan die gemeenskapskonsultasiemeganisme versterk word. Kuratoriale standaardbeskerm bly egter permanent.

---

### 6.3 Token Utility (Token Gebruiksareas)

**Voordele wat aan $CULTURE token-houers verskaf word:**

**1. Prioriteitstoegang tot Galery-geleenthede:**
- Reg om 1 week per jaar 'n uitstalling by İlhanArt Gallery te hou (reg kan oorgedra word)
- Afslag op drop paintings
- Reg op 10% tot 30% afslag op skilderye in die galery

**2. Volle Toegang tot PoArt Register:**
- Gedetailleerde rekords van alle geverifieerde kunswerke
- Volledige weergawes van Evidence Packs
- Forensiese verifikasie-gereedskap

**3. Advisory Voting:**
- Adviesreg in PoArt Verified-aansoeke
- Toegang tot gemeenskapsterugvoerkanale
- Deelname aan bestuursgesprekke

**4. Eksklusiewe Inhoud:**
- Ateljee agter-die-skerms-inhoud
- Kunstenaaronderhoude en prosesvideo's
- Toegang tot tegniese dokumentasie

**Let wel:**  
Token-houers gee advisory vote (adviesstemmings). Die finale besluit behoort aan die kuratorspan. Hierdie struktuur is gekies om walvismanipulasie en spekulatiewe aanvalle te voorkom. Daar is geen staking-belonings nie omdat ons langtermyn kulturele deelnemers soek, nie korttermyn huurlingkapitaal nie.

---

### 6.4 Metadata Sync (Sinchronisasie met Fisiese Wêreld)

- **Metadata Sync:** Tegniese data in die register moet 100% met die fisiese bate ooreenstem.

**Tegniese definisie van "100% ooreenstemming" (voorgestelde duidelikheid):**

- **Minimum ooreenstemming (verpligtend):**
  - `asset.fingerprints.sha256/sha512` in die register en die hash van die lêer in hand moet **presies dieselfde** wees.
  - `proof.notary_seal` in die register wanneer dit herproduseer word (indien Evidence Pack beskikbaar is) moet **presies dieselfde** wees.

- **Fisiese verwysing ooreenstemming (bewysstipe):**
  - Bewyse soos fisiese kunswerk + datum/blok verwysing getoon in lewende uitsending, moet konsekwent wees met Evidence Pack.

- **Privaatheidskonformiteit:**
  - In `masked` sigbaarheid word velde soos IP/ligging **gepubliseer volgens maskeringsstandaard**.

---

### 6.5 Betwisting, Hersiening en Herroeping (Dispute & Revocation)

Die register is nie net 'n "goedkeuring" meganisme nie; dit is 'n **lewende toesigmeganisme teen vervalsing**.

- Wanneer 'n betwisting begin word, kan die rekord in **"review"** modus geplaas word.
- Indien vervalsing opgespoor word, word dit gemerk as `status: void` en rede word bygevoeg:
  - `void_reason` (AI-gebruik / diefstal / manipulasie ens.)
  - `revoked_at` (herroepingstyd)
- Die bron van die herroepingsbesluit is duidelik sigbaar in die register:
  - kuratoriale hersiening / gemeenskapsbetwisting / forensiese analise-nota (wat ook al van toepassing is)

> **Hierdie afdeling is die registerekwivalent van die VOID-konsep in die "Red Flag Protocol"-afdeling.**

---

### 6.6 Voorbeeld Register Rekord (Masjien-leesbaar)
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

> *Let wel: `asset.fingerprints.sha512` en ander hash-waardes is verkort vir vertoning; in werklike toepassing word vollengte heksadesimale karakterstringe gebruik.*

---

## 7) 🔐 TEGNIESE SEËL (NOTARY SEAL)

**Onwrikbare seël-algoritme geproduseer deur PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$
# [PoArt] Digitale Notaris & Forensiese Bewys Protokol (Beta v1.0)

> **"Kultuur is groter as kapitaal. Beskerm jou kunswerke vandag, dra dit oor na môre."**

---

## Waarom Openbaar?

Werklike sekuriteit kom van deursigtigheid. Danksy ons **Public Registry (Openbare Register)** stelsel kan enige iemand enige plek in die wêreld; binne sekondes verifieer of die lêer in hul hand oorspronklik is, sonder om enige gesag te benodig.

---

## 🧩 Waarom Veelvuldige "Sigbaarheidsmodules"?

Dit is die mees kritieke deel van die kode (sigbaarheid keuslys). Hierdie opsies laat gebruikers toe om die **"Privaatheid vs. Deursigtigheid"** balans te stel:

### 🔒 Privaat (Private)

- **Scenario:** Die kunstenaar wil die kunswerk nog nie publiseer nie, maar wil 'n datumstempel sit en bewys "Ek het dit op hierdie datum gemaak".
- **Wat die Kode Doen:** Dit skryf data na die databasis maar sit 'n `visibility: "private"` etiket. In die toekoms wanneer jy "Public Read" beleid skryf, kan jy hierdie rekords van die publiek versteek deur `WHERE visibility = 'public'` te sê.

### 🕶️ Gemaskerd (Masked)

- **Scenario:** Die kunstenaar wil deursigtigheid maar is bang sy huisadres (IP-ligging) sal gevind word.
- **Wat die Kode Doen:** Aan die JavaScript-kant werk `maskIP` en `maskLoc` funksies. Dit verander die IP-adres na die `88.241.***.***` formaat, ligging na die `***/TR` formaat en stuur die gesensureerde weergawe na die databasis.
- **Privaatheidsnota:** Maskering word in die blaaier gedoen, Supabase sien nie die werklike ligging nie. **Maar:** As derdeparty-API's soos ipapi.co vir liggingsdata gebruik word, sien hierdie verskaffers die IP-adres op die oomblik van versoek.
- **Verseëling in Masked Mode:** EvidenceRoot en NotarySeal berekening word gedoen met gemaskerde forensiese data; so verifikasie bly deterministies.

### 🌍 Openbaar (Public)

- **Scenario:** Volle deursigtigheid. Volgens die [PoArt]-standaard word dit duidelik verklaar waar, wanneer, uit watter netwerk die kunswerk geproduseer is.

---

## 💡 Tegnologiese Innovasie

PoArt is nie net 'n lêeroplaaaistelsel nie. Dit is 'n **"Forensiese Bewysketting" (Forensic Chain of Custody)** enjin wat drie verskillende tegnologielae in een pot smelt en 'n nuwe standaard bring.

**Die laag wat in hierdie afdeling as "enjin" beskryf word, stem ooreen met die PoArt Forensic Engine (PFE) kern in vorige terminologie.**

### 1) Client-Side Hashing (Maksimum Privaatheid)

Jou kunswerklêers word nooit na die bediener opgelaai nie. Ons blaaier-gebaseerde (Client-side) enjin bereken die hash (digitale opsomming) van die lêer op jou eie rekenaar. Slegs hierdie vingerafdruk en metadata word na die bediener gestuur.

> **Privaatheidsnota:** Die kunswerklêer word nie na die bediener opgelaai nie en word so beskerm. Forensiese data (IP/ligging) word egter gedeel volgens die gekose sigbaarheidsmodus (private/masked/public).

### 2) Forensic Data Fusion (Forensiese Krag)

Dit is baie meer as 'n gewone tydstempel (Timestamp). Die stelsel kombineer die volgende data in 'n enkele "Genesis Seal":

- **Digitale Opsomming (SHA-512):** Digitale vingerafdruk wat sal breek selfs as 'n enkele pixel van die kunswerk verander, geproduseer met behulp van die kriptografiese opsomming (SHA-512) standaard.
- **Ligging & Tyd:** Datum met millisekondeakkuraatheid van wanneer die transaksie gedoen is, land, stad en distrikdata.
- **Toestelidentiteit:** Bedryfstelsel, blaaier en toesteltipe (User-Agent analise).

---

## 🛡️ Gebruiksareas en Voordele

As jy 'n kunstenaar, skrywer of ontwerper is, is dit nie genoeg om te sê "Ek het dit vroeër gedoen" nie, jy moet dit bewys.

**'n Kunswerk wat jy met PoArt verseël:**

- **Wiskundige Bewys:** Selfs as 'n enkele pixel van jou lêer verander, weet die stelsel dit. Manipulasie is onmoontlik.
- **Wetlike Basis:** Dit word geregistreer op watter datum, in watter stad, van watter toestel die kunswerk verseël is.
- **Onmiddellike Sertifikaat:** Binne sekondes produseer dit 'n **"Bate-identiteitsertifikaat"** uniek aan jou, met QR-kode en verseël.

---

## ⚙️ Stelselargitektuur en Tegniese Kenmerke

Die stelsel is ontwerp op 'n "Serverless" (Bediener-loos) argitektuur, gefokus op hoë prestasie en skaalbaarheid.

| Laag | Tegnologie | Beskrywing |
|------|------------|------------|
| **Kriptografie** | SHA-256 & SHA-512 | Dubbellaag kriptografiese opsomming |
| **Databasis** | Supabase (PostgreSQL) | JSONB datastruktuur, RLS-beleide |
| **Forensiese Data** | ipapi.co API | IP/Ligging/Tyd drietalligheid |
| **Rendering** | html2canvas + jsPDF | Client-side PNG/PDF produksie |
| **Frontend** | Vanilla JavaScript | Nul raamwerk-afhanklikheid |
| **Sekuriteit** | Client-side hashing | Lêer word nooit na bediener opgelaai nie |

### Uitstaande Kenmerke

| Kenmerk | Detail | By Mededingers? |
|---------|--------|-----------------|
| **Drag & Drop UI** | Sleep en los lêer, onmiddellike voorskou | ❌ Meeste het nie |
| **Multi-Format Export** | PNG, JSON, PDF - een klik | ⚠️ Beperk |
| **Real-Time Preview** | Sertifikaat lewende voorskou | ❌ Nie beskikbaar |
| **Privacy Controls** | Private/Masked/Public opsies | ❌ Nie beskikbaar |
| **Client-Side Hashing** | Lêer gaan nooit na bediener nie | ✅ Slegs 'n paar |
| **Forensic Metadata** | IP, ligging, toestel, tyd - alles saam | ❌ Gefragmenteer |
| **QR Verification** | Onmiddellike verifikasie QR-kode | ⚠️ Beperk |
| **Rate Limiting** | Spam-beskerming (RLS + Client) | ❌ Meeste het nie |

---

## 🗺️ Padkaart: "Trustless" Toekoms

Die huidige weergawe **(Beta v1.0)** is geoptimaliseer om die eindgebruiker maksimum spoed, maklike koppelvlak en gratis toegang te bied. Ons uiteindelike visie is egter om oor te gaan na 'n struktuur waar selfs die databasisadministrateur (ons) nie kan inmeng nie.

### Fase 1: Beta v1.0 (Tans Aanlyn)

**Infrastruktuur:**
- Cloud Database (Supabase)
- Off-chain register (PostgreSQL + IPFS-rugsteun)
- Gallery self-attestation (gesentraliseerd maar deursigtig)

**Token:**
- Platform: Pump.fun
- Likiditeit: Raydium (outomaties)
- Bestuur: Slegs advies (gemeenskapskonsultasie)

**Doel:**
- Spoed, verwyder UX-hindernisse
- Verskaf "wrywingslose" sekuriteit
- Bou gemeenskap

**Token Utility (v1.0):**
- Prioriteitstoegang tot galery-geleenthede
- Sien PoArt Register
- Advisory voting reg

---

### 🚀 Fase 2: Decentralized Authority (2026 Q2-Q4)

Hierdie fase dek die oorgang van die stelsel van 'n volledig "Client-Side" werkende struktuur na 'n veiliger en meer gedesentraliseerde struktuur.

| Kenmerk | Wat Bied Dit? | Tech Stack | ETA |
|---------|--------------|------------|-----|
| **Edge Function INSERT** | Spam-blokkering + API Key-sekuriteit | Supabase Edge (Deno) | Q2 2026 |
| **Wallet Signature** | Gedesentraliseerde identiteit | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | Gedesentraliseerde argief | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | Vals sertifikaat herroeping | DB Schema Update | Q2 2026 |
| **Audit Log** | Forensiese navraag rekord | Custom logs tabel | Q3 2026 |
| **OpenTimestamps** | Bitcoin-anker | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain stemming (x/web) + beursie handtekening
- Gemeenskapverteenwoordigers verkiesing (eerste 90 dae)
- Multi-sig operasies beursie beheer
- Weighted advisory voting (met walviskapitaal)

**Onveranderlikheid:**
- Register-rugsteun met IPFS-hashes
- Bitcoin-tydstempelanker
- Cross-chain verifikasie voorbereiding

---

### Fase 3: Volle Desentralisasie (2027+)

| Kenmerk | Doelwit | ETA |
|---------|---------|-----|
| **On-Chain Register** | Solana on-chain rekord | Q1 2027 |
| **Enhanced Token Utility** | NFT mint, gevorderde kenmerke | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **DID Integration** | Gedesentraliseerde Identiteit | Q3 2027 |
| **Community Governance** | Versterkte advies stelsel | Q4 2027 |
| **Legal Recognition** | Geldigheid in Turkse howe | 2027-2028 |
| **API for Developers** | Openbare API-eindpunt | Q3 2027 |

**Bestuur Evolusie:**
- v3.0: Hibriede model (kuratoriaal + gemeenskap geweeg)
- 2028+: Volledige gemeenskapsbestuur (opsioneel)
- Kuratoriale kwaliteitsbeheer bly altyd

---

## 🧬 Protokol Datastruktuur (JSON Schema)

**Elke [PoArt] sertifikaat het 'n draagbare en verifieerbare JSON-identiteitskaart wat in die volgende standaard geproduseer word.**

> **Let wel:** Hierdie Identity JSON-formaat is die sertifikaatformaat wat aan die gebruiker aangebied word. In registerrekords word `registry.asset` in plaas van `identity.asset_data` gebruik (kartering: `identity.asset_data` == `registry.asset`).
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

## 🔬 Tegniese Diepte: Seël-algoritme

### Deterministiese Hash-funksies
```javascript
// Helperfunksies: Skakel digest om na hex-string
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Skakel String om na byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Kanonieke forensiese string produksie (v1.0: vaste veldvolgorde + UTF-8 + \n delimiter)
// Fase 2 nota: Sal oorskakel na kanonieke JSON met RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal Produksieproses (Volledig Deterministies)
```javascript
// 1. FileHash berekening (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Forensiese data insameling (enkele tydstempel gebruik)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Enkele tydstempel produksie
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Dieselfde tydstempel
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot skepping (met kanonieke enkodering)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal produksie (dieselfde tydstempel gebruik)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Maskering helperfunksies (IPv4 en IPv6 ondersteuning)
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4 kontrole
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 of onbekende formaat
  return "***";
}
```

### Verifikasiestroom (Twee Vlakke)

#### Quick Verify (Vinnige Verifikasie)
```javascript
// Kontroleer slegs lêer-hash (vinnige rooi vlag)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Trek uit register
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Hash vergelyking
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Oorspronklik - Lêer-hash stem ooreen"
    };
  } else {
    return {
      valid: false,
      message: "❌ Vals - Lêer gemanipuleer"
    };
  }
}
```

#### Full Verify (Volledige Verifikasie)
```javascript
// Herproduseer EvidenceRoot en NotarySeal en verifieer
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Trek uit register
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash kontrole (vinnige rooi vlag)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Vals - Lêer-hash stem nie ooreen nie" };
  }

  // 2) Herproduseer EvidenceRoot (met forensics gestoor in register)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Stem nie ooreen nie - EvidenceRoot klop nie" };
  }

  // 3) Herproduseer NotarySeal (dieselfde tydstempel + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Stem nie ooreen nie - NotarySeal klop nie" };
  }

  // Opsioneel: In Fase 2 verifieer ook signer_sig met attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Handtekening ongeldig" };

  return { valid: true, message: "✅ Oorspronklik - Full Verify geslaag" };
}
```

> **Belangrike Notas:**
> - **Quick Verify:** Kontroleer slegs lêer-hash vir vinnige gebruik.
> - **Full Verify:** Verifieer alle lae van die protokol (EvidenceRoot + NotarySeal).
> - Alle hash-bewerkings word deterministies gedoen, met vaste enkodering en delimiters.
> - **v1.0 kanonikaliseringstandaard:** Vaste veldvolgorde + UTF-8 enkodering + `\n` delimiter.
> - **Fase 2 plan:** Oorgang na kanonieke JSON met RFC 8785 (JCS - JSON Canonicalization Scheme).
> - In Masked modus word EvidenceRoot en NotarySeal berekening gedoen met gemaskerde forensics.
> - Enkele tydstempel word deurgaans in die hele proses (forensics + NotarySeal) gebruik; determinisme is gewaarborg.
> - **Forensics veldname:** `ip_masked`, `location`, `device`, `timestamp` (kode en register is volledig verenigbaar).
> - **Register pad:** `certificate.asset.fingerprints` (volledig verenigbaar met verifikasieklode).
> - **signer_sig in Register:** `proof.signer_sig` veld is nodig vir Full Verify.
> - SignerSignature-meganisme sal in Fase 2 met Solana Wallet Adapter geaktiveer word; in v1.0 kan verifikasie gedoen word met `attestation_pubkey`.

---

## 📊 Mededinger-analise (Opgedateer)

PoArt is geposisioneer op die "Sweet Spot" (ideale punt) wat die tekortkominge van bestaande oplossings aanvul.

| Kenmerk | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Koste** | 🆓 Gratis | 🆓 | 💰 Betaald | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Baie Maklik | ❌ CLI | ⚠️ Gemiddeld | ⚠️ Gemiddeld | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Lewendig | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Modusse | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privaatheid | ✅ | ❌ Oplaai | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Volledig | ❌ | ❌ | ⚠️ Beperk | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Onmiddellik | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Padkaart | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Afrikaans Ondersteuning** | ✅ Inheems | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Verduideliking:**
- ✅ : Volle ondersteuning / beskikbaar
- ⚠️ : Beperk / in betaalde planne
- ❌ : Nie beskikbaar / nie ondersteun nie
- 🔄 : Op padkaart (word ontwikkel)
- 🆓 : Volledig gratis
- 💰 : Betaald / intekening benodig

### Mededingers se Tekortkominge, PoArt se Sterk Punte

| Tekort | Mededingers | PoArt |
|--------|-------------|-------|
| **Gebruiksmoeilikheid** | CLI, API-kennis, beursie benodig | Sleep en los, klaar met 3 klieke |
| **Koste-hindernis** | $50-500/maand intekening | 100% gratis |
| **Privaatheid** | Lêer word na bediener opgelaai | Client-side, lêer gaan nooit |
| **Forensiese Data** | Slegs tydstempel | IP, ligging, toestel, tyd - alles |
| **Afrikaans Ondersteuning** | Nie beskikbaar of baie beperk | Inheemse taalondersteuning |
| **Oopbron** | Geslote boks | Alle kode oop op GitHub |

---

## 📈 Gebruikstatistieke (2026 Q1 Doelwitte)

| Metriek | Doelwit | Status |
|---------|---------|--------|
| **Totale Sertifikate** | 1,000 | 🔄 Vordering |
| **Aktiewe Gebruikers** | 500 | 🔄 Vordering |
| **Verifikasie Getal** | 5,000 | 🔄 Vordering |
| **Uptime** | 99.9% | ✅ Aktief |
| **Gem. Responstyd** | <200ms | ✅ Optimaal |

---

## 🌍 Gemeenskap & Ondersteuning

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **E-pos:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Bydraers

Die PoArt-protokol bly ontwikkel met bydraes van die oopbron-gemeenskap.

**Om by te dra:**
1. Fork
2. Skep 'n feature branch (`git checkout -b feature/amazing-feature`)
3. Commit (`git commit -m 'Add amazing feature'`)
4. Push (`git push origin feature/amazing-feature`)
5. Maak 'n Pull Request oop

### 🛠️ Wat Het Ons Nou Nodig? (Hulpoproep)

Ons wag op bydraes van ervare ontwikkelaars in die volgende onderwerpe vir **Fase 2** ontwikkelinge van die PoArt Protokol:

* **Supabase Edge Functions:** Skuif spam-beskerming na bedienerkant.
* **Solana Web3.js:** Beursie-ondertekening (Wallet Signing) integrasie.
* **IPFS / Arweave:** Argivering en pinning dienste integrasie.
* **Community Tools:** X stemming, stemsisteme, analytics dashboard.

> Begin asseblief 'n bespreking in die "Issues"-oortjie voordat jy 'n kenmerk byvoeg.

---

## 💬 Finale Notas

### Pump.fun en Werklikheid

Hierdie projek is op Pump.fun begin omdat:
- ✅ Likiditeit toegang (Raydium outomatiese migrasie)
- ✅ Bestaande gemeenskap toegang
- ✅ Lae beginkoste

Maar laat ons dit duidelik maak:
- **Token prys** is nie 'n aanduiding van artistieke sukses nie
- **Operasionele begroting** vir token waarde is belangrik (galery, uitstallings, infrastruktuur)
- **Sukses-metrieke:** Geverifieerde kunswerke + gemeenskapsbetrokkenheid + fisiese besoekers

### Bestuur en Desentralisasie

**v1.0 Werklikheid (2026):**
- Register: Off-chain (PostgreSQL + IPFS-rugsteun)
- Attestasie: Gallery self-signed (gesentraliseerd maar deursigtig)
- Bestuur: Slegs advies (kuratoriale finale besluit)
- Token utility: Gallery toegang + register + NFT prioriteit

**v2.0+ Visie (2027+):**
- Register: On-chain (Solana)
- Handtekeninge: Beursie-gebaseer (gedesentraliseerd)
- Bestuur: Hibried (gemeenskap advies + kuratoriale kwaliteit)
- Token utility: Verbeterde kenmerke + gevorderde toegang

Hierdie struktuur verskaf **operasionele doeltreffendheid** en **kwaliteitsbeheer** in die vroeë stadium, terwyl dit die pad oopmaak om **gemeenskapsdeelname** in die toekoms te verhoog.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Kultuur is Groter as Kapitaal*

## 🧾 Lisensie

MIT-lisensie © 2026 İlhan Art Gallery Initiative

Sien [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) vir volledige terme.

---

## 💬 Erkennings

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Hierdie projek is ontwikkel met die [İlhan Art Gallery] inisiatief, en bronkodes is oop vir die publiek ter wille van deursigtigheid.**

**PROTOKOL V1.0 // VERSEËL MET SHA-512.**

*© 2026 İLHAN ART | ALLE REGTE OP KUNSWERKE, BEELDE EN IDEES VOORBEHOU.*

---
