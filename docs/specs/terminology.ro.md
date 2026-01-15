# 📚 DICȚIONAR DE TERMINOLOGIE & CONCEPTE
> **"A înțelege limba acestui protocol înseamnă a-i înțelege viziunea."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Infrastructura de Bază

**PoArt Forensic Engine (PFE)** este stratul principal care reprezintă logica de bază și funcționarea tehnică din spatele protocolului [PoArt]. Acesta este "motorul forensic" care preia datele brute de producție ale operei de artă și le transformă în **dovezi digitale** verificabile și imuabile.

### 🧩 De ce "PoArt Forensic"?

- **PoArt (Proof of Art):** Focusul motorului este de a lega valoarea unui activ digital nu de speculație, ci de **procesul de producție verificabil**.
- **Forensic (Verificare Forensică):**
  - **Definiție Tehnică:** O abordare algoritmică și a lanțului de înregistrare orientată spre verificarea că datele procesului de producție (lovituri de pensulă, timelapse, log-uri) nu au fost manipulate.
  - **Strat Filozofic:** Împotriva producției de "output instant" a inteligenței artificiale; susținerea transformării producției **umane cu timp, efort și cost de decizie** într-o realitate măsurabilă.

> Notă: Integrarea blockchain (de ex. Solana) nu este nucleul PFE; este tratată ca un **Chain Anchor Layer** definit separat pentru verificare/registru.

### 🛠️ Acoperire Tehnică v1.0

**PoArt Forensic Engine (PFE) v1.0** este construit pe acești **3 piloni principali** în loc de modele financiare complexe:

1. **Hashing & Sealing (Sigilare):**  
   PFE procesează deterministă toate elementele din Evidence Pack (fișier operă, video, JSON/log, semnătură etc.) și generează valoarea unică **NotarySeal**.

   **Concepte de bază (v1.0):**
   - **FileHash (amprenta operei):** Hash generat din byte-ii fișierului operei.
   - **EvidenceRoot (rădăcina pachetului de dovezi):** Rezumat rădăcină reprezentând integritatea Evidence Pack (Merkle root sau hash manifest canonic).
   - **NotarySeal (sigiliu final / PFE Output):** Sigiliu final generat din combinația EvidenceRoot + timp + semnătură.

   **Formule (vizibile clar pentru investitori):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Definiții Canonical Payload (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Notă: Valoarea menționată ca output PFE este **NotarySeal**. Mecanismul **SignerSignature** va fi activat în Faza 2 (cu Solana Wallet Adapter); în v1.0 curent se folosește semnătura de atestare proprie a sistemului. Cheia publică de atestare este publicată în registru în câmpul `issuer.attestation_pubkey`.

2. **Indexing (Arhivare):**  
   Procesează ce portofel, la ce dată, pentru ce operă a prezentat **Labor Proof (Dovada Muncii)** într-un strat de înregistrare transparent și interogabil.  
   *(Acest strat poate fi o bază de date; integrarea în lanț este tratată separat ca "Chain Anchor Layer".)*

3. **Verification (Verificare):**  
   Când autenticitatea unei opere este pusă la îndoială, PFE reprocesează dovezile brute; testează cu certitudine matematică dacă valorile calculate **EvidenceRoot / NotarySeal** se potrivesc cu înregistrarea din arhivă.

---

### 🧮 Teorema Valorii PoArt (The Value Theorem)

Protocolul [PoArt] leagă valoarea unui activ digital ($V$) nu de percepția subiectivă a pieței, ci de **realitatea fizică a procesului de producție**.

Inteligența Artificială (AI) distruge procesul prin oferirea rezultatului instantaneu ($t \to 0$). [PoArt] tratează valoarea ca acumularea componentelor de **timp, muncă și voință**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definiția Variabilelor

- **$\int dt$ (Acumulare de Proces):**  
  Valoarea nu este un "output" instantaneu; este un **proces** care se acumulează între $t_{\text{start}}$ și $t_{\text{end}}$. Pe măsură ce durata scade (producție AI), rezultatul integralei tinde spre 0.

- **$P_{\text{labor}}(t)$ (Forță de Muncă Instantanee):**  
  Reprezintă intensitatea efortului mental și fizic cheltuit în momentul producției. Pe măsură ce efortul verificabil crește, integrandul crește.  
  > Notă: Acest termen poate fi normalizat în practică prin "semnale de muncă măsurabile/verificabile".

- **$I_{\text{agency}}(t)$ (Coeficient de Voință):**  
  Capacitatea producătorului de a lua riscuri și de a lua decizii. Ia o valoare între $0$ și $1$.
  - **AI ($I \approx 0$):** Execută comenzi, nu ia riscuri, nu plătește prețul.
  - **Om ($I \to 1$):** Schimbă decizii, ezită, ia riscuri.

- **$U_{\text{irreversible}}$ (Unicitate Ireversibilă):**  
  În timp ce anularea (`Ctrl+Z`) este posibilă în producția digitală; în producția fizică (vopsea aplicată pe pânză, marmură cioplită, gest în transmisie live) nu există întoarcere. Această **ireversibilitate** este un termen suplimentar care creează "unicitate" (caracter non-fungibil) în operă.

### 🔎 Studiu de Caz: AI "Output Instant" vs. Om "Proces Dovedit"

Următorul scenariu arată cum funcționează **Teorema Valorii PoArt** în practică și de ce producțiile AI au scor scăzut în standardul [PoArt].

#### Scenariul A: Producție Vizuală cu AI în 10 Secunde

- **Durată ($\Delta t$):** $10$ secunde (proces neglijabil)
- **Forță de Muncă ($P_{\text{labor}}$):** $1$ unitate (doar scrierea comenzii)
- **Coeficient de Voință ($I_{\text{agency}}$):** $0.01$ (fără risc, fără preț)
- **Ireversibilitate ($U_{\text{irreversible}}$):** $0$ (reversibil / copiabil)

**Rezultat:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Comentariu:** Chiar dacă output-ul este perfect; deoarece procesul nu a fost trăit și nu conține voință/risc, valoarea [PoArt] tinde spre $0$.

#### Scenariul B: Producție Fizică de 6 Ore în Transmisie Live

- **Durată ($\Delta t$):** $6$ ore ($21{,}600$ secunde)
- **Forță de Muncă ($P_{\text{labor}}$):** $0.5$ unități (continuitatea efortului fizic și mental)
- **Coeficient de Voință ($I_{\text{agency}}$):** $0.9$ (schimbarea deciziilor, asumarea riscurilor, alegeri ireversibile)
- **Ireversibilitate ($U_{\text{irreversible}}$):** $>0$ (urmele fizice nu pot fi anulate)

**Rezultat:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Comentariu:** Pe măsură ce procesul se prelungește și voința (riscul) crește, valoarea crește cumulativ. Termenul $U_{\text{irreversible}}$ este o contribuție suplimentară care creează "unicitate" (caracter non-fungibil) în operă.

---

### ✅ Concluzie: Valoarea Blocată cu Dovada (Proof-Bound Value)

Această teoremă desprinde afirmația de valoare a [PoArt] de un "like" sau "narațiune de piață" și o leagă de o **realitate de producție verificabilă**.

1. **Fără Proces Nu Există Valoare:**  
   AI distruge procesul în output-ul instantaneu ($t \to 0$). Pe măsură ce fereastra procesului se restrânge, rezultatul integralei scade printr-o necesitate matematică:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Voința și Riscul sunt Multiplicatori:**  
   [PoArt] măsoară nu doar "timpul cheltuit"; ci și stratul real de decizie, risc și preț în acel timp. Valoarea unei producții care nu își asumă riscuri (AI) este scăzută:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Unicitatea este Dovadă Fizică, Nu Marketing:**  
   Urmele ireversibile în producția fizică (lovitură de pânză, cioburi de marmură) sunt în afara logicii `Ctrl+Z` din digital. Această ireversibilitate ($U_{\text{irreversible}}$) face opera unică ontologic.

> **🔐 REZUMAT:** Deși teorema valorii pare nesigură ca măsurare (chiar dacă nu poate fi măsurată 100% în viața reală), scopul acestei formule este; să arate construcția și direcția variabilelor. Ceea ce este rar în epoca AI nu este "imaginea"; ci **munca verificabilă, timpul și voința.** [PoArt] măsoară această raritate și o înregistrează cu **Evidence Pack**.

### 🏛️ Importanța Conceptului de "Engine" (Motor)

Token-urile care provin din Pump.fun sau platforme similare sunt adesea doar **"bilete de acces"**. **PoArt Forensic Engine (PFE)** este în schimb **stratul de logică constituțională** care determină ce drepturi protejează acel bilet, cum va fi înregistrată munca și cum va fi perpetuată arta/știința/tehnologia.

> **Notă:** Motivul pentru care am lansat acest proiect pe Pump.fun este că nu aveam suficientă lichiditate și suficienți urmăritori. Folosirea datelor existente nu a fost cea mai înaltă calitate strategic, dar putem spune că a fost mișcarea corectă. Независent де буџет și средства, definirea logicii acestui motor pe GitHub dovedește că proiectul nu este doar o speculație financiară, ci o viziune de **infrastructură software** pe termen lung și **bibliotecă națională digitală**.

---

## 🎨 [PoArt] PROTOCOLUL DOVEZII MUNCII (Proof of Art Protocol v1.0)

> **"Artist Adevărat, Producție Adevărată, Valoare Adevărată."**

Acest protocol este dezvoltat ca un **mecanism de apărare biologic și intelectual** împotriva escroci anonimi care înconjoară ecosistemul cripto, elemente vizuale de inteligență artificială produse în 5 minute și cultura "Pump & Dump".

---

## a) Ce este [PoArt]? (Definiție Filosofică și Tehnică)

**Proof of Art [PoArt];** este un standard de verificare instituțională care garantează că valoarea din spatele unui activ pe blockchain nu se bazează pe speculație, ci pe **muncă umană** verificabilă, **timp** și **energie fizică**.

La fel cum Bitcoin creează valoare cu *"Electricitate și Putere de Procesor"* **(Proof of Work)**; proiectele conforme [PoArt] creează valoare cu *"Talent Artistic și Timp Uman"*.

Elimină riscul de *"Developer (Dev) a vândut, proiectul s-a terminat"* pe platformele Pump.fun și DEX; pentru că aici valoarea nu este în cod, ci în **continuitatea producției**.

> **[PoArt] nu spune participantului "Aveți încredere în noi"; spune "Iată dovezile, vezi cu ochii tăi, verifică cu matematica ta".**

---

## b) [PoArt] Standardul în 5 Puncte (The 5 Pillars of Truth)

Aceste 5 puncte sunt filtre nemanipulabile pe care un proiect trebuie să le treacă pentru a primi sigiliul [PoArt].

### 1) Dovada Identității Live (Live Identity Proof)

- **Problemă:** Lumea cripto este plină de fondatori anonimi (Dev-uri) cu identitate neclară care colectează bani și abandonează proiectul.
- **Soluția [PoArt]:** Producătorul dovedește nu doar un card de identitate, ci **prezența sa în momentul producției**. Aceasta nu include videoclipuri preînregistrate, ci sesiuni de transmisie live în care se interacționează cu comunitatea și se îndeplinesc cerințe specifice instantanee.  
  (Ex: *"Scrie data de astăzi și numărul blocului curent în colțul din dreapta al pânzei"*)
- **Motto:** *"Roboții pot picta, dar roboții nu transpiră și nu pot improviza."*

### 2) Dovada Muncii și Procesului (Labor & Process Proof)

- **Problemă:** Elemente vizuale AI (Inteligență Artificială) produse în 2 secunde și un tablou în ulei realizat în 2 luni primesc același tratament "jpeg" în lumea digitală.
- **Soluția [PoArt]:** Procesul de "sarcină și naștere" al operei este înregistrat. Etapele de schiță, straturile de vopsea, orele cumulative cheltuite și procesul fizic prin care a trecut artistul creând acea operă sunt documentate. Aceasta adaugă **"Cost de Timp" (Time Cost)** la token. Cu cât producția unui activ este mai dificilă, cu atât valoarea este mai solidă.

### 3) Dovada Valorii Estetice (Aesthetic Value Proof)

- **Problemă:** Cultura "Meme" care ignoră estetica și profunzimea artistică concentrându-se doar pe comedie instantanee, rezultând proiecte "Hype" de scurtă durată.
- **Soluția [PoArt]:** Proiectul trebuie să respecte standardele de artă academică, teoria culorilor, regulile de compoziție și cunoașterea materialelor (Impasto, Textură etc.). Conținutul nu trebuie doar să distreze; trebuie să trezească admirație în privitor și să aibă **valoare de colecție**.

### 4) Inovație Conceptuală (Conceptual Novelty)

- **Problemă:** Mii de monede câine/pisică care sunt copii unele ale altora, lipsite de creativitate.
- **Soluția [PoArt]:** Proiectul trebuie să construiască o nouă punte care combină arta, știința, filozofia sau tehnologia într-o structură semnificativă.  
  (Ex: Combinarea statuii clasice David cu datele pieței cripto; procesarea ideii de "pietrifcare" a percepției umane prin aceasta și fundamentarea ei cu surse științifice.)  
  Opera nu trebuie să fie doar o sărbătoare vizuală; ci și o provocare intelectuală care face să reflectezi asupra **Științei, Filozofiei sau Tehnologiei**.

> [!IMPORTANT]
> **Exemplu de Referință (Efectul Las Palmitas):**  
> În cartierul Las Palmitas din Mexic, care se luptă cu criminalitatea, peste 200 de case au fost transformate într-o sărbătoare gigantică de curcubeu. Ca urmare a acestei intervenții estetice, ratele criminalității din cartier au scăzut într-o anumită măsură, tinerii au început să se intereseze de artă în loc de bande. Schimbarea estetică a recodat respectul oamenilor față de mediul lor și unii față de alții (Social Cohesion).
>
> **Așteptare:** Un proiect care intră în lista [PoArt]; trebuie să conțină, ca în exemplul de mai sus, o relație sociologică, științifică sau filozofică cauză-efect care depășește estetica vizuală pură. Deoarece "Timpul" este singurul activ care nu poate fi cumpărat cu bani, în acest protocol timpul trebuie dovedit prin staking ca garanție. Baza intelectuală a proiectului trebuie să fie atât de puternică și universală încât; chiar și într-un posibil scenariu CTO (Community Take Over) ani mai târziu, comunitatea poate prelua această moștenire și continua potențialul inovator al proiectului în mod autonom.

### 5) Voință Non-Algoritmică (Non-Algorithmic Agency)

- **Problemă:** Producții digitale perfecte dar fără suflet, care se repetă.
- **Soluția [PoArt]:** Voința autentică a omului care poate face greșeli, își asumă riscuri și experimentează fluctuații emoționale trebuie să fie simțită în operă. Incertitudinea în loviturile de pensulă, reacțiile neașteptate ale materialului și deciziile instantanee ale artistului sunt **Semnătura Biologică** care diferențiază opera de "Producția Mașinii".

---

## c) Verificare & Mecanism Anti-Falsificare

Acest sistem asigură că proiectul rămâne de încredere și viu nu doar "la început" ci "pentru totdeauna".

### 📦 Pachetul de Dovezi (Evidence Pack - The Digital Twin)

În spatele fiecărei opere certificate [PoArt] se află un pachet de date criptat și marcat temporal pe care investitorii îl pot descărca:

- **Înregistrări Video RAW:** Imagini brute neîntrerupte ale momentului de producție.
- **Analiză Metadata:** Data creării fișierului, informații despre dispozitivul folosit și date de locație.
- **Referințe Fizice:** Dovezi că opera există în lumea fizică  
  (Ex: Ziar actual lângă operă sau date blockchain din acel moment).

> *Notă de consistență:* Expresia "pachet de dovezi" este conectată la linia **Evidence Pack → EvidenceRoot → NotarySeal** din secțiunile anterioare; adică integritatea pachetului este reprezentată de un sigiliu verificabil.

### 🔄 Reînnoire de 365 Zile (The Sustainability Protocol)

- **Caracteristică Revoluționară:** În proiectele cripto, "Dev" (Dezvoltatorul) lansează tokenul pe piață și de obicei dispare după 1-2 luni (Soft Rug). [PoArt] face acest lucru imposibil.
- **Regulă:** Statutul "Verified Artist" (Artist Verificat) nu este pe viață. Este valabil doar **1 an**.
- **Funcționare:** Artistul/Dezvoltatorul trebuie să prezinte comunității o **operă nouă, mare și verificabilă** la fiecare 365 de zile.
- **Scenar Exemplu:** Ați lansat proiectul în 2026. În ianuarie 2027, sistemul oferă avertismentul "Perioada de Dovadă Expirată". Dacă artistul nu prezintă o nouă expoziție, o nouă operă fizică sau o nouă integrare tehnologică, "Badge-ul de Încredere" al proiectului scade.
- **Rezultat:** Acest sistem asigură că **conținutul nu își pierde niciodată relevanța** și investitorul nu experimentează frica *"Dezvoltatorul mai este aici?"*. Proiectul devine un studio viu.

### 🚩 Protocolul Steagului Roșu (Red Flag Protocol)

**În caz de falsificare detectată de comunitate sau algoritmi (utilizare AI, operă furată, video manipulat):**

1. Certificatul este marcat imediat ca **"ANULAT" (VOID)**.
2. Pachetele de dovezi sunt etichetate public ca **"False"**.
3. Proiectul este adăugat pe lista neagră [PoArt]. Acest lucru consolidează faptul că **reputația este singura monedă** într-o lume descentralizată.

---

## d) Concluzie: Nu Cazinou, Ci Muzeu

**Pump.fun și Schimburile Descentralizate (DEX) sunt din păcate cazinouri în prezent; luminile clipesc, toată lumea urmărește profituri rapide și casa (escrocii) câștigă întotdeauna. Motivul pentru care am lansat proiectul aici este că nu aveam suficient buget și am putut ajunge la publicul existent prin transmisiuni live.**

**[PoArt] este o fortăreață construită în mijlocul acestui cazinou.**

- 🎰 Cazinourile se bazează pe jocuri de cărți; noi ne bazăm pe **realitate fizică**.
- 🃏 Cazinourile sunt deschise înșelăciunii; noi suntem deschisi **dovezilor transparente**.
- ⏳ Cazinourile sunt temporare; noi suntem concentrați pe **eternitatea artei și științei**.

**Tokenul care folosește acest protocol nu este doar o "monedă"; este o acțiune digitală cu sudoare, vopsea, cod și filozofie în spate.**

---

## 🗳️ 6) GUVERNARE ȘI REGISTRU PUBLIC (Governance & Public Registry)

**Scopul acestei secțiuni este: A scoate standardul [PoArt] din planul "încrederii în persoane" și a-l transforma într-o infrastructură publică durabilă cu înregistrare + verificare + supraveghere comunitară.**

### 6.1 Registru Public (Public Registry)

- **Public Registry:** Toate datele aprobate sunt înregistrate la `ilhanart.org/registry` (sau GitHub Registry).

**Logica de înregistrare (standard recomandat - format cale JSON):**

Fiecare înregistrare care intră în registru poartă minimum aceste câmpuri de bază verificabile:

- **Identitate & Statut:**
  - `certificate_id` (referință citibilă)
  - `status` (active / void)
  - `void_reason` (dacă este cazul)
  - `visibility` (private / masked / public)
  - `created_at` (timestamp)

- **Instituția Emitentă:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informații Operă:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (dacă este posibil; pentru identitatea deținătorului de token)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Date Forensice:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Dovezi Criptografice:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Guvernare:**
  - `governance.decision`
  - `governance.review_notes`

Registrul poate avea două straturi:
- **1)** Index citibil de om (listare web / căutare / filtrare)
- **2)** Manifest citibil de mașină (înregistrări JSON; pentru verificarea PFE)

**"Înregistrarea" aici devine verificabilă cu lanțul Evidence Pack → EvidenceRoot → NotarySeal al PFE. Registrul oferă un obiectiv de verificare, nu o "afirmație".**

---

### 6.2 Procesul de Aplicare PoArt Verified

**Aplicațiile PoArt Verified sunt evaluate de İlhanArt Gallery conform celor 5 standarde PoArt. Feedback-ul comunității este luat în considerare, dar decizia finală aparține echipei curatoriale. Deciziile sunt explicate transparent și înregistrate pe ilhanart.org/registry.**

#### Procesul de Aplicare

**Aplicare:**
- Artistul/proiectul face aplicația PoArt Verified
- Evidence Pack este pregătit (înregistrări video, metadata, linkuri de transmisiune live)
- Aplicația este trimisă la İlhanArt Gallery

**Examinare (30 Zile):**
- Echipa galeriei examinează detaliat Evidence Pack
- Toate cele 5 standarde PoArt sunt verificate:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Interviu cu artistul (opțional)

**Consultare Comunitară:**
- Evidence Pack este partajat public în timpul procesului de aplicare
- Comunitatea poate oferi feedback prin Discord și ilhanart.org/applications
- Token holder-ii (minimum 10.000 $CULTURE) pot face sugestii în mod special
- **Tot feedback-ul este luat în considerare în timpul procesului de examinare**
- **Dar decizia finală aparține evaluării curatoriale**

**Decizie:**
- Galeria aprobă sau respinge aplicația
- Motivarea deciziei este explicată transparent
- Dacă este aprobat → PoArt Verified badge
- Dacă este respins → Reaplicare posibilă după 6 luni

**Transparență:**
- Toate aplicațiile și deciziile sunt înregistrate pe ilhanart.org/registry
- Decision record este publicat public:
  - Data aplicării
  - Rezumatul procesului de examinare
  - Decizie (Approved / Rejected)
  - Motivarea deciziei (explicație scurtă)
  - Rezumatul feedback-ului comunității (anonim)

#### De ce Decizie Curatorială?

**Control de Calitate:**  
Statutul PoArt Verified este un badge cu standarde înalte. Evaluarea curatorială garantează menținerea acestor standarde.

**Prevenirea Manipulării Speculative:**  
Guvernarea completă on-chain (ex: Realms, DAO voting) nu este posibilă tehnic cu token-urile Pump.fun. Sistemele de voting off-chain sunt deschise manipulării whale și atacurilor coordonate. Decizia curatorială elimină acest risc.

**Eficiență Operațională:**  
În loc de mecanisme complexe de vot, proces de decizie rapid și clar. Artiștii primesc rezultat în 30 de zile.

**Participare Comunitară:**  
Feedback-ul comunității este luat complet în considerare și influențează procesul de decizie. Dar decizia finală aparține echipei curatoriale protejate împotriva manipulării.

**Viitor:**  
Când proiectul ajunge la maturitate (2027+), mecanismul de consultare a comunității poate fi întărit. Dar protecția standardului curatorial rămâne permanentă.

---

### 6.3 Utilitatea Token-ului (Token Utility)

**Beneficii oferite deținătorilor de token-uri $CULTURE:**

**1. Acces Prioritar la Evenimente de Galerie:**
- Deschideri de expoziții fizice İlhanArt Gallery
- Întâlniri cu artiști și vizite de atelier
- Vizualizări de colecții speciale

**2. Acces Complet la PoArt Registry:**
- Înregistrări detaliate ale tuturor operelor autentificate
- Versiuni complete ale Evidence Pack-urilor
- Instrumente de verificare forensică

**3. Prioritate Mint NFT:**
- Acces whitelist când operele PoArt Verified sunt mintate ca NFT
- Oportunități de mint timpurii
- NFT-uri de colecție speciale

**4. Vot Consultativ:**
- Drept de consultare în aplicațiile PoArt Verified
- Acces la canalele de feedback ale comunității
- Participare la discuții de guvernare

**5. Conținut Exclusiv:**
- Conținut behind-the-scenes din studio
- Interviuri cu artiști și videoclipuri de proces
- Acces la documentație tehnică

**Notă:**  
Token holder-ii dau vot consultativ (advisory vote). Decizia finală aparține echipei curatoriale. Această structură este preferată pentru a preveni manipularea whale și atacurile speculative. Nu există staking reward pentru că căutăm participanți culturali pe termen lung, nu capital mercenary pe termen scurt.

---

### 6.4 Sincronizare Metadata (Metadata Sync)

- **Metadata Sync:** Datele tehnice din registru trebuie să se potrivească 100% cu activul fizic.

**Definirea tehnică a "potrivirii 100%" (claritate recomandată):**

- **Potrivire minimă (obligatorie):**
  - `asset.fingerprints.sha256/sha512` din registru și hash-ul fișierului în mână trebuie să fie **exact aceleași**.
  - `proof.notary_seal` din registru când este reprodus (dacă Evidence Pack există) trebuie să fie **exact același**.

- **Potrivire referință fizică (tip de dovadă):**
  - Dovezi precum opera fizică + referință dată/bloc arătate în transmisiune live trebuie să fie consistente cu Evidence Pack.

- **Conformitate confidențialitate:**
  - Câmpurile precum IP/locație la vizibilitatea `masked` sunt publicate **conform standardului de mascare**.

---

### 6.5 Dispută, Examinare și Anulare (Dispute & Revocation)

Registrul nu este doar un mecanism de "aprobare"; ci un **mecanism de supraveghere viu împotriva falsificării**.

- Când este inițiată o dispută, înregistrarea poate fi pusă în modul **"review"**.
- Dacă este detectată falsificare, este marcată ca `status: void` și se adaugă motivul:
  - `void_reason` (utilizare AI / furt / manipulare etc.)
  - `revoked_at` (timpul anulării)
- Sursa deciziei de anulare este clar vizibilă în registru:
  - examinare curatorială / dispută comunitară / notă de analiză forensică (oricare se aplică)

> **Această secțiune este corespondența pe registru a conceptului VOID din secțiunea "Red Flag Protocol".**

---

### 6.6 Exemplu Înregistrare Registru (Citibil de Mașină)
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

> *Notă: `asset.fingerprints.sha512` și alte valori hash sunt scurtate în scopuri de afișare; în aplicația reală se folosește un șir de caractere hexazecimale de lungime completă.*

---

## 7) 🔐 SIGILIU TEHNIC (NOTARY SEAL)

**Algoritm de sigiliu indestructibil produs de PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Protocol Notar Digital & Dovadă Forensică (Beta v1.0)

> **"Cultura este mai mare decât capitalul. Protejează-ți operele de astăzi, poartă-le spre mâine."**

---

## De ce Public?

Adevărata securitate vine din transparență. Datorită sistemului nostru **Public Registry (Registru Public)**, cineva oriunde în lume; poate verifica în câteva secunde dacă fișierul în mână este original, fără nevoie de o autoritate.

---

## 🧩 De ce Există Mai Multe "Module de Vizibilitate"?

Aceasta este partea cea mai critică a codului (meniul de selectare a vizibilității). Aceste opțiuni permit utilizatorilor să stabilească echilibrul **"Confidențialitate vs. Transparență"**:

### 🔒 Privat (Private)

- **Scenariu:** Artistul nu vrea încă să publice opera dar vrea să pună un timestamp și să dovedească "am făcut asta la această dată".
- **Ce Face Codul:** Scrie datele în baza de date dar pune eticheta `visibility: "private"`. Mai târziu când scrii politica "Public Read" poți ascunde aceste înregistrări de public spunând `WHERE visibility = 'public'`.

### 🕶️ Mascat (Masked)

- **Scenariu:** Artistul vrea transparență dar se teme că adresa casei (locația IP) va fi găsită.
- **Ce Face Codul:** Funcțiile `maskIP` și `maskLoc` funcționează pe partea JavaScript. Convertește adresa IP în forma `88.241.***.***`, locația în forma `***/TR` și trimite versiunea cenzurată în baza de date.
- **Notă Confidențialitate:** Mascarea se face în browser, Supabase nu vede locația reală. **Dar:** Dacă datele de locație sunt folosite prin API-uri terțe precum ipapi.co, acești furnizori văd adresa IP în momentul cererii.
- **Sigilare în Modul Mascat:** Calculul EvidenceRoot și NotarySeal se face cu datele forensice mascate; astfel verificarea rămâne deterministă.

### 🌍 Public (Public)

- **Scenariu:** Transparență completă. Conform standardului [PoArt], se declară clar unde, când, din ce rețea a fost produsă opera.

---

## 💡 Inovație Tehnologică

PoArt nu este doar un sistem de încărcare fișiere. Este un motor **"Lanț Forensic de Custodie" (Forensic Chain of Custody)** care topește trei straturi tehnologice diferite într-o oală și aduce un nou standard.

**Stratul explicat ca "motor" în această secțiune corespunde nucleului PoArt Forensic Engine (PFE) în terminologia anterioară.**

### 1) Client-Side Hashing (Confidențialitate Maximă)

Fișierele operelor dvs. nu sunt niciodată încărcate pe server. Motorul nostru care funcționează pe bază de browser (Client-side) calculează hash-ul fișierului (rezumatul digital) pe propriul dvs. calculator. Doar această amprentă și metadatele sunt trimise pe server.

> **Notă Confidențialitate:** Fișierul operei nu este încărcat pe server și este astfel protejat. Dar datele forensice (IP/locație) sunt partajate conform modului de vizibilitate selectat (private/masked/public).

### 2) Forensic Data Fusion (Putere Forensică)

Este mult mai mult decât un simplu timestamp. Sistemul combină următoarele date într-un singur "Sigiliu Genesis":

- **Rezumat Digital (SHA-512):** Amprentă digitală care se va deteriora chiar dacă un singur pixel al operei se schimbă, folosind standardul de rezumat criptografic (SHA-512).
- **Locație & Timp:** Dată cu precizie de milisecundă, țară, oraș și date de district unde a avut loc tranzacția.
- **Identitate Dispozitiv:** Sistem de operare, browser și tip de dispozitiv (analiză User-Agent).

---

## 🛡️ Domenii de Utilizare și Beneficii

Dacă sunteți artist, scriitor sau designer, nu este suficient să spuneți "Am făcut asta mai devreme", trebuie să o dovediți.

**O operă sigilată cu PoArt:**

- **Dovadă Matematică:** Dacă chiar un singur pixel al fișierului dvs. se schimbă, sistemul o observă. Manipularea este imposibilă.
- **Bază Juridică:** Este înregistrat la ce dată, în ce oraș, de pe ce dispozitiv a fost sigilată opera.
- **Certificat Instant:** Generează în câteva secunde un **"Certificat de Identitate Activ"** personalizat, cu cod QR și sigilat pentru dvs.

---

## ⚙️ Arhitectură Sistem și Specificații Tehnice

Sistemul este proiectat pe o arhitectură "Serverless" (Fără Server), concentrat pe performanță înaltă și scalabilitate.

| Strat | Tehnologie | Descriere |
|--------|-----------|----------|
| **Criptografie** | SHA-256 & SHA-512 | Rezumat criptografic dublu strat |
| **Bază de Date** | Supabase (PostgreSQL) | Structură de date JSONB, politici RLS |
| **Date Forensice** | ipapi.co API | Triplet IP/Locație/Timp |
| **Rendering** | html2canvas + jsPDF | Generare PNG/PDF client-side |
| **Frontend** | Vanilla JavaScript | Zero dependență framework |
| **Securitate** | Client-side hashing | Fișierul nu merge niciodată pe server |

### Caracteristici Excelente

| Caracteristică | Detaliu | La Concurenți? |
|---------|-------|-------------|
| **Drag & Drop UI** | Tragere-plasare fișier, previzualizare instantanee | ❌ Lipsește la majoritatea |
| **Multi-Format Export** | PNG, JSON, PDF - cu un clic | ⚠️ Limitat |
| **Real-Time Preview** | Previzualizare certificat live | ❌ Nu |
| **Privacy Controls** | Opțiuni Private/Masked/Public | ❌ Nu |
| **Client-Side Hashing** | Fișierul nu merge niciodată pe server | ✅ Doar la câțiva |
| **Forensic Metadata** | IP, locație, dispozitiv, timp - toate împreună | ❌ Fragmentat |
| **QR Verification** | Cod QR verificare instantanee | ⚠️ Limitat |
| **Rate Limiting** | Protecție spam (RLS + Client) | ❌ Lipsește la majoritatea |

---

## 🗺️ Foaie de Parcurs: Viitor "Trustless"

Versiunea curentă **(Beta v1.0)** este optimizată pentru a oferi utilizatorului final viteză maximă, interfață ușoară și acces gratuit. Dar viziunea noastră finală este să trecem la o structură în care nici măcar administratorul bazei de date (noi) nu poate interveni.

### Faza 1: Beta v1.0 (Acum Live)

**Infrastructură:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + IPFS backup)
- Gallery self-attestation (centralizat dar transparent)

**Token:**
- Platformă: Pump.fun
- Lichiditate: Raydium (automat)
- Guvernare: Advisory only (consultare comunitate)

**Scop:**
- Viteză, eliminarea barierelor UX
- Oferirea securității "fără fricțiune"
- Construirea comunității

**Token Utility (v1.0):**
- Acces prioritar evenimente galerie
- Vizualizare PoArt Registry
- Drept de vot consultativ

---

### 🚀 Faza 2: Autoritate Descentralizată (2026 Q2-Q4)

Această fază acoperă tranziția sistemului de la structura care funcționează complet "Client-Side" la o structură mai sigură și descentralizată.

| Caracteristică | Ce Aduce? | Tech Stack | ETA |
|---------|---------------|------------|-----|
| **Edge Function INSERT** | Blocare spam + securitate API Key | Supabase Edge (Deno) | Q2 2026 |
| **Semnătură Portofel** | Decentralized identity | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | Arhivă descentralizată | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | Anulare certificat fals | DB Schema Update | Q2 2026 |
| **Audit Log** | Înregistrare interogare forensică | Tabel logs personalizat | Q3 2026 |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain voting (Discord/web) + wallet signature
- Selectare reprezentanți comunitate (primele 90 zile)
- Control portofel operațiuni multi-sig
- Weighted advisory voting (cu whale cap)

**Imuabilitate:**
- Backup registru cu hash-uri IPFS
- Bitcoin timestamp anchoring
- Pregătire verificare cross-chain

---

### Faza 3: Descentralizare Completă (2027+)

| Caracteristică | Obiectiv | ETA |
|---------|-------|-----|
| **On-Chain Registry** | Înregistrare on-chain Solana | Q1 2027 |
| **Enhanced Token Utility** | NFT mint, caracteristici avansate | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **DID Integration** | Decentralized Identity | Q3 2027 |
| **Community Governance** | Sistem advisory întărit | Q4 2027 |
| **Legal Recognition** | Validitate în instanțele românești | 2027-2028 |
| **API for Developers** | Endpoint API public | Q3 2027 |

**Evoluție Guvernare:**
- v3.0: Model hibrid (curatorial + community weighted)
- 2028+: Full community governance (opțional)
- Controlul calității curatorial rămâne întotdeauna păstrat

---

## 🧬 Structură Date Protocol (JSON Schema)

**Fiecare certificat [PoArt] are un card de identitate JSON portabil și verificabil produs în standardul de mai jos.**

> **Notă:** Acest format Identity JSON este formatul de certificat prezentat utilizatorului. În înregistrările registry se folosește `registry.asset` în loc de `identity.asset_data` (mapping: `identity.asset_data` == `registry.asset`).
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

## 🔬 Profunzime Tehnică: Algoritm Sigiliu

### Funcții Hash Deterministă
```javascript
// Funcții ajutătoare: Convertire digest în hex string
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Convertire string în byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Producție string forensics canonic (v1.0: ordine câmp fix + UTF-8 + \n delimiter)
// Notă Faza 2: Tranziție la JSON canonic cu RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Proces Producție NotarySeal (Complet Deterministă)
```javascript
// 1. Calcul FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Colectare date forensice (utilizare timestamp unic)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Producție timestamp unic
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Același timestamp
  };
  
  return { forensics, timestamp };
}

// 3. Creare EvidenceRoot (cu encoding canonic)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Producție NotarySeal (utilizare același timestamp)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Funcții ajutătoare mascare (suport IPv4 și IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Verificare IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 sau format necunoscut
  return "***";
}
```

### Flux Verificare (Două Niveluri)

#### Quick Verify (Verificare Rapidă)
```javascript
// Verifică doar hash fișier (steag roșu rapid)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Extrage din Registry
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Comparație hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Original - Hash fișier se potrivește"
    };
  } else {
    return {
      valid: false,
      message: "❌ Fals - Fișier manipulat"
    };
  }
}
```

#### Full Verify (Verificare Completă)
```javascript
// Regenerează și verifică EvidenceRoot și NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Extrage din Registry
  const cert = await fetchFromRegistry(certificateId);

  // 1) Verificare FileHash (steag roșu rapid)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Fals - Hash fișier nu se potrivește" };
  }

  // 2) Regenerare EvidenceRoot (cu forensics salvat în registry)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Nu se potrivește - EvidenceRoot nu se verifică" };
  }

  // 3) Regenerare NotarySeal (cu același timestamp + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Nu se potrivește - NotarySeal nu se verifică" };
  }

  // Opțional: În Faza 2 verifică și signer_sig cu attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Semnătură invalidă" };

  return { valid: true, message: "✅ Original - Full Verify reușit" };
}
```

> **Note Importante:**
> - **Quick Verify:** Verifică doar hash-ul fișierului pentru utilizare rapidă.
> - **Full Verify:** Verifică toate straturile protocolului (EvidenceRoot + NotarySeal).
> - Toate operațiile hash sunt efectuate determinist, cu encoding fix și delimitatori.
> - **Standard canonicalizare v1.0:** Ordine câmp fix + UTF-8 encoding + `\n` delimiter.
> - **Plan Faza 2:** Tranziție la JSON canonic cu RFC 8785 (JCS - JSON Canonicalization Scheme).
> - În modul mascat, calculul EvidenceRoot și NotarySeal se face cu forensics mascat.
> - Timestamp unic este folosit în tot procesul (forensics + NotarySeal); determinismul este garantat.
> - **Nume câmpuri forensics:** `ip_masked`, `location`, `device`, `timestamp` (cod și registry complet compatibile).
> - **Cale registry:** `certificate.asset.fingerprints` (complet compatibil cu codul verify).
> - **Registry signer_sig:** Câmpul `proof.signer_sig` este necesar pentru Full Verify.
> - Mecanismul SignerSignature va fi activat în Faza 2 cu Solana Wallet Adapter; în v1.0 poate fi efectuată verificare cu `attestation_pubkey`.

---

## 📊 Analiză Concurenți (Actualizat)

PoArt este poziționat pe "Sweet Spot" (Punctul cel mai ideal) care completează deficiențele soluțiilor existente.

| Caracteristică | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Cost** | 🆓 Gratuit | 🆓 | 💰 Plătit | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Foarte Ușor | ❌ CLI | ⚠️ Mediu | ⚠️ Mediu | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Live | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Moduri | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Confidențialitate | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Complet | ❌ | ❌ | ⚠️ Limitat | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Instant | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Suport Română** | ✅ Nativ | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Explicație:**
- ✅ : Suport complet / prezent
- ⚠️ : Limitat / în planuri plătite
- ❌ : Nu / nesuportat
- 🔄 : În Roadmap (în dezvoltare)
- 🆓 : Complet gratuit
- 💰 : Plătit / abonament necesar

### Deficiențe Concurenți, Puncte Forte PoArt

| Deficiență | Concurenți | PoArt |
|------|----------|-------|
| **Dificultate Utilizare** | CLI, cunoștințe API, portofel necesar | Tragere-plasare, gata în 3 clicuri |
| **Barieră Cost** | Abonament $50-500/lună | 100% gratuit |
| **Confidențialitate** | Fișier încărcat pe server | Client-side, fișierul nu pleacă niciodată |
| **Date Forensice** | Doar timestamp | IP, locație, dispozitiv, timp - toate |
| **Suport Română** | Nu sau foarte limitat | Suport nativ limbă |
| **Open Source** | Cutie închisă | Tot codul deschis pe GitHub |

---

## 📈 Statistici Utilizare (Obiective 2026 Q1)

| Metrică | Obiectiv | Status |
|--------|-------|-------|
| **Total Certificate** | 1.000 | 🔄 În progres |
| **Utilizatori Activi** | 500 | 🔄 În progres |
| **Număr Verificări** | 5.000 | 🔄 În progres |
| **Uptime** | 99,9% | ✅ Activ |
| **Timp Răspuns Mediu** | <200ms | ✅ Optim |

---

## 🌍 Comunitate & Suport

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Contributori

Protocolul PoArt continuă să se dezvolte cu contribuțiile comunității open source.

**Pentru a contribui:**
1. Faceți Fork
2. Creați feature branch (`git checkout -b feature/amazing-feature`)
3. Faceți Commit (`git commit -m 'Add amazing feature'`)
4. Faceți Push (`git push origin feature/amazing-feature`)
5. Deschideți Pull Request

### 🛠️ La Ce Avem Nevoie Acum? (Apel Ajutor)

Pentru dezvoltările **Faza 2** ale Protocolului PoArt așteptăm contribuții de la dezvoltatori experimentați în următoarele subiecte:

* **Supabase Edge Functions:** Mutarea protecției spam pe server-side.
* **Solana Web3.js:** Integrare semnătură portofel (Wallet Signing).
* **IPFS / Arweave:** Integrare servicii arhivare și pinning.
* **Community Tools:** Bot Discord, sisteme de votare, dashboard analytics.

> Vă rugăm să inițiați o discuție în tab-ul "Issues" înainte de a adăuga o caracteristică.

---

## 💬 Note Finale

### Pump.fun și Realitate

Acest proiect a fost lansat pe Pump.fun pentru că:
- ✅ Acces lichiditate (Raydium automatic migration)
- ✅ Acces comunitate existentă
- ✅ Cost de pornire redus

Dar să clarificăm acest lucru:
- **Prețul token-ului** nu este un indicator al succesului artistic
- Valoarea token-ului este importantă pentru **bugetul operațional** (galerie, expoziții, infrastructură)
- **Indicatori de succes:** Opere autentificate + angajament comunitate + vizitatori fizici

### Guvernare și Descentralizare

**Realitate v1.0 (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (centralizat dar transparent)
- Governance: Advisory only (decizie finală curatorială)
- Token utility: Acces galerie + registry + prioritate NFT

**Viziune v2.0+ (2027+):**
- Registry: On-chain (Solana)
- Signatures: Bazate pe portofel (descentralizat)
- Governance: Hibrid (consultare comunitate + calitate curatorială)
- Token utility: Caracteristici îmbunătățite + acces avansat

Această structură oferă **eficiență operațională** și **control calitate** în fază timpurie, menținând deschisă calea pentru creșterea **participării comunității** în viitor.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Cultura Este Mai Mare Decât Capitalul*

## 🧾 Licență

MIT License © 2026 İlhan Art Gallery Initiative

Vezi [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) pentru termeni completi.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Acest proiect este dezvoltat cu inițiativa [İlhan Art Gallery] și codul sursă este public accesibil în scopuri de transparență.**

**PROTOCOL V1.0 // SIGILAT CU SHA-512.**

*© 2026 İLHAN ART | TOATE DREPTURILE ASUPRA OPERELOR, ELEMENTELOR VIZUALE ȘI IDEILOR REZERVATE.*

---
