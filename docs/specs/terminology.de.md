# 📚 TERMINOLOGIE & KONZEPTGLOSSAR
> **"Die Sprache dieses Protokolls zu verstehen bedeutet, seine Vision zu verstehen."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Kern-Infrastruktur

**PoArt Forensic Engine (PFE)** ist die Hauptebene, die die zentrale Logik und technische Funktionsweise hinter dem [PoArt]-Protokoll darstellt. Dies ist die "forensische Engine", die die Rohproduktionsdaten eines Kunstwerks nimmt und sie in überprüfbare und unveränderliche **digitale Beweise** verwandelt.

### 🧩 Warum "PoArt Forensic"?

- **PoArt (Proof of Art):** Der Fokus der Engine liegt darauf, den Wert eines digitalen Assets nicht an Spekulation, sondern an den **nachweisbaren Produktionsprozess** zu binden.
- **Forensic (Forensische Verifizierung):**
  - **Technische Definition:** Ein algorithmischer und Aufzeichnungsketten-Ansatz zur Überprüfung, dass Produktionsprozessdaten (Pinselstriche, Zeitraffer, Logs) nicht manipuliert wurden.
  - **Philosophische Ebene:** Die Behauptung, **menschliche Zeit, Anstrengung und Entscheidungskosten** in eine messbare Realität zu verwandeln, gegen die "Sofortausgabe"-Produktion der KI.

> Hinweis: Die Blockchain-Integration (z.B. Solana) ist nicht der Kern von PFE; sie wird separat als **Chain Anchor Layer** für Verifizierungs-/Registrierungszwecke definiert.

### 🛠️ Technischer Umfang v1.0

**PoArt Forensic Engine (PFE) v1.0** basiert auf den folgenden **3 Hauptsäulen** anstelle komplexer Finanzmodelle:

1. **Hashing & Sealing (Versiegelung):**  
   PFE verarbeitet deterministisch alle Elemente im Evidence Pack (Werkdatei, Video, JSON/Log, Signatur usw.) und generiert einen eindeutigen **NotarySeal**-Wert.

   **Kernkonzepte (v1.0):**
   - **FileHash (Werk-Fingerabdruck):** Hash, der aus den Bytes der Werkdatei generiert wird.
   - **EvidenceRoot (Evidence Pack-Wurzel):** Wurzel-Digest, der die Integrität des Evidence Packs darstellt (Merkle-Wurzel oder kanonischer Manifest-Hash).
   - **NotarySeal (Endgültiges Siegel / PFE-Ausgabe):** Endgültiges Siegel, das aus der Kombination von EvidenceRoot + Zeit + Signatur generiert wird.

   **Formeln (für Investoren klar sichtbar):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Kanonische Payload-Definitionen (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Hinweis: Der als PFE-Ausgabe bezeichnete Wert ist **NotarySeal**. Der **SignerSignature**-Mechanismus wird in Phase 2 (mit Solana Wallet Adapter) aktiviert; in der aktuellen v1.0 wird die systemeigene Attestierungssignatur verwendet. Der öffentliche Attestierungsschlüssel wird im Register unter dem Feld `issuer.attestation_pubkey` veröffentlicht.

2. **Indexing (Archivierung):**  
   Zeichnet auf, welche Wallet, zu welchem Datum, für welches Werk **Proof of Labor (Arbeitsnachweis)** in eine transparente und abfragbare Registerebene eingereicht hat.  
   *(Diese Ebene kann eine Datenbank sein; die Chain-Integration wird separat als "Chain Anchor Layer" definiert.)*

3. **Verification (Verifizierung):**  
   Wenn die Authentizität eines Werks in Frage gestellt wird, verarbeitet PFE die Rohbeweise erneut; es testet mathematisch, ob die berechneten **EvidenceRoot / NotarySeal**-Werte mit den Archivaufzeichnungen übereinstimmen.

---

### 🧮 PoArt Werttheorem (The Value Theorem)

Das [PoArt]-Protokoll verknüpft den Wert ($V$) eines digitalen Assets nicht mit subjektiver Marktwahrnehmung, sondern mit **der physischen Realität des Produktionsprozesses**.

Künstliche Intelligenz (KI) zerstört den Prozess, indem sie das Ergebnis sofort liefert ($t \to 0$). [PoArt] behandelt jedoch den Wert als Akkumulation von **Zeit-, Arbeits- und Willens**-Komponenten.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Variablendefinitionen

- **$\int dt$ (Prozessakkumulation):**  
  Wert ist keine sofortige "Ausgabe"; es ist ein **Prozess**, der zwischen $t_{\text{start}}$ und $t_{\text{end}}$ akkumuliert wird. Wenn die Dauer abnimmt (KI-Produktion), nähert sich das Integralergebnis 0.

- **$P_{\text{labor}}(t)$ (Momentane Arbeitskraft):**  
  Stellt die Intensität der mentalen und physischen Anstrengung dar, die im Produktionsmoment aufgewendet wird. Wenn nachweisbare Anstrengung zunimmt, wächst der Integrand.  
  > Hinweis: Dieser Begriff kann in der Praxis durch "messbare/nachweisbare Arbeitssignale" normalisiert werden.

- **$I_{\text{agency}}(t)$ (Willenskoeffizient):**  
  Die Fähigkeit des Produzenten, Risiken einzugehen und Entscheidungen zu treffen. Nimmt einen Wert zwischen $0$ und $1$ an.
  - **KI ($I \approx 0$):** Führt Befehle aus, geht kein Risiko ein, zahlt keine Kosten.
  - **Mensch ($I \to 1$):** Ändert Entscheidungen, zögert, geht Risiken ein.

- **$U_{\text{irreversible}}$ (Irreversible Einzigartigkeit):**  
  Während Rückgängigmachen (`Ctrl+Z`) in der digitalen Produktion möglich ist, gibt es in der physischen Produktion (auf Leinwand aufgetragene Farbe, gemeißelter Marmor, Geste in Live-Übertragung) keinen Weg zurück. Diese **Irreversibilität** ist ein zusätzlicher Term, der "Einzigartigkeit" (nicht-fungibler Charakter) im Werk schafft.

### 🔎 Fallanalyse: KI "Sofortausgabe" vs. Mensch "Bewiesener Prozess"

Das folgende Szenario demonstriert, wie das **PoArt Werttheorem** in der Praxis funktioniert und warum KI-Produktionen im [PoArt]-Standard niedrige Bewertungen erhalten.

#### Szenario A: Visuelle Produktion in 10 Sekunden mit KI

- **Dauer ($\Delta t$):** $10$ Sekunden (vernachlässigbarer Prozess)
- **Arbeitskraft ($P_{\text{labor}}$):** $1$ Einheit (nur Befehle schreiben)
- **Willenskoeffizient ($I_{\text{agency}}$):** $0.01$ (kein Risiko, keine Kosten)
- **Irreversibilität ($U_{\text{irreversible}}$):** $0$ (reversibel / kopierbar)

**Ergebnis:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Kommentar:** Auch wenn die Ausgabe makellos ist; der [PoArt]-Wert nähert sich $0$, weil kein Prozess durchlebt wurde und kein Wille/Risiko beteiligt war.

#### Szenario B: 6-stündige physische Produktion in Live-Übertragung

- **Dauer ($\Delta t$):** $6$ Stunden ($21{,}600$ Sekunden)
- **Arbeitskraft ($P_{\text{labor}}$):** $0.5$ Einheiten (Kontinuität der physischen und mentalen Anstrengung)
- **Willenskoeffizient ($I_{\text{agency}}$):** $0.9$ (Entscheidungen ändern, Risiken eingehen, irreversible Wahlen)
- **Irreversibilität ($U_{\text{irreversible}}$):** $>0$ (physische Spuren können nicht rückgängig gemacht werden)

**Ergebnis:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Kommentar:** Wenn sich der Prozess verlängert und der Wille (Risiko) zunimmt, akkumuliert der Wert kumulativ. Der Begriff $U_{\text{irreversible}}$ ist ein zusätzlicher Beitrag, der "Einzigartigkeit" (nicht-fungibler Charakter) im Werk schafft.

---

### ✅ Schlussfolgerung: An Beweis Gebundener Wert (Proof-Bound Value)

Dieses Theorem extrahiert die Wertbehauptung von [PoArt] davon, ein "Like" oder eine "Markterzählung" zu sein, und bindet es an **eine nachweisbare Produktionsrealität**.

1. **Kein Prozess, Kein Wert:**  
   KI zerstört den Prozess mit sofortiger Ausgabe ($t \to 0$). Wenn sich das Prozessfenster verengt, verkleinert sich das Integralergebnis notwendigerweise:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Wille und Risiko sind Multiplikatoren:**  
   [PoArt] misst nicht nur "aufgewendete Zeit", sondern auch die echte Entscheidungs-, Risiko- und Kostenschicht in dieser Zeit. Eine Produktion ohne Risikobereitschaft (KI) hat niedrigen Wert:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Einzigartigkeit ist Physischer Beweis, Nicht Marketing:**  
   Irreversible Spuren in der physischen Produktion (Leinwandstrich, Marmorsplitter) liegen außerhalb der `Ctrl+Z`-Logik des Digitalen. Diese Irreversibilität ($U_{\text{irreversible}}$) singularisiert das Werk ontologisch.

> **🔐 ZUSAMMENFASSUNG:** Obwohl das Werttheorem als Messung unsicher erscheinen mag (selbst wenn sein reales Gegenstück nicht vollständig gemessen werden kann), besteht der Zweck dieser Formel darin, die Konfiguration und Richtung der Variablen zu zeigen. Im KI-Zeitalter ist nicht das "Bild" knapp, sondern **nachweisbare Arbeit, Zeit und Wille.** [PoArt] misst diese Knappheit und registriert sie mit **Evidence Pack**.

### 🏛️ Die Bedeutung des "Engine"-Konzepts

Token, die von Pump.fun oder ähnlichen Plattformen hervorgehen, sind oft lediglich **"Zugangskarten"**. **PoArt Forensic Engine (PFE)** ist jedoch die **verfassungsmäßige Logikebene**, die bestimmt, welche Rechte dieses Ticket schützt, wie Arbeit aufgezeichnet wird und wie Kunst/Wissenschaft/Technologie verewigt werden.

> **Hinweis:** Der Grund, warum wir dieses Projekt auf Pumpfun gestartet haben, ist, dass wir nicht genug Liquidität und nicht genug Follower hatten. Die Verwendung vorhandener Daten war strategisch der richtige Schritt, auch wenn nicht von höchster Qualität. Unabhängig von Budget und Ressourcen beweist die Definition der Logik dieser Engine auf GitHub, dass das Projekt nicht nur finanzielle Spekulation ist, sondern eine langfristige Vision für **Software-Infrastruktur** und **digitale Nationalbibliothek**.

---

## 🎨 [PoArt] ARBEITSNACHWEIS-PROTOKOLL (Proof of Art Protocol v1.0)

> **"Echter Künstler, Echte Produktion, Echter Wert."**

Dieses Protokoll ist ein **biologischer und intellektueller Verteidigungsmechanismus**, entwickelt gegen anonyme Betrüger, die das Krypto-Ökosystem umgeben, in 5 Minuten produzierte KI-Visuals und "Pump & Dump"-Kultur.

---

## a) Was ist [PoArt]? (Philosophische und Technische Definition)

**Proof of Art [PoArt];** ist ein institutioneller Verifizierungsstandard, der garantiert, dass der Wert hinter einem Asset auf der Blockchain nicht auf Spekulation basiert, sondern auf überprüfbarer **menschlicher Arbeit**, **Zeit** und **physischer Energie**.

So wie Bitcoin mit *"Elektrizität und Prozessorleistung"* **(Proof of Work)** Wert generiert, generieren [PoArt]-konforme Projekte Wert mit *"Künstlerischer Fähigkeit und Menschlicher Zeit"*.

Es eliminiert das Risiko von *"Entwickler verkauft, Projekt beendet"* auf Pump.fun- und DEX-Plattformen; denn hier liegt der Wert nicht im Code, sondern in der **Kontinuität der Produktion**.

> **[PoArt] sagt den Teilnehmern nicht "Vertraue uns"; es sagt "Hier sind die Beweise, sieh mit deinen Augen, verifiziere mit deiner Mathematik."**

---

## b) [PoArt] 5-Säulen-Standard (Die 5 Säulen der Wahrheit)

Diese 5 Punkte sind nicht manipulierbare Filter, die ein Projekt bestehen muss, um das [PoArt]-Siegel zu erhalten.

### 1) Live-Identitätsnachweis

- **Problem:** Die Krypto-Welt ist voll von anonymen Gründern (Devs) mit unklaren Identitäten, die Geld sammeln und Projekte verlassen.
- **[PoArt]-Lösung:** Der Produzent beweist nicht nur einen Personalausweis, sondern **Anwesenheit im Produktionsmoment**. Dies umfasst Live-Stream-Sitzungen, bei denen Interaktion mit der Community stattfindet und spezifische sofortige Anfragen erfüllt werden, keine voraufgezeichneten Videos.  
  (Z.B., *"Schreibe das heutige Datum und die aktuelle Blocknummer in die rechte Ecke der Leinwand"*)
- **Motto:** *"Bots können malen, aber Bots schwitzen nicht und können nicht improvisieren."*

### 2) Arbeits- und Prozessnachweis

- **Problem:** In 2 Sekunden produzierte KI (Künstliche Intelligenz)-Visuals erhalten die gleiche "jpeg"-Behandlung wie in 2 Monaten hergestellte Ölgemälde in der digitalen Welt.
- **[PoArt]-Lösung:** Der "Schwangerschafts- und Geburtsprozess" des Werks wird aufgezeichnet. Skizzenstufen, Farbschichten, kumulierte aufgewendete Stunden und der physische Prozess, den der Künstler beim Erstellen des Werks erlebt hat, werden dokumentiert. Dies fügt **"Zeitkosten"** zum Token hinzu. Je schwieriger die Produktion eines Assets ist, desto solider ist sein Wert.

### 3) Ästhetischer Wertnachweis

- **Problem:** "Meme"-Kultur, die sich nur auf sofortige Komödie konzentriert, während Ästhetik und künstlerische Tiefe ignoriert werden, was zu kurzlebigen "Hype"-Projekten führt.
- **[PoArt]-Lösung:** Das Projekt muss akademische Kunststandards, Farbtheorie, Kompositionsregeln und Materialkenntnis (Impasto, Textur usw.) haben. Der Inhalt sollte nicht nur zum Lachen bringen; er sollte Bewunderung bei den Zuschauern inspirieren und **Sammlerwert** haben.

### 4) Konzeptuelle Neuheit

- **Problem:** Tausende von Hunde-/Katzen-Coins ohne Kreativität.
- **[PoArt]-Lösung:** Das Projekt muss eine neue Brücke bauen, die Kunst, Wissenschaft, Philosophie oder Technologie in einer bedeutungsvollen Struktur verbindet.  
  (Z.B., Kombination der klassischen David-Skulptur mit Kryptomarktdaten; Verarbeitung der Idee, dass menschliche Wahrnehmung "zu Stein wird" dadurch und Grundlegung mit wissenschaftlichen Quellen.)  
  Das Werk sollte nicht nur ein visuelles Fest sein, sondern auch eine intellektuelle Herausforderung, die zum Nachdenken über **Wissenschaft, Philosophie oder Technologie** anregt.

> [!IMPORTANT]
> **Referenzbeispiel (Las Palmitas-Effekt):** Im kriminalitätsgeplagten Viertel Las Palmitas in Mexiko wurden über 200 Häuser in ein massives Regenbogenspektakel verwandelt. Als Ergebnis dieser ästhetischen Intervention sanken die Kriminalitätsraten im Viertel in gewissem Maße, und Jugendliche begannen sich mit Kunst statt mit Gangs zu beschäftigen. Ästhetische Veränderung kodierte den Respekt der Menschen für ihre Umgebung und füreinander neu (Sozialer Zusammenhalt).
>
> **Erwartung:** Ein Projekt, das in die [PoArt]-Liste eintritt, muss, wie im obigen Beispiel, eine soziologische, wissenschaftliche oder philosophische Ursache-Wirkungs-Beziehung enthalten, die über reine visuelle Ästhetik hinausgeht. Da Zeit der einzige Vermögenswert ist, der nicht mit Geld gekauft werden kann, muss Zeit in diesem Protokoll durch Staking als Sicherheit bewiesen werden. Die konzeptionelle Grundlage des Projekts muss so stark und universell sein, dass selbst in einem möglichen CTO (Community Take Over)-Szenario Jahre später die Community das innovative Potenzial des Projekts autonom fortsetzen kann, indem sie dieses Erbe erbt.

### 5) Nicht-Algorithmischer Wille

- **Problem:** Perfekte, aber seelenlose digitale Produktionen, die sich gegenseitig wiederholen.
- **[PoArt]-Lösung:** Der einzigartige Wille des Menschen, der Fehler machen, Risiken eingehen und emotionale Schwankungen erleben kann, muss im Werk zu spüren sein. Die Unsicherheit in Pinselstrichen, unerwartete Reaktionen von Materialien und sofortige Entscheidungen des Künstlers sind die **Biologische Signatur**, die das Werk von "Maschinenproduktion" trennt.

---

## c) Verifizierungs- und Anti-Betrugs-Mechanismus

Dieses System garantiert, dass das Projekt nicht nur "am Anfang", sondern "für immer" zuverlässig und lebendig bleibt.

### 📦 Evidence Pack - Der Digitale Zwilling

Hinter jedem [PoArt]-zertifizierten Werk steht ein verschlüsseltes und zeitgestempeltes Datenpaket, das Investoren herunterladen können:

- **RAW-Videoaufnahmen:** Ununterbrochenes Rohmaterial des Produktionsmoments.
- **Metadaten-Analyse:** Dateierstellungsdatum, verwendete Geräteinformationen und Standortdaten.
- **Physische Referenzen:** Beweis, dass das Werk in der physischen Welt existiert  
  (Z.B., Aktuelle Zeitung oder Blockchain-Daten dieses Moments neben dem Werk).

> *Konsistenzhinweis:* Der Begriff "Evidence Pack" verbindet sich mit der Kette **Evidence Pack → EvidenceRoot → NotarySeal** in vorherigen Abschnitten; d.h. die Integrität des Pakets wird durch ein verifizierbares Siegel dargestellt.

### 🔄 365-Tage-Erneuerung (Das Nachhaltigkeitsprotokoll)

- **Revolutionäres Merkmal:** In Krypto-Projekten gibt der "Dev" (Entwickler) den Token heraus und verschwindet normalerweise nach 1-2 Monaten (Soft Rug). [PoArt] macht dies unmöglich.
- **Regel:** Der Status "Verifizierter Künstler" ist nicht lebenslang. Nur **1 Jahr** ist gültig.
- **Betrieb:** Künstler/Entwickler müssen der Community alle 365 Tage **ein neues, bedeutendes und nachweisbares Werk** präsentieren.
- **Beispielszenario:** Sie haben das Projekt 2026 gestartet. Im Januar 2027 gibt das System eine Warnung "Nachweiszeitraum Abgelaufen". Wenn der Künstler keine neue Ausstellung, kein neues physisches Werk oder keine neue technologische Integration präsentiert, fällt das "Vertrauensabzeichen" des Projekts.
- **Ergebnis:** Dieses System garantiert, dass **Inhalt nie an Relevanz verliert** und der Investor nie die Angst *"Ist der Entwickler noch da?"* erlebt. Das Projekt wird zu einem lebenden Studio.

### 🚩 Rote-Flagge-Protokoll

**Im Falle von Betrug, der von der Community oder Algorithmen erkannt wird (KI-Nutzung, gestohlenes Werk, manipuliertes Video):**

1. Das Zertifikat wird sofort als **"VOID" (UNGÜLTIG)** markiert.
2. Evidence Packs werden öffentlich als **"Gefälscht"** gekennzeichnet.
3. Das Projekt wird auf die [PoArt]-Schwarze Liste gesetzt. Dies verstärkt, dass in einer dezentralen Welt **Reputation die einzige Währung ist**.

---

## d) Schlussfolgerung: Kein Casino, Sondern ein Museum

**Pump.fun und Dezentrale Börsen (DEX) sind leider gerade Casinos; Lichter blinken, alle jagen schnellen Gewinnen nach, und das Haus (Betrüger) gewinnt immer. Der Grund, warum wir das Projekt hier gestartet haben, ist der Mangel an ausreichendem Budget und eine Umgebung, um das bestehende Publikum über Live-Streams zu erreichen.**

**[PoArt] ist eine Festung, die mitten in diesem Casino gebaut wurde.**

- 🎰 Das Casino basiert auf Kartenspielen; wir basieren auf **physischer Realität**.
- 🃏 Das Casino ist offen für Betrug; wir sind offen für **transparente Beweise**.
- ⏳ Das Casino ist temporär; wir konzentrieren uns auf **die Ewigkeit von Kunst und Wissenschaft**.

**Ein Token, der dieses Protokoll verwendet, ist nicht nur eine "Münze"; es ist digitales Eigenkapital, das Schweiß, Farbe, Code und Philosophie enthält.**

---

## 🗳️ 6) GOVERNANCE UND ÖFFENTLICHES REGISTER

**Der Zweck dieses Abschnitts ist: den [PoArt]-Standard von der Ebene "Vertrauen in Einzelpersonen" in eine nachhaltige öffentliche Infrastruktur mit Register + Verifizierung + Community-Aufsicht zu transformieren.**

### 6.1 Öffentliches Register

- **Öffentliches Register:** Alle genehmigten Daten werden unter `ilhanart.org/registry` (oder GitHub Registry) aufgezeichnet.

**Registerlogik (empfohlener Standard - im JSON-Pfadformat):**

Jeder Eintrag, der in das Register eingeht, trägt diese minimalen verifizierbaren Kernfelder:

- **Identität & Status:**
  - `certificate_id` (lesbare Referenz)
  - `status` (active / void)
  - `void_reason` (falls zutreffend)
  - `visibility` (private / masked / public)
  - `created_at` (Zeitstempel)

- **Ausstellende Institution:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Werkinformationen:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (falls möglich; für Token-gesteuerte Identität)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Forensische Daten:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Kryptografische Beweise:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Governance:**
  - `governance.decision`
  - `governance.veto_threshold`

Das Register kann zwei Ebenen haben:
- **1)** Menschenlesbarer Index (Web-Listing / Suche / Filter)
- **2)** Maschinenlesbares Manifest (JSON-Einträge; für PFE-Verifizierung)

**Dieser "Eintrag" wird durch die Evidence Pack → EvidenceRoot → NotarySeal-Kette von PFE verifizierbar. Das Register bietet Verifizierungsziele, nicht "Behauptungen".**

---

### 6.2 40% Community-Veto (Token-Gesteuerte Governance)

- **40% Community-Veto:** Die Abstimmung beginnt einen Monat vor der Statuserteilung; 40% Widerspruch der **Token-Gesteuerten (Solana-Verifizierten)** Community macht den Antrag ungültig.

**Abstimmungsablauf (empfohlener klarer Prozess):**
- **Antragsfenster:** Das Kandidatenprojekt öffnet "PoArt-Kandidatenregistrierung" (Kandidatenregistrierungen erscheinen im Status "ausstehend").
- **Prüfungszeitraum:** Die Community prüft 30 Tage lang Beweise (Evidence Pack + Live-Stream-Aufzeichnungen + Metadaten).
- **Token-gesteuerte Verifizierung:** Die Abstimmung erfolgt mit Solana-verifizierten Wallets (z.B. spezifischer Token/NFT-Besitz + Wallet-Signatur).
- **Veto-Regel:** Wenn 40% der Stimmen **Widerspruch (NEIN / VETO)** sind, wird der Antrag abgelehnt.
- **Transparenz:** Das Abstimmungsergebnis wird im Register als "Entscheidungseintrag" gespeichert (Datum, Verhältnis, Snapshot-ID).

---

### 6.3 Metadaten-Synchronisation (Ausrichtung mit der Physischen Welt)

- **Metadaten-Synchronisation:** Technische Daten im Register müssen zu 100% mit der physischen Entität übereinstimmen.

**Technische Definition von "100% Übereinstimmung" (empfohlene Klarheit):**
- **Minimale Übereinstimmung (obligatorisch):**
  - `asset.fingerprints.sha256/sha512` im Register muss **identisch** mit dem Hash der vorliegenden Datei sein.
  - Wenn `proof.notary_seal` im Register reproduziert wird (falls Evidence Pack existiert), muss es **identisch** sein.
- **Physische Referenzübereinstimmung (Beweistyp):**
  - Physisches Werk + Datums-/Blockreferenz im Live-Stream gezeigt und ähnliche Beweise müssen mit dem Evidence Pack konsistent sein.
- **Datenschutz-Compliance:**
  - Felder wie IP/Standort in `masked`-Sichtbarkeit werden **gemäß Maskierungsstandards** veröffentlicht.

---

### 6.4 Streit und Widerruf

Das Register ist nicht nur ein "Genehmigungs"-Mechanismus; es ist ein **lebendiger Audit-Mechanismus gegen Betrug**.

- Wenn ein Streit eingeleitet wird, kann der Eintrag in den **"review"**-Modus versetzt werden.
- Wenn Betrug festgestellt wird, wird er als `status: void` markiert mit hinzugefügtem Grund:
  - `void_reason` (KI-Nutzung / Diebstahl / Manipulation usw.)
  - `revoked_at` (Widerrufszeit)
- Die Quelle der Widerrufsentscheidung ist im Register deutlich sichtbar:
  - Community-Abstimmung / autorisiertes Komitee / forensische Untersuchungsnotiz (was zutrifft)

> **Dieser Abschnitt ist das Register-Gegenstück zum VOID-Konzept im Abschnitt "Rote-Flagge-Protokoll".**

---

### 6.5 Beispiel-Registereintrag (Maschinenlesbar)
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
> *Hinweis: `asset.fingerprints.sha512` und andere Hash-Werte sind zu Anzeigezwecken abgekürzt; in der tatsächlichen Implementierung werden vollständige hexadezimale Zeichenketten verwendet.*

---

## 7) 🔐 TECHNISCHES SIEGEL (NOTARY SEAL)

Der unerschütterliche Siegelalgorithmus, generiert von **PoArt Forensic Engine (PFE) v1.0**:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Digitales Notar- & Forensisches Beweisprotokoll (Beta v1.0)

> **"Kultur ist größer als Kapital. Schütze deine Werke heute, trage sie in morgen."**

---

## Warum Öffentlich?

Wahre Sicherheit kommt von Transparenz. Dank unseres **Öffentlichen Register**-Systems kann jeder überall auf der Welt in Sekunden überprüfen, ob eine Datei original ist, ohne Autorität zu benötigen.

---

## 🧩 Warum Mehrere "Sichtbarkeitsmodule"?

Dies ist der kritischste Teil des Codes (Sichtbarkeitsauswahlmenü). Diese Optionen ermöglichen es Benutzern, **"Privatsphäre vs. Transparenz"** auszubalancieren:

### 🔒 Privat

- **Szenario:** Der Künstler möchte das Werk noch nicht veröffentlichen, aber möchte es zeitstempeln, um zu beweisen "ich habe dies an diesem Datum gemacht".
- **Was der Code Macht:** Schreibt Daten in die Datenbank, stempelt aber `visibility: "private"`. Später beim Schreiben der "Public Read"-Richtlinie können Sie diese Einträge mit `WHERE visibility = 'public'` vor der Öffentlichkeit verbergen.

### 🕶️ Maskiert

- **Szenario:** Der Künstler möchte Transparenz, aber befürchtet, dass seine Heimadresse (IP-Standort) gefunden wird.
- **Was der Code Macht:** `maskIP`- und `maskLoc`-Funktionen arbeiten auf der JavaScript-Seite. Konvertiert die IP-Adresse in das Format `88.241.***.***`, den Standort in das Format `***/TR`, und sendet die zensierte Version an die Datenbank.
- **Datenschutzhinweis:** Die Maskierung erfolgt im Browser, Supabase sieht den echten Standort nicht. **Jedoch:** Wenn Drittanbieter-APIs wie ipapi.co für Standortdaten verwendet werden, sehen diese Anbieter die IP-Adresse zum Zeitpunkt der Anfrage.
- **Versiegelung im Maskierten Modus:** EvidenceRoot- und NotarySeal-Berechnung erfolgt mit maskierten forensischen Daten; somit bleibt die Verifizierung deterministisch.

### 🌍 Öffentlich

- **Szenario:** Volle Transparenz. Gemäß [PoArt]-Standards wird klar erklärt, wo, wann, aus welchem Netzwerk das Werk produziert wurde.

---

## 💡 Technologische Innovation

PoArt ist nicht nur ein Datei-Upload-System. Es ist eine **"Forensische Gewahrsams-Kette"**-Engine, die einen neuen Standard bringt, indem sie drei verschiedene Technologieebenen in einem Topf verschmilzt.

**Die in diesem Abschnitt als "Engine" beschriebene Ebene entspricht dem PoArt Forensic Engine (PFE)-Kern in der vorherigen Terminologie.**

### 1) Client-Side Hashing (Maximale Privatsphäre)

Ihre Kunstwerkdateien werden niemals auf den Server hochgeladen. Unsere browserbasierte (Client-Side)-Engine berechnet den Hash (digitalen Digest) der Datei auf Ihrem eigenen Computer. Nur dieser Fingerabdruck und Metadaten werden an den Server gesendet.

> **Datenschutzhinweis:** Die Werkdatei wird nicht auf den Server hochgeladen und ist auf diese Weise geschützt. Forensische Daten (IP/Standort) werden jedoch gemäß dem ausgewählten Sichtbarkeitsmodus (privat/maskiert/öffentlich) geteilt.

### 2) Forensische Datenfusion (Forensische Kraft)

Weit mehr als ein gewöhnlicher Zeitstempel. Das System kombiniert diese Daten in einem einzigen "Genesis-Siegel":

- **Digitaler Digest (SHA-512):** Digitaler Fingerabdruck mit kryptografischem Digest (SHA-512)-Standard, der bricht, wenn sich auch nur ein Pixel des Werks ändert.
- **Standort & Zeit:** Millisekundengenaues Datum, Land, Stadt und Bezirksdaten der Transaktion.
- **Geräteidentität:** Betriebssystem, Browser und Gerätetyp (User-Agent-Analyse).

---

## 🛡️ Anwendungsfälle und Vorteile

Wenn Sie Künstler, Schriftsteller oder Designer sind, reicht es nicht zu sagen "Ich habe dies früher gemacht"; Sie müssen es beweisen.

**Ein Werk, das Sie mit PoArt versiegeln:**

- **Mathematischer Beweis:** Wenn sich auch nur ein Pixel Ihrer Datei ändert, weiß das System es. Manipulation ist unmöglich.
- **Rechtliche Grundlage:** An welchem Datum, in welcher Stadt, von welchem Gerät das Werk versiegelt wurde, ist aufgezeichnet.
- **Sofortiges Zertifikat:** Generiert in Sekunden ein spezielles, QR-codiertes und versiegeltes **"Asset-Identitätszertifikat"** für Sie.

---

## ⚙️ Systemarchitektur und Technische Merkmale

Das System ist auf einer "Serverlosen" Architektur konzipiert, mit Fokus auf hohe Leistung und Skalierbarkeit.

| Ebene | Technologie | Beschreibung |
|--------|-----------|----------|
| **Kryptografie** | SHA-256 & SHA-512 | Doppelschichtiger kryptografischer Digest |
| **Datenbank** | Supabase (PostgreSQL) | JSONB-Datenstruktur, RLS-Richtlinien |
| **Forensische Daten** | ipapi.co API | IP/Standort/Zeit-Trinität |
| **Rendering** | html2canvas + jsPDF | Client-Side PNG/PDF-Generierung |
| **Frontend** | Vanilla JavaScript | Null Framework-Abhängigkeit |
| **Sicherheit** | Client-Side Hashing | Datei geht nie zum Server |

### Herausragende Merkmale

| Funktion | Detail | Bei Konkurrenten? |
|---------|-------|-----------------|
| **Drag & Drop UI** | Datei ziehen & ablegen, Sofortvorschau | ❌ Bei den meisten fehlend |
| **Multi-Format-Export** | PNG, JSON, PDF - ein Klick | ⚠️ Begrenzt |
| **Echtzeit-Vorschau** | Live-Zertifikatsvorschau | ❌ Keine |
| **Datenschutzkontrollen** | Privat/Maskiert/Öffentlich-Optionen | ❌ Keine |
| **Client-Side Hash** | Datei geht nie zum Server | ✅ Nur bei einigen |
| **Forensische Metadaten** | IP, Standort, Gerät, Zeit - alles zusammen | ❌ Fragmentiert |
| **QR-Verifizierung** | Sofortiger Verifizierungs-QR-Code | ⚠️ Begrenzt |
| **Rate Limiting** | Spam-Schutz (RLS + Client) | ❌ Bei den meisten fehlend |

---

## 🗺️ Roadmap: "Vertrauenslose" Zukunft

Die aktuelle Version **(Beta v1.0)** ist optimiert, um Endbenutzern maximale Geschwindigkeit, einfache Benutzeroberfläche und kostenlosen Zugang zu bieten. Unsere ultimative Vision ist jedoch der Übergang zu einer Struktur, in der selbst der Datenbankadministrator (wir) nicht eingreifen kann.

### Phase 1: Beta (Derzeit Live)

- **Infrastruktur:** Cloud-Datenbank (Supabase).
- **Zweck:** Geschwindigkeit, Beseitigung von UX (User Experience)-Barrieren und Anpassung. Bereitstellung "reibungsloser" Sicherheit.

### 🚀 Phase 2: (Backend / Edge Function Anforderungen)

Diese Phase umfasst den Übergang von der vollständig "Client-Side" arbeitenden Struktur zu einer sichereren und verwaltbareren "Server-Side Authority"-Struktur.

| Element | Was Bringt Es? | Tech Stack | Priorität |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Function** | Spam-Verhinderung + API-Key-Sicherheit | Supabase Edge (Deno) | 🔴 Hoch |
| **Wallet-Signatur** | Kryptografische Authentifizierung | Solana Wallet Adapter | 🟡 Mittel |
| **IPFS/Arweave Backup** | Dezentrale Unveränderlichkeit | IPFS SDK + Pinata | 🟢 Niedrig |
| **Widerrufsmechanismus** | Gefälschte Zertifikatsstornierung | DB Schema Update | 🔴 Hoch |
| **Audit-Log** | Forensischer Abfragedatensatz | Benutzerdefinierte Logs-Tabelle | 🟡 Mittel |
| **OpenTimestamps** | Bitcoin-Verankerung | OTS JavaScript | 🟢 Niedrig |
| **DID-Integration** | Dezentrale Identität | ION/Ceramic | 🟢 Niedrig |

### Phase 3: Vollständige Dezentralisierung (Langfristig)

| Funktion | Ziel | ETA |
|---------|------|-----|
| **Blockchain-Register** | Ethereum/Solana On-Chain-Registrierung | Q4 2026 |
| **DAO-Governance** | Community-Verwaltung | Q1 2027 |
| **Multi-Chain-Unterstützung** | Polygon, Arbitrum, Base | Q2 2027 |
| **Rechtliche Anerkennung** | Gültigkeit in türkischen Gerichten | 2027-2028 |
| **API für Entwickler** | Öffentlicher API-Endpunkt | Q3 2026 |

---

## 📊 Wettbewerbsanalyse (Aktualisiert)

PoArt ist auf dem "Sweet Spot" positioniert, der die Mängel bestehender Lösungen vervollständigt.

| Funktion | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Kosten** | 🆓 Kostenlos | 🆓 | 💰 Bezahlt | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Sehr Einfach | ❌ CLI | ⚠️ Mittel | ⚠️ Mittel | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format-Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Echtzeit-Vorschau** | ✅ Live | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Datenschutzkontrollen** | ✅ 3 Modi | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Privatsphäre | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensische Metadaten** | ✅ Vollständig | ❌ | ❌ | ⚠️ Begrenzt | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR-Verifizierung** | ✅ Sofort | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain-Verankerung** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Türkische Unterstützung** | ✅ Nativ | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Legende:**
- ✅ : Volle Unterstützung / verfügbar
- ⚠️ : Begrenzt / in bezahlten Plänen
- ❌ : Keine / nicht unterstützt
- 🔄 : In der Roadmap (in Entwicklung)
- 🆓 : Vollständig kostenlos
- 💰 : Bezahlt / Abonnement erforderlich

### Mängel der Konkurrenten, Stärken von PoArt

| Minus | Konkurrenten | PoArt |
|-------|-------------|-------|
| **Nutzungsschwierigkeit** | CLI, API-Kenntnisse, Wallet erforderlich | Ziehen & Ablegen, fertig in 3 Klicks |
| **Kostenbarriere** | $50-500/Monat Abonnement | 100% kostenlos |
| **Privatsphäre** | Datei wird auf Server hochgeladen | Client-Side, Datei geht nie |
| **Forensische Daten** | Nur Zeitstempel | IP, Standort, Gerät, Zeit - alles |
| **Türkische Unterstützung** | Keine oder sehr begrenzt | Native Sprachunterstützung |
| **Open Source** | Geschlossene Box | Gesamter Code offen auf GitHub |

---

## 🧬 Protokoll-Datenstruktur (JSON Schema)

**Jedes [PoArt]-Zertifikat hat eine portable und verifizierbare JSON-Identitätskarte, die im folgenden Standard produziert wird.**

> **Hinweis:** Dieses Identitäts-JSON-Format ist das Zertifikatsformat, das Benutzern präsentiert wird. In Registereinträgen wird `registry.asset` anstelle von `identity.asset_data` verwendet (Mapping: `identity.asset_data` == `registry.asset`).
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

## 🔬 Technische Tiefe: Siegelalgorithmus

### Deterministische Hash-Funktionen
```javascript
// Hilfsfunktionen: Digest in Hex-String umwandeln
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// String in Byte-Array umwandeln
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Kanonische forensische String-Generierung (v1.0: feste Feldreihenfolge + UTF-8 + \n Delimiter)
// Phase 2 Hinweis: Übergang zu kanonischem JSON mit RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal-Produktionsprozess (Vollständig Deterministisch)
```javascript
// 1. FileHash-Berechnung (Client-Side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Forensische Datensammlung (einzelne Zeitstempelverwendung)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Einzelne Zeitstempelgenerierung
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Gleicher Zeitstempel
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot-Erstellung (mit kanonischer Kodierung)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal-Generierung (gleiche Zeitstempelverwendung)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Maskierungs-Hilfsfunktionen (IPv4- und IPv6-Unterstützung)
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4-Prüfung
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 oder unbekanntes Format
  return "***";
}
```

### Verifizierungsablauf (Zwei Ebenen)

#### Quick Verify (Schnellverifizierung)
```javascript
// Überprüft nur den Datei-Hash (schnelle rote Flagge)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Aus Register abrufen
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Hash-Vergleich
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Original - Datei-Hash stimmt überein"
    };
  } else {
    return {
      valid: false,
      message: "❌ Fälschung - Datei wurde manipuliert"
    };
  }
}
```

#### Full Verify (Vollständige Verifizierung)
```javascript
// Regeneriert und verifiziert EvidenceRoot und NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Aus Register abrufen
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash-Überprüfung (schnelle rote Flagge)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Fälschung - Datei-Hash stimmt nicht überein" };
  }

  // 2) EvidenceRoot regenerieren (mit im Register gespeicherten forensischen Daten)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Stimmt nicht überein - EvidenceRoot hält nicht" };
  }

  // 3) NotarySeal regenerieren (mit gleichem Zeitstempel + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Stimmt nicht überein - NotarySeal hält nicht" };
  }

  // Optional: In Phase 2 auch signer_sig mit attestation_pubkey verifizieren
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Ungültige Signatur" };

  return { valid: true, message: "✅ Original - Vollständige Verifizierung bestanden" };
}
```

> **Wichtige Hinweise:**
> - **Quick Verify:** Überprüft nur den Datei-Hash für schnelle Verwendung.
> - **Full Verify:** Verifiziert alle Ebenen des Protokolls (EvidenceRoot + NotarySeal).
> - Alle Hash-Operationen werden deterministisch mit fester Kodierung und Delimitern durchgeführt.
> - **v1.0 Kanonisierungsstandard:** Feste Feldreihenfolge + UTF-8-Kodierung + `\n` Delimiter.
> - **Phase 2 Plan:** Übergang zu kanonischem JSON mit RFC 8785 (JCS - JSON Canonicalization Scheme).
> - Im maskierten Modus werden EvidenceRoot- und NotarySeal-Berechnungen mit maskierten forensischen Daten durchgeführt; somit bleibt die Verifizierung deterministisch.
> - Ein einzelner Zeitstempel wird im gesamten Prozess verwendet (forensisch + NotarySeal); Determinismus ist garantiert.
> - **Forensische Feldnamen:** `ip_masked`, `location`, `device`, `timestamp` (Code und Register vollständig kompatibel).
> - **Registerpfad:** `certificate.asset.fingerprints` (vollständig kompatibel mit Verifizierungscode).
> - **signer_sig im Register:** Das Feld `proof.signer_sig` ist für Full Verify erforderlich.
> - Der SignerSignature-Mechanismus wird in Phase 2 mit Solana Wallet Adapter aktiviert; in v1.0 kann die Verifizierung mit `attestation_pubkey` durchgeführt werden.

---

## 📈 Nutzungsstatistiken (Q1 2026 Ziele)

| Metrik | Ziel | Status |
|--------|--------|--------|
| **Gesamtzertifikate** | 1,000 | 🔄 Fortschritt |
| **Aktive Benutzer** | 500 | 🔄 Fortschritt |
| **Verifizierungsanzahl** | 5,000 | 🔄 Fortschritt |
| **Betriebszeit** | 99.9% | ✅ Aktiv |
| **Durchschn. Antwortzeit** | <200ms | ✅ Optimal |

---

## 🌍 Community & Support

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 Mitwirkende

Das PoArt-Protokoll entwickelt sich weiter mit Beiträgen der Open-Source-Community.

**Um beizutragen:**
1. Fork das Repository
2. Erstelle einen Feature-Branch (`git checkout -b feature/amazing-feature`)
3. Commit (`git commit -m 'Add amazing feature'`)
4. Push (`git push origin feature/amazing-feature`)
5. Öffne einen Pull Request

### 🛠️ Was Brauchen Wir Jetzt? (Hilferuf)

Das PoArt-Protokoll sucht erfahrene Entwickler in den folgenden Bereichen für **Phase 2**-Entwicklungen:

* **Supabase Edge Functions:** Spam-Schutz auf die Serverseite verschieben.
* **Solana Web3.js:** Wallet-Signaturintegration.
* **IPFS / Arweave:** Archivierungs- und Pinning-Dienste-Integration.

> Bitte starten Sie eine Diskussion im "Issues"-Tab, bevor Sie eine Funktion hinzufügen.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Kultur > Kapital"*

## 🧾 Lizenz

MIT-Lizenz © 2026 İlhan Art Gallery Initiative

Siehe [![Lizenz](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) für vollständige Bedingungen.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Sicherheit](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Plattform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![Lizenz](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Dieses Projekt wird von der [İlhan Art Gallery]-Initiative entwickelt, und seine Quellcodes sind öffentlich für Transparenz verfügbar.**

**PROTOKOLL V1.0 // VERSIEGELT MIT SHA-512**

*© 2026 İLHAN ART | ALLE RECHTE FÜR KUNSTWERKE, VISUALS UND IDEEN VORBEHALTEN.*

---
