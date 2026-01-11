# 📚 GLOSAR DE TERMINOLOGIE ȘI CONCEPTE
> **"A înțelege limbajul acestui protocol înseamnă a-i înțelege viziunea."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Infrastructura de Bază

**PoArt Forensic Engine (PFE)** este stratul de bază care reprezintă logica fundamentală și funcționarea tehnică din spatele protocolului [PoArt]. Este "motorul criminalistic" care transformă datele brute de producție ale unei opere de artă într-o **dovadă digitală** verificabilă și imuabilă.

### 🧩 De Ce "PoArt Forensic"?

- **PoArt (Proof of Art):** Focusul motorului este legarea valorii unui activ digital nu de speculație, ci de **procesul de producție verificat**.
- **Forensic (Verificare Criminalistică):**
  - **Definiție Tehnică:** Abordarea algoritmică și lanțul de dovezi pentru verificarea faptului că datele procesului de producție (lovituri de pensulă, timelapse, loguri) nu au fost manipulate.
  - **Nivel Filozofic:** Împotriva "producției instantanee" a inteligenței artificiale; afirmația transformării producției umane care conține **timp, efort și cost al deciziilor** într-o realitate măsurabilă.

> Notă: Integrarea blockchain (de ex., Solana) nu este nucleul PFE; va fi definită separat ca **Chain Anchor Layer** pentru verificare/registru.

### 🛠️ Domeniu Tehnic v1.0

**PoArt Forensic Engine (PFE) v1.0** este construit pe **3 piloni de bază** în loc de modele financiare complexe:

1. **Hashing & Sealing (Sigilare):**  
   PFE procesează în mod determinist toate elementele din Evidence Pack (fișier operă, video, JSON/log, semnătură etc.) și generează o valoare unică **NotarySeal**.

   **Concepte cheie (v1.0):**
   - **FileHash (amprenta operei):** Hash-ul generat din octeții fișierului operei.
   - **EvidenceRoot (rădăcina pachetului de dovezi):** Digestul rădăcină care reprezintă integritatea Evidence Pack (rădăcină Merkle sau hash al manifestului canonic).
   - **NotarySeal (sigiliul final / ieșirea PFE):** Sigiliul final generat din combinația EvidenceRoot + timp + semnătură.

   **Formule (în format inteligibil pentru investitori):**
   
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
   
   > Notă: Valoarea considerată ca ieșire PFE este **NotarySeal**. Mecanismul **SignerSignature** va fi activat în Faza 2 (cu Solana Wallet Adapter); în v1.0 curentă se folosește semnătura proprie de atestare a sistemului. Cheia publică de atestare este publicată în registru în câmpul `issuer.attestation_pubkey`.

2. **Indexing (Arhivare):**  
   Înregistrează ce portofel, la ce dată, a prezentat **Labor Proof (Dovada Muncii)** pentru ce operă; într-un strat de registru transparent și interogabil.  
   *(Acest strat poate fi o bază de date; integrarea blockchain este definită separat ca "Chain Anchor Layer".)*

3. **Verification (Verificare):**  
   Când originalitatea unei opere este pusă la îndoială, PFE reprocesează dovezile brute; testează cu certitudine matematică dacă valorile calculate **EvidenceRoot / NotarySeal** corespund înregistrărilor din arhivă.

---

### 🧮 Teorema Valorii PoArt (The Value Theorem)

Protocolul [PoArt] leagă valoarea ($V$) unui activ digital nu de percepția subiectivă a pieței, ci de **realitatea fizică a procesului de producție**.

Inteligența Artificială (AI) anulează procesul oferind rezultate instantanee ($t \to 0$). [PoArt] consideră în schimb valoarea ca acumulare a componentelor **timp, muncă și voință**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definiția Variabilelor

- **$\int dt$ (Acumularea Procesului):**  
  Valoarea nu este o "ieșire" instantanee; este un **proces** care se acumulează între $t_{\text{start}}$ și $t_{\text{end}}$. Pe măsură ce timpul scade (producție AI), rezultatul integralei se apropie de 0.

- **$P_{\text{labor}}(t)$ (Intensitatea Instantanee a Muncii):**  
  Reprezintă intensitatea efortului mental și fizic cheltuit în momentul producției. Pe măsură ce efortul verificat crește, integrandul crește.  
  > Notă: Acest termen poate fi normalizat în practică la "semnale de muncă măsurabile/verificabile".

- **$I_{\text{agency}}(t)$ (Coeficientul de Voință):**  
  Aceasta este capacitatea producătorului de a-și asuma riscuri și de a lua decizii. Ia valori între $0$ și $1$.
  - **AI ($I \approx 0$):** Execută comenzi, nu își asumă riscuri, nu plătește costuri.
  - **Om ($I \to 1$):** Schimbă decizii, ezită, își asumă riscuri.

- **$U_{\text{irreversible}}$ (Unicitate Ireversibilă):**  
  În timp ce în producția digitală poți anula (`Ctrl+Z`); în producția fizică (vopsea aplicată pe pânză, marmură cioplită, gest în timpul unui live) nu există întoarcere. Această **ireversibilitate** este un termen suplimentar care creează "unicitatea" (caracterul non-fungibil) în operă.

### 🔎 Analiză de Caz: AI "Ieșire Instantanee" vs Om "Proces Dovedit"

Următorul scenariu arată cum funcționează **Teorema Valorii PoArt** în practică și de ce producțiile AI primesc scoruri scăzute în standardul [PoArt].

#### Scenariu A: Producție Vizuală cu AI în 10 Secunde

- **Durată ($\Delta t$):** $10$ secunde (proces practic inexistent)
- **Intensitate Muncă ($P_{\text{labor}}$):** $1$ unitate (doar scrierea comenzii)
- **Coeficient Voință ($I_{\text{agency}}$):** $0.01$ (fără risc, fără cost)
- **Ireversibilitate ($U_{\text{irreversible}}$):** $0$ (reversibil / copiabil)

**Rezultat:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Comentariu:** Chiar dacă ieșirea este perfectă; deoarece procesul nu a fost trăit și nu conține voință/risc, valoarea [PoArt] se apropie de $0$.

#### Scenariu B: Producție Fizică în Direct Timp de 6 Ore

- **Durată ($\Delta t$):** $6$ ore ($21{,}600$ secunde)
- **Intensitate Muncă ($P_{\text{labor}}$):** $0.5$ unități (continuitate efort fizic și mental)
- **Coeficient Voință ($I_{\text{agency}}$):** $0.9$ (schimbarea deciziilor, asumarea riscurilor, alegeri ireversibile)
- **Ireversibilitate ($U_{\text{irreversible}}$):** $>0$ (urmele fizice nu pot fi anulate)

**Rezultat:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Comentariu:** Pe măsură ce procesul se prelungește și voința (riscul) crește, valoarea se acumulează cumulativ. Termenul $U_{\text{irreversible}}$ este o contribuție suplimentară care creează "unicitatea" (caracterul non-fungibil) în operă.

---

### ✅ Concluzie: Valoare Legată de Dovadă (Proof-Bound Value)

Această teoremă îndepărtează afirmația de valoare [PoArt] de la a fi un "like" sau o "narațiune de piață" și o leagă de **realitatea verificată a producției**.

1. **Fără Proces Nu Se Creează Valoare:**  
   AI anulează procesul în ieșirea instantanee ($t \to 0$). Pe măsură ce fereastra procesului se îngustează, rezultatul integralei scade din necesitate matematică:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Voința și Riscul Sunt Multiplicatori:**  
   [PoArt] măsoară nu doar "timpul cheltuit", ci și nivelul real de decizie, risc și cost în acel timp. Valoarea unei producții fără asumarea riscurilor (AI) este scăzută:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Unicitatea Este Dovadă Fizică, Nu Marketing:**  
   În producția fizică, urmele ireversibile (lovitura de pensulă pe pânză, marmura spartă) sunt în afara logicii `Ctrl+Z` digitale. Această ireversibilitate ($U_{\text{irreversible}}$) face opera unic ontologic.

> **🔐 REZUMAT:** Deși teorema valorii poate părea nedefinită ca măsurare (chiar dacă nu poate fi măsurată 100% în viața reală), scopul acestei formule este de a arăta structura și direcția variabilelor. Ceea ce este rar în era AI nu este "imaginea", ci **munca verificată, timpul și voința.** [PoArt] măsoară această raritate și o înregistrează prin **Evidence Pack**.

### 🏛️ Semnificația Conceptului de "Engine" (Motor)

Token-urile care apar pe platforme precum Pump.fun sunt adesea doar **"bilete de acces"**. **PoArt Forensic Engine (PFE)** este în schimb un **strat logic constituțional** care definește ce drepturi protejează acest bilet, cum este înregistrată munca și cum arta/știința/tehnologia devin permanente.

> **Notă:** Motivul pentru care am lansat acest proiect pe Pumpfun este că nu aveam suficientă lichiditate și urmăritori. Utilizarea datelor existente a fost un pas strategic corect, deși nu cel mai calitativ. Definirea logicii acestui motor pe GitHub, independent de buget și resurse, dovedește că proiectul nu este doar speculație financiară, ci o viziune pe termen lung de **infrastructură software** și **bibliotecă națională digitală**.

---

## 🎨 PROTOCOLUL [PoArt] PROOF OF ART (Proof of Art Protocol v1.0)

> **"Artist Adevărat, Producție Adevărată, Valoare Adevărată."**

Acest protocol este un **mecanism de apărare biologică și intelectuală** conceput împotriva escrocilor anonimi care au inundat ecosistemul cripto, imaginilor AI produse în 5 minute și culturii "Pump & Dump".

---

## a) Ce Este [PoArt]? (Definiție Filozofică și Tehnică)

**Proof of Art [PoArt];** este un standard instituțional de verificare care garantează că valoarea din spatele unui activ pe blockchain se bazează nu pe speculație, ci pe **munca umană**, **timpul** și **energia fizică** verificate.

La fel cum Bitcoin produce valoare prin *"Electricitate și Putere de Calcul"* **(Proof of Work)**; proiectele compatibile cu [PoArt] produc valoare prin *"Abilitate Artistică și Timp Uman"*.

Elimină riscul *"Dev a vândut, proiectul s-a terminat"*, prezent pe Pump.fun și platformele DEX; pentru că aici valoarea nu este în cod, ci în **continuitatea producției**.

> **[PoArt] nu spune participantului "Ai încredere în noi"; spune "Iată dovezile, vezi cu ochii tăi, verifică cu matematica ta".**

---

## b) Standardul [PoArt] cu 5 Piloni (The 5 Pillars of Truth)

Acești 5 puncte sunt filtre nemanipulabile pe care un proiect trebuie să le treacă pentru a obține sigiliul [PoArt].

### 1) Dovada Identității Live (Live Identity Proof)

- **Problema:** Lumea cripto este plină de fondatori anonimi (Dev) cu identitate nedefinită care adună bani și abandonează proiectul.
- **Soluția [PoArt]:** Producătorul dovedește nu doar identitatea, ci **prezența sa în timpul producției**. Aceasta include sesiuni live unde interacționează cu comunitatea și îndeplinesc cerințe specifice instantanee, nu cu videoclipuri preînregistrate.  
  (De exemplu: *"Scrie data de astăzi și numărul curent al blocului în colțul din dreapta al pânzei"*)
- **Motto:** *"Roboții pot desena, dar roboții nu transpiră și nu improvizează."*

### 2) Dovada Muncii și Procesului (Labor & Process Proof)

- **Problema:** Imaginile AI produse în 2 secunde și picturile în ulei realizate în 2 luni sunt considerate același "jpeg" în lumea digitală.
- **Soluția [PoArt]:** Procesul de "sarcină și naștere" al operei este înregistrat. Etapele schiței, straturile de vopsea, orele acumulate cheltuite și procesul fizic trăit de artist în timpul creării operei sunt documentate. Aceasta adaugă **"Cost de Timp" (Time Cost)** la token. Cu cât este mai dificil de produs activul, cu atât valoarea sa este mai solidă.

### 3) Dovada Valorii Estetice (Aesthetic Value Proof)

- **Problema:** Estetica și profunzimea artistică a culturii "Meme" care ignoră totul și se concentrează doar pe comedie instantanee, și proiectele "Hype" pe termen scurt care rezultă din aceasta.
- **Soluția [PoArt]:** Proiectul trebuie să aibă standarde artistice academice, teorie a culorilor, reguli de compoziție și cunoașterea materialelor (Impasto, Textură etc.). Conținutul nu trebuie doar să facă râs; trebuie să trezească admirație în privitor și să aibă **valoare de colecție**.

### 4) Inovație Conceptuală (Conceptual Novelty)

- **Problema:** Mii de dog/cat coin identice, departe de creativitate.
- **Soluția [PoArt]:** Proiectul trebuie să construiască o nouă punte care combină semnificativ arta, știința, filozofia sau tehnologia.  
  (De exemplu: Combinarea statuii clasice a lui David cu datele pieței cripto; elaborarea prin aceasta a ideii de "pietrificare" a percepției umane și posibilitatea justificării cu surse științifice.)  
  Opera trebuie să fie nu doar o sărbătoare vizuală, ci și o provocare intelectuală care stimulează gândirea despre **Știință, Filozofie sau Tehnologie**.

> [!IMPORTANT]
> **Exemplu de Referință (Efectul Las Palmitas):** În districtul Las Palmitas din Mexic, care se luptă cu criminalitatea, peste 200 de case au fost transformate într-o >sărbătoare uriașă curcubeu. Ca rezultat al acestei intervenții estetice, ratele criminalității din district au scăzut într-o anumită măsură, tinerii au început să se >intereseze de artă în locul bandelor. Schimbarea estetică a recodat respectul oamenilor față de mediu și unul față de celălalt (Coeziune Socială).
>
> **Așteptare:** Un proiect care intră în lista [PoArt]; la fel ca în exemplul de mai sus, trebuie să conțină o legătură cauzală sociologică, științifică sau filozofică >dincolo de estetica vizuală. Deoarece singurul lucru care nu poate fi cumpărat cu bani este "Timpul", în acest protocol timpul trebuie dovedit ca garanție prin staking. >Fundamentul conceptual al proiectului trebuie să fie atât de puternic și universal; încât chiar într-un scenariu posibil de CTO (Community Take Over) ani mai târziu, >comunitatea să poată menține autonom potențialul inovator al proiectului, moștenind această moștenire.

### 5) Voință Nealgoritmică (Non-Algorithmic Agency)

- **Problema:** Producții digitale perfecte dar lipsite de suflet, repetitive.
- **Soluția [PoArt]:** Voința originală a unei ființe umane care poate greși, își asumă riscuri și simte fluctuații emoționale trebuie să se simtă în operă. Incertitudinea în loviturile de pensulă, reacțiile neașteptate ale materialului și deciziile instantanee ale artistului sunt **Semnătura Biologică** care diferențiază opera de "Producția Mecanică".

---

## c) Mecanismul de Verificare și Anti-Contrafacere

Acest sistem asigură că proiectul rămâne de încredere și viu nu doar "la început", ci "pentru totdeauna".

### 📦 Pachet de Dovezi (Evidence Pack - The Digital Twin)

În spatele fiecărei opere certificate [PoArt] se află un pachet de date criptat și marcat temporal pe care investitorii îl pot descărca:

- **Înregistrări Video RAW:** Înregistrări brute continue ale momentului producției.
- **Analiză Metadata:** Data creării fișierului, informații despre dispozitivul utilizat și date despre locație.
- **Referințe Fizice:** Dovezi că opera există în lumea fizică  
  (De exemplu: Ziar curent sau date blockchain curente lângă operă).

> *Notă despre consistență:* Expresia "pachet de dovezi" este legată de linia **Evidence Pack → EvidenceRoot → NotarySeal** din secțiunile anterioare; adică integritatea pachetului este reprezentată de sigiliul verificat.

### 🔄 Actualizare la 365 de Zile (The Sustainability Protocol)

- **Caracteristică Revoluționară:** În proiectele cripto "Dev" (Dezvoltatorul) lansează token-ul pe piață și de obicei dispare după 1-2 luni (Soft Rug). [PoArt] face acest lucru imposibil.
- **Regulă:** Statutul de "Verified Artist" (Artist Verificat) nu este pe viață. Este valabil doar pentru **1 an**.
- **Funcționare:** Artistul/dezvoltatorul trebuie să prezinte comunității la fiecare 365 de zile **o nouă operă mare și verificată**.
- **Exemplu de Scenariu:** Ai lansat proiectul în 2026. În ianuarie 2027, sistemul emite avertismentul "Perioada de Dovadă Expirată". Dacă artistul nu prezintă o nouă expoziție, o nouă operă fizică sau o nouă integrare tehnologică, "Insigna de Încredere" a proiectului scade.
- **Rezultat:** Acest sistem asigură că **conținutul nu își pierde niciodată relevanța** și că investitorul nu trăiește în frica *"Este dezvoltatorul încă aici?"*. Proiectul devine un studio live.

### 🚩 Steag Roșu (Red Flag Protocol)

**În cazul detectării oricărei contrafaceri de către comunitate sau algoritmi (utilizare AI, lucrare furată, video manipulat):**

1. Certificatul este marcat imediat ca **"ANULAT" (VOID)**.
2. Pachetele de dovezi sunt marcate public ca **"False"**.
3. Proiectul este introdus în lista neagră [PoArt]. Aceasta întărește faptul că în lumea descentralizată **reputația este singura monedă**.

---

## d) Concluzie: Nu Un Cazinou, Un Muzeu

**Pump.fun și Schimburile Descentralizate (DEX) sunt din păcate acum cazinouri; luminile clipesc, toată lumea caută profituri rapide, iar cazinoul (escroci) câștigă întotdeauna. Motivul pentru care am lansat proiectul aici este lipsa unui buget suficient și existența unui public existent accesibil prin live-uri.**

**[PoArt] este o fortăreață construită în mijlocul acestui cazinou.**

- 🎰 Cazinourile se bazează pe cărți; noi ne bazăm pe **realitatea fizică**.
- 🃏 Cazinourile sunt deschise fraudei; noi suntem deschiși la **dovezi transparente**.
- ⏳ Cazinourile sunt temporare; noi ne concentrăm pe **eternitatea artei și științei**.

**Un token care folosește acest protocol nu este doar o "monedă"; este un titlu de valoare digital care conține sudoare, vopsea, cod și filozofie.**

---

## 🗳️ 6) GUVERNANȚĂ ȘI REGISTRU PUBLIC (Governance & Public Registry)

**Scopul acestei secțiuni este: îndepărtarea standardului [PoArt] din sfera "încrederii în oameni" și transformarea sa într-o infrastructură publică durabilă cu registru + verificare + supraveghere comunitară.**

### 6.1 Registru Public (Public Registry)

- **Public Registry:** Toate datele aprobate sunt înregistrate la adresa `ilhanart.org/registry` (sau GitHub Registry).

**Logica înregistrării (standard recomandat - format cale JSON):**

Fiecare înregistrare care intră în registru conține cel puțin aceste câmpuri de bază verificate:

- **Identitate și Statut:**
  - `certificate_id` (referință lizibilă)
  - `status` (active / void)
  - `void_reason` (dacă există)
  - `visibility` (private / masked / public)
  - `created_at` (timestamp)

- **Instituție Emitentă:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informații despre Operă:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (dacă este posibil; pentru identitate token-gated)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Date Criminalistice:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Dovezi Criptografice:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Guvernanță:**
  - `governance.decision`
  - `governance.veto_threshold`

Registrul poate avea două niveluri:
- **1)** Index lizibil pentru oameni (listă web / căutare / filtru)
- **2)** Manifest lizibil pentru mașini (înregistrări JSON; pentru verificare PFE)

**Aici "înregistrarea" devine verificată de lanțul Evidence Pack → EvidenceRoot → NotarySeal al PFE. Registrul oferă scopul verificării, nu "afirmația".**

---

### 6.2 Veto Comunitar de 40% (Token-Gated Governance)

- **Veto Comunitar de 40%:** Votul începe cu o lună înainte de a primi statutul; obiecția a 40% din comunitatea **Token-Gated (Solana-Verified)** anulează cererea.

**Flux de vot (proces recomandat curat):**
- **Fereastră de candidatură:** Proiectul candidat deschide "înregistrarea candidat PoArt" (înregistrările candidaților apar cu statutul "pending").
- **Perioadă de revizuire:** Timp de 30 de zile comunitatea examinează dovezile (Evidence Pack + înregistrări live + metadata).
- **Verificare token-gated:** Votul se face prin portofele verificate pe Solana (de ex., deținerea unui anumit token/NFT + semnătură portofel).
- **Regula de veto:** Dacă 40% din voturi sunt **obiecție (NO / VETO)**, cererea este respinsă.
- **Transparență:** Rezultatul votului este stocat în registru ca "decision record" (dată, raport, ID snapshot).

---

### 6.3 Sincronizare Metadata (Conformitate cu Lumea Fizică)

- **Metadata Sync:** Datele tehnice din registru trebuie să corespundă 100% cu activul fizic.

**Definiția tehnică a "conformității 100%" (claritate recomandată):**
- **Conformitate minimă (obligatorie):**
  - `asset.fingerprints.sha256/sha512` din registru trebuie să fie **exact identic** cu hash-ul fișierului din mână.
  - `proof.notary_seal` din registru, când este reprodus (dacă Evidence Pack există), trebuie să fie **exact identic**.
- **Conformitate referință fizică (tip dovadă):**
  - Dovezi precum opera fizică arătată în live + referință dată/bloc trebuie să fie consistente cu Evidence Pack.
- **Conformitate confidențialitate:**
  - Câmpuri precum IP/locație în vizibilitate `masked` sunt publicate **conform standardului de mascare**.

---

### 6.4 Contestație, Revizuire și Anulare (Dispute & Revocation)

Registrul nu este doar un mecanism de "aprobare"; este un **mecanism de supraveghere vie împotriva contrafacerii**.

- Când se inițiază o contestație, înregistrarea poate fi pusă în modul **"review"**.
- Dacă se detectează contrafacere, este marcată ca `status: void` și se adaugă motivul:
  - `void_reason` (utilizare AI / plagiat / manipulare etc.)
  - `revoked_at` (momentul anulării)
- Sursa deciziei de anulare este clar vizibilă în registru:
  - vot comunitate / consiliu autorizat / notă investigație criminalistică (în funcție de aplicabilitate)

> **Această secțiune este echivalentul din registru al conceptului VOID din secțiunea "Red Flag Protocol".**

---

### 6.5 Exemplu de Înregistrare în Registru (Lizibil pentru Mașini)
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
    "title": "Fără titlu",
    "creator": "Anonim",
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
> *Notă: `asset.fingerprints.sha512` și alte valori hash sunt scurtate în scopuri demonstrative; în aplicația reală se folosește șirul de caractere hexazecimale de lungime completă.*

---

## 7) 🔐 SIGILIU TEHNIC (NOTARY SEAL)

**PoArt Forensic Engine (PFE) v1.0** algoritm de sigilare neclintit produs cu:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Protocolul [PoArt] Notar Digital și Dovadă Criminalistică (Beta v1.0)

> **"Cultura Mai Mare decât Capitalul. Protejează-ți operele astăzi, du-le mâine."**

---

## De Ce Public?

Securitatea adevărată vine din transparență. Datorită sistemului nostru **Public Registry (Registru Public)**, o persoană din orice parte a lumii poate verifica în câteva secunde dacă fișierul pe care îl are în mână este original, fără a avea nevoie de nicio autoritate.

---

## 🧩 De Ce Există Mai Multe "Module de Vizibilitate"?

Cea mai critică parte a codului este aici (meniul de selectare a vizibilității). Aceste opțiuni permit utilizatorilor să echilibreze **"Confidențialitate vs Transparență"**:

### 🔒 Privat (Private)

- **Scenariu:** Artistul nu dorește încă să publice opera, dar dorește să o marcheze temporal și să dovedească "am făcut asta la această dată".
- **Ce Face Codul:** Înregistrează datele în baza de date, dar aplică tag-ul `visibility: "private"`. În viitor, la scrierea politicii "Public Read", puteți ascunde aceste înregistrări de public spunând `WHERE visibility = 'public'`.

### 🕶️ Mascat (Masked)

- **Scenariu:** Artistul dorește transparență, dar se teme că va fi găsită adresa casei (locația IP).
- **Ce Face Codul:** Pe partea JavaScript funcționează funcțiile `maskIP` și `maskLoc`. Convertește adresa IP în formatul `88.241.***.***` și locația în formatul `***/TR` și trimite versiunea cenzurată în baza de date.
- **Notă despre Confidențialitate:** Mascarea se întâmplă în browser, Supabase nu vede locația reală. **Cu toate acestea:** Dacă se folosesc API-uri terțe precum ipapi.co pentru date despre locație, acești furnizori văd adresa IP la momentul cererii.
- **Sigilare în Modul Masked:** Calculul EvidenceRoot și NotarySeal se face cu datele forensics mascate; astfel verificarea rămâne deterministă.

### 🌍 Public (Public)

- **Scenariu:** Transparență completă. Conform standardului [PoArt], unde, când și din ce rețea a fost produsă opera este declarat explicit.

---

## 💡 Inovație Tehnologică

PoArt nu este doar un sistem de încărcare fișiere. Este un motor **"Forensic Chain of Custody"** care topește trei straturi tehnologice diferite într-un singur creuzet și aduce un nou standard.

**Stratul descris în această secțiune ca "motor" corespunde nucleului PoArt Forensic Engine (PFE) în terminologia anterioară.**

### 1) Client-Side Hashing (Confidențialitate Maximă)

Fișierele operelor tale nu sunt niciodată încărcate pe server. Motorul nostru bazat pe browser (Client-side) calculează hash-ul (digestul digital) al fișierului pe computerul tău. Doar această amprentă și metadata sunt trimise pe server.

> **Notă despre Confidențialitate:** Fișierul operei nu este încărcat pe server și astfel este protejat. Cu toate acestea, datele forensics (IP/locație) sunt partajate conform modului de vizibilitate ales (private/masked/public).

### 2) Forensic Data Fusion (Putere Criminalistică)

Este mult mai mult decât un simplu marcaj temporal. Sistemul combină următoarele date într-un singur "Genesis Seal":

- **Digest Digital (SHA-512):** Folosind standardul de digest criptografic (SHA-512), amprenta digitală care se va strica chiar dacă se schimbă un singur pixel al operei.
- **Locație și Timp:** Data cu precizie de milisecundă, țara, orașul și districtul unde a fost efectuată tranzacția.
- **Identitate Dispozitiv:** Sistem de operare, browser și tip de dispozitiv (analiză User-Agent).

---

## 🛡️ Zone de Aplicare și Avantaje

Dacă ești artist, scriitor sau designer, nu este suficient să spui "Am făcut asta mai devreme", trebuie să dovedești.

**O operă sigilată PoArt:**

- **Dovadă Matematică:** Sistemul detectează aceasta chiar dacă se schimbă un singur pixel al fișierului. Manipularea este imposibilă.
- **Fundament Legal:** Este înregistrat la ce dată, în ce oraș, de pe ce dispozitiv a fost sigilată opera.
- **Certificat Instant:** În câteva secunde generează un **"Certificat de Identitate Activ"** personalizat cu cod QR și sigilat.

---

## ⚙️ Arhitectură Sistem și Specificații Tehnice

Sistemul este proiectat pe arhitectura "Serverless" (Fără Server), concentrat pe performanță ridicată și scalabilitate.

| Strat | Tehnologie | Descriere |
|--------|-----------|----------|
| **Criptografie** | SHA-256 & SHA-512 | Digest criptografic cu două straturi |
| **Bază de Date** | Supabase (PostgreSQL) | Structură date JSONB, politici RLS |
| **Date Criminalistice** | ipapi.co API | Triada IP/Locație/Timp |
| **Redare** | html2canvas + jsPDF | Generare PNG/PDF pe partea client |
| **Frontend** | Vanilla JavaScript | Dependențe zero de framework |
| **Securitate** | Client-side hashing | Fișierul nu ajunge niciodată pe server |

### Caracteristici Distinctive

| Caracteristică | Detaliu | La Concurenți? |
|---------|-------|-------------|
| **Drag & Drop UI** | Trage și plasează fișierul, previzualizare instantanee | ❌ Absent la majoritatea |
| **Multi-Format Export** | PNG, JSON, PDF - o singură apăsare | ⚠️ Limitat |
| **Real-Time Preview** | Previzualizare certificat în timp real | ❌ Absent |
| **Privacy Controls** | Opțiuni Private/Masked/Public | ❌ Absent |
| **Client-Side Hashing** | Fișierul nu ajunge niciodată pe server | ✅ Doar la unele |
| **Forensic Metadata** | IP, locație, dispozitiv, timp - toate împreună | ❌ Fragmentar |
| **QR Verification** | Cod QR pentru verificare instantanee | ⚠️ Limitat |
| **Rate Limiting** | Protecție împotriva spam (RLS + Client) | ❌ Absent la majoritatea |

---

## 🗺️ Foaie de Parcurs: Viitor "Trustless"

Versiunea curentă **(Beta v1.0)** este optimizată pentru a oferi utilizatorului final viteză maximă, interfață ușoară și acces gratuit. Cu toate acestea, viziunea noastră finală este tranziția către o structură în care nici măcar administratorul bazei de date (noi) nu poate interveni.

### Faza 1: Beta (Acum Disponibilă)

- **Infrastructură:** Cloud Database (Supabase).
- **Scop:** Viteză, eliminarea barierelor UX (Experiență Utilizator) și adaptare. Asigurarea securității "fără frecare".

### 🚀 Faza 2: (Ce Necesită Backend / Edge Function)

Această fază acoperă tranziția de la structura sistemului care funcționează complet "Client-Side" la o structură mai sigură și gestionată "Server-Side Authority".

| Element | Ce Aduce? | Tech Stack | Prioritate |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Function** | Blocare spam + securitate cheie API | Supabase Edge (Deno) | 🔴 Ridicat |
| **Semnătură Portofel** | Autentificare identitate criptografică | Solana Wallet Adapter | 🟡 Mediu |
| **Backup IPFS/Arweave** | Imuabilitate descentralizată | IPFS SDK + Pinata | 🟢 Scăzut |
| **Mecanism Revocare** | Anulare certificate false | Actualizare Schemă DB | 🔴 Ridicat |
| **Audit Log** | Înregistrare investigație criminalistică | Tabel loguri personalizat | 🟡 Mediu |
| **OpenTimestamps** | Ancorare în Bitcoin | OTS JavaScript | 🟢 Scăzut |
| **Integrare DID** | Decentralized Identity | ION/Ceramic | 🟢 Scăzut |

### Faza 3: Descentralizare Completă (Termen Lung)

| Caracteristică | Scop | ETA |
|---------|-------|-----|
| **Blockchain Registry** | Înregistrare on-chain Ethereum/Solana | Q4 2026 |
| **DAO Governance** | Guvernare comunitară | Q1 2027 |
| **Multi-Chain Support** | Polygon, Arbitrum, Base | Q2 2027 |
| **Legal Recognition** | Validitate în instanțele turcești | 2027-2028 |
| **API for Developers** | Endpoint API public | Q3 2026 |

---

## 📊 Analiză Concurenți (Actualizată)

PoArt este poziționat pe "Sweet Spot" (Punctul Optim Ideal) care completează golurile soluțiilor existente.

| Caracteristică | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 証 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Cost** | 🆓 Gratuit | 🆓 | 💰 Plătit | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Foarte Ușor | ❌ CLI | ⚠️ Mediu | ⚠️ Mediu | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ În Timp Real | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Moduri | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Confidențialitate | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Complet | ❌ | ❌ | ⚠️ Limitat | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Instant | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Foaie de parcurs | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Suport Românesc** | 🔄 În dezvoltare | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Legendă:**
- ✅ : Suport complet / disponibil
- ⚠️ : Limitat / în planuri plătite
- ❌ : Absent / nu este suportat
- 🔄 : Pe Foaia de Parcurs (în dezvoltare)
- 🆓 : Complet gratuit
- 💰 : Plătit / abonament necesar

### Dezavantajele Concurenților, Punctele Forte ale PoArt

| Minus | Concurenți | PoArt |
|------|----------|-------|
| **Complexitate Utilizare** | CLI, cunoștințe API, portofel necesar | Trage și plasează, se termină în 3 apăsări |
| **Barieră Cost** | Abonament $50-500/lună | 100% gratuit |
| **Confidențialitate** | Fișierul este încărcat pe server | Client-side, fișierul nu pleacă niciodată |
| **Date Criminalistice** | Doar marcaj temporal | IP, locație, dispozitiv, timp - toate |
| **Suport Românesc** | Absent sau foarte limitat | Suport nativ în limbă |
| **Open Source** | Cutie închisă | Tot codul deschis pe GitHub |

---

## 🧬 Structură Date Protocol (JSON Schema)

**Fiecare certificat [PoArt] are o identitate JSON portabilă și verificabilă produsă în următorul standard.**

> **Notă:** Acest format Identity JSON este formatul certificatului prezentat utilizatorului. În înregistrările de registru în loc de `identity.asset_data` se folosește `registry.asset` (mapare: `identity.asset_data` == `registry.asset`).
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
    "title": "Whitepaper Oficial",
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

## 🔬 Profunzime Tehnică: Algoritmul de Sigilare

### Funcții Hash Deterministe
```javascript
// Funcții Ajutătoare: Convertiți digestul în șir hex
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Convertiți șirul în array de octeți
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Generarea șirului canonic forensics (v1.0: ordine fixă câmpuri + UTF-8 + separator \n)
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

### Procesul de Producție NotarySeal (Complet Determinist)
```javascript
// 1. Calculul FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Colectarea datelor criminalistice (folosind un singur timestamp)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Generarea unui singur timestamp
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

// 3. Crearea EvidenceRoot (cu codare canonică)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Producția NotarySeal (folosind același timestamp)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Funcții ajutătoare de mascare (suport IPv4 și IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Control IPv4
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

### Fluxul de Verificare (Două Niveluri)

#### Quick Verify (Verificare Rapidă)
```javascript
// Verifică doar hash-ul fișierului (steag roșu rapid)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Obține din Registru
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Comparare hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Original - Hash-ul fișierului se potrivește"
    };
  } else {
    return {
      valid: false,
      message: "❌ Fals - Fișierul este manipulat"
    };
  }
}
```

#### Full Verify (Verificare Completă)
```javascript
// Reproduce și verifică EvidenceRoot și NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Obține din Registru
  const cert = await fetchFromRegistry(certificateId);

  // 1) Control FileHash (steag roșu rapid)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Fals - Hash-ul fișierului nu se potrivește" };
  }

  // 2) Reproduceți EvidenceRoot (cu datele forensics salvate în registru)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Nu se potrivește - EvidenceRoot invalid" };
  }

  // 3) Reproduceți NotarySeal (cu același timestamp + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Nu se potrivește - NotarySeal invalid" };
  }

  // Opțional: În Faza 2 verificați și signer_sig cu attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Semnătură invalidă" };

  return { valid: true, message: "✅ Original - Full Verify trecut" };
}
```

> **Note Importante:**
> - **Quick Verify:** Verifică doar hash-ul fișierului pentru utilizare rapidă.
> - **Full Verify:** Verifică toate straturile protocolului (EvidenceRoot + NotarySeal).
> - Toate operațiunile de hash se execută în mod determinist, cu codare fixă și separatori.
> - **Standard canonizare v1.0:** Ordine fixă câmpuri + codare UTF-8 + separator `\n`.
> - **Plan Faza 2:** Tranziție la JSON canonic cu RFC 8785 (JCS - JSON Canonicalization Scheme).
> - În modul Masked calculul EvidenceRoot și NotarySeal se face cu forensics mascat.
> - Se folosește un singur timestamp în întregul proces (forensics + NotarySeal); determinismul este garantat.
> - **Nume câmpuri Forensics:** `ip_masked`, `location`, `device`, `timestamp` (cod și registru complet compatibile).
> - **Cale Registru:** `certificate.asset.fingerprints` (complet compatibil cu codul de verificare).
> - **signer_sig în Registru:** Câmpul `proof.signer_sig` este necesar pentru Full Verify.
> - Mecanismul SignerSignature va fi activat în Faza 2 cu Solana Wallet Adapter; în v1.0 se poate efectua verificarea cu `attestation_pubkey`.

---

## 📈 Statistici Utilizare (Obiective Q1 2026)

| Metrică | Obiectiv | Stare |
|--------|-------|-------|
| **Certificate Totale** | 1,000 | 🔄 În Proces |
| **Utilizatori Activi** | 500 | 🔄 În Proces |
| **Număr Verificări** | 5,000 | 🔄 În Proces |
| **Uptime** | %99.9 | ✅ Activ |
| **Timp Răspuns Mediu** | <200ms | ✅ Optim |

---

## 🌍 Comunitate și Suport

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 Contribuitori

Protocolul PoArt evoluează datorită contribuțiilor comunității open source.

**Pentru a contribui:**
1. Faceți fork
2. Creați ramura de funcție (`git checkout -b feature/amazing-feature`)
3. Faceți commit (`git commit -m 'Add amazing feature'`)
4. Faceți push (`git push origin feature/amazing-feature`)
5. Deschideți Pull Request

### 🛠️ Ce Avem Nevoie Acum? (Apel pentru Ajutor)

Căutăm contribuții de la dezvoltatori experimentați în următoarele subiecte pentru dezvoltările **Faza 2** ale Protocolului PoArt:

* **Supabase Edge Functions:** Mutarea protecției împotriva spam pe partea server.
* **Solana Web3.js:** Integrare semnătură portofel (Wallet Signing).
* **IPFS / Arweave:** Integrarea serviciilor de arhivare și ancorare.

> Înainte de a adăuga o funcție, vă rugăm să începeți o discuție în secțiunea "Issues".

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Cultura Mai Mare decât Capitalul*

## 🧾 Licență

MIT License © 2026 İlhan Art Gallery Initiative

Vezi [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) pentru condiții complete.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Acest proiect a fost dezvoltat cu inițiativa [İlhan Art Gallery] și codul sursă este disponibil public pentru transparență.**

**PROTOCOL V1.0 // SIGILAT CU SHA-512.**

*© 2026 İLHAN ART | TOATE DREPTURILE ASUPRA OPERELOR, IMAGINILOR ȘI IDEILOR SUNT PROTEJATE.*

---
