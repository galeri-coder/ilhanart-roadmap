# 📚 GLOSSAR DER TERMINOLOGIE UND KONZEPTE
> **"Die Sprache dieses Protokolls zu verstehen bedeutet, seine Vision zu verstehen."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Kerninfrastruktur

**PoArt Forensic Engine (PFE)** ist die Hauptschicht, die die Kernlogik und den technischen Betrieb hinter dem [PoArt]-Protokoll repräsentiert. Dies ist der "forensische Motor", der die Rohproduktionsdaten des Kunstwerks nimmt und sie in einen verifizierbaren und unveränderlichen **digitalen Beweis** verwandelt.

### 🧩 Warum "PoArt Forensic"?

- **PoArt (Proof of Art):** Der Fokus des Motors liegt darauf, den Wert eines digitalen Vermögenswerts nicht an Spekulation, sondern an den **nachweisbaren Produktionsprozess** zu binden.
- **Forensic (Forensische Verifizierung):**
  - **Technische Definition:** Algorithmischer und Aufzeichnungsketten-Ansatz zur Verifizierung, dass Daten des Produktionsprozesses (Pinselstriche, Timelapse, Logs) nicht manipuliert wurden.
  - **Philosophische Ebene:** Die Behauptung, die menschliche Produktion, die **Zeit, Aufwand und Entscheidungskosten** enthält, in eine messbare Realität zu verwandeln, im Gegensatz zur "sofortigen Ausgabe"-Produktion der Künstlichen Intelligenz.

> Hinweis: Blockchain-Integration (z.B. Solana) ist nicht der Kern von PFE; sie wird als separate **Chain Anchor Layer** behandelt, die für Verifizierung/Registry definiert wird.

### 🛠️ Technischer Umfang v1.0

**PoArt Forensic Engine (PFE) v1.0** ist auf diesen **3 Hauptsäulen** aufgebaut, anstatt auf komplexen Finanzmodellen:

1. **Hashing & Sealing (Versiegelung):**  
   PFE verarbeitet deterministisch alle Elemente im Evidence Pack (Werkdatei, Video, JSON/Logs, Signatur usw.) und erzeugt den einzigartigen **NotarySeal**-Wert.

   **Kernkonzepte (v1.0):**
   - **FileHash (Werk-Fingerabdruck):** Hash, der aus den Bytes der Werkdatei generiert wird.
   - **EvidenceRoot (Beweispacket-Wurzel):** Wurzelzusammenfassung, die die Integrität des Evidence Pack repräsentiert (Merkle Root oder kanonischer Manifest-Hash).
   - **NotarySeal (finales Siegel / PFE-Ausgabe):** Finales Siegel, das aus der Kombination von EvidenceRoot + Zeit + Signatur generiert wird.

   **Formeln (klar für Investoren sichtbar):**
   
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
   
   > Hinweis: Der als PFE-Ausgabe gemeinte Wert ist **NotarySeal**. Der **SignerSignature**-Mechanismus wird in Phase 2 (mit Solana Wallet Adapter) aktiviert; in der aktuellen v1.0 wird die Attestation-Signatur des Systems selbst verwendet. Der Attestation Public Key wird im Registry-Feld `issuer.attestation_pubkey` veröffentlicht.

2. **Indexing (Archivierung):**  
   Verarbeitet in einer transparenten und abfragbaren Aufzeichnungsschicht, welche Wallet, zu welchem Datum, welchen **Labor Proof (Arbeitsnachweis)** für welches Werk vorgelegt hat.  
   *(Diese Schicht kann eine Datenbank sein; Chain-Integration wird separat als "Chain Anchor Layer" definiert.)*

3. **Verification (Verifizierung):**  
   Wenn die Authentizität eines Werks in Frage gestellt wird, verarbeitet PFE die Rohbeweise erneut; testet mit mathematischer Gewissheit, ob die berechneten **EvidenceRoot / NotarySeal**-Werte mit dem Eintrag im Archiv übereinstimmen.

---

### 🧮 PoArt-Werttheorem (The Value Theorem)

Das [PoArt]-Protokoll verknüpft den Wert ($V$) eines digitalen Vermögenswerts nicht mit der subjektiven Marktwahrnehmung, sondern mit **der physischen Realität des Produktionsprozesses**.

Künstliche Intelligenz (KI) zerstört den Prozess, indem sie das Ergebnis sofort liefert ($t \to 0$). [PoArt] hingegen behandelt den Wert als Akkumulation der Komponenten **Zeit, Arbeit und Wille**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definition der Variablen

- **$\int dt$ (Prozessakkumulation):**  
  Wert ist keine sofortige "Ausgabe" (Output); es ist ein **Prozess**, der sich zwischen $t_{\text{start}}$ und $t_{\text{end}}$ akkumuliert. Wenn die Dauer abnimmt (KI-Produktion), nähert sich das Ergebnis des Integrals 0.

- **$P_{\text{labor}}(t)$ (Momentane Arbeitskraft):**  
  Repräsentiert die Intensität der mentalen und physischen Anstrengung, die im Moment der Produktion aufgewendet wird. Wenn die nachweisbare Anstrengung zunimmt, wächst der Integrand.  
  > Hinweis: Dieser Term kann in der Praxis durch "messbare/nachweisbare Arbeitssignale" normalisiert werden.

- **$I_{\text{agency}}(t)$ (Willenskoeffizient):**  
  Ist die Fähigkeit des Produzenten, Risiken einzugehen und Entscheidungen zu treffen. Nimmt einen Wert zwischen $0$ und $1$ an.
  - **KI ($I \approx 0$):** Führt Befehle aus, geht keine Risiken ein, zahlt keinen Preis.
  - **Mensch ($I \to 1$):** Ändert Entscheidungen, zögert, geht Risiken ein.

- **$U_{\text{irreversible}}$ (Irreversible Singularität):**  
  Während in der digitalen Produktion Rückgängigmachen möglich ist (`Strg+Z`); gibt es in der physischen Produktion (auf Leinwand aufgetragene Farbe, gemeißelter Marmor, Geste in Live-Übertragung) kein Zurück. Diese **Irreversibilität** ist ein zusätzlicher Term, der "Singularität" (non-fungiblen Charakter) im Werk schafft.

### 🔎 Fallanalyse: KI "Sofortige Ausgabe" vs. Mensch "Nachgewiesener Prozess"

Das folgende Szenario zeigt, wie das **PoArt-Werttheorem** in der Praxis funktioniert und warum KI-Produktionen im [PoArt]-Standard niedrige Punktzahlen erhalten.

#### Szenario A: Visuelle Produktion mit KI in 10 Sekunden

- **Dauer ($\Delta t$):** $10$ Sekunden (Prozess fast nicht vorhanden)
- **Arbeitskraft ($P_{\text{labor}}$):** $1$ Einheit (nur Befehl schreiben)
- **Willenskoeffizient ($I_{\text{agency}}$):** $0.01$ (kein Risiko, keine Kosten)
- **Irreversibilität ($U_{\text{irreversible}}$):** $0$ (reversibel / kopierbar)

**Ergebnis:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Kommentar:** Auch wenn die Ausgabe perfekt ist; da der Prozess nicht erlebt wurde und kein Wille/Risiko enthält, nähert sich der [PoArt]-Wert $0$.

#### Szenario B: 6-stündige physische Produktion in Live-Übertragung

- **Dauer ($\Delta t$):** $6$ Stunden ($21{,}600$ Sekunden)
- **Arbeitskraft ($P_{\text{labor}}$):** $0.5$ Einheiten (Kontinuität der physischen und mentalen Anstrengung)
- **Willenskoeffizient ($I_{\text{agency}}$):** $0.9$ (Entscheidungsänderungen, Risikobereitschaft, irreversible Entscheidungen)
- **Irreversibilität ($U_{\text{irreversible}}$):** $>0$ (physische Spuren irreversibel)

**Ergebnis:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Kommentar:** Wenn sich der Prozess verlängert und der Wille (Risiko) zunimmt, steigt der Wert kumulativ. Der Term $U_{\text{irreversible}}$ ist ein zusätzlicher Beitrag, der "Singularität" (non-fungiblen Charakter) im Werk schafft.

---

### ✅ Fazit: An Beweis Gebundener Wert (Proof-Bound Value)

Dieses Theorem bringt die Wertbehauptung von [PoArt] aus einem "Geschmack" oder einer "Marktnarrative" heraus und bindet sie an eine **nachweisbare Produktionsrealität**.

1. **Ohne Prozess Kein Wert:**  
   KI zerstört den Prozess mit sofortiger Ausgabe ($t \to 0$). Wenn sich das Prozessfenster verengt, verkleinert sich das Ergebnis des Integrals durch mathematische Notwendigkeit:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Wille und Risiko sind Multiplikatoren:**  
   [PoArt] misst nicht nur die "aufgewendete Zeit", sondern auch die tatsächliche Schicht von Entscheidung, Risiko und Kosten in dieser Zeit. Der Wert einer Produktion ohne Risiko (KI) ist niedrig:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Singularität ist ein Physischer Beweis, Kein Marketing:**  
   Irreversible Spuren in der physischen Produktion (Pinselstrich auf Leinwand, Marmorbruch) liegen außerhalb der Logik des digitalen `Strg+Z`. Diese Irreversibilität ($U_{\text{irreversible}}$) singularisiert das Werk ontologisch.

> **🔐 ZUSAMMENFASSUNG:** Auch wenn das Werttheorem als Messung unbestimmt erscheinen mag (auch wenn es im realen Leben nicht zu 100% gemessen werden kann), ist der Zweck dieser Formel, die Konstruktion und Richtung der Variablen zu zeigen. Im KI-Zeitalter ist das Seltene nicht das "Bild"; es ist die **nachweisbare Arbeit, Zeit und Wille**. [PoArt] misst diese Knappheit und registriert sie mit dem **Evidence Pack**.

### 🏛️ Bedeutung des Konzepts "Engine" (Motor)

Token, die von Pump.fun oder ähnlichen Plattformen stammen, sind oft nur **"Zugangstickets"**. **PoArt Forensic Engine (PFE)** hingegen ist die **verfassungsmäßige Logikschicht**, die bestimmt, welche Rechte dieses Ticket schützt, wie Arbeit aufgezeichnet wird und wie Kunst/Wissenschaft/Technologie verewigt wird.

> **Hinweis:** Der Grund, warum wir dieses Projekt auf Pump.fun gestartet haben, ist, dass wir nicht über ausreichende Liquidität und Followerzahl verfügten. Die Nutzung der vorhandenen Daten war strategisch der richtige Zug, wenn auch nicht von höchster Qualität. Unabhängig von Budget und Möglichkeiten beweist die Definition der Logik dieses Motors auf GitHub, dass das Projekt nicht nur eine finanzielle Spekulation ist, sondern eine langfristige **Softwareinfrastruktur** und eine Vision einer **digitalen Nationalbibliothek**.

---

## 🎨 [PoArt] ARBEITSNACHWEIS-PROTOKOLL (Proof of Art Protocol v1.0)

> **"Echter Künstler, Echte Produktion, Echter Wert."**

Dieses Protokoll ist ein **biologischer und intellektueller Verteidigungsmechanismus**, der gegen anonyme Betrüger, die das Krypto-Ökosystem umgeben, in 5 Minuten produzierte KI-Bilder und die "Pump & Dump"-Kultur entwickelt wurde.

---

## a) Was ist [PoArt]? (Philosophische und Technische Definition)

**Proof of Art [PoArt];** ist ein institutioneller Verifizierungsstandard, der garantiert, dass der Wert hinter einem Vermögenswert auf der Blockchain nicht auf Spekulation, sondern auf verifizierbarer **menschlicher Arbeit**, **Zeit** und **physischer Energie** basiert.

So wie Bitcoin Wert mit *"Elektrizität und Prozessorleistung"* **(Proof of Work)** generiert, generieren [PoArt]-kompatible Projekte Wert mit *"Künstlerischem Talent und Menschlicher Zeit"*.

Eliminiert das Risiko von *"Der Entwickler (Dev) hat verkauft, Projekt beendet"* auf Pump.fun und DEX-Plattformen; denn hier liegt der Wert nicht im Code, sondern in der **Kontinuität der Produktion**.

> **[PoArt] sagt seinem Teilnehmer nicht "Vertrauen Sie uns"; es sagt "Hier sind die Beweise, sehen Sie mit Ihren Augen, verifizieren Sie mit Ihrer Mathematik".**

---

## b) [PoArt] 5-Säulen-Standard (The 5 Pillars of Truth)

Diese 5 Elemente sind nicht manipulierbare Filter, die ein Projekt passieren muss, um das [PoArt]-Siegel zu erhalten.

### 1) Live-Identitätsnachweis (Live Identity Proof)

- **Problem:** Die Kryptowelt ist voll von anonymen Gründern (Devs) mit unklarer Identität, die Geld sammeln und das Projekt verlassen.
- **[PoArt]-Lösung:** Der Produzent beweist nicht nur seinen Ausweis, sondern **seine Anwesenheit während der Produktion**. Dies beinhaltet Live-Übertragungssitzungen, in denen mit der Community interagiert wird und spezifische sofortige Anfragen erfüllt werden, nicht voraufgezeichnete Videos.  
  (Z.B.: *"Schreibe das heutige Datum und die aktuelle Blocknummer in die rechte Ecke der Leinwand"*)
- **Motto:** *"Bots können Bilder machen, aber Bots schwitzen nicht und improvisieren nicht."*

### 2) Arbeits- und Prozessnachweis (Labor & Process Proof)

- **Problem:** Dass in 2 Sekunden produzierte KI-Bilder (Künstliche Intelligenz) und in 2 Monaten erstellte Ölgemälde in der digitalen Welt dieselbe "JPEG"-Behandlung erhalten.
- **[PoArt]-Lösung:** Der "Schwangerschafts- und Geburtsprozess" des Werks wird aufgezeichnet. Skizzenstadien, Farbschichten, aufgewendete kumulative Stunden und der physische Prozess, den der Künstler bei der Schaffung dieses Werks durchlebte, werden dokumentiert. Dies fügt dem Token **"Zeitkosten" (Time Cost)** hinzu. Je schwieriger die Produktion eines Vermögenswerts ist, desto solider ist sein Wert.

### 3) Ästhetischer Wertnachweis (Aesthetic Value Proof)

- **Problem:** Dass die "Meme"-Kultur Ästhetik und künstlerische Tiefe ignoriert, sich nur auf sofortige Komödie konzentriert und daraus kurzlebige "Hype"-Projekte entstehen.
- **[PoArt]-Lösung:** Das Projekt muss akademische Kunststandards, Farbtheorie, Kompositionsregeln und Materialwissen (Impasto, Textur usw.) haben. Der Inhalt soll nicht nur zum Lachen bringen; er soll Bewunderung beim Betrachter wecken und **Sammlerwert** haben.

### 4) Konzeptionelle Innovation (Conceptual Novelty)

- **Problem:** Tausende von Hunde-/Katzen-Coins, die Kopien voneinander sind, fern von Kreativität.
- **[PoArt]-Lösung:** Das Projekt muss eine neue Brücke bauen, die Kunst, Wissenschaft, Philosophie oder Technologie in einer bedeutungsvollen Struktur verbindet.  
  (Z.B.: Die klassische David-Statue mit Krypto-Marktdaten zu verbinden; die Idee zu verarbeiten, dass die menschliche Wahrnehmung "versteinert" wird, und dies mit wissenschaftlichen Quellen zu begründen.)  
  Das Werk sollte nicht nur ein visuelles Fest sein; es sollte auch eine intellektuelle Herausforderung sein, die über **Wissenschaft, Philosophie oder Technologie** nachdenken lässt.

> [!IMPORTANT]
> **Referenzbeispiel (Las Palmitas-Effekt):**  
> Im mexikanischen Viertel Las Palmitas, das mit Kriminalität kämpfte, wurden über 200 Häuser in ein riesiges Regenbogenfest verwandelt. Als Ergebnis dieser ästhetischen Intervention sanken die Kriminalitätsraten im Viertel in gewissem Maße, Jugendliche begannen sich für Kunst statt für Banden zu interessieren. Die ästhetische Veränderung hat den Respekt der Menschen gegenüber ihrer Umgebung und untereinander (Sozialer Zusammenhalt) neu kodiert.
>
> **Erwartung:** Ein Projekt, das in die [PoArt]-Liste eintreten wird; sollte wie im obigen Beispiel eine soziologische, wissenschaftliche oder philosophische Ursache-Wirkungs-Beziehung über die reine visuelle Ästhetik hinaus enthalten. Da der einzige Vermögenswert, der nicht mit Geld gekauft werden kann, "Zeit" ist, muss in diesem Protokoll Zeit als Garantie gestaked und bewiesen werden. Die konzeptionelle Grundlage des Projekts muss so stark und universell sein, dass die Community dieses Erbe übernehmen und das innovative Potenzial des Projekts autonom fortsetzen kann, selbst in einem möglichen CTO (Community Take Over)-Szenario Jahre später.

### 5) Nicht-Algorithmischer Wille (Non-Algorithmic Agency)

- **Problem:** Perfekte, aber seelenlose digitale Produktionen, die sich wiederholen.
- **[PoArt]-Lösung:** Der authentische Wille des Menschen, der Fehler machen, Risiken eingehen und emotionale Schwankungen erleben kann, muss im Werk spürbar sein. Die Unsicherheit in den Pinselstrichen, die unerwarteten Reaktionen des Materials und die spontanen Entscheidungen des Künstlers sind die **Biologische Signatur**, die das Werk von "Maschinenproduktion" unterscheidet.

---

## c) Verifizierungs- und Anti-Fälschungsmechanismus

Dieses System gewährleistet, dass das Projekt nicht nur "am Anfang", sondern "für immer" vertrauenswürdig und lebendig bleibt.

### 📦 Beweispaket (Evidence Pack - The Digital Twin)

Hinter jedem [PoArt]-zertifizierten Werk befindet sich ein verschlüsseltes und mit Zeitstempel versehenes Datenpaket, das Investoren herunterladen können:

- **RAW-Videoaufnahmen:** Ununterbrochene Rohaufnahmen des Produktionsmoments.
- **Metadatenanalyse:** Erstellungsdatum der Datei, verwendete Geräteinformationen und Standortdaten.
- **Physische Referenzen:** Beweis, dass das Werk in der physischen Welt existiert  
  (Z.B.: Aktuelle Zeitung neben dem Werk oder Blockchain-Daten von diesem Moment).

> *Konsistenzhinweis:* Der Ausdruck "Beweispaket" verbindet sich mit der Linie **Evidence Pack → EvidenceRoot → NotarySeal** aus vorherigen Abschnitten; d.h. die Integrität des Pakets wird durch ein verifizierbares Siegel repräsentiert.

### 🔄 365-Tage-Erneuerung (The Sustainability Protocol)

- **Revolutionäres Merkmal:** In Krypto-Projekten bringt der "Dev" (Entwickler) den Token auf den Markt und verschwindet normalerweise nach 1-2 Monaten (Soft Rug). [PoArt] macht dies unmöglich.
- **Regel:** Der "Verified Artist" (Verifizierter Künstler)-Status ist nicht lebenslang. Er ist nur **1 Jahr** gültig.
- **Funktionsweise:** Der Künstler/Entwickler muss der Community alle 365 Tage ein **neues, bedeutendes und nachweisbares Werk** präsentieren.
- **Beispielszenario:** Sie haben das Projekt 2026 gestartet. Im Januar 2027 gibt das System die Warnung "Nachweiszeit Abgelaufen". Wenn der Künstler keine neue Ausstellung, kein neues physisches Werk oder keine neue technologische Integration präsentiert, fällt das "Vertrauensabzeichen" des Projekts.
- **Ergebnis:** Dieses System gewährleistet, dass **der Inhalt niemals seine Aktualität verliert** und dass der Investor nicht die Angst *"Ist der Entwickler noch da?"* erlebt. Das Projekt wird zu einem lebenden Studio.

### 🚩 Rote Flagge (Red Flag Protocol)

**Im Falle jeglicher Fälschung, die von der Community oder Algorithmen erkannt wird (KI-Nutzung, gestohlenes Werk, manipuliertes Video):**

1. Das Zertifikat wird sofort als **"ANNULLIERT" (VOID)** markiert.
2. Beweispakete werden öffentlich als **"Falsch"** gekennzeichnet.
3. Das Projekt wird zur [PoArt]-Blacklist hinzugefügt. Dies verstärkt die Tatsache, dass in einer dezentralen Welt **Reputation die einzige Währung** ist.

---

## d) Fazit: Kein Casino, Sondern ein Museum

**Pump.fun und Dezentrale Börsen (DEX) sind derzeit leider Casinos; die Lichter blinken, jeder jagt nach schnellen Gewinnen und das Haus (Betrüger) gewinnt immer. Wir haben das Projekt hier gestartet, weil wir nicht über ausreichendes Budget verfügten und eine Umgebung hatten, um das bestehende Publikum mit Live-Übertragungen zu erreichen.**

**[PoArt] ist eine Festung, die mitten in diesem Casino gebaut wurde.**

- 🎰 Das Casino basiert auf Kartenspielen; wir basieren auf **physischer Realität**.
- 🃏 Das Casino ist offen für Betrug; wir sind offen für **transparente Beweise**.
- ⏳ Das Casino ist temporär; wir konzentrieren uns auf **die Ewigkeit von Kunst und Wissenschaft**.

**Der Token, der dieses Protokoll verwendet, ist nicht nur eine "Coin"; es ist eine digitale Aktie, die Schweiß, Farbe, Code und Philosophie dahinter enthält.**

---
## 🗳️ 6) GOVERNANCE UND ÖFFENTLICHES REGISTER (Governance & Public Registry)

**Der Zweck dieses Abschnitts ist folgender: Den [PoArt]-Standard aus der Ebene des "Vertrauens in Personen" herauszubringen und ihn in eine nachhaltige öffentliche Infrastruktur mit Registrierung + Verifizierung + Community-Aufsicht zu verwandeln.**

### 6.1 Öffentliches Register (Public Registry)

- **Öffentliches Register:** Alle genehmigten Daten werden unter der Adresse `ilhanart.org/registry` (oder GitHub Registry) registriert.

**Registrierungslogik (empfohlener Standard - JSON-Pfadformat):**

Jeder Eintrag, der ins Register kommt, trägt mindestens diese verifizierbaren Kernfelder:

- **Identität & Status:**
  - `certificate_id` (lesbare Referenz)
  - `status` (active / void)
  - `void_reason` (falls vorhanden)
  - `visibility` (private / masked / public)
  - `created_at` (Zeitstempel)

- **Ausstellende Institution:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Werk-Informationen:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (falls möglich; für Token-Halter-Identifikation)
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
  - `governance.review_notes`

Das Register kann zwei Schichten haben:
- **1)** Menschenlesbarer Index (Web-Auflistung / Suche / Filter)
- **2)** Maschinenlesbares Manifest (JSON-Aufzeichnungen; für PFE-Verifizierung)

**Der "Eintrag" hier wird durch die Kette Evidence Pack → EvidenceRoot → NotarySeal von PFE verifizierbar. Das Register bietet ein Verifizierungsziel, keine "Behauptung".**

---

### 6.2 PoArt Verified Bewerbungsprozess

**PoArt Verified Bewerbungen werden von der İlhanArt Gallery nach den 5 PoArt-Standards bewertet. Das Community-Feedback wird berücksichtigt, aber die endgültige Entscheidung liegt beim kuratorischen Team. Entscheidungen werden transparent erklärt und auf ilhanart.org/registry aufgezeichnet.**

#### Bewerbungsprozess

**Bewerbung:**
- Künstler/Projekt reicht PoArt Verified Bewerbung ein
- Evidence Pack wird vorbereitet (Videoaufnahmen, Metadaten, Live-Übertragungslinks)
- Bewerbung wird an İlhanArt Gallery gesendet

**Prüfung (30 Tage):**
- Galerie-Team prüft Evidence Pack detailliert
- Alle 5 PoArt-Standards werden überprüft:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Interview mit Künstler (optional)

**Community-Konsultation:**
- Evidence Pack wird während des Bewerbungsprozesses öffentlich geteilt
- Token-Holder (mindestens 10.000 $CULTURE) können besonders Vorschläge machen
- **Alles Feedback wird im Prüfungsprozess berücksichtigt**
- **Die endgültige Entscheidung hängt jedoch von der kuratorischen Bewertung ab**

**Entscheidung:**
- Galerie genehmigt oder lehnt Bewerbung ab
- Entscheidungsbegründung wird transparent erklärt
- Bei Genehmigung → PoArt Verified Badge
- Bei Ablehnung → Erneute Bewerbung nach 6 Monaten möglich

**Transparenz:**
- Alle Bewerbungen und Entscheidungen werden auf ilhanart.org/registry aufgezeichnet
- Entscheidungsprotokoll wird öffentlich veröffentlicht:
  - Bewerbungsdatum
  - Zusammenfassung des Prüfungsprozesses
  - Entscheidung (Genehmigt / Abgelehnt)
  - Entscheidungsbegründung (kurze Erklärung)
  - Zusammenfassung des Community-Feedbacks (anonym)

#### Warum Kuratorische Entscheidung?

**Qualitätskontrolle:**  
Der PoArt Verified Status ist ein Badge mit hohen Standards. Kuratorische Bewertung garantiert die Aufrechterhaltung dieser Standards.

**Verhinderung Spekulativer Manipulation:**  
Mit Pump.fun-Token ist vollständige On-Chain-Governance (z.B.: Realms, DAO-Abstimmung) technisch nicht möglich. Off-Chain-Voting-Systeme sind anfällig für Wal-Manipulation und koordinierte Angriffe. Kuratorische Entscheidung eliminiert dieses Risiko.

**Operative Effizienz:**  
Statt komplexer Voting-Mechanismen, schneller und klarer Entscheidungsprozess. Künstler erhalten Ergebnisse innerhalb von 30 Tagen.

**Community-Beteiligung:**  
Community-Feedback wird vollständig berücksichtigt und beeinflusst den Entscheidungsprozess. Die endgültige Entscheidung liegt jedoch beim vor Manipulation geschützten kuratorischen Team.

**Zukunft:**  
Wenn das Projekt reift (2027+), kann der Community-Konsultationsmechanismus gestärkt werden. Der kuratorische Standardschutz bleibt jedoch dauerhaft.

---

### 6.3 Token-Nutzen (Token Utility)

**Vorteile für $CULTURE-Token-Holder:**

**1. Prioritärer Zugang zu Galerie-Veranstaltungen:**
- Eröffnungen physischer Ausstellungen der İlhanArt Gallery
- Künstlertreffen und Atelierbesuche
- Spezielle Sammlungsansichten

**2. Vollständiger Zugang zum PoArt-Register:**
- Detaillierte Aufzeichnungen aller authentifizierten Kunstwerke
- Vollständige Versionen der Evidence Packs
- Forensische Verifizierungswerkzeuge


**3. Beratende Abstimmung:**
- Beratungsrecht bei PoArt Verified Bewerbungen
- Zugang zu Community-Feedback-Kanälen
- Teilnahme an Governance-Diskussionen

**4. Exklusiver Inhalt:**
- Studio-Behind-the-Scenes-Inhalte
- Künstlerinterviews und Prozessvideos
- Zugang zur technischen Dokumentation

**Hinweis:**  
Token-Holder geben beratende Stimmen (Advisory Vote) ab. Die endgültige Entscheidung liegt beim kuratorischen Team. Diese Struktur wird bevorzugt, um Wal-Manipulation und spekulative Angriffe zu verhindern. Es gibt keine Staking-Belohnungen, weil wir langfristige kulturelle Teilnehmer suchen, nicht kurzfristiges Söldnerkapital.

---

### 6.4 Metadaten-Synchronisation (Metadata Sync)

- **Metadaten-Synchronisation:** Technische Daten im Register müssen zu 100% mit der physischen Entität übereinstimmen.

**"100% Übereinstimmung" technisch definieren (empfohlene Klarheit):**

- **Mindestübereinstimmung (obligatorisch):**
  - `asset.fingerprints.sha256/sha512` im Register muss **genau dasselbe** sein wie der Hash der Datei in der Hand.
  - Wenn `proof.notary_seal` im Register reproduziert wird (falls Evidence Pack vorhanden) muss es **genau dasselbe** sein.

- **Physische Referenzübereinstimmung (Beweistyp):**
  - Beweise wie physisches Werk + Datum/Block-Referenz, die in Live-Übertragung gezeigt werden, müssen mit Evidence Pack konsistent sein.

- **Datenschutz-Compliance:**
  - In `masked`-Sichtbarkeit werden Felder wie IP/Standort **gemäß Maskierungsstandard** veröffentlicht.

---

### 6.5 Streit, Prüfung und Widerruf (Dispute & Revocation)

Das Register ist nicht nur ein "Genehmigungs"-Mechanismus; es ist ein **lebender Aufsichtsmechanismus gegen Fälschung**.

- Wenn ein Streit initiiert wird, kann der Eintrag in den **"Review"**-Modus (Prüfung) versetzt werden.
- Wenn Fälschung festgestellt wird, wird er als `status: void` markiert und Begründung hinzugefügt:
  - `void_reason` (KI-Nutzung / Plagiat / Manipulation usw.)
  - `revoked_at` (Widerrufszeit)
- Die Quelle der Widerrufsentscheidung ist im Register klar sichtbar:
  - kuratorische Prüfung / Community-Streit / forensische Analysenotiz (je nachdem, was anwendbar ist)

> **Dieser Teil ist das Gegenstück im Register zum VOID-Konzept im "Red Flag Protocol"-Abschnitt.**

---

### 6.6 Beispiel-Registereintrag (Maschinenlesbar)
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

> *Hinweis: `asset.fingerprints.sha512` und andere Hash-Werte sind zu Demonstrationszwecken abgekürzt; in der realen Anwendung wird eine hexadezimale Zeichenfolge voller Länge verwendet.*

---

## 7) 🔐 TECHNISCHES SIEGEL (NOTARY SEAL)

**Unerschütterlicher Siegelalgorithmus, produziert von PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] Digitales Notar- und Forensisches Beweisprotokoll (Beta v1.0)

> **"Kultur ist größer als Kapital. Schützen Sie Ihre Werke von heute an, tragen Sie sie in die Zukunft."**

---

## Warum Öffentlich?

Echte Sicherheit kommt von Transparenz. Dank unseres **Öffentlichen Registers (Public Registry)** kann eine Person irgendwo auf der Welt in Sekunden verifizieren, ob die Datei, die sie hat, original ist, ohne jegliche Autorität zu benötigen.

---

## 🧩 Warum Mehrere "Sichtbarkeitsmodule"?

Dies ist der kritischste Teil des Codes (Sichtbarkeits-Auswahlmenü). Diese Optionen ermöglichen es Benutzern, das Gleichgewicht **"Privatsphäre vs. Transparenz"** herzustellen:

### 🔒 Privat (Private)

- **Szenario:** Der Künstler möchte das Werk noch nicht veröffentlichen, aber einen Zeitstempel setzen und beweisen "ich habe dies an diesem Datum gemacht".
- **Was der Code Macht:** Schreibt die Daten in die Datenbank, setzt aber das Label `visibility: "private"`. Beim späteren Schreiben der "Public Read"-Richtlinie kann man diese Einträge vor der Öffentlichkeit verbergen, indem man `WHERE visibility = 'public'` sagt.

### 🕶️ Maskiert (Masked)

- **Szenario:** Der Künstler möchte Transparenz, fürchtet aber, dass seine Heimadresse (IP-Standort) gefunden wird.
- **Was der Code Macht:** Auf der JavaScript-Seite arbeiten die Funktionen `maskIP` und `maskLoc`. Konvertiert die IP-Adresse in die Form `88.241.***.***`, den Standort in die Form `***/TR` und sendet die zensierte Version an die Datenbank.
- **Datenschutzhinweis:** Maskierung erfolgt im Browser, Supabase sieht den echten Standort nicht. **Jedoch:** Wenn Drittanbieter-APIs wie ipapi.co für Standortdaten verwendet werden, sehen diese Anbieter die IP-Adresse zum Zeitpunkt der Anfrage.
- **Versiegelung im Maskierten Modus:** Die Berechnung von EvidenceRoot und NotarySeal erfolgt mit maskierten Forensic-Daten; so bleibt die Verifizierung deterministisch.

### 🌍 Öffentlich (Public)

- **Szenario:** Volle Transparenz. Gemäß [PoArt]-Standard wird klar erklärt, wo, wann, aus welchem Netzwerk das Werk produziert wurde.

---

## 💡 Technologische Innovation

PoArt ist nicht nur ein Datei-Upload-System. Es ist ein **"Forensische Verwahrungskette" (Forensic Chain of Custody)**-Motor, der drei verschiedene Technologieschichten in einem Topf verschmilzt und einen neuen Standard bringt.

**Die in diesem Abschnitt als "Motor" erklärte Schicht entspricht dem PoArt Forensic Engine (PFE)-Kern in der vorherigen Terminologie.**

### 1) Clientseitiges Hashing (Maximale Privatsphäre)

Ihre Werkdateien werden nie auf den Server hochgeladen. Unser browserbasierter (clientseitiger) Motor berechnet den Hash (digitale Zusammenfassung) der Datei auf Ihrem eigenen Computer. Nur dieser Fingerabdruck und Metadaten werden an den Server gesendet.

> **Datenschutzhinweis:** Die Werkdatei wird nicht auf den Server hochgeladen und so geschützt. Forensische Daten (IP/Standort) werden jedoch gemäß dem gewählten Sichtbarkeitsmodus (private/masked/public) geteilt.

### 2) Forensische Datenfusion (Forensische Kraft)

Es ist viel mehr als ein einfacher Zeitstempel (Timestamp). Das System kombiniert diese Daten in einem einzigen "Genesis-Siegel":

- **Digitale Zusammenfassung (SHA-512):** Digitaler Fingerabdruck, der beschädigt wird, selbst wenn ein einzelnes Pixel des Werks sich ändert, unter Verwendung des kryptografischen Zusammenfassungsstandards (SHA-512).
- **Standort & Zeit:** Datum, Land, Stadt und Bezirksdaten mit Millisekundenpräzision, wann die Operation durchgeführt wurde.
- **Geräte-Identität:** Betriebssystem, Browser und Gerätetyp (User-Agent-Analyse).

---

## 🛡️ Anwendungsbereiche und Nutzen

Wenn Sie Künstler, Autor oder Designer sind, reicht es nicht zu sagen "Ich habe dies vorher gemacht", Sie müssen es beweisen.

**Ein Werk, das Sie mit PoArt versiegeln:**

- **Mathematischer Beweis:** Selbst wenn ein einzelnes Pixel Ihrer Datei sich ändert, versteht das System dies. Manipulation ist unmöglich.
- **Rechtsgrundlage:** Es ist aufgezeichnet, an welchem Datum, in welcher Stadt, von welchem Gerät das Werk versiegelt wurde.
- **Sofortiges Zertifikat:** Erzeugt in Sekunden ein personalisiertes, QR-codiertes und versiegeltes **"Vermögenswert-Identitätszertifikat"**.

---

## ⚙️ Systemarchitektur und Technische Merkmale

Das System ist auf einer "Serverlosen" (Serverless) Architektur konzipiert, mit Fokus auf hohe Leistung und Skalierbarkeit.

| Schicht | Technologie | Beschreibung |
|---------|-------------|--------------|
| **Kryptografie** | SHA-256 & SHA-512 | Doppelschichtige kryptografische Zusammenfassung |
| **Datenbank** | Supabase (PostgreSQL) | JSONB-Datenstruktur, RLS-Richtlinien |
| **Forensische Daten** | ipapi.co API | IP/Standort/Zeit-Trio |
| **Rendering** | html2canvas + jsPDF | Clientseitige PNG/PDF-Generierung |
| **Frontend** | Vanilla JavaScript | Null Framework-Abhängigkeit |
| **Sicherheit** | Clientseitiges Hashing | Datei geht nie zum Server |

### Herausragende Merkmale

| Merkmal | Detail | Bei Konkurrenten? |
|---------|--------|-------------------|
| **Drag & Drop UI** | Datei ziehen-ablegen, sofortige Vorschau | ❌ Bei den meisten nicht |
| **Multi-Format-Export** | PNG, JSON, PDF - ein Klick | ⚠️ Begrenzt |
| **Echtzeit-Vorschau** | Live-Zertifikatsvorschau | ❌ Nein |
| **Datenschutz-Kontrollen** | Private/Masked/Public-Optionen | ❌ Nein |
| **Clientseitiges Hashing** | Datei geht nie zum Server | ✅ Nur bei einigen |
| **Forensische Metadaten** | IP, Standort, Gerät, Zeit - alles zusammen | ❌ Fragmentiert |
| **QR-Verifizierung** | Sofortiger Verifizierungs-QR-Code | ⚠️ Eingeschränkt |
| **Rate Limiting** | Spam-Schutz (RLS + Client) | ❌ Bei den meisten nicht |

---

## 🗺️ Roadmap: "Vertrauenslose" Zukunft

Die aktuelle Version **(Beta v1.0)** ist optimiert, um dem Endbenutzer maximale Geschwindigkeit, einfache Oberfläche und kostenlosen Zugang zu bieten. Unsere ultimative Vision ist jedoch, zu einer Struktur überzugehen, in die selbst der Datenbankadministrator (wir) nicht eingreifen kann.

### Phase 1: Beta v1.0 (Derzeit Online)

**Infrastruktur:**
- Cloud-Datenbank (Supabase)
- Off-Chain-Register (PostgreSQL + IPFS-Backup)
- Galerie-Selbstattestation (zentralisiert aber transparent)

**Token:**
- Plattform: Pump.fun
- Liquidität: Raydium (automatisch)
- Governance: Nur beratend (Community-Beratung)

**Zweck:**
- Geschwindigkeit, UX-Barrieren beseitigen
- "Reibungslose" Sicherheit bieten
- Community-Aufbau

**Token-Nutzen (v1.0):**
- Prioritärer Zugang zu Galerie-Veranstaltungen
- PoArt-Register-Ansicht
- Beratendes Stimmrecht

---

### 🚀 Phase 2: Dezentralisierte Autorität (2026 Q2-Q4)

Diese Phase umfasst den Übergang des Systems von einer vollständig "clientseitigen" Arbeitsstruktur zu einer sichereren und dezentralisierten Struktur.

| Merkmal | Was Bringt Es? | Tech-Stack | ETA |
|---------|----------------|------------|-----|
| **Edge Function INSERT** | Spam-Blockierung + API-Key-Sicherheit | Supabase Edge (Deno) | Q2 2026 |
| **Wallet-Signatur** | Dezentralisierte Identität | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave-Backup** | Dezentralisiertes Archiv | IPFS SDK + Pinata | Q3 2026 |
| **Widerrufsmechanismus** | Falsch-Zertifikat-Stornierung | DB-Schema-Update | Q2 2026 |
| **Audit-Log** | Forensische Abfrageaufzeichnung | Benutzerdefinierte Logs-Tabelle | Q3 2026 |
| **OpenTimestamps** | Bitcoin-Verankerung | OTS JavaScript | Q4 2026 |

**Token-Governance (v2.0):**
- Off-Chain-Voting (x/Web) + Wallet-Signatur
- Auswahl von Community-Vertretern (erste 90 Tage)
- Multi-Sig-Operations-Wallet-Kontrolle
- Gewichtetes beratendes Voting (mit Wal-Cap)

**Unveränderlichkeit:**
- Register-Backup mit IPFS-Hashes
- Bitcoin-Zeitstempel-Verankerung
- Cross-Chain-Verifizierungsvorbereitung

---

### Phase 3: Vollständige Dezentralisierung (2027+)

| Merkmal | Ziel | ETA |
|---------|------|-----|
| **On-Chain-Register** | Solana On-Chain-Aufzeichnung | Q1 2027 |
| **Erweiterter Token-Nutzen** | NFT-Mint, erweiterte Funktionen | Q1 2027 |
| **Multi-Chain-Support** | Ethereum, Polygon, Base | Q2 2027 |
| **DID-Integration** | Dezentralisierte Identität | Q3 2027 |
| **Community-Governance** | Verstärktes beratendes System | Q4 2027 |
| **Rechtliche Anerkennung** | Gültigkeit vor türkischen Gerichten | 2027-2028 |
| **API für Entwickler** | Öffentlicher API-Endpunkt | Q3 2027 |

**Governance-Evolution:**
- v3.0: Hybridmodell (kuratorial + Community-gewichtet)
- 2028+: Vollständige Community-Governance (optional)
- Kuratorische Qualitätskontrolle bleibt immer erhalten

---

## 🧬 Protokoll-Datenstruktur (JSON-Schema)

**Jedes [PoArt]-Zertifikat hat eine tragbare und verifizierbare JSON-Identitätskarte, die im folgenden Standard produziert wird.**

> **Hinweis:** Dieses Identity-JSON-Format ist das Zertifikatsformat, das dem Benutzer präsentiert wird. In Registry-Aufzeichnungen wird `registry.asset` anstelle von `identity.asset_data` verwendet (Mapping: `identity.asset_data` == `registry.asset`).
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
// Hilfsfunktionen: Digest in Hex-String konvertieren
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// String in Byte-Array konvertieren
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Kanonische Forensik-String-Generierung (v1.0: feste Feldreihenfolge + UTF-8 + \n Delimiter)
// Phase-2-Hinweis: Übergang zu kanonischem JSON mit RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal-Generierungsprozess (Vollständig Deterministisch)
```javascript
// 1. FileHash-Berechnung (clientseitig)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Forensische Datensammlung (Verwendung eines einzigen Zeitstempels)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Einzelne Zeitstempelgenerierung
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Derselbe Zeitstempel
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot-Erstellung (mit kanonischer Kodierung)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal-Generierung (unter Verwendung desselben Zeitstempels)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Hilfsfunktionen zur Maskierung (IPv4- und IPv6-Unterstützung)
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

### Verifizierungsablauf (Zwei Stufen)

#### Schnelle Verifizierung (Quick Verify)
```javascript
// Überprüft nur den Datei-Hash (schnelle rote Flagge)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Vom Register abrufen
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
      message: "❌ Falsch - Datei manipuliert"
    };
  }
}
```

#### Vollständige Verifizierung (Full Verify)
```javascript
// Regeneriert und verifiziert EvidenceRoot und NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Vom Register abrufen
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash-Überprüfung (schnelle rote Flagge)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Falsch - Datei-Hash stimmt nicht überein" };
  }

  // 2) EvidenceRoot regenerieren (mit im Register gespeicherten Forensik-Daten)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Stimmt nicht überein - EvidenceRoot passt nicht" };
  }

  // 3) NotarySeal regenerieren (mit demselben Zeitstempel + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Stimmt nicht überein - NotarySeal passt nicht" };
  }

  // Optional: In Phase 2 auch signer_sig mit attestation_pubkey verifizieren
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Signatur ungültig" };

  return { valid: true, message: "✅ Original - Full Verify bestanden" };
}
```

> **Wichtige Hinweise:**
> - **Quick Verify:** Überprüft nur den Datei-Hash für schnelle Verwendung.
> - **Full Verify:** Verifiziert alle Schichten des Protokolls (EvidenceRoot + NotarySeal).
> - Alle Hash-Operationen werden deterministisch durchgeführt, mit fester Kodierung und Delimitern.
> - **v1.0-Kanonisierungsstandard:** Feste Feldreihenfolge + UTF-8-Kodierung + `\n`-Delimiter.
> - **Phase-2-Plan:** Übergang zu kanonischem JSON mit RFC 8785 (JCS - JSON Canonicalization Scheme).
> - Im maskierten Modus werden EvidenceRoot- und NotarySeal-Berechnungen mit maskierten forensischen Daten durchgeführt.
> - Ein einziger Zeitstempel wird im gesamten Prozess verwendet (Forensik + NotarySeal); Determinismus ist garantiert.
> - **Forensik-Feldnamen:** `ip_masked`, `location`, `device`, `timestamp` (Code und Register vollständig kompatibel).
> - **Register-Pfad:** `certificate.asset.fingerprints` (vollständig kompatibel mit Verifizierungscode).
> - **signer_sig im Register:** Das Feld `proof.signer_sig` ist für Full Verify erforderlich.
> - Der SignerSignature-Mechanismus wird in Phase 2 mit Solana Wallet Adapter aktiviert; in v1.0 kann mit `attestation_pubkey` verifiziert werden.

---

## 📊 Wettbewerbsanalyse (Aktualisiert)

PoArt ist auf dem "Sweet Spot" (optimalen Punkt) positioniert, der die Mängel bestehender Lösungen ergänzt.

| Merkmal | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 証 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Kosten** | 🆓 Kostenlos | 🆓 | 💰 Kostenpflichtig | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Sehr einfach | ❌ CLI | ⚠️ Mittel | ⚠️ Mittel | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format-Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Echtzeit-Vorschau** | ✅ Live | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Datenschutz-Kontrollen** | ✅ 3 Modi | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Clientseitiger Hash** | ✅ Privatsphäre | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensische Metadaten** | ✅ Vollständig | ❌ | ❌ | ⚠️ Eingeschränkt | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR-Verifizierung** | ✅ Sofort | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain-Verankerung** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Deutsche Unterstützung** | ✅ Nativ | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Erklärung:**
- ✅ : Vollständige Unterstützung / verfügbar
- ⚠️ : Eingeschränkt / in kostenpflichtigen Plänen
- ❌ : Existiert nicht / nicht unterstützt
- 🔄 : In Roadmap (in Entwicklung)
- 🆓 : Vollständig kostenlos
- 💰 : Kostenpflichtig / Abonnement erforderlich

### Mängel der Konkurrenten, Stärken von PoArt

| Mangel | Konkurrenten | PoArt |
|--------|--------------|-------|
| **Nutzungsschwierigkeit** | CLI, API-Kenntnisse, Wallet erforderlich | Drag & Drop, in 3 Klicks fertig |
| **Kostenbarriere** | $50-500/Monat Abonnement | 100% kostenlos |
| **Privatsphäre** | Datei auf Server hochgeladen | Clientseitig, Datei geht nie weg |
| **Forensische Daten** | Nur Zeitstempel | IP, Standort, Gerät, Zeit - alles |
| **Deutsche Unterstützung** | Existiert nicht oder sehr eingeschränkt | Native Sprachunterstützung |
| **Open Source** | Geschlossene Box | Gesamter Code offen auf GitHub |

---

## 📈 Nutzungsstatistiken (Ziele Q1 2026)

| Metrik | Ziel | Status |
|--------|------|--------|
| **Gesamt-Zertifikate** | 1.000 | 🔄 In Bearbeitung |
| **Aktive Benutzer** | 500 | 🔄 In Bearbeitung |
| **Verifizierungsanzahl** | 5.000 | 🔄 In Bearbeitung |
| **Verfügbarkeitszeit** | 99,9% | ✅ Aktiv |
| **Durchschn. Antwortzeit** | <200ms | ✅ Optimal |

---

## 🌍 Community und Support

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **E-Mail:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Mitwirkende

Das PoArt-Protokoll entwickelt sich weiter mit Beiträgen der Open-Source-Community.

**Um beizutragen:**
1. Forken
2. Feature-Branch erstellen (`git checkout -b feature/amazing-feature`)
3. Committen (`git commit -m 'Add amazing feature'`)
4. Pushen (`git push origin feature/amazing-feature`)
5. Pull Request öffnen

### 🛠️ Was Brauchen Wir Jetzt? (Hilferuf)

Wir erwarten Beiträge von erfahrenen Entwicklern in den folgenden Themen für **Phase-2**-Entwicklungen des PoArt-Protokolls:

* **Supabase Edge Functions:** Spam-Schutz serverseitig verschieben.
* **Solana Web3.js:** Wallet-Signatur-Integration (Wallet Signing).
* **IPFS / Arweave:** Integration von Archivierungs- und Pinning-Diensten.
* **Community-Tools:** Voting-Systeme, Analytics-Dashboard.

> Bitte starten Sie eine Diskussion im "Issues"-Tab, bevor Sie eine Funktion hinzufügen.

---

## 💬 Abschließende Hinweise

### Pump.fun und Realität

Dieses Projekt wurde auf Pump.fun gestartet, weil:
- ✅ Zugang zu Liquidität (automatische Raydium-Migration)
- ✅ Zugang zur bestehenden Community
- ✅ Niedrige Anfangskosten

Lassen Sie uns dies jedoch klarstellen:
- **Der Token-Preis** ist kein Indikator für künstlerischen Erfolg
- Der Token-Wert ist wichtig für das **operative Budget** (Galerie, Ausstellungen, Infrastruktur)
- **Erfolgsmetriken:** Authentifizierte Werke + Community-Engagement + physische Besucher

### Governance und Dezentralisierung

**v1.0 Realität (2026):**
- Register: Off-Chain (PostgreSQL + IPFS-Backup)
- Attestation: Galerie-selbstsigniert (zentralisiert aber transparent)
- Governance: Nur beratend (finale kuratoriale Entscheidung)
- Token-Nutzen: Galerie-Zugang + Register + NFT-Priorität

**v2.0+ Vision (2027+):**
- Register: On-Chain (Solana)
- Signaturen: Wallet-basiert (dezentralisiert)
- Governance: Hybrid (Community-beratend + kuratoriale Qualität)
- Token-Nutzen: Erweiterte Funktionen + erweiterter Zugang

Diese Struktur bietet **operative Effizienz** und **Qualitätskontrolle** in der frühen Phase, während der Weg offen bleibt, um die **Community-Beteiligung** in der Zukunft zu erhöhen.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Kultur ist Größer als Kapital*

## 🧾 Lizenz

MIT License © 2026 İlhan Art Gallery Initiative

Siehe [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) für vollständige Bedingungen.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Dieses Projekt wurde mit der [İlhan Art Gallery]-Initiative entwickelt und die Quellcodes sind im Namen der Transparenz öffentlich zugänglich.**

**PROTOKOLL V1.0 // VERSIEGELT MIT SHA-512**

*© 2026 İLHAN ART | ALLE RECHTE AN WERKEN, BILDERN UND IDEEN VORBEHALTEN.*

---
