# 📚 GLOSSARIO DELLA TERMINOLOGIA E DEI CONCETTI
> **"Comprendere il linguaggio di questo protocollo significa comprenderne la visione."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Infrastruttura centrale

**PoArt Forensic Engine (PFE)** è il livello principale che rappresenta la logica centrale e il funzionamento tecnico alla base del protocollo [PoArt]. Questo è il "motore forense" che prende i dati grezzi di produzione dell'opera d'arte e li trasforma in una **prova digitale** verificabile e immutabile.

### 🧩 Perché "PoArt Forensic"?

- **PoArt (Proof of Art):** Il focus del motore è legare il valore di un asset digitale non alla speculazione, ma al **processo di produzione dimostrabile**.
- **Forensic (Verifica forense):**
  - **Definizione tecnica:** Approccio algoritmico e catena di registrazione per verificare che i dati relativi al processo di produzione (pennellate, timelapse, log) non siano stati manipolati.
  - **Livello filosofico:** L'affermazione di trasformare la produzione umana, che contiene **tempo, sforzo e costo delle decisioni**, in una realtà misurabile, in contrasto con la "produzione istantanea" dell'intelligenza artificiale.

> Nota: L'integrazione della blockchain (ad es. Solana) non è il nucleo del PFE; viene considerata come un **Chain Anchor Layer** separato da definire per la verifica/registro.

### 🛠️ Ambito tecnico v1.0

**PoArt Forensic Engine (PFE) v1.0** è costruito su questi **3 pilastri principali** invece che su modelli finanziari complessi:

1. **Hashing & Sealing (Sigillatura):**  
   Il PFE elabora deterministicamente tutti gli elementi nell'Evidence Pack (file dell'opera, video, JSON/log, firma ecc.) e produce il valore univoco **NotarySeal**.

   **Concetti fondamentali (v1.0):**
   - **FileHash (impronta digitale dell'opera):** Hash generato dai byte del file dell'opera.
   - **EvidenceRoot (radice del pacchetto di prove):** Riepilogo della radice che rappresenta l'integrità dell'Evidence Pack (radice Merkle o hash del manifest canonico).
   - **NotarySeal (sigillo finale / Output PFE):** Sigillo finale prodotto dalla combinazione di EvidenceRoot + tempo + firma.

   **Formule (chiaramente visibili all'investitore):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Definizioni del Payload Canonico (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Nota: Il valore inteso come output del PFE è **NotarySeal**. Il meccanismo **SignerSignature** sarà attivato nella Fase 2 (con Solana Wallet Adapter); nella v1.0 attuale viene utilizzata la firma di attestazione propria del sistema. La chiave pubblica di attestazione viene pubblicata nel registro nel campo `issuer.attestation_pubkey`.

2. **Indexing (Archiviazione):**  
   Elabora in un livello di registrazione trasparente e interrogabile quale portafoglio, in quale data, ha presentato **Labor Proof (Prova di lavoro)** per quale opera.  
   *(Questo livello può essere un database; l'integrazione della catena è definita separatamente come "Chain Anchor Layer".)*

3. **Verification (Verifica):**  
   Quando l'autenticità di un'opera viene messa in discussione, il PFE rielabora le prove grezze; verifica con certezza matematica se i valori calcolati di **EvidenceRoot / NotarySeal** corrispondono alla registrazione nell'archivio.

---

### 🧮 Teorema del valore PoArt (The Value Theorem)

Il protocollo [PoArt] collega il valore ($V$) di un asset digitale non alla percezione soggettiva del mercato, ma alla **realtà fisica del processo di produzione**.

L'Intelligenza Artificiale (AI) distrugge il processo fornendo il risultato istantaneamente ($t \to 0$). [PoArt] invece considera il valore come l'accumulo dei componenti **tempo, lavoro e volontà**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definizione delle variabili

- **$\int dt$ (Accumulo del processo):**  
  Il valore non è un "output" istantaneo; è un **processo** che si accumula tra $t_{\text{start}}$ e $t_{\text{end}}$. Man mano che la durata diminuisce (produzione AI), il risultato dell'integrale si avvicina a 0.

- **$P_{\text{labor}}(t)$ (Forza lavoro istantanea):**  
  Rappresenta l'intensità dello sforzo mentale e fisico speso nel momento della produzione. All'aumentare dello sforzo dimostrabile, l'integrando cresce.  
  > Nota: Questo termine può essere normalizzato in pratica attraverso "segnali di lavoro misurabili/dimostrabili".

- **$I_{\text{agency}}(t)$ (Coefficiente di volontà):**  
  È la capacità del produttore di assumersi rischi e prendere decisioni. Assume un valore tra $0$ e $1$.
  - **AI ($I \approx 0$):** Esegue comandi, non si assume rischi, non paga un prezzo.
  - **Umano ($I \to 1$):** Cambia decisioni, esita, si assume rischi.

- **$U_{\text{irreversible}}$ (Singolarità irreversibile):**  
  Mentre nella produzione digitale è possibile l'annullamento (`Ctrl+Z`); nella produzione fisica (vernice applicata su tela, marmo scolpito, gesto in diretta) non c'è ritorno. Questa **irreversibilità** è un termine aggiuntivo che crea "singolarità" (carattere non fungibile) nell'opera.

### 🔎 Analisi del caso: AI "Output istantaneo" vs Umano "Processo dimostrato"

Lo scenario seguente mostra come funziona in pratica il **Teorema del valore PoArt** e perché le produzioni AI ricevono punteggi bassi nello standard [PoArt].

#### Scenario A: Produzione visiva con AI in 10 secondi

- **Durata ($\Delta t$):** $10$ secondi (processo praticamente assente)
- **Forza lavoro ($P_{\text{labor}}$):** $1$ unità (solo scrittura del comando)
- **Coefficiente di volontà ($I_{\text{agency}}$):** $0.01$ (nessun rischio, nessun prezzo)
- **Irreversibilità ($U_{\text{irreversible}}$):** $0$ (reversibile / copiabile)

**Risultato:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Commento:** Anche se l'output è impeccabile; poiché il processo non è stato vissuto e non contiene volontà/rischio, il valore [PoArt] si avvicina a $0$.

#### Scenario B: Produzione fisica di 6 ore in diretta

- **Durata ($\Delta t$):** $6$ ore ($21{,}600$ secondi)
- **Forza lavoro ($P_{\text{labor}}$):** $0.5$ unità (continuità dello sforzo fisico e mentale)
- **Coefficiente di volontà ($I_{\text{agency}}$):** $0.9$ (cambiamenti di decisione, assunzione di rischi, scelte irreversibili)
- **Irreversibilità ($U_{\text{irreversible}}$):** $>0$ (tracce fisiche irreversibili)

**Risultato:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Commento:** Man mano che il processo si allunga e la volontà (rischio) aumenta, il valore cresce cumulativamente. Il termine $U_{\text{irreversible}}$ è un contributo aggiuntivo che crea "singolarità" (carattere non fungibile) nell'opera.

---

### ✅ Conclusione: Valore vincolato alla prova (Proof-Bound Value)

Questo teorema porta l'affermazione di valore di [PoArt] fuori dall'essere un "gusto" o una "narrativa di mercato" e la lega a una **realtà di produzione dimostrabile**.

1. **Senza processo non si crea valore:**  
   L'AI distrugge il processo con output istantaneo ($t \to 0$). Man mano che la finestra del processo si restringe, il risultato dell'integrale diminuisce per necessità matematica:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Volontà e rischio sono moltiplicatori:**  
   [PoArt] misura non solo il "tempo speso", ma anche il livello reale di decisione, rischio e prezzo in quel tempo. Il valore di una produzione senza rischio (AI) è basso:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **La singolarità è una prova fisica, non marketing:**  
   Le tracce irreversibili nella produzione fisica (pennellata su tela, scheggia di marmo) sono al di fuori della logica del `Ctrl+Z` digitale. Questa irreversibilità ($U_{\text{irreversible}}$) singolarizza l'opera ontologicamente.

> **🔐 RIEPILOGO:** Anche se il teorema del valore può sembrare indeterminato come misurazione (anche se nella vita reale non può essere misurato al 100%), lo scopo di questa formula è mostrare la costruzione e la direzione delle variabili. Nell'era dell'AI, ciò che è raro non è l'"immagine"; è il **lavoro dimostrabile, il tempo e la volontà**. [PoArt] misura questa scarsità e la registra con l'**Evidence Pack**.

### 🏛️ L'importanza del concetto di "Engine" (Motore)

I token provenienti da Pump.fun o piattaforme simili sono spesso solo **"biglietti di accesso"**. **PoArt Forensic Engine (PFE)** invece è il **livello logico costituzionale** che determina quali diritti protegge quel biglietto, come verrà registrato il lavoro e come verranno perpetuati arte/scienza/tecnologia.

> **Nota:** Il motivo per cui abbiamo lanciato questo progetto su Pump.fun è che non avevamo liquidità sufficiente e un numero sufficiente di follower. Utilizzare i dati esistenti è stata strategicamente la mossa giusta, anche se non della massima qualità. Indipendentemente dal budget e dalle possibilità, definire la logica di questo motore su GitHub dimostra che il progetto non è solo una speculazione finanziaria, ma una visione di **infrastruttura software** a lungo termine e di **biblioteca nazionale digitale**.

---

## 🎨 PROTOCOLLO DI PROVA DEL LAVORO [PoArt] (Proof of Art Protocol v1.0)

> **"Vero artista, vera produzione, vero valore."**

Questo protocollo è un **meccanismo di difesa biologico e intellettuale** sviluppato contro i truffatori anonimi che circondano l'ecosistema crypto, le immagini di intelligenza artificiale prodotte in 5 minuti e la cultura "Pump & Dump" (pompa e scarica).

---

## a) Cos'è [PoArt]? (Definizione filosofica e tecnica)

**Proof of Art [PoArt];** è uno standard di verifica istituzionale che garantisce che il valore dietro un asset sulla blockchain sia basato non sulla speculazione, ma sul **lavoro umano** verificabile, sul **tempo** e sull'**energia fisica**.

Come Bitcoin crea valore con *"Elettricità e potenza del processore"* **(Proof of Work)**; i progetti compatibili con [PoArt] creano valore con *"Talento artistico e tempo umano"*.

Elimina il rischio di *"Lo sviluppatore (Dev) ha venduto, progetto finito"* su piattaforme Pump.fun e DEX; perché qui il valore non è nel codice, ma nella **continuità della produzione**.

> **[PoArt] non dice al partecipante "Fidati di noi"; dice "Ecco le prove, guarda con i tuoi occhi, verifica con la tua matematica".**

---

## b) Standard a 5 pilastri [PoArt] (The 5 Pillars of Truth)

Questi 5 punti sono filtri non manipolabili che un progetto deve superare per ottenere il sigillo [PoArt].

### 1) Prova di identità dal vivo (Live Identity Proof)

- **Problema:** Il mondo crypto è pieno di fondatori anonimi (Dev) con identità poco chiara che raccolgono denaro e abbandonano il progetto.
- **Soluzione [PoArt]:** Il produttore dimostra non solo la carta d'identità, ma **la sua presenza durante la produzione**. Questo include sessioni di streaming dal vivo in cui si interagisce con la comunità e si soddisfano richieste specifiche istantanee, non video preregistrati.  
  (Es: *"Scrivi la data di oggi e il numero del blocco corrente nell'angolo destro della tela"*)
- **Motto:** *"I bot possono fare immagini ma i bot non sudano e non improvvisano."*

### 2) Prova di lavoro e processo (Labor & Process Proof)

- **Problema:** Il fatto che le immagini AI (Intelligenza Artificiale) prodotte in 2 secondi e la pittura ad olio realizzata in 2 mesi ricevano lo stesso trattamento "jpeg" nel mondo digitale.
- **Soluzione [PoArt]:** Il processo di "gravidanza e nascita" dell'opera viene registrato. Vengono documentate le fasi di schizzo, gli strati di vernice, le ore cumulative spese e il processo fisico che l'artista ha vissuto creando quell'opera. Questo aggiunge un **"Costo del tempo" (Time Cost)** al token. Più è difficile la produzione di un asset, più solido è il suo valore.

### 3) Prova del valore estetico (Aesthetic Value Proof)

- **Problema:** La cultura dei "meme" ignora l'estetica e la profondità artistica concentrandosi solo sulla commedia istantanea, risultando in progetti "Hype" di breve durata.
- **Soluzione [PoArt]:** Il progetto deve avere standard artistici accademici, teoria del colore, regole di composizione e conoscenza dei materiali (Impasto, Texture ecc.). Il contenuto non deve solo far ridere; deve suscitare ammirazione nello spettatore e avere **valore collezionistico**.

### 4) Innovazione concettuale (Conceptual Novelty)

- **Problema:** Migliaia di monete di cani/gatti che sono copie l'una dell'altra, lontane dalla creatività.
- **Soluzione [PoArt]:** Il progetto deve costruire un nuovo ponte che unisce arte, scienza, filosofia o tecnologia in una struttura significativa.  
  (Es: Combinare la classica statua del David con i dati del mercato crypto; elaborare l'idea della "pietrificazione" della percezione umana e giustificarla con fonti scientifiche.)  
  L'opera non deve essere solo una festa visiva; deve anche essere una sfida intellettuale che fa riflettere su **Scienza, Filosofia o Tecnologia**.

> [!IMPORTANT]
> **Esempio di riferimento (Effetto Las Palmitas):**  
> Nel quartiere messicano di Las Palmitas che lotta contro il crimine, oltre 200 case sono state trasformate in una gigantesca festa arcobaleno. Come risultato di questo intervento estetico, i tassi di criminalità nel quartiere sono diminuiti in una certa misura, i giovani hanno iniziato ad interessarsi all'arte invece che alle gang. Il cambiamento estetico ha ricodificato il rispetto delle persone per il loro ambiente e tra loro (Coesione sociale).
>
> **Aspettativa:** Un progetto che entrerà nella lista [PoArt]; deve, come nell'esempio sopra, contenere una relazione causa-effetto sociologica, scientifica o filosofica oltre alla pura estetica visiva. Poiché l'unico asset che non può essere acquistato con denaro è il "Tempo", in questo protocollo il tempo deve essere messo in staking e dimostrato come garanzia. La base concettuale del progetto deve essere così forte e universale che; anche in un possibile scenario CTO (Community Take Over) anni dopo, la comunità possa ereditare questa eredità e continuare autonomamente il potenziale innovativo del progetto.

### 5) Volontà non algoritmica (Non-Algorithmic Agency)

- **Problema:** Produzioni digitali impeccabili ma senz'anima che si ripetono.
- **Soluzione [PoArt]:** La volontà autentica dell'essere umano capace di sbagliare, assumersi rischi e sperimentare fluttuazioni emotive deve essere percepita nell'opera. L'incertezza nelle pennellate, le reazioni inaspettate del materiale e le decisioni istantanee dell'artista sono la **Firma biologica** che distingue l'opera dalla "Produzione meccanica".

---

## c) Meccanismo di verifica e anticontraffazione

Questo sistema garantisce che il progetto rimanga affidabile e vivo non solo "all'inizio", ma "per sempre".

### 📦 Pacchetto di prove (Evidence Pack - The Digital Twin)

Dietro ogni opera certificata [PoArt] c'è un pacchetto di dati crittografato e con timestamp che gli investitori possono scaricare:

- **Registrazioni video RAW:** Immagini grezze ininterrotte del momento della produzione.
- **Analisi dei metadati:** Data di creazione del file, informazioni sul dispositivo utilizzato e dati sulla posizione.
- **Riferimenti fisici:** Prove dell'esistenza dell'opera nel mondo fisico  
  (Es: Giornale corrente accanto all'opera o dati della blockchain di quel momento).

> *Nota di coerenza:* L'espressione "pacchetto di prove" si collega alla linea **Evidence Pack → EvidenceRoot → NotarySeal** delle sezioni precedenti; cioè l'integrità del pacchetto è rappresentata da un sigillo verificabile.

### 🔄 Rinnovo di 365 giorni (The Sustainability Protocol)

- **Caratteristica rivoluzionaria:** Nei progetti crypto lo "Dev" (Sviluppatore) lancia il token sul mercato e generalmente scompare dopo 1-2 mesi (Soft Rug). [PoArt] rende questo impossibile.
- **Regola:** Lo status "Verified Artist" (Artista verificato) non è a vita. È valido solo per **1 anno**.
- **Funzionamento:** L'artista/Sviluppatore deve presentare alla comunità **un'opera nuova, grande e dimostrabile** ogni 365 giorni.
- **Scenario di esempio:** Hai lanciato il progetto nel 2026. A gennaio 2027 il sistema avverte "Periodo di prova scaduto". Se l'artista non presenta una nuova mostra, una nuova opera fisica o una nuova integrazione tecnologica, il "Badge di fiducia" del progetto scende.
- **Risultato:** Questo sistema garantisce che **il contenuto non perda mai attualità** e l'investitore non viva la paura *"Lo sviluppatore è ancora qui?"*. Il progetto si trasforma in uno studio vivente.

### 🚩 Bandiera rossa (Red Flag Protocol)

**In caso di qualsiasi contraffazione rilevata dalla comunità o dagli algoritmi (uso di AI, opera rubata, video manipolato):**

1. Il certificato viene immediatamente contrassegnato come **"ANNULLATO" (VOID)**.
2. I pacchetti di prove vengono etichettati pubblicamente come **"Falsi"**.
3. Il progetto viene aggiunto alla lista nera [PoArt]. Questo rafforza il fatto che in un mondo decentralizzato **la reputazione è l'unica valuta**.

---

## d) Conclusione: Non casinò, ma museo

**Pump.fun e gli Exchange Decentralizzati (DEX) sono purtroppo attualmente dei casinò; le luci lampeggiano, tutti sono alla ricerca di guadagni rapidi e la cassa (truffatori) vince sempre. Il motivo per cui abbiamo lanciato il progetto qui è la mancanza di budget sufficiente e l'ambiente per raggiungere il pubblico esistente con dirette streaming.**

**[PoArt] è una fortezza costruita nel mezzo di questo casinò.**

- 🎰 Il casinò si basa sui giochi di carte; noi ci basiamo sulla **realtà fisica**.
- 🃏 Il casinò è aperto all'inganno; noi siamo aperti alle **prove trasparenti**.
- ⏳ Il casinò è temporaneo; noi ci concentriamo sull'**eternità dell'arte e della scienza**.

**Il token che utilizza questo protocollo non è solo una "moneta"; è un'azione digitale che contiene sudore, vernice, codice e filosofia.**

---
## 🗳️ 6) GOVERNANCE E REGISTRO PUBBLICO (Governance & Public Registry)

**Lo scopo di questa sezione è il seguente: Portare lo standard [PoArt] fuori dal piano del "fiducia nelle persone" e trasformarlo in un'infrastruttura pubblica sostenibile con registrazione + verifica + supervisione della comunità.**

### 6.1 Registro pubblico (Public Registry)

- **Registro pubblico:** Tutti i dati approvati vengono registrati all'indirizzo `ilhanart.org/registry` (o GitHub Registry).

**Logica di registrazione (standard raccomandato - formato percorso JSON):**

Ogni registrazione che entra nel registro contiene almeno questi campi verificabili essenziali:

- **Identità e stato:**
  - `certificate_id` (riferimento leggibile)
  - `status` (active / void)
  - `void_reason` (se presente)
  - `visibility` (private / masked / public)
  - `created_at` (timestamp)

- **Istituzione emittente:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informazioni sull'opera:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (se possibile; per l'identità del possessore del token)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Dati forensi:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Prove crittografiche:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Governance:**
  - `governance.decision`
  - `governance.review_notes`

Il registro può avere due livelli:
- **1)** Indice leggibile dall'uomo (elenco web / ricerca / filtro)
- **2)** Manifest leggibile dalla macchina (registrazioni JSON; per la verifica PFE)

**Qui la "registrazione" diventa verificabile attraverso la catena Evidence Pack → EvidenceRoot → NotarySeal del PFE. Il registro offre un obiettivo di verifica, non una "affermazione".**

---

### 6.2 Processo di candidatura PoArt Verified

**Le candidature PoArt Verified vengono valutate dalla Galleria İlhanArt secondo i 5 standard PoArt. Il feedback della comunità viene preso in considerazione, ma la decisione finale spetta al team curatoriale. Le decisioni vengono spiegate in modo trasparente e registrate su ilhanart.org/registry.**

#### Processo di candidatura

**Candidatura:**
- L'artista/progetto presenta domanda per PoArt Verified
- Viene preparato l'Evidence Pack (registrazioni video, metadati, link alle dirette)
- La candidatura viene inviata alla Galleria İlhanArt

**Revisione (30 giorni):**
- Il team della galleria esamina in dettaglio l'Evidence Pack
- Vengono controllati tutti i 5 standard PoArt:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Intervista con l'artista (opzionale)

**Consultazione della comunità:**
- L'Evidence Pack viene condiviso pubblicamente durante il processo di candidatura
- I possessori di token (minimo 10.000 $CULTURE) possono fare proposte in particolare
- **Tutto il feedback viene preso in considerazione nel processo di revisione**
- **Tuttavia la decisione finale dipende dalla valutazione curatoriale**

**Decisione:**
- La galleria approva o respinge la candidatura
- La motivazione della decisione viene spiegata in modo trasparente
- Se approvato → badge PoArt Verified
- Se respinto → è possibile ripresentare la candidatura dopo 6 mesi

**Trasparenza:**
- Tutte le candidature e decisioni vengono registrate su ilhanart.org/registry
- Il verbale della decisione viene pubblicato pubblicamente:
  - Data della candidatura
  - Riepilogo del processo di revisione
  - Decisione (Approvato / Respinto)
  - Motivazione della decisione (breve spiegazione)
  - Riepilogo del feedback della comunità (anonimo)

#### Perché la decisione curatoriale?

**Controllo di qualità:**  
Lo status PoArt Verified è un badge con standard elevati. La valutazione curatoriale garantisce il mantenimento di questi standard.

**Prevenzione della manipolazione speculativa:**  
Con i token Pump.fun, la governance completa on-chain (es: Realms, voting DAO) non è tecnicamente possibile. I sistemi di voto off-chain sono vulnerabili alla manipolazione delle balene e agli attacchi coordinati. La decisione curatoriale elimina questo rischio.

**Efficienza operativa:**  
Invece di complessi meccanismi di voto, processo decisionale rapido e chiaro. Gli artisti ottengono risultati entro 30 giorni.

**Partecipazione della comunità:**  
Il feedback della comunità viene completamente preso in considerazione e influenza il processo decisionale. Tuttavia la decisione finale spetta al team curatoriale protetto dalla manipolazione.

**Futuro:**  
Quando il progetto matura (2027+), il meccanismo di consultazione della comunità può essere rafforzato. Tuttavia la protezione dello standard curatoriale rimane permanente.

---

### 6.3 Utilità del token (Token Utility)

**Vantaggi forniti ai possessori del token $CULTURE:**

**1. Accesso prioritario agli eventi della galleria:**
- Inaugurazioni di mostre fisiche della Galleria İlhanArt
- Incontri con artisti e visite agli atelier
- Visualizzazioni di collezioni speciali

**2. Accesso completo al registro PoArt:**
- Registrazioni dettagliate di tutte le opere d'arte autenticate
- Versioni complete degli Evidence Pack
- Strumenti di verifica forense

**3. Voto consultivo:**
- Diritto di consultazione sulle candidature PoArt Verified
- Accesso ai canali di feedback della comunità
- Partecipazione alle discussioni di governance

**4. Contenuti esclusivi:**
- Contenuti dietro le quinte dello studio
- Interviste agli artisti e video del processo
- Accesso alla documentazione tecnica

**Nota:**  
I possessori di token danno voti consultivi (Advisory Vote). La decisione finale spetta al team curatoriale. Questa struttura è preferita per prevenire la manipolazione delle balene e gli attacchi speculativi. Non ci sono ricompense di staking perché cerchiamo partecipanti culturali a lungo termine, non capitale mercenario a breve termine.

---

### 6.4 Sincronizzazione dei metadati (Metadata Sync)

- **Sincronizzazione dei metadati:** I dati tecnici nel registro devono corrispondere al 100% con l'entità fisica.

**Definire tecnicamente la "corrispondenza al 100%" (chiarezza raccomandata):**

- **Corrispondenza minima (obbligatoria):**
  - `asset.fingerprints.sha256/sha512` nel registro deve essere **esattamente uguale** all'hash del file in possesso.
  - Quando `proof.notary_seal` nel registro viene riprodotto (se esiste l'Evidence Pack) deve essere **esattamente uguale**.

- **Corrispondenza del riferimento fisico (tipo di prova):**
  - Le prove come l'opera fisica + riferimento data/blocco mostrate in diretta devono essere coerenti con l'Evidence Pack.

- **Conformità alla privacy:**
  - In visibilità `masked`, campi come IP/posizione vengono pubblicati **in conformità con lo standard di mascheramento**.

---

### 6.5 Contestazione, revisione e revoca (Dispute & Revocation)

Il registro non è solo un meccanismo di "approvazione"; è un **meccanismo di supervisione vivente contro la contraffazione**.

- Quando viene avviata una contestazione, la registrazione può essere messa in modalità **"review"** (revisione).
- Se viene rilevata una contraffazione, viene contrassegnata come `status: void` e viene aggiunta la motivazione:
  - `void_reason` (uso di AI / plagio / manipolazione ecc.)
  - `revoked_at` (tempo di revoca)
- La fonte della decisione di revoca è chiaramente visibile nel registro:
  - revisione curatoriale / contestazione della comunità / nota di analisi forense (a seconda di quale viene applicata)

> **Questa parte è l'equivalente nel registro del concetto VOID dalla sezione "Red Flag Protocol".**

---

### 6.6 Esempio di registrazione del registro (Leggibile dalla macchina)
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

> *Nota: `asset.fingerprints.sha512` e altri valori hash sono abbreviati a scopo dimostrativo; nell'applicazione reale viene utilizzata una stringa di caratteri esadecimali di lunghezza completa.*

---

## 7) 🔐 SIGILLO TECNICO (NOTARY SEAL)

**Algoritmo di sigillo incrollabile prodotto da PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Protocollo di notaio digitale e prova forense [PoArt] (Beta v1.0)

> **"La cultura è più grande del capitale. Proteggi le tue opere da oggi, portale nel domani."**

---

## Perché pubblico?

La vera sicurezza viene dalla trasparenza. Grazie al nostro sistema **Registro pubblico (Public Registry)**, una persona in qualsiasi parte del mondo può verificare in pochi secondi se il file che ha è originale, senza bisogno di alcuna autorità.

---

## 🧩 Perché esistono più "moduli di visibilità"?

Questa è la parte più critica del codice (menu di selezione della visibilità). Queste opzioni consentono agli utenti di stabilire l'equilibrio **"Privacy vs Trasparenza"**:

### 🔒 Privato (Private)

- **Scenario:** L'artista non vuole ancora pubblicare l'opera ma vuole mettere un timestamp e dimostrare "l'ho fatto in questa data".
- **Cosa fa il codice:** Scrive i dati nel database ma applica l'etichetta `visibility: "private"`. In futuro quando si scrive la politica "Public Read" si possono nascondere queste registrazioni dal pubblico dicendo `WHERE visibility = 'public'`.

### 🕶️ Mascherato (Masked)

- **Scenario:** L'artista vuole trasparenza ma ha paura che venga trovato il suo indirizzo di casa (posizione IP).
- **Cosa fa il codice:** Sul lato JavaScript funzionano le funzioni `maskIP` e `maskLoc`. Converte l'indirizzo IP nella forma `88.241.***.***`, la posizione nella forma `***/TR` e invia al database la versione censurata.
- **Nota sulla privacy:** Il mascheramento viene effettuato nel browser, Supabase non vede la posizione reale. **Tuttavia:** Se vengono utilizzate API di terze parti come ipapi.co per i dati sulla posizione, questi fornitori vedono l'indirizzo IP al momento della richiesta.
- **Sigillatura in modalità mascherata:** Il calcolo di EvidenceRoot e NotarySeal viene effettuato con dati forensi mascherati; in questo modo la verifica rimane deterministica.

### 🌍 Pubblico (Public)

- **Scenario:** Trasparenza completa. Secondo lo standard [PoArt], viene dichiarato chiaramente dove, quando, da quale rete è stata prodotta l'opera.

---

## 💡 Innovazione tecnologica

PoArt non è solo un sistema di caricamento file. È un motore **"Catena di custodia forense" (Forensic Chain of Custody)** che fonde tre diversi livelli tecnologici in un'unica pentola e introduce un nuovo standard.

**Il livello spiegato come "motore" in questa sezione corrisponde al nucleo di PoArt Forensic Engine (PFE) nella terminologia precedente.**

### 1) Hashing lato client (Massima privacy)

I file delle vostre opere non vengono mai caricati sul server. Il nostro motore basato su browser (lato client) calcola l'hash (riepilogo digitale) del file sul proprio computer. Al server vengono inviati solo questa impronta digitale e i metadati.

> **Nota sulla privacy:** Il file dell'opera non viene caricato sul server e viene quindi protetto. Tuttavia i dati forensi (IP/posizione) vengono condivisi secondo la modalità di visibilità selezionata (private/masked/public).

### 2) Fusione di dati forensi (Forza forense)

È molto più di un semplice timestamp. Il sistema combina questi dati in un unico "Sigillo Genesi":

- **Riepilogo digitale (SHA-512):** Impronta digitale che verrà danneggiata anche se cambia un singolo pixel dell'opera, utilizzando lo standard di riepilogo crittografico (SHA-512).
- **Posizione e tempo:** Data con precisione al millisecondo dell'operazione, paese, città e distretto.
- **Identità del dispositivo:** Sistema operativo, browser e tipo di dispositivo (analisi User-Agent).

---

## 🛡️ Aree di utilizzo e vantaggi

Se sei un artista, scrittore o designer, non basta dire "L'ho fatto prima", devi dimostrarlo.

**Un'opera che sigilli con PoArt:**

- **Prova matematica:** Anche se cambia un singolo pixel del file, il sistema lo capisce. La manipolazione è impossibile.
- **Base legale:** È registrato in quale data, in quale città, da quale dispositivo è stata sigillata l'opera.
- **Certificato istantaneo:** Genera in pochi secondi un **"Certificato di identità dell'asset"** personalizzato, con codice QR e sigillato.

---

## ⚙️ Architettura del sistema e caratteristiche tecniche

Il sistema è progettato su un'architettura "Serverless" (senza server), orientata alle alte prestazioni e alla scalabilità.

| Livello | Tecnologia | Descrizione |
|---------|------------|-------------|
| **Crittografia** | SHA-256 & SHA-512 | Riepilogo crittografico a doppio strato |
| **Database** | Supabase (PostgreSQL) | Struttura dati JSONB, politiche RLS |
| **Dati forensi** | ipapi.co API | Triade IP/Posizione/Tempo |
| **Rendering** | html2canvas + jsPDF | Generazione PNG/PDF lato client |
| **Frontend** | Vanilla JavaScript | Zero dipendenze da framework |
| **Sicurezza** | Hashing lato client | Il file non viene mai caricato sul server |

### Caratteristiche distintive

| Caratteristica | Dettagli | Nei concorrenti? |
|----------------|----------|------------------|
| **Drag & Drop UI** | Trascina e rilascia file, anteprima istantanea | ❌ Assente nella maggior parte |
| **Esportazione multi-formato** | PNG, JSON, PDF - con un clic | ⚠️ Limitato |
| **Anteprima in tempo reale** | Anteprima del certificato dal vivo | ❌ Assente |
| **Controlli sulla privacy** | Opzioni Private/Masked/Public | ❌ Assente |
| **Hashing lato client** | Il file non va mai al server | ✅ Solo in alcuni |
| **Metadati forensi** | IP, posizione, dispositivo, tempo - tutto insieme | ❌ Frammentario |
| **Verifica QR** | Codice QR di verifica istantaneo | ⚠️ Limitato |
| **Limitazione della frequenza** | Protezione spam (RLS + Client) | ❌ Assente nella maggior parte |

---

## 🗺️ Roadmap: Futuro "senza fiducia"

La versione attuale **(Beta v1.0)** è ottimizzata per fornire all'utente finale massima velocità, interfaccia semplice e accesso gratuito. Tuttavia la nostra visione finale è passare a una struttura in cui nemmeno l'amministratore del database (noi) può intervenire.

### Fase 1: Beta v1.0 (Attualmente online)

**Infrastruttura:**
- Database cloud (Supabase)
- Registro off-chain (PostgreSQL + backup IPFS)
- Auto-attestazione della galleria (centralizzata ma trasparente)

**Token:**
- Piattaforma: Pump.fun
- Liquidità: Raydium (automatico)
- Governance: Solo consultiva (consultazione della comunità)

**Obiettivo:**
- Velocità, rimozione delle barriere UX
- Fornire sicurezza "senza attrito"
- Costruzione della comunità

**Utilità del token (v1.0):**
- Accesso prioritario agli eventi della galleria
- Visualizzazione del registro PoArt
- Diritto di voto consultivo

---

### 🚀 Fase 2: Autorità decentralizzata (2026 Q2-Q4)

Questa fase copre la transizione del sistema da una struttura completamente funzionante "lato client" a una struttura più sicura e decentralizzata.

| Caratteristica | Cosa porta? | Stack tecnologico | ETA |
|----------------|-------------|-------------------|-----|
| **Edge Function INSERT** | Blocco spam + sicurezza chiave API | Supabase Edge (Deno) | Q2 2026 |
| **Firma del portafoglio** | Identità decentralizzata | Solana Wallet Adapter | Q2 2026 |
| **Backup IPFS/Arweave** | Archivio decentralizzato | IPFS SDK + Pinata | Q3 2026 |
| **Meccanismo di revoca** | Annullamento certificato falso | Aggiornamento schema DB | Q2 2026 |
| **Registro di audit** | Registrazione query forensi | Tabella log personalizzata | Q3 2026 |
| **OpenTimestamps** | Ancoraggio Bitcoin | OTS JavaScript | Q4 2026 |

**Governance del token (v2.0):**
- Voto off-chain (x/web) + firma del portafoglio
- Selezione dei rappresentanti della comunità (primi 90 giorni)
- Controllo del portafoglio delle operazioni multi-sig
- Voto consultivo ponderato (con limite per le balene)

**Immutabilità:**
- Backup del registro con hash IPFS
- Ancoraggio timestamp Bitcoin
- Preparazione per la verifica cross-chain

---

### Fase 3: Decentralizzazione completa (2027+)

| Caratteristica | Obiettivo | ETA |
|----------------|-----------|-----|
| **Registro on-chain** | Registrazione on-chain Solana | Q1 2027 |
| **Supporto multi-catena** | Ethereum, Polygon, Base | Q2 2027 |
| **Integrazione DID** | Identità decentralizzata | Q3 2027 |
| **Governance della comunità** | Sistema consultivo rafforzato | Q4 2027 |
| **Riconoscimento legale** | Validità nei tribunali turchi | 2027-2028 |
| **API per sviluppatori** | Endpoint API pubblico | Q3 2027 |

**Evoluzione della governance:**
- v3.0: Modello ibrido (curatoriale + ponderato dalla comunità)
- 2028+: Governance completa della comunità (opzionale)
- Il controllo di qualità curatoriale viene sempre mantenuto

---

## 🧬 Struttura dati del protocollo (Schema JSON)

**Ogni certificato [PoArt] ha una carta d'identità JSON portatile e verificabile prodotta nello standard seguente.**

> **Nota:** Questo formato Identity JSON è il formato del certificato presentato all'utente. Nelle registrazioni del registro viene utilizzato `registry.asset` invece di `identity.asset_data` (mappatura: `identity.asset_data` == `registry.asset`).
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

## 🔬 Profondità tecnica: Algoritmo del sigillo

### Funzioni hash deterministiche
```javascript
// Funzioni ausiliarie: Convertire digest in stringa esadecimale
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Convertire stringa in array di byte
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Generazione stringa forense canonica (v1.0: ordine fisso dei campi + UTF-8 + delimitatore \n)
// Nota fase 2: Passaggio a JSON canonico con RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Processo di generazione NotarySeal (Completamente deterministico)
```javascript
// 1. Calcolo FileHash (lato client)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Raccolta dati forensi (utilizzo di un singolo timestamp)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Generazione di un singolo timestamp
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Stesso timestamp
  };
  
  return { forensics, timestamp };
}

// 3. Creazione EvidenceRoot (con codifica canonica)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Generazione NotarySeal (utilizzo dello stesso timestamp)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Funzioni ausiliarie di mascheramento (supporto IPv4 e IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Controllo IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 o formato sconosciuto
  return "***";
}
```

### Flusso di verifica (Due livelli)

#### Verifica rapida (Quick Verify)
```javascript
// Controlla solo l'hash del file (bandiera rossa rapida)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Recupera dal registro
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Confronto hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Originale - L'hash del file corrisponde"
    };
  } else {
    return {
      valid: false,
      message: "❌ Falso - Il file è stato manipolato"
    };
  }
}
```

#### Verifica completa (Full Verify)
```javascript
// Rigenera e verifica EvidenceRoot e NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Recupera dal registro
  const cert = await fetchFromRegistry(certificateId);

  // 1) Controllo FileHash (bandiera rossa rapida)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Falso - L'hash del file non corrisponde" };
  }

  // 2) Rigenera EvidenceRoot (con i dati forensi memorizzati nel registro)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Non corrisponde - EvidenceRoot non valido" };
  }

  // 3) Rigenera NotarySeal (con lo stesso timestamp + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Non corrisponde - NotarySeal non valido" };
  }

  // Opzionale: Nella fase 2 verificare anche signer_sig con attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Firma non valida" };

  return { valid: true, message: "✅ Originale - Full Verify superata" };
}
```

> **Note importanti:**
> - **Quick Verify:** Controlla solo l'hash del file per un uso rapido.
> - **Full Verify:** Verifica tutti i livelli del protocollo (EvidenceRoot + NotarySeal).
> - Tutte le operazioni di hash vengono eseguite in modo deterministico, con codifica fissa e delimitatori.
> - **Standard di canonizzazione v1.0:** Ordine fisso dei campi + codifica UTF-8 + delimitatore `\n`.
> - **Piano fase 2:** Passaggio a JSON canonico con RFC 8785 (JCS - JSON Canonicalization Scheme).
> - In modalità mascherata, il calcolo di EvidenceRoot e NotarySeal viene effettuato con dati forensi mascherati.
> - Un singolo timestamp viene utilizzato in tutto il processo (forensica + NotarySeal); il determinismo è garantito.
> - **Nomi dei campi forensi:** `ip_masked`, `location`, `device`, `timestamp` (codice e registro completamente compatibili).
> - **Percorso del registro:** `certificate.asset.fingerprints` (completamente compatibile con il codice di verifica).
> - **signer_sig nel registro:** Il campo `proof.signer_sig` è necessario per Full Verify.
> - Il meccanismo SignerSignature sarà attivato nella fase 2 con Solana Wallet Adapter; in v1.0 è possibile la verifica con `attestation_pubkey`.

---

## 📊 Analisi competitiva (Aggiornata)

PoArt è posizionato sul "Sweet Spot" (punto ottimale) che completa le lacune delle soluzioni esistenti.

| Caratteristica | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 証 Proof | Trust-Stamp |
|----------------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Costo** | 🆓 Gratuito | 🆓 | 💰 A pagamento | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Molto facile | ❌ CLI | ⚠️ Medio | ⚠️ Medio | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Esportazione multi-formato** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Anteprima in tempo reale** | ✅ Dal vivo | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Controlli sulla privacy** | ✅ 3 modalità | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Hash lato client** | ✅ Privacy | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Metadati forensi** | ✅ Completi | ❌ | ❌ | ⚠️ Limitati | ❌ | ⚠️ | ❌ | ⚠️ |
| **Verifica QR** | ✅ Istantanea | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Limitazione di frequenza** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Ancoraggio blockchain** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Supporto italiano** | ✅ Nativo | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Spiegazione:**
- ✅ : Supporto completo / disponibile
- ⚠️ : Limitato / nei piani a pagamento
- ❌ : Assente / non supportato
- 🔄 : Nella roadmap (in sviluppo)
- 🆓 : Completamente gratuito
- 💰 : A pagamento / abbonamento richiesto

### Lacune dei concorrenti, punti di forza di PoArt

| Lacuna | Concorrenti | PoArt |
|--------|-------------|-------|
| **Difficoltà d'uso** | CLI, conoscenza API, portafoglio necessario | Trascina e rilascia, finito in 3 clic |
| **Barriera di costo** | Abbonamento $50-500/mese | 100% gratuito |
| **Privacy** | File caricato sul server | Lato client, il file non va mai via |
| **Dati forensi** | Solo timestamp | IP, posizione, dispositivo, tempo - tutto |
| **Supporto italiano** | Assente o molto limitato | Supporto linguistico nativo |
| **Open source** | Scatola chiusa | Tutto il codice aperto su GitHub |

---

## 📈 Statistiche di utilizzo (Obiettivi Q1 2026)

| Metrica | Obiettivo | Stato |
|---------|-----------|-------|
| **Certificati totali** | 1.000 | 🔄 In corso |
| **Utenti attivi** | 500 | 🔄 In corso |
| **Numero di verifiche** | 5.000 | 🔄 In corso |
| **Tempo di attività** | 99,9% | ✅ Attivo |
| **Tempo di risposta medio** | <200ms | ✅ Ottimale |

---

## 🌍 Comunità e supporto

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Contributori

Il protocollo PoArt continua a svilupparsi con i contributi della comunità open source.

**Per contribuire:**
1. Fare fork
2. Creare branch delle funzionalità (`git checkout -b feature/amazing-feature`)
3. Fare commit (`git commit -m 'Add amazing feature'`)
4. Fare push (`git push origin feature/amazing-feature`)
5. Aprire Pull Request

### 🛠️ Di cosa abbiamo bisogno ora? (Richiesta di aiuto)

Attendiamo i contributi di sviluppatori esperti nei seguenti argomenti per gli sviluppi della **Fase 2** del protocollo PoArt:

* **Supabase Edge Functions:** Spostare la protezione spam lato server.
* **Solana Web3.js:** Integrazione della firma del portafoglio (Wallet Signing).
* **IPFS / Arweave:** Integrazione di servizi di archiviazione e pinning.
* **Strumenti della comunità:**  sistemi di voto, dashboard di analisi.

> Si prega di avviare una discussione nella scheda "Issues" prima di aggiungere una funzionalità.

---

## 💬 Note finali

### Pump.fun e realtà

Questo progetto è stato lanciato su Pump.fun perché:
- ✅ Accesso alla liquidità (migrazione automatica Raydium)
- ✅ Accesso alla comunità esistente
- ✅ Costo iniziale basso

Tuttavia chiariamo questo:
- **Il prezzo del token** non è un indicatore di successo artistico
- Il valore del token è importante per il **budget operativo** (galleria, mostre, infrastruttura)
- **Metriche di successo:** Opere autenticate + coinvolgimento della comunità + visitatori fisici

### Governance e decentralizzazione

**Realtà v1.0 (2026):**
- Registro: Off-chain (PostgreSQL + backup IPFS)
- Attestazione: Auto-firmata dalla galleria (centralizzata ma trasparente)
- Governance: Solo consultiva (decisione finale curatoriale)

**Visione v2.0+ (2027+):**
- Registro: On-chain (Solana)
- Firme: Basate su portafoglio (decentralizzate)
- Governance: Ibrida (consultiva della comunità + qualità curatoriale)
- Utilità del token: Funzionalità avanzate + accesso ampliato

Questa struttura fornisce **efficienza operativa** e **controllo di qualità** nella fase iniziale, lasciando aperta la strada per aumentare la **partecipazione della comunità** in futuro.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // La cultura è più grande del capitale*

## 🧾 Licenza

MIT License © 2026 İlhan Art Gallery Initiative

Vedere [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) per i termini completi.

---
