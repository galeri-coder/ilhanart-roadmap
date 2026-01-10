# 📚 WOORDELYS VAN TEGNIESE TERME EN KONSEPTE
> **"Om die taal van hierdie protokol te verstaan, beteken om die visie daarvan te verstaan."**

## ⚙️ PoArt Forensiese Enjin (PFE) v1.0: Grondslag Infrastruktuur

**PoArt Forensiese Enjin (PFE)** is die hooflaag wat die sentrale logika en tegniese werking agter die [PoArt] protokol verteenwoordig. Dit is die "forensiese enjin" wat rou data van kunswerk produksie neem en dit omskakel in **digitale bewyse** wat geverifieer kan word en onveranderbaar is.

### 🧩 Hoekom "PoArt Forensic"?

- **PoArt (Bewys van Kuns):** Die doel van die enjin is om die waarde van 'n digitale bate nie aan spekulasie te koppel nie, maar aan **'n verifieerbare produksieproses**.
- **Forensic (Wetenskaplike Verifikasie):**
  - **Tegniese Definisie:** Algoritme metode en rekordreeks om te verifieer dat die data van die produksieproses (kwas slae, tyd video, rekords) nie gemanipuleer is nie.
  - **Filosofiese Vlak:** Die bewering om **menslike tyd, poging en besluitnemingskoste** om te skakel in meetbare waarheid, teen AI se "onmiddellike resultaat" produksie.

> Let wel: Blockchain integrasie (bv. Solana) is nie die kern van PFE nie; dit sal apart beskryf word as die **Ketting Anker Laag** vir verifikasie/registrasie doeleindes.

### 🛠️ Tegniese Omvang v1.0

**PoArt Forensiese Enjin (PFE) v1.0** is gebou op die volgende **3 sleutelpilare** eerder as komplekse finansiële modelle:

1. **Hashing & Sealing (Verseëling):**  
   PFE verwerk op 'n bepaalbare manier al die elemente in die Bewys Pak (kunswerkfêer, video, JSON/rekord, handtekening, ens.) en genereer 'n unieke **NotarySeal** waarde.

   **Sleutelkonsepte (v1.0):**
   - **FileHash (vingerafdruk van werk):** Hash gegenereer vanaf die kunswerkfêer se bytes.
   - **EvidenceRoot (wortelpak van bewys):** Wortelsamevatting wat die integriteit van die Bewys Pak verteenwoordig (Merkle wortel of hash van kanonieke voorstelling).
   - **NotarySeal (finale seël / PFE uitset):** Finale seël gegenereer vanaf die kombinasie van EvidenceRoot + tyd + handtekening.

   **Formules (duidelik sigbaar vir beleggers):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Kanonieke Payload Definisies (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Let wel: Die waarde waarna verwys word as PFE uitset is **NotarySeal**. Die **SignerSignature** prosedure sal geaktiveer word in Fase 2 (met Solana Wallet Adapter); in die huidige v1.0 word die stelsel se attestasie handtekening gebruik. Die attestasie openbare sleutel word gepubliseer in die register onder die `issuer.attestation_pubkey` veld.

2. **Indexing (Opberging):**  
   Dit skryf watter beursie, op watter datum, **Bewys van Werk** vir watter werk gestuur het na 'n duidelike en navraagbare registervlak.  
   *(Hierdie vlak kan 'n databasis wees; ketting integrasie word apart beskryf as "Ketting Anker Laag".)*

3. **Verification (Verifikasie):**  
   Wanneer die geldigheid van 'n werk bevraagteken word, verwerk PFE die rou bewyse weer; dit toets wiskundig of die berekende **EvidenceRoot / NotarySeal** waardes ooreenstem met die gestoorde rekords.

---

### 🧮 PoArt Waarde Teorie (The Value Theorem)

Die [PoArt] protokol koppel die waarde ($V$) van 'n digitale bate nie aan ongrypsbare markpersepsie nie, maar aan die **fisiese werklikheid van die produksieproses**.

Kunsmatige Intelligensie (AI) vernietig die proses deur onmiddellik resultate te lewer ($t \to 0$). [PoArt], egter, hanteer waarde as die akkumulasie van elemente van **tyd, arbeid en agentskap**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definisies van Veranderlikes

- **$\int dt$ (Prosesakkumulasie):**  
  Waarde is nie 'n "onmiddellike resultaat" nie; dit is 'n **proses** wat akkumuleer tussen $t_{\text{start}}$ en $t_{\text{end}}$. Soos die duur afneem (AI produksie), nader die integraalresultaat 0.

- **$P_{\text{labor}}(t)$ (Oombliklike Arbeidskrag):**  
  Verteenwoordig die intensiteit van verstandelike en fisiese poging wat tydens produksie bestee word. Soos verifieerbare poging toeneem, groei die integrand.  
  > Let wel: Hierdie term kan in praktyk genormaliseer word deur "meetbare/verifieerbare arbeidstekens".

- **$I_{\text{agency}}(t)$ (Agentskap Faktor):**  
  Die vermoë van die skepper om risiko's te neem en besluite te neem. Dit neem waardes tussen $0$ en $1$.
  - **AI ($I \approx 0$):** Voer opdragte uit, neem geen risiko's, betaal geen koste.
  - **Mens ($I \to 1$):** Verander besluite, twyfel, neem risiko's.

- **$U_{\text{irreversible}}$ (Onomkeerbare Uniekheid):**  
  Terwyl ongedaan maak (`Ctrl+Z`) moontlik is in digitale produksie, in fisiese produksie (verf aangebring op doek, gebeitel klip, beweging in regstreekse uitsending) is daar geen terugweg nie. Hierdie **onomkeerbaarheid** is 'n bykomende term wat "uniekheid" (onvervangbare eienskappe) in die werk skep.

### 🔎 Gevalle Analise: AI "Onmiddellike Resultaat" vs. Mens "Geverifieerde Proses"

Die volgende scenario toon hoe die **PoArt Waarde Teorie** in praktyk werk en hoekom AI produksie laer tellings kry op die [PoArt] skaal.

#### Scenario A: 10-Sekonde Visuele Produksie met AI

- **Duur ($\Delta t$):** $10$ sekondes (klein proses)
- **Arbeidskrag ($P_{\text{labor}}$):** $1$ eenheid (net opdrag skryf)
- **Agentskap Faktor ($I_{\text{agency}}$):** $0.01$ (geen risiko, geen koste)
- **Onomkeerbaarheid ($U_{\text{irreversible}}$):** $0$ (omkeerbaar / kopieerbaar)

**Resultaat:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Kommentaar:** Selfs al is die resultaat perfek; die [PoArt] waarde nader $0$ omdat daar geen proses geleef is nie en geen agentskap/risiko betrokke is nie.

#### Scenario B: 6-Uur Fisiese Produksie in Regstreekse Uitsending

- **Duur ($\Delta t$):** $6$ ure ($21{,}600$ sekondes)
- **Arbeidskrag ($P_{\text{labor}}$):** $0.5$ eenhede (volgehoue fisiese en verstandelike poging)
- **Agentskap Faktor ($I_{\text{agency}}$):** $0.9$ (veranderende besluite, neem risiko's, onomkeerbare keuses)
- **Onomkeerbaarheid ($U_{\text{irreversible}}$):** $>0$ (fisiese tekens kan nie ongedaan gemaak word nie)

**Resultaat:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Kommentaar:** Soos die proses verleng en agentskap (risiko) toeneem, akkumuleer die waarde kumulatief. Die $U_{\text{irreversible}}$ term is 'n bykomende bydrae wat "uniekheid" (onvervangbare eienskappe) in die werk skep.

---

### ✅ Gevolgtrekking: Bewys-Gebonde Waarde (Proof-Bound Value)

Hierdie teorie haal die waarde-bewering van [PoArt] uit om "voorkeur" of "markverhaal" te wees en koppel dit aan **verifieerbare produksiewerklikheid**.

1. **Geen Proses, Geen Waarde:**  
   AI vernietig die proses met onmiddellike resultate ($t \to 0$). Soos die prosesvenster krimp, moet die integraalresultaat afneem:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Agentskap en Risiko is Vermenigvuldigers:**  
   [PoArt] meet nie net "tyd spandeer" nie maar ook die werklike vlak van besluitneming, risiko en koste in daardie tyd. Produksie sonder risiko (AI) het lae waarde:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Uniekheid is Fisiese Bewys, Nie Bemarking Nie:**  
   Onomkeerbare tekens in fisiese produksie (doek slag, klip stuk) is buite die `Ctrl+Z` logika van digitaal. Hierdie onomkeerbaarheid ($U_{\text{irreversible}}$) maak die werk uniek deur ontologie.

> **🔐 OPSOMMING:** Alhoewel die waarde teorie onsekerheid as 'n maatstaf kan lyk (selfs al kan die werklike wêreld ekwivalent nie volledig gemeet word nie), is die doel van hierdie formule om die opstelling en rigting van veranderlikes te toon. In die AI-era is wat skaars is nie die "prentjie" nie maar **verifieerbare werk, tyd en agentskap.** [PoArt] meet hierdie skaarsheid en skryf dit neer met die **Bewys Pak**.

### 🏛️ Belangrikheid van die "Enjin" Konsep

Tokens wat verskyn vanaf Pump.fun of soortgelyke platforms is dikwels slegs **"toegangkaartjies"**. Die **PoArt Forensiese Enjin (PFE)**, egter, is die **grondwetlike logika laag** wat bepaal watter regte hierdie kaartjie beskerm, hoe die werk opgeskryf sal word en hoe kuns/wetenskap/tegnologie volgehou sal word.

> **Let wel:** Die rede waarom ons hierdie projek op Pumpfun begin het, is omdat ons nie genoeg finansiering of genoeg volgelinge gehad het nie. Om bestaande data te gebruik was 'n strategiese korrekte stap, selfs al was dit nie die hoogste gehalte nie. Ongeag die begroting en hulpbronne, bewys die definiëring van hierdie enjin se logika op GitHub dat die projek nie net 'n finansiële spekulasie is nie, maar 'n langetermyn visie van **sagteware infrastruktuur** en **nasionale digitale biblioteek**.

---

## �🎨 [PoArt] BEWYS VAN WERK PROTOKOL (Proof of Art Protocol v1.0)

> **"Egte Kunstenaar, Egte Produksie, Egte Waarde."**

Hierdie protokol is 'n **biologiese en intellektuele beskermingsprosedure** wat ontwikkel is teen onbekende opligters wat die crypto ekosisteem omring, AI beelde wat in 5 minute geskep word, en "Pump & Dump" kultuur.

---

## a) Wat is [PoArt]? (Filosofiese en Tegniese Definisie)

**Bewys van Kuns [PoArt];** is 'n institusionele verifikasie standaard wat verseker dat die waarde agter 'n bate op die blockchain nie gebaseer is op spekulasie nie, maar op **menslike arbeid**, **tyd** en **fisiese energie** wat geverifieer kan word.

Soos Bitcoin waarde skep met *"Elektrisiteit en Prosessorkrag"* **(Bewys van Werk)**, skep projekte wat ooreenstem met [PoArt] waarde met *"Kuns Vaardigheid en Menslike Tyd"*.

Dit verwyder die risiko van *"Ontwikkelaar het verkoop, projek is verby"* op Pump.fun en DEX platforms; want hier is waarde nie in die kode nie, maar in die **voortsetting van produksie**.

> **[PoArt] sê nie vir deelnemers "Glo ons"; dit sê "Hier is die bewys, kyk met jou oë, verifieer met jou wiskunde."**

---

## b) [PoArt] se 5-Pilaar Standaard (5 Pilare van Waarheid)

Hierdie 5 items is onomkeerbare filters wat 'n projek moet slaag om die [PoArt] seël te ontvang.

### 1) Direkte Identiteit Bewys

- **Probleem:** Die crypto wêreld is vol anonieme stigters (Devs) met onduidelike identiteite wat geld insamel en projekte verlaat.
- **[PoArt] Oplossing:** Die skepper verifieer nie net identiteit nie, maar **teenwoordigheid tydens produksie**. Dit sluit in regstreekse uitsending sessies waar gemeenskap interaksie plaasvind en spesifieke versoeke dadelik uitgevoer word, nie vooraf opgenome video's nie.  
  (Byvoorbeeld, *"Skryf vandag se datum en huidige blok nommer op die regterkantste hoek van die doek"*)
- **Slagspreuk:** *"Bots kan verf maar bots sweet nie en kan nie improviseer nie."*

### 2) Bewys van Werk en Proses

- **Probleem:** AI (Kunsmatige Intelligensie) beelde geskep in 2 sekondes kry dieselfde "jpeg" behandeling as olieverf wat 2 maande lank gemaak is in die digitale wêreld.
- **[PoArt] Oplossing:** Die "swangerskap en geboorte" proses van die werk word opgeskryf. Skets stappe, verfstadiums, gestoorde opgehoopte ure en die fisiese proses wat die kunstenaar ondergaan het tydens die skep van die werk word opgeskryf. Dit voeg **"Tydkoste"** by die token. Hoe moeiliker die bate produksie, hoe sterker sy waarde.

### 3) Bewys van Estetiese Waarde

- **Probleem:** "Meme" kultuur wat fokus op oombliklike komedie terwyl dit estetika en artistieke diepte verontagsaam, wat lei tot korttermyn "Hype" projekte.
- **[PoArt] Oplossing:** Die projek moet akademiese kunstandaarde hê, kleurteorie, komposisiereëls en materiaalkennis (Impasto, Tekstuur, ens.). Inhoud moet nie net jou laat lag nie; dit moet verwondering in kykers opwek en **versamelwaarde** hê.

### 4) Konsep Nuutheid

- **Probleem:** Duisende hond/kat munt afskrifte sonder kreatiwiteit.
- **[PoArt] Oplossing:** Die projek moet 'n nuwe brug bou wat kuns, wetenskap, filosofie of tegnologie in 'n betekenisvolle struktuur kombineer.  
  (Byvoorbeeld, Kombineer die antieke standbeeld van David met crypto mark data; verwerk die idee dat menslike persepsie "in klip verander" deur dit en grond dit met wetenskaplike bronne.)  
  Die werk moet nie net 'n visuele fees wees nie maar ook 'n intellektuele uitdaging wat gedagtes oor **Wetenskap, Filosofie of Tegnologie** opwek.

> [!IMPORTANT]
> **Geheue Voorbeeld (Las Palmitas Effek):** In die Las Palmitas buurt in Meksiko, geteister deur misdaad, is meer as 200 huise omskep in 'n groot reënboog spektakel. As gevolg van hierdie estetiese ingryping het misdaadvlakke in die buurt aansienlik afgeneem, en jongmense het begin om betrokke te raak by kuns eerder as misdaad bendes. Die estetiese verandering het mense se respek vir hul omgewing en mekaar herskryf (Sosiale Integrasie).
>
> **Verwagting:** 'n Projek wat die [PoArt] lys betree moet, soos in die voorbeeld hierbo, 'n verhouding van sosiale, wetenskaplike of filosofiese oorsaak en gevolg hê bo net visuele estetika. Aangesien tyd die enigste bate is wat nie met geld gekoop kan word nie, moet tyd in hierdie protokol geverifieer word deur dit as sekuriteit te sit. Die konsep grondslag van die projek moet so sterk en universeel wees dat selfs in die geval van 'n moontlike CTO (Gemeenskap Oorneem) jare later, die gemeenskap onafhanklik kan voortgaan met die kreatiewe potensiaal van die projek deur hierdie nalatenskap te erf.

### 5) Nie-Algoritmiese Agentskap

- **Probleem:** Volledige maar sielloos herhalende digitale produksies.
- **[PoArt] Oplossing:** Die unieke agentskap van 'n mens wat foute kan maak, risiko's kan neem en emosionele veranderinge kan ondervind moet gevoel word in die werk. Onsekerheid in kwasslae, onverwagte reaksies van materiale en die oombliklike besluite van die kunstenaar is die **Biologiese Handtekening** wat die werk skei van "Masjien Produksie".

---

## c) Verifikasie Prosedure en Bedrog Voorkoming

Hierdie stelsel verseker dat die projek geloofwaardig en lewend bly nie net "aan die begin" nie maar "vir ewig".

### 📦 Bewys Pak - Digitale Tweeling

Agter elke werk wat deur [PoArt] goedgekeur is, is daar 'n geënkripteerde en tyd-gestempelde data pakket wat beleggers kan aflaai:

- **RAW Video Rekords:** Rou ononderbroke film van die produksietyd.
- **Metadata Analise:** Fêer skeppingsdatum, inligting oor die apparaat wat gebruik is en ligging data.
- **Fisiese Verwysings:** Bewys dat die werk bestaan in die fisiese wêreld  
  (Byvoorbeeld, Huidige koerant of blockchain data van daardie tyd naby die werk).

> *Ooreenstemming nota:* Die term "bewys pak" koppel aan die ketting **Bewys Pak → EvidenceRoot → NotarySeal** in voorafgaande afdelings; dit wil sê, die integriteit van die pakket word verteenwoordig deur 'n verifieerbare seël.

### 🔄 365-Dag Hernuwing (Volhoubaarheid Protokol)

- **Revolusionêre Kenmerk:** In crypto projekte gee die "Dev" (Ontwikkelaar) gewoonlik die token uit en verdwyn gewoonlik na 1-2 maande (Sagte Mat). [PoArt] maak dit onmoontlik.
- **Reël:** Die status van "Geverifieerde Kunstenaar" is nie lewenslank nie. Slegs **1 Jaar** is geldig.
- **Werking:** Die kunstenaar/ontwikkelaar moet elke 365 dae 'n **nuwe belangrike en verifieerbare werk** aan die gemeenskap voorlê.
- **Scenario Voorbeeld:** Jy het die projek in 2026 begin. In Januarie 2027 gee die stelsel 'n waarskuwing "Bewys Tydperk het Verstryk". As die kunstenaar nie 'n nuwe vertoning, nuwe fisiese werk of nuwe tegnologie-integrasie voorlê nie, val die "Vertroue Badge" van die projek.
- **Resultaat:** Hierdie stelsel verseker dat **inhoud nooit relevansie verloor nie** en dat die belegger nooit die vrees het van *"Is die ontwikkelaar nog daar?"*. Die projek word 'n lewende ateljee.

### 🚩 Rooi Vlag Protokol

**In die geval van enige bedrog wat deur die gemeenskap of algoritmes ontdek word (AI gebruik, gesteelde werk, gemanipuleerde video):**

1. Die sertifikaat word onmiddellik gemerk as **"VOID" (NIETIG)**.
2. Bewys pakkette word openbaar gemerk as **"Vals"**.
3. Die projek word op die [PoArt] swartlys geplaas. Dit versterk dat in die gedekentraliseerde wêreld, **reputasie die enigste munt is**.

---

## d) Gevolgtrekking: Nie 'n Casino Nie, Maar 'n Museum

**Pump.fun en Gedekentraliseerde Uitruilings (DEX) is ongelukkig nou 'n casino; ligte flikker, almal jaag vinnige winste, en die huis (opligters) wen altyd. Die rede waarom ons die projek hier begin het, is gebrek aan voldoende finansiering en om 'n omgewing te hê om bestaande gehore te bereik deur regstreekse uitsending.**

**[PoArt] is 'n vesting gebou in die middel van hierdie casino.**

- 🎰 Casino is gebaseer op kaartspeletjies; ons is gebaseer op **fisiese werklikheid**.
- 🃏 Casino is oop vir bedrog; ons is oop vir **duidelike bewys**.
- ⏳ Casino is tydelik; ons fokus op **ewigheid van kuns en wetenskap**.

**Die token wat hierdie protokol gebruik is nie net "'n munt" nie; dit is digitale kapitaal met sweet, verf, kode en filosofie.**

---

## 🗳️ 6) BESTUUR EN OPENBARE REGISTER

**Die doel van hierdie afdeling is: om die [PoArt] standaard te verander van die vlak van "vertrou individue" na volhoubare openbare infrastruktuur met register + verifikasie + gemeenskapstoesig.**

### 6.1 Openbare Register

- **Openbare Register:** Alle goedgekeurde data word geskryf by `ilhanart.org/registry` (of GitHub Registry).

**Register logika (voorgestelde standaard - in JSON pad formaat):**

Elke inskrywing wat die register betree dra hierdie minimum verifieerbare kern velde:

- **Identiteit en Status:**
  - `certificate_id` (leesbare verwysing)
  - `status` (active / void)
  - `void_reason` (indien van toepassing)
  - `visibility` (private / masked / public)
  - `created_at` (tydstempel)

- **Uitreikende Gesag:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Werk Inligting:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (indien moontlik; vir identiteit met token hek)
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
  - `governance.veto_threshold`

Die register kan twee vlakke hê:
- **1)** Mens-leesbare indeks (weblys / soek / filter)
- **2)** Masjien-leesbare verteenwoordiging (JSON rekords; vir PFE verifikasie)

**Hierdie "inskrywing" word verifieerbaar deur die ketting Bewys Pak → EvidenceRoot → NotarySeal van PFE. Die register verskaf verifikasie doelwitte, nie "bewerings" nie.**

---

### 6.2 40% Gemeenskap Veto (Token-Gated Bestuur)

- **40% Gemeenskap Veto:** Stemming begin een maand voor die toekenning van status; 'n 40% gemeenskap **Token-Gated (geverifieer met Solana)** veto kanselleer die aansoek.

**Stemvloei (voorgestelde duidelike proses):**
- **Aansoek venster:** Kandidaat projek open "'n PoArt kandidaat registrasie" (kandidaat rekords sigbaar in "wagstatus").
- **Resensie tydperk:** Gemeenskap ondersoek bewyse vir 30 dae (Bewys Pak + regstreekse uitsending rekords + metadata).
- **Token-gated verifikasie:** Stemming word gedoen met geverifieerde Solana beursies (bv. eienaarskap van spesifieke token/NFT + beursie handtekening).
- **Veto reël:** As 40% van stemme **teenkanting (NEE / VETO)** is, word die aansoek verwerp.
- **Deursigtigheid:** Stemresultate word in die register gestoor as "'n besluitrekord" (datum, verhouding, beeld ID).

---

### 6.3 Metadata Sinchronisasie (Ooreenstemming met Fisiese Wêreld)

- **Metadata Sinchronisasie:** Tegniese data in die register moet 100% ooreenstem met die fisiese entiteit.

**Tegniese definisie van "100% ooreenstemming" (voorgestelde deursigtigheid):**
- **Minimum ooreenstemming (verpligtend):**
  - `asset.fingerprints.sha256/sha512` in die register moet **dieselfde** wees as die hash van die betrokke fêer.
  - Wanneer `proof.notary_seal` in die register hergenereer word (as Bewys Pak teenwoordig is), moet dit **dieselfde** wees.
- **Fisiese verwysing ooreenstemming (tipe bewys):**
  - Fisiese werk + datum/blok verwysing getoon in regstreekse uitsending en dieselfde bewys moet ooreenstem met die Bewys Pak.
- **Privaatheid nakoming:**
  - Velde soos IP/ligging in `masked` sigbaarheid word gepubliseer **volgens maskering standaarde**.

---

### 6.4 Geskil en Kansellasie

Die register is nie net 'n "goedkeuring" prosedure nie; dit is 'n **lewende resensie proses teen bedrog**.

- Wanneer 'n geskil begin word, kan die inskrywing in **"review" (resensie)** status geplaas word.
- As bedrog ontdek word, word dit gemerk as `status: void` met rede bygevoeg:
  - `void_reason` (AI gebruik / diefstal / manipulasie, ens.)
  - `revoked_at` (kansellasie tyd)
- Die bron van die kansellasie besluit is duidelik in die register:
  - gemeenskap stem / gemagtigde komitee / wetenskaplike ondersoek nota (wat van toepassing is)

> **Hierdie afdeling is die register tweeling van die VOID konsep in die "Rooi Vlag Protokol" afdeling.**

---

### 6.5 Register Inskrywing Voorbeeld (Masjien Leesbaar)
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
> *Let wel: `asset.fingerprints.sha512` en ander hash waardes is afgekort vir vertoon doeleindes; in werklike implementering word volle lengte hexadecimale stringe gebruik.*

---

## 7) 🔐 TEGNIESE SEËL (NOTARY SEAL)

Onwrikbare seël algoritme gegenereer deur die **PoArt Forensiese Enjin (PFE) v1.0**:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Digitale Notaris en Wetenskaplike Bewys Protokol (Beta v1.0)

> **"Kultuur is Groter as Kapitaal. Beskerm jou werke vandag, neem hulle môre."**

---

## Hoekom Openbaar?

Werklike sekuriteit kom van deursigtigheid. Danksy ons **Openbare Register** stelsel kan enigiemand oral in die wêreld binne sekondes verifieer dat 'n fêer outentiek is, sonder enige gesag.

---

## 🧩 Hoekom Veelvuldige "Sigbaarheid Modules"?

Dit is die mees kritiese deel van die kode (sigbaarheid keuse kieslys). Hierdie keuses stel gebruikers in staat om **"Privaatheid vs. Deursigtigheid"** te balanseer:

### 🔒 Privaat

- **Scenario:** Kunstenaar wil nog nie die werk publiseer nie, maar wil dit tyd-stempel om te bewys "ek het dit op hierdie datum gemaak".
- **Wat Doen Die Kode:** Dit skryf data in die databasis maar druk die seël `visibility: "private"`. Later wanneer jy die "Openbare Lees" beleid skryf, kan jy hierdie rekords van die publiek wegsteek met `WHERE visibility = 'public'`.

### 🕶️ Gemaskeer

- **Scenario:** Kunstenaar wil deursigtigheid maar is bevrees sy huis adres (IP ligging) sal gevind word.
- **Wat Doen Die Kode:** Die `maskIP` en `maskLoc` funksies werk aan die JavaScript kant. Dit verander die IP adres na formaat `88.241.***.***`, ligging na formaat `***/TR`, en stuur die gesensureerde weergawe na die databasis.
- **Privaatheid Waarheid:** Maskering word gedoen op die blaaier, Supabase sien nie die werklike ligging nie. **Maar:** As derde party APIs soos ipapi.co gebruik word vir ligging data, sien hierdie verskaffers die IP adres tydens die versoek.
- **Verseëling in Maskeer Modus:** EvidenceRoot en NotarySeal berekening word gedoen met gemaskeerde forensiese data; dus bly verifikasie bepaalbaar.

### 🌍 Openbaar

- **Scenario:** Volle deursigtigheid. Volgens [PoArt] standaarde word waar, wanneer, vanaf watter netwerk die werk geskep is openlik aangekondig.

---

## 💡 Tegnologiese Innovasie

PoArt is nie net 'n fêer oplaai stelsel nie. Dit is 'n **"Wetenskaplike Sorg Ketting"** enjin wat 'n nuwe standaard bring deur drie verskillende tegnologie vlakke in een pot te kombineer.

**Die laag wat as "enjin" in hierdie afdeling beskryf word stem ooreen met die kern van die PoArt Forensiese Enjin (PFE) in voorafgaande terme.**

### 1) Kliënt-Kant Hashing (Hoogste Privaatheid)

Jou kunswerkfêers word nie na die bediener opgelaai nie. Ons blaaier-gebaseerde (kliënt-kant) enjin bereken die hash (digitale opsomming) van die fêer op jou eie rekenaar. Net hierdie vingerafdruk en metadata word na die bediener gestuur.

> **Privaatheid Waarheid:** Die werkfêer word nie na die bediener opgelaai nie en word op hierdie manier beskerm. Maar, forensiese data (IP/ligging) word gedeel volgens die gekose sigbaarheid modus (privaat/gemaskeer/openbaar).

### 2) Forensiese Data Samesmelting (Wetenskaplike Krag)

Meer as gewone tydstempel. Die stelsel smelt hierdie data saam in een "Oorsprong Seël":

- **Digitale Opsomming (SHA-512):** Vingerafdruk deur gebruik te maak van die kriptografiese opsomming standaard (SHA-512) wat sal breek as selfs een pixel van die werk verander.
- **Ligging en Tyd:** Datum met millisekondes akkuraatheid, land, stad en distrik data van die transaksie.
- **Toestel Identiteit:** Bedryfstelsel, blaaier en toestel tipe (User-Agent analise).

---

## 🛡️ Gebruik Gevalle en Voordele

As jy 'n kunstenaar, skrywer of ontwerper is, is dit nie genoeg om te sê "Ek het dit vroeër gemaak" nie; jy moet bewys.

**Die werk wat jy met PoArt seël:**

- **Wiskundige Bewys:** As selfs een pixel van jou fêer verander, weet die stelsel dit. Manipulasie is onmoontlik.
- **Wetlike Grondslag:** Watter datum, watter stad, vanaf watter toestel die werk verseël is, is opgeskryf.
- **Onmiddellike Sertifikaat:** Dit genereer 'n spesiale **"Bate Identiteit Sertifikaat"** vir jou binne sekondes, met QR kode en verseël.

---

## ⚙️ Stelsel Argitektuur en Tegniese Kenmerke

Die stelsel is ontwerp op "Serverless" argitektuur, met fokus op hoë werkverrigting en skaalbaarheid.

| Laag | Tegnologie | Beskrywing |
|--------|-----------|-------------|
| **Enkripsie** | SHA-256 & SHA-512 | Twee-vlak kriptografiese opsomming |
| **Databasis** | Supabase (PostgreSQL) | JSONB data struktuur, RLS beleide |
| **Forensiese Data** | ipapi.co API | IP/Ligging/Tyd driehoek |
| **Vertoning** | html2canvas + jsPDF | Kliënt-kant PNG/PDF generasie |
| **Frontend** | Vanilla JavaScript | Zero raamwerk afhanklikheid |
| **Sekuriteit** | Kliënt-kant hashing | Fêer gaan nooit na bediener |

### Opvallende Kenmerke

| Kenmerk | Beskrywing | By Mededingers? |
|---------|-------|-----------------|
| **UI Sleep & Los** | Sleep en los fêer, onmiddellike voorskou | ❌ Nie by meeste |
| **Veelvuldige Formaat Uitvoer** | PNG, JSON, PDF - een klik | ⚠️ Beperk |
| **Regtydse Voorskou** | Sertifikaat voorskou direk | ❌ Niks |
| **Privaatheid Kontroles** | Privaat/Gemaskeer/Openbaar keuses | ❌ Niks |
| **Kliënt-Kant Hash** | Fêer gaan nooit na bediener | ✅ Net by paar |
| **Forensiese Metadata** | IP, ligging, toestel, tyd - alles saam | ❌ Verdeel |
| **QR Verifikasie** | Onmiddellike verifikasie QR kode | ⚠️ Beperk |
| **Spoed Beperking** | Spam beskerming (RLS + Kliënt) | ❌ Nie by meeste |

---

## 🗺️ Padkaart: Toekoms "Sonder Vertroue"

Die huidige weergawe **(Beta v1.0)** is ontwerp om eindgebruikers maksimum spoed, maklike koppelvlak en gratis toegang te gee. Ons uiteindelike visie is egter die oorgang na 'n struktuur waar selfs die databasis bestuurder (ons) nie kan inmeng nie.

### Fase 1: Beta (Leef Nou)

- **Infrastruktuur:** Wolk Databasis (Supabase).
- **Doel:** Spoed, verwyder UX (Gebruikerservaring) hindernisse en ooreenstemming. Verskaf "wrywinglose" sekuriteit.

### 🚀 Fase 2: (Backend / Rand Werk Vereistes)

Hierdie fase behels die oorgang vanaf "kliënt-kant" algehele werking struktuur na 'n "Bediener Kant Gesag" struktuur met meer sekuriteit en beheerbaar.

| Item | Wat Bring Dit? | Tegnologie Stapel | Prioriteit |
|-------|---------------|------------|---------|
| **`INSERT` → Rand Funksie** | Voorkom spam + API sleutel sekuriteit | Supabase Edge (Deno) | 🔴 Hoog |
| **Beursie Handtekening** | Kriptografiese verifikasie | Solana Wallet Adapter | 🟡 Medium |
| **IPFS/Arweave Rugsteun** | Gedekentraliseerde onveranderlikheid | IPFS SDK + Pinata | 🟢 Laag |
| **Kansellasie Prosedure** | Kanselleer vals sertifikate | Opdateer DB Skema | 🔴 Hoog |
| **Oorsig Loglêer** | Wetenskaplike navraag rekord | Spesiale rekord tabel | 🟡 Medium |
| **OpenTimestamps** | Bitcoin anker | OTS JavaScript | 🟢 Laag |
| **DID Integrasie** | Gedekentraliseerde Identiteit | ION/Ceramic | 🟢 Laag |

### Fase 3: Volle Desentralisasie (Langter myn)

| Kenmerk | Doel | ETA |
|---------|------|-----|
| **Blockchain Register** | On-chain registrasie Ethereum/Solana | Q4 2026 |
| **DAO Bestuur** | Gemeenskap bestuur | Q1 2027 |
| **Multi-Ketting Ondersteuning** | Polygon, Arbitrum, Base | Q2 2027 |
| **Wetlike Erkenning** | Geldigheid in Turkse howe | 2027-2028 |
| **API vir Ontwikkelaars** | Openbare API eindpunt | Q3 2026 |

---

## 📊 Mededingende Analise (Opgedateer)

PoArt staan in die "Sweet Spot" wat die leemtes van bestaande oplossings vul.

| Kenmerk | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Koste** | 🆓 Gratis | 🆓 | 💰 Betaald | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI Sleep & Los** | ✅ Baie Maklik | ❌ CLI | ⚠️ Medium | ⚠️ Medium | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Veelvuldige Formaat Uitvoer** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Regtydse Voorskou** | ✅ Direk | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privaatheid Kontroles** | ✅ 3 Modusse | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Kliënt-Kant Hash** | ✅ Privaatheid | ✅ | ❌ Oplaai | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensiese Metadata** | ✅ Volledig | ❌ | ❌ | ⚠️ Beperk | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verifikasie** | ✅ Onmiddellik | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Spoed Beperking** | ✅ RLS+Kliënt | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anker** | 🔄 Padkaart | ✅ Bitcoin | ✅ Ethereum | ✅ Veelvoudig | ✅ | ✅ | ✅ | ✅ |
| **Oopbron** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Turkse Ondersteuning** | ✅ Inheems | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Sleutel:**
- ✅ : Volle ondersteuning / beskikbaar
- ⚠️ : Beperk / in betaalde planne
- ❌ : Niks / nie ondersteun
- 🔄 : In padkaart (word ontwikkel)
- 🆓 : Heeltemal gratis
- 💰 : Betaald / registrasie benodig

### Mededingers se Leemtes, PoArt se Sterkpunte

| Leemte | Mededingers | PoArt |
|-------|-------------|-------|
| **Gebruik Moeilikheid** | CLI, API kennis, beursie benodig | Sleep en los, gereed met 3 klieke |
| **Koste Hindernis** | Registrasie $50-500/maand | 100% gratis |
| **Privaatheid** | Fêer opgelaai na bediener | Kliënt-kant, fêer gaan nooit |
| **Forensiese Data** | Net tydstempel | IP, ligging, toestel, tyd - alles |
| **Turkse Ondersteuning** | Niks of baie beperk | Inheemse taal ondersteuning |
| **Oopbron** | Geslote boks | Alle kode oop op GitHub |

---

## 🧬 Protokol Data Struktuur (JSON Schema)

**Elke [PoArt] sertifikaat het 'n dragbare en verifieerbare JSON identiteitskaart gegenereer volgens die volgende standaard.**

> **Let wel:** Hierdie JSON identiteit formaat is die sertifikaat formaat wat aan gebruikers voorgelê word. In register rekords word `registry.asset` gebruik in plaas van `identity.asset_data` (kartering: `identity.asset_data` == `registry.asset`).
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

## 🔬 Tegniese Diepte: Seël Algoritme

### Bepaalbare Hash Funksies
```javascript
// Hulp Funksies: Skakel opsomming om na hexadecimale string
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Skakel string om na byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Kanonieke forensiese string generasie (v1.0: vaste veld volgorde + UTF-8 + skeier \n)
// Fase 2 waarheid: Oorgang na kanonieke JSON met RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal Generasie Proses (Volledig Bepaalbaar)
```javascript
// 1. FileHash Berekening (kliënt-kant)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Forensiese data versameling (gebruik van enkele tydstempel)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Enkele tydstempel generasie
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

// 3. EvidenceRoot konstruksie (met kanonieke enkripsie)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal generasie (gebruik van dieselfde tydstempel)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Maskering hulp funksies (IPv4 en IPv6 ondersteuning)
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

### Verifikasie Vloei (Twee Vlakke)

#### Quick Verify (Vinnige Verifikasie)
```javascript
// Verifieer net fêer hash (vinnige rooi vlag)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Kry van register
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Hash vergelyking
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Outentiek - Fêer hash stem ooreen"
    };
  } else {
    return {
      valid: false,
      message: "❌ Vals - Fêer is gemanipuleer"
    };
  }
}
```

#### Full Verify (Volle Verifikasie)
```javascript
// Hergenereer en verifieer EvidenceRoot en NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Kry van register
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash Verifikasie (vinnige rooi vlag)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Vals - Fêer hash stem nie ooreen" };
  }

  // 2) Hergenereer EvidenceRoot (met forensiese data gestoor in register)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Stem nie ooreen - EvidenceRoot staan nie" };
  }

  // 3) Hergenereer NotarySeal (met dieselfde tydstempel + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Stem nie ooreen - NotarySeal staan nie" };
  }

  // Opsioneel: In Fase 2, verifieer ook signer_sig met attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Ongeldige handtekening" };

  return { valid: true, message: "✅ Outentiek - Volle verifikasie geslaag" };
}
```

> **Kritiese Waarhede:**
> - **Quick Verify:** Verifieer net fêer hash vir vinnige gebruik.
> - **Full Verify:** Verifieer alle protokol vlakke (EvidenceRoot + NotarySeal).
> - Alle hash operasies word bepaalbaar uitgevoer met vaste enkripsie en vaste skeiers.
> - **Huidige standaard v1.0:** Vaste veld volgorde + UTF-8 enkripsie + skeier `\n`.
> - **Fase 2 Plan:** Oorgang na kanonieke JSON met RFC 8785 (JCS - JSON Canonicalization Scheme).
> - In maskeer modus word EvidenceRoot en NotarySeal berekening gedoen met gemaskeerde forensiese data; dus bly verifikasie bepaalbaar.
> - Enkele tydstempel word gebruik regdeur die proses (forensies + NotarySeal); bepaalbaarheid is gewaarborg.
> - **Forensiese veld name:** `ip_masked`, `location`, `device`, `timestamp` (kode en register stem presies ooreen).
> - **Register pad:** `certificate.asset.fingerprints` (stem presies ooreen met verifikasie kode).
> - **signer_sig in register:** Die `proof.signer_sig` veld is nodig vir Volle Verifikasie.
> - SignerSignature prosedure sal geaktiveer word in Fase 2 met Solana Wallet Adapter; in v1.0 kan verifikasie met `attestation_pubkey` gedoen word.

---

## 📈 Gebruik Statistieke (Q1 2026 Doelwitte)

| Metriek | Teiken | Status |
|--------|--------|--------|
| **Totaal Sertifikate** | 1,000 | 🔄 Aan die gang |
| **Aktiewe Gebruikers** | 500 | 🔄 Aan die gang |
| **Verifikasie Tel** | 5,000 | 🔄 Aan die gang |
| **Uptime** | 99.9% | ✅ Leef |
| **Gemiddelde Reaksie Tyd** | <200ms | ✅ Uitstekend |

---

## 🌍 Gemeenskap en Ondersteuning

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Webwerf:** [ilhanart.org](https://ilhanart.org)
- **E-pos:** galeri@ilhanart.org

---

## 🙏 Bydraers

Die PoArt protokol groei voort met bydraes van die oopbron gemeenskap.

**Om by te dra:**
1. Fork die repository
2. Skep 'n kenmerk tak (`git checkout -b feature/amazing-feature`)
3. Commit (`git commit -m 'Add amazing feature'`)
4. Stoot (`git push origin feature/amazing-feature`)
5. Maak 'n Trek Versoek oop

### 🛠️ Wat Het Ons Nou Nodig? (Hulp Oproep)

Die PoArt protokol soek ervare ontwikkelaars in die volgende areas vir **Fase 2** ontwikkeling:

* **Supabase Edge Funksies:** Skuif spam beskerming na bediener kant.
* **Solana Web3.js:** Beursie handtekening integrasie.
* **IPFS / Arweave:** Stoor en pin diensintegrasie.

> Asseblief begin 'n bespreking in die "Issues" oortjie voor om 'n kenmerk by te voeg.

---

**[PoArt] Proof of Art Protokol v1.0**  
*"Kultuur > Kapitaal"*

## 🧾 Lisensie

MIT Lisensie © 2026 Ilhan Art Gallery Initiative

Sien [![Lisensie](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) vir volledige terme.

---

## 💬 Erkennings

![Weergawe](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Sekuriteit](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![Lisensie](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Hierdie projek word ontwikkel deur die [Ilhan Art Gallery] inisiatief, en sy bronkode is openlik beskikbaar vir deursigtigheid.**

**PROTOKOL V1.0 // VERSEËL MET SHA-512**

*© 2026 İLHAN ART | ALLE REGTE VOORBEHOU VIR KUNSWERKE, BEELDE EN IDEES.*

---
