# 📚 TERMINOLOGI OCH BEGREPPSORDLISTA
> **"Att förstå detta protokolls språk innebär att förstå dess vision."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Grundinfrastruktur

**PoArt Forensic Engine (PFE)** är grundskiktet som representerar den grundläggande logiken och tekniska funktionen bakom [PoArt]-protokollet. Det är "den kriminaltekniska motorn" som omvandlar rådata från ett konstverks produktion till verifierbart och oföränderligt **digitalt bevis**.

### 🧩 Varför "PoArt Forensic"?

- **PoArt (Proof of Art):** Motorns fokus är att binda värdet av en digital tillgång inte till spekulation, utan till den **verifierade produktionsprocessen**.
- **Forensic (Kriminalteknisk Verifiering):**
  - **Teknisk Definition:** Algoritmisk metod och beviskedja för att verifiera att data från produktionsprocessen (penseldrag, timelapse, loggar) inte har manipulerats.
  - **Filosofiskt Plan:** Mot artificiell intelligensens "omedelbara produktion"; påståendet om omvandling av mänsklig produktion som innehåller **tid, ansträngning och beslutskostnader** till mätbar verklighet.

> Notering: Blockchain-integration (t.ex. Solana) är inte PFE:s kärna; den kommer att definieras separat som **Chain Anchor Layer** för verifiering/register.

### 🛠️ Teknisk Omfattning v1.0

**PoArt Forensic Engine (PFE) v1.0** är byggd på **3 grundpelare** istället för komplexa finansiella modeller:

1. **Hashing & Sealing (Försegling):**  
   PFE behandlar deterministiskt alla element i Evidence Pack (verksfil, video, JSON/logg, signatur etc.) och genererar ett unikt **NotarySeal**-värde.

   **Nyckelbegrepp (v1.0):**
   - **FileHash (verkets fingeravtryck):** Hash genererat från verkfilens bytes.
   - **EvidenceRoot (bevispaketets rot):** Rotsammanfattningen som representerar Evidence Pack:s integritet (Merkle-rot eller hash av kanoniskt manifest).
   - **NotarySeal (slutligt sigill / PFE:s utdata):** Slutligt sigill genererat från kombinationen EvidenceRoot + tid + signatur.

   **Formler (i format begripligt för investerare):**
   
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
   
   > Notering: Värdet som betraktas som PFE:s utdata är **NotarySeal**. **SignerSignature**-mekanismen aktiveras i fas 2 (med Solana Wallet Adapter); i nuvarande v1.0 används systemets egen attesteringssignatur. Den offentliga attesteringsnyckeln publiceras i registret i fältet `issuer.attestation_pubkey`.

2. **Indexing (Arkivering):**  
   Registrerar vilken plånbok, vilket datum, presenterade **Labor Proof (Arbetsbevis)** för vilket verk; i ett transparent och frågebart registerskikt.  
   *(Detta skikt kan vara en databas; blockchain-integration definieras separat som "Chain Anchor Layer".)*

3. **Verification (Verifiering):**  
   När ett verks äkthet ifrågasätts, ombearbetar PFE råbevisen; testar med matematisk säkerhet om de beräknade **EvidenceRoot / NotarySeal**-värdena motsvarar arkivets poster.

---

### 🧮 PoArt Värdeteorem (The Value Theorem)

[PoArt]-protokollet binder en digital tillgångs värde ($V$) inte till subjektiv marknadsuppfattning, utan till **produktionsprocessens fysiska verklighet**.

Artificiell Intelligens (AI) upphäver processen genom att erbjuda omedelbara resultat ($t \to 0$). [PoArt] betraktar istället värde som ackumulering av komponenterna **tid, arbete och vilja**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definition av Variabler

- **$\int dt$ (Processens Ackumulering):**  
  Värdet är inte en omedelbar "utdata"; det är en **process** som ackumuleras mellan $t_{\text{start}}$ och $t_{\text{end}}$. När tiden minskar (AI-produktion), närmar sig integralens resultat noll.

- **$P_{\text{labor}}(t)$ (Omedelbar Arbetsintensitet):**  
  Representerar intensiteten av mental och fysisk ansträngning som spenderats vid produktionsögonblicket. När verifierad ansträngning ökar, växer integranden.  
  > Notering: Denna term kan i praktiken normaliseras till "mätbara/verifierbara arbetssignaler".

- **$I_{\text{agency}}(t)$ (Viljekoefficient):**  
  Detta är producentens förmåga att ta risker och fatta beslut. Tar värden mellan $0$ och $1$.
  - **AI ($I \approx 0$):** Utför kommandon, tar inga risker, betalar inga kostnader.
  - **Människa ($I \to 1$):** Ändrar beslut, tvekar, tar risker.

- **$U_{\text{irreversible}}$ (Oåterkallelig Unikhet):**  
  Medan du i digital produktion kan ångra (`Ctrl+Z`); i fysisk produktion (målarfärg applicerad på duk, huggen marmor, gest under en livesändning) finns ingen återvändo. Denna **oåterkallelighet** är en tilläggsterm som skapar "unikhet" (icke-utbytbar karaktär) i verket.

### 🔎 Fallanalys: AI "Omedelbar Utdata" mot Människa "Bevisad Process"

Följande scenario visar hur **PoArt Värdeteorem** fungerar i praktiken och varför AI-produktioner får låga poäng i [PoArt]-standarden.

#### Scenario A: Visuell Produktion med AI på 10 Sekunder

- **Varaktighet ($\Delta t$):** $10$ sekunder (process praktiskt taget obefintlig)
- **Arbetsintensitet ($P_{\text{labor}}$):** $1$ enhet (endast skrivning av kommando)
- **Viljekoefficient ($I_{\text{agency}}$):** $0.01$ (ingen risk, ingen kostnad)
- **Oåterkallelighet ($U_{\text{irreversible}}$):** $0$ (återkallningsbar / kopierbar)

**Resultat:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Kommentar:** Även om utdata är perfekt; eftersom processen inte har upplevts och inte innehåller vilja/risk, närmar sig [PoArt]-värdet $0$.

#### Scenario B: Fysisk Produktion i Livesändning under 6 Timmar

- **Varaktighet ($\Delta t$):** $6$ timmar ($21{,}600$ sekunder)
- **Arbetsintensitet ($P_{\text{labor}}$):** $0.5$ enheter (kontinuitet av fysisk och mental ansträngning)
- **Viljekoefficient ($I_{\text{agency}}$):** $0.9$ (ändring av beslut, risktagande, oåterkalleliga val)
- **Oåterkallelighet ($U_{\text{irreversible}}$):** $>0$ (fysiska spår kan inte ångras)

**Resultat:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Kommentar:** När processen förlängs och viljan (risk) ökar, ackumuleras värdet kumulativt. Termen $U_{\text{irreversible}}$ är ett tilläggsbidrag som skapar "unikhet" (icke-utbytbar karaktär) i verket.

---

### ✅ Slutsats: Bevisbundet Värde (Proof-Bound Value)

Detta teorem tar bort [PoArt]-värdepåståendet från att vara en "gilla-markering" eller en "marknadsberättelse" och binder det till **verifierad produktionsverklighet**.

1. **Utan Process Skapas Inget Värde:**  
   AI upphäver processen i omedelbar utdata ($t \to 0$). När processfönstret smalnar av, minskar integralens resultat av matematisk nödvändighet:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Vilja och Risk Är Multiplikatorer:**  
   [PoArt] mäter inte bara "spenderad tid", utan också den verkliga nivån av beslut, risk och kostnad under den tiden. Värdet av en produktion utan risktagande (AI) är lågt:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Unikhet Är Fysiskt Bevis, Inte Marknadsföring:**  
   I fysisk produktion är oåterkalleliga spår (penselstrykning på duk, brutet marmor) utanför den digitala `Ctrl+Z`-logiken. Denna oåterkallelighet ($U_{\text{irreversible}}$) gör verket ontologiskt unikt.

> **🔐 SAMMANFATTNING:** Även om värdeteoremet kan verka odefinierat som mätning (även om det inte kan mätas 100% i verkliga livet), är syftet med denna formel att visa variablernas struktur och riktning. Det som är sällsynt i AI-eran är inte "bilden", utan **verifierat arbete, tid och vilja.** [PoArt] mäter denna sällsynthet och registrerar den genom **Evidence Pack**.

### 🏛️ Betydelsen av Begreppet "Engine" (Motor)

Tokens som kommer från plattformar som Pump.fun är ofta bara **"åtkomstbiljetter"**. **PoArt Forensic Engine (PFE)** är istället ett **konstitutionellt logiskt skikt** som definierar vilka rättigheter denna biljett skyddar, hur arbete registreras och hur konst/vetenskap/teknologi blir permanenta.

> **Notering:** Anledningen till att vi startade detta projekt på Pumpfun är att vi inte hade tillräcklig likviditet och följare. Användningen av befintliga data var ett strategiskt korrekt steg, även om det inte var det mest kvalitativa. Att definiera denna motors logik på GitHub, oberoende av budget och resurser, bevisar att projektet inte bara är finansiell spekulation, utan en långsiktig vision av **mjukvaruinfrastruktur** och **digitalt nationalbibliotek**.

---

## 🎨 [PoArt] PROOF OF ART-PROTOKOLLET (Proof of Art Protocol v1.0)

> **"Äkta Konstnär, Äkta Produktion, Äkta Värde."**

Detta protokoll är en **biologisk och intellektuell försvarsmekanisms** designad mot anonyma bedragare som har översvämmat kryptoekosystemet, AI-bilder producerade på 5 minuter och "Pump & Dump"-kulturen.

---

## a) Vad Är [PoArt]? (Filosofisk och Teknisk Definition)

**Proof of Art [PoArt];** är en institutionell verifieringsstandard som garanterar att värdet bakom en tillgång på blockchain baseras inte på spekulation, utan på verifierat **mänskligt arbete**, **tid** och **fysisk energi**.

Precis som Bitcoin producerar värde genom *"Elektricitet och Beräkningskraft"* **(Proof of Work)**; producerar [PoArt]-kompatibla projekt värde genom *"Konstnärlig Skicklighet och Mänsklig Tid"*.

Eliminerar risken *"Dev sålde, projektet avslutades"*, närvarande på Pump.fun och DEX-plattformar; eftersom här är värdet inte i koden, utan i **produktionens kontinuitet**.

> **[PoArt] säger inte till deltagaren "Lita på oss"; det säger "Här är bevisen, se med egna ögon, verifiera med din egen matematik".**

---

## b) [PoArt] 5-Pelarstandarden (The 5 Pillars of Truth)

Dessa 5 punkter är icke-manipulerbara filter som ett projekt måste passera för att få [PoArt]-sigillet.

### 1) Live-identitetsbevis (Live Identity Proof)

- **Problem:** Kryptovärlden är full av anonyma grundare (Dev) med odefinierad identitet som samlar pengar och överger projektet.
- **[PoArt]-lösning:** Producenten bevisar inte bara identiteten, utan **närvaron under produktionen**. Detta inkluderar livesessioner där de interagerar med gemenskapen och uppfyller specifika omedelbara krav, inte med förinspelad video.  
  (Till exempel: *"Skriv dagens datum och nuvarande blocknummer i dukens högra hörn"*)
- **Motto:** *"Robotar kan måla, men robotar svettas inte och improviserar inte."*

### 2) Arbets- och Processbevis (Labor & Process Proof)

- **Problem:** AI-bilder producerade på 2 sekunder och oljemålningar gjorda på 2 månader betraktas som samma "jpeg" i den digitala världen.
- **[PoArt]-lösning:** Verkets "graviditets- och födelseprocess" registreras. Skissfaser, färglager, ackumulerade spenderade timmar och den fysiska processen som konstnären upplevde under verkets skapande dokumenteras. Detta lägger till **"Tidskostnad" (Time Cost)** till token. Ju svårare tillgången är att producera, desto starkare är dess värde.

### 3) Estetiskt Värdebevis (Aesthetic Value Proof)

- **Problem:** "Meme"-kulturens estetik och konstnärliga djup som ignorerar allt och bara fokuserar på omedelbar komedi, och de kortsiktiga "Hype"-projekt som följer därav.
- **[PoArt]-lösning:** Projektet måste ha akademiska konststandarder, färgteori, kompositionsregler och materialkunskap (Impasto, Textur etc.). Innehållet ska inte bara få en att skratta; det ska väcka beundran hos betraktaren och ha **samlarvärde**.

### 4) Konceptuell Innovation (Conceptual Novelty)

- **Problem:** Tusentals identiska dog/cat coin, långt från kreativitet.
- **[PoArt]-lösning:** Projektet måste bygga en ny bro som meningsfullt kombinerar konst, vetenskap, filosofi eller teknologi.  
  (Till exempel: Kombination av den klassiska Davidstatyn med kryptovalutamarknadsdata; genom detta bearbetning av idén om "förstenande" av mänsklig perception och möjligheten att motivera detta med vetenskapliga källor.)  
  Verket måste inte bara vara en visuell fest, utan också en intellektuell utmaning som uppmuntrar till eftertanke om **Vetenskap, Filosofi eller Teknologi**.

> [!IMPORTANT]
> **Referensexempel (Las Palmitas-effekten):** I Mexikos Las Palmitas-område, som kämpar med brottslighet, förvandlades över 200 hus till en jättestor >regnbågsfest. Som ett resultat av denna estetiska intervention sjönk brottslighetstalen i området till viss grad, ungdomar började intressera sig för konst istället >för gäng. Den estetiska förändringen omkodade människors respekt för miljön och varandra (Social Sammanhållning).
>
> **Förväntan:** Ett projekt som kommer in på [PoArt]-listan; som i exemplet ovan, måste innehålla en sociologisk, vetenskaplig eller filosofisk orsakssamband >bortom visuell estetik. Eftersom det enda som inte kan köpas med pengar är "Tid", i detta protokoll måste tiden bevisas som garanti genom staking. Projektets >konceptuella grund måste vara så stark och universell; att även i ett möjligt CTO (Community Take Over)-scenario år senare, kan gemenskapen autonomt >upprätthålla projektets innovativa potential genom att ärva detta arv.

### 5) Icke-Algoritmisk Vilja (Non-Algorithmic Agency)

- **Problem:** Perfekta men själslösa, repetitiva digitala produktioner.
- **[PoArt]-lösning:** Den ursprungliga viljan hos en mänsklig varelse som kan göra misstag, ta risker och känna känslomässiga fluktuationer måste kännas i verket. Osäkerheten i penseldragen, materialets oväntade reaktioner och konstnärens omedelbara beslut är **Biologisk Signatur** som skiljer verket från "Mekanisk Produktion".

---

## c) Verifieringsmekanismen och Förfalskningsbekämpning

Detta system säkerställer att projektet förblir pålitligt och levande inte bara "i början", utan "för evigt".

### 📦 Bevispaket (Evidence Pack - The Digital Twin)

Bakom varje [PoArt]-certifierat verk finns ett krypterat och tidsstämplat datapaket som investerare kan ladda ner:

- **RAW-videoinspelningar:** Kontinuerliga råinspelningar av produktionsögonblicket.
- **Metadataanalys:** Filens skapandedatum, information om använd enhet och platsdata.
- **Fysiska Referenser:** Bevis på att verket existerar i den fysiska världen  
  (Till exempel: Aktuell tidning eller aktuell blockchain-data bredvid verket).

> *Notering om konsistens:* Uttrycket "bevispaket" är kopplat till linjen **Evidence Pack → EvidenceRoot → NotarySeal** från tidigare avsnitt; det vill säga paketets integritet representeras av det verifierade sigillet.

### 🔄 365-dagarsuppdatering (The Sustainability Protocol)

- **Revolutionerande Funktion:** I kryptoprojekt lanserar "Dev" (Utvecklaren) token på marknaden och försvinner vanligtvis efter 1-2 månader (Soft Rug). [PoArt] gör detta omöjligt.
- **Regel:** "Verified Artist" (Verifierad Konstnär)-status är inte livslång. Den är endast giltig i **1 år**.
- **Funktion:** Konstnären/utvecklaren måste presentera för gemenskapen var 365:e dag **ett nytt, stort och verifierat verk**.
- **Exempelscenario:** Du startade projektet 2026. I januari 2027 ger systemet varningen "Bevisperiod Avslutad". Om konstnären inte presenterar ny utställning, nytt fysiskt verk eller ny teknologisk integration, sjunker projektets "Förtroendemärke".
- **Resultat:** Detta system säkerställer att **innehållet aldrig förlorar sin relevans** och att investeraren inte lever i rädsla för *"Är utvecklaren fortfarande här?"*. Projektet blir en levande studio.

### 🚩 Röd Flagga (Red Flag Protocol)

**Om någon förfalskning upptäcks av gemenskapen eller algoritmer (AI-användning, stulet arbete, manipulerad video):**

1. Certifikatet markeras omedelbart som **"OGILTIGT" (VOID)**.
2. Bevispaketen markeras offentligt som **"Falska"**.
3. Projektet läggs till [PoArt]-svarta listan. Detta förstärker faktum att i den decentraliserade världen är **rykte den enda valutan**.

---

## d) Slutsats: Inte Kasino, Museum

**Pump.fun och Decentraliserade Börser (DEX) är tyvärr nu kasinon; lamporna blinkar, alla söker snabba vinster, och kasinot (bedragare) vinner alltid. Anledningen till att vi startade projektet här är bristen på tillräcklig budget och förekomsten av befintlig publik tillgänglig genom livesändningar.**

**[PoArt] är en fästning byggd mitt i detta kasino.**

- 🎰 Kasinon baseras på kort; vi baseras på **fysisk verklighet**.
- 🃏 Kasinon är öppna för bedrägeri; vi är öppna för **transparenta bevis**.
- ⏳ Kasinon är tillfälliga; vi fokuserar på **konstens och vetenskapens evighet**.

**En token som använder detta protokoll är inte bara ett "mynt"; det är ett digitalt värdepapper som innehåller svett, färg, kod och filosofi.**

---

## 🗳️ 6) STYRNING OCH OFFENTLIGT REGISTER (Governance & Public Registry)

**Syftet med detta avsnitt är: att ta bort [PoArt]-standarden från sfären "förtroende för människor" och omvandla den till en hållbar offentlig infrastruktur med register + verifiering + gemenskapsövervakning.**

### 6.1 Offentligt Register (Public Registry)

- **Public Registry:** All godkänd data registreras på adressen `ilhanart.org/registry` (eller GitHub Registry).

**Registreringslogik (rekommenderad standard - JSON-sökvägsformat):**

Varje post som kommer in i registret innehåller minst dessa verifierade grundfält:

- **Identitet och Status:**
  - `certificate_id` (läsbar referens)
  - `status` (active / void)
  - `void_reason` (om det finns)
  - `visibility` (private / masked / public)
  - `created_at` (tidsstämpel)

- **Utfärdande Organisation:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Information om Verket:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (om möjligt; för token-gated identitet)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Kriminaltekniska Data:**
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
  - `governance.veto_threshold`

Registret kan ha två nivåer:
- **1)** Mänskligt läsbart index (webblista / sökning / filter)
- **2)** Maskinläsbart manifest (JSON-poster; för PFE-verifiering)

**Här blir "registreringen" verifierad av PFE:s kedja Evidence Pack → EvidenceRoot → NotarySeal. Registret tillhandahåller verifieringens syfte, inte "påståendet".**

---

### 6.2 40 % Gemenskapsveto (Token-Gated Governance)

- **40 % Gemenskapsveto:** Omröstningen börjar en månad innan statusen erhålls; 40 % invändning från **Token-Gated (Solana-Verified)** gemenskapen ogiltigförklarar ansökan.

**Omröstningsflöde (rekommenderad ren process):**
- **Kandidatfönster:** Kandidatprojektet öppnar "PoArt-kandidatregistrering" (kandidatregistreringar visas med status "pending").
- **Granskningsperiod:** I 30 dagar granskar gemenskapen bevisen (Evidence Pack + liveinspelningar + metadata).
- **Token-gated verifiering:** Omröstning sker genom plånböcker verifierade på Solana (t.ex. ägande av viss token/NFT + plånbokssignatur).
- **Veto-regel:** Om 40 % av rösterna är **invändning (NO / VETO)**, avvisas ansökan.
- **Transparens:** Omröstningsresultatet lagras i registret som "decision record" (datum, förhållande, snapshot ID).

---

### 6.3 Metadatasynkronisering (Överensstämmelse med Fysisk Värld)

- **Metadata Sync:** Tekniska data i registret måste motsvara 100 % den fysiska tillgången.

**Teknisk definition av "100 % överensstämmelse" (rekommenderad tydlighet):**
- **Minimal överensstämmelse (obligatorisk):**
  - Registrets `asset.fingerprints.sha256/sha512` måste vara **exakt samma** som hashen för filen i handen.
  - Registrets `proof.notary_seal`, när det reproduceras (om Evidence Pack finns), måste vara **exakt samma**.
- **Fysisk referensöverensstämmelse (bevistyp):**
  - Bevis som fysiskt verk visat i livesändning + datum/blockreferens måste vara konsekventa med Evidence Pack.
- **Integritetsöverensstämmelse:**
  - Fält som IP/plats i `masked`-synlighet publiceras **enligt maskeringsstandarden**.

---

### 6.4 Tvist, Granskning och Återkallelse (Dispute & Revocation)

Registret är inte bara en "godkännandesmekanism"; det är en **levande övervakningsmekanism mot förfalskning**.

- När tvist initieras kan posten sättas i **"review"**-läge.
- Om förfalskning upptäcks markeras den som `status: void` och anledning läggs till:
  - `void_reason` (AI-användning / plagiat / manipulation etc.)
  - `revoked_at` (återkallelseögonblick)
- Källan till återkallelsebeslutet är tydligt synlig i registret:
  - gemenskapsomröstning / auktoriserad råd / kriminalteknisk undersökningsnot (beroende på vad som gäller)

> **Detta avsnitt är registermotsvarigheten till VOID-konceptet i "Red Flag Protocol"-avsnittet.**

---

### 6.5 Exempel på Registerpost (Maskinläsbar)
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
    "title": "Utan titel",
    "creator": "Anonym",
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
> *Notering: `asset.fingerprints.sha512` och andra hash-värden är förkortade för demonstrationssyften; i den verkliga applikationen används hexadecimal teckensträng av full längd.*

---

## 7) 🔐 TEKNISKT SIGILL (NOTARY SEAL)

**PoArt Forensic Engine (PFE) v1.0** orubblig förseglings-algoritm producerad med:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt]-protokoll Digital Notarie och Kriminaltekniskt Bevis (Beta v1.0)

> **"Kultur Större än Kapital. Skydda dina verk idag, ta dem till morgondagen."**

---

## Varför Offentligt?

Verklig säkerhet kommer från transparens. Tack vare vårt **Public Registry (Offentligt Register)**-system kan en person var som helst i världen verifiera på några sekunder om filen i handen är original, utan någon myndighet.

---

## 🧩 Varför Finns Det Flera "Synlighetsmoduler"?

Den mest kritiska delen av koden är här (synlighetsvalsmeny). Dessa alternativ tillåter användare att balansera **"Integritet mot Transparens"**:

### 🔒 Privat (Private)

- **Scenario:** Konstnären vill ännu inte publicera verket, men vill tidsstämpla det och bevisa "jag gjorde detta detta datum".
- **Vad Koden Gör:** Sparar data i databasen, men använder taggen `visibility: "private"`. I framtiden, när du skriver "Public Read"-policyn, kan du dölja dessa poster från allmänheten genom att säga `WHERE visibility = 'public'`.

### 🕶️ Maskerad (Masked)

- **Scenario:** Konstnären vill ha transparens, men fruktar att hemadressen ska hittas (IP-plats).
- **Vad Koden Gör:** På JavaScript-sidan fungerar funktionerna `maskIP` och `maskLoc`. Konverterar IP-adressen till formatet `88.241.***.***` och platsen till formatet `***/TR` och skickar den censurerade versionen till databasen.
- **Notering om Integritet:** Maskering sker i webbläsaren, Supabase ser inte den verkliga platsen. **Dock:** Om tredjepartss-API:er som ipapi.co används för platsdata, ser dessa leverantörer IP-adressen vid förfrågningsögonblicket.
- **Försegling i Masked-läge:** Beräkningen av EvidenceRoot och NotarySeal görs med maskerade forensics-data; därmed förblir verifieringen deterministisk.

### 🌍 Offentlig (Public)

- **Scenario:** Full transparens. Enligt [PoArt]-standarden, var, när och från vilket nätverk verket producerades deklareras uttryckligen.

---

## 💡 Teknologisk Innovation

PoArt är inte bara ett filuppladdningssystem. Det är en **"Forensic Chain of Custody"**-motor som smälter tre olika teknologiska lager i en enda smältdegel och för med sig en ny standard.

**Skiktet som beskrivs i detta avsnitt som "motor" motsvarar PoArt Forensic Engine (PFE)-kärnan i tidigare terminologi.**

### 1) Client-Side Hashing (Maximal Integritet)

Dina verks filer laddas aldrig upp till servern. Vår webbläsarbaserade (Client-side) motor beräknar filens hash (digital sammanfattning) på din dator. Endast detta fingeravtryck och metadata skickas till servern.

> **Notering om Integritet:** Verkfilen laddas inte upp till servern och skyddas därmed. Dock delas forensics-data (IP/plats) enligt valt synlighetsläge (private/masked/public).

### 2) Forensic Data Fusion (Kriminalteknisk Kraft)

Detta är mycket mer än en enkel tidsstämpel. Systemet kombinerar följande data i ett enda "Genesis Seal":

- **Digital Sammanfattning (SHA-512):** Med användning av kryptografisk sammanfattning (SHA-512)-standard, det digitala fingeravtrycket som går sönder även om en pixel av verket ändras.
- **Plats och Tid:** Datumet med millisekunds noggrannhet, landet, staden och området där transaktionen genomfördes.
- **Enhetsidentitet:** Operativsystem, webbläsare och enhetstyp (User-Agent-analys).

---

## 🛡️ Tillämpningsområden och Fördelar

Om du är konstnär, författare eller designer räcker det inte att säga "Jag gjorde detta tidigare", du måste bevisa det.

**Ett verk förseglatmed PoArt:**

- **Matematiskt Bevis:** Systemet upptäcker detta även om en pixel av filen ändras. Manipulation är omöjlig.
- **Juridisk Grund:** Det registreras vilket datum, i vilken stad, från vilken enhet verket förseglades.
- **Omedelbart Certifikat:** På några sekunder genererar ett personligt **"Tillgångsidentitetscertifikat"** med QR-kod och förseglat.

---

## ⚙️ Systemarkitektur och Tekniska Specifikationer

Systemet är designat på "Serverless" (Serverlös)-arkitektur, fokuserad på hög prestanda och skalbarhet.

| Skikt | Teknologi | Beskrivning |
|--------|-----------|----------|
| **Kryptografi** | SHA-256 & SHA-512 | Tvålagers kryptografisk sammanfattning |
| **Databas** | Supabase (PostgreSQL) | JSONB-datastruktur, RLS-policyer |
| **Kriminaltekniska Data** | ipapi.co API | IP/Plats/Tid-triad |
| **Rendering** | html2canvas + jsPDF | PNG/PDF-generering på klientsidan |
| **Frontend** | Vanilla JavaScript | Noll framework-beroenden |
| **Säkerhet** | Client-side hashing | Filen når aldrig servern |

### Utmärkande Funktioner

| Funktion | Detalj | Hos Konkurrenter? |
|---------|-------|-------------|
| **Drag & Drop UI** | Dra och släpp filen, omedelbar förhandsvisning | ❌ Saknas hos de flesta |
| **Multi-Format Export** | PNG, JSON, PDF - ett klick | ⚠️ Begränsat |
| **Real-Time Preview** | Förhandsvisning av certifikat i realtid | ❌ Saknas |
| **Privacy Controls** | Private/Masked/Public-alternativ | ❌ Saknas |
| **Client-Side Hashing** | Filen når aldrig servern | ✅ Endast hos några |
| **Forensic Metadata** | IP, plats, enhet, tid - allt tillsammans | ❌ Fragmenterat |
| **QR Verification** | QR-kod för omedelbar verifiering | ⚠️ Begränsat |
| **Rate Limiting** | Skräppostskydd (RLS + Client) | ❌ Saknas hos de flesta |

---

## 🗺️ Färdplan: "Trustless" Framtid

Den nuvarande versionen **(Beta v1.0)** är optimerad för att ge slutanvändaren maximal hastighet, enkelt gränssnitt och gratis åtkomst. Dock är vår slutliga vision övergången till en struktur där inte ens databasadministratören (vi) kan ingripa.

### Fas 1: Beta (Nu Tillgänglig)

- **Infrastruktur:** Cloud Database (Supabase).
- **Syfte:** Hastighet, eliminering av UX (Användarupplevelse)-hinder och anpassning. Säkerställande av "friktionsfri" säkerhet.

### 🚀 Fas 2: (Vad Som Kräver Backend / Edge Function)

Denna fas täcker övergången från systemets helt "Client-Side" fungerande struktur till en säkrare och hanterad "Server-Side Authority"-struktur.

| Element | Vad För Det Med Sig? | Tech Stack | Prioritet |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Function** | Skräppostsblockering + API-nyckelsäkerhet | Supabase Edge (Deno) | 🔴 Hög |
| **Plånbokssignatur** | Kryptografisk identitetsautentisering | Solana Wallet Adapter | 🟡 Medel |
| **IPFS/Arweave Backup** | Decentraliserad oföränderlighet | IPFS SDK + Pinata | 🟢 Låg |
| **Återkallelsesmekanism** | Ogiltigförklaring av falska certifikat | DB Schema uppdatering | 🔴 Hög |
| **Audit Log** | Kriminalteknisk undersökningsregistrering | Anpassad loggtabell | 🟡 Medel |
| **OpenTimestamps** | Bitcoin-förankring | OTS JavaScript | 🟢 Låg |
| **DID-integration** | Decentralized Identity | ION/Ceramic | 🟢 Låg |

### Fas 3: Full Decentralisering (Långsiktigt)

| Funktion | Syfte | ETA |
|---------|-------|-----|
| **Blockchain Registry** | On-chain registrering Ethereum/Solana | Q4 2026 |
| **DAO Governance** | Gemenskapsstyrning | Q1 2027 |
| **Multi-Chain Support** | Polygon, Arbitrum, Base | Q2 2027 |
| **Legal Recognition** | Giltighet i turkiska domstolar | 2027-2028 |
| **API for Developers** | Offentlig API-slutpunkt | Q3 2026 |

---

## 📊 Konkurrentanalys (Uppdaterad)

PoArt är placerad på "Sweet Spot" (Optimal Idealplats) som kompletterar luckor i befintliga lösningar.

| Funktion | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 証 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Kostnad** | 🆓 Gratis | 🆓 | 💰 Betald | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Mycket Enkelt | ❌ CLI | ⚠️ Medel | ⚠️ Medel | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ I Realtid | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Lägen | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Integritet | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Komplett | ❌ | ❌ | ⚠️ Begränsat | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Omedelbar | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Färdplan | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Svenskt Stöd** | 🔄 Under utveckling | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Förklaring:**
- ✅ : Fullt stöd / tillgängligt
- ⚠️ : Begränsat / i betalplaner
- ❌ : Saknas / stöds inte
- 🔄 : På Färdplanen (under utveckling)
- 🆓 : Helt gratis
- 💰 : Betald / prenumeration krävs

### Konkurrenternas Nackdelar, PoArt:s Styrkor

| Minus | Konkurrenter | PoArt |
|------|----------|-------|
| **Användningskomplexitet** | CLI, API-kunskap, plånbok krävs | Dra och släpp, slutar på 3 klick |
| **Kostnadshinder** | Prenumeration $50-500/månad | 100 % gratis |
| **Integritet** | Fil laddas upp till server | Client-side, filen lämnar aldrig |
| **Kriminaltekniska Data** | Endast tidsstämpel | IP, plats, enhet, tid - allt |
| **Svenskt Stöd** | Saknas eller mycket begränsat | Nativt språkstöd |
| **Open Source** | Stängd låda | All kod öppen på GitHub |

---

## 🧬 Protokollets Datastruktur (JSON Schema)

**Varje [PoArt]-certifikat har en portabel och verifierbar JSON-identitet producerad enligt följande standard.**

> **Notering:** Detta Identity JSON-format är certifikatformatet som presenteras för användaren. I registerposter används `registry.asset` istället för `identity.asset_data` (mappning: `identity.asset_data` == `registry.asset`).
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
    "title": "Officiell Whitepaper",
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

## 🔬 Tekniskt Djup: Förseglings-algoritm

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

// Generering av kanonisk forensics-sträng (v1.0: fast fältordning + UTF-8 + \n separator)
// Fas 2-notering: Övergång till kanonisk JSON med RFC 8785 (JCS)
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

// 2. Insamling av kriminaltekniska data (med användning av en tidsstämpel)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Generering av en tidsstämpel
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Samma tidsstämpel
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot-skapande (med kanonisk kodning)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal-produktion (med användning av samma tidsstämpel)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Maskeringshjälpfunktioner (IPv4- och IPv6-stöd)
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
// Kontrollerar endast filens hash (snabb röd flagga)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Hämta från Register
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Hash-jämförelse
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Äkta - Filens hash matchar"
    };
  } else {
    return {
      valid: false,
      message: "❌ Falsk - Filen har manipulerats"
    };
  }
}
```

#### Full Verify (Full Verifiering)
```javascript
// Reproducerar och verifierar EvidenceRoot och NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Hämta från Register
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash-kontroll (snabb röd flagga)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Falsk - Filens hash matchar inte" };
  }

  // 2) EvidenceRoot-reproduktion (med forensics-data lagrad i registret)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Matchar inte - EvidenceRoot ogiltig" };
  }

  // 3) NotarySeal-reproduktion (med samma tidsstämpel + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Matchar inte - NotarySeal ogiltig" };
  }

  // Valfritt: I fas 2 verifiera också signer_sig med attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Signatur ogiltig" };

  return { valid: true, message: "✅ Äkta - Full Verify godkänd" };
}
```

> **Viktiga Noteringar:**
> - **Quick Verify:** Kontrollerar endast filens hash för snabb användning.
> - **Full Verify:** Verifierar alla protokollets lager (EvidenceRoot + NotarySeal).
> - Alla hash-operationer utförs deterministiskt, med fast kodning och separatorer.
> - **v1.0 kanoniseringsstandard:** Fast fältordning + UTF-8 kodning + `\n` separator.
> - **Fas 2-plan:** Övergång till kanonisk JSON med RFC 8785 (JCS - JSON Canonicalization Scheme).
> - I Masked-läge görs beräkningen av EvidenceRoot och NotarySeal med maskerade forensics-data.
> - En tidsstämpel används i hela processen (forensics + NotarySeal); determinism garanterad.
> - **Forensics-fältnamn:** `ip_masked`, `location`, `device`, `timestamp` (kod och register helt kompatibla).
> - **Registerväg:** `certificate.asset.fingerprints` (helt kompatibel med verifieringskoden).
> - **signer_sig i Registret:** Fältet `proof.signer_sig` behövs för Full Verify.
> - SignerSignature-mekanismen aktiveras i fas 2 med Solana Wallet Adapter; i v1.0 kan verifiering utföras med `attestation_pubkey`.

---

## 📈 Användningsstatistik (Q1 2026 Mål)

| Mått | Mål | Status |
|--------|-------|-------|
| **Totala Certifikat** | 1,000 | 🔄 Pågår |
| **Aktiva Användare** | 500 | 🔄 Pågår |
| **Antal Verifieringar** | 5,000 | 🔄 Pågår |
| **Uptime** | %99.9 | ✅ Aktiv |
| **Genomsnittlig Svarstid** | <200ms | ✅ Optimal |

---

## 🌍 Gemenskap och Support

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 Bidragsgivare

PoArt-protokollet utvecklas tack vare bidrag från open source-gemenskapen.

**För att bidra:**
1. Gör en fork
2. Skapa funktionsgren (`git checkout -b feature/amazing-feature`)
3. Gör commit (`git commit -m 'Add amazing feature'`)
4. Gör push (`git push origin feature/amazing-feature`)
5. Öppna Pull Request

### 🛠️ Vad Behöver Vi Nu? (Uppmaning om Hjälp)

Vi söker bidrag från erfarna utvecklare i följande ämnen för **Fas 2**-utvecklingar av PoArt-protokollet:

* **Supabase Edge Functions:** Flytta skräppostskydd till serversidan.
* **Solana Web3.js:** Integration av plånbokssignering (Wallet Signing).
* **IPFS / Arweave:** Integration av arkiverings- och förankringstjänster.

> Innan du lägger till en funktion, vänligen starta en diskussion i "Issues"-sektionen.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Kultur Större än Kapital*

## 🧾 Licens

MIT License © 2026 İlhan Art Gallery Initiative

Se [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) för fullständiga villkor.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Detta projekt har utvecklats med [İlhan Art Gallery]-initiativet och källkoden är offentligt tillgänglig för transparens.**

**PROTOKOLL V1.0 // FÖRSEGLAT MED SHA-512.**

*© 2026 İLHAN ART | ALLA RÄTTIGHETER TILL VERK, BILDER OCH IDÉER SKYDDADE.*

---
