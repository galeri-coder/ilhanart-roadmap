# 📚 TERMINOLOGIE & BEGRIPPEN WOORDENBOEK
> **"De taal van dit protocol begrijpen betekent de visie ervan begrijpen."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Kerninfrastructuur

**PoArt Forensic Engine (PFE)** is de hoofdlaag die de kernlogica en technische werking achter het [PoArt] protocol vertegenwoordigt. Dit is de "forensische motor" die de ruwe productiegegevens van het kunstwerk neemt en transformeert in een verifieerbaar en onveranderlijk **digitaal bewijs**.

### 🧩 Waarom "PoArt Forensic"?

- **PoArt (Proof of Art):** De focus van de motor is om de waarde van een digitaal activum niet te koppelen aan speculatie, maar aan het **verifieerbare productieproces**.
- **Forensic (Forensische Verificatie):**
  - **Technische Definitie:** Algoritmische methoden en registerketens om te verifiëren dat productieprocessgegevens (penseelstreken, timelapse, logs) niet zijn gemanipuleerd.
  - **Filosofische Laag:** De bewering om de **menselijke tijd-, inspannings- en beslissingskosten** van AI's "instant output" te transformeren in een meetbare realiteit.

> Opmerking: Blockchain (bijv. Solana) integratie is niet de kern van PFE; het wordt apart gedefinieerd als een **Chain Anchor Layer** voor verificatie/registry doeleinden.

### 🛠️ v1.0 Technisch Bereik

**PoArt Forensic Engine (PFE) v1.0** is gebouwd op de volgende **3 hoofdpilaren** in plaats van complexe financiële modellen:

1. **Hashing & Sealing (Verzegeling):**  
   PFE verwerkt alle elementen in het Evidence Pack (werkbestand, video, JSON/log, handtekening, enz.) deterministisch en genereert een unieke **NotarySeal** waarde.

   **Kernconcepten (v1.0):**
   - **FileHash (digitale vingerafdruk van werk):** Hash gegenereerd uit de bytes van het werkbestand.
   - **EvidenceRoot (bewijspakket wortel):** Wortel samenvatting die de integriteit van het Evidence Pack vertegenwoordigt (Merkle root of canonieke manifest hash).
   - **NotarySeal (definitieve zegel / PFE Output):** Definitieve zegel gegenereerd uit de combinatie EvidenceRoot + tijd + handtekening.

   **Formules (duidelijk zichtbaar voor investeerders):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonieke Payload Definities (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Opmerking: De waarde bedoeld als PFE output is **NotarySeal**. Het **SignerSignature** mechanisme wordt geactiveerd in Fase 2 (met Solana Wallet Adapter); in de huidige v1.0 wordt de systeem attestation handtekening gebruikt. De attestation publieke sleutel wordt gepubliceerd in het register onder het `issuer.attestation_pubkey` veld.

2. **Indexing (Archivering):**  
   Schrijft naar een transparante en bevraagbare registerlaag welke wallet, op welke datum, **Labor Proof (Arbeidsbewijs)** heeft ingediend voor welk werk.  
   *(Deze laag kan een database zijn; keten integratie wordt apart gedefinieerd als "Chain Anchor Layer".)*

3. **Verification (Verificatie):**  
   Wanneer de authenticiteit van een werk in twijfel wordt getrokken, herverwerkt PFE de ruwe bewijzen; het verifieert wiskundig of de berekende **EvidenceRoot / NotarySeal** waarden overeenkomen met de opgeslagen records.

---

### 🧮 PoArt Waarde Theorema (The Value Theorem)

Het [PoArt] protocol koppelt de waarde ($V$) van een digitaal activum niet aan subjectieve marktperceptie, maar aan de **fysieke realiteit van het productieproces**.

Kunstmatige Intelligentie (AI) vernietigt het proces door instant resultaten te leveren ($t \to 0$). [PoArt] daarentegen beschouwt waarde als de accumulatie van **tijd, arbeid en wilskracht** componenten.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Variabele Definities

- **$\int dt$ (Proces Accumulatie):**  
  Waarde is geen instant "output"; het is een **proces** dat zich accumuleert tussen $t_{\text{start}}$ en $t_{\text{end}}$. Wanneer de duur afneemt (AI productie), nadert het integraalresultaat tot 0.

- **$P_{\text{labor}}(t)$ (Instant Arbeidskracht):**  
  Vertegenwoordigt de intensiteit van mentale en fysieke inspanning die tijdens de productie wordt besteed. Wanneer verifieerbare inspanning toeneemt, neemt de integrand toe.  
  > Opmerking: Deze term kan praktisch worden genormaliseerd over "meetbare/verifieerbare arbeidssignalen".

- **$I_{\text{agency}}(t)$ (Wilskracht Factor):**  
  Het vermogen van de schepper om risico's te nemen en beslissingen te nemen. Neemt een waarde aan tussen $0$ en $1$.
  - **AI ($I \approx 0$):** Voert commando's uit, neemt geen risico, betaalt geen prijs.
  - **Mens ($I \to 1$):** Verandert beslissingen, twijfelt, neemt risico's.

- **$U_{\text{irreversible}}$ (Onomkeerbare Uniciteit):**  
  Hoewel in digitale productie annuleren mogelijk is (`Ctrl+Z`), is er in fysieke productie (verf op canvas, gehouwen marmer, gebaar in livestream) geen terugweg. Deze **onomkeerbaarheid** is een additionele term die "uniciteit" (non-fungible karakter) in het werk creëert.

### 🔎 Case Analyse: AI "Instant Output" vs. Mens "Geverifieerd Proces"

Het volgende scenario toont hoe het **PoArt Waarde Theorema** in de praktijk werkt en waarom AI-producties lagere scores krijgen op de [PoArt] standaard.

#### Scenario A: 10 Seconden Visual Productie met AI

- **Duur ($\Delta t$):** $10$ seconden (verwaarloosbaar kort proces)
- **Arbeidskracht ($P_{\text{labor}}$):** $1$ eenheid (alleen commando schrijven)
- **Wilskracht Factor ($I_{\text{agency}}$):** $0.01$ (geen risico, geen kosten)
- **Onomkeerbaarheid ($U_{\text{irreversible}}$):** $0$ (omkeerbaar / kopieerbaar)

**Resultaat:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Commentaar:** Ook al is de output perfect; de [PoArt] waarde nadert $0$ omdat er geen proces heeft overleefd en er geen wilskracht/risico betrokken was.

#### Scenario B: 6 Uur Fysieke Productie in Livestream

- **Duur ($\Delta t$):** $6$ uur ($21{,}600$ seconden)
- **Arbeidskracht ($P_{\text{labor}}$):** $0.5$ eenheid (continuïteit van fysieke en mentale inspanning)
- **Wilskracht Factor ($I_{\text{agency}}$):** $0.9$ (beslissingen veranderen, risico nemen, onomkeerbare keuzes)
- **Onomkeerbaarheid ($U_{\text{irreversible}}$):** $>0$ (fysieke sporen zijn niet terugdraaibaar)

**Resultaat:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Commentaar:** Naarmate het proces zich uitbreidt en de wilskracht (risico) toeneemt, accumuleert de waarde cumulatief. De $U_{\text{irreversible}}$ term is een additionele bijdrage die "uniciteit" (non-fungible karakter) in het werk creëert.

---

### ✅ Conclusie: Bewijs-Gebonden Waarde (Proof-Bound Value)

Dit theorema trekt de waardeclaim van [PoArt] weg van "voorkeur" of "marktverhaal" en koppelt het aan **verifieerbare productierealiteit**.

1. **Geen Proces, Geen Waarde:**  
   AI vernietigt het proces met instant resultaten ($t \to 0$). Wanneer het procesvenster krimpt, moet het integraalresultaat afnemen als wiskundige noodzaak:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Wilskracht en Risico zijn Vermenigvuldigers:**  
   [PoArt] meet niet alleen "bestede tijd"; het meet ook de werkelijke beslissing, risico en prijslaag in die tijd. Productie zonder risico (AI) heeft minder waarde:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Uniciteit is Fysiek Bewijs, Geen Marketing:**  
   Onomkeerbare sporen in fysieke productie (canvasslag, marmer breuk) liggen buiten de digitale `Ctrl+Z` logica. Deze onomkeerbaarheid ($U_{\text{irreversible}}$) maakt het werk ontologisch uniek.

> **🔐 SAMENVATTING:** Hoewel het waarde theorema onzeker lijkt als meting (ook al kan het equivalent in de echte wereld niet volledig worden gemeten), is het doel van deze formule om de constructie en richting van variabelen te tonen. In het AI-tijdperk is het schaarse niet het "beeld"; het is **verifieerbare arbeid, tijd en wilskracht**. [PoArt] meet deze schaarste en registreert het met het **Evidence Pack**.

### 🏛️ Het Belang van het "Engine" Concept

Tokens die van Pump.fun of vergelijkbare platforms komen zijn vaak slechts **"toegangstickets"**. **PoArt Forensic Engine (PFE)** daarentegen is de **constitutionele logica laag** die bepaalt welke rechten dit ticket beschermt, hoe arbeid wordt geregistreerd en hoe kunst/wetenschap/technologie wordt bewaard.

> **Opmerking:** De reden dat we dit project op Pumpfun zijn gestart is vanwege onvoldoende liquiditeit en het gebrek aan een omgeving om het huidige publiek via livestreams te bereiken. Het gebruik van de huidige data is strategisch gezien de juiste zet, ook al is het niet de hoogste kwaliteit. Ongeacht budget en middelen bewijst het definiëren van deze motorlogica op GitHub dat het project niet alleen een financiële speculatie is, maar een langetermijnvisie van een **software-infrastructuur** en **digitale nationale bibliotheek**.

---

## 🎨 [PoArt] ARBEIDSBEWIJS PROTOCOL (Proof of Art Protocol v1.0)

> **"Echte Kunstenaar, Echte Productie, Echte Waarde."**

Dit protocol is een **biologisch en intellectueel verdedigingsmechanisme** ontwikkeld tegen anonieme oplichters die het crypto-ecosysteem omringen, tegen AI-visuals gemaakt in 5 minuten, en tegen de "Pump & Dump" cultuur.

---

## a) Wat is [PoArt]? (Filosofische en Technische Definitie)

**Proof of Art [PoArt];** is een institutionele verificatiestandaard die garandeert dat de waarde achter een activum op de blockchain niet gebaseerd is op speculatie, maar op verifieerbare **menselijke arbeid**, **tijd** en **fysieke energie**.

Zoals Bitcoin waarde genereert met *"Elektriciteit en Processorkracht"* **(Proof of Work)**, zo genereren [PoArt] conforme projecten waarde met *"Artistiek Talent en Menselijke Tijd"*.

Het elimineert het *"Developer verkoopt, project eindigt"* risico op Pump.fun en DEX platforms; omdat hier de waarde niet in de code ligt, maar in de **continuïteit van productie**.

> **[PoArt] zegt niet tegen deelnemers "vertrouw ons"; het zegt "hier is het bewijs, zie met je eigen ogen, verifieer met je wiskunde."**

---

## b) [PoArt] 5-Pijler Standaard (The 5 Pillars of Truth)

Deze 5 items zijn de onmanipuleerbare filters die een project moet passeren om de [PoArt] zegel te ontvangen.

### 1) Live Identiteitsbewijs (Live Identity Proof)

- **Probleem:** De crypto wereld is vol van anonieme oprichters (Devs) met onduidelijke identiteit die geld ophalen en het project verlaten.
- **[PoArt] Oplossing:** De maker verifieert niet alleen identiteit maar ook **aanwezigheid tijdens productie**. Dit omvat livestream sessies waarin interactie met de gemeenschap plaatsvindt en specifieke verzoeken onmiddellijk worden uitgevoerd, niet vooraf opgenomen video's.  
  (bijv., *"Schrijf de datum van vandaag en het huidige bloknummer in de rechterhoek van het canvas"*)
- **Motto:** *"Bots kunnen tekenen maar bots zweten niet en kunnen niet improviseren."*

### 2) Arbeids- en Procesbewijs (Labor & Process Proof)

- **Probleem:** AI (Kunstmatige Intelligentie) beelden gemaakt in 2 seconden krijgen in de digitale wereld dezelfde "jpeg" behandeling als een olieverfschilderij gemaakt in 2 maanden.
- **[PoArt] Oplossing:** Het "zwangerschap en geboorte" proces van het werk wordt geregistreerd. Schetsfasen, verflagen, bestede cumulatieve uren en het fysieke proces dat de kunstenaar doormaakte tijdens het creëren van het werk worden gedocumenteerd. Dit voegt **"Tijdkosten"** toe aan de token. Hoe moeilijker de productie van een activum, hoe sterker de waarde.

### 3) Esthetisch Waardebewijs (Aesthetic Value Proof)

- **Probleem:** De "meme" cultuur die esthetiek en artistieke diepte negeert door zich alleen te richten op instant komedie, en de daaruit voortvloeiende kortstondige "Hype" projecten.
- **[PoArt] Oplossing:** Het project moet academische kunststandaarden, kleurentheorie, compositieregels en materiaalkennis (Impasto, Textuur, etc.) hebben. Inhoud moet niet alleen laten lachen; het moet bewondering wekken bij de kijker en **verzamelwaarde** hebben.

### 4) Conceptuele Innovatie (Conceptual Novelty)

- **Probleem:** Duizenden kopieer hond/kat coins zonder creativiteit.
- **[PoArt] Oplossing:** Het project moet een nieuwe brug creëren die kunst, wetenschap, filosofie of technologie in een betekenisvolle structuur verbindt.  
  (bijv., Het klassieke David standbeeld verbinden met crypto marktgegevens; het idee van "menselijke perceptie transformeren in steen" erdoorheen verwerken en het funderen met wetenschappelijke bronnen.)  
  Het werk moet niet alleen een visueel feest zijn; het moet ook een **intellectuele uitdaging** zijn die doet nadenken over wetenschap, filosofie of technologie.

> [!IMPORTANT]
> **Referentie Voorbeeld (Las Palmitas Effect):** In de wijk Las Palmitas in Mexico, die worstelde met criminaliteit, werden meer dan 200 huizen getransformeerd in een gigantisch regenboogfeest. Als gevolg van deze esthetische interventie daalde het criminaliteitscijfer in de wijk aanzienlijk, en jongeren begonnen zich met kunst bezig te houden in plaats van met criminele bendes. De esthetische transformatie herschreef het respect van mensen voor hun omgeving en elkaar (Sociale Cohesie).
>
> **Verwachting:** Een project dat op de [PoArt] lijst komt, moet, net als het bovenstaande voorbeeld, een sociologische, wetenschappelijke of filosofische oorzaak-gevolg relatie bevatten buiten pure visuele esthetiek. Tijd is het enige kapitaal dat niet met geld kan worden gekocht, daarom moet het in dit protocol worden geverifieerd door tijd als onderpand in te zetten. De conceptuele basis van het project moet zo sterk en universeel zijn dat, zelfs jaren later, in een mogelijk CTO (Community Takeover) scenario, de gemeenschap het creatieve potentieel van het project autonoom kan voortzetten terwijl ze deze erfenis erft.

### 5) Niet-Algoritmische Wilskracht (Non-Algorithmic Agency)

- **Probleem:** Perfecte maar zielloze, elkaar herhalende digitale producties.
- **[PoArt] Oplossing:** De unieke wilskracht van de mens die fouten kan maken, risico's kan nemen en emotionele fluctuaties kan ervaren, moet voelbaar zijn in het werk. De onzekerheid in penseelstreken, onverwachte materiaalreacties en de onmiddellijke beslissingen van de kunstenaar zijn de **Biologische Handtekening** die het werk onderscheidt van "Mechanische Productie".

---

## c) Verificatie & Anti-Fraude Mechanisme

Dit systeem zorgt ervoor dat het project niet alleen "in het begin" maar "altijd" betrouwbaar en levend blijft.

### 📦 Bewijspakket (Evidence Pack - The Digital Twin)

Achter elk [PoArt] gecertificeerd werk is er een versleuteld en tijdgestempeld datapakket dat investeerders kunnen downloaden:

- **RAW Video Opnames:** Ononderbroken ruwe beelden van het productie moment.
- **Metadata Analyse:** Aanmaakdatum van bestand, gebruikte apparaatinformatie en locatiegegevens.
- **Fysieke Referenties:** Bewijs dat het werk in de fysieke wereld bestaat  
  (bijv., Huidige krant of blockchain data van die tijd naast het werk).

> *Consistentie noot:* De term "bewijspakket" in vorige secties verbindt met de **Evidence Pack → EvidenceRoot → NotarySeal** keten; dat wil zeggen, de integriteit van het pakket wordt vertegenwoordigd door een verifieerbare zegel.

### 🔄 365 Dagen Vernieuwing (The Sustainability Protocol)

- **Revolutionaire Functie:** In crypto projecten publiceert de "Dev" (Developer) de token en verdwijnt meestal na 1-2 maanden (Soft Rug). [PoArt] maakt dit onmogelijk.
- **Regel:** "Geverifieerd Kunstenaar" status is niet levenslang. Het is slechts **1 jaar** geldig.
- **Werking:** De kunstenaar/developer moet elke 365 dagen een **nieuw, significant en verifieerbaar werk** presenteren aan de gemeenschap.
- **Voorbeeld Scenario:** Project starten in 2026. In januari 2027 geeft het systeem een "Bewijs Vervallen" waarschuwing. Als de kunstenaar geen nieuwe tentoonstelling, nieuw fysiek werk of nieuwe technische integratie presenteert, daalt het "Vertrouwensbadge" van het project.
- **Resultaat:** Dit systeem zorgt ervoor dat **inhoud nooit relevantie verliest** en investeerders nooit bang hoeven te zijn voor *"Is de Developer nog hier?"*. Het project wordt een levende studio.

### 🚩 Rode Vlag Protocol (Red Flag Protocol)

**In elke fraudesituatie gedetecteerd door de gemeenschap of algoritmen (AI gebruik, gestolen werk, gemanipuleerde video):**

1. Certificaat wordt onmiddellijk gemarkeerd als **"VOID" (nietig)**.
2. Bewijspakketten worden publiekelijk geëtiketteerd als **"vals"**.
3. Project wordt op de [PoArt] zwarte lijst geplaatst. Dit versterkt dat in een gedecentraliseerde wereld **reputatie de enige valuta is**.

---

## d) Conclusie: Geen Casino, Maar Museum

**Pump.fun en Gedecentraliseerde Beurzen (DEX) zijn helaas nu casino's; lichten knipperen, iedereen jaagt op snelle winst, en het huis (oplichters) wint altijd. De reden dat we dit project hier zijn gestart is vanwege onvoldoende budget en het gebrek aan een omgeving om het huidige publiek via livestreams te bereiken.**

**[PoArt] is een fort gebouwd in het midden van dit casino.**

- 🎰 Casino is gebaseerd op kaartspellen; wij zijn **gebaseerd op fysieke realiteit**.
- 🃏 Casino staat open voor fraude; wij staan **open voor transparant bewijs**.
- ⏳ Casino is tijdelijk; wij zijn **gefocust op de eeuwigheid van kunst en wetenschap**.

**De token die dit protocol gebruikt is niet alleen een "coin"; het is digitaal eigen vermogen met zweet, verf, code en filosofie.**

---

## 🗳️ 6) GOVERNANCE EN OPENBAAR REGISTER (Governance & Public Registry)

**Het doel van deze sectie is: De [PoArt] standaard transformeren van het "vertrouw mensen" niveau naar een duurzame publieke infrastructuur met register + verificatie + gemeenschapstoezicht.**

### 6.1 Openbaar Register (Public Registry)

- **Openbaar Register:** Alle goedgekeurde gegevens worden geschreven op `ilhanart.org/registry` (of GitHub Registry).

**Register logica (voorgestelde standaard - in JSON pad formaat):**

Elk record dat het register binnengaat heeft deze minimale verifieerbare kernvelden:

- **Identiteit & Status:**
  - `certificate_id` (leesbare referentie)
  - `status` (active / void)
  - `void_reason` (indien van toepassing)
  - `visibility` (private / masked / public)
  - `created_at` (tijdstempel)

- **Uitgevende Autoriteit:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Werk Informatie:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (indien mogelijk; voor token-gated identificatie)
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

- **Governance:**
  - `governance.decision`
  - `governance.veto_threshold`

Het register kan twee lagen hebben:
- **1)** Mens-leesbare index (weblijst / zoeken / filteren)
- **2)** Machine-leesbaar manifest (JSON records; voor PFE verificatie)

**Deze "registratie" wordt verifieerbaar via de PFE keten Evidence Pack → EvidenceRoot → NotarySeal. Het register biedt een verificatiedoel, geen "claim".**

---

### 6.2 40% Gemeenschaps Veto (Token-Gated Governance)

- **40% Gemeenschaps Veto:** Stemming begint een maand voor statusverlening; **40% van de token-gated (Solana-Verified) gemeenschap** veto maakt de aanvraag ongeldig.

**Stem Flow (voorgesteld duidelijk proces):**
- **Aanvraag Venster:** Kandidaat project opent "PoArt kandidaat registratie" (kandidaat records verschijnen met "pending" status).
- **Beoordeling Periode:** Gemeenschap beoordeelt bewijs tot 30 dagen (Evidence Pack + livestream records + metadata).
- **Token-gated Verificatie:** Stemmen wordt gedaan met Solana geverifieerde wallets (bijv. bepaalde token/NFT eigendom + wallet signature).
- **Veto Regel:** Als 40% van de stemmen **bezwaar (NO / VETO)** is, wordt de aanvraag afgewezen.
- **Transparantie:** Stemresultaat wordt opgeslagen in het register als "besluit record" (datum, ratio, snapshot ID).

---

### 6.3 Metadata Synchronisatie (Afstemming met Fysieke Wereld)

- **Metadata Synchronisatie:** Technische gegevens in het register moeten 100% overeenkomen met de fysieke entiteit.

**Technische definitie van "100% afstemming" (voorgestelde openheid):**
- **Minimale afstemming (verplicht):**
  - `asset.fingerprints.sha256/sha512` in het register moet **identiek zijn** aan de hash van het besproken bestand.
  - `proof.notary_seal` in het register wanneer opnieuw gegenereerd (als Evidence Pack bestaat), moet **identiek zijn**.
- **Fysieke referentie afstemming (bewijs type):**
  - Fysiek werk + datum/blok referentie getoond in livestream en hetzelfde bewijs moet overeenkomen met Evidence Pack.
- **Privacy naleving:**
  - Velden zoals IP/locatie in `masked` zichtbaarheid worden gepubliceerd **volgens maskeringsstandaard**.

---

### 6.4 Geschil, Beoordeling en Intrekking (Dispute & Revocation)

Het register is niet alleen een "goedkeurings" mechanisme; het is een **levend toezicht** mechanisme tegen fraude.

- Wanneer een geschil begint, kan het record in **"review"** modus worden geplaatst.
- Wanneer fraude wordt gedetecteerd, wordt het gemarkeerd als `status: void` en wordt de reden toegevoegd:
  - `void_reason` (AI gebruik / diefstal / manipulatie, etc.)
  - `revoked_at` (intrekkingstijd)
- De bron van de intrekkingsbeslissing is duidelijk zichtbaar in het register:
  - gemeenschapsstem / officiële commissie / forensisch onderzoeksnotitie (welke van toepassing is)

> **Deze sectie is de register tegenhanger van het VOID concept in de "Rode Vlag Protocol" sectie.**

---

### 6.5 Voorbeeld Register Record (Machine-leesbaar)
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
> *Opmerking: `asset.fingerprints.sha512` en andere hash waarden zijn verkort voor weergavedoeleinden; in werkelijke implementatie wordt de volledige lengte hexadecimale tekenreeks gebruikt.*

---

## 7) 🔐 TECHNISCHE ZEGEL (NOTARY SEAL)

**Het onwrikbare zegel algoritme gegenereerd door PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Digitale Notaris & Forensisch Bewijs Protocol (Beta v1.0)

> **"Cultuur is groter dan kapitaal. Bescherm je werken vandaag, draag over naar morgen."**

---

## Waarom Openbaar?

Echte veiligheid komt van transparantie. Dankzij ons **Openbaar Register** systeem kan iemand overal ter wereld in seconden verifiëren of een bestand origineel is, zonder enige autoriteit nodig te hebben.

---

## 🧩 Waarom Meerdere "Zichtbaarheidsmodules"?

Dit is het meest kritieke deel van de code (zichtbaarheid selectie menu). Deze opties stellen gebruikers in staat om de **"Privacy vs. Transparantie"** balans te creëren:

### 🔒 Privé (Private)

- **Scenario:** Kunstenaar wil het werk nog niet publiceren maar wil een tijdstempel plaatsen om te bewijzen "ik heb dit op deze datum gemaakt".
- **Wat de Code Doet:** Schrijft gegevens naar de database maar stempelt `visibility: "private"`. Later bij het schrijven van "Public Read" beleid, kun je deze records verbergen voor mensen met `WHERE visibility = 'public'`.

### 🕶️ Gemaskeerd (Masked)

- **Scenario:** Kunstenaar wil transparantie maar maakt zich zorgen dat hun huisadres (IP locatie) bekend wordt.
- **Wat de Code Doet:** `maskIP` en `maskLoc` functies werken aan de JavaScript kant. Dit verandert het IP-adres naar `88.241.***.***` formaat, locatie naar `***/TR` formaat, en stuurt de gecensureerde versie naar de database.
- **Privacy Waarheid:** Maskering wordt gedaan in de browser, Supabase ziet de werkelijke locatie niet. **Maar:** Als derde partij API's zoals ipapi.co worden gebruikt voor locatiegegevens, zien deze providers het IP-adres op het moment van de aanvraag.
- **Verzegeling in Gemaskeerde Modus:** EvidenceRoot en NotarySeal berekening wordt gedaan met gemaskeerde forensische gegevens; dus verificatie blijft deterministisch.

### 🌍 Openbaar (Public)

- **Scenario:** Volledige transparantie. Volgens [PoArt] standaard wordt waar, wanneer, van welk netwerk het werk is gemaakt openbaar verklaard.

---

## 💡 Technologische Innovatie

PoArt is niet alleen een bestandsupload systeem. Het is een **"Forensische Toezichtketen" (Forensic Chain of Custody)** motor die drie verschillende technologische lagen in één pot smelten om een nieuwe standaard te brengen.

**De laag beschreven als "motor" in deze sectie komt overeen met de PoArt Forensic Engine (PFE) kern in eerdere terminologie.**

### 1) Client-Side Hashing (Maximale Privacy)

Uw kunstwerk bestanden worden nooit naar de server geüpload. Onze browser-gebaseerde (Client-side) motor berekent de hash van het bestand (digitale samenvatting) op uw eigen computer. Alleen deze vingerafdruk en metadata worden naar de server gestuurd.

> **Privacy Waarheid:** Werkbestand wordt niet naar de server geüpload en is dus veilig. Echter, forensische gegevens (IP/locatie) worden gedeeld volgens de geselecteerde zichtbaarheidsmodus (privé/gemaskeerd/openbaar).

### 2) Forensische Gegevensfusie (Wetenschappelijke Kracht)

Meer dan een eenvoudige tijdstempel. Het systeem verbindt deze gegevens in één "Genesis Zegel":

- **Digitale Samenvatting (SHA-512):** Digitale vingerafdruk met cryptografische samenvatting (SHA-512) standaard die breekt als zelfs één pixel van het werk verandert.
- **Locatie & Tijd:** Datum, land, stad en district gegevens met milliseconde precisie waarop de transactie plaatsvond.
- **Apparaat Identificatie:** Besturingssysteem, browser en apparaat type (User-Agent analyse).

---

## 🛡️ Gebruiksgebieden en Voordelen

Als je een kunstenaar, schrijver of ontwerper bent, is het niet genoeg om te zeggen "ik heb dit eerder gedaan", je moet het bewijzen.

**Een werk verzegeld met PoArt:**

- **Wiskundig Bewijs:** Als zelfs één pixel van je bestand verandert, weet het systeem het. Manipulatie is onmogelijk.
- **Juridische Basis:** Op welke datum, in welke stad, vanaf welk apparaat het werk werd verzegeld is geregistreerd.
- **Instant Certificaat:** Genereert in seconden een speciaal, QR-code en verzegeld **"Asset Identiteit Certificaat"** voor je.

---

## ⚙️ Systeemarchitectuur en Technische Kenmerken

Het systeem is ontworpen op een "Serverless" architectuur, gericht op hoge prestaties en schaalbaarheid.

| Laag | Technologie | Beschrijving |
|--------|-----------|----------|
| **Cryptografie** | SHA-256 & SHA-512 | Twee-laags cryptografische samenvatting |
| **Database** | Supabase (PostgreSQL) | JSONB gegevensstructuur, RLS beleid |
| **Forensische Gegevens** | ipapi.co API | IP/Locatie/Tijd driehoek |
| **Rendering** | html2canvas + jsPDF | Client-side PNG/PDF generatie |
| **Frontend** | Vanilla JavaScript | Nul framework afhankelijkheid |
| **Beveiliging** | Client-side hashing | Bestand gaat nooit naar server |

### Uitgelichte Kenmerken

| Kenmerk | Detail | Bij Concurrenten? |
|---------|-------|-------------|
| **Drag & Drop UI** | Bestand slepen-neerzetten, instant preview | ❌ Bij de meesten niet |
| **Multi-Format Export** | PNG, JSON, PDF - met één klik | ⚠️ Beperkt |
| **Real-Time Preview** | Live certificaat preview | ❌ Geen |
| **Privacy Controls** | Privé/Gemaskeerd/Openbaar opties | ❌ Geen |
| **Client-Side Hashing** | Bestand gaat nooit naar server | ✅ Alleen bij enkelen |
| **Forensische Metadata** | IP, locatie, apparaat, tijd - allemaal samen | ❌ Gefragmenteerd |
| **QR Verificatie** | Instant verificatie QR code | ⚠️ Beperkt |
| **Rate Limiting** | Spam bescherming (RLS + Client) | ❌ Bij de meesten niet |

---

## 🗺️ Roadmap: "Trustless" Toekomst

De huidige versie **(Beta v1.0)** is geoptimaliseerd om eindgebruikers maximale snelheid, eenvoudige interface en gratis toegang te bieden. Onze ultieme visie is echter om te transformeren naar een structuur waarin de database beheerder (wij) zelfs niet kan ingrijpen.

### Fase 1: Beta (Nu Live)

- **Infrastructuur:** Cloud Database (Supabase).
- **Doel:** Snelheid, UX (Gebruikerservaring) barrières elimineren en adoptie. "Wrijvingsloze" beveiliging bieden.

### 🚀 Fase 2: (Backend / Edge Function Vereisten)

Deze fase omvat de transitie van de volledig "Client-Side" werkende structuur naar een veiligere en beheerbare "Server-Side Authority" structuur.

| Item | Wat Levert Het Op? | Tech Stack | Prioriteit |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Function** | Spam preventie + API Key beveiliging | Supabase Edge (Deno) | 🔴 Hoog |
| **Wallet Handtekening** | Cryptografische authenticatie | Solana Wallet Adapter | 🟡 Gemiddeld |
| **IPFS/Arweave Backup** | Gedecentraliseerde onveranderlijkheid | IPFS SDK + Pinata | 🟢 Laag |
| **Intrekkingsmechanisme** | Vals certificaat intrekken | DB Schema Update | 🔴 Hoog |
| **Audit Log** | Forensisch onderzoek record | Custom logs tabel | 🟡 Gemiddeld |
| **OpenTimestamps** | Bitcoin verankering | OTS JavaScript | 🟢 Laag |
| **DID Integratie** | Gedecentraliseerde Identiteit | ION/Ceramic | 🟢 Laag |

### Fase 3: Volledige Decentralisatie (Lange Termijn)

| Functie | Doel | ETA |
|---------|------|-----|
| **Blockchain Register** | Ethereum/Solana on-chain registratie | Q4 2026 |
| **DAO Governance** | Gemeenschapsbestuur | Q1 2027 |
| **Multi-Chain Support** | Polygon, Arbitrum, Base | Q2 2027 |
| **Juridische Erkenning** | Geldigheid in Turkse rechtbanken | 2027-2028 |
| **API voor Ontwikkelaars** | Publiek API endpoint | Q3 2026 |

---

## 📊 Concurrent Analyse (Bijgewerkt)

PoArt is gepositioneerd op de "Sweet Spot" terwijl het de lacunes van huidige oplossingen opvult.

| Functie | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Kosten** | 🆓 Gratis | 🆓 | 💰 Betaald | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Zeer Eenvoudig | ❌ CLI | ⚠️ Gemiddeld | ⚠️ Gemiddeld | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Live | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Modi | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privacy | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensische Metadata** | ✅ Volledig | ❌ | ❌ | ⚠️ Beperkt | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verificatie** | ✅ Instant | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Nederlandse Ondersteuning** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Uitleg:**
- ✅ : Volledige ondersteuning / beschikbaar
- ⚠️ : Beperkt / in betaalde plannen
- ❌ : Geen / niet ondersteund
- 🔄 : In roadmap (in ontwikkeling)
- 🆓 : Volledig gratis
- 💰 : Betaald / abonnement vereist

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Cultuur > Kapitaal"*

## 🧾 Licentie

MIT Licentie © 2026 Ilhan Art Gallery Initiative

Zie [![Licentie](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) voor volledige voorwaarden.

---

## 💬 Credits

![Versie](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Beveiliging](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![Licentie](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Dit project is ontwikkeld door het [Ilhan Art Gallery] initiatief, en de broncode is publiekelijk beschikbaar voor transparantie.**

**PROTOCOL V1.0 // VERZEGELD MET SHA-512.**

*© 2026 İLHAN ART | ALLE RECHTEN VOORBEHOUDEN VOOR WERKEN, BEELDEN EN IDEEËN.*

---
