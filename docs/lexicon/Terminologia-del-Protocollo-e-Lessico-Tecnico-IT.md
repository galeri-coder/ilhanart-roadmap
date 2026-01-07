---
title: "Ilhan Art Protocol (Protocollo d’Arte di İlhan)"
version: "1.0 (Versione Stabile)"
status: "HARD_LOCKED"
integrity: "SHA-512"
ecosystem: "[PoArt] + [FPP] + [Michelangelo] + [Cultural Layers]"
last_updated: "2026-01-07"
---

# 📜 Terminologia del Protocollo e Lessico Tecnico 🇮🇹
> **Versione del protocollo:** 1.0 (Stabile)  
> **Visione di rete:** 2025 → 3000, archivio globale della civiltà  
> **Ecosistema:** [PoArt] + [FPP] + [Michelangelo] + [Cultural Layers]  
> **Stato:** **HARD_LOCKED** (documentazione attiva e firmata)  
> **Integrità:** Sigillato con SHA-512, compatibile con notarizzazione digitale

---

## 🔰 Architettura Stratificata (Layered Architecture Overview)

| Livello | Scopo | Protocollo |
|:--|:--|:--|
| **L1** | Verifica del lavoro umano | **[PoArt] Proof of Art** |
| **L2** | Lealtà ed economia sostenibile | **[FPP] Foundational Pillar Protocol** |
| **L3** | Meritocrazia e governance | **[Michelangelo Framework]** |
| **L4** | Integrazione culturale e reale | **Cultural Layers & Privileges** |

> Questa struttura definisce una coerenza tecnica e filosofica su quattro piani fondamentali.  
> L’intero sistema può essere compreso in meno di due minuti grazie a questa visione sintetica.

---

## 🧩 Struttura di Membro — “Primer → Texture → Impasto”

| Livello | Definizione | Base tecnica |
|:--|:--|:--|
| **Primer (Base)** | Livello iniziale, utente verificato con bassa frizione temporale (TWAB). | `0 < TWAB ≤ 10⁰` |
| **Texture (Intermedio)** | Partecipante attivo con permanenza stabile. | `10⁰ < TWAB ≤ 10²` |
| **Impasto (Avanzato)** | Membro veterano con attività ≥ 365 giorni. | `TWAB > 10²` |

### Formula di Classificazione:
$$
\text{Tier}(u)=
\begin{cases}
\text{Primer},&0<\text{TWAB}_u\le10^0\\
\text{Texture},&10^0<\text{TWAB}_u\le10^2\\
\text{Impasto},&\text{TWAB}_u>10^2
\end{cases}
$$

> I livelli si aggiornano dinamicamente in base alla stabilità temporale e al contributo culturale.

---

## 🏛️ 1) Pilastri del Protocollo (Pillars of the Protocol)

### **[PoArt] Proof of Art (v1.0)**
**Definizione:**  
Protocollo che certifica non solo l’opera finale, ma l’intero **processo creativo umano** attraverso dati tecnici tracciabili.  

**Problema risolto:**  
Nell’era dell’IA generativa, il confine tra creazione umana e automatizzata è sfocato, causando la svalutazione dell’arte reale.  

**Funzionamento:**  
L’artista genera un **Pacchetto di Prova (Evidence Pack)** contenente ogni fase della creazione.  
Il protocollo lo sigilla con timestamp e hash su blockchain.  

**Esempio:**  
Un dipinto creato in 40 ore viene validato non per l’immagine finale, ma per le 40 ore di lavoro dimostrabile.

---

### **[FPP] Foundational Pillar Protocol (v1.0)**
**Definizione:**  
Sistema che costruisce le basi economiche e di governance del protocollo, premiando lealtà e partecipazione sostenuta.  

**Problema affrontato:**  
Il principio ingiusto “chi ha più capitale comanda”.  

**Meccanismo:**  
L’influenza non dipende dal capitale posseduto, ma dalla **durata della detenzione** e dalla **stabilità del contributo**.  

**Esempio:**  
Un patrono che mantiene 100 token per un anno avrà più potere di voto di un investitore con 1 milione di token detenuti da una settimana.

---

## 👥 2) Ruoli e Entità (Roles & Entities)

| Ruolo | Descrizione |
|:--|:--|
| **Artista (Artist)** | Crea e firma l’Evidence Pack per [PoArt]; rinnova la prova ogni anno (heartbeat). |
| **Patrono (Patron)** | Guadagna reputazione attraverso la lealtà e la partecipazione [FPP]. |
| **Validatore (Validator)** | Verifica la coerenza e l’integrità dei dati. |
| **Notaio Digitale (Digital Notary)** | Smart contract che convalida e sigilla i pacchetti verificati. |
| **Registro Pubblico (Public Registry)** | Memorizza permanentemente lo stato: Verified / Legacy / Revoked. |
| **Archivio Off-chain (Evidence Storage)** | Archivia i file grezzi su IPFS o Arweave; solo gli hash vengono scritti On-Chain. |

---

## 📊 3) Metriche Economiche e di Governance (Economic & Governance Metrics)

### 3.1) Finestre Temporali e Epoche (Time Windows & Epochs)

| Tipo | Durata | Funzione |
|:--|:--|:--|
| **Epoca Operativa (Operational Epoch)** | 7 giorni | Aggiornamenti periodici e sincronizzazione dei log |
| **Finestra di Protezione (Guard Window)** | 30 giorni | Blocca movimenti di capitale prima di voti critici |
| **Ciclo di Integrità (Integrity Cycle)** | 365 giorni | Rinnovo annuale di verifica |

---

### 3.2) Media Ponderata per Tempo (TWAB)
$$
TWAB = \frac{\sum_{i=1}^{n}(\text{Saldo}_i\times\Delta t_i)}{\sum_{i=1}^{n}\Delta t_i}
$$  

**Definizione alternativa (TWA):**
$$
TWA = \sum_{i=1}^{n}(\text{Saldo}_i\times\Delta t_i)
$$  

> Misura la **lealtà temporale**, non solo la ricchezza momentanea.

---

### 3.3) Potere di Voto (Voting Power)
$$
VotingPower = f(TWAB, EpochRules, StatusTier)
$$

Durante le votazioni critiche, viene applicata la finestra di 30 giorni (Guard Window).

---

### 3.4) Punteggio Logaritmico (Logarithmic Power Scoring)
$$
Score = \log_{10}(TWAB + 1)
$$  
$$
VotingPower = Score \times g(EpochRules, StatusTier)
$$  

| TWAB | Score | Interpretazione |
|:--|:--|:--|
| 10 | 1.04 | Impatto base |
| 1.000 | 3.00 | 100× potere medio |
| 1.000.000 | 6.00 | 100.000× potere nominale |

> Simulazioni disponibili sulla [PoArt Console](https://galeri-coder.github.io/ilhanart-protocol/[PoArt]/).

---

## 🛡️ 4) Sicurezza e Validazione (Security & Validation) 🇮🇹

### 4.1) Il “Millennium Vault” (Baule del Millennio)
**Definizione:**  
Archivio di fiducia a lungo termine dove i token vengono bloccati per cicli annuali.  
**Scopo:**  
Preservare la visione di lungo periodo (2025–3000) e impedire manipolazioni speculative.  
**Regola:**  
Accesso riservato ai membri [FPP] “Pillar Fundazionale” con attività ≥ 1 anno.

---

### 4.2) Il Pacchetto di Prova (Evidence Pack)
**Definizione:**  
Set tecnico obbligatorio per la convalida di un’opera in [PoArt].  

#### La Trinità della Prova:
1. **Log in diretta (Live Logs)**  
2. **Timelapse del processo**  
3. **Impronta digitale (Hash firmato)**  

#### Livello di Integrità Criptografica:
4. **Manifesto di Cattura (Capture Manifest)** — specifiche tecniche, checksum, durata.  
5. **Radice Merkle (Merkle Root):**
$$
EvidenceRoot = MerkleRoot(AllFiles)
$$  
6. **Challenge Frames casuali:** richieste casuali che provano la presenza umana.  

**Risultato:**  
Dimostra matematicamente la creazione umana e la autenticità contro IA o deepfake.

## 🏛️ 5) Verifica e Persistenza (Validation & Persistence) 🇮🇹

### 5.1) Verifica Cold-Wallet (365 Giorni)
**Definizione:**  
Tutti gli asset devono rimanere in un portafoglio hardware (Ledger, Trezor, ecc.) per almeno 365 giorni consecutivi.  

**Previene:**
1. Wash Trading (transazioni simulate)  
2. Pressione speculativa a breve termine  
3. Rischi di hacking su hot wallet  

---

#### Scala di Penalità (Penalty Ladder)
**Prima violazione:**  
$$
EffectiveTWAB = TWAB \times 0.20
$$  
**Seconda violazione:**  
$$
EffectiveTWAB = TWAB \times 0.05
$$  
**Terza violazione:**  
Status = Revoked (Revocato)

> Una struttura che punisce la speculazione ma conserva l’equità proporzionale.

---

#### Eccezioni di Trasferimento Sicuro (Move Permit / Time-Lock)
- Richiesta di trasferimento approvata  
- Attivazione Time-Lock temporaneo  
- Supervisione comunitaria (Veto + Quorum)  
- On-chain vengono registrati solo firma e nuovo indirizzo  

---

### 5.2) Verifica del Pacchetto di Prova (Evidence Pack)
**Elementi richiesti:**
1. Log in tempo reale  
2. Video del processo  
3. Metadati tecnici  
4. EvidenceRoot  

> La verifica riguarda il **processo creativo**, non solo il risultato.

---

### 5.3) Heartbeat Annuale (365 Giorni)
- Ogni record deve essere rinnovato annualmente.  
- Notifica automatica 30 giorni prima della scadenza.  
- Se non rinnovato → stato = *Legacy Archive*  

**Scopo:** mantenere la freschezza dei dati e rimuovere archivi dormienti.

---

## 🗳️ 6) Supervisione Decentralizzata (Decentralized Supervision) 🇮🇹

### 6.1) Meccanismo di Veto Comunitario (Community Veto)
**Definizione:**  
Sistema democratico che consente a una minoranza (40% TWAB) di bloccare proposte.  

**Condizioni:**  
- Quorum ≥ 25% partecipazione attiva  
- Veto ≥ 40% peso TWAB  

**Protegge da:**
1. Attacchi Sybil  
2. Collusione e corruzione  
3. Manipolazione di voto  

> Anche se un’opera IA riceve certificazione [PoArt], può essere esclusa dal registro tramite veto del 40%.

---

### 6.2) Governance d’Emergenza e Consiglio di Backup (Emergency Governance / Fallback Council)
**Scopo:**  
Evitare lo stallo decisionale per mancanza di partecipazione.

**Formula:**
$$
Deadlock = (ParticipationRate < 25\%) \land (ProposalTimeout > 7\,giorni)
$$

**Quando attivo:**
1. Formazione di un consiglio composto dal top 10% Impasto.  
2. Decisioni valide solo con consenso ≥ 2/3.  
3. Se non confermato dalla comunità entro 30 giorni → nullo.  
4. Tutte le azioni registrate nel *Registro di Emergenza (Emergency Ledger)*.

---

## ⚙️ 7) Il Framework Michelangelo (Motore Meritocratico) 🇮🇹

### 7.1) Filosofia di Michelangelo (Michelangelo Philosophy)
**Definizione:**  
Motore meritocratico di governance dell’ecosistema Ilhan Art,  
che sostituisce il potere economico con il merito culturale e cognitivo.  

**Principio guida:**  
> “Non il denaro, ma la cultura e il lavoro salgono al vertice.”

**Esempio:**  
Un utente con 1.000.000 token ma inattivo  
ha meno influenza di chi contribuisce con traduzioni o educazione continua.

---

### 7.2) Formula dello Status (Status Formula)
$$
Status = HoldingTime \times CulturalContribution
$$

- **HoldingTime:** giorni di possesso in cold wallet  
- **CulturalContribution:** traduzioni, insegnamento, sviluppo, archiviazione  
**Scopo:**  
Combinare tempo + contributo per calcolare la legittimità culturale.

---

### 7.3) Principio di Meritocrazia Culturale
- L’influenza cresce con la stabilità del contributo.  
- Ogni azione è tracciabile (firma + timestamp).  
- La governance diventa un atto d’artigianato intellettuale.  

> “Equità matematica al posto del potere politico.”

---

## 📊 8) Moltiplicatori Culturali e Livelli di Rango (Cultural Multipliers & Rank Tiers) 🇮🇹

### 8.1) Moltiplicatore Culturale (Cultural Multiplier)
**Definizione:**  
Sistema quantitativo che misura e premia il contributo culturale nel tempo.

| Ambito | Descrizione | Peso |
|:--|:--|:--|
| Traduzione | Traduzione di testi artistici o filosofici | +4.500 |
| Curazione | Revisione, mostre, archiviazione | +2.000 |
| Infrastruttura | Codice, documentazione, strumenti open source | +3.000 |
| Educazione | Corsi, formazione, divulgazione | +1.500 |

**Formula:**
$$
FinalScore = BaseScore \times (1 + CulturalMultiplier)
$$

---

### 8.2) Livelli di Rango (Rank Tiers)
**Definizione:**  
Tre categorie che definiscono ogni livello di governance.

| Rango | Punteggio | Diritti |
|:--|:--|:--|
| **Impasto (≥100k)** | Costituzionale | Strategia, tasse, direzione ecosistemica |
| **Texture (50k–99k)** | Curatoriale | Revisione, auditing, voto |
| **Primer (<50k)** | Fondamentale | Proposte minori e partecipazione |

> I ranghi vengono rivalutati dinamicamente in base a TWAB e merito culturale.

---

## 📈 9) Soglie e Metriche di Rete (Cut-off Thresholds & Network Metrics) 🇮🇹

### 9.1) Soglie d’Ingresso (Entry Thresholds)
| Categoria | Punti richiesti | Descrizione |
|:--|:--|:--|
| **Impasto** | ≥ 100.000 | Pieno diritto di governance |
| **Top 100** | ≥ 45.000 | Partecipazione strategica |
| **Entry** | ≥ 250 | Livello base di accesso |

**Obiettivo:**  
Preservare la proporzionalità del potere indipendentemente dalla crescita del network.

---

### 9.2) Indice TWAB della Rete (Network TWAB Index)
**Definizione:**  
Somma globale dei TWAB individuali come indice di stabilità del protocollo.  
**Interpretazione:**  
Un valore alto → maggiore resilienza alle manipolazioni.  
**Aggiornamento:**  
Ogni 24 ore con nuovi record [PoArt].

---

## 🧬 12) Eredità Generazionale e Governance (Generational Legacy & Governance) 🇮🇹

### 12.1) Eredità Generazionale (Generational Inheritance)
**Definizione:**  
I membri **Impasto** attivi per oltre 4 anni (1.460 giorni consecutivi) possono designare un erede ufficiale.  

**Obiettivo:**  
Prevenire la perdita di patrimonio culturale dovuta a inattività, decesso o perdita d’accesso.  

**Procedura:**  
- L’attivazione è concessa dopo 4 anni di attività verificata.  
- Il trasferimento avviene via **multisig** e viene registrato on-chain.  

> La continuità culturale diventa ereditaria, non finanziaria.

---

### 12.2) Diritti di Governance Parlamentare (Parliamentary Governance Rights)
**Definizione:**  
Sistema tripartito che suddivide la governance in **Cultura / Tecnologia / Strategia**.

| Livello | Area | Responsabilità |
|:--|:--|:--|
| **Impasto (≥100k)** | Costituzionale / Strategica | Definisce politiche, tasse e direzione dell’ecosistema |
| **Texture (50k–99k)** | Gestione / Curazione | Valida, cura e supervisiona i voti |
| **Primer (<50k)** | Proposte / Micro-decisioni | Presenta proposte minori, partecipa ai dibattiti |

> “La democrazia della competenza” — dove la conoscenza pesa più della quantità.

---

## 🌍 13) Livelli di Privilegio Culturale e Integrazione Reale (Cultural Privilege Layers & Real-World Integration) 🇮🇹

> Queste sezioni (2026–2030) collegano la governance digitale del protocollo con infrastrutture culturali fisiche.

---

### 13.1) Diritto di Esposizione Annuale (Annual Exhibition Right)
**Definizione:**  
Gli artisti e i patroni con verifica [PoArt] e punteggio [FPP] qualificato  
ricevono il diritto di esporre annualmente per 7 giorni presso la **Ilhan Art Gallery**.  

**Scopo:**  
Garantire un **accesso equo all’esposizione artistica**, basato su merito e contributo, non sul capitale.  

**Meccanismo:**  
- Prenotazione automatica tramite calendario on-chain  
- Assegnazione slot in base a punteggio culturale e reputazione  
- Nessun costo di locazione, commissioni minime  

> Democratizzazione dell’esposizione artistica tramite smart contract verificabile.

---

### 13.2) Prezzi Dinamici dell’Arte (Dynamic Art Pricing, JSON-Linked Discounts)
**Definizione:**  
Sistema di prezzo dinamico collegato a un’API JSON che calcola sconti secondo il rango culturale.  

| Livello | Sconto |
|:--|:--|
| **Impasto (≥100k)** | 50% o più |
| **Texture (50k–99k)** | 30% |
| **Primer (<50k)** | 10% |

**Principio:**  
> “Nessuna contrattazione: solo valore dimostrato.”

**Struttura Tecnica:**  
- L’API è sincronizzata con gli indici [FPP]  
- I prezzi si aggiornano in tempo reale in base al *CulturalMultiplier*  

---

### 13.3) Integrazione Fisica dell’Ecosistema (Physical Ecosystem Integration)
**Definizione:**  
Estende il [Ilhan Art Protocol] alle reti culturali fisiche reali.  

**Componenti:**  
- Reti partner: librerie, caffè, centri d’arte, gallerie  
- Verifica QR: controllo d’identità on-chain in spazi fisici  
- API JSON: verifica in tempo reale di stato e privilegi  

**Effetto:**  
L’identità digitale diventa una forma di cittadinanza culturale Web3.

---

### 13.4) Lavoro sopra il Capitale (Labor Over Capital)
**Definizione:**  
Algoritmo etico che valorizza il lavoro creativo più del possesso economico.

**Formula:**
$$
ClaimRight \propto CulturalScore + \log_{10}(Balance)
$$

**Esempio:**
- Utente A: 250 ILHAN + contributi culturali → alto diritto  
- Utente B: 100.000 ILHAN + inattività → basso diritto  

**Filosofia:**  
Il valore viene redistribuito in base al merito, trasformando la *plutocrazia* in *laborocrazia*.  
> “Dal dominio del capitale alla democrazia del lavoro.”

---

## 🧩 14) Macchina di Stato — Ciclo di Vita di un Record (State Machine — Lifecycle of a Record) 🇮🇹

### Flusso del Processo:
1. **Draft (Bozza)** → creato localmente  
2. **Submitted (Inviato)** → caricato on-chain  
3. **Under Review (In revisione)** → in verifica  
4. **Challenged (Contestato)** → con obiezione attiva  
5. **Verified (Verificato)** → sigillato da notaio digitale  
6. **Renew Due (Rinnovo richiesto)** → notifica annuale  
7. **Legacy Archive (Archiviato)** → non rinnovato  
8. **Revoked (Revocato)** → penalità o violazione confermata  

---

### Regole di Transizione:
| Stato attuale | Stato successivo | Condizione |
|:--|:--|:--|
| Draft | Submitted | Caricamento completato |
| Submitted | Under Review | Approvazione validatore |
| Under Review | Verified | Consenso ≥ 66% |
| Under Review | Challenged | Obiezione |
| Challenged | Revoked | Obiezione accolta |
| Challenged | Verified | Obiezione respinta |
| Verified | Legacy | Mancato rinnovo |
| Legacy | Revoked | Mancata verifica annuale |

> Ogni passaggio è tracciato con firma digitale e timestamp verificabile.

---

## 🔗 15) Dati On-Chain Minimi / Off-Chain Massimi 🇮🇹

### Dati On-Chain:
- EvidenceRoot (radice Merkle)  
- NotarySeal (sigillo notarile)  
- TimeStamp (marcatura temporale)  
- Signer (indirizzo firmatario)  
- Status (Verified / Legacy / Revoked)  
- Permit (trasferimento o eredità)

### Dati Off-Chain:
- Video originali e log tecnici  
- Manifesto di cattura  
- Archiviazione su IPFS / Arweave  

**Scopo:** ridurre il carico sulla blockchain senza sacrificare la verificabilità.  
**Integrità:** ogni elemento può essere riconvalidato via SHA-512.

---
## 🏛️ 16) Meccanismo di Appello e Obiezione (Appeals & Objection Mechanism) 🇮🇹

### 16.1) Principi Fondamentali
- **Basato su prove:** ogni appello deve includere dati verificabili.  
- **Nessuna emozione:** reclami soggettivi vengono ignorati.  
- **Trasparenza:** ogni fase è pubblica e firmata con timestamp.  
- **Regola di blocco:** durante l’appello, l’Evidence Pack è congelato.

---

### 16.2) Salvaguardie Comunitarie
- Soglia di veto: 40% del TWAB attivo  
- Quorum minimo: ≥ 25% partecipazione  
- Protezione Sybil: Turnstile + staking verificato  
- Filtro IA: esclusione automatica delle richieste generate  

---

### 16.3) Ciclo di Vita dell’Appello
1. **Inizio:** presentazione dell’appello  
2. **Congelamento delle prove:** blocco automatico  
3. **Revisione comunitaria:** analisi pubblica  
4. **Voto:** periodo di 7 giorni  
5. **Chiusura:** hash SHA-512 e archiviazione nel registro  

> Ogni appello diventa parte della trasparenza pubblica della rete.

---

## 🧨 17) Modello di Minaccia e Contromisure (Threat Model & Countermeasures) 🇮🇹

| Minaccia | Contromisura |
|:--|:--|
| Attacco Sybil | Turnstile + Zombie Filter + Quorum |
| Flash Loan | TWAB + Guard Window + punteggio logaritmico |
| Dominio delle balene | TWAB stabile + riduzione logaritmica |
| Wash Trading | Cold-Wallet + scala di penalità |
| Collusione e corruzione | Veto + registro pubblico d’audit |
| Manipolazione dati | EvidenceRoot + SHA-512 + NotarySeal |
| Acquisto di voti | Time-Lock + verifica TWAB |
| Deepfake / IA | Challenge Frames + catena di hash |

> Tutte le regole di difesa sono versionate e mantenute nel repository [FPP].

---

## ⚖️ 18) Manifesto Finale — Progetto per la Governance Globale (Final Manifesto — Blueprint for Global Governance) 🇮🇹

> “L’arte è il prototipo, la governance è la tela.”

La fusione di [PoArt] e [FPP] dimostra che le stesse leggi matematiche  
che proteggono l’autenticità artistica possono garantire la legittimità politica.

---

### 18.1) Fine della Plutocrazia (End of Plutocracy)
**Problema:**  
Il potere del capitale distorce la governance decentralizzata.  
**Soluzione:**  
- Il punteggio logaritmico limita l’influenza dei grandi capitali.  
- Il tempo e il lavoro diventano i nuovi assi della legittimità.  
**Principio:**  
Possedere non equivale a creare → il merito costruisce il diritto.

---

### 18.2) Il Parlamento Meritocratico (Meritocratic Parliament)
- Rappresentanza basata su competenza, non popolarità.  
- La governance è un atto di comprensione, non d’opinione.  
- Responsabilità tecnica invece di consenso emotivo.  

> “La democrazia del sapere sostituisce la tirannia del denaro.”

---

### 18.3) Integrità Elettorale (Electoral Integrity — SHA-512)
- **Turnstile:** previene la creazione di identità artificiali.  
- **TWAB:** neutralizza la manipolazione tramite spostamento di fondi.  
- **Veto + Quorum:** garantisce il controllo delle minoranze.  

> Una costituzione digitale sostenuta da prova matematica.

---

### 18.4) Manifesto per il Futuro (Manifesto — Saving the Future)
**Definizione:**  
Il protocollo non è solo un certificato artistico,  
ma un modello sociale e tecnico per la civiltà millenaria.

**Visione:**  
- Sforzo verificato > profitto immediato  
- Continuità a lungo termine > soddisfazione istantanea  
- Giustizia matematica > polarizzazione politica  

> “Nell’era dell’automazione, il valore umano risiede nella volontà di creare.”

---

## 📅 19) Roadmap e Visione Futura (Roadmap & Future Notes) 🇮🇹

| Fase | Anno | Focus Principale |
|:--|:--|:--|
| **v1.0** | 2026 | Modulo di verifica e notarizzazione |
| **v1.1** | 2027 | API pubblica e console di simulazione |
| **v1.2** | 2028 | Integrazione fisica (POS / QR) |
| **v2.0** | 2030 | Governance autonoma + indicizzazione inter-protocollare |

**Obiettivo:**  
Costruire le basi tecniche e culturali della *Ilhan Art Millennium Vision (2026–3000).*

---

## 🔐 Firma Hash (Hash Signature, v1.0 Hard-Locked) 🇮🇹

- Supervisione comunitaria sempre attiva  
- Solo gli indirizzi verificati vengono sigillati sulla catena  

**Parametri temporali:**
- **Epoca Operativa:** 7 giorni  
- **Guard Window:** 30 giorni  
- **Ciclo di Integrità:** 365 giorni  

**Verifica Annuale:**
Tutti i pacchetti di prova vengono ri-hashati con SHA-512.

---

