# 📚 SŁOWNIK TERMINOLOGII I KONCEPCJI
> **"Zrozumienie języka tego protokołu oznacza zrozumienie jego wizji."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Infrastruktura Podstawowa

**PoArt Forensic Engine (PFE)** jest główną warstwą reprezentującą podstawową logikę i techniczne funkcjonowanie protokołu [PoArt]. To jest "silnik kryminalistyczny", który przekształca surowe dane produkcyjne dzieła sztuki w weryfikowalny i niezmienny **dowód cyfrowy**.

### 🧩 Dlaczego "PoArt Forensic"?

- **PoArt (Proof of Art):** Fokus silnika polega na powiązaniu wartości zasobu cyfrowego nie ze spekulacją, ale z **weryfikowalnym procesem produkcji**.
- **Forensic (Weryfikacja Kryminalistyczna):**
  - **Definicja Techniczna:** Algorytmiczne podejście i łańcuch dowodów w celu weryfikacji, że dane dotyczące procesu produkcji (pociągnięcia pędzlem, timelapse, logi) nie zostały zmanipulowane.
  - **Warstwa Filozoficzna:** Przeciwko "natychmiastowej produkcji" sztucznej inteligencji; twierdzenie o przekształceniu ludzkiej produkcji zawierającej **czas, wysiłek i koszt decyzyjny** w mierzalną rzeczywistość.

> Uwaga: Integracja blockchain (np. Solana) nie jest rdzeniem PFE; zostanie zdefiniowana osobno jako **Chain Anchor Layer** do weryfikacji/rejestru.

### 🛠️ Zakres Techniczny v1.0

**PoArt Forensic Engine (PFE) v1.0** jest zbudowany na **3 głównych filarach** zamiast skomplikowanych modeli finansowych:

1. **Hashing & Sealing (Pieczętowanie):**  
   PFE deterministycznie przetwarza wszystkie elementy w Evidence Pack (plik dzieła, wideo, JSON/log, podpis itp.) i generuje unikalną wartość **NotarySeal**.

   **Podstawowe koncepcje (v1.0):**
   - **FileHash (odcisk palca dzieła):** Hash generowany z bajtów pliku dzieła.
   - **EvidenceRoot (korzeń pakietu dowodów):** Skrót korzenia reprezentujący integralność Evidence Pack (Merkle root lub hash kanonicznego manifestu).
   - **NotarySeal (ostateczna pieczęć / Wyjście PFE):** Ostateczna pieczęć generowana z połączenia EvidenceRoot + czas + podpis.

   **Formuły (w formacie przejrzystym dla inwestorów):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Definicje Canonical Payload (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Uwaga: Wartość zamierzona jako wyjście PFE to **NotarySeal**. Mechanizm **SignerSignature** zostanie aktywowany w Fazie 2 (z Solana Wallet Adapter); w obecnej wersji v1.0 używany jest własny podpis atestacyjny systemu. Klucz publiczny atestacji jest publikowany w rejestrze w polu `issuer.attestation_pubkey`.

2. **Indexing (Archiwizacja):**  
   Rejestruje, który portfel, w jakiej dacie, przedstawił **Labor Proof (Dowód Pracy)** dla jakiego dzieła; w przejrzystej i queryowalnej warstwie rejestru.  
   *(Ta warstwa może być bazą danych; integracja blockchain jest zamiast tego zdefiniowana osobno jako "Chain Anchor Layer".)*

3. **Verification (Weryfikacja):**  
   Gdy oryginalność dzieła jest kwestionowana, PFE ponownie przetwarza surowe dowody; testuje z matematyczną pewnością, czy obliczone wartości **EvidenceRoot / NotarySeal** odpowiadają zapisom w archiwum.

---

### 🧮 Twierdzenie o Wartości PoArt (The Value Theorem)

Protokół [PoArt] łączy wartość ($V$) zasobu cyfrowego nie z subiektywną percepcją rynku, ale z **fizyczną rzeczywistością procesu produkcji**.

Sztuczna Inteligencja (AI) anuluje proces, dostarczając natychmiastowe wyniki ($t \to 0$). [PoArt] natomiast traktuje wartość jako akumulację komponentów **czasu, pracy i woli**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definicja Zmiennych

- **$\int dt$ (Akumulacja Procesu):**  
  Wartość nie jest natychmiastowym "outputem"; jest **procesem**, który akumuluje się między $t_{\text{start}}$ a $t_{\text{end}}$. W miarę jak czas się zmniejsza (produkcja AI), wynik całki zbliża się do 0.

- **$P_{\text{labor}}(t)$ (Natychmiastowa Intensywność Pracy):**  
  Reprezentuje intensywność wysiłku umysłowego i fizycznego wydanego w momencie produkcji. W miarę jak weryfikowalny wysiłek wzrasta, całkująca rośnie.  
  > Uwaga: Ten termin może być w praktyce znormalizowany na "mierzalnych/weryfikowalnych sygnałach pracy".

- **$I_{\text{agency}}(t)$ (Współczynnik Woli):**  
  Jest to zdolność producenta do podejmowania ryzyka i podejmowania decyzji. Przyjmuje wartość między $0$ a $1$.
  - **AI ($I \approx 0$):** Wykonuje polecenia, nie podejmuje ryzyka, nie ponosi kosztów.
  - **Człowiek ($I \to 1$):** Zmienia decyzje, waha się, podejmuje ryzyko.

- **$U_{\text{irreversible}}$ (Nieodwracalna Unikalność):**  
  Podczas gdy w produkcji cyfrowej można cofnąć (`Ctrl+Z`); w produkcji fizycznej (farba nałożona na płótno, wyrzeźbiony marmur, gest podczas transmisji na żywo) nie ma powrotu. Ta **nieodwracalność** jest dodatkowym terminem tworzącym "unikalność" (charakter non-fungible) w dziele.

### 🔎 Analiza Przypadku: AI "Natychmiastowe Wyjście" vs. Człowiek "Udowodniony Proces"

Poniższy scenariusz pokazuje, jak **Twierdzenie o Wartości PoArt** działa w praktyce i dlaczego produkcje AI otrzymują niskie wyniki w standardzie [PoArt].

#### Scenariusz A: Produkcja Wizualna z AI w 10 Sekund

- **Czas trwania ($\Delta t$):** $10$ sekund (proces prawie nieistniejący)
- **Intensywność Pracy ($P_{\text{labor}}$):** $1$ jednostka (tylko pisanie polecenia)
- **Współczynnik Woli ($I_{\text{agency}}$):** $0.01$ (brak ryzyka, brak kosztów)
- **Nieodwracalność ($U_{\text{irreversible}}$):** $0$ (odwracalne / kopyjowalne)

**Wynik:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Komentarz:** Nawet jeśli output jest doskonały; ponieważ proces nie został przeżyty i nie zawiera woli/ryzyka, wartość [PoArt] zbliża się do $0$.

#### Scenariusz B: Fizyczna Produkcja na Żywo przez 6 Godzin

- **Czas trwania ($\Delta t$):** $6$ godzin ($21{,}600$ sekund)
- **Intensywność Pracy ($P_{\text{labor}}$):** $0.5$ jednostki (ciągłość wysiłku fizycznego i umysłowego)
- **Współczynnik Woli ($I_{\text{agency}}$):** $0.9$ (zmiana decyzji, podejmowanie ryzyka, nieodwracalne wybory)
- **Nieodwracalność ($U_{\text{irreversible}}$):** $>0$ (ślady fizyczne nie mogą być cofnięte)

**Wynik:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Komentarz:** W miarę jak proces się wydłuża i wola (ryzyko) wzrasta, wartość akumuluje się kumulatywnie. Termin $U_{\text{irreversible}}$ jest dodatkowym wkładem tworzącym "unikalność" (charakter non-fungible) w dziele.

---

### ✅ Wniosek: Wartość Związana z Dowodem (Proof-Bound Value)

To twierdzenie usuwa twierdzenie o wartości [PoArt] z bycia "polubienia" lub "narracji rynkowej" i wiąże je z **weryfikowalną rzeczywistością produkcji**.

1. **Bez Procesu Nie Tworzy Się Wartość:**  
   AI anuluje proces w natychmiastowym wyjściu ($t \to 0$). W miarę jak okno procesu się zwęża, wynik całki maleje z matematycznej konieczności:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Wola i Ryzyko Są Mnożnikami:**  
   [PoArt] mierzy nie tylko "spędzony czas", ale także rzeczywisty poziom decyzji, ryzyka i kosztów podczas tego czasu. Wartość produkcji, która nie podejmuje ryzyka (AI), jest niska:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Unikalność Jest Fizycznym Dowodem, Nie Marketingiem:**  
   W produkcji fizycznej nieodwracalne ślady (pociągnięcie pędzlem na płótnie, złamanie marmuru) są poza logiką `Ctrl+Z` cyfrowego. Ta nieodwracalność ($U_{\text{irreversible}}$) czyni dzieło ontologicznie unikalnym.

> **🔐 PODSUMOWANIE:** Chociaż twierdzenie o wartości może wydawać się niepewne jako pomiar (nawet jeśli nie można go zmierzyć w 100% w prawdziwym życiu), celem tej formuły jest pokazanie struktury i kierunku zmiennych. To, co jest rzadkie w erze AI, to nie "obraz", ale **weryfikowalna praca, czas i wola.** [PoArt] mierzy ten niedobór i rejestruje go za pomocą **Evidence Pack**.

### 🏛️ Znaczenie Koncepcji "Engine" (Silnik)

Tokeny wyłaniające się z platform takich jak Pump.fun są często tylko **"biletami dostępu"**. **PoArt Forensic Engine (PFE)** jest natomiast **konstytucyjną warstwą logiczną**, która określa, jakie prawa chroni ten bilet, jak rejestrowana jest praca i jak sztuka/nauka/technologia jest utrwalana.

> **Uwaga:** Powodem, dla którego uruchomiliśmy ten projekt na Pumpfun, jest to, że nie mieliśmy wystarczającej płynności i obserwujących. Wykorzystanie istniejących danych było strategicznie właściwym ruchem, choć nie najbardziej jakościowym. Zdefiniowanie logiki tego silnika na GitHubie, niezależnie od budżetu i zasobów, dowodzi, że projekt nie jest tylko spekulacją finansową, ale długoterminową wizją **infrastruktury oprogramowania** i **cyfrowej biblioteki narodowej**.

---

## 🎨 PROTOKÓŁ [PoArt] PROOF OF ART (Proof of Art Protocol v1.0)

> **"Prawdziwy Artysta, Prawdziwa Produkcja, Prawdziwa Wartość."**

Ten protokół jest **biologicznym i intelektualnym mechanizmem obronnym** opracowanym przeciwko anonimowym oszustom nękającym ekosystem kryptowalut, obrazom sztucznej inteligencji wyprodukowanym w 5 minut i kulturze "Pump & Dump" (Pompuj i Zrzuć).

---

## a) Czym Jest [PoArt]? (Definicja Filozoficzna i Techniczna)

**Proof of Art [PoArt];** jest instytucjonalnym standardem weryfikacji, który gwarantuje, że wartość stojąca za zasobem na blockchainie opiera się nie na spekulacji, ale na weryfikowalnej **pracy ludzkiej**, **czasie** i **energii fizycznej**.

Tak jak Bitcoin produkuje wartość za pomocą *"Elektryczności i Mocy Obliczeniowej"* **(Proof of Work)**; projekty zgodne z [PoArt] produkują wartość za pomocą *"Umiejętności Artystycznych i Czasu Ludzkiego"*.

Eliminuje ryzyko *"Deweloper (Dev) sprzedał, projekt skończony"* obecne na Pump.fun i platformach DEX; ponieważ tutaj wartość nie jest w kodzie, ale w **ciągłości produkcji**.

> **[PoArt] nie mówi uczestnikowi "Zaufaj nam"; mówi "Oto dowody, zobacz własnymi oczami, zweryfikuj swoją matematyką".**

---

## b) 5-Filarowy Standard [PoArt] (The 5 Pillars of Truth)

Te 5 punktów to niemanipulowalne filtry, które projekt musi przejść, aby uzyskać pieczęć [PoArt].

### 1) Dowód Tożsamości na Żywo (Live Identity Proof)

- **Problem:** Świat kryptowalut jest pełen anonimowych założycieli (Dev) o niepewnej tożsamości, którzy zbierają pieniądze i porzucają projekt.
- **Rozwiązanie [PoArt]:** Producent udowadnia nie tylko dowód osobisty, ale **swoją obecność podczas produkcji**. Obejmuje to sesje transmisji na żywo, w których wchodzi się w interakcję ze społecznością i spełnia konkretne natychmiastowe żądania, a nie z nagraniami wideo.  
  (Np.: *"Napisz dzisiejszą datę i bieżący numer bloku w prawym rogu płótna"*)
- **Motto:** *"Boty mogą rysować, ale boty nie pocą się i nie improwizują."*

### 2) Dowód Pracy i Procesu (Labor & Process Proof)

- **Problem:** Obrazy AI wyprodukowane w 2 sekundy i obrazy olejne wykonane w 2 miesiące są traktowane jako ten sam "jpeg" w świecie cyfrowym.
- **Rozwiązanie [PoArt]:** Proces "ciąży i narodzin" dzieła jest rejestrowany. Etapy szkicu, warstwy farby, skumulowane spędzone godziny i fizyczny proces przeżyty przez artystę podczas tworzenia dzieła są dokumentowane. To dodaje **"Koszt Czasowy" (Time Cost)** do tokena. Im trudniej wyprodukować zasób, tym mocniejsza jest jego wartość.

### 3) Dowód Wartości Estetycznej (Aesthetic Value Proof)

- **Problem:** Estetyka i głębia artystyczna kultury "Meme", która ignoruje wszystko i skupia się tylko na natychmiastowej komedii, oraz krótkotrwałe projekty "Hype", które z tego wynikają.
- **Rozwiązanie [PoArt]:** Projekt musi posiadać akademickie standardy artystyczne, teorię koloru, zasady kompozycji i wiedzę o materiałach (Impasto, Tekstura itp.). Treść nie powinna tylko śmieszyć; powinna wzbudzać podziw u widza i mieć **wartość kolekcjonerską**.

### 4) Innowacja Koncepcyjna (Conceptual Novelty)

- **Problem:** Tysiące identycznych coinów psów/kotów, dalekich od kreatywności.
- **Rozwiązanie [PoArt]:** Projekt musi zbudować nowy pomost łączący w znaczący sposób sztukę, naukę, filozofię lub technologię.  
  (Np.: Połączenie klasycznej statui Dawida z danymi rynku kryptowalut; opracowanie poprzez to idei "skamienienia" percepcji ludzkiej i możliwość ugruntowania tego źródłami naukowymi.)  
  Dzieło musi być nie tylko wizualną ucztą, ale także intelektualnym wyzwaniem, które skłania do refleksji nad **Nauką, Filozofią lub Technologią**.

> [!IMPORTANT]
> **Przykład Odniesienia (Efekt Las Palmitas):** W dzielnicy Las Palmitas w Meksyku, borykającej się z przestępczością, ponad 200 domów zostało przekształconych w gigantyczną tęczową ucztę. W wyniku tej >interwencji estetycznej wskaźniki przestępczości w dzielnicy spadły do pewnego stopnia, młodzi ludzie zaczęli interesować się sztuką zamiast gangami. Zmiana estetyczna >przekodowała szacunek ludzi dla środowiska i siebie nawzajem (Spójność Społeczna).
>
> **Oczekiwanie:** Projekt, który wejdzie na listę [PoArt]; tak jak w powyższym przykładzie, musi zawierać socjologiczny, naukowy lub filozoficzny związek przyczynowo-skutkowy poza estetyką wizualną. Ponieważ jedyną rzeczą, której nie można kupić za pieniądze, jest "Czas", w tym protokole czas musi być udowodniony jako >gwarancja poprzez staking. Podstawa koncepcyjna projektu musi być tak silna i uniwersalna, że; nawet w scenariuszu możliwego CTO (Community Take Over) po latach, >społeczność może autonomicznie podtrzymywać innowacyjny potencjał projektu, dziedzicząc to dziedzictwo.

### 5) Wola Niealgorytmiczna (Non-Algorithmic Agency)

- **Problem:** Doskonałe, ale bezduszne produkcje cyfrowe, które się powtarzają.
- **Rozwiązanie [PoArt]:** Oryginalna wola istoty ludzkiej, która może popełniać błędy, podejmować ryzyko i doświadczać wahań emocjonalnych, musi być odczuwalna w dziele. Niepewność w pociągnięciach pędzla, nieoczekiwane reakcje materiału i natychmiastowe decyzje artysty to **Podpis Biologiczny**, który odróżnia dzieło od "Produkcji Mechanicznej".

---

## c) Mechanizm Weryfikacji i Anty-Podróbki

Ten system zapewnia, że projekt pozostanie wiarygodny i żywy nie tylko "na początku", ale "na zawsze".

### 📦 Pakiet Dowodów (Evidence Pack - The Digital Twin)

Za każdym dziełem certyfikowanym [PoArt] znajduje się zaszyfrowany i oznaczony znacznikiem czasu pakiet danych, który inwestorzy mogą pobrać:

- **Nagrania Wideo RAW:** Nieprzerwane surowe nagrania momentu produkcji.
- **Analiza Metadanych:** Data utworzenia pliku, informacje o używanym urządzeniu i dane lokalizacji.
- **Odniesienia Fizyczne:** Dowody, że dzieło istnieje w świecie fizycznym  
  (Np.: Aktualna gazeta lub bieżące dane blockchain obok dzieła).

> *Uwaga dotycząca spójności:* Wyrażenie "pakiet dowodów" łączy się z linią **Evidence Pack → EvidenceRoot → NotarySeal** z poprzednich sekcji; czyli integralność pakietu jest reprezentowana przez weryfikowalną pieczęć.

### 🔄 Odnowienie na 365 Dni (The Sustainability Protocol)

- **Rewolucyjna Funkcja:** W projektach kryptowalutowych "Dev" (Deweloper) uruchamia token na rynek i zazwyczaj znika po 1-2 miesiącach (Soft Rug). [PoArt] czyni to niemożliwym.
- **Zasada:** Status "Verified Artist" (Zweryfikowany Artysta) nie jest dożywotni. Jest ważny tylko przez **1 rok**.
- **Funkcjonowanie:** Artysta/deweloper musi co 365 dni przedstawić społeczności **nowe, duże i weryfikowalne dzieło**.
- **Przykładowy Scenariusz:** Uruchomiliście projekt w 2026 roku. W styczniu 2027 system wyświetla ostrzeżenie "Okres Dowodu Wygasł". Jeśli artysta nie przedstawi nowej wystawy, nowego dzieła fizycznego lub nowej integracji technologicznej, "Odznaka Zaufania" projektu spada.
- **Wynik:** Ten system zapewnia, że **treść nigdy nie traci aktualności** i że inwestor nie żyje w strachu *"Czy deweloper jest wciąż tutaj?"*. Projekt staje się żywym studiem.

### 🚩 Czerwona Flaga (Red Flag Protocol)

**W przypadku wykrycia jakiegokolwiek fałszerstwa przez społeczność lub algorytmy (użycie AI, skradziona praca, zmanipulowane wideo):**

1. Certyfikat jest natychmiast oznaczony jako **"UNIEWAŻNIONY" (VOID)**.
2. Pakiety dowodów są publicznie oznaczone jako **"Fałszywe"**.
3. Projekt jest umieszczany na czarnej liście [PoArt]. To wzmacnia fakt, że w zdecentralizowanym świecie **reputacja jest jedyną walutą**.

---

## d) Wniosek: Nie Kasyno, Muzeum

**Pump.fun i Zdecentralizowane Giełdy (DEX) są niestety teraz kasynami; światła migają, wszyscy szukają szybkich zysków, a kasyno (oszuści) zawsze wygrywa. Powodem, dla którego uruchomiliśmy projekt tutaj, jest brak wystarczającego budżetu i posiadanie istniejącej publiczności osiągalnej poprzez transmisje na żywo.**

**[PoArt] jest fortecą zbudowaną w środku tego kasyna.**

- 🎰 Kasyno opiera się na grach w karty; my opieramy się na **rzeczywistości fizycznej**.
- 🃏 Kasyno jest otwarte na oszustwa; my jesteśmy otwarci na **przejrzyste dowody**.
- ⏳ Kasyno jest tymczasowe; my koncentrujemy się na **wieczności sztuki i nauki**.

**Token korzystający z tego protokołu nie jest tylko "coinem"; jest cyfrowym papierem wartościowym zawierającym pot, farbę, kod i filozofię.**

---

## 🗳️ 6) ZARZĄDZANIE I REJESTR PUBLICZNY (Governance & Public Registry)

**Celem tej sekcji jest: usunięcie standardu [PoArt] ze sfery "zaufania do osób" i przekształcenie go w zrównoważoną infrastrukturę publiczną z rejestrem + weryfikacją + nadzorem społeczności.**

### 6.1 Rejestr Publiczny (Public Registry)

- **Public Registry:** Wszystkie zatwierdzone dane są rejestrowane pod adresem `ilhanart.org/registry` (lub GitHub Registry).

**Logika rejestracji (zalecany standard - format ścieżki JSON):**

Każdy rekord wchodzący do rejestru zawiera co najmniej te weryfikowalne podstawowe pola:

- **Tożsamość i Status:**
  - `certificate_id` (czytelne odniesienie)
  - `status` (active / void)
  - `void_reason` (jeśli istnieje)
  - `visibility` (private / masked / public)
  - `created_at` (znacznik czasu)

- **Instytucja Wydająca:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informacje o Dziele:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (jeśli to możliwe; dla tożsamości token-gated)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Dane Kryminalistyczne:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Dowody Kryptograficzne:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Zarządzanie:**
  - `governance.decision`
  - `governance.veto_threshold`

Rejestr może mieć dwa poziomy:
- **1)** Indeks czytelny dla człowieka (lista internetowa / wyszukiwanie / filtr)
- **2)** Manifest czytelny dla maszyny (rekordy JSON; do weryfikacji PFE)

**Tutaj "rejestracja" staje się weryfikowalna łańcuchem Evidence Pack → EvidenceRoot → NotarySeal PFE. Rejestr zapewnia cel weryfikacji, a nie "twierdzenie".**

---

### 6.2 Weto Społeczności na 40% (Token-Gated Governance)

- **Weto Społeczności na 40%:** Głosowanie rozpoczyna się miesiąc przed uzyskaniem statusu; sprzeciw 40% społeczności **Token-Gated (Solana-Verified)** unieważnia wniosek.

**Przepływ głosowania (zalecany proces netto):**
- **Okno kandydowania:** Projekt kandydujący otwiera "rejestrację kandydata PoArt" (rejestracje kandydatów pojawiają się ze statusem "pending").
- **Okres przeglądu:** Przez 30 dni społeczność bada dowody (Evidence Pack + nagrania transmisji na żywo + metadane).
- **Weryfikacja token-gated:** Głosowanie odbywa się za pomocą portfeli zweryfikowanych na Solanie (np. posiadanie konkretnego tokena/NFT + podpis portfela).
- **Zasada weta:** Jeśli 40% głosów to **sprzeciw (NO / VETO)**, wniosek zostaje odrzucony.
- **Przejrzystość:** Wynik głosowania jest przechowywany w rejestrze jako "decision record" (data, stosunek, ID snapshot).

---

### 6.3 Synchronizacja Metadanych (Dopasowanie do Świata Fizycznego)

- **Metadata Sync:** Dane techniczne w rejestrze muszą w 100% odpowiadać fizycznemu zasobowi.

**Techniczne zdefiniowanie "dopasowania 100%" (zalecana jasność):**
- **Minimalne dopasowanie (obowiązkowe):**
  - `asset.fingerprints.sha256/sha512` w rejestrze musi być **dokładnie identyczny** z hashem pliku w ręku.
  - `proof.notary_seal` w rejestrze, gdy jest odtwarzany (jeśli Evidence Pack istnieje), musi być **dokładnie identyczny**.
- **Dopasowanie odniesienia fizycznego (typ dowodu):**
  - Dowody takie jak fizyczne dzieło pokazane w transmisji na żywo + odniesienie data/blok muszą być spójne z Evidence Pack.
- **Zgodność z prywatnością:**
  - Pola takie jak IP/lokalizacja w widoczności `masked` są publikowane **zgodnie ze standardem maskowania**.

---

### 6.4 Sprzeciw, Przegląd i Unieważnienie (Dispute & Revocation)

Rejestr nie jest tylko mechanizmem "zatwierdzania"; jest **żywym mechanizmem nadzoru przeciwko fałszerstwom**.

- Gdy sprzeciw jest inicjowany, rekord może zostać umieszczony w trybie **"review"**.
- Jeśli zostanie wykryte fałszerstwo, jest oznaczany jako `status: void` i dodawany jest powód:
  - `void_reason` (użycie AI / plagiat / manipulacja itp.)
  - `revoked_at` (moment unieważnienia)
- Źródło decyzji o unieważnieniu jest wyraźnie widoczne w rejestrze:
  - głosowanie społeczności / autoryzowana rada / notatka z dochodzenia kryminalistycznego (w zależności od tego, co ma zastosowanie)

> **Ta sekcja jest odpowiednikiem w rejestrze koncepcji VOID w sekcji "Red Flag Protocol".**

---

### 6.5 Przykładowy Rekord w Rejestrze (Czytelny dla Maszyny)
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
    "title": "Bez tytułu",
    "creator": "Anonimowy",
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
> *Uwaga: `asset.fingerprints.sha512` i inne wartości hash są skrócone w celach demonstracyjnych; w rzeczywistej aplikacji używany jest ciąg znaków szesnastkowych o pełnej długości.*

---

## 7) 🔐 PIECZĘĆ TECHNICZNA (NOTARY SEAL)

**PoArt Forensic Engine (PFE) v1.0** niezachwiany algorytm pieczętowania produkowany przez:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Protokół [PoArt] Notariusz Cyfrowy i Dowód Kryminalistyczny (Beta v1.0)

> **"Kultura jest większa od Kapitału. Chroń swoje dzieła dzisiaj, przenieś je w jutro."**

---

## Dlaczego Publiczny?

Prawdziwe bezpieczeństwo pochodzi z przejrzystości. Dzięki naszemu systemowi **Public Registry (Rejestr Publiczny)**, osoba w dowolnym miejscu na świecie może w ciągu kilku sekund zweryfikować, czy plik, który ma w ręku, jest oryginalny, bez potrzeby jakiejkolwiek władzy.

---

## 🧩 Dlaczego Istnieje Więcej "Modułów Widoczności"?

Najbardziej krytyczna część kodu jest tutaj (menu wyboru widoczności). Te opcje pozwalają użytkownikom zrównoważyć **"Prywatność vs. Przejrzystość"**:

### 🔒 Prywatny (Private)

- **Scenariusz:** Artysta nie chce jeszcze publikować dzieła, ale chce oznaczyć znacznikiem czasu i udowodnić "zrobiłem to w tej dacie".
- **Co Robi Kod:** Zapisuje dane do bazy danych, ale stosuje tag `visibility: "private"`. W przyszłości, podczas pisania polityki "Public Read", można ukryć te rekordy przed publicznością, mówiąc `WHERE visibility = 'public'`.

### 🕶️ Zamaskowany (Masked)

- **Scenariusz:** Artysta chce przejrzystości, ale obawia się, że zostanie znaleziony adres domu (lokalizacja IP).
- **Co Robi Kod:** Po stronie JavaScript działają funkcje `maskIP` i `maskLoc`. Konwertuje adres IP na format `88.241.***.***` i lokalizację na format `***/TR` i wysyła cenzurowaną wersję do bazy danych.
- **Uwaga Dotycząca Prywatności:** Maskowanie odbywa się w przeglądarce, Supabase nie widzi rzeczywistej lokalizacji. **Jednak:** Jeśli używane są API stron trzecich, takie jak ipapi.co dla danych lokalizacji, ci dostawcy widzą adres IP w momencie żądania.
- **Pieczętowanie w Trybie Masked:** Obliczanie EvidenceRoot i NotarySeal odbywa się z zamaskowanymi danymi forensics; w ten sposób weryfikacja pozostaje deterministyczna.

### 🌍 Publiczny (Public)

- **Scenariusz:** Pełna przejrzystość. Zgodnie ze standardem [PoArt], gdzie, kiedy i z jakiej sieci zostało wyprodukowane dzieło jest jawnie deklarowane.

---

## 💡 Innowacja Technologiczna

PoArt nie jest tylko systemem przesyłania plików. Jest silnikiem **"Forensic Chain of Custody"**, który łączy trzy różne warstwy technologiczne w jeden tygiel i przynosi nowy standard.

**Warstwa opisana w tej sekcji jako "silnik" odpowiada rdzeniowi PoArt Forensic Engine (PFE) w poprzedniej terminologii.**

### 1) Client-Side Hashing (Maksymalna Prywatność)

Pliki Twoich dzieł nigdy nie są przesyłane na serwer. Nasz silnik oparty na przeglądarce (Client-side) oblicza hash (skrót cyfrowy) pliku na Twoim komputerze. Tylko ten odcisk palca i metadane są wysyłane na serwer.

> **Uwaga Dotycząca Prywatności:** Plik dzieła nie jest przesyłany na serwer i jest w ten sposób chroniony. Jednak dane forensics (IP/lokalizacja) są udostępniane zgodnie z wybranym trybem widoczności (private/masked/public).

### 2) Forensic Data Fusion (Moc Kryminalistyczna)

To znacznie więcej niż tylko znacznik czasu (Timestamp). System łączy następujące dane w jedną "Genesis Seal":

- **Skrót Cyfrowy (SHA-512):** Używając standardu skrótu kryptograficznego (SHA-512), odcisk palca cyfrowego, który pęknie, nawet jeśli zmieni się jeden piksel dzieła.
- **Lokalizacja i Czas:** Data z dokładnością do milisekundy, kraj, miasto i dzielnica, w której przeprowadzono transakcję.
- **Tożsamość Urządzenia:** System operacyjny, przeglądarka i typ urządzenia (analiza User-Agent).

---

## 🛡️ Obszary Zastosowania i Korzyści

Jeśli jesteś artystą, pisarzem lub projektantem, nie wystarczy powiedzieć "Zrobiłem to wcześniej", musisz to udowodnić.

**Dzieło opieczętowane PoArt:**

- **Dowód Matematyczny:** System wykrywa to, nawet jeśli zmieni się jeden piksel pliku. Manipulacja jest niemożliwa.
- **Podstawa Prawna:** Jest zarejestrowane, w jakiej dacie, w jakim mieście, z jakiego urządzenia dzieło zostało opieczętowane.
- **Natychmiastowy Certyfikat:** W ciągu kilku sekund generuje spersonalizowany **"Certyfikat Tożsamości Zasobu"** z kodem QR i opieczętowany.

---

## ⚙️ Architektura Systemu i Specyfikacje Techniczne

System jest zaprojektowany na architekturze "Serverless" (Bezserwerowej), skoncentrowanej na wysokiej wydajności i skalowalności.

| Warstwa | Technologia | Opis |
|--------|-----------|----------|
| **Kryptografia** | SHA-256 & SHA-512 | Dwuwarstwowy skrót kryptograficzny |
| **Baza Danych** | Supabase (PostgreSQL) | Struktura danych JSONB, polityki RLS |
| **Dane Kryminalistyczne** | ipapi.co API | Triada IP/Lokalizacja/Czas |
| **Renderowanie** | html2canvas + jsPDF | Generowanie PNG/PDF po stronie klienta |
| **Frontend** | Vanilla JavaScript | Zero zależności frameworkowych |
| **Bezpieczeństwo** | Client-side hashing | Plik nigdy nie trafia na serwer |

### Wyróżniające Cechy

| Cecha | Szczegół | U Konkurentów? |
|---------|-------|-------------|
| **Drag & Drop UI** | Przeciągnij i upuść plik, natychmiastowy podgląd | ❌ Brak w większości |
| **Multi-Format Export** | PNG, JSON, PDF - jednym kliknięciem | ⚠️ Ograniczone |
| **Real-Time Preview** | Podgląd certyfikatu na żywo | ❌ Brak |
| **Privacy Controls** | Opcje Private/Masked/Public | ❌ Brak |
| **Client-Side Hashing** | Plik nigdy nie trafia na serwer | ✅ Tylko w niektórych |
| **Forensic Metadata** | IP, lokalizacja, urządzenie, czas - wszystko razem | ❌ Fragmentaryczne |
| **QR Verification** | Kod QR do natychmiastowej weryfikacji | ⚠️ Ograniczone |
| **Rate Limiting** | Ochrona przed spamem (RLS + Client) | ❌ Brak w większości |

---

## 🗺️ Mapa Drogowa: Przyszłość "Trustless"

Obecna wersja **(Beta v1.0)** jest zoptymalizowana, aby zapewnić użytkownikowi końcowemu maksymalną prędkość, łatwy interfejs i bezpłatny dostęp. Jednak nasza ostateczna wizja to przejście do struktury, w której nawet administrator bazy danych (my) nie może interweniować.

### Faza 1: Beta (Obecnie Dostępna)

- **Infrastruktura:** Cloud Database (Supabase).
- **Cel:** Prędkość, eliminacja barier UX (Doświadczenie Użytkownika) i adaptacja. Zapewnienie bezpieczeństwa "bez tarcia".

### 🚀 Faza 2: (Wymagające Backend / Edge Function)

Ta faza obejmuje przejście od całkowicie "Client-Side" działającej struktury systemu do bardziej bezpiecznej i zarządzalnej struktury "Server-Side Authority".

| Element | Co Wnosi? | Tech Stack | Priorytet |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Function** | Blokada spamu + bezpieczeństwo klucza API | Supabase Edge (Deno) | 🔴 Wysoki |
| **Podpis Portfela** | Uwierzytelnianie tożsamości kryptograficznej | Solana Wallet Adapter | 🟡 Średni |
| **Kopia Zapasowa IPFS/Arweave** | Zdecentralizowana niezmienność | IPFS SDK + Pinata | 🟢 Niski |
| **Mechanizm Odwołania** | Unieważnienie fałszywych certyfikatów | Aktualizacja Schematu DB | 🔴 Wysoki |
| **Audit Log** | Rejestrowanie dochodzenia kryminalistycznego | Niestandardowa tabela logów | 🟡 Średni |
| **OpenTimestamps** | Zakotwiczenie w Bitcoinie | OTS JavaScript | 🟢 Niski |
| **Integracja DID** | Decentralized Identity | ION/Ceramic | 🟢 Niski |

### Faza 3: Pełna Decentralizacja (Długoterminowa)

| Cecha | Cel | ETA |
|---------|-------|-----|
| **Blockchain Registry** | Rejestracja on-chain Ethereum/Solana | Q4 2026 |
| **DAO Governance** | Zarządzanie społecznościowe | Q1 2027 |
| **Multi-Chain Support** | Polygon, Arbitrum, Base | Q2 2027 |
| **Legal Recognition** | Ważność w sądach tureckich | 2027-2028 |
| **API for Developers** | Publiczny endpoint API | Q3 2026 |

---

## 📊 Analiza Konkurencji (Zaktualizowana)

PoArt jest pozycjonowany na "Sweet Spot" (Optymalny punkt idealny), który uzupełnia luki istniejących rozwiązań.

| Cecha | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 証 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Koszt** | 🆓 Bezpłatny | 🆓 | 💰 Płatny | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Bardzo Łatwy | ❌ CLI | ⚠️ Średni | ⚠️ Średni | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Na Żywo | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Tryby | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Prywatność | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Kompletny | ❌ | ❌ | ⚠️ Ograniczony | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Natychmiastowy | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Mapa drogowa | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Wsparcie Polskie** | 🔄 W rozwoju | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Legenda:**
- ✅ : Pełne wsparcie / dostępne
- ⚠️ : Ograniczone / w płatnych planach
- ❌ : Brak / nie obsługiwane
- 🔄 : Na Mapie Drogowej (w rozwoju)
- 🆓 : Całkowicie bezpłatne
- 💰 : Płatne / wymaga subskrypcji

### Braki Konkurentów, Mocne Strony PoArt

| Minus | Konkurenci | PoArt |
|------|----------|-------|
| **Trudność Użycia** | CLI, wiedza o API, wymagany portfel | Przeciągnij i upuść, kończy się w 3 kliknięciach |
| **Bariera Kosztów** | Subskrypcja $50-500/miesiąc | 100% bezpłatny |
| **Prywatność** | Plik przesyłany na serwer | Client-side, plik nigdy nie idzie |
| **Dane Kryminalistyczne** | Tylko znacznik czasu | IP, lokalizacja, urządzenie, czas - wszystko |
| **Wsparcie Polskie** | Brak lub bardzo ograniczone | Natywne wsparcie językowe |
| **Open Source** | Zamknięte pudełko | Cały kod otwarty na GitHubie |

---

## 🧬 Struktura Danych Protokołu (JSON Schema)

**Każdy certyfikat [PoArt] ma przenośny i weryfikowalny dowód tożsamości JSON produkowany w poniższym standardzie.**

> **Uwaga:** Ten format Identity JSON jest formatem certyfikatu prezentowanym użytkownikowi. W rekordach rejestru zamiast `identity.asset_data` używa się `registry.asset` (mapowanie: `identity.asset_data` == `registry.asset`).
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
    "title": "Oficjalny Whitepaper",
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

## 🔬 Głębokość Techniczna: Algorytm Pieczętowania

### Deterministyczne Funkcje Hash
```javascript
// Funkcje Pomocnicze: Konwertuj digest na ciąg hex
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Konwertuj ciąg na tablicę bajtów
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Generowanie kanonicznego ciągu forensics (v1.0: stała kolejność pól + UTF-8 + ogranicznik \n)
// Uwaga Faza 2: Przejście do kanonicznego JSON z RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Proces Produkcji NotarySeal (Całkowicie Deterministyczny)
```javascript
// 1. Obliczanie FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Zbieranie danych kryminalistycznych (użycie pojedynczego znacznika czasu)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Generowanie pojedynczego znacznika czasu
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Ten sam znacznik czasu
  };
  
  return { forensics, timestamp };
}

// 3. Tworzenie EvidenceRoot (z kodowaniem kanonicznym)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Produkcja NotarySeal (użycie tego samego znacznika czasu)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Funkcje pomocnicze maskowania (obsługa IPv4 i IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Kontrola IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 lub nieznany format
  return "***";
}
```

### Przepływ Weryfikacji (Dwa Poziomy)

#### Quick Verify (Szybka Weryfikacja)
```javascript
// Sprawdza tylko hash pliku (szybka czerwona flaga)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Pobierz z Rejestru
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Porównanie hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Oryginał - Hash pliku pasuje"
    };
  } else {
    return {
      valid: false,
      message: "❌ Fałszywy - Plik zmanipulowany"
    };
  }
}
```

#### Full Verify (Pełna Weryfikacja)
```javascript
// Odtwarza i weryfikuje EvidenceRoot i NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Pobierz z Rejestru
  const cert = await fetchFromRegistry(certificateId);

  // 1) Kontrola FileHash (szybka czerwona flaga)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Fałszywy - Hash pliku nie pasuje" };
  }

  // 2) Odtwórz EvidenceRoot (z danymi forensics zapisanymi w rejestrze)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Nie pasuje - EvidenceRoot nieważny" };
  }

  // 3) Odtwórz NotarySeal (z tym samym znacznikiem czasu + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Nie pasuje - NotarySeal nieważny" };
  }

  // Opcjonalnie: W Fazie 2 zweryfikuj również signer_sig z attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Podpis nieważny" };

  return { valid: true, message: "✅ Oryginał - Full Verify przeszedł" };
}
```

> **Ważne Uwagi:**
> - **Quick Verify:** Sprawdza tylko hash pliku dla szybkiego użycia.
> - **Full Verify:** Weryfikuje wszystkie warstwy protokołu (EvidenceRoot + NotarySeal).
> - Wszystkie operacje hash są wykonywane w sposób deterministyczny, ze stałym kodowaniem i ogranicznikami.
> - **Standard kanonizacji v1.0:** Stała kolejność pól + kodowanie UTF-8 + ogranicznik `\n`.
> - **Plan Fazy 2:** Przejście do kanonicznego JSON z RFC 8785 (JCS - JSON Canonicalization Scheme).
> - W trybie Masked obliczanie EvidenceRoot i NotarySeal odbywa się z zamaskowanymi forensics.
> - Pojedynczy znacznik czasu jest używany w całym procesie (forensics + NotarySeal); determinizm jest zagwarantowany.
> - **Nazwy pól Forensics:** `ip_masked`, `location`, `device`, `timestamp` (kod i rejestr całkowicie zgodne).
> - **Ścieżka Rejestru:** `certificate.asset.fingerprints` (całkowicie zgodna z kodem weryfikacji).
> - **signer_sig w Rejestrze:** Pole `proof.signer_sig` jest niezbędne dla Full Verify.
> - Mechanizm SignerSignature zostanie aktywowany w Fazie 2 z Solana Wallet Adapter; w v1.0 można przeprowadzić weryfikację z `attestation_pubkey`.

---

## 📈 Statystyki Użycia (Cele Q1 2026)

| Metryka | Cel | Status |
|--------|-------|-------|
| **Łączne Certyfikaty** | 1,000 | 🔄 W Toku |
| **Aktywni Użytkownicy** | 500 | 🔄 W Toku |
| **Liczba Weryfikacji** | 5,000 | 🔄 W Toku |
| **Uptime** | %99.9 | ✅ Aktywny |
| **Średni Czas Odpowiedzi** | <200ms | ✅ Optymalny |

---

## 🌍 Społeczność i Wsparcie

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 Współtwórcy

Protokół PoArt rozwija się dzięki wkładowi społeczności open source.

**Aby wnieść wkład:**
1. Zrób fork
2. Utwórz gałąź funkcji (`git checkout -b feature/amazing-feature`)
3. Zrób commit (`git commit -m 'Add amazing feature'`)
4. Zrób push (`git push origin feature/amazing-feature`)
5. Otwórz Pull Request

### 🛠️ Czego Teraz Potrzebujemy? (Wezwanie do Pomocy)

Szukamy wkładu doświadczonych programistów w następujących tematach dla rozwojów **Fazy 2** Protokołu PoArt:

* **Supabase Edge Functions:** Przeniesienie ochrony przed spamem po stronie serwera.
* **Solana Web3.js:** Integracja podpisu portfela (Wallet Signing).
* **IPFS / Arweave:** Integracja usług archiwizacji i przypinania.

> Przed dodaniem funkcji proszę rozpocząć dyskusję w sekcji "Issues".

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Kultura jest większa od Kapitału*

## 🧾 Licencja

MIT License © 2026 İlhan Art Gallery Initiative

Zobacz [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) dla pełnych warunków.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Ten projekt został opracowany z inicjatywy [İlhan Art Gallery] i kod źródłowy jest publicznie dostępny dla przejrzystości.**

**PROTOKÓŁ V1.0 // OPIECZĘTOWANY SHA-512.**

*© 2026 İLHAN ART | WSZYSTKIE PRAWA DO DZIEŁ, OBRAZÓW I POMYSŁÓW SĄ ZASTRZEŻONE.*

---
