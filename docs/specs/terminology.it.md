# 📚 GLOSSARIO DI TERMINOLOGIA E CONCETTI
> **"Comprendere il linguaggio di questo protocollo significa comprenderne la visione."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Infrastruttura Centrale

**PoArt Forensic Engine (PFE)** è il livello principale che rappresenta la logica fondamentale e il funzionamento tecnico alla base del protocollo [PoArt]. Questo è il "motore forense" che trasforma i dati grezzi di produzione di un'opera d'arte in una **prova digitale** verificabile e immutabile.

### 🧩 Perché "PoArt Forensic"?

- **PoArt (Proof of Art):** Il focus del motore è legare il valore di un asset digitale non alla speculazione, ma al **processo di produzione dimostrabile**.
- **Forensic (Verifica Forense):**
  - **Definizione Tecnica:** Un approccio algoritmico e di chain-of-custody per verificare che i dati relativi al processo di produzione (pennellate, timelapse, log) non siano stati manipolati.
  - **Livello Filosofico:** Contro la "produzione istantanea" dell'intelligenza artificiale; l'affermazione di trasformare la produzione umana che contiene **tempo, sforzo e costo decisionale** in una realtà misurabile.

> Nota: L'integrazione blockchain (es. Solana) non è il nucleo del PFE; sarà definita separatamente come **Chain Anchor Layer** per la verifica/registro.

### 🛠️ Ambito Tecnico v1.0

**PoArt Forensic Engine (PFE) v1.0** è costruito su **3 pilastri principali** invece di modelli finanziari complessi:

1. **Hashing & Sealing (Sigillatura):**  
   Il PFE elabora in modo deterministico tutti gli elementi nell'Evidence Pack (file dell'opera, video, JSON/log, firma ecc.) e produce un valore univoco **NotarySeal**.

   **Concetti fondamentali (v1.0):**
   - **FileHash (impronta dell'opera):** Hash generato dai byte del file dell'opera.
   - **EvidenceRoot (radice del pacchetto di prove):** Il digest radice che rappresenta l'integrità dell'Evidence Pack (Merkle root o hash del manifest canonico).
   - **NotarySeal (sigillo finale / Output PFE):** Il sigillo finale generato dalla combinazione di EvidenceRoot + tempo + firma.

   **Formule (in formato chiaro per gli investitori):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Definizioni Canonical Payload (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Nota: Il valore inteso come output del PFE è **NotarySeal**. Il meccanismo **SignerSignature** sarà attivato nella Fase 2 (con Solana Wallet Adapter); nella v1.0 attuale viene utilizzata la firma di attestazione propria del sistema. La chiave pubblica di attestazione è pubblicata nel registro nel campo `issuer.attestation_pubkey`.

2. **Indexing (Archiviazione):**  
   Registra quale wallet, in quale data, ha presentato la **Labor Proof (Prova del Lavoro)** per quale opera; in uno strato di registro trasparente e interrogabile.  
   *(Questo livello può essere un database; l'integrazione blockchain è invece definita separatamente come "Chain Anchor Layer".)*

3. **Verification (Verifica):**  
   Quando viene interrogata l'originalità di un'opera, il PFE rielabora le prove grezze; testa con certezza matematica se i valori **EvidenceRoot / NotarySeal** calcolati corrispondono ai record nell'archivio.

---

### 🧮 Il Teorema del Valore PoArt (The Value Theorem)

Il protocollo [PoArt] collega il valore ($V$) di un asset digitale non con la percezione soggettiva del mercato, ma con **la realtà fisica del processo di produzione**.

L'Intelligenza Artificiale (AI) annulla il processo fornendo risultati istantanei ($t \to 0$). [PoArt] invece considera il valore come l'accumulo delle componenti di **tempo, lavoro e volontà**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definizione delle Variabili

- **$\int dt$ (Accumulo del Processo):**  
  Il valore non è un "output" istantaneo; è un **processo** che si accumula tra $t_{\text{start}}$ e $t_{\text{end}}$. Man mano che il tempo diminuisce (produzione AI), il risultato dell'integrale si avvicina a 0.

- **$P_{\text{labor}}(t)$ (Intensità Istantanea del Lavoro):**  
  Rappresenta l'intensità dello sforzo mentale e fisico speso nel momento della produzione. Man mano che lo sforzo dimostrabile aumenta, l'integrando cresce.  
  > Nota: Questo termine può essere normalizzato in pratica su "segnali di lavoro misurabili/dimostrabili".

- **$I_{\text{agency}}(t)$ (Coefficiente di Volontà):**  
  È la capacità del produttore di assumersi rischi e prendere decisioni. Assume un valore tra $0$ e $1$.
  - **AI ($I \approx 0$):** Esegue comandi, non si assume rischi, non paga costi.
  - **Umano ($I \to 1$):** Cambia decisioni, esita, si assume rischi.

- **$U_{\text{irreversible}}$ (Unicità Irreversibile):**  
  Mentre nella produzione digitale è possibile annullare (`Ctrl+Z`); nella produzione fisica (vernice applicata su tela, marmo scolpito, gesto durante una diretta) non c'è ritorno. Questa **irreversibilità** è un termine aggiuntivo che crea "unicità" (carattere non fungibile) nell'opera.

### 🔎 Analisi di Caso: AI "Output Istantaneo" vs. Umano "Processo Dimostrato"

Lo scenario seguente mostra come funziona il **Teorema del Valore PoArt** nella pratica e perché le produzioni AI ottengono punteggi bassi nello standard [PoArt].

#### Scenario A: Produzione Visuale con AI in 10 Secondi

- **Durata ($\Delta t$):** $10$ secondi (processo quasi inesistente)
- **Intensità del Lavoro ($P_{\text{labor}}$):** $1$ unità (solo scrittura del comando)
- **Coefficiente di Volontà ($I_{\text{agency}}$):** $0.01$ (nessun rischio, nessun costo)
- **Irreversibilità ($U_{\text{irreversible}}$):** $0$ (reversibile / copiabile)

**Risultato:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Commento:** Anche se l'output è perfetto; poiché il processo non è stato vissuto e non contiene volontà/rischio, il valore [PoArt] si avvicina a $0$.

#### Scenario B: Produzione Fisica in Diretta di 6 Ore

- **Durata ($\Delta t$):** $6$ ore ($21{,}600$ secondi)
- **Intensità del Lavoro ($P_{\text{labor}}$):** $0.5$ unità (continuità dello sforzo fisico e mentale)
- **Coefficiente di Volontà ($I_{\text{agency}}$):** $0.9$ (cambiamento di decisioni, assunzione di rischi, scelte irreversibili)
- **Irreversibilità ($U_{\text{irreversible}}$):** $>0$ (le tracce fisiche non possono essere annullate)

**Risultato:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Commento:** Man mano che il processo si allunga e la volontà (rischio) aumenta, il valore si accumula in modo cumulativo. Il termine $U_{\text{irreversible}}$ è un contributo aggiuntivo che crea "unicità" (carattere non fungibile) nell'opera.

---

### ✅ Conclusione: Valore Vincolato alla Prova (Proof-Bound Value)

Questo teorema rimuove l'affermazione di valore di [PoArt] dall'essere un "mi piace" o una "narrazione di mercato" e la lega a **una realtà di produzione dimostrabile**.

1. **Senza Processo Non Si Crea Valore:**  
   L'AI annulla il processo nell'output istantaneo ($t \to 0$). Man mano che la finestra del processo si restringe, il risultato dell'integrale diminuisce per necessità matematica:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **La Volontà e il Rischio Sono Moltiplicatori:**  
   [PoArt] misura non solo il "tempo speso", ma anche il reale livello di decisione, rischio e costo durante quel tempo. Il valore di una produzione che non si assume rischi (AI) è basso:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **L'Unicità È una Prova Fisica, Non Marketing:**  
   Nella produzione fisica, le tracce irreversibili (pennellata su tela, rottura del marmo) sono al di fuori della logica `Ctrl+Z` del digitale. Questa irreversibilità ($U_{\text{irreversible}}$) rende l'opera ontologicamente unica.

> **🔐 RIEPILOGO:** Anche se il teorema del valore può sembrare incerto come misurazione (anche se non può essere misurato al 100% nella vita reale), lo scopo di questa formula è mostrare la struttura e la direzione delle variabili. Ciò che è raro nell'era dell'AI non è l'"immagine", ma **il lavoro dimostrabile, il tempo e la volontà.** [PoArt] misura questa scarsità e la registra con l'**Evidence Pack**.

### 🏛️ L'Importanza del Concetto di "Engine" (Motore)

I token che emergono da piattaforme come Pump.fun sono spesso solo **"biglietti di accesso"**. **PoArt Forensic Engine (PFE)** è invece **il livello logico costituzionale** che determina quali diritti protegge quel biglietto, come viene registrato il lavoro e come l'arte/scienza/tecnologia viene resa permanente.

> **Nota:** Il motivo per cui abbiamo avviato questo progetto su Pumpfun è che non avevamo liquidità e follower sufficienti. Utilizzare i dati esistenti è stata strategicamente la mossa giusta, anche se non la più qualitativa. Definire la logica di questo motore su GitHub, indipendentemente dal budget e dalle risorse, dimostra che il progetto non è solo una speculazione finanziaria, ma una visione di **infrastruttura software** a lungo termine e una **biblioteca nazionale digitale**.

---

## 🎨 PROTOCOLLO [PoArt] PROOF OF ART (Proof of Art Protocol v1.0)

> **"Vero Artista, Vera Produzione, Vero Valore."**

Questo protocollo è un **meccanismo di difesa biologico e intellettuale** sviluppato contro truffatori anonimi che infestano l'ecosistema crypto, immagini di intelligenza artificiale prodotte in 5 minuti e la cultura del "Pump & Dump".

---

## a) Cos'è [PoArt]? (Definizione Filosofica e Tecnica)

**Proof of Art [PoArt];** è uno standard di verifica istituzionale che garantisce che il valore dietro un asset sulla blockchain si basi non sulla speculazione, ma sul **lavoro umano** verificabile, sul **tempo** e sull'**energia fisica**.

Proprio come Bitcoin produce valore con *"Elettricità e Potenza di Elaborazione"* **(Proof of Work)**; i progetti conformi a [PoArt] producono valore con *"Abilità Artistica e Tempo Umano"*.

Elimina il rischio di *"Lo sviluppatore (Dev) ha venduto, il progetto è finito"* presente su Pump.fun e piattaforme DEX; perché qui il valore non è nel codice, ma nella **continuità della produzione**.

> **[PoArt] non dice al partecipante "Fidati di noi"; dice "Ecco le prove, guarda con i tuoi occhi, verifica con la tua matematica".**

---

## b) Lo Standard a 5 Pilastri [PoArt] (The 5 Pillars of Truth)

Questi 5 punti sono filtri inmanipola bili che un progetto deve superare per ottenere il sigillo [PoArt].

### 1) Prova di Identità dal Vivo (Live Identity Proof)

- **Problema:** Il mondo crypto è pieno di fondatori anonimi (Dev) di identità incerta che raccolgono denaro e abbandonano il progetto.
- **Soluzione [PoArt]:** Il produttore dimostra non solo la carta d'identità, ma **la sua presenza durante la produzione**. Ciò include sessioni di live streaming in cui si interagisce con la comunità e si soddisfano richieste specifiche istantanee, non con video preregistrati.  
  (Es: *"Scrivi la data di oggi e il numero di blocco corrente nell'angolo destro della tela"*)
- **Motto:** *"I bot possono fare disegni, ma i bot non sudano e non improvvisano."*

### 2) Prova di Lavoro e Processo (Labor & Process Proof)

- **Problema:** Immagini AI prodotte in 2 secondi e dipinti a olio realizzati in 2 mesi vengono trattati come lo stesso "jpeg" nel mondo digitale.
- **Soluzione [PoArt]:** Il processo di "gravidanza e nascita" dell'opera viene registrato. Fasi di schizzo, strati di vernice, ore cumulative spese e il processo fisico vissuto dall'artista durante la creazione dell'opera vengono documentati. Ciò aggiunge un **"Costo Temporale" (Time Cost)** al token. Più è difficile produrre un asset, più solido è il suo valore.

### 3) Prova del Valore Estetico (Aesthetic Value Proof)

- **Problema:** L'estetica e la profondità artistica della cultura "Meme" che ignora tutto e si concentra solo sulla commedia istantanea, e i progetti "Hype" di breve durata che ne derivano.
- **Soluzione [PoArt]:** Il progetto deve avere standard artistici accademici, teoria del colore, regole di composizione e conoscenza dei materiali (Impasto, Texture ecc.). Il contenuto non deve solo far ridere; deve suscitare ammirazione nello spettatore e avere **valore da collezione**.

### 4) Innovazione Concettuale (Conceptual Novelty)

- **Problema:** Migliaia di dog/cat coin identiche, lontane dalla creatività.
- **Soluzione [PoArt]:** Il progetto deve costruire un nuovo ponte che combini in modo significativo arte, scienza, filosofia o tecnologia.  
  (Es: Combinare la classica statua di Davide con i dati di mercato crypto; elaborare attraverso questo l'idea della "pietrificazione" della percezione umana e poterlo fondare con fonti scientifiche.)  
  L'opera deve essere non solo una festa visiva, ma anche una sfida intellettuale che fa riflettere su **Scienza, Filosofia o Tecnologia**.

> [!IMPORTANT]
> **Esempio di Riferimento (Effetto Las Palmitas):** Nel quartiere di Las Palmitas in Messico, alle prese con il crimine, oltre 200 case sono state trasformate in una festa arcobaleno gigante. A seguito di questo >intervento estetico, i tassi di criminalità nel quartiere sono diminuiti in una certa misura, i giovani hanno iniziato a interessarsi all'arte invece che alle gang. Il cambiamento estetico ha ricodificato il rispetto delle persone per l'ambiente e gli uni per gli altri (Coesione Sociale).
>
> **Aspettativa:** Un progetto che entrerà nella lista [PoArt]; proprio come nell'esempio sopra, deve contenere una relazione causa-effetto sociologica, scientifica o filosofica oltre l'estetica visiva. Poiché l'unica cosa che non può essere acquistata con denaro è il "Tempo", in questo protocollo il tempo deve essere dimostrato come >garanzia attraverso lo staking. La base concettuale del progetto deve essere così forte e universale che; anche in uno scenario di possibile CTO (Community Take Over) anni dopo, la comunità può sostenere autonomamente il potenziale innovativo del progetto ereditando questa eredità.

### 5) Volontà Non-Algoritmica (Non-Algorithmic Agency)

- **Problema:** Produzioni digitali perfette ma senza anima, che si ripetono.
- **Soluzione [PoArt]:** La volontà originale dell'essere umano, che può commettere errori, assumersi rischi e sperimentare fluttuazioni emotive, deve essere percepita nell'opera. L'incertezza nelle pennellate, le reazioni inaspettate del materiale e le decisioni istantanee dell'artista sono la **Firma Biologica** che distingue l'opera dalla "Produzione Meccanica".

---

## c) Meccanismo di Verifica e Anti-Contraffazione

Questo sistema garantisce che il progetto rimanga affidabile e vivo non solo "all'inizio", ma "per sempre".

### 📦 Pacchetto di Prove (Evidence Pack - The Digital Twin)

Dietro ogni opera certificata [PoArt] c'è un pacchetto di dati crittografato e timestampato che gli investitori possono scaricare:

- **Registrazioni Video RAW:** Filmati grezzi ininterrotti del momento di produzione.
- **Analisi Metadata:** Data di creazione del file, informazioni sul dispositivo utilizzato e dati di posizione.
- **Riferimenti Fisici:** Prove che l'opera esiste nel mondo fisico  
  (Es: Giornale corrente o dati blockchain attuali accanto all'opera).

> *Nota di coerenza:* L'espressione "pacchetto di prove" si collega alla linea **Evidence Pack → EvidenceRoot → NotarySeal** delle sezioni precedenti; cioè, l'integrità del pacchetto è rappresentata da un sigillo verificabile.

### 🔄 Rinnovo a 365 Giorni (The Sustainability Protocol)

- **Caratteristica Rivoluzionaria:** Nei progetti crypto, il "Dev" (Sviluppatore) lancia il token sul mercato e generalmente scompare dopo 1-2 mesi (Soft Rug). [PoArt] lo rende impossibile.
- **Regola:** Lo status di "Verified Artist" (Artista Verificato) non è per tutta la vita. È valido solo per **1 anno**.
- **Funzionamento:** L'artista/sviluppatore deve presentare alla comunità **una nuova, grande e dimostrabile opera** ogni 365 giorni.
- **Scenario di Esempio:** Avete avviato il progetto nel 2026. A gennaio 2027 il sistema emette un avviso "Periodo di Prova Scaduto". Se l'artista non presenta una nuova mostra, una nuova opera fisica o una nuova integrazione tecnologica, il "Badge di Fiducia" del progetto viene abbassato.
- **Risultato:** Questo sistema garantisce che **il contenuto non perda mai attualità** e che l'investitore non viva la paura di *"Lo sviluppatore è ancora qui?"*. Il progetto diventa uno studio vivente.

### 🚩 Bandiera Rossa (Red Flag Protocol)

**In caso di qualsiasi contraffazione rilevata dalla comunità o dagli algoritmi (uso di AI, opera rubata, video manipolato):**

1. Il certificato viene immediatamente contrassegnato come **"ANNULLATO" (VOID)**.
2. I pacchetti di prove vengono pubblicamente etichettati come **"Falsi"**.
3. Il progetto viene inserito nella blacklist [PoArt]. Ciò rafforza il fatto che in un mondo decentralizzato **la reputazione è l'unica valuta**.

---

## d) Conclusione: Non un Casinò, un Museo

**Pump.fun e gli Exchange Decentralizzati (DEX) sono purtroppo ora casinò; le luci lampeggiano, tutti cercano guadagni rapidi e la casa (i truffatori) vince sempre. Il motivo per cui abbiamo avviato il progetto qui è la mancanza di budget sufficiente e l'avere un pubblico esistente raggiungibile tramite live streaming.**

**[PoArt] è una fortezza costruita nel mezzo di questo casinò.**

- 🎰 Il casinò si basa su giochi di carte; noi ci basiamo sulla **realtà fisica**.
- 🃏 Il casinò è aperto all'inganno; noi siamo aperti a **prove trasparenti**.
- ⏳ Il casinò è temporaneo; noi ci concentriamo sull'**eternità dell'arte e della scienza**.

**Il token che utilizza questo protocollo non è solo una "coin"; è un titolo digitale che contiene sudore, vernice, codice e filosofia.**

---

## 🗳️ 6) GOVERNANCE E REGISTRO PUBBLICO (Governance & Public Registry)

**Lo scopo di questa sezione è: rimuovere lo standard [PoArt] dalla sfera della "fiducia nelle persone" e trasformarlo in un'infrastruttura pubblica sostenibile con registro + verifica + supervisione della comunità.**

### 6.1 Registro Pubblico (Public Registry)

- **Public Registry:** Tutti i dati approvati sono registrati all'indirizzo `ilhanart.org/registry` (o GitHub Registry).

**Logica di registrazione (standard consigliato - formato path JSON):**

Ogni record che entra nel registro porta almeno questi campi fondamentali verificabili:

- **Identità e Stato:**
  - `certificate_id` (riferimento leggibile)
  - `status` (active / void)
  - `void_reason` (se presente)
  - `visibility` (private / masked / public)
  - `created_at` (timestamp)

- **Istituzione Emittente:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informazioni sull'Opera:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (se possibile; per identità token-gated)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Dati Forensi:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Prove Crittografiche:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Governance:**
  - `governance.decision`
  - `governance.veto_threshold`

Il registro può avere due livelli:
- **1)** Indice leggibile dall'uomo (elenco web / ricerca / filtro)
- **2)** Manifest leggibile dalla macchina (record JSON; per verifica PFE)

**Qui la "registrazione" diventa verificabile con la catena Evidence Pack → EvidenceRoot → NotarySeal del PFE. Il registro fornisce un obiettivo di verifica, non un'"affermazione".**

---

### 6.2 Veto della Comunità al 40% (Token-Gated Governance)

- **Veto della Comunità al 40%:** La votazione inizia un mese prima dell'acquisizione dello status; l'obiezione del 40% della comunità **Token-Gated (Solana-Verified)** invalida la domanda.

**Flusso di votazione (processo netto consigliato):**
- **Finestra di candidatura:** Il progetto candidato apre una "registrazione candidata PoArt" (le registrazioni candidate appaiono con stato "pending").
- **Periodo di revisione:** Per 30 giorni la comunità esamina le prove (Evidence Pack + registrazioni live streaming + metadata).
- **Verifica token-gated:** La votazione viene effettuata con wallet verificati su Solana (es. proprietà di specifici token/NFT + firma wallet).
- **Regola del veto:** Se il 40% dei voti è **obiezione (NO / VETO)**, la domanda viene rifiutata.
- **Trasparenza:** Il risultato della votazione viene memorizzato nel registro come "decision record" (data, rapporto, ID snapshot).

---

### 6.3 Sincronizzazione Metadata (Corrispondenza con il Mondo Fisico)

- **Metadata Sync:** I dati tecnici nel registro devono corrispondere al 100% con l'asset fisico.

**Definire tecnicamente "corrispondenza al 100%" (chiarezza consigliata):**
- **Corrispondenza minima (obbligatoria):**
  - L'`asset.fingerprints.sha256/sha512` nel registro deve essere **esattamente identico** all'hash del file in mano.
  - Il `proof.notary_seal` nel registro, quando riprodotto (se è presente Evidence Pack), deve essere **esattamente identico**.
- **Corrispondenza del riferimento fisico (tipo di prova):**
  - Le prove come l'opera fisica mostrata in live streaming + riferimento data/blocco devono essere coerenti con l'Evidence Pack.
- **Conformità alla privacy:**
  - I campi come IP/posizione nella visibilità `masked` vengono pubblicati **conformemente allo standard di mascheramento**.

---

### 6.4 Obiezione, Revisione e Annullamento (Dispute & Revocation)

Il registro non è solo un meccanismo di "approvazione"; è un **meccanismo di supervisione vivente contro la contraffazione**.

- Quando viene avviata un'obiezione, il record può essere messo in modalità **"review"**.
- Se viene rilevata contraffazione, viene contrassegnato come `status: void` e viene aggiunto un motivo:
  - `void_reason` (uso di AI / plagio / manipolazione ecc.)
  - `revoked_at` (momento dell'annullamento)
- La fonte della decisione di annullamento è chiaramente visibile nel registro:
  - votazione della comunità / consiglio autorizzato / nota di indagine forense (a seconda di quale si applica)

> **Questa sezione è la controparte nel registro del concetto VOID nella sezione "Red Flag Protocol".**

---

### 6.5 Esempio di Record nel Registro (Leggibile dalla Macchina)
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
    "title": "Senza titolo",
    "creator": "Anonimo",
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
> *Nota: `asset.fingerprints.sha512` e altri valori hash sono abbreviati a scopo dimostrativo; nell'applicazione reale viene utilizzata una stringa di caratteri esadecimali di lunghezza completa.*

---

## 7) 🔐 SIGILLO TECNICO (NOTARY SEAL)

**PoArt Forensic Engine (PFE) v1.0** algoritmo di sigillatura incrollabile prodotto da:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Protocollo [PoArt] Notaio Digitale e Prova Forense (Beta v1.0)

> **"La Cultura è più grande del Capitale. Proteggi le tue opere oggi, portale nel domani."**

---

## Perché Pubblico?

La vera sicurezza viene dalla trasparenza. Grazie al nostro sistema **Public Registry (Registro Pubblico)**, una persona in qualsiasi parte del mondo può verificare in pochi secondi se il file che ha in mano è originale, senza la necessità di alcuna autorità.

---

## 🧩 Perché Ci Sono Più "Moduli di Visibilità"?

La parte più critica del codice è qui (menu di selezione della visibilità). Queste opzioni consentono agli utenti di bilanciare **"Privacy vs. Trasparenza"**:

### 🔒 Privato (Private)

- **Scenario:** L'artista non vuole ancora pubblicare l'opera ma vuole apporre un timestamp e dimostrare "l'ho fatta in questa data".
- **Cosa Fa il Codice:** Scrive i dati nel database ma applica il tag `visibility: "private"`. In futuro, quando si scrive la politica "Public Read", è possibile nascondere questi record al pubblico dicendo `WHERE visibility = 'public'`.

### 🕶️ Mascherato (Masked)

- **Scenario:** L'artista vuole trasparenza ma ha paura che venga trovato l'indirizzo di casa (posizione IP).
- **Cosa Fa il Codice:** Sul lato JavaScript funzionano le funzioni `maskIP` e `maskLoc`. Converte l'indirizzo IP in formato `88.241.***.***` e la posizione in formato `***/TR` e invia la versione censurata al database.
- **Nota sulla Privacy:** Il mascheramento avviene nel browser, Supabase non vede la posizione reale. **Tuttavia:** Se vengono utilizzate API di terze parti come ipapi.co per i dati di posizione, questi provider vedono l'indirizzo IP al momento della richiesta.
- **Sigillatura in Modalità Masked:** Il calcolo di EvidenceRoot e NotarySeal viene effettuato con dati forensics mascherati; in questo modo la verifica rimane deterministica.

### 🌍 Pubblico (Public)

- **Scenario:** Piena trasparenza. Secondo lo standard [PoArt], dove, quando e da quale rete è stata prodotta l'opera è dichiarato apertamente.

---

## 💡 Innovazione Tecnologica

PoArt non è solo un sistema di caricamento file. È un motore **"Forensic Chain of Custody"** che fonde tre diversi livelli tecnologici in un unico crogiolo e porta un nuovo standard.

**Il livello descritto in questa sezione come "motore" corrisponde al nucleo PoArt Forensic Engine (PFE) nella terminologia precedente.**

### 1) Client-Side Hashing (Massima Privacy)

I file delle vostre opere non vengono mai caricati sul server. Il nostro motore basato su browser (Client-side) calcola l'hash (digest digitale) del file sul vostro computer. Solo questa impronta e i metadati vengono inviati al server.

> **Nota sulla Privacy:** Il file dell'opera non viene caricato sul server ed è così protetto. Tuttavia, i dati forensics (IP/posizione) vengono condivisi secondo la modalità di visibilità selezionata (private/masked/public).

### 2) Forensic Data Fusion (Potere Forense)

È molto più di un semplice timestamp. Il sistema combina i seguenti dati in un singolo "Genesis Seal":

- **Digest Digitale (SHA-512):** Utilizzando lo standard di digest crittografico (SHA-512), un'impronta digitale che si romperà anche se un singolo pixel dell'opera cambia.
- **Posizione e Tempo:** Data con precisione al millisecondo, paese, città e distretto in cui è stata effettuata la transazione.
- **Identità del Dispositivo:** Sistema operativo, browser e tipo di dispositivo (analisi User-Agent).

---

## 🛡️ Aree di Utilizzo e Benefici

Se sei un artista, scrittore o designer, non basta dire "L'ho fatto prima io", devi dimostrarlo.

**Un'opera sigillata con PoArt:**

- **Prova Matematica:** Il sistema lo rileva anche se un singolo pixel del file cambia. La manipolazione è impossibile.
- **Base Legale:** È registrato in quale data, in quale città, da quale dispositivo l'opera è stata sigillata.
- **Certificato Istantaneo:** In pochi secondi genera un **"Certificato di Identità dell'Asset"** personalizzato, con codice QR e sigillato.

---

## ⚙️ Architettura del Sistema e Specifiche Tecniche

Il sistema è progettato su un'architettura "Serverless", focalizzata su alte prestazioni e scalabilità.

| Livello | Tecnologia | Descrizione |
|--------|-----------|----------|
| **Crittografia** | SHA-256 & SHA-512 | Digest crittografico a doppio strato |
| **Database** | Supabase (PostgreSQL) | Struttura dati JSONB, politiche RLS |
| **Dati Forensi** | ipapi.co API | Triade IP/Posizione/Tempo |
| **Rendering** | html2canvas + jsPDF | Generazione PNG/PDF lato client |
| **Frontend** | Vanilla JavaScript | Zero dipendenze da framework |
| **Sicurezza** | Client-side hashing | Il file non viene mai caricato sul server |

### Caratteristiche Distintive

| Caratteristica | Dettaglio | Nei Concorrenti? |
|---------|-------|-------------|
| **Drag & Drop UI** | Trascina e rilascia file, anteprima istantanea | ❌ Assente nella maggior parte |
| **Multi-Format Export** | PNG, JSON, PDF - con un clic | ⚠️ Limitato |
| **Real-Time Preview** | Anteprima certificato live | ❌ Assente |
| **Privacy Controls** | Opzioni Private/Masked/Public | ❌ Assente |
| **Client-Side Hashing** | Il file non va mai sul server | ✅ Solo in alcuni |
| **Forensic Metadata** | IP, posizione, dispositivo, tempo - tutto insieme | ❌ Frammentato |
| **QR Verification** | Codice QR per verifica istantanea | ⚠️ Limitato |
| **Rate Limiting** | Protezione spam (RLS + Client) | ❌ Assente nella maggior parte |

---

## 🗺️ Roadmap: Futuro "Trustless"

La versione attuale **(Beta v1.0)** è ottimizzata per fornire all'utente finale massima velocità, interfaccia facile e accesso gratuito. Tuttavia, la nostra visione finale è passare a una struttura in cui nemmeno l'amministratore del database (noi) può intervenire.

### Fase 1: Beta (Attualmente Live)

- **Infrastruttura:** Cloud Database (Supabase).
- **Obiettivo:** Velocità, eliminazione delle barriere UX (Esperienza Utente) e adattamento. Fornire sicurezza "senza attrito".

### 🚀 Fase 2: (Richiedenti Backend / Edge Function)

Questa fase copre la transizione dalla struttura completamente "Client-Side" del sistema a una struttura "Server-Side Authority" più sicura e gestibile.

| Elemento | Cosa Porta? | Tech Stack | Priorità |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Function** | Blocco spam + sicurezza API Key | Supabase Edge (Deno) | 🔴 Alta |
| **Firma Wallet** | Autenticazione identità crittografica | Solana Wallet Adapter | 🟡 Media |
| **Backup IPFS/Arweave** | Immutabilità decentralizzata | IPFS SDK + Pinata | 🟢 Bassa |
| **Meccanismo di Revoca** | Annullamento certificati falsi | Aggiornamento Schema DB | 🔴 Alta |
| **Audit Log** | Registrazione indagine forense | Tabella logs personalizzata | 🟡 Media |
| **OpenTimestamps** | Ancoraggio Bitcoin | OTS JavaScript | 🟢 Bassa |
| **Integrazione DID** | Decentralized Identity | ION/Ceramic | 🟢 Bassa |

### Fase 3: Piena Decentralizzazione (Lungo Termine)

| Caratteristica | Obiettivo | ETA |
|---------|-------|-----|
| **Blockchain Registry** | Registrazione on-chain Ethereum/Solana | Q4 2026 |
| **DAO Governance** | Governance comunitaria | Q1 2027 |
| **Multi-Chain Support** | Polygon, Arbitrum, Base | Q2 2027 |
| **Legal Recognition** | Validità nei tribunali turchi | 2027-2028 |
| **API for Developers** | Endpoint API pubblico | Q3 2026 |

---

## 📊 Analisi Competitiva (Aggiornata)

PoArt è posizionato sullo "Sweet Spot" (Punto ideale ottimale) che completa le lacune delle soluzioni esistenti.

| Caratteristica | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Costo** | 🆓 Gratuito | 🆓 | 💰 A pagamento | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Molto Facile | ❌ CLI | ⚠️ Medio | ⚠️ Medio | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Live | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Modalità | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privacy | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Completo | ❌ | ❌ | ⚠️ Limitato | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Istantaneo | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Supporto Italiano** | 🔄 In sviluppo | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Legenda:**
- ✅ : Supporto completo / disponibile
- ⚠️ : Limitato / nei piani a pagamento
- ❌ : Assente / non supportato
- 🔄 : Nella Roadmap (in sviluppo)
- 🆓 : Completamente gratuito
- 💰 : A pagamento / richiede abbonamento

### Carenze dei Concorrenti, Punti di Forza di PoArt

| Meno | Concorrenti | PoArt |
|------|----------|-------|
| **Difficoltà d'Uso** | CLI, conoscenza API, wallet richiesto | Trascina e rilascia, finisce in 3 clic |
| **Barriera dei Costi** | Abbonamento $50-500/mese | 100% gratuito |
| **Privacy** | File caricato sul server | Client-side, il file non va mai |
| **Dati Forensi** | Solo timestamp | IP, posizione, dispositivo, tempo - tutto |
| **Supporto Italiano** | Assente o molto limitato | Supporto linguistico nativo |
| **Open Source** | Scatola chiusa | Tutto il codice aperto su GitHub |

---

## 🧬 Struttura Dati del Protocollo (JSON Schema)

**Ogni certificato [PoArt] ha una carta d'identità JSON portatile e verificabile prodotta nello standard seguente.**

> **Nota:** Questo formato Identity JSON è il formato del certificato presentato all'utente. Nei record del registro, invece di `identity.asset_data` si usa `registry.asset` (mapping: `identity.asset_data` == `registry.asset`).
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
    "title": "Whitepaper Ufficiale",
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

## 🔬 Profondità Tecnica: Algoritmo di Sigillatura

### Funzioni Hash Deterministiche
```javascript
// Funzioni Ausiliarie: Converti digest in stringa hex
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Converti stringa in byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Generazione stringa forensics canonica (v1.0: ordine campo fisso + UTF-8 + delimitatore \n)
// Nota Fase 2: Si passerà a JSON canonico con RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Processo di Produzione NotarySeal (Completamente Deterministico)
```javascript
// 1. Calcolo FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Raccolta dati forensi (uso di singolo timestamp)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Generazione singolo timestamp
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

// 3. Creazione EvidenceRoot (con encoding canonico)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Produzione NotarySeal (uso stesso timestamp)
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

### Flusso di Verifica (Due Livelli)

#### Quick Verify (Verifica Rapida)
```javascript
// Controlla solo l'hash del file (bandiera rossa veloce)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Recupera dal Registry
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Confronto hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Originale - Hash file corrispondente"
    };
  } else {
    return {
      valid: false,
      message: "❌ Falso - File manipolato"
    };
  }
}
```

#### Full Verify (Verifica Completa)
```javascript
// Riproduce e verifica EvidenceRoot e NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Recupera dal Registry
  const cert = await fetchFromRegistry(certificateId);

  // 1) Controllo FileHash (bandiera rossa veloce)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Falso - Hash file non corrispondente" };
  }

  // 2) Riproduci EvidenceRoot (con forensics memorizzati nel registry)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Non corrisponde - EvidenceRoot non valido" };
  }

  // 3) Riproduci NotarySeal (con stesso timestamp + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Non corrisponde - NotarySeal non valido" };
  }

  // Opzionale: Nella Fase 2 verifica anche signer_sig con attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Firma non valida" };

  return { valid: true, message: "✅ Originale - Full Verify superata" };
}
```

> **Note Importanti:**
> - **Quick Verify:** Controlla solo l'hash del file per uso rapido.
> - **Full Verify:** Verifica tutti i livelli del protocollo (EvidenceRoot + NotarySeal).
> - Tutte le operazioni hash sono eseguite in modo deterministico, con encoding e delimitatori fissi.
> - **Standard di canonicalizzazione v1.0:** Ordine campo fisso + encoding UTF-8 + delimitatore `\n`.
> - **Piano Fase 2:** Passaggio a JSON canonico con RFC 8785 (JCS - JSON Canonicalization Scheme).
> - In modalità Masked, il calcolo di EvidenceRoot e NotarySeal viene effettuato con forensics mascherati.
> - Viene utilizzato un singolo timestamp in tutto il processo (forensics + NotarySeal); il determinismo è garantito.
> - **Nomi campi Forensics:** `ip_masked`, `location`, `device`, `timestamp` (codice e registry completamente compatibili).
> - **Path Registry:** `certificate.asset.fingerprints` (completamente compatibile con il codice di verifica).
> - **signer_sig nel Registry:** Il campo `proof.signer_sig` è necessario per Full Verify.
> - Il meccanismo SignerSignature sarà attivato nella Fase 2 con Solana Wallet Adapter; nella v1.0 è possibile effettuare la verifica con `attestation_pubkey`.

---

## 📈 Statistiche di Utilizzo (Obiettivi Q1 2026)

| Metrica | Obiettivo | Stato |
|--------|-------|-------|
| **Certificati Totali** | 1,000 | 🔄 In Progresso |
| **Utenti Attivi** | 500 | 🔄 In Progresso |
| **Numero Verifiche** | 5,000 | 🔄 In Progresso |
| **Uptime** | %99.9 | ✅ Attivo |
| **Tempo Risposta Medio** | <200ms | ✅ Ottimale |

---

## 🌍 Comunità e Supporto

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 Contributori

Il protocollo PoArt continua a evolversi con i contributi della comunità open source.

**Per contribuire:**
1. Fai fork
2. Crea feature branch (`git checkout -b feature/amazing-feature`)
3. Fai commit (`git commit -m 'Add amazing feature'`)
4. Fai push (`git push origin feature/amazing-feature`)
5. Apri Pull Request

### 🛠️ Di Cosa Abbiamo Bisogno Ora? (Chiamata per Aiuto)

Stiamo cercando i contributi di sviluppatori esperti nei seguenti argomenti per gli sviluppi **Fase 2** del Protocollo PoArt:

* **Supabase Edge Functions:** Spostare la protezione spam lato server.
* **Solana Web3.js:** Integrazione firma wallet (Wallet Signing).
* **IPFS / Arweave:** Integrazione servizi di archiviazione e pinning.

> Prima di aggiungere una funzionalità, avvia una discussione nella sezione "Issues".

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // La Cultura è più grande del Capitale*

## 🧾 Licenza

MIT License © 2026 İlhan Art Gallery Initiative

Vedi [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) per i termini completi.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Questo progetto è stato sviluppato con l'iniziativa [İlhan Art Gallery] e il codice sorgente è pubblicamente disponibile per trasparenza.**

**PROTOCOLLO V1.0 // SIGILLATO CON SHA-512.**

*© 2026 İLHAN ART | TUTTI I DIRITTI SULLE OPERE, IMMAGINI E IDEE SONO RISERVATI.*

---
