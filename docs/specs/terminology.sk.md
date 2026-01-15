# 📚 SLOVNÍK TERMINOLÓGIE A POJMOV
> **"Pochopenie jazyka tohto protokolu znamená pochopenie jeho vízie."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Základná Infraštruktúra

**PoArt Forensic Engine (PFE)** je základná vrstva, ktorá predstavuje fundamentálnu logiku a technické fungovanie za [PoArt] protokolom. Je to "kriminalistický motor", ktorý transformuje surové dáta výroby umeleckého diela na overiteľný a nemenný **digitálny dôkaz**.

### 🧩 Prečo "PoArt Forensic"?

- **PoArt (Proof of Art):** Zameranie motora je viazanie hodnoty digitálneho aktíva nie na špekuláciu, ale na **overený výrobný proces**.
- **Forensic (Kriminalistické Overenie):**
  - **Technická Definícia:** Algoritmický prístup a reťaz dôkazov na overenie, že dáta výrobného procesu (ťahy štetcom, timelapse, logy) neboli manipulované.
  - **Filozofická Úroveň:** Proti "okamžitej výrobe" umelej inteligencie; tvrdenie o transformácii ľudskej výroby, ktorá obsahuje **čas, úsilie a cenu rozhodnutí**, na merateľnú realitu.

> Poznámka: Blockchain integrácia (napr. Solana) nie je jadrom PFE; bude definovaná samostatne ako **Chain Anchor Layer** pre overenie/register.

### 🛠️ Technický Rozsah v1.0

**PoArt Forensic Engine (PFE) v1.0** je postavený na **3 základných pilieroch** namiesto zložitých finančných modelov:

1. **Hashing & Sealing (Zapečatenie):**  
   PFE deterministicky spracováva všetky elementy v Evidence Pack (súbor diela, video, JSON/log, podpis atď.) a generuje jedinečnú hodnotu **NotarySeal**.

   **Kľúčové pojmy (v1.0):**
   - **FileHash (odtlačok diela):** Hash generovaný z bytov súboru diela.
   - **EvidenceRoot (koreň balíka dôkazov):** Koreňový digest, ktorý reprezentuje integritu Evidence Pack (Merkle koreň alebo hash kanonického manifestu).
   - **NotarySeal (konečná pečať / výstup PFE):** Konečná pečať generovaná z kombinácie EvidenceRoot + čas + podpis.

   **Vzorce (vo formáte zrozumiteľnom pre investorov):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload definície (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Poznámka: Hodnota považovaná za výstup PFE je **NotarySeal**. Mechanizmus **SignerSignature** bude aktivovaný vo fáze 2 (so Solana Wallet Adapter); v súčasnej v1.0 sa používa vlastný osvedčovací podpis systému. Verejný osvedčovací kľúč je publikovaný v registri v poli `issuer.attestation_pubkey`.

2. **Indexing (Archivovanie):**  
   Zaznamenáva, ktorá peňaženka, ktorý dátum, predložila **Labor Proof (Dôkaz Práce)** pre ktoré dielo; v transparentnej a vyhľadateľnej registrovej vrstve.  
   *(Táto vrstva môže byť databáza; blockchain integrácia je definovaná samostatne ako "Chain Anchor Layer".)*

3. **Verification (Overenie):**  
   Keď je autenticita diela spochybnená, PFE prepracováva surové dôkazy; testuje s matematickou istotou, či vypočítané hodnoty **EvidenceRoot / NotarySeal** zodpovedajú záznamom v archíve.

---

### 🧮 Teoréma Hodnoty PoArt (The Value Theorem)

[PoArt] protokol viaže hodnotu ($V$) digitálneho aktíva nie na subjektívne vnímanie trhu, ale na **fyzickú realitu výrobného procesu**.

Umelá inteligencia (AI) ruší proces tým, že poskytuje okamžité výsledky ($t \to 0$). [PoArt] namiesto toho považuje hodnotu za akumuláciu komponentov **čas, práca a vôľa**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definícia Premenných

- **$\int dt$ (Akumulácia Procesu):**  
  Hodnota nie je okamžitý "výstup"; je to **proces**, ktorý sa akumuluje medzi $t_{\text{start}}$ a $t_{\text{end}}$. Keď sa čas znižuje (AI výroba), výsledok integrálu sa blíži k 0.

- **$P_{\text{labor}}(t)$ (Okamžitá Intenzita Práce):**  
  Predstavuje intenzitu duševného a fyzického úsilia vynaloženého v momente výroby. Keď overené úsilie rastie, integrand rastie.  
  > Poznámka: Tento člen môže byť v praxi normalizovaný na "merateľné/overiteľné signály práce".

- **$I_{\text{agency}}(t)$ (Koeficient Vôle):**  
  Toto je schopnosť výrobcu riskovať a robiť rozhodnutia. Nadobúda hodnoty medzi $0$ a $1$.
  - **AI ($I \approx 0$):** Vykonáva príkazy, neriskuje, neplatí náklady.
  - **Človek ($I \to 1$):** Mení rozhodnutia, váha, riskuje.

- **$U_{\text{irreversible}}$ (Nezvratná Jedinečnosť):**  
  Zatiaľ čo v digitálnej výrobe môžeš vrátiť späť (`Ctrl+Z`); vo fyzickej výrobe (farba nanesená na plátno, vytesaný mramor, gesto počas živého vysielania) nie je cesty späť. Táto **nezvratnosť** je doplnkový člen, ktorý vytvára "jedinečnosť" (nezameniteľný charakter) v diele.

### 🔎 Prípadová Analýza: AI "Okamžitý Výstup" vs. Človek "Overený Proces"

Nasledujúci scenár ukazuje, ako **Teoréma Hodnoty PoArt** funguje v praxi a prečo AI výroby dostávajú nízke skóre v [PoArt] štandarde.

#### Scenár A: Vizuálna Výroba s AI za 10 Sekúnd

- **Trvanie ($\Delta t$):** $10$ sekúnd (proces prakticky neexistujúci)
- **Intenzita Práce ($P_{\text{labor}}$):** $1$ jednotka (len písanie príkazu)
- **Koeficient Vôle ($I_{\text{agency}}$):** $0.01$ (žiadne riziko, žiadne náklady)
- **Nezvratnosť ($U_{\text{irreversible}}$):** $0$ (zvratné / kopírovateľné)

**Výsledok:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Komentár:** Aj keď je výstup dokonalý; keďže proces nebol prežitý a neobsahuje vôľu/riziko, [PoArt] hodnota sa blíži k $0$.

#### Scenár B: Fyzická Výroba Naživo počas 6 Hodín

- **Trvanie ($\Delta t$):** $6$ hodín ($21{,}600$ sekúnd)
- **Intenzita Práce ($P_{\text{labor}}$):** $0.5$ jednotiek (kontinuita fyzického a duševného úsilia)
- **Koeficient Vôle ($I_{\text{agency}}$):** $0.9$ (zmena rozhodnutí, riskovaní, nezvratné voľby)
- **Nezvratnosť ($U_{\text{irreversible}}$):** $>0$ (fyzické stopy nemôžu byť vrátené späť)

**Výsledok:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Komentár:** Keď sa proces predlžuje a vôľa (riziko) rastie, hodnota sa akumuluje kumulatívne. Člen $U_{\text{irreversible}}$ je doplnkový príspevok, ktorý vytvára "jedinečnosť" (nezameniteľný charakter) v diele.

---

### ✅ Záver: Hodnota Viazaná na Dôkaz (Proof-Bound Value)

Táto teoréma odstraňuje tvrdenie hodnoty [PoArt] z toho, aby bolo "like" alebo "trhový príbeh" a viaže ho na **overenú realitu výroby**.

1. **Bez Procesu Sa Nevytvára Hodnota:**  
   AI ruší proces v okamžitom výstupe ($t \to 0$). Keď sa okno procesu zužuje, výsledok integrálu klesá z matematickej nevyhnutnosti:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Vôľa a Riziko Sú Násobitelia:**  
   [PoArt] meria nielen "vynaložený čas", ale aj skutočnú úroveň rozhodnutia, rizika a nákladov počas toho času. Hodnota výroby bez riskovania (AI) je nízka:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Jedinečnosť Je Fyzický Dôkaz, Nie Marketing:**  
   Vo fyzickej výrobe sú nezvratné stopy (ťah štetcom na plátne, zlomený mramor) mimo digitálnej `Ctrl+Z` logiky. Táto nezvratnosť ($U_{\text{irreversible}}$) robí dielo ontologicky jedinečným.

> **🔐 ZHRNUTIE:** Aj keď sa teoréma hodnoty môže zdať neurčitá ako meranie (aj keď sa nedá merať 100% v reálnom živote), účelom tohto vzorca je ukázať štruktúru a smer premenných. To, co je vzácne v ére AI, nie je "obraz", ale **overená práca, čas a vôľa.** [PoArt] meria túto vzácnosť a zaznamenáva ju cez **Evidence Pack**.

### 🏛️ Význam Pojmu "Engine" (Motor)

Tokeny, ktoré pochádzajú z platforiem ako Pump.fun, sú často len **"vstupné lístky"**. **PoArt Forensic Engine (PFE)** je namiesto toho **ústavná logická vrstva**, ktorá definuje, aké práva tento lístok chráni, ako sa zaznamenáva práca a ako sa umenie/veda/technológia stávajú trvalými.

> **Poznámka:** Dôvod, prečo sme začali tento projekt na Pumpfun, je, že sme nemali dostatočnú likviditu a sledovateľov. Použitie existujúcich dát bolo strategicky správnym krokom, hoci nie najkvalitnejším. Definovanie logiky tohto motora na GitHub, nezávisle od rozpočtu a zdrojov, dokazuje, že projekt nie je len finančná špekulácia, ale dlhodobá vízia **softvérovej infraštruktúry** a **digitálnej národnej knižnice**.

---

## 🎨 [PoArt] PROOF OF ART PROTOKOL (Proof of Art Protocol v1.0)

> **"Skutočný Umelec, Skutočná Výroba, Skutočná Hodnota."**

Tento protokol je **biologický a intelektuálny obranný mechanizmus** navrhnutý proti anonymným podvodníkom, ktorí zaplavili krypto ekosystém, AI obrázkom vyrobeným za 5 minút a kultúre "Pump & Dump".

---

## a) Čo Je [PoArt]? (Filozofická a Technická Definícia)

**Proof of Art [PoArt];** je inštitucionálny overovací štandard, ktorý zaručuje, že hodnota za aktívom na blockchain je založená nie na špekulácii, ale na overenej **ľudskej práci**, **čase** a **fyzickej energii**.

Presne ako Bitcoin produkuje hodnotu cez *"Elektrina a Výpočtový Výkon"* **(Proof of Work)**; [PoArt] kompatibilné projekty produkujú hodnotu cez *"Umelecké Zručnosti a Ľudský Čas"*.

Eliminuje riziko *"Dev predal, projekt skončil"*, prítomné v Pump.fun a DEX platformách; pretože tu hodnota nie je v kóde, ale v **kontinuite výroby**.

> **[PoArt] nehovorí účastníkovi "Verte nám"; hovorí "Tu sú dôkazy, pozrite sa vlastnými očami, overte vlastnou matematikou".**

---

## b) [PoArt] 5-Pilierový Štandard (The 5 Pillars of Truth)

Týchto 5 bodov sú nemanipulovateľné filtre, ktorými musí projekt prejsť, aby dostal [PoArt] pečať.

### 1) Dôkaz Identity Naživo (Live Identity Proof)

- **Problém:** Krypto svet je plný anonymných zakladateľov (Dev) s nedefinovanou identitou, ktorí zbierajú peniaze a opúšťajú projekt.
- **[PoArt] riešenie:** Výrobca dokazuje nielen identitu, ale **prítomnosť počas výroby**. To zahŕňa živé relácie, kde interagujú s komunitou a plnia špecifické okamžité požiadavky, nie s vopred nahranými videami.  
  (Napríklad: *"Napíš dnešný dátum a aktuálne číslo bloku v pravom rohu plátna"*)
- **Motto:** *"Roboty môžu maľovať, ale roboty sa nepotia a neimprovisujú."*

### 2) Dôkaz Práce a Procesu (Labor & Process Proof)

- **Problém:** AI obrázky vyrobené za 2 sekundy a olejomaľby vyrobené za 2 mesiace sa považujú za rovnaký "jpeg" v digitálnom svete.
- **[PoArt] riešenie:** "Tehotenský a pôrodný proces" diela sa zaznamenáva. Fázy náčrtu, vrstvy farby, akumulované strávené hodiny a fyzický proces, ktorý umelec zažil počas tvorby diela, sa dokumentujú. To pridáva **"Časové Náklady" (Time Cost)** k tokenu. Čím ťažšie je aktívum vyrobiť, tým pevnejšia je jeho hodnota.

### 3) Dôkaz Estetickej Hodnoty (Aesthetic Value Proof)

- **Problém:** Estetika a umelecká hĺbka "Meme" kultúry, ktorá ignoruje všetko a zameriava sa len na okamžitú komédiu, a krátkodobé "Hype" projekty, ktoré z toho vyplývajú.
- **[PoArt] riešenie:** Projekt musí mať akademické umelecké štandardy, teóriu farieb, pravidlá kompozície a poznanie materiálov (Impasto, Textúra atď.). Obsah by nemal len rozosmiať; mal by vzbudiť obdiv u diváka a mať **zberateľskú hodnotu**.

### 4) Koncepčná Inovácia (Conceptual Novelty)

- **Problém:** Tisíce identických dog/cat coin, ďaleko od kreativity.
- **[PoArt] riešenie:** Projekt musí vybudovať nový most, ktorý zmysluplne kombinuje umenie, vedu, filozofiu alebo technológiu.  
  (Napríklad: Kombinácia klasickej sochy Dávida s dátami krypto trhu; cez to spracovanie myšlienky "skamenenia" ľudského vnímania a možnosť odôvodniť to vedeckými zdrojmi.)  
  Dielo musí byť nielen vizuálna hostina, ale aj intelektuálna výzva, ktorá podnecuje zamyslenie nad **Vedou, Filozofiou alebo Technológiou**.

> [!IMPORTANT]
> **Referenčný Príklad (Efekt Las Palmitas):** V oblasti Las Palmitas v Mexiku, ktorá bojuje s kriminalitou, bolo viac ako 200 domov premenených na >obrovskú dúhovú oslavu. V dôsledku tejto estetickej intervencie klesli miery kriminality v oblasti do určitej miery, mladí ľudia sa začali zaujímať o umenie namiesto >gangov. Estetická zmena prekódovala rešpekt ľudí k prostrediu a navzájom (Sociálna Kohézia).
>
> **Očakávanie:** Projekt, ktorý sa dostane na [PoArt] zoznam; ako vo vyššie uvedenom príklade, musí obsahovať sociologickú, vedeckú alebo filozofickú >príčinno-dôsledkovú súvislosť nad rámec vizuálnej estetiky. Keďže jediná vec, ktorú nemožno kúpiť za peniaze, je "Čas", v tomto protokole musí byť čas >dokázaný ako záruka prostredníctvom stakingu. Koncepčný základ projektu musí byť taký silný a univerzálny; že aj v možnom CTO (Community Take Over) >scenári o roky neskôr, komunita môže autonómne udržiavať inovačný potenciál projektu dedením tohto dedičstva.

### 5) Nealgoritimická Vôľa (Non-Algorithmic Agency)

- **Problém:** Dokonalé, ale bezdušné, opakujúce sa digitálne výroby.
- **[PoArt] riešenie:** Originálna vôľa ľudskej bytosti, ktorá môže robiť chyby, riskovať a pociťovať emocionálne výkyvy, musí byť cítiť v diele. Neistota v ťahoch štetcom, neočakávané reakcie materiálu a okamžité rozhodnutia umelca sú **Biologický Podpis**, ktorý odlišuje dielo od "Mechanickej Výroby".

---

## c) Overovací Mechanizmus a Ochrana proti Falšovaniu

Tento systém zabezpečuje, že projekt zostáva spoľahlivý a živý nielen "na začiatku", ale "navždy".

### 📦 Balík Dôkazov (Evidence Pack - The Digital Twin)

Za každým [PoArt] certifikovaným dielom stojí šifrovaný a časovo označený balík dát, ktorý môžu investori stiahnuť:

- **RAW Videozáznamy:** Súvislé surové záznamy momentu výroby.
- **Analýza Metadát:** Dátum vytvorenia súboru, informácie o použitom zariadení a údaje o polohe.
- **Fyzické Referencie:** Dôkazy, že dielo existuje vo fyzickom svete  
  (Napríklad: Aktuálne noviny alebo aktuálne blockchain dáta vedľa diela).

> *Poznámka o konzistencii:* Výraz "balík dôkazov" je spojený s líniou **Evidence Pack → EvidenceRoot → NotarySeal** z predchádzajúcich sekcií; t.j. integrita balíka je reprezentovaná overenou pečaťou.

### 🔄 365-Dňová Aktualizácia (The Sustainability Protocol)

- **Revolučná Funkcia:** V krypto projektoch "Dev" (Vývojár) vypustí token na trh a zvyčajne zmizne po 1-2 mesiacoch (Soft Rug). [PoArt] to robí nemožným.
- **Pravidlo:** Stav "Verified Artist" (Overený Umelec) nie je doživotný. Je platný len **1 rok**.
- **Funkcia:** Umelec/vývojár musí predstaviť komunite každých 365 dní **nové, veľké a overené dielo**.
- **Príkladový Scenár:** Začal si projekt v roku 2026. V januári 2027 systém vydá upozornenie "Obdobie Dôkazu Skončilo". Ak umelec nepredstaví novú výstavu, nové fyzické dielo alebo novú technologickú integráciu, "Značka Dôvery" projektu klesá.
- **Výsledok:** Tento systém zabezpečuje, že **obsah nikdy nestráca svoju relevantnosť** a že investor nežije v strachu *"Je vývojár stále tu?"*. Projekt sa stáva živým štúdiom.

### 🚩 Červená Vlajka (Red Flag Protocol)

**Ak komunita alebo algoritmy zistia akékoľvek falšovanie (použitie AI, odcudzená práca, manipulované video):**

1. Certifikát sa okamžite označí ako **"NEPLATNÝ" (VOID)**.
2. Balíky dôkazov sa verejne označia ako **"Falošné"**.
3. Projekt sa pridá na [PoArt] čiernu listinu. To posilňuje fakt, že v decentralizovanom svete je **reputácia jedinou menou**.

---

## d) Záver: Nie Kasíno, Múzeum

**Pump.fun a Decentralizované Burzy (DEX) sú bohužiaľ teraz kasína; svetlá blikajú, všetci hľadajú rýchle zisky, a kasíno (podvodníci) vždy vyhráva. Dôvod, prečo sme začali projekt tu, je nedostatok dostatočného rozpočtu a existencia existujúceho publika dostupného prostredníctvom živých vysielaní.**

**[PoArt] je pevnosť postavená uprostred tohto kasína.**

- 🎰 Kasína sú založené na kartách; my sme založení na **fyzickej realite**.
- 🃏 Kasína sú otvorené podvodom; my sme otvorení **transparentným dôkazom**.
- ⏳ Kasína sú dočasné; my sa zameriavame na **večnosť umenia a vedy**.

**Token, ktorý používa tento protokol, nie je len "minca"; je to digitálny cenný papier, ktorý obsahuje pot, farbu, kód a filozofiu.**

---

## 🗳️ 6) SPRÁVA A VEREJNÝ REGISTER (Governance & Public Registry)

**Účelom tejto sekcie je: odstránenie [PoArt] štandardu zo sféry "dôvery v ľudí" a premena na udržateľnú verejnú infraštruktúru s registrom + overením + komunitným dohľadom.**

### 6.1 Verejný Register (Public Registry)

- **Public Registry:** Všetky schválené dáta sa zaznamenávajú na adrese `ilhanart.org/registry` (alebo GitHub Registry).

**Registračná logika (odporúčaný štandard - formát JSON cesty):**

Každý záznam, ktorý vstupuje do registra, obsahuje aspoň tieto overené základné polia:

- **Identita a Stav:**
  - `certificate_id` (čitateľná referencia)
  - `status` (active / void)
  - `void_reason` (ak existuje)
  - `visibility` (private / masked / public)
  - `created_at` (časová značka)

- **Vydávajúca Organizácia:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informácie o Diele:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (ak je to možné; pre token-gated identitu)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Kriminalistické Dáta:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Kryptografické Dôkazy:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Správa:**
  - `governance.decision`
  - `governance.veto_threshold`

Register môže mať dve úrovne:
- **1)** Ľudsky čitateľný index (web zoznam / vyhľadávanie / filter)
- **2)** Strojovo čitateľný manifest (JSON záznamy; pre PFE overenie)

**Tu sa "registrácia" stáva overenou z reťaze PFE Evidence Pack → EvidenceRoot → NotarySeal. Register poskytuje účel overenia, nie "tvrdenie".**

---

### 6.2 40 % Komunitné Veto (Token-Gated Governance)

- **40 % Komunitné Veto:** Hlasovanie začína mesiac pred získaním stavu; 40 % námietka **Token-Gated (Solana-Verified)** komunity anuluje žiadosť.

**Tok hlasovania (odporúčaný čistý proces):**
- **Kandidátske okno:** Kandidátsky projekt otvorí "PoArt kandidát registráciu" (kandidátske registrácie sa zobrazujú so stavom "pending").
- **Obdobie revízie:** Počas 30 dní komunita skúma dôkazy (Evidence Pack + živé záznamy + metadáta).
- **Token-gated overenie:** Hlasovanie sa vykonáva prostredníctvom peňaženiek overených na Solana (napr. vlastníctvo konkrétneho tokenu/NFT + podpis peňaženky).
- **Veto pravidlo:** Ak je 40 % hlasov **námietka (NO / VETO)**, žiadosť sa zamietne.
- **Transparentnosť:** Výsledok hlasovania sa uloží v registri ako "decision record" (dátum, pomer, snapshot ID).

---

### 6.3 Synchronizácia Metadát (Zhoda s Fyzickým Svetom)

- **Metadata Sync:** Technické dáta v registri musia zodpovedať 100 % fyzickému aktívu.

**Technická definícia "100 % zhody" (odporúčaná jasnosť):**
- **Minimálna zhoda (povinná):**
  - `asset.fingerprints.sha256/sha512` v registri musí byť **presne rovnaký** ako hash súboru v ruke.
  - `proof.notary_seal` v registri, keď sa reprodukuje (ak existuje Evidence Pack), musí byť **presne rovnaký**.
- **Zhoda fyzickej referencie (typ dôkazu):**
  - Dôkazy ako fyzické dielo zobrazené naživo + dátum/blok referencia musia byť konzistentné s Evidence Pack.
- **Zhoda súkromia:**
  - Polia ako IP/poloha v `masked` viditeľnosti sa publikujú **podľa štandardu maskovania**.

---

### 6.4 Spor, Revízia a Zrušenie (Dispute & Revocation)

Register nie je len "schvaľovací mechanizmus"; je to **živý dohľadový mechanizmus proti falšovaniu**.

- Keď sa iniciuje spor, záznam môže byť nastavený do režimu **"review"**.
- Ak sa zistí falšovanie, označí sa ako `status: void` a pridá sa dôvod:
  - `void_reason` (použitie AI / plagiát / manipulácia atď.)
  - `revoked_at` (moment zrušenia)
- Zdroj rozhodnutia o zrušení je jasne viditeľný v registri:
  - komunitné hlasovanie / autorizovaná rada / poznámka kriminalistického vyšetrovania (v závislosti od toho, čo platí)

> **Táto sekcia je registerový ekvivalent pojmu VOID v sekcii "Red Flag Protocol".**

---

### 6.5 Príklad Záznamu v Registri (Strojovo Čitateľný)
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
    "title": "Bez názvu",
    "creator": "Anonymný",
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
> *Poznámka: `asset.fingerprints.sha512` a iné hash hodnoty sú skrátené na demonštračné účely; v reálnej aplikácii sa používa hexadecimálny reťazec plnej dĺžky.*

---

## 7) 🔐 TECHNICKÁ PEČAŤ (NOTARY SEAL)

**PoArt Forensic Engine (PFE) v1.0** neotrasiteľný algoritmus zapečatenia vyrobený s:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] protokol Digitálny Notár a Kriminalistický Dôkaz (Beta v1.0)

> **"Kultúra Väčšia ako Kapitál. Chráň svoje diela dnes, vezmi ich do zajtrajška."**

---

## Prečo Verejný?

Skutočná bezpečnosť pochádza z transparentnosti. Vďaka nášmu systému **Public Registry (Verejný Register)** môže osoba kdekoľvek na svete overiť za pár sekúnd, či je súbor, ktorý má v ruke, originálny, bez akejkoľvek autority.

---

## 🧩 Prečo Existuje Viacero "Modulov Viditeľnosti"?

Najkritickejšia časť kódu je tu (menu výberu viditeľnosti). Tieto možnosti umožňujú používateľom vyvážiť **"Súkromie vs. Transparentnosť"**:

### 🔒 Súkromný (Private)

- **Scenár:** Umelec ešte nechce publikovať dielo, ale chce ho časovo označiť a dokázať "urobil som to tento dátum".
- **Čo Kód Robí:** Ukladá dáta do databázy, ale aplikuje štítok `visibility: "private"`. V budúcnosti, keď napíšete politiku "Public Read", môžete skryť tieto záznamy pred verejnosťou povedaním `WHERE visibility = 'public'`.

### 🕶️ Maskovaný (Masked)

- **Scenár:** Umelec chce transparentnosť, ale obáva sa, že sa nájde adresa domu (IP poloha).
- **Čo Kód Robí:** Na strane JavaScript fungujú funkcie `maskIP` a `maskLoc`. Konvertuje IP adresu na formát `88.241.***.***` a polohu na formát `***/TR` a posiela cenzurovanú verziu do databázy.
- **Poznámka o Súkromí:** Maskovanie sa deje v prehliadači, Supabase nevidí skutočnú polohu. **Avšak:** Ak sa používajú API tretích strán ako ipapi.co pre údaje o polohe, títo poskytovatelia vidia IP adresu v momente požiadavky.
- **Zapečatenie v Masked režime:** Výpočet EvidenceRoot a NotarySeal sa vykonáva s maskovanými forensics dátami; takže overenie zostáva deterministické.

### 🌍 Verejný (Public)

- **Scenár:** Plná transparentnosť. Podľa [PoArt] štandardu, kde, kedy a z ktorej siete bolo dielo vyrobené, sa vyhlasuje explicitne.

---

## 💡 Technologická Inovácia

PoArt nie je len systém nahrávania súborov. Je to **"Forensic Chain of Custody"** motor, ktorý roztápa tri rôzne technologické vrstvy do jedného tiegla a prináša nový štandard.

**Vrstva opísaná v tejto sekcii ako "motor" zodpovedá jadru PoArt Forensic Engine (PFE) v predchádzajúcej terminológii.**

### 1) Client-Side Hashing (Maximálne Súkromie)

Súbory vašich diel sa nikdy nenačítajú na server. Náš motor založený na prehliadači (Client-side) vypočíta hash (digitálny digest) súboru na vašom počítači. Len tento odtlačok a metadáta sa posielajú na server.

> **Poznámka o Súkromí:** Súbor diela sa nenačíta na server a je tak chránený. Avšak forensics dáta (IP/poloha) sa zdieľajú podľa zvoleného režimu viditeľnosti (private/masked/public).

### 2) Forensic Data Fusion (Kriminalistická Sila)

To je oveľa viac ako jednoduchá časová značka. Systém kombinuje nasledujúce dáta do jednej "Genesis Seal":

- **Digitálny Digest (SHA-512):** Použitím štandardu kryptografického digestu (SHA-512), digitálny odtlačok, ktorý sa rozpadne, aj keď sa zmení jeden pixel diela.
- **Poloha a Čas:** Dátum s presnosťou na milisekundy, krajina, mesto a oblasť, kde bola transakcia vykonaná.
- **Identita Zariadenia:** Operačný systém, prehliadač a typ zariadenia (User-Agent analýza).

---

## 🛡️ Oblasti Aplikácie a Výhody

Ak ste umelec, spisovateľ alebo dizajnér, nestačí povedať "Urobil som to skôr", musíte to dokázať.

**Dielo zapečatené s PoArt:**

- **Matematický Dôkaz:** Systém to zistí, aj keď sa zmení jeden pixel súboru. Manipulácia je nemožná.
- **Právny Základ:** Je zaznamenané, ktorý dátum, v ktorom meste, z ktorého zariadenia bolo dielo zapečatené.
- **Okamžitý Certifikát:** Za pár sekúnd generuje personalizovaný **"Certifikát Identity Aktíva"** s QR kódom a zapečatený.

---

## ⚙️ Architektúra Systému a Technické Špecifikácie

Systém je navrhnutý na architektúre "Serverless" (Bez Servera), zameranej na vysoký výkon a škálovateľnosť.

| Vrstva | Technológia | Popis |
|--------|-----------|----------|
| **Kryptografia** | SHA-256 & SHA-512 | Dvojvrstvový kryptografický digest |
| **Databáza** | Supabase (PostgreSQL) | JSONB dátová štruktúra, RLS politiky |
| **Kriminalistické Dáta** | ipapi.co API | IP/Poloha/Čas triáda |
| **Renderovanie** | html2canvas + jsPDF | PNG/PDF generovanie na strane klienta |
| **Frontend** | Vanilla JavaScript | Nula framework závislostí |
| **Bezpečnosť** | Client-side hashing | Súbor nikdy nedosiahne server |

### Rozlišujúce Charakteristiky

| Charakteristika | Detail | U Konkurentov? |
|---------|-------|-------------|
| **Drag & Drop UI** | Potiahnite a pustite súbor, okamžitý náhľad | ❌ Chýba u väčšiny |
| **Multi-Format Export** | PNG, JSON, PDF - jedno kliknutie | ⚠️ Obmedzené |
| **Real-Time Preview** | Náhľad certifikátu v reálnom čase | ❌ Chýba |
| **Privacy Controls** | Private/Masked/Public možnosti | ❌ Chýba |
| **Client-Side Hashing** | Súbor nikdy nedosiahne server | ✅ Len u niektorých |
| **Forensic Metadata** | IP, poloha, zariadenie, čas - všetko spolu | ❌ Fragmentované |
| **QR Verification** | QR kód pre okamžité overenie | ⚠️ Obmedzené |
| **Rate Limiting** | Ochrana proti spamu (RLS + Client) | ❌ Chýba u väčšiny |

---

## 🗺️ Cestovná Mapa: "Trustless" Budúcnosť

Súčasná verzia **(Beta v1.0)** je optimalizovaná na poskytnutie koncovému používateľovi maximálnej rýchlosti, jednoduchého rozhrania a bezplatného prístupu. Avšak naša konečná vízia je prechod na štruktúru, kde ani správca databázy (my) nemôže zasahovať.

### Fáza 1: Beta (Teraz Dostupná)

- **Infraštruktúra:** Cloud Database (Supabase).
- **Účel:** Rýchlosť, odstránenie UX (Používateľská Skúsenosť) bariér a adaptácia. Zabezpečenie "bez trenia" bezpečnosti.

### 🚀 Fáza 2: (Čo Vyžaduje Backend / Edge Function)

Táto fáza pokrýva prechod z úplne "Client-Side" fungujúcej štruktúry systému na bezpečnejšiu a spravovanejšiu "Server-Side Authority" štruktúru.

| Element | Čo Prináša? | Tech Stack | Priorita |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Function** | Blokovanie spamu + bezpečnosť API kľúča | Supabase Edge (Deno) | 🔴 Vysoká |
| **Podpis Peňaženky** | Kryptografické overenie identity | Solana Wallet Adapter | 🟡 Stredná |
| **IPFS/Arweave Záloha** | Decentralizovaná nemennosť | IPFS SDK + Pinata | 🟢 Nízka |
| **Mechanizmus Zrušenia** | Zneplatnenie falošných certifikátov | DB Schema aktualizácia | 🔴 Vysoká |
| **Audit Log** | Kriminalistické vyšetrovanie zaznamenanie | Vlastná log tabuľka | 🟡 Stredná |
| **OpenTimestamps** | Bitcoin zakotvenie | OTS JavaScript | 🟢 Nízka |
| **DID integrácia** | Decentralized Identity | ION/Ceramic | 🟢 Nízka |

### Fáza 3: Úplná Decentralizácia (Dlhodobo)

| Charakteristika | Účel | ETA |
|---------|-------|-----|
| **Blockchain Registry** | On-chain registrácia Ethereum/Solana | Q4 2026 |
| **DAO Governance** | Komunitná správa | Q1 2027 |
| **Multi-Chain Support** | Polygon, Arbitrum, Base | Q2 2027 |
| **Legal Recognition** | Platnosť v tureckých súdoch | 2027-2028 |
| **API for Developers** | Verejný API endpoint | Q3 2026 |

---

## 📊 Analýza Konkurentov (Aktualizovaná)

PoArt je umiestnený na "Sweet Spot" (Optimálny Ideálny Bod), ktorý dopĺňa medzery v existujúcich riešeniach.

| Charakteristika | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 証 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Cena** | 🆓 Zadarmo | 🆓 | 💰 Platené | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Veľmi Jednoduché | ❌ CLI | ⚠️ Stredné | ⚠️ Stredné | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ V Reálnom Čase | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Režimy | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Súkromie | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Kompletné | ❌ | ❌ | ⚠️ Obmedzené | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Okamžité | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Cestovná mapa | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Natívna jazyková podpora** | 🔄 Vo vývoji | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Legenda:**
- ✅ : Plná podpora / dostupné
- ⚠️ : Obmedzené / v platených plánoch
- ❌ : Chýba / nie je podporované
- 🔄 : Na Cestovnej Mape (vo vývoji)
- 🆓 : Úplne zadarmo
- 💰 : Platené / vyžaduje sa predplatné

### Nedostatky Konkurentov, Silné Stránky PoArt

| Mínus | Konkurenti | PoArt |
|------|----------|-------|
| **Zložitosť Používania** | CLI, API znalosti, peňaženka vyžadovaná | Potiahnite a pustite, končí za 3 kliknutia |
| **Cenová Bariéra** | Predplatné $50-500/mesiac | 100 % zadarmo |
| **Súkromie** | Súbor sa načíta na server | Client-side, súbor nikdy neopustí |
| **Kriminalistické Dáta** | Len časová značka | IP, poloha, zariadenie, čas - všetko |
| **Slovenská Podpora** | Chýba alebo veľmi obmedzená | Natívna jazyková podpora |
| **Open Source** | Zatvorená škatuľa | Celý kód otvorený na GitHub |

---

## 🧬 Dátová Štruktúra Protokolu (JSON Schema)

**Každý [PoArt] certifikát má prenosnú a overiteľnú JSON identitu vyrobenú podľa nasledujúceho štandardu.**

> **Poznámka:** Tento Identity JSON formát je formát certifikátu prezentovaný používateľovi. V registerových záznamoch sa namiesto `identity.asset_data` používa `registry.asset` (mapovanie: `identity.asset_data` == `registry.asset`).
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
    "title": "Oficiálny Whitepaper",
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

## 🔬 Technická Hĺbka: Algoritmus Zapečatenia

### Deterministické Hash Funkcie
```javascript
// Pomocné Funkcie: Konverzia digestu na hex reťazec
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Konverzia reťazca na pole bytov
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Generovanie kanonického forensics reťazca (v1.0: fixné poradie polí + UTF-8 + oddeľovač \n)
// Poznámka Fáza 2: Prechod na kanonický JSON s RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal Proces Výroby (Úplne Deterministický)
```javascript
// 1. FileHash výpočet (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Zber kriminalistických dát (použitie jednej časovej značky)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Generovanie jednej časovej značky
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Rovnaká časová značka
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot vytvorenie (s kanonickým kódovaním)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal výroba (použitie rovnakej časovej značky)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Pomocné funkcie maskovania (IPv4 a IPv6 podpora)
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4 kontrola
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 alebo neznámy formát
  return "***";
}
```

### Tok Overenia (Dve Úrovne)

#### Quick Verify (Rýchle Overenie)
```javascript
// Kontroluje len hash súboru (rýchla červená vlajka)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Získanie z Registra
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Hash porovnanie
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Originál - Hash súboru sa zhoduje"
    };
  } else {
    return {
      valid: false,
      message: "❌ Falošný - Súbor bol manipulovaný"
    };
  }
}
```

#### Full Verify (Úplné Overenie)
```javascript
// Reprodukuje a overuje EvidenceRoot a NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Získanie z Registra
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash kontrola (rýchla červená vlajka)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Falošný - Hash súboru sa nezhoduje" };
  }

  // 2) EvidenceRoot reprodukcia (s forensics dátami uloženými v registri)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Nezhoduje sa - EvidenceRoot neplatný" };
  }

  // 3) NotarySeal reprodukcia (s rovnakou časovou značkou + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Nezhoduje sa - NotarySeal neplatný" };
  }

  // Voliteľné: Vo fáze 2 overte tiež signer_sig s attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Podpis neplatný" };

  return { valid: true, message: "✅ Originál - Full Verify schválené" };
}
```

> **Dôležité Poznámky:**
> - **Quick Verify:** Kontroluje len hash súboru pre rýchle použitie.
> - **Full Verify:** Overuje všetky vrstvy protokolu (EvidenceRoot + NotarySeal).
> - Všetky hash operácie sa vykonávajú deterministicky, s fixným kódovaním a oddeľovačmi.
> - **v1.0 štandard kanonizácie:** Fixné poradie polí + UTF-8 kódovanie + `\n` oddeľovač.
> - **Plán Fáza 2:** Prechod na kanonický JSON s RFC 8785 (JCS - JSON Canonicalization Scheme).
> - V Masked režime sa výpočet EvidenceRoot a NotarySeal vykonáva s maskovanými forensics dátami.
> - Používa sa jedna časová značka v celom procese (forensics + NotarySeal); determinizmus zaručený.
> - **Forensics názvy polí:** `ip_masked`, `location`, `device`, `timestamp` (kód a register úplne kompatibilné).
> - **Cesta Registra:** `certificate.asset.fingerprints` (úplne kompatibilné s kódom overenia).
> - **signer_sig v Registri:** Pole `proof.signer_sig` je potrebné pre Full Verify.
> - Mechanizmus SignerSignature bude aktivovaný vo fáze 2 so Solana Wallet Adapter; v v1.0 možno vykonať overenie s `attestation_pubkey`.

---

## 📈 Štatistiky Používania (Q1 2026 Ciele)

| Metrika | Cieľ | Stav |
|--------|-------|-------|
| **Celkové Certifikáty** | 1,000 | 🔄 Prebieha |
| **Aktívni Používatelia** | 500 | 🔄 Prebieha |
| **Počet Overení** | 5,000 | 🔄 Prebieha |
| **Uptime** | %99.9 | ✅ Aktívny |
| **Priemerný Čas Odpovede** | <200ms | ✅ Optimálny |

---

## 🌍 Komunita a Podpora

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 Prispievatelia

PoArt protokol sa vyvíja vďaka príspevkom komunity s otvoreným zdrojom.

**Pre príspevok:**
1. Urobte fork
2. Vytvorte vetvu funkcie (`git checkout -b feature/amazing-feature`)
3. Urobte commit (`git commit -m 'Add amazing feature'`)
4. Urobte push (`git push origin feature/amazing-feature`)
5. Otvorte Pull Request

### 🛠️ Čo Potrebujeme Teraz? (Výzva na Pomoc)

Hľadáme príspevky od skúsených vývojárov v nasledujúcich témach pre vývoj **Fázy 2** PoArt protokolu:

* **Supabase Edge Functions:** Presunutie ochrany proti spamu na stranu servera.
* **Solana Web3.js:** Integrácia podpisovania peňaženky (Wallet Signing).
* **IPFS / Arweave:** Integrácia archivačných a zakotvovacích služieb.

> Pred pridaním funkcie, prosím začnite diskusiu v sekcii "Issues".

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Kultúra Väčšia ako Kapitál*

## 🧾 Licencia

MIT License © 2026 İlhan Art Gallery Initiative

Pozrite si [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) pre úplné podmienky.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Tento projekt bol vyvinutý s iniciatívou [İlhan Art Gallery] a zdrojový kód je verejne dostupný pre transparentnosť.**

**PROTOKOL V1.0 // ZAPEČATENÉ SO SHA-512.**

*© 2026 İLHAN ART | VŠETKY PRÁVA NA DIELA, OBRÁZKY A MYŠLIENKY SÚ CHRÁNENÉ.*

---
