# 📚 TERMINOLOGIE & BEGRIPPEN WOORDENBOEK
> **"De taal van dit protocol begrijpen betekent de visie ervan begrijpen."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Kerninfrastructuur

**PoArt Forensic Engine (PFE)** is de hoofdlaag die de kernlogica en technische werking achter het [PoArt]-protocol vertegenwoordigt. Dit is de "forensische motor" die de ruwe productiegegevens van een kunstwerk neemt en deze omzet in verifieerbaar en onveranderlijk **digitaal bewijs**.

### 🧩 Waarom "PoArt Forensic"?

- **PoArt (Proof of Art):** De focus van de motor is om de waarde van een digitaal bezit te koppelen aan een **bewijsbaar productieproces**, niet aan speculatie.
- **Forensic (Forensische Verificatie):**
  - **Technische Definitie:** Een algoritme- en registratiekettenbenadering gericht op het verifiëren dat productieprocessgegevens (penseelstreken, timelapse, logs) niet zijn gemanipuleerd.
  - **Filosofische Laag:** Tegen de "instant output" productie van kunstmatige intelligentie; de claim om de productie van de **mens met tijd, inspanning en beslissingsprijs** om te zetten in een meetbare realiteit.

> Opmerking: Blockchain-integratie (bijv. Solana) is niet de kern van PFE; het wordt behandeld als een afzonderlijk gedefinieerde **Chain Anchor Layer** voor verificatie/register.

### 🛠️ v1.0 Technische Reikwijdte

**PoArt Forensic Engine (PFE) v1.0** is gebouwd op deze **3 hoofdpijlers** in plaats van complexe financiële modellen:

1. **Hashing & Sealing (Verzegeling):**  
   PFE verwerkt alle items in het Evidence Pack (kunstwerkbestand, video, JSON/log, handtekening, enz.) deterministisch en genereert de unieke **NotarySeal**-waarde.

   **Kernconcepten (v1.0):**
   - **FileHash (kunstwerk vingerafdruk):** Hash gegenereerd uit de bytes van het kunstwerkbestand.
   - **EvidenceRoot (bewijspakket wortel):** Wortelsamenvat­ting die de integriteit van het Evidence Pack vertegenwoordigt (Merkle root of canonieke manifest hash).
   - **NotarySeal (definitieve zegel / PFE Output):** Definitieve zegel gegenereerd uit de combinatie van EvidenceRoot + tijd + handtekening.

   **Formules (duidelijk zichtbaar voor investeerders):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload Definities (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Opmerking: De waarde bedoeld als PFE-output is **NotarySeal**. Het **SignerSignature**-mechanisme wordt geactiveerd in Fase 2 (met Solana Wallet Adapter); in de huidige v1.0 wordt de eigen attestation-handtekening van het systeem gebruikt. De attestation public key wordt gepubliceerd in het register in het veld `issuer.attestation_pubkey`.

2. **Indexing (Archivering):**  
   Verwerkt welke portemonnee, op welke datum, welk kunstwerk **Labor Proof (Bewijs van Arbeid)** heeft aangeleverd in een transparante en opvraagbare registerlaag.  
   *(Deze laag kan een database zijn; ketenintegratie wordt afzonderlijk behandeld als "Chain Anchor Layer".)*

3. **Verification (Verificatie):**  
   Wanneer de authenticiteit van een kunstwerk wordt bevraagd, verwerkt PFE de ruwe bewijzen opnieuw; het test met wiskundige zekerheid of de berekende **EvidenceRoot / NotarySeal**-waarden overeenkomen met het record in het archief.

---

### 🧮 PoArt Waardestelling (The Value Theorem)

Het [PoArt]-protocol koppelt de waarde van een digitaal bezit ($V$) niet aan subjectieve marktperceptie, maar aan **de fysieke realiteit van het productieproces**.

Kunstmatige Intelligentie (AI) vernietigt het proces door het resultaat onmiddellijk te geven ($t \to 0$). [PoArt] behandelt waarde daarentegen als de accumulatie van componenten van **tijd, arbeid en wilskracht**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definitie van Variabelen

- **$\int dt$ (Procesaccumulatie):**  
  Waarde is geen momentane "output"; het is een **proces** dat accumuleert tussen $t_{\text{start}}$ en $t_{\text{end}}$. Naarmate de duur afneemt (AI-productie), nadert het resultaat van de integraal tot 0.

- **$P_{\text{labor}}(t)$ (Momentane Arbeidskracht):**  
  Vertegenwoordigt de intensiteit van mentale en fysieke inspanning tijdens de productie. Naarmate de bewijsbare inspanning toeneemt, groeit de integrand.  
  > Opmerking: Deze term kan in de praktijk worden genormaliseerd via "meetbare/bewijsbare arbeidssignalen".

- **$I_{\text{agency}}(t)$ (Wilscoëfficiënt):**  
  Het vermogen van de producent om risico's te nemen en beslissingen te nemen. Neemt een waarde aan tussen $0$ en $1$.
  - **AI ($I \approx 0$):** Voert opdrachten uit, neemt geen risico, betaalt geen prijs.
  - **Mens ($I \to 1$):** Verandert beslissingen, aarzelt, neemt risico's.

- **$U_{\text{irreversible}}$ (Onomkeerbare Uniciteit):**  
  Terwijl ongedaan maken (`Ctrl+Z`) mogelijk is in digitale productie; is er geen weg terug in fysieke productie (verf op canvas, gehouwen marmer, gebaar in live-uitzending). Deze **onomkeerbaarheid** is een extra term die "uniciteit" (non-fungible karakter) in het werk creëert.

### 🔎 Casestudie: AI "Instant Output" vs. Mens "Bewezen Proces"

Het volgende scenario laat zien hoe het **PoArt Waardestelling** in de praktijk werkt en waarom AI-producties laag scoren in de [PoArt]-standaard.

#### Scenario A: Visuele Productie met AI in 10 Seconden

- **Duur ($\Delta t$):** $10$ seconden (proces verwaarloosbaar)
- **Arbeidskracht ($P_{\text{labor}}$):** $1$ eenheid (alleen opdracht schrijven)
- **Wilscoëfficiënt ($I_{\text{agency}}$):** $0.01$ (geen risico, geen prijs)
- **Onomkeerbaarheid ($U_{\text{irreversible}}$):** $0$ (omkeerbaar / kopieerbaar)

**Resultaat:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Commentaar:** Zelfs als de output perfect is; omdat het proces niet is doorleefd en geen wilskracht/risico bevat, nadert de [PoArt]-waarde tot $0$.

#### Scenario B: 6 Uur Fysieke Productie in Live Uitzending

- **Duur ($\Delta t$):** $6$ uur ($21{,}600$ seconden)
- **Arbeidskracht ($P_{\text{labor}}$):** $0.5$ eenheid (continuïteit van fysieke en mentale inspanning)
- **Wilscoëfficiënt ($I_{\text{agency}}$):** $0.9$ (beslissingen veranderen, risico nemen, onomkeerbare keuzes)
- **Onomkeerbaarheid ($U_{\text{irreversible}}$):** $>0$ (fysieke sporen kunnen niet worden teruggedraaid)

**Resultaat:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Commentaar:** Naarmate het proces langer wordt en de wilskracht (risico) toeneemt, groeit de waarde cumulatief. De term $U_{\text{irreversible}}$ is een extra bijdrage die "uniciteit" (non-fungible karakter) in het werk creëert.

---

### ✅ Conclusie: Waarde Vergrendeld met Bewijs (Proof-Bound Value)

Dit theorema koppelt de waardeclaim van [PoArt] los van een "like" of "marktnarratief" en bindt het aan een **bewijsbare productierealiteit**.

1. **Geen Waarde Zonder Proces:**  
   AI vernietigt het proces in instant output ($t \to 0$). Naarmate het procesvenster verkleint, krimpt het resultaat van de integraal met wiskundige noodzaak:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Wilskracht en Risico zijn Vermenigvuldigers:**  
   [PoArt] meet niet alleen "bestede tijd"; maar ook de echte beslissing, risico en prijslaag in die tijd. De waarde van een productie die geen risico neemt (AI) is laag:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Uniciteit is Fysiek Bewijs, Geen Marketing:**  
   Onomkeerbare sporen in fysieke productie (canvasslag, marmerscherf) vallen buiten de `Ctrl+Z`-logica in digitaal. Deze onomkeerbaarheid ($U_{\text{irreversible}}$) maakt het werk ontologisch uniek.

> **🔐 SAMENVATTING:** Hoewel het waardestelling onzeker lijkt als meting (zelfs als het niet 100% kan worden gemeten in het echte leven), is het doel van deze formule; het opzet en de richting van de variabelen te tonen. Wat schaars is in het AI-tijdperk is niet "beeld"; maar **bewijsbare arbeid, tijd en wilskracht.** [PoArt] meet deze schaarste en registreert deze met het **Evidence Pack**.

### 🏛️ Het Belang van het "Engine" (Motor) Concept

Tokens die voortkomen uit Pump.fun of soortgelijke platforms zijn vaak slechts **"toegangstickets"**. De **PoArt Forensic Engine (PFE)** is daarentegen de **constitutionele logische laag** die bepaalt welke rechten dat ticket beschermt, hoe arbeid wordt geregistreerd en hoe kunst/wetenschap/technologie wordt geëeterniseerd.

> **Opmerking:** De reden dat we dit project op Pump.fun hebben gelanceerd, is omdat we niet voldoende liquiditeit en voldoende aantal volgers hadden. Het gebruik van de bestaande data was strategisch gezien niet de hoogste kwaliteit, maar we kunnen zeggen dat het de juiste zet was. Onafhankelijk van budget en middelen bewijst het definiëren van de logica van deze motor op GitHub dat het project niet alleen een financiële speculatie is, maar een langetermijn **software-infrastructuur** en **digitale nationale bibliotheek** visie.

---

## 🎨 [PoArt] BEWIJS VAN ARBEID PROTOCOL (Proof of Art Protocol v1.0)

> **"Echte Kunstenaar, Echte Productie, Echte Waarde."**

Dit protocol is ontwikkeld als een **biologisch en intellectueel verdedigingsmechanisme** tegen anonieme oplichters die het crypto-ecosysteem teisteren, kunstmatige intelligentie visuele elementen geproduceerd in 5 minuten, en de "Pump & Dump" cultuur.

---

## a) Wat is [PoArt]? (Filosofische en Technische Definitie)

**Proof of Art [PoArt];** is een institutionele verificatiestandaard die garandeert dat de waarde achter een bezit op de blockchain niet is gebaseerd op speculatie, maar op verifieerbare **menselijke arbeid**, **tijd** en **fysieke energie**.

Net zoals Bitcoin waarde creëert met *"Elektriciteit en Processorkracht"* **(Proof of Work)**; creëren [PoArt]-conforme projecten waarde met *"Artistiek Talent en Menselijke Tijd"*.

Het elimineert het risico van *"Developer (Dev) verkocht, project beëindigd"* op Pump.fun en DEX-platforms; omdat hier waarde niet in code zit, maar in **de continuïteit van productie**.

> **[PoArt] zegt niet tegen de deelnemer "Vertrouw ons"; het zegt "Hier is het bewijs, zie met je eigen ogen, verifieer met je wiskunde".**

---

## b) [PoArt] 5-voudig Standaard (The 5 Pillars of Truth)

Deze 5 items zijn niet-manipuleerbare filters die een project moet doorstaan om het [PoArt]-zegel te ontvangen.

### 1) Live Identiteitsbewijs (Live Identity Proof)

- **Probleem:** De cryptowereld zit vol anonieme oprichters (Devs) met onduidelijke identiteit die geld inzamelen en het project verlaten.
- **[PoArt] Oplossing:** De producent bewijst niet alleen een identiteitskaart, maar **zijn aanwezigheid tijdens de productie**. Dit omvat geen vooraf opgenomen video's, maar live-uitzendingssessies waarin interactie met de gemeenschap plaatsvindt en specifieke directe verzoeken worden vervuld.  
  (bijv.: *"Schrijf de datum van vandaag en het huidige bloknummer in de rechterhoek van het canvas"*)
- **Motto:** *"Bots kunnen schilderen, maar bots zweten niet en kunnen niet improviseren."*

### 2) Arbeid en Procesbewijs (Labor & Process Proof)

- **Probleem:** AI (Kunstmatige Intelligentie) visuele elementen geproduceerd in 2 seconden en een olieverfschilderij gemaakt in 2 maanden krijgen dezelfde "jpeg" behandeling in de digitale wereld.
- **[PoArt] Oplossing:** Het "zwangerschap en geboorte" proces van het werk wordt geregistreerd. Schetsfasen, verflagen, cumulatieve uren besteed en het fysieke proces dat de kunstenaar doormaakte tijdens het creëren van dat werk worden gedocumenteerd. Dit voegt **"Tijdkosten" (Time Cost)** toe aan de token. Hoe moeilijker de productie van een bezit, hoe solider de waarde.

### 3) Esthetische Waardebewijs (Aesthetic Value Proof)

- **Probleem:** De "Meme"-cultuur die esthetiek en artistieke diepte negeert en zich alleen richt op momentane komedie, resulterend in kortdurende "Hype"-projecten.
- **[PoArt] Oplossing:** Het project moet voldoen aan academische kunststandaarden, kleurtheorie, compositieregels en materiaalkennis (Impasto, Textuur, enz.). De inhoud mag niet alleen vermaken; het moet bewondering wekken bij de kijker en **collectiewaarde** hebben.

### 4) Conceptuele Innovatie (Conceptual Novelty)

- **Probleem:** Duizenden hond/kat coins die kopieën van elkaar zijn, verstoken van creativiteit.
- **[PoArt] Oplossing:** Het project moet een nieuwe brug bouwen die kunst, wetenschap, filosofie of technologie combineert in een betekenisvolle structuur.  
  (bijv.: Het klassieke David-beeld combineren met crypto-marktgegevens; het idee van menselijke perceptie die "verstenen" verwerken en dit kunnen onderbouwen met wetenschappelijke bronnen.)  
  Het werk moet niet alleen een visueel feest zijn; maar ook een intellectuele uitdaging die doet nadenken over **Wetenschap, Filosofie of Technologie**.

> [!IMPORTANT]
> **Referentie Voorbeeld (Las Palmitas Effect):**  
> In de met misdaad worstelende wijk Las Palmitas in Mexico zijn meer dan 200 huizen getransformeerd in een gigantisch regenboogfeest. Als gevolg van deze esthetische interventie zijn de misdaadcijfers in de wijk tot op zekere hoogte gedaald, zijn jongeren zich bezig gaan houden met kunst in plaats van bendes. Esthetische verandering heeft het respect van mensen voor hun omgeving en voor elkaar (Social Cohesion) opnieuw gecodeerd.
>
> **Verwachting:** Een project dat op de [PoArt]-lijst komt; moet, net als in het bovenstaande voorbeeld, een sociologische, wetenschappelijke of filosofische oorzaak-gevolg relatie bevatten die verder gaat dan louter visuele esthetiek. Omdat "Tijd" het enige bezit is dat niet met geld kan worden gekocht, moet in dit protocol tijd worden bewezen door te worden gestaked als onderpand. De intellectuele basis van het project moet zo sterk en universeel zijn dat; zelfs in een mogelijk CTO (Community Take Over) scenario jaren later, de gemeenschap deze erfenis kan overnemen en het innovatieve potentieel van het project autonoom kan voortzetten.

### 5) Niet-Algoritmische Wilskracht (Non-Algorithmic Agency)

- **Probleem:** Perfecte maar zielloze, zich herhalende digitale producties.
- **[PoArt] Oplossing:** De authentieke wilskracht van de mens die fouten kan maken, risico's neemt en emotionele schommelingen ervaart, moet voelbaar zijn in het werk. De onzekerheid in penseelstreken, de onverwachte reacties van materiaal en de momentane beslissingen van de kunstenaar zijn de **Biologische Handtekening** die het werk onderscheidt van "Machineproductie".

---

## c) Verificatie & Anti-Vervalsingsmechanisme

Dit systeem zorgt ervoor dat het project niet alleen "aan het begin" maar "voor altijd" betrouwbaar en levend blijft.

### 📦 Bewijspakket (Evidence Pack - The Digital Twin)

Achter elk [PoArt]-gecertificeerd werk bevindt zich een versleuteld en voorzien van tijdstempel datapakket dat investeerders kunnen downloaden:

- **RAW Video-opnames:** Ononderbroken ruwe beelden van het productiemoment.
- **Metadata Analyse:** Aanmaakdatum van het bestand, gebruikte apparaatinformatie en locatiegegevens.
- **Fysieke Referenties:** Bewijs dat het werk bestaat in de fysieke wereld  
  (bijv.: Actuele krant naast het werk of blockchain-gegevens van dat moment).

> *Consistentienota:* De uitdrukking "bewijspakket" is verbonden met de lijn **Evidence Pack → EvidenceRoot → NotarySeal** in eerdere secties; d.w.z. de integriteit van het pakket wordt vertegenwoordigd door een verifieerbaar zegel.

### 🔄 365-dagen Vernieuwing (The Sustainability Protocol)

- **Revolutionaire Eigenschap:** In crypto-projecten lanceert de "Dev" (Ontwikkelaar) de token op de markt en verdwijnt meestal na 1-2 maanden (Soft Rug). [PoArt] maakt dit onmogelijk.
- **Regel:** De status "Verified Artist" (Geverifieerde Kunstenaar) is niet levenslang. Hij is slechts **1 jaar** geldig.
- **Werking:** De Kunstenaar/Ontwikkelaar moet elke 365 dagen een **nieuw, groot en bewijsbaar werk** aan de gemeenschap presenteren.
- **Voorbeeldscenario:** U lanceerde het project in 2026. In januari 2027 geeft het systeem een waarschuwing "Bewijsperiode Verlopen". Als de kunstenaar geen nieuwe tentoonstelling, nieuw fysiek werk of nieuwe technologische integratie presenteert, valt de "Vertrouwensbadge" van het project.
- **Resultaat:** Dit systeem zorgt ervoor dat **de inhoud nooit verouderd raakt** en dat de investeerder geen *"Is de ontwikkelaar er nog?"* angst ervaart. Het project wordt een levende studio.

### 🚩 Rode Vlag Protocol (Red Flag Protocol)

**In geval van vervalsing gedetecteerd door de gemeenschap of algoritmes (AI-gebruik, gestolen werk, gemanipuleerde video):**

1. Het certificaat wordt onmiddellijk gemarkeerd als **"GEANNULEERD" (VOID)**.
2. Bewijspakketten worden publiekelijk gelabeld als **"Vervalst"**.
3. Het project wordt op de [PoArt] zwarte lijst geplaatst. Dit versterkt het feit dat **reputatie de enige valuta** is in een gedecentraliseerde wereld.

---

## d) Conclusie: Geen Casino, Een Museum

**Pump.fun en Gedecentraliseerde Beurzen (DEX) zijn helaas momenteel casino's; lichten flitsen, iedereen jaagt op snelle winst en de bank (oplichters) wint altijd. De reden dat we het project hier lanceerden is omdat we onvoldoende budget hadden en via live-uitzendingen onze bestaande netwerk konden bereiken.**

**[PoArt] is een fort gebouwd in het midden van dit casino.**

- 🎰 Casino is gebaseerd op kaartspellen; wij zijn gebaseerd op **fysieke realiteit**.
- 🃏 Casino is vatbaar voor bedrog; wij zijn open voor **transparant bewijs**.
- ⏳ Casino is tijdelijk; wij zijn gericht op de **eeuwigheid van kunst en wetenschap**.

**De token die dit protocol gebruikt is niet alleen een "coin"; het is een digitaal aandeel met zweet, verf, code en filosofie erachter.**

---

## 🗳️ 6) BESTUUR EN OPENBAAR REGISTER (Governance & Public Registry)

**Het doel van dit gedeelte is: De [PoArt]-standaard uit het vlak van "vertrouwen in personen" halen en het omzetten in een duurzame openbare infrastructuur met registratie + verificatie + gemeenschapstoezicht.**

### 6.1 Openbaar Register (Public Registry)

- **Public Registry:** Alle goedgekeurde gegevens worden geregistreerd op `ilhanart.org/registry` (of GitHub Registry).

**Registratielogica (aanbevolen standaard - JSON path-formaat):**

Elk record dat in het register komt, draagt minimaal deze verifieerbare kernvelden:

- **Identiteit & Status:**
  - `certificate_id` (leesbare referentie)
  - `status` (active / void)
  - `void_reason` (indien van toepassing)
  - `visibility` (private / masked / public)
  - `created_at` (tijdstempel)

- **Uitgevende Instelling:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Werkinformatie:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (indien mogelijk; voor token holder identiteit)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Forensische Gegevens:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Cryptografisch Bewijs:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Bestuur:**
  - `governance.decision`
  - `governance.review_notes`

Het register kan twee lagen hebben:
- **1)** Mens-leesbare index (web listing / zoeken / filteren)
- **2)** Machine-leesbaar manifest (JSON-records; voor PFE-verificatie)

**Het "record" hier wordt verifieerbaar met de keten Evidence Pack → EvidenceRoot → NotarySeal van PFE. Het register biedt een verificatiedoel, geen "claim".**

---

### 6.2 PoArt Verified Aanvraagproces

**PoArt Verified aanvragen worden door İlhanArt Gallery beoordeeld volgens 5 PoArt-standaarden. Gemeenschapsfeedback wordt in overweging genomen, maar de definitieve beslissing berust bij het curatoriale team. Beslissingen worden transparant uitgelegd en geregistreerd op ilhanart.org/registry.**

#### Aanvraagproces

**Aanvraag:**
- Kunstenaar/project dient PoArt Verified aanvraag in
- Evidence Pack wordt voorbereid (video-opnames, metadata, live-uitzendingslinks)
- Aanvraag wordt naar İlhanArt Gallery gestuurd

**Onderzoek (30 Dagen):**
- Galerieteam onderzoekt Evidence Pack in detail
- Alle 5 PoArt-standaarden worden gecontroleerd:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Interview met kunstenaar (optioneel)

**Gemeenschapsconsultatie:**
- Evidence Pack wordt tijdens het aanvraagproces publiekelijk gedeeld
- Gemeenschap kan feedback geven via Discord en ilhanart.org/applications
- Token holders (minimum 10.000 $CULTURE) kunnen specifiek aanbevelingen doen
- **Alle feedback wordt in overweging genomen tijdens het onderzoeksproces**
- **Maar de definitieve beslissing berust bij curatoriale beoordeling**

**Beslissing:**
- Galerij keurt de aanvraag goed of wijst deze af
- Beslissingsgrondslag wordt transparant uitgelegd
- Indien goedgekeurd → PoArt Verified badge
- Indien afgewezen → Heraanvraag mogelijk na 6 maanden

**Transparantie:**
- Alle aanvragen en beslissingen worden geregistreerd op ilhanart.org/registry
- Decision record wordt publiekelijk gepubliceerd:
  - Aanvraagdatum
  - Samenvatting onderzoeksproces
  - Beslissing (Approved / Rejected)
  - Beslissingsgrondslag (korte uitleg)
  - Samenvatting gemeenschapsfeedback (anoniem)

#### Waarom Curatoriale Beslissing?

**Kwaliteitscontrole:**  
PoArt Verified-status is een badge met hoge standaarden. Curatoriale beoordeling garandeert het behoud van deze standaarden.

**Speculatieve Manipulatie Preventie:**  
Volledige on-chain governance (bijv.: Realms, DAO voting) is technisch niet mogelijk met Pump.fun tokens. Off-chain voting systemen zijn vatbaar voor whale-manipulatie en gecoördineerde aanvallen. Curatoriale beslissing elimineert dit risico.

**Operationele Efficiëntie:**  
In plaats van complexe stemming mechanismen, snel en helder beslissingsproces. Kunstenaars krijgen binnen 30 dagen resultaat.

**Gemeenschapsdeelname:**  
Gemeenschapsfeedback wordt volledig in overweging genomen en beïnvloedt het beslissingsproces. Maar de definitieve beslissing berust bij het curatoriale team beschermd tegen manipulatie.

**Toekomst:**  
Wanneer het project matured wordt (2027+), kan het gemeenschapsconsultatiemodel worden versterkt. Maar curatoriale standaardbescherming blijft permanent.

---

### 6.3 Token Utility (Token Gebruiksgebieden)

**Voordelen voor $CULTURE token houders:**

**1. Prioriteitstoega ng Galerij Evenementen:**
- İlhanArt Gallery fysieke tentoonstelling openingen
- Kunstenaarsontmoetingen en atelierbezoeken
- Speciale collectie bekijkingen

**2. PoArt Registry Volledige Toegang:**
- Gedetailleerde records van alle geauthenticeerde kunstwerken
- Volledige versies van Evidence Packs
- Forensische verificatie tools

**3. NFT Mint Prioriteit:**
- Whitelist-toegang wanneer PoArt Verified werken als NFT worden gemint
- Vroege mint-mogelijkheden
- Speciale collectie NFT's

**4. Advisory Voting:**
- Adviesrecht in PoArt Verified aanvragen
- Toegang tot gemeenschapsfeedback kanalen
- Deelname aan governance discussies

**5. Exclusieve Content:**
- Studio behind-the-scenes inhoud
- Kunstenaarsinterviews en procesvideos
- Technische documentatie toegang

**Opmerking:**  
Token holders geven advisory vote (advies stem). De definitieve beslissing berust bij het curatoriale team. Deze structuur is gekozen om whale-manipulatie en speculatieve aanvallen te voorkomen. Er is geen staking reward omdat we op zoek zijn naar langetermijn culturele deelnemers, niet kortetermijn mercenary capital.

---

### 6.4 Metadata Sync (Synchronisatie met Fysieke Wereld)

- **Metadata Sync:** Technische gegevens in het register moeten 100% overeenkomen met het fysieke bezit.

**"100% overeenkomst" technisch definiëren (aanbevolen helderheid):**

- **Minimale overeenkomst (verplicht):**
  - De `asset.fingerprints.sha256/sha512` in het register en de hash van het bestand in handen moeten **exact hetzelfde** zijn.
  - Wanneer de `proof.notary_seal` in het register opnieuw wordt gegenereerd (als Evidence Pack aanwezig is), moet deze **exact hetzelfde** zijn.

- **Fysieke referentie overeenkomst (bewijs type):**
  - Bewijs zoals fysiek werk + datum/blok referentie getoond in live-uitzending moet consistent zijn met Evidence Pack.

- **Privacy naleving:**
  - Velden zoals IP/locatie bij `masked` zichtbaarheid worden gepubliceerd **volgens maskeringstandaard**.

---

### 6.5 Bezwaar, Onderzoek en Annulering (Dispute & Revocation)

Het register is niet alleen een "goedkeurings"mechanisme; maar een **levend toezichtsmechanisme tegen vervalsing**.

- Wanneer een bezwaar wordt gestart, kan het record in **"review"** modus worden gezet.
- Als vervalsing wordt gedetecteerd, wordt het gemarkeerd als `status: void` en reden toegevoegd:
  - `void_reason` (AI-gebruik / gestolen / manipulatie etc.)
  - `revoked_at` (annuleringstijd)
- De bron van de annuleringsbeslissing is duidelijk zichtbaar in het register:
  - curatoriale beoordeling / gemeenschapsbezwaar / forensische analyse nota (wat van toepassing is)

> **Dit gedeelte is de correspondentie op het register van het VOID-concept in de "Red Flag Protocol" sectie.**

---

### 6.6 Voorbeeld Registerrecord (Machine-leesbaar)
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

> *Opmerking: `asset.fingerprints.sha512` en andere hash-waarden zijn verkort voor weergavedoeleinden; in werkelijke toepassing wordt een hexadecimale tekenreeks van volledige lengte gebruikt.*

---

## 7) 🔐 TECHNISCH ZEGEL (NOTARY SEAL)

**Onwrikbaar zegelalgoritme geproduceerd door PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Digitale Notaris & Forensisch Bewijsprotocol (Beta v1.0)

> **"Cultuur is groter dan kapitaal. Bescherm uw werken vanaf vandaag, draag ze over naar morgen."**

---

## Waarom Publiek?

Echte veiligheid komt van transparantie. Dankzij ons **Public Registry (Openbaar Register)** systeem kan iemand overal ter wereld; binnen enkele seconden verifiëren of het bestand in handen origineel is, zonder dat een autoriteit nodig is.

---

## 🧩 Waarom Meerdere "Zichtbaarheidsmodules"?

Dit is het meest kritieke deel van de code (visibility select menu). Deze opties stellen gebruikers in staat om de **"Privacy vs. Transparantie"** balans in te stellen:

### 🔒 Privé (Private)

- **Scenario:** De kunstenaar wil het werk nog niet publiceren, maar wil een tijdstempel plaatsen en bewijzen "ik heb dit op deze datum gemaakt".
- **Wat de Code Doet:** Schrijft gegevens naar database maar plaatst `visibility: "private"` tag. Later bij het schrijven van "Public Read" beleid kan je deze records van het publiek verbergen door `WHERE visibility = 'public'` te zeggen.

### 🕶️ Gemaskeerd (Masked)

- **Scenario:** De kunstenaar wil transparantie maar is bang dat zijn huisadres (IP-locatie) wordt gevonden.
- **Wat de Code Doet:** `maskIP` en `maskLoc` functies werken aan JavaScript-zijde. Converteert IP-adres naar vorm `88.241.***.***`, locatie naar vorm `***/TR` en stuurt gecensureerde versie naar database.
- **Privacy Opmerking:** Maskering wordt gedaan in de browser, Supabase ziet de echte locatie niet. **Maar:** Als locatiegegevens worden gebruikt via derde partij API's zoals ipapi.co, zien deze providers het IP-adres op het moment van het verzoek.
- **Verzegeling in Masked Modus:** EvidenceRoot en NotarySeal berekening wordt gedaan met gemaskeerde forensics data; zo blijft verificatie deterministisch.

### 🌍 Publiek (Public)

- **Scenario:** Volledige transparantie. Volgens [PoArt]-standaard wordt duidelijk verklaard waar, wanneer, van welk netwerk het werk is geproduceerd.

---

## 💡 Technologische Innovatie

PoArt is niet alleen een bestandsupload systeem. Het is een **"Forensische Bewijsketen" (Forensic Chain of Custody)** motor die drie verschillende technologie lagen in één pot smelt en een nieuwe standaard brengt.

**De laag die als "motor" wordt uitgelegd in dit gedeelte komt overeen met de PoArt Forensic Engine (PFE) kern in eerdere terminologie.**

### 1) Client-Side Hashing (Maximale Privacy)

Uw werkbestanden worden nooit naar de server geüpload. Onze browser-gebaseerde (Client-side) werkende motor berekent de hash (digitale samenvatting) van het bestand op uw eigen computer. Alleen deze vingerafdruk en metadata worden naar de server gestuurd.

> **Privacy Opmerking:** Werkbestand wordt niet naar server geüpload en wordt zo beschermd. Maar forensics-gegevens (IP/locatie) worden gedeeld volgens geselecteerde zichtbaarheidsmodus (private/masked/public).

### 2) Forensic Data Fusion (Forensische Kracht)

Het is veel meer dan een gewone tijdstempel (Timestamp). Het systeem combineert de volgende gegevens in één "Genesis Zegel":

- **Digitale Samenvatting (SHA-512):** Digitale vingerafdruk die zal breken als zelfs één pixel van het werk verandert, met behulp van cryptografische samenvatting (SHA-512) standaard.
- **Locatie & Tijd:** Datum met milliseconde nauwkeurigheid, land, stad en district gegevens van waar de transactie plaatsvond.
- **Apparaat Identiteit:** Besturingssysteem, browser en apparaattype (User-Agent analyse).

---

## 🛡️ Gebruiksgebieden en Voordelen

Als u een kunstenaar, schrijver of ontwerper bent, is het niet genoeg om te zeggen "Ik heb dit eerder gemaakt", u moet het bewijzen.

**Een werk verzegeld met PoArt:**

- **Wiskundig Bewijs:** Als zelfs één pixel van uw bestand verandert, merkt het systeem dit. Manipulatie is onmogelijk.
- **Juridische Basis:** Het is geregistreerd op welke datum, in welke stad, vanaf welk apparaat het werk is verzegeld.
- **Onmiddellijk Certificaat:** Binnen enkele seconden genereert het een persoonlijk, QR-code en verzegeld **"Bezit Identiteitscertificaat"** voor u.

---

## ⚙️ Systeemarchitectuur en Technische Specificaties

Het systeem is ontworpen op een "Serverless" architectuur, gericht op hoge prestaties en schaalbaarheid.

| Laag | Technologie | Beschrijving |
|--------|-----------|----------|
| **Cryptografie** | SHA-256 & SHA-512 | Dubbel-laags cryptografische samenvatting |
| **Database** | Supabase (PostgreSQL) | JSONB datastructuur, RLS policies |
| **Forensische Data** | ipapi.co API | IP/Locatie/Tijd drieluik |
| **Rendering** | html2canvas + jsPDF | Client-side PNG/PDF generatie |
| **Frontend** | Vanilla JavaScript | Nul framework dependency |
| **Beveiliging** | Client-side hashing | Bestand gaat nooit naar server |

### Uitstekende Functies

| Functie | Detail | Bij Concurrenten? |
|---------|-------|-------------|
| **Drag & Drop UI** | Bestand slepen-neerzetten, onmiddellijke preview | ❌ Bij de meeste niet |
| **Multi-Format Export** | PNG, JSON, PDF - met één klik | ⚠️ Beperkt |
| **Real-Time Preview** | Certificaat live preview | ❌ Niet |
| **Privacy Controls** | Private/Masked/Public opties | ❌ Niet |
| **Client-Side Hashing** | Bestand gaat nooit naar server | ✅ Slechts bij enkelen |
| **Forensic Metadata** | IP, locatie, apparaat, tijd - allemaal samen | ❌ Gefragmenteerd |
| **QR Verification** | Onmiddellijke verificatie QR-code | ⚠️ Beperkt |
| **Rate Limiting** | Spam bescherming (RLS + Client) | ❌ Bij de meeste niet |

---

## 🗺️ Roadmap: "Trustless" Toekomst

De huidige versie **(Beta v1.0)** is geoptimaliseerd om de eindgebruiker maximale snelheid, gemakkelijke interface en gratis toegang te bieden. Maar onze ultieme visie is om over te gaan naar een structuur waarin zelfs de databasebeheerder (wij) niet kan ingrijpen.

### Fase 1: Beta v1.0 (Nu Live)

**Infrastructuur:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + IPFS backup)
- Gallery self-attestation (gecentraliseerd maar transparant)

**Token:**
- Platform: Pump.fun
- Liquidity: Raydium (automatic)
- Governance: Advisory only (gemeenschapsconsultatie)

**Doel:**
- Snelheid, UX-barrières verwijderen
- "Wrijvingsloze" beveiliging bieden
- Gemeenschap bouwen

**Token Utility (v1.0):**
- Galerij evenementen prioriteitstoega ng
- PoArt Registry bekijken
- Advisory voting recht

---

### 🚀 Fase 2: Gedecentraliseerd Gezag (2026 Q2-Q4)

Deze fase omvat de overgang van de volledig "Client-Side" werkende structuur van het systeem naar een veiligere en gedecentraliseerde structuur.

| Functie | Wat Brengt Het? | Tech Stack | ETA |
|---------|---------------|------------|-----|
| **Edge Function INSERT** | Spam blokkade + API Key beveiliging | Supabase Edge (Deno) | Q2 2026 |
| **Wallet Handtekening** | Decentralized identity | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | Gedecentraliseerd archief | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | Vals certificaat annulering | DB Schema Update | Q2 2026 |
| **Audit Log** | Forensische vraag registratie | Custom logs table | Q3 2026 |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain voting (Discord/web) + wallet signature
- Community representatives selectie (eerste 90 dagen)
- Multi-sig operations wallet controle
- Weighted advisory voting (met whale cap)

**Onveranderlijkheid:**
- Registry backup met IPFS hashes
- Bitcoin timestamp anchoring
- Cross-chain verificatie voorbereiding

---

### Fase 3: Volledige Decentralisatie (2027+)

| Functie | Doel | ETA |
|---------|-------|-----|
| **On-Chain Registry** | Solana on-chain registratie | Q1 2027 |
| **Enhanced Token Utility** | NFT mint, advanced features | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **DID Integration** | Decentralized Identity | Q3 2027 |
| **Community Governance** | Versterkt advisory system | Q4 2027 |
| **Legal Recognition** | Geldigheid in Nederlandse rechtbanken | 2027-2028 |
| **API for Developers** | Public API endpoint | Q3 2027 |

**Governance Evolutie:**
- v3.0: Hybride model (curatoriale + community weighted)
- 2028+: Full community governance (optioneel)
- Curatoriale kwaliteitscontrole blijft altijd behouden

---

## 🧬 Protocol Datastructuur (JSON Schema)

**Elk [PoArt] certificaat heeft een draagbare en verifieerbare JSON-identiteitskaart geproduceerd in de onderstaande standaard.**

> **Opmerking:** Dit Identity JSON-formaat is het certificaatformaat gepresenteerd aan de gebruiker. In registerrecords wordt `registry.asset` gebruikt in plaats van `identity.asset_data` (mapping: `identity.asset_data` == `registry.asset`).
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

## 🔬 Technische Diepte: Zegelalgoritme

### Deterministische Hash-functies
```javascript
// Hulpfuncties: Digest converteren naar hex string
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// String converteren naar byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Canonical forensics string productie (v1.0: vaste veldvolgorde + UTF-8 + \n delimiter)
// Fase 2 opmerking: Overgang naar canonical JSON met RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal Productieproces (Volledig Deterministisch)
```javascript
// 1. FileHash berekening (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Forensic data verzameling (enkele timestamp gebruik)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Enkele timestamp productie
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Zelfde timestamp
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot creatie (met canonical encoding)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal productie (zelfde timestamp gebruik)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Maskering hulpfuncties (IPv4 en IPv6 ondersteuning)
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4 controle
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 of onbekend formaat
  return "***";
}
```

### Verificatiestroom (Twee Niveaus)

#### Quick Verify (Snelle Verificatie)
```javascript
// Controleert alleen bestands hash (snelle rode vlag)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Ophalen uit Register
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Hash vergelijking
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Origineel - Bestands hash komt overeen"
    };
  } else {
    return {
      valid: false,
      message: "❌ Vervalst - Bestand gemanipuleerd"
    };
  }
}
```

#### Full Verify (Volledige Verificatie)
```javascript
// EvidenceRoot en NotarySeal opnieuw genereren en verifiëren
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Ophalen uit Register
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash controle (snelle rode vlag)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Vervalst - Bestands hash komt niet overeen" };
  }

  // 2) EvidenceRoot opnieuw genereren (met forensics opgeslagen in register)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Komt niet overeen - EvidenceRoot klopt niet" };
  }

  // 3) NotarySeal opnieuw genereren (met zelfde timestamp + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Komt niet overeen - NotarySeal klopt niet" };
  }

  // Optioneel: In Fase 2 ook signer_sig verifiëren met attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Handtekening ongeldig" };

  return { valid: true, message: "✅ Origineel - Full Verify geslaagd" };
}
```

> **Belangrijke Opmerkingen:**
> - **Quick Verify:** Controleert alleen bestands hash voor snel gebruik.
> - **Full Verify:** Verifieert alle lagen van het protocol (EvidenceRoot + NotarySeal).
> - Alle hash-operaties worden deterministisch uitgevoerd, met vaste encoding en delimiters.
> - **v1.0 canonicalization standaard:** Vaste veldvolgorde + UTF-8 encoding + `\n` delimiter.
> - **Fase 2 plan:** Overgang naar canonical JSON met RFC 8785 (JCS - JSON Canonicalization Scheme).
> - In masked modus wordt EvidenceRoot en NotarySeal berekening gedaan met gemaskeerde forensics.
> - Enkele timestamp wordt gebruikt in het hele proces (forensics + NotarySeal); determinisme gegarandeerd.
> - **Forensics veldnamen:** `ip_masked`, `location`, `device`, `timestamp` (code en register volledig compatibel).
> - **Register path:** `certificate.asset.fingerprints` (volledig compatibel met verify code).
> - **Register signer_sig:** `proof.signer_sig` veld is vereist voor Full Verify.
> - SignerSignature mechanisme wordt geactiveerd in Fase 2 met Solana Wallet Adapter; in v1.0 kan verificatie worden gedaan met `attestation_pubkey`.

---

## 📊 Concurrent Analyse (Bijgewerkt)

PoArt is gepositioneerd op de "Sweet Spot" (Meest ideale punt) dat de tekortkomingen van bestaande oplossingen aanvult.

| Functie | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Kosten** | 🆓 Gratis | 🆓 | 💰 Betaald | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Zeer Makkelijk | ❌ CLI | ⚠️ Gemiddeld | ⚠️ Gemiddeld | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Live | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Modi | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privacy | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Volledig | ❌ | ❌ | ⚠️ Beperkt | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Onmiddellijk | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Nederlandse Ondersteuning** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Toelichting:**
- ✅ : Volledige ondersteuning / aanwezig
- ⚠️ : Beperkt / in betaalde abonnementen
- ❌ : Niet / niet ondersteund
- 🔄 : In Roadmap (in ontwikkeling)
- 🆓 : Volledig gratis
- 💰 : Betaald / abonnement vereist

### Tekortkomingen van Concurrenten, Sterke Punten van PoArt

| Tekort | Concurrenten | PoArt |
|------|----------|-------|
| **Gebruiksmoeilijkheid** | CLI, API-kennis, portemonnee vereist | Slepen-neerzetten, klaar in 3 klikken |
| **Kostenbarrière** | $50-500/maand abonnement | 100% gratis |
| **Privacy** | Bestand wordt naar server geüpload | Client-side, bestand gaat nooit weg |
| **Forensische Data** | Alleen timestamp | IP, locatie, apparaat, tijd - allemaal |
| **Nederlandse Ondersteuning** | Niet of zeer beperkt | Native taalondersteuning |
| **Open Source** | Gesloten doos | Alle code open op GitHub |

---

## 📈 Gebruiksstatistieken (2026 Q1 Doelen)

| Metriek | Doel | Status |
|--------|-------|-------|
| **Totaal Certificaten** | 1.000 | 🔄 In uitvoering |
| **Actieve Gebruikers** | 500 | 🔄 In uitvoering |
| **Verificatie Aantal** | 5.000 | 🔄 In uitvoering |
| **Uptime** | 99,9% | ✅ Actief |
| **Gem. Responstijd** | <200ms | ✅ Optimaal |

---

## 🌍 Gemeenschap & Ondersteuning

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Bijdragers

Het PoArt-protocol blijft zich ontwikkelen met bijdragen van de open source gemeenschap.

**Om bij te dragen:**
1. Fork maken
2. Feature branch maken (`git checkout -b feature/amazing-feature`)
3. Commit maken (`git commit -m 'Add amazing feature'`)
4. Push maken (`git push origin feature/amazing-feature`)
5. Pull Request openen

### 🛠️ Waar Hebben We Nu Hulp Bij Nodig? (Hulp Oproep)

Voor **Fase 2** ontwikkelingen van het PoArt Protocol verwachten we bijdragen van ervaren ontwikkelaars in de volgende onderwerpen:

* **Supabase Edge Functions:** Spam-bescherming naar serverside verplaatsen.
* **Solana Web3.js:** Portemonnee handtekening (Wallet Signing) integratie.
* **IPFS / Arweave:** Archivering en pinning services integratie.
* **Community Tools:** Discord bot, voting systems, analytics dashboard.

> Gelieve een discussie te starten in het "Issues" tabblad voordat u een functie toevoegt.

---

## 💬 Slotnotities

### Pump.fun en Realiteit

Dit project is gelanceerd op Pump.fun omdat:
- ✅ Liquiditeitstoegang (Raydium automatic migration)
- ✅ Toegang tot bestaande gemeenschap
- ✅ Lage startkosten

Maar laten we dit verduidelijken:
- **Token prijs** is geen indicator van artistiek succes
- Token waarde is belangrijk voor **operationeel budget** (galerij, tentoonstellingen, infrastructuur)
- **Succesindicatoren:** Authenticated artworks + community engagement + fysieke bezoekers

### Bestuur en Decentralisatie

**v1.0 Realiteit (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (gecentraliseerd maar transparant)
- Governance: Advisory only (curatoriale definitieve beslissing)
- Token utility: Gallery access + registry + NFT priority

**v2.0+ Visie (2027+):**
- Registry: On-chain (Solana)
- Signatures: Wallet-based (decentralized)
- Governance: Hybrid (community advisory + curatorial quality)
- Token utility: Enhanced features + advanced access

Deze structuur biedt **operationele efficiëntie** en **kwaliteitscontrole** in een vroeg stadium, terwijl de weg wordt opengehouden om **gemeenschapsdeelname** in de toekomst te verhogen.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Cultuur is Groter dan Kapitaal*

## 🧾 Licentie

MIT License © 2026 İlhan Art Gallery Initiative

Zie [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) voor volledige voorwaarden.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Dit project is ontwikkeld met het [İlhan Art Gallery] initiatief en de broncode is publiekelijk toegankelijk in het kader van transparantie.**

**PROTOCOL V1.0 // VERZEGELD MET SHA-512.**

*© 2026 İLHAN ART | ALLE RECHTEN OP WERKEN, VISUELE ELEMENTEN EN IDEEËN VOORBEHOUDEN.*

---
