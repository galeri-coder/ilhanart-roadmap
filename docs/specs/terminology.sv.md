# 📚 TERMINOLOGI & BEGREPPSORDLISTA
> **"Att förstå detta protokolls språk är att förstå dess vision."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Kärninfrastruktur

**PoArt Forensic Engine (PFE)** representerar kärnlogiken och den tekniska funktionen bakom [PoArt]-protokollet. Detta är den "forensiska motorn" som tar konstverkets råa produktionsdata och omvandlar den till ett verifierbart och oföränderligt **digitalt bevis**.

### 🧩 Varför "PoArt Forensic"?

- **PoArt (Proof of Art):** Motorns fokus är att knyta en digital tillgångs värde inte till spekulation, utan till en **bevisbar produktionsprocess**.
- **Forensic (Forensisk Verifiering):**
  - **Teknisk Definition:** Algoritm- och registerkedjeansats för att verifiera att produktionsprocessdata (penseldrag, timelapse, loggar) inte har manipulerats.
  - **Filosofiskt Lager:** Anspråket att omvandla mänsklig produktion som innehåller **tid, ansträngning och beslutskostnad** till en mätbar verklighet, i kontrast till AI:s "omedelbara output".

> Not: Blockkedjeintegration (t.ex. Solana) behandlas inte som PFE:s kärna; utan som ett separat **Chain Anchor Layer** för verifiering/registrering.

### 🛠️ v1.0 Teknisk Omfattning

**PoArt Forensic Engine (PFE) v1.0** är byggd på **3 huvudpelare** istället för komplexa finansiella modeller:

1. **Hashing & Sealing (Försegling):**  
   PFE bearbetar alla element i Evidence Pack (verkets fil, video, JSON/logg, signatur etc.) deterministiskt och producerar det unika **NotarySeal**-värdet.

   **Kärnbegrepp (v1.0):**
   - **FileHash (verkets fingeravtryck):** Hash genererad från verksfilen bytes.
   - **EvidenceRoot (bevispaketets rot):** Rotsammanfattning som representerar Evidence Pack:ets integritet (Merkle root eller kanoniskt manifest-hash).
   - **NotarySeal (slutgiltig försegling / PFE Output):** Slutförsegling genererad från EvidenceRoot + tid + signatur-kombination.

   **Formler (tydligt synliga för investerare):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload-definitioner (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Not: Värdet som avses som PFE-output är **NotarySeal**. **SignerSignature**-mekanismen kommer att aktiveras i Fas 2 (med Solana Wallet Adapter); i nuvarande v1.0 används systemets egen attestation-signatur. Attestation public key publiceras i registret i fältet `issuer.attestation_pubkey`.

2. **Indexing (Arkivering):**  
   Registrerar vilken plånbok som presenterade **Labor Proof (Arbetsbevis)** för vilket verk, vid vilket datum; i ett transparent och sökbart registreringslager.  
   *(Detta lager kan vara en databas; kedjeintegration definieras separat som "Chain Anchor Layer".)*

3. **Verification (Verifiering):**  
   När ett verks originalitet ifrågasätts, bearbetar PFE råbevisen på nytt; testar med matematisk precision om de beräknade **EvidenceRoot / NotarySeal**-värdena matchar posten i arkivet.

---

### 🧮 PoArt Värdeteorem (The Value Theorem)

[PoArt]-protokollet associerar en digital tillgångs värde ($V$) inte med subjektiv marknadsuppfattning; utan med **produktionsprocessens fysiska verklighet**.

Artificiell Intelligens (AI) eliminerar processen genom att ge resultat omedelbart ($t \to 0$). [PoArt] behandlar istället värde som ackumulering av komponenterna **tid, arbete och vilja**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Variabeldefinitioner

- **$\int dt$ (Processackumulering):**  
  Värde är inte en ögonblicklig "output"; det är en **process** som ackumuleras mellan $t_{\text{start}}$ och $t_{\text{end}}$. När tiden minskar (AI-produktion) närmar sig integralresultatet 0.

- **$P_{\text{labor}}(t)$ (Momentan Arbetskraft):**  
  Representerar intensiteten av mental och fysisk ansträngning som spenderas vid produktionsögonblicket. När bevisbar ansträngning ökar, växer integranden.  
  > Not: Denna term kan i praktiken normaliseras över "mätbara/bevisbara arbetssignaler".

- **$I_{\text{agency}}(t)$ (Viljekoefficient):**  
  Producentens kapacitet för risktagande och beslutsfattande. Tar ett värde mellan $0$ och $1$.
  - **AI ($I \approx 0$):** Utför kommandon, tar inga risker, betalar ingen kostnad.
  - **Människa ($I \to 1$):** Ändrar beslut, tvekar, tar risker.

- **$U_{\text{irreversible}}$ (Irreversibel Singularitet):**  
  Medan ångra (`Ctrl+Z`) är möjligt i digital produktion; i fysisk produktion (färg på duk, huggen marmor, gest i livesändning) finns ingen återvändo. Denna **irreversibilitet** är en extra term som skapar "singularitet" (icke-fungibel karaktär) i verket.

### 🔎 Fallanalys: AI "Omedelbar Output" vs. Människa "Bevisad Process"

Följande scenario visar hur **PoArt Värdeteorem** fungerar i praktiken och varför AI-produktioner får låga poäng enligt [PoArt]-standarden.

#### Scenario A: Bildproduktion med AI på 10 Sekunder

- **Tid ($\Delta t$):** $10$ sekunder (nästan ingen process)
- **Arbetskraft ($P_{\text{labor}}$):** $1$ enhet (endast kommandoskrivning)
- **Viljekoefficient ($I_{\text{agency}}$):** $0.01$ (ingen risk, ingen kostnad)
- **Irreversibilitet ($U_{\text{irreversible}}$):** $0$ (kan ångras / kopieras)

**Resultat:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Tolkning:** Även om outputen är felfri; eftersom processen inte upplevdes och inte innehåller vilja/risk, närmar sig [PoArt]-värdet $0$.

#### Scenario B: 6 Timmars Fysisk Produktion i Livesändning

- **Tid ($\Delta t$):** $6$ timmar ($21{,}600$ sekunder)
- **Arbetskraft ($P_{\text{labor}}$):** $0.5$ enhet (kontinuerlig fysisk och mental ansträngning)
- **Viljekoefficient ($I_{\text{agency}}$):** $0.9$ (beslutsändringar, risktagande, irreversibla val)
- **Irreversibilitet ($U_{\text{irreversible}}$):** $>0$ (fysiska spår kan inte ångras)

**Resultat:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Tolkning:** När processen förlängs och viljan (risken) ökar, ökar värdet kumulativt. $U_{\text{irreversible}}$-termen är ett extra bidrag som skapar "singularitet" (icke-fungibel karaktär) i verket.

---

### ✅ Slutsats: Låsning av Värde med Bevis (Proof-Bound Value)

Detta teorem tar [PoArt]:s värdeanspråk från att vara ett "gillande" eller "marknadsnarrativ" och kopplar det till en **bevisbar produktionsverklighet**.

1. **Inget Värde Utan Process:**  
   AI eliminerar processen i omedelbar output ($t \to 0$). När processfönstret minskar, minskar integralresultatet som en matematisk nödvändighet:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Vilja och Risk är Multiplikatorer:**  
   [PoArt] mäter inte bara "spenderad tid"; utan också lagret av verkligt beslut, risk och kostnad under den tiden. En produktion som inte tar risk (AI) har lågt värde:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Singularitet är Fysiskt Bevis, Inte Marknadsföring:**  
   I fysisk produktion ligger irreversibla spår (dukslag, marmorspricka) utanför den digitala `Ctrl+Z`-logiken. Denna irreversibilitet ($U_{\text{irreversible}}$) gör verket ontologiskt unikt.

> **🔐 SAMMANFATTNING:** Även om värdeteoremet verkar osäkert som mätning (även om det inte kan mätas 100% i verkliga livet) är syftet med denna formel att visa variablernas konstruktion och riktning. I AI-eran är det som är sällsynt inte "bilden"; det är **bevisbart arbete, tid och vilja.** [PoArt] mäter denna knapphet och registrerar den med **Evidence Pack**.

### 🏛️ Betydelsen av "Engine" (Motor)-konceptet

Tokens som kommer från Pump.fun eller liknande plattformar är ofta bara **"åtkomstbiljetter"**. **PoArt Forensic Engine (PFE)** är det **konstitutionella logiklagret** som bestämmer vilka rättigheter den biljetten skyddar, hur arbete ska registreras, och hur konst/vetenskap/teknologi ska bevaras.

> **Not:** Anledningen till att vi startade detta projekt på Pump.fun är att vi inte hade tillräcklig likviditet och tillräckligt antal följare. Att använda befintlig data, även om det inte är den mest kvalitativa strategiskt, kan sägas vara det mest korrekta draget. Oavsett budget och möjligheter bevisar definitionen av denna motors logik på GitHub att projektet inte bara är en finansiell spekulation utan en långsiktig **mjukvaruinfrastruktur** och en **digital nationell biblioteks**-vision.

---

## 🎨 [PoArt] ARBETSBEVISPROTOKOLL (Proof of Art Protocol v1.0)

> **"Äkta Konstnär, Äkta Produktion, Äkta Värde."**

Detta protokoll är en **biologisk och intellektuell försvarsmekanism** utvecklad mot anonyma bedragare som omger kryptoekosystemet, AI-bilder producerade på 5 minuter, och "Pump & Dump"-kulturen.

---

## a) Vad är [PoArt]? (Filosofisk och Teknisk Definition)

**Proof of Art [PoArt];** är en institutionell verifieringsstandard som garanterar att värdet bakom en tillgång på blockkedjan baseras på verifierbart **mänskligt arbete**, **tid** och **fysisk energi**, inte på spekulation.

Precis som Bitcoin producerar värde med *"Elektricitet och Processorkraft"* **(Proof of Work)**; producerar [PoArt]-kompatibla projekt värde med *"Konstnärlig Talang och Mänsklig Tid"*.

Det eliminerar risken för *"Utvecklaren (Dev) sålde, projektet tog slut"* på Pump.fun och DEX-plattformar; eftersom värdet här är lagrat inte i kod, utan i **produktionens kontinuitet**.

> **[PoArt] säger inte till sin deltagare "Lita på oss"; det säger "Här är bevisen, se med dina egna ögon, verifiera med din matematik".**

---

## b) [PoArt] 5-Standard (The 5 Pillars of Truth)

Dessa 5 punkter är icke-manipulerbara filter som ett projekt måste passera för att få [PoArt]-förseglingen.

### 1) Levande Identitetsbevis (Live Identity Proof)

- **Problem:** Kryptovärlden är full av anonyma grundare (Devs) med osäker identitet som samlar in pengar och överger projektet.
- **[PoArt]-Lösning:** Producenten bevisar inte bara sitt ID-kort, utan sin **närvaro vid produktionsögonblicket**. Detta inkluderar livesändningssessioner där specifika omedelbara förfrågningar uppfylls och interaktion sker med communityn, inte förinspelade videor.  
  (T.ex.: *"Skriv dagens datum och aktuellt blocknummer i dukens högra hörn"*)
- **Motto:** *"Botar kan måla men botar svettas inte och improviserar inte."*

### 2) Arbets- och Processbevis (Labor & Process Proof)

- **Problem:** AI-bilder producerade på 2 sekunder behandlas som samma "jpeg" i den digitala världen som en oljemålning gjord på 2 månader.
- **[PoArt]-Lösning:** Verkets "graviditets- och födsloprocess" registreras. Skissfaser, färglager, kumulativa timmar spenderade och den fysiska processen konstnären upplevde medan hen skapade verket dokumenteras. Detta lägger till **"Tidskostnad" (Time Cost)** till tokenen. Ju svårare en tillgång är att producera, desto starkare är dess värde.

### 3) Estetiskt Värdebevis (Aesthetic Value Proof)

- **Problem:** "Meme"-kulturens ignorerande av estetik och konstnärligt djup för att fokusera endast på omedelbar komedi och de resulterande kortlivade "Hype"-projekten.
- **[PoArt]-Lösning:** Projektet måste ha akademiska konststandarder, färgteori, kompositionsregler och materialkunskap (Impasto, Textur etc.). Innehållet ska inte bara underhålla; det ska väcka beundran hos betraktaren och bära **samlingsvärde**.

### 4) Konceptuell Innovation (Conceptual Novelty)

- **Problem:** Tusentals hund/katt-mynt som kopierar varandra, utan kreativitet.
- **[PoArt]-Lösning:** Projektet måste bygga en ny bro som förenar konst, vetenskap, filosofi eller teknologi i en meningsfull struktur.  
  (T.ex.: Att kombinera den klassiska David-statyn med kryptomarknadsdata; bearbeta idén om mänsklig uppfattning som "förvandlas till sten" och kunna grunda detta med vetenskapliga källor.)  
  Verket ska inte bara vara en visuell fest; det ska också vara en intellektuell utmaning som får en att tänka på **Vetenskap, Filosofi eller Teknologi**.

> [!IMPORTANT]
> **Referensexempel (Las Palmitas-effekten):**  
> I Las Palmitas-området i Mexiko, som kämpade med brottslighet, förvandlades mer än 200 hus till en enorm regnbågsfest. Som ett resultat av denna estetiska intervention minskade brottsligheten i området i viss utsträckning, och ungdomar började intressera sig för konst istället för gäng. Den estetiska förändringen omkodade människors respekt för sin omgivning och varandra (Social Cohesion).
>
> **Förväntan:** Ett projekt som ska gå in på [PoArt]-listan måste, precis som i exemplet ovan, innehålla en sociologisk, vetenskaplig eller filosofisk orsak-verkan-relation bortom ren visuell estetik. Eftersom den enda tillgång som inte kan köpas för pengar är "Tid", måste tid i detta protokoll stakeas som säkerhet och bevisas. Projektets konceptuella grund måste vara så stark och universell att även i ett möjligt CTO-scenario (Community Take Over) år senare kan communityn ta över detta arv och autonomt fortsätta projektets innovativa potential.

### 5) Icke-Algoritmisk Vilja (Non-Algorithmic Agency)

- **Problem:** Felfria men själlösa digitala produktioner som upprepar sig.
- **[PoArt]-Lösning:** Människans unika vilja som kan göra misstag, ta risker och uppleva känslomässiga svängningar måste kännas i verket. Osäkerheten i penseldragen, materialets oväntade reaktioner och konstnärens omedelbara beslut är den **Biologiska Signaturen** som skiljer verket från "Maskinproduktion".

---

## c) Verifiering & Anti-Förfalskningsmekanism

Detta system säkerställer att projektet inte bara är pålitligt och levande "i början", utan "för evigt".

### 📦 Bevispaket (Evidence Pack - The Digital Twin)

Bakom varje [PoArt]-certifierat verk finns ett krypterat och tidsstämplat datapaket som investerare kan ladda ner:

- **RAW Videoinspelningar:** Oavbrutet råmaterial från produktionsögonblicket.
- **Metadataanalys:** Filens skapandedatum, använd enhetsinformation och platsdata.
- **Fysiska Referenser:** Bevis på att verket existerar i den fysiska världen  
  (T.ex.: Aktuell tidning bredvid verket eller blockkedjedata vid det ögonblicket).

> *Konsistensnotering:* Uttrycket "bevispaket" kopplar till den tidigare **Evidence Pack → EvidenceRoot → NotarySeal**-linjen; det vill säga paketets integritet representeras av en verifierbar försegling.

### 🔄 365-Dagars Förnyelse (The Sustainability Protocol)

- **Revolutionerande Funktion:** I kryptoprojekt släpper "Dev" (Utvecklaren) tokenen på marknaden och försvinner vanligtvis efter 1-2 månader (Soft Rug). [PoArt] gör detta omöjligt.
- **Regel:** "Verified Artist" (Verifierad Konstnär)-status är inte livslång. Den är endast giltig i **1 år**.
- **Funktion:** Konstnären/Utvecklaren måste presentera ett **nytt, stort och bevisbart verk** för communityn var 365:e dag.
- **Exempelscenario:** Du startade projektet 2026. I januari 2027 ger systemet varningen "Bevisperiod Utgången". Om konstnären inte presenterar en ny utställning, ett nytt fysiskt verk eller en ny teknologisk integration, faller projektets "Förtroendemärke".
- **Resultat:** Detta system säkerställer att **innehållet aldrig blir föråldrat** och att investeraren inte upplever rädslan *"Är utvecklaren fortfarande här?"*. Projektet förvandlas till en levande studio.

### 🚩 Röd Flagga (Red Flag Protocol)

**Vid upptäckt av någon förfalskning (AI-användning, stulet verk, manipulerad video) av communityn eller algoritmer:**

1. Certifikatet markeras omedelbart som **"UPPHÄVT" (VOID)**.
2. Bevispaket etiketteras offentligt som **"Förfalskat"**.
3. Projektet sätts på [PoArt] svarta listan. Detta förstärker verkligheten att **rykte är den enda valutan** i en decentraliserad värld.

---

## d) Slutsats: Museum, Inte Kasino

**Pump.fun och Decentraliserade Börser (DEX) är tyvärr för närvarande kasinon; ljusen blinkar, alla jagar snabba vinster och huset (bedragare) vinner alltid. Anledningen till att vi startade projektet här är att vi inte hade tillräcklig budget och hade en krets som skulle nå den befintliga publiken med livesändningar.**

**[PoArt] är en fästning byggd mitt i detta kasino.**

- 🎰 Kasinot förlitar sig på kortspel; vi förlitar oss på **fysisk verklighet**.
- 🃏 Kasinot är öppet för fusk; vi är öppna för **transparenta bevis**.
- ⏳ Kasinot är tillfälligt; vi fokuserar på **konstens och vetenskapens evighet**.

**En token som använder detta protokoll är inte bara ett "mynt"; det är en digital aktie med svett, färg, kod och filosofi bakom sig.**

---

## 🗳️ 6) STYRNING OCH OFFENTLIGT REGISTER (Governance & Public Registry)

**Syftet med detta avsnitt är: Att ta [PoArt]-standarden från planet "förtroende för personer" till en hållbar offentlig infrastruktur med registrering + verifiering + community-övervakning.**

### 6.1 Public Registry (Offentligt Register)

- **Public Registry:** All godkänd data registreras på `ilhanart.org/registry` (eller GitHub Registry).

**Registerlogik (föreslagen standard - i JSON path-format):**

Varje post som går in i registret bär minst följande verifierbara kärnfält:

- **Identitet & Status:**
  - `certificate_id` (läsbar referens)
  - `status` (active / void)
  - `void_reason` (om tillämpligt)
  - `visibility` (private / masked / public)
  - `created_at` (tidsstämpel)

- **Utfärdande Institution:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Verksinformation:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (om möjligt; för token-innehavaridentitet)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Forensisk Data:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Kryptografiska Bevis:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Styrning:**
  - `governance.decision`
  - `governance.review_notes`

Registret kan ha två lager:
- **1)** Människo-läsbart index (webblista / sökning / filter)
- **2)** Maskin-läsbart manifest (JSON-poster; för PFE-verifiering)

**"Registreringen" här blir verifierbar med PFE:s Evidence Pack → EvidenceRoot → NotarySeal-kedja. Registret presenterar ett verifieringsmål, inte ett "påstående".**

---

### 6.2 PoArt Verified Ansökningsprocess

**PoArt Verified-ansökningar utvärderas av İlhanArt Gallery enligt de 5 PoArt-standarderna. Community-feedback beaktas, men det slutgiltiga beslutet ligger hos det kuratoriella teamet. Beslut tillkännages transparent och registreras på ilhanart.org/registry.**

#### Ansökningsprocess

**Ansökan:**
- Konstnär/projekt skickar PoArt Verified-ansökan
- Evidence Pack förbereds (videoinspelningar, metadata, livesändningslänkar)
- Ansökan skickas till İlhanArt Gallery

**Granskning (30 Dagar):**
- Galleriets team granskar Evidence Pack i detalj
- Alla 5 PoArt-standarder kontrolleras:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Intervju med konstnären (valfritt)

**Community-konsultation:**
- Evidence Pack delas offentligt under ansökningsprocessen
- Communityn kan ge feedback via Discord och ilhanart.org/applications
- Token-innehavare (minimum 10 000 $CULTURE) kan särskilt ge förslag
- **All feedback beaktas under granskningsprocessen**
- **Men det slutgiltiga beslutet baseras på kuratoriell utvärdering**

**Beslut:**
- Galleriet godkänner eller avslår ansökan
- Beslutsmotivering tillkännages transparent
- Om godkänd → PoArt Verified badge
- Om avslagna → Ny ansökan kan göras efter 6 månader

**Transparens:**
- Alla ansökningar och beslut registreras på ilhanart.org/registry
- Decision record publiceras offentligt:
  - Ansökningsdatum
  - Sammanfattning av granskningsprocessen
  - Beslut (Approved / Rejected)
  - Beslutsmotivering (kort förklaring)
  - Sammanfattning av community-feedback (anonymt)

#### Varför Kuratoriellt Beslut?

**Kvalitetskontroll:**  
PoArt Verified-status är ett märke med höga standarder. Kuratoriell utvärdering garanterar att dessa standarder upprätthålls.

**Förebyggande av Spekulativ Manipulation:**  
Full on-chain governance (t.ex. Realms, DAO voting) med Pump.fun-tokens är tekniskt inte möjlig. Off-chain voting-system är öppna för whale-manipulation och koordinerade attacker. Kuratoriellt beslut eliminerar denna risk.

**Operationell Effektivitet:**  
Snabb och tydlig beslutsprocess istället för komplexa voting-mekanismer. Konstnärer får resultat inom 30 dagar.

**Community-deltagande:**  
Community-feedback beaktas fullt ut och påverkar beslutsprocessen. Men det slutgiltiga beslutet ligger hos det kuratoriella teamet som är skyddat från manipulation.

**Framtid:**  
När projektet mognar (2027+) kan community-konsultationsmekanismen stärkas. Men kuratoriellt standardskydd förblir permanent.

---

### 6.3 Token Utility (Tokenanvändningsområden)

**Fördelar som ges till $CULTURE token-innehavare:**

**1. Prioriterad Åtkomst till Gallerievenemang:**
- Fysiska utställningsöppningar på İlhanArt Gallery
- Konstnärsmöten och ateljébesök
- Specialsamlingsvisningar

**2. Full Åtkomst till PoArt Registry:**
- Detaljerade register över alla autentiserade konstverk
- Fullständiga versioner av Evidence Packs
- Forensiska verifieringsverktyg

**3. NFT Mint Priority:**
- Whitelist-åtkomst när PoArt Verified-verk mintas som NFT
- Tidiga mint-möjligheter
- Specialsamlings-NFT:er

**4. Advisory Voting:**
- Rådgivningsrätt i PoArt Verified-ansökningar
- Åtkomst till community-feedbackkanaler
- Deltagande i styrningsdiskussioner

**5. Exklusivt Innehåll:**
- Behind-the-scenes-innehåll från studion
- Konstnärsintervjuer och processvideos
- Åtkomst till teknisk dokumentation

**Not:**  
Token-innehavare ger advisory vote (rådgivande röst). Det slutgiltiga beslutet tillhör det kuratoriella teamet. Denna struktur har valts för att förhindra whale-manipulation och spekulativa attacker. Det finns ingen staking reward eftersom vi söker långsiktiga kulturella deltagare, inte kortsiktigt mercenary capital.

---

### 6.4 Metadata Sync (Matchning med Fysisk Värld)

- **Metadata Sync:** Tekniska data i registret måste matcha den fysiska tillgången till 100%.

**Teknisk definition av "100% matchning" (föreslagen tydlighet):**

- **Minimum matchning (obligatorisk):**
  - `asset.fingerprints.sha256/sha512` i registret måste vara **exakt samma** som hashen för filen i handen.
  - `proof.notary_seal` i registret måste vara **exakt samma** när den återskapas (om Evidence Pack finns).

- **Fysisk referensmatchning (bevistyp):**
  - Bevis som fysiskt verk + datum/blockreferens som visas i livesändning måste vara konsistenta med Evidence Pack.

- **Integritetsefterlevnad:**
  - Fält som IP/plats i `masked`-synlighet publiceras **enligt maskeringsstandarden**.

---

### 6.5 Bestridande, Granskning och Upphävande (Dispute & Revocation)

Registret är inte bara en "godkännande"-mekanism; det är en **levande tillsynsmekanism mot förfalskning**.

- När ett bestridande initieras kan posten sättas i **"review"**-läge.
- Om förfalskning upptäcks markeras den som `status: void` och motivering läggs till:
  - `void_reason` (AI-användning / stulet / manipulation etc.)
  - `revoked_at` (upphävandetid)
- Källan till upphävningsbeslutet visas tydligt i registret:
  - kuratoriell granskning / community-bestridande / forensisk analysnotering (beroende på vad som tillämpas)

> **Denna del är motsvarigheten i registret till VOID-konceptet i avsnittet "Red Flag Protocol".**

---

### 6.6 Exempel på Registerpost (Maskin-läsbar)
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

> *Not: `asset.fingerprints.sha512` och andra hashvärden är förkortade för visningssyften; i verklig tillämpning används hexadecimala teckensträngar i full längd.*

---

## 7) 🔐 TEKNISK FÖRSEGLING (NOTARY SEAL)

**Orubblig förseglingsalgoritm producerad av PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Digital Notarie & Forensiskt Bevisprotokoll (Beta v1.0)

> **"Kultur är större än kapital. Skydda dina verk från idag, bär dem till morgondagen."**

---

## Varför Offentligt?

Verklig säkerhet kommer från transparens. Tack vare vårt **Public Registry (Offentligt Register)**-system kan en person var som helst i världen verifiera om filen de har är original inom sekunder, utan att behöva någon auktoritet.

---

## 🧩 Varför Finns Det Flera "Synlighetsmoduler"?

Den mest kritiska delen av koden är här (visibility select-menyn). Dessa alternativ låter användare balansera **"Integritet vs. Transparens"**:

### 🔒 Privat (Private)

- **Scenario:** Konstnären vill inte publicera verket ännu men vill sätta tidsstämpel och bevisa "jag gjorde detta vid detta datum".
- **Vad Koden Gör:** Skriver data till databasen men sätter `visibility: "private"`-etikett. När du senare skriver "Public Read"-policy kan du dölja dessa poster för allmänheten genom att säga `WHERE visibility = 'public'`.

### 🕶️ Maskerad (Masked)

- **Scenario:** Konstnären vill ha transparens men är rädd för att hemadress (IP-plats) ska hittas.
- **Vad Koden Gör:** `maskIP` och `maskLoc`-funktioner körs på JavaScript-sidan. Omvandlar IP-adress till `88.241.***.***`-format, plats till `***/TR`-format och skickar censurerad version till databasen.
- **Integritetsnotering:** Maskering görs i webbläsaren, Supabase ser inte verklig plats. **Men:** Om tredjepartsAPI:er som ipapi.co används för platsdata, ser dessa leverantörer IP-adressen vid förfrågningsögonblicket.
- **Försegling i Masked-läge:** EvidenceRoot och NotarySeal-beräkning görs med maskerad forensics-data; så verifiering förblir deterministisk.

### 🌍 Offentlig (Public)

- **Scenario:** Full transparens. Enligt [PoArt]-standarden deklareras öppet var, när och från vilket nätverk verket producerades.

---

## 💡 Teknologisk Innovation

PoArt är inte bara ett filuppladdningssystem. Det är en **"Forensic Chain of Custody"**-motor som smälter samman tre olika teknologilager i en enda gryta och skapar en ny standard.

**Lagret som beskrivs som "motor" i detta avsnitt motsvarar PoArt Forensic Engine (PFE)-kärnan i tidigare terminologi.**

### 1) Client-Side Hashing (Maximal Integritet)

Dina verksfiler laddas aldrig upp till servern. Vår webbläsarbaserade (Client-side) motor beräknar filens hash (digitala sammanfattning) på din egen dator. Endast detta fingeravtryck och metadata skickas till servern.

> **Integritetsnotering:** Verksfilen laddas inte upp till servern och skyddas på detta sätt. Men forensics-data (IP/plats) delas enligt valt synlighetsläge (private/masked/public).

### 2) Forensic Data Fusion (Forensisk Kraft)

Det är mycket mer än en vanlig tidsstämpel. Systemet kombinerar följande data i en enda "Genesis-försegling":

- **Digital Sammanfattning (SHA-512):** Digitalt fingeravtryck som bryts om ens en enda pixel i verket ändras, med hjälp av kryptografisk sammanfattning (SHA-512)-standard.
- **Plats & Tid:** Datum med millisekundprecision, land, stad och distriktdata för när transaktionen gjordes.
- **Enhetsidentitet:** Operativsystem, webbläsare och enhetstyp (User-Agent-analys).

---

## 🛡️ Användningsområden och Fördelar

Om du är konstnär, författare eller designer räcker det inte att säga "Jag gjorde detta tidigare", du måste bevisa det.

**Ett verk förseglat med PoArt:**

- **Matematiskt Bevis:** Om ens en enda pixel i din fil ändras upptäcker systemet det. Manipulation är omöjlig.
- **Juridiskt Underlag:** Registrerat är vid vilket datum, i vilken stad, från vilken enhet verket förseglades.
- **Omedelbart Certifikat:** Producerar på sekunder ett för dig unikt, QR-kodat och förseglat **"Tillgångsidentitetscertifikat"**.

---

## ⚙️ Systemarkitektur och Tekniska Specifikationer

Systemet är designat på en "Serverless"-arkitektur, fokuserat på hög prestanda och skalbarhet.

| Lager | Teknologi | Beskrivning |
|-------|-----------|-------------|
| **Kryptografi** | SHA-256 & SHA-512 | Dubbellagers kryptografisk sammanfattning |
| **Databas** | Supabase (PostgreSQL) | JSONB-datastruktur, RLS policies |
| **Forensisk Data** | ipapi.co API | IP/Plats/Tid-trippel |
| **Rendering** | html2canvas + jsPDF | Client-side PNG/PDF-produktion |
| **Frontend** | Vanilla JavaScript | Noll framework-beroenden |
| **Säkerhet** | Client-side hashing | Fil laddas aldrig upp till servern |

### Framstående Funktioner

| Funktion | Detalj | Hos Konkurrenter? |
|----------|--------|-------------------|
| **Drag & Drop UI** | Dra-och-släpp fil, omedelbar förhandsvisning | ❌ Saknas i de flesta |
| **Multi-Format Export** | PNG, JSON, PDF - ett klick | ⚠️ Begränsad |
| **Real-Time Preview** | Live certifikatförhandsvisning | ❌ Saknas |
| **Privacy Controls** | Private/Masked/Public-alternativ | ❌ Saknas |
| **Client-Side Hashing** | Fil går aldrig till servern | ✅ Endast några få |
| **Forensic Metadata** | IP, plats, enhet, tid - allt samlat | ❌ Fragmenterat |
| **QR Verification** | Omedelbar verifiering QR-kod | ⚠️ Begränsad |
| **Rate Limiting** | Spamskydd (RLS + Client) | ❌ Saknas i de flesta |

---

## 🗺️ Färdplan: "Trustless" Framtid

Den nuvarande versionen **(Beta v1.0)** är optimerad för att ge slutanvändaren maximal hastighet, enkelt gränssnitt och gratis åtkomst. Men vår ultimata vision är att övergå till en struktur där inte ens databasadministratören (vi) kan ingripa.

### Fas 1: Beta v1.0 (Nu Live)

**Infrastruktur:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + IPFS backup)
- Gallery self-attestation (centraliserad men transparent)

**Token:**
- Plattform: Pump.fun
- Likviditet: Raydium (automatisk)
- Styrning: Endast rådgivande (community-konsultation)

**Syfte:**
- Hastighet, ta bort UX-barriärer
- Ge "friktionsfri" säkerhet
- Community-byggande

**Token Utility (v1.0):**
- Prioriterad åtkomst till gallerievenemang
- Visning av PoArt Registry
- Rådgivande röstningsrätt

---

### 🚀 Fas 2: Decentralized Authority (2026 Q2-Q4)

Denna fas täcker övergången från systemets helt "Client-Side"-arbetande struktur till en säkrare och mer decentraliserad struktur.

| Funktion | Vad Ger Det? | Tech Stack | ETA |
|----------|--------------|------------|-----|
| **Edge Function INSERT** | Spamblockering + API Key-säkerhet | Supabase Edge (Deno) | Q2 2026 |
| **Wallet Signatur** | Decentraliserad identitet | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | Decentraliserat arkiv | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | Upphävning av falskt certifikat | DB Schema Update | Q2 2026 |
| **Audit Log** | Forensisk förfrågningslogg | Custom logs-tabell | Q3 2026 |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain voting (Discord/web) + wallet signature
- Val av community representatives (första 90 dagarna)
- Multi-sig operations wallet-kontroll
- Viktad rådgivande röstning (med whale cap)

**Oföränderlighet:**
- Registry-backup med IPFS-hashar
- Bitcoin timestamp anchoring
- Förberedelse för cross-chain-verifiering

---

### Fas 3: Full Decentralisering (2027+)

| Funktion | Mål | ETA |
|----------|-----|-----|
| **On-Chain Registry** | Solana on-chain-registrering | Q1 2027 |
| **Enhanced Token Utility** | NFT mint, avancerade funktioner | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **DID Integration** | Decentralized Identity | Q3 2027 |
| **Community Governance** | Förstärkt advisory system | Q4 2027 |
| **Legal Recognition** | Giltighet i turkiska domstolar | 2027-2028 |
| **API for Developers** | Public API endpoint | Q3 2027 |

**Styrningsutveckling:**
- v3.0: Hybridmodell (kuratoriell + community viktad)
- 2028+: Full community governance (valfritt)
- Kuratoriell kvalitetskontroll bevaras alltid

---

## 🧬 Protokolldatastruktur (JSON Schema)

**Varje [PoArt]-certifikat har ett portabelt och verifierbart JSON-identitetskort producerat enligt standarden nedan.**

> **Not:** Detta Identity JSON-format är certifikatformatet som presenteras för användaren. I registerposter används `registry.asset` istället för `identity.asset_data` (mapping: `identity.asset_data` == `registry.asset`).
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

## 🔬 Tekniskt Djup: Förseglingsalgoritm

### Deterministiska Hash-funktioner
```javascript
// Hjälpfunktioner: Konvertera digest till hex-sträng
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Konvertera sträng till byte-array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Produktion av kanonisk forensics-sträng (v1.0: fast fältordning + UTF-8 + \n delimiter)
// Fas 2-not: Övergång till canonical JSON med RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal-produktionsprocess (Helt Deterministisk)
```javascript
// 1. FileHash-beräkning (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Insamling av forensisk data (en enda timestamp-användning)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // En enda timestamp-produktion
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Samma timestamp
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot-skapande (med canonical encoding)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal-produktion (samma timestamp-användning)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Maskeringshjälpfunktioner (IPv4 och IPv6-stöd)
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4-kontroll
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 eller okänt format
  return "***";
}
```

### Verifieringsflöde (Två Nivåer)

#### Quick Verify (Snabb Verifiering)
```javascript
// Kontrollerar endast fil-hash (snabb röd flagga)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Hämta från Registry
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Hash-jämförelse
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Original - Fil-hash matchar"
    };
  } else {
    return {
      valid: false,
      message: "❌ Falskt - Filen har manipulerats"
    };
  }
}
```

#### Full Verify (Full Verifiering)
```javascript
// Återskapar och verifierar EvidenceRoot och NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Hämta från Registry
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash-kontroll (snabb röd flagga)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Falskt - Fil-hash matchar inte" };
  }

  // 2) Återskapa EvidenceRoot (med forensics lagrad i registry)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Matchar inte - EvidenceRoot stämmer inte" };
  }

  // 3) Återskapa NotarySeal (med samma timestamp + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Matchar inte - NotarySeal stämmer inte" };
  }

  // Valfritt: I Fas 2 verifiera även signer_sig med attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Ogiltig signatur" };

  return { valid: true, message: "✅ Original - Full Verify godkänd" };
}
```

> **Viktiga Noter:**
> - **Quick Verify:** Kontrollerar endast fil-hash för snabb användning.
> - **Full Verify:** Verifierar alla lager i protokollet (EvidenceRoot + NotarySeal).
> - Alla hash-operationer görs deterministiskt med fast encoding och delimiters.
> - **v1.0 canonicalization-standard:** Fast fältordning + UTF-8 encoding + `\n` delimiter.
> - **Fas 2-plan:** Övergång till canonical JSON med RFC 8785 (JCS - JSON Canonicalization Scheme).
> - I masked-läge görs EvidenceRoot- och NotarySeal-beräkning med maskerad forensics.
> - En enda timestamp används genom hela processen (forensics + NotarySeal); determinism garanteras.
> - **Forensics-fältnamn:** `ip_masked`, `location`, `device`, `timestamp` (kod och registry helt kompatibla).
> - **Registry-sökväg:** `certificate.asset.fingerprints` (helt kompatibel med verifieringskoden).
> - **signer_sig i Registry:** Fältet `proof.signer_sig` krävs för Full Verify.
> - SignerSignature-mekanismen kommer att aktiveras i Fas 2 med Solana Wallet Adapter; i v1.0 kan verifiering göras med `attestation_pubkey`.

---

## 📊 Konkurrentanalys (Uppdaterad)

PoArt positionerar sig på "Sweet Spot" (Den mest ideala punkten) som kompletterar bristerna i befintliga lösningar.

| Funktion | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|----------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Kostnad** | 🆓 Gratis | 🆓 | 💰 Betald | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Mycket Lätt | ❌ CLI | ⚠️ Medel | ⚠️ Medel | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Live | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Lägen | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Integritet | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Komplett | ❌ | ❌ | ⚠️ Begränsad | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Omedelbar | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Turkish Support** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Förklaring:**
- ✅ : Fullt stöd / tillgängligt
- ⚠️ : Begränsat / i betalplaner
- ❌ : Saknas / stöds inte
- 🔄 : I roadmap (under utveckling)
- 🆓 : Helt gratis
- 💰 : Betald / prenumeration krävs

### Konkurrenters Brister, PoArt:s Styrkor

| Brist | Konkurrenter | PoArt |
|-------|--------------|-------|
| **Användningssvårigheter** | CLI, API-kunskap, plånbok krävs | Dra-och-släpp, klart med 3 klick |
| **Kostnadsbarriär** | $50-500/månad prenumeration | 100% gratis |
| **Integritet** | Fil laddas upp till server | Client-side, fil skickas aldrig |
| **Forensisk Data** | Endast tidsstämpel | IP, plats, enhet, tid - allt |
| **Svenskt Stöd** | Saknas eller mycket begränsat | Professionell lokalisering |
| **Öppen Källkod** | Stängd låda | All kod öppen på GitHub |

---

## 📈 Användningsstatistik (2026 Q1-mål)

| Metrik | Mål | Status |
|--------|-----|--------|
| **Totala Certifikat** | 1 000 | 🔄 Pågående |
| **Aktiva Användare** | 500 | 🔄 Pågående |
| **Antal Verifieringar** | 5 000 | 🔄 Pågående |
| **Uptime** | 99,9% | ✅ Aktiv |
| **Avg Response Time** | <200ms | ✅ Optimal |

---

## 🌍 Community & Support

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Webb:** [ilhanart.org](https://ilhanart.org)
- **E-post:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Bidragsgivare

PoArt-protokollet fortsätter att utvecklas med bidrag från open source-communityn.

**För att bidra:**
1. Gör en fork
2. Skapa feature branch (`git checkout -b feature/amazing-feature`)
3. Gör commit (`git commit -m 'Add amazing feature'`)
4. Gör push (`git push origin feature/amazing-feature`)
5. Öppna Pull Request

### 🛠️ Vad Behöver Vi Just Nu? (Hjälpbegäran)

PoArt Protocol **Fas 2**-utvecklingar väntar på bidrag från erfarna utvecklare inom följande områden:

* **Supabase Edge Functions:** Flytta spamskydd till serversidan.
* **Solana Web3.js:** Wallet Signing-integration.
* **IPFS / Arweave:** Arkivering och pinning-tjänstintegration.
* **Community Tools:** Discord bot, voting systems, analytics dashboard.

> Vänligen starta en diskussion i "Issues"-fliken innan du lägger till en funktion.

---

## 💬 Slutnoteringar

### Pump.fun och Verklighet

Detta projekt startades på Pump.fun eftersom:
- ✅ Likviditetsåtkomst (Raydium automatic migration)
- ✅ Befintlig community-åtkomst
- ✅ Låg startkostnad

Men låt oss klargöra detta:
- **Token-pris** är inte en indikator på konstnärlig framgång
- **Operationell budget** kräver token-värde (galleri, utställningar, infrastruktur)
- **Framgångsmått:** Authenticated artworks + community engagement + fysiska besökare

### Styrning och Decentralisering

**v1.0 Verklighet (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (centraliserad men transparent)
- Governance: Endast rådgivande (kuratoriellt slutgiltigt beslut)
- Token utility: Gallery access + registry + NFT priority

**v2.0+ Vision (2027+):**
- Registry: On-chain (Solana)
- Signaturer: Wallet-baserade (decentraliserade)
- Governance: Hybrid (community advisory + curatorial quality)
- Token utility: Förbättrade funktioner + avancerad åtkomst

Denna struktur ger **operationell effektivitet** och **kvalitetskontroll** i tidigt skede, samtidigt som den håller vägen öppen för att **öka community-deltagande** i framtiden.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Kultur är Större än Kapital*

## 🧾 Licens

MIT License © 2026 İlhan Art Gallery Initiative

Se [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) för fullständiga villkor.

---

## 💬 Tack till

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Detta projekt har utvecklats av [İlhan Art Gallery]-initiativet, och källkoderna är öppna för allmänheten för transparensens skull.**

**PROTOKOLL V1.0 // FÖRSEGLAT MED SHA-512.**

*© 2026 İLHAN ART | ALLA RÄTTIGHETER TILL VERK, BILDER OCH IDÉER ÄR FÖRBEHÅLLNA.*

---
