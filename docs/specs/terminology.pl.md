# 📚 SŁOWNIK TERMINOLOGII I KONCEPCJI
> **"Zrozumienie języka tego protokołu oznacza zrozumienie jego wizji."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Infrastruktura podstawowa

**PoArt Forensic Engine (PFE)** to główna warstwa reprezentująca podstawową logikę i techniczne funkcjonowanie protokołu [PoArt]. To "silnik kryminalistyczny", który pobiera surowe dane produkcyjne dzieła sztuki i przekształca je w weryfikowalny i niezmienny **dowód cyfrowy**.

### 🧩 Dlaczego "PoArt Forensic"?

- **PoArt (Proof of Art):** Fokus silnika polega na powiązaniu wartości zasobu cyfrowego nie ze spekulacją, ale z **udowodnionym procesem produkcji**.
- **Forensic (Weryfikacja kryminalistyczna):**
  - **Definicja techniczna:** Algorytmiczne podejście i łańcuch zapisów do weryfikacji, że dane związane z procesem produkcji (pociągnięcia pędzla, timelapse, logi) nie zostały zmanipulowane.
  - **Warstwa filozoficzna:** Twierdzenie o przekształceniu ludzkiej produkcji zawierającej **czas, wysiłek i koszt decyzji** w mierzalną rzeczywistość, w przeciwieństwie do "natychmiastowego wyniku" sztucznej inteligencji.

> Uwaga: Integracja blockchain (np. Solana) nie jest rdzeniem PFE; jest traktowana jako oddzielna warstwa **Chain Anchor Layer** do zdefiniowania dla weryfikacji/rejestru.

### 🛠️ Zakres techniczny v1.0

**PoArt Forensic Engine (PFE) v1.0** jest zbudowany na tych **3 głównych filarach** zamiast złożonych modeli finansowych:

1. **Hashing & Sealing (Pieczętowanie):**  
   PFE deterministycznie przetwarza wszystkie elementy w Evidence Pack (plik dzieła, wideo, JSON/log, podpis itp.) i generuje unikalną wartość **NotarySeal**.

   **Podstawowe koncepcje (v1.0):**
   - **FileHash (odcisk palca dzieła):** Hash wygenerowany z bajtów pliku dzieła.
   - **EvidenceRoot (korzeń pakietu dowodów):** Korzeń podsumowania reprezentujący integralność Evidence Pack (korzeń Merkle lub kanoniczny hash manifestu).
   - **NotarySeal (pieczęć końcowa / wyjście PFE):** Końcowa pieczęć wygenerowana z kombinacji EvidenceRoot + czas + podpis.

   **Formuły (wyraźnie widoczne dla inwestora):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Definicje kanonicznego ładunku (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Uwaga: Wartość rozumiana jako wyjście PFE to **NotarySeal**. Mechanizm **SignerSignature** zostanie aktywowany w Fazie 2 (z Solana Wallet Adapter); w obecnej v1.0 używany jest własny podpis atestacji systemu. Klucz publiczny atestacji jest publikowany w rejestrze w polu `issuer.attestation_pubkey`.

2. **Indexing (Archiwizacja):**  
   Przetwarza do przejrzystej i możliwej do odpytania warstwy zapisu, który portfel, w jakiej dacie przedstawił **Labor Proof (Dowód pracy)** dla jakiego dzieła.  
   *(Ta warstwa może być bazą danych; integracja łańcucha jest definiowana osobno jako "Chain Anchor Layer".)*

3. **Verification (Weryfikacja):**  
   Gdy autentyczność dzieła jest kwestionowana, PFE ponownie przetwarza surowe dowody; z matematyczną pewnością testuje, czy obliczone wartości **EvidenceRoot / NotarySeal** pasują do zapisu w archiwum.

---

### 🧮 Twierdzenie o wartości PoArt (The Value Theorem)

Protokół [PoArt] wiąże wartość ($V$) zasobu cyfrowego nie z subiektywną percepcją rynku, ale z **fizyczną rzeczywistością procesu produkcji**.

Sztuczna Inteligencja (AI) niszczy proces, dostarczając wynik natychmiast ($t \to 0$). [PoArt] natomiast traktuje wartość jako akumulację komponentów **czasu, pracy i woli**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Definicja zmiennych

- **$\int dt$ (Akumulacja procesu):**  
  Wartość nie jest natychmiastowym "wyjściem" (output); jest **procesem** akumulującym się między $t_{\text{start}}$ a $t_{\text{end}}$. W miarę zmniejszania się czasu trwania (produkcja AI) wynik całki zbliża się do 0.

- **$P_{\text{labor}}(t)$ (Natychmiastowa siła robocza):**  
  Reprezentuje intensywność wysiłku umysłowego i fizycznego wydanego w momencie produkcji. W miarę wzrostu udowodnionego wysiłku, całkowana rośnie.  
  > Uwaga: Ten termin może być w praktyce znormalizowany przez "mierzalne/udowodnione sygnały pracy".

- **$I_{\text{agency}}(t)$ (Współczynnik woli):**  
  To zdolność producenta do podejmowania ryzyka i podejmowania decyzji. Przyjmuje wartość między $0$ a $1$.
  - **AI ($I \approx 0$):** Wykonuje polecenia, nie podejmuje ryzyka, nie płaci ceny.
  - **Człowiek ($I \to 1$):** Zmienia decyzje, waha się, podejmuje ryzyko.

- **$U_{\text{irreversible}}$ (Nieodwracalna osobliwość):**  
  Podczas gdy w produkcji cyfrowej możliwe jest cofnięcie (`Ctrl+Z`); w produkcji fizycznej (farba nałożona na płótno, rzeźbiony marmur, gest na żywo) nie ma powrotu. Ta **nieodwracalność** jest dodatkowym terminem tworzącym "osobliwość" (charakter non-fungible) w dziele.

### 🔎 Analiza przypadku: AI "Natychmiastowe wyjście" vs Człowiek "Udowodniony proces"

Poniższy scenariusz pokazuje, jak **Twierdzenie o wartości PoArt** działa w praktyce i dlaczego produkcje AI otrzymują niskie wyniki w standardzie [PoArt].

#### Scenariusz A: Produkcja wizualna z AI w 10 sekund

- **Czas trwania ($\Delta t$):** $10$ sekund (proces praktycznie nieobecny)
- **Siła robocza ($P_{\text{labor}}$):** $1$ jednostka (tylko pisanie polecenia)
- **Współczynnik woli ($I_{\text{agency}}$):** $0.01$ (brak ryzyka, brak ceny)
- **Nieodwracalność ($U_{\text{irreversible}}$):** $0$ (odwracalne / kopiowalne)

**Wynik:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Komentarz:** Nawet jeśli wyjście jest bezbłędne; ponieważ proces nie został przeżyty i nie zawiera woli/ryzyka, wartość [PoArt] zbliża się do $0$.

#### Scenariusz B: 6-godzinna produkcja fizyczna na żywo

- **Czas trwania ($\Delta t$):** $6$ godzin ($21{,}600$ sekund)
- **Siła robocza ($P_{\text{labor}}$):** $0.5$ jednostki (ciągłość wysiłku fizycznego i umysłowego)
- **Współczynnik woli ($I_{\text{agency}}$):** $0.9$ (zmiany decyzji, podejmowanie ryzyka, nieodwracalne wybory)
- **Nieodwracalność ($U_{\text{irreversible}}$):** $>0$ (fizyczne ślady nieodwracalne)

**Wynik:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Komentarz:** W miarę wydłużania się procesu i wzrostu woli (ryzyka) wartość rośnie kumulatywnie. Termin $U_{\text{irreversible}}$ jest dodatkowym wkładem tworzącym "osobliwość" (charakter non-fungible) w dziele.

---

### ✅ Wniosek: Wartość związana z dowodem (Proof-Bound Value)

To twierdzenie wyprowadza twierdzenie o wartości [PoArt] z bycia "gustem" lub "narracją rynkową" i wiąże je z **udowodnioną rzeczywistością produkcji**.

1. **Bez procesu nie tworzy się wartość:**  
   AI niszczy proces natychmiastowym wyjściem ($t \to 0$). W miarę zawężania się okna procesu wynik całki maleje z matematycznej konieczności:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Wola i ryzyko są mnożnikami:**  
   [PoArt] mierzy nie tylko "spędzony czas", ale także rzeczywistą warstwę decyzji, ryzyka i ceny w tym czasie. Wartość produkcji bez ryzyka (AI) jest niska:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Osobliwość to fizyczny dowód, nie marketing:**  
   Nieodwracalne ślady w produkcji fizycznej (pociągnięcie pędzlem po płótnie, odprysk marmuru) są poza logiką cyfrowego `Ctrl+Z`. Ta nieodwracalność ($U_{\text{irreversible}}$) singularyzuje dzieło ontologicznie.

> **🔐 PODSUMOWANIE:** Chociaż twierdzenie o wartości może wydawać się nieokreślone jako pomiar (nawet jeśli w prawdziwym życiu nie można zmierzyć w 100%), cel tej formuły to pokazanie konstrukcji i kierunku zmiennych. W erze AI rzadkością nie jest "obraz"; to **udowodniona praca, czas i wola**. [PoArt] mierzy ten niedobór i rejestruje go za pomocą **Evidence Pack**.

### 🏛️ Znaczenie koncepcji "Engine" (Silnik)

Tokeny pochodzące z Pump.fun lub podobnych platform są często tylko **"biletami dostępu"**. **PoArt Forensic Engine (PFE)** natomiast jest **konstytucyjną warstwą logiczną** określającą, jakie prawa chroni ten bilet, jak zostanie zarejestrowana praca i jak zostaną utrwalone sztuka/nauka/technologia.

> **Uwaga:** Powodem, dla którego uruchomiliśmy ten projekt na Pump.fun, jest to, że nie mieliśmy wystarczającej płynności i wystarczającej liczby obserwujących. Wykorzystanie istniejących danych było strategicznie właściwym posunięciem, choć nie najwyższej jakości. Niezależnie od budżetu i możliwości, zdefiniowanie logiki tego silnika na GitHubie dowodzi, że projekt to nie tylko spekulacja finansowa, ale długoterminowa **infrastruktura oprogramowania** i wizja **cyfrowej biblioteki narodowej**.

---

## 🎨 PROTOKÓŁ DOWODU PRACY [PoArt] (Proof of Art Protocol v1.0)

> **"Prawdziwy artysta, prawdziwa produkcja, prawdziwa wartość."**

Ten protokół to **biologiczny i intelektualny mechanizm obronny** opracowany przeciwko anonimowym oszustom otaczającym ekosystem krypto, obrazom sztucznej inteligencji produkowanym w 5 minut i kulturze "Pump & Dump" (pompuj i zrzuć).

---

## a) Czym jest [PoArt]? (Definicja filozoficzna i techniczna)

**Proof of Art [PoArt];** to instytucjonalny standard weryfikacji, który gwarantuje, że wartość stojąca za zasobem na blockchainie opiera się nie na spekulacji, ale na weryfikowalnej **ludzkiej pracy**, **czasie** i **energii fizycznej**.

Tak jak Bitcoin tworzy wartość za pomocą *"Elektryczności i mocy procesora"* **(Proof of Work)**; projekty zgodne z [PoArt] tworzą wartość za pomocą *"Talentu artystycznego i czasu ludzkiego"*.

Eliminuje ryzyko *"Deweloper (Dev) sprzedał, projekt skończony"* na platformach Pump.fun i DEX; ponieważ tutaj wartość nie leży w kodzie, ale w **ciągłości produkcji**.

> **[PoArt] nie mówi uczestnikowi "Zaufaj nam"; mówi "Oto dowody, zobacz własnymi oczami, zweryfikuj swoją matematyką".**

---

## b) Standard 5 filarów [PoArt] (The 5 Pillars of Truth)

Tych 5 punktów to niemanipulowalne filtry, przez które musi przejść projekt, aby otrzymać pieczęć [PoArt].

### 1) Dowód tożsamości na żywo (Live Identity Proof)

- **Problem:** Świat krypto jest pełen anonimowych założycieli (Devów) o niejasnej tożsamości, którzy zbierają pieniądze i porzucają projekt.
- **Rozwiązanie [PoArt]:** Producent dowodzi nie tylko dowodu osobistego, ale **swojej obecności podczas produkcji**. Obejmuje to sesje transmisji na żywo, w których następuje interakcja ze społecznością i spełniane są konkretne natychmiastowe żądania, a nie nagrania wideo z wyprzedzeniem.  
  (Np.: *"Napisz dzisiejszą datę i aktualny numer bloku w prawym rogu płótna"*)
- **Motto:** *"Boty mogą tworzyć obrazy, ale boty nie pocą się i nie improwizują."*

### 2) Dowód pracy i procesu (Labor & Process Proof)

- **Problem:** Fakt, że obrazy AI (Sztucznej Inteligencji) produkowane w 2 sekundy i obraz olejny wykonany w 2 miesiące otrzymują to samo traktowanie "jpeg" w świecie cyfrowym.
- **Rozwiązanie [PoArt]:** Proces "ciąży i narodzin" dzieła jest rejestrowany. Dokumentowane są etapy szkicu, warstwy farby, skumulowane godziny spędzone i fizyczny proces, który artysta przeżył podczas tworzenia tego dzieła. To dodaje **"Koszt czasu" (Time Cost)** do tokena. Im trudniejsza produkcja zasobu, tym solidniejsza jego wartość.

### 3) Dowód wartości estetycznej (Aesthetic Value Proof)

- **Problem:** Kultura "memów" ignoruje estetykę i głębię artystyczną, koncentrując się tylko na natychmiastowej komedii, w wyniku czego powstają krótkotrwałe projekty "Hype".
- **Rozwiązanie [PoArt]:** Projekt musi mieć akademickie standardy artystyczne, teorię koloru, zasady kompozycji i wiedzę o materiałach (Impasto, Tekstura itp.). Treść nie powinna tylko śmieszyć; powinna wzbudzać podziw u widza i mieć **wartość kolekcjonerską**.

### 4) Innowacja koncepcyjna (Conceptual Novelty)

- **Problem:** Tysiące monet psów/kotów, które są kopiami siebie nawzajem, dalekie od kreatywności.
- **Rozwiązanie [PoArt]:** Projekt musi zbudować nowy most łączący sztukę, naukę, filozofię lub technologię w znaczącej strukturze.  
  (Np.: Połączenie klasycznej statui Dawida z danymi rynku krypto; opracowanie idei "skamienienia" ludzkiej percepcji i uzasadnienie jej źródłami naukowymi.)  
  Dzieło nie powinno być tylko wizualną ucztą; powinno być również intelektualnym wyzwaniem zmuszającym do refleksji nad **Nauką, Filozofią lub Technologią**.

> [!IMPORTANT]
> **Przykład referencyjny (Efekt Las Palmitas):**  
> W meksykańskiej dzielnicy Las Palmitas walczącej z przestępczością, ponad 200 domów zostało przekształconych w gigantyczną tęczową ucztę. W wyniku tej interwencji estetycznej wskaźniki przestępczości w dzielnicy spadły w pewnym stopniu, młodzi ludzie zaczęli interesować się sztuką zamiast gangami. Zmiana estetyczna przekodowała szacunek ludzi do ich otoczenia i do siebie nawzajem (Spójność społeczna).
>
> **Oczekiwanie:** Projekt, który wejdzie na listę [PoArt]; powinien, podobnie jak w powyższym przykładzie, zawierać socjologiczny, naukowy lub filozoficzny związek przyczynowo-skutkowy wykraczający poza czystą estetykę wizualną. Ponieważ jedynym zasobem, którego nie można kupić za pieniądze, jest "Czas", w tym protokole czas musi być zestakowany i udowodniony jako zabezpieczenie. Podstawa koncepcyjna projektu musi być tak silna i uniwersalna, że; nawet w możliwym scenariuszu CTO (Community Take Over) lata później, społeczność może odziedziczyć to dziedzictwo i autonomicznie kontynuować innowacyjny potencjał projektu.

### 5) Wola niealgorytmiczna (Non-Algorithmic Agency)

- **Problem:** Bezbłędne, ale bezduszne produkcje cyfrowe powtarzające się nawzajem.
- **Rozwiązanie [PoArt]:** Autentyczna wola człowieka zdolnego do popełniania błędów, podejmowania ryzyka i doświadczania wahań emocjonalnych musi być odczuwalna w dziele. Niepewność w pociągnięciach pędzla, nieoczekiwane reakcje materiału i natychmiastowe decyzje artysty to **Podpis biologiczny** odróżniający dzieło od "Produkcji maszynowej".

---

## c) Mechanizm weryfikacji i przeciwdziałania fałszerstwom

Ten system zapewnia, że projekt pozostaje godny zaufania i żywy nie tylko "na początku", ale "na zawsze".

### 📦 Pakiet dowodów (Evidence Pack - The Digital Twin)

Za każdym dziełem certyfikowanym [PoArt] znajduje się zaszyfrowany i oznaczony czasem pakiet danych, który inwestorzy mogą pobrać:

- **Nagrania wideo RAW:** Nieprzerwane surowe obrazy momentu produkcji.
- **Analiza metadanych:** Data utworzenia pliku, informacje o używanym urządzeniu i dane lokalizacji.
- **Odniesienia fizyczne:** Dowody istnienia dzieła w świecie fizycznym  
  (Np.: Aktualna gazeta obok dzieła lub dane blockchain z tego momentu).

> *Uwaga o spójności:* Wyrażenie "pakiet dowodów" łączy się z linią **Evidence Pack → EvidenceRoot → NotarySeal** z poprzednich sekcji; czyli integralność pakietu jest reprezentowana przez weryfikowalną pieczęć.

### 🔄 Odnowienie 365-dniowe (The Sustainability Protocol)

- **Cecha rewolucyjna:** W projektach krypto "Dev" (Deweloper) uruchamia token na rynek i zazwyczaj znika po 1-2 miesiącach (Soft Rug). [PoArt] czyni to niemożliwym.
- **Zasada:** Status "Verified Artist" (Zweryfikowany artysta) nie jest dożywotni. Jest ważny tylko przez **1 rok**.
- **Funkcjonowanie:** Artysta/Deweloper musi co 365 dni przedstawiać społeczności **nowe, duże i udowodnione dzieło**.
- **Przykładowy scenariusz:** Uruchomiłeś projekt w 2026 roku. W styczniu 2027 roku system ostrzega "Okres dowodu wygasł". Jeśli artysta nie przedstawi nowej wystawy, nowego dzieła fizycznego lub nowej integracji technologicznej, "Odznaka zaufania" projektu spada.
- **Wynik:** Ten system zapewnia, że **treść nigdy nie traci aktualności** i inwestor nie doświadcza strachu *"Czy deweloper jest nadal tutaj?"*. Projekt zamienia się w żywe studio.

### 🚩 Czerwona flaga (Red Flag Protocol)

**W przypadku jakiegokolwiek fałszerstwa wykrytego przez społeczność lub algorytmy (użycie AI, skradzione dzieło, zmanipulowane wideo):**

1. Certyfikat jest natychmiast oznaczany jako **"ANULOWANY" (VOID)**.
2. Pakiety dowodów są publicznie oznaczane jako **"Fałszywe"**.
3. Projekt jest dodawany do czarnej listy [PoArt]. To potwierdza fakt, że w zdecentralizowanym świecie **reputacja jest jedyną walutą**.

---

## d) Wniosek: Nie kasyno, ale muzeum

**Pump.fun i zdecentralizowane giełdy (DEX) są niestety obecnie kasynami; światła migają, wszyscy gonią za szybkimi zyskami, a kasa (oszuści) zawsze wygrywa. Powodem uruchomienia projektu tutaj jest brak wystarczającego budżetu i środowiska do dotarcia do istniejącej publiczności za pomocą transmisji na żywo.**

**[PoArt] to twierdza zbudowana pośrodku tego kasyna.**

- 🎰 Kasyno opiera się na grach karcianych; my opieramy się na **rzeczywistości fizycznej**.
- 🃏 Kasyno jest otwarte na oszustwo; my jesteśmy otwarci na **przejrzyste dowody**.
- ⏳ Kasyno jest tymczasowe; my koncentrujemy się na **wieczności sztuki i nauki**.

**Token używający tego protokołu to nie tylko "moneta"; to cyfrowa akcja zawierająca pot, farbę, kod i filozofię.**

---
## 🗳️ 6) ZARZĄDZANIE I REJESTR PUBLICZNY (Governance & Public Registry)

**Celem tej sekcji jest: wyprowadzenie standardu [PoArt] z płaszczyzny "zaufania do osób" i przekształcenie go w zrównoważoną infrastrukturę publiczną poprzez rejestrację + weryfikację + nadzór społeczności.**

### 6.1 Public Registry (Rejestr publiczny)

- **Public Registry:** Wszystkie zatwierdzone dane są rejestrowane pod adresem `ilhanart.org/registry` (lub GitHub Registry).

**Logika rejestracji (zalecany standard - w formacie ścieżki JSON):**

Każdy wpis do rejestru zawiera minimum te weryfikowalne pola rdzeniowe:

- **Tożsamość i status:**
  - `certificate_id` (czytelna referencja)
  - `status` (active / void)
  - `void_reason` (jeśli istnieje)
  - `visibility` (private / masked / public)
  - `created_at` (znacznik czasu)

- **Instytucja wydająca:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Informacje o dziele:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (jeśli możliwe; dla identyfikacji posiadacza tokena)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Dane kryminalistyczne:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Dowody kryptograficzne:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Zarządzanie:**
  - `governance.decision`
  - `governance.review_notes`

Rejestr może mieć dwie warstwy:
- **1)** Indeks czytelny dla człowieka (lista internetowa / wyszukiwanie / filtr)
- **2)** Manifest czytelny dla maszyny (rekordy JSON; do weryfikacji PFE)

**"Rejestracja" tutaj staje się weryfikowalna za pomocą łańcucha Evidence Pack → EvidenceRoot → NotarySeal PFE. Rejestr dostarcza cel weryfikacji, a nie "twierdzenie".**

---

### 6.2 Proces aplikacji PoArt Verified

**Aplikacje PoArt Verified są oceniane przez İlhan Art Gallery zgodnie z 5 standardami PoArt. Uwzględniany jest wkład społeczności, ale ostateczna decyzja należy do zespołu kuratorskiego. Decyzje są wyjaśniane przejrzyście i rejestrowane w ilhanart.org/registry.**

#### Proces aplikacji

**Aplikacja:**
- Artysta/projekt składa wniosek o PoArt Verified
- Przygotowywany jest Evidence Pack (nagrania wideo, metadane, linki do transmisji na żywo)
- Wniosek jest wysyłany do İlhan Art Gallery

**Przegląd (30 dni):**
- Zespół galerii szczegółowo bada Evidence Pack
- Sprawdzane są wszystkie 5 standardów PoArt:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Rozmowa z artystą (opcjonalna)

**Konsultacja społecznościowa:**
- Evidence Pack jest publicznie udostępniany podczas procesu aplikacji
- Posiadacze tokenów (minimum 10,000 $CULTURE) mogą szczególnie składać propozycje
- **Wszystkie opinie są brane pod uwagę podczas procesu przeglądu**
- **Jednak ostateczna decyzja zależy od oceny kuratorskiej**

**Decyzja:**
- Galeria zatwierdza lub odrzuca wniosek
- Powody decyzji są wyjaśniane przejrzyście
- Jeśli zatwierdzono → odznaka PoArt Verified
- Jeśli odrzucono → można ponownie złożyć wniosek po 6 miesiącach

**Przejrzystość:**
- Wszystkie wnioski i decyzje są rejestrowane w ilhanart.org/registry
- Zapis decyzji jest publikowany publicznie:
  - Data wniosku
  - Podsumowanie procesu przeglądu
  - Decyzja (Approved / Rejected)
  - Powody decyzji (krótkie wyjaśnienie)
  - Podsumowanie opinii społeczności (anonimowe)

#### Dlaczego decyzja kuratorska?

**Kontrola jakości:**  
Status PoArt Verified to odznaka o wysokich standardach. Ocena kuratorska gwarantuje utrzymanie tych standardów.

**Zapobieganie manipulacji spekulacyjnej:**  
Pełne zarządzanie on-chain (np.: Realms, głosowanie DAO) technicznie nie jest możliwe z tokenami Pump.fun. Systemy głosowania off-chain są podatne na manipulację wielorybów i skoordynowane ataki. Decyzja kuratorska eliminuje to ryzyko.

**Efektywność operacyjna:**  
Szybki i jasny proces decyzyjny zamiast złożonych mechanizmów głosowania. Artyści otrzymują wynik w ciągu 30 dni.

**Udział społeczności:**  
Opinie społeczności są w pełni brane pod uwagę i wpływają na proces decyzyjny. Jednak ostateczna decyzja należy do zespołu kuratorskiego chronionego przed manipulacją.

**Przyszłość:**  
Gdy projekt dojrzeje (2027+), mechanizm konsultacji społecznościowej może zostać wzmocniony. Jednak kuratorska ochrona standardów pozostaje trwała.

---

### 6.3 Token Utility (Zastosowania tokena)

**Korzyści zapewniane posiadaczom tokenów $CULTURE:**

**1. Pierwszeństwo dostępu do wydarzeń w galerii:**
- Otwarcia wystaw fizycznych İlhan Art Gallery
- Spotkania z artystami i wizyty w warsztatach
- Specjalne oglądanie kolekcji

**2. Pełny dostęp do PoArt Registry:**
- Szczegółowe zapisy wszystkich uwierzytelnionych dzieł sztuki
- Pełne wersje Evidence Packs
- Narzędzia weryfikacji kryminalistycznej

**3. Głosowanie doradcze:**
- Prawo do konsultacji w wnioskach PoArt Verified
- Dostęp do kanałów opinii społeczności
- Udział w dyskusjach o zarządzaniu

**4. Treści ekskluzywne:**
- Treści zza kulis ze studia
- Wywiady z artystami i filmy procesowe
- Dostęp do dokumentacji technicznej

**Uwaga:**  
Posiadacze tokenów oddają głos doradczy (advisory vote). Ostateczna decyzja należy do zespołu kuratorskiego. Ta struktura jest preferowana, aby zapobiec manipulacji wielorybów i atakom spekulacyjnym. Nie ma nagrody za stakowanie, ponieważ szukamy długoterminowych uczestników kulturalnych, a nie krótkoterminowego kapitału najemnego.

---

### 6.4 Metadata Sync (Synchronizacja ze światem fizycznym)

- **Metadata Sync:** Dane techniczne w rejestrze muszą być w 100% zgodne z fizycznym zasobem.

**Techniczne zdefiniowanie "100% zgodności" (zalecana jasność):**

- **Minimalna zgodność (obowiązkowa):**
  - `asset.fingerprints.sha256/sha512` w rejestrze i hash posiadanego pliku muszą być **dokładnie takie same**.
  - `proof.notary_seal` w rejestrze, gdy zostanie odtworzony (jeśli Evidence Pack jest dostępny), musi być **dokładnie taki sam**.

- **Zgodność referencji fizycznej (typ dowodu):**
  - Dowody takie jak fizyczne dzieło pokazane w transmisji na żywo + odniesienie do daty/bloku muszą być zgodne z Evidence Pack.

- **Zgodność z prywatnością:**
  - Pola takie jak IP/lokalizacja o widoczności `masked` są publikowane **zgodnie ze standardem maskowania**.

---

### 6.5 Spór, przegląd i unieważnienie (Dispute & Revocation)

Rejestr to nie tylko mechanizm "zatwierdzania", ale **żywy mechanizm nadzoru** przeciwko fałszerstwom.

- Gdy zostanie wszczęty spór, rejestracja może zostać przeniesiona do trybu **"review"**.
- Jeśli zostanie wykryte fałszerstwo, jest oznaczane jako `status: void` i dodawany jest powód:
  - `void_reason` (użycie AI / skradzione / manipulacja itp.)
  - `revoked_at` (czas unieważnienia)
- Źródło decyzji o unieważnieniu jest wyraźnie widoczne w rejestrze:
  - przegląd kuratorski / spór społeczności / notatka analizy kryminalistycznej (w zależności od tego, co ma zastosowanie)

> **Ta część to odpowiednik rejestru dla koncepcji VOID z sekcji "Red Flag Protocol".**

---

### 6.6 Przykładowy rekord rejestru (Czytelny dla maszyny)
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
    "review_notes": "Spełnia wszystkie 5 standardów PoArt. Pozytywna opinia społeczności."
  }
}
```

> *Uwaga: `asset.fingerprints.sha512` i inne wartości hash są skrócone w celach demonstracyjnych; w rzeczywistej aplikacji używany jest ciąg znaków szesnastkowych pełnej długości.*

---

## 7) 🔐 PIECZĘĆ TECHNICZNA (NOTARY SEAL)

**Algorytm niezachwiany pieczęci produkowany przez PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Protokół notariatu cyfrowego i dowodów kryminalistycznych [PoArt] (Beta v1.0)

> **"Kultura jest większa niż kapitał. Chroń swoje dzieła dzisiaj, przenieś je do jutra."**

---

## Dlaczego publicznie?

Prawdziwe bezpieczeństwo pochodzi z przejrzystości. Dzięki naszemu systemowi **Public Registry (Rejestr publiczny)**, osoba z dowolnego miejsca na świecie może w ciągu sekund zweryfikować, czy posiadany plik jest oryginalny, bez potrzeby jakiegokolwiek autorytetu.

---

## 🧩 Dlaczego jest wiele "modułów widoczności"?

Najbardziej krytyczna część kodu jest tutaj (menu wyboru widoczności). Te opcje pozwalają użytkownikom ustalić równowagę **"Prywatność vs. Przejrzystość"**:

### 🔒 Prywatne (Private)

- **Scenariusz:** Artysta jeszcze nie chce publikować dzieła, ale chce oznaczyć je znacznikiem czasu i udowodnić "zrobiłem to w tej dacie".
- **Co robi kod:** Zapisuje dane do bazy danych, ale oznacza etykietą `visibility: "private"`. Później, pisząc politykę "Public Read", możesz ukryć te zapisy przed publicznością mówiąc `WHERE visibility = 'public'`.

### 🕶️ Maskowane (Masked)

- **Scenariusz:** Artysta chce przejrzystości, ale obawia się znalezienia adresu domowego (lokalizacji IP).
- **Co robi kod:** Po stronie JavaScript działają funkcje `maskIP` i `maskLoc`. Przekształca adres IP w formę `88.241.***.***`, lokalizację w formę `***/TR` i wysyła ocenzurowaną wersję do bazy danych.
- **Uwaga o prywatności:** Maskowanie odbywa się w przeglądarce, Supabase nie widzi prawdziwej lokalizacji. **Jednak:** Jeśli używane są interfejsy API stron trzecich, takie jak ipapi.co dla danych lokalizacji, ci dostawcy widzą adres IP w momencie żądania.
- **Pieczętowanie w trybie maskowanym:** Obliczenia EvidenceRoot i NotarySeal są wykonywane z maskowanymi danymi kryminalistycznymi; w ten sposób weryfikacja pozostaje deterministyczna.

### 🌍 Publiczne (Public)

- **Scenariusz:** Pełna przejrzystość. Zgodnie ze standardem [PoArt], wyraźnie deklarowane jest, gdzie, kiedy i z jakiej sieci zostało wyprodukowane dzieło.

---

## 💡 Innowacja technologiczna

PoArt to nie tylko system przesyłania plików. To silnik **"Łańcucha dowodów kryminalistycznych" (Forensic Chain of Custody)**, który topi trzy różne warstwy technologiczne w jednym tyglu i wprowadza nowy standard.

**Warstwa opisana tutaj jako "silnik" odpowiada rdzeniowi PoArt Forensic Engine (PFE) z poprzedniej terminologii.**

### 1) Client-Side Hashing (Maksymalna prywatność)

Pliki dzieł nigdy nie są przesyłane na serwer. Nasz silnik działający po stronie przeglądarki (Client-side) oblicza hash (cyfrowe podsumowanie) pliku na własnym komputerze. Na serwer są wysyłane tylko ten odcisk palca i metadane.

> **Uwaga o prywatności:** Plik dzieła nie jest przesyłany na serwer i jest w ten sposób chroniony. Jednak dane kryminalistyczne (IP/lokalizacja) są udostępniane zgodnie z wybranym trybem widoczności (private/masked/public).

### 2) Forensic Data Fusion (Siła kryminalistyczna)

To znacznie więcej niż zwykły znacznik czasu (Timestamp). System łączy następujące dane w jedną "Pieczęć Genesis":

- **Cyfrowe podsumowanie (SHA-512):** Cyfrowy odcisk palca, który zostanie uszkodzony, nawet jeśli zmieni się pojedynczy piksel dzieła, przy użyciu standardu skrótu kryptograficznego (SHA-512).
- **Lokalizacja i czas:** Data z dokładnością do milisekundy, kraj, miasto i dane dzielnicowe operacji.
- **Identyfikacja urządzenia:** System operacyjny, przeglądarka i typ urządzenia (analiza User-Agent).

---

## 🛡️ Zastosowania i korzyści

Jeśli jesteś artystą, pisarzem lub projektantem, powiedzenie "Zrobiłem to wcześniej" nie wystarczy, musisz to udowodnić.

**Dzieło opieczętowane PoArt:**

- **Dowód matematyczny:** Jeśli nawet pojedynczy piksel pliku się zmieni, system to wykryje. Manipulacja jest niemożliwa.
- **Podstawa prawna:** Zarejestrowane jest, w jakiej dacie, w jakim mieście, z jakiego urządzenia dzieło zostało opieczętowane.
- **Natychmiastowy certyfikat:** W ciągu sekund generuje specjalny dla Ciebie, z kodem QR i opieczętowany **"Certyfikat tożsamości zasobu"**.

---

## ⚙️ Architektura systemu i cechy techniczne

System jest zaprojektowany na architekturze "Serverless" (Bezserwerowej), z naciskiem na wysoką wydajność i skalowalność.

| Warstwa | Technologia | Opis |
|---------|-----------|---------|
| **Kryptografia** | SHA-256 & SHA-512 | Dwuwarstwowy skrót kryptograficzny |
| **Baza danych** | Supabase (PostgreSQL) | Struktura danych JSONB, polityki RLS |
| **Dane kryminalistyczne** | ipapi.co API | Trójka IP/Lokalizacja/Czas |
| **Renderowanie** | html2canvas + jsPDF | Generowanie PNG/PDF po stronie klienta |
| **Frontend** | Vanilla JavaScript | Zero zależności frameworkowych |
| **Bezpieczeństwo** | Client-side hashing | Plik nigdy nie jest przesyłany na serwer |

### Wyróżniające się cechy

| Cecha | Szczegół | U konkurencji? |
|---------|-------|-------------|
| **Drag & Drop UI** | Przeciągnij i upuść plik, natychmiastowy podgląd | ❌ Brak u większości |
| **Multi-Format Export** | PNG, JSON, PDF - jednym kliknięciem | ⚠️ Ograniczone |
| **Real-Time Preview** | Podgląd certyfikatu na żywo | ❌ Brak |
| **Privacy Controls** | Opcje Private/Masked/Public | ❌ Brak |
| **Client-Side Hashing** | Plik nigdy nie trafia na serwer | ✅ Tylko u kilku |
| **Forensic Metadata** | IP, lokalizacja, urządzenie, czas - wszystko razem | ❌ Częściowe |
| **QR Verification** | Natychmiastowy kod QR do weryfikacji | ⚠️ Ograniczone |
| **Rate Limiting** | Ochrona przed spamem (RLS + Client) | ❌ Brak u większości |

---

## 🗺️ Mapa drogowa: Przyszłość "Trustless"

Obecna wersja **(Beta v1.0)** jest zoptymalizowana pod kątem zapewnienia końcowemu użytkownikowi maksymalnej szybkości, łatwego interfejsu i bezpłatnego dostępu. Jednak naszą ostateczną wizją jest przejście do struktury, w której nawet administrator bazy danych (my) nie może interweniować.

### Faza 1: Beta v1.0 (Obecnie na żywo)

**Infrastruktura:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + kopia zapasowa IPFS)
- Gallery self-attestation (scentralizowana, ale przejrzysta)

**Token:**
- Platforma: Pump.fun
- Płynność: Raydium (automatyczna)
- Zarządzanie: Tylko doradcze (konsultacje społecznościowe)

**Cel:**
- Szybkość, usunięcie barier UX
- Zapewnienie "bezproblemowego" bezpieczeństwa
- Budowanie społeczności

**Token Utility (v1.0):**
- Pierwszeństwo dostępu do wydarzeń w galerii
- Przeglądanie PoArt Registry
- Prawo do głosowania doradczego

---

### 🚀 Faza 2: Zdecentralizowany autorytet (2026 Q2-Q4)

Ta faza obejmuje przejście systemu z całkowicie działającej struktury "Client-Side" do bezpieczniejszej i bardziej zdecentralizowanej struktury.

| Cecha | Co daje? | Tech Stack | ETA |
|---------|---------------|------------|-----|
| **Edge Function INSERT** | Blokada spamu + bezpieczeństwo klucza API | Supabase Edge (Deno) | Q2 2026 |
| **Podpis portfela** | Zdecentralizowana tożsamość | Solana Wallet Adapter | Q2 2026 |
| **Kopia zapasowa IPFS/Arweave** | Zdecentralizowane archiwum | IPFS SDK + Pinata | Q3 2026 |
| **Mechanizm odwołania** | Unieważnienie fałszywego certyfikatu | Aktualizacja schematu bazy danych | Q2 2026 |
| **Dziennik audytu** | Rejestracja zapytań kryminalistycznych | Niestandardowa tabela logów | Q3 2026 |
| **OpenTimestamps** | Zakotwiczenie Bitcoin | OTS JavaScript | Q4 2026 |

**Zarządzanie tokenem (v2.0):**
- Głosowanie off-chain (x/web) + podpis portfela
- Wybór przedstawicieli społeczności (pierwsze 90 dni)
- Kontrola portfela operacji multi-sig
- Ważone głosowanie doradcze (z limitem wielorybów)

**Niezmienność:**
- Kopia zapasowa rejestru z hashami IPFS
- Zakotwiczenie znacznika czasu Bitcoin
- Przygotowanie do weryfikacji cross-chain

---

### Faza 3: Pełna decentralizacja (2027+)

| Cecha | Cel | ETA |
|---------|-------|-----|
| **On-Chain Registry** | Rejestracja on-chain Solana | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **Integracja DID** | Zdecentralizowana tożsamość | Q3 2027 |
| **Community Governance** | Wzmocniony system doradczy | Q4 2027 |
| **Uznanie prawne** | Ważność w sądach tureckich | 2027-2028 |
| **API dla deweloperów** | Publiczny endpoint API | Q3 2027 |

**Ewolucja zarządzania:**
- v3.0: Model hybrydowy (kuratorski + ważony społecznościowy)
- 2028+: Pełne zarządzanie społecznościowe (opcjonalne)
- Kuratorska kontrola jakości zawsze zachowana

---

## 🧬 Struktura danych protokołu (JSON Schema)

**Każdy certyfikat [PoArt] ma przenośną i weryfikowalną kartę tożsamości JSON wygenerowaną w poniższym standardzie.**

> **Uwaga:** Ten format Identity JSON to format certyfikatu przedstawiany użytkownikowi. W zapisach rejestru używane jest `registry.asset` zamiast `identity.asset_data` (mapowanie: `identity.asset_data` == `registry.asset`).
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

## 🔬 Głębia techniczna: Algorytm pieczęci

### Deterministyczne funkcje hash
```javascript
// Funkcje pomocnicze: Konwertuj digest na hex string
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Konwertuj string na byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Generowanie kanonicznego stringu forensics (v1.0: stała kolejność pól + UTF-8 + delimiter \n)
// Uwaga Fazy 2: przejście na kanoniczny JSON z RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Proces produkcji NotarySeal (Całkowicie deterministyczny)
```javascript
// 1. Obliczanie FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Zbieranie danych forensic (użycie pojedynczego timestamp)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Generowanie pojedynczego timestamp
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Ten sam timestamp
  };
  
  return { forensics, timestamp };
}

// 3. Tworzenie EvidenceRoot (z kanonicznym kodowaniem)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Produkcja NotarySeal (użycie tego samego timestamp)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Funkcje pomocnicze maskowania (obsługa IPv4 i IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Sprawdzenie IPv4
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

### Przepływ weryfikacji (Dwa poziomy)

#### Quick Verify (Szybka weryfikacja)
```javascript
// Sprawdza tylko hash pliku (szybka czerwona flaga)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Pobierz z rejestru
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Porównanie hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Oryginalny - Hash pliku się zgadza"
    };
  } else {
    return {
      valid: false,
      message: "❌ Fałszywy - Plik został zmanipulowany"
    };
  }
}
```

#### Full Verify (Pełna weryfikacja)
```javascript
// Odtwarza i weryfikuje EvidenceRoot i NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Pobierz z rejestru
  const cert = await fetchFromRegistry(certificateId);

  // 1) Kontrola FileHash (szybka czerwona flaga)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Fałszywy - Hash pliku nie zgadza się" };
  }

  // 2) Odtwórz EvidenceRoot (z forensics zapisanych w rejestrze)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Niezgodne - EvidenceRoot nie pasuje" };
  }

  // 3) Odtwórz NotarySeal (z tym samym timestamp + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Niezgodne - NotarySeal nie pasuje" };
  }

  // Opcjonalnie: W Fazie 2 zweryfikuj signer_sig również z attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Podpis nieważny" };

  return { valid: true, message: "✅ Oryginalny - Full Verify zaliczone" };
}
```

> **Ważne uwagi:**
> - **Quick Verify:** Sprawdza tylko hash pliku dla szybkiego użycia.
> - **Full Verify:** Weryfikuje wszystkie warstwy protokołu (EvidenceRoot + NotarySeal).
> - Wszystkie operacje hash są wykonywane deterministycznie, ze stałym kodowaniem i delimiterami.
> - **Standard kanonizacji v1.0:** Stała kolejność pól + kodowanie UTF-8 + delimiter `\n`.
> - **Plan Fazy 2:** Przejście na kanoniczny JSON z RFC 8785 (JCS - JSON Canonicalization Scheme).
> - W trybie maskowanym, obliczenia EvidenceRoot i NotarySeal są wykonywane z maskowanymi forensics.
> - Pojedynczy timestamp jest używany w całym procesie (forensics + NotarySeal); deterministyczność jest gwarantowana.
> - **Nazwy pól forensics:** `ip_masked`, `location`, `device`, `timestamp` (kod i rejestr w pełnej zgodności).
> - **Ścieżka rejestru:** `certificate.asset.fingerprints` (w pełnej zgodności z kodem weryfikacji).
> - **signer_sig w rejestrze:** Pole `proof.signer_sig` jest wymagane dla Full Verify.
> - Mechanizm SignerSignature zostanie aktywowany w Fazie 2 z Solana Wallet Adapter; w v1.0 można dokonać weryfikacji z `attestation_pubkey`.

---

## 📊 Analiza konkurencji (Zaktualizowana)

PoArt jest umieszczony na "Sweet Spot" (Idealny punkt), który uzupełnia braki istniejących rozwiązań.

| Cecha | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Koszt** | 🆓 Darmowy | 🆓 | 💰 Płatny | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Bardzo łatwy | ❌ CLI | ⚠️ Średni | ⚠️ Średni | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Na żywo | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 tryby | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Prywatność | ✅ | ❌ Upload | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Pełne | ❌ | ❌ | ⚠️ Ograniczone | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Natychmiastowe | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Roadmap | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Wsparcie polskie** | ✅ Natywne | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Wyjaśnienie:**
- ✅ : Pełne wsparcie / dostępne
- ⚠️ : Ograniczone / w płatnych planach
- ❌ : Brak / niewspierane
- 🔄 : W roadmap (w rozwoju)
- 🆓 : Całkowicie darmowe
- 💰 : Płatne / wymaga subskrypcji

### Braki konkurencji, Mocne strony PoArt

| Minus | Konkurencja | PoArt |
|------|----------|-------|
| **Trudność użytkowania** | CLI, wiedza o API, wymagany portfel | Przeciągnij i upuść, kończy się 3 kliknięciami |
| **Bariera kosztowa** | Abonament $50-500/miesiąc | 100% darmowe |
| **Prywatność** | Plik jest przesyłany na serwer | Client-side, plik nigdy nie trafia |
| **Dane kryminalistyczne** | Tylko timestamp | IP, lokalizacja, urządzenie, czas - wszystko |
| **Wsparcie polskie** | Brak lub bardzo ograniczone | Natywne wsparcie języka |
| **Open Source** | Zamknięte pudełko | Cały kod otwarty na GitHubie |

---

## 📈 Statystyki użytkowania (Cele Q1 2026)

| Metryka | Cel | Status |
|--------|-------|-------|
| **Łączne certyfikaty** | 1,000 | 🔄 W toku |
| **Aktywni użytkownicy** | 500 | 🔄 W toku |
| **Liczba weryfikacji** | 5,000 | 🔄 W toku |
| **Uptime** | 99.9% | ✅ Aktywny |
| **Śr. czas odpowiedzi** | <200ms | ✅ Optymalny |

---

## 🌍 Społeczność i wsparcie

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Współtwórcy

Protokół PoArt nadal się rozwija dzięki wkładowi społeczności open source.

**Aby wnieść wkład:**
1. Zrób Fork
2. Utwórz branch funkcji (`git checkout -b feature/amazing-feature`)
3. Commit (`git commit -m 'Add amazing feature'`)
4. Push (`git push origin feature/amazing-feature`)
5. Otwórz Pull Request

### 🛠️ Czego teraz potrzebujemy? (Wezwanie do pomocy)

Oczekujemy wkładu doświadczonych deweloperów w następujących obszarach dla rozwoju **Fazy 2** Protokołu PoArt:

* **Supabase Edge Functions:** Przeniesienie ochrony przed spamem po stronie serwera.
* **Solana Web3.js:** Integracja podpisywania portfela (Wallet Signing).
* **IPFS / Arweave:** Integracja usług archiwizacji i pinowania.
* **Community Tools:** systemy głosowania, dashboard analityczny.

> Przed dodaniem funkcji prosimy o rozpoczęcie dyskusji w zakładce "Issues".

---

## 💬 Uwagi końcowe

### Pump.fun i rzeczywistość

Ten projekt został uruchomiony na Pump.fun, ponieważ:
- ✅ Dostęp do płynności (automatyczna migracja Raydium)
- ✅ Dostęp do istniejącej społeczności
- ✅ Niski koszt początkowy

Jednak wyjaśnijmy to:
- **Cena tokena** nie jest wskaźnikiem sukcesu artystycznego
- **Budżet operacyjny** wymaga wartości tokena (galeria, wystawy, infrastruktura)
- **Metryki sukcesu:** Uwierzytelnione dzieła sztuki + zaangażowanie społeczności + fizyczni odwiedzający

### Zarządzanie i decentralizacja

**Rzeczywistość v1.0 (2026):**
- Rejestr: Off-chain (PostgreSQL + kopia zapasowa IPFS)
- Atestacja: Podpisane przez galerię (scentralizowane, ale przejrzyste)
- Zarządzanie: Tylko doradcze (kuratorska ostateczna decyzja)

**Wizja v2.0+ (2027+):**
- Rejestr: On-chain (Solana)
- Podpisy: Oparte na portfelu (zdecentralizowane)
- Zarządzanie: Hybrydowe (doradztwo społecznościowe + jakość kuratorska)
- Użyteczność tokena: Rozszerzone funkcje + zaawansowany dostęp

Ta struktura zapewnia **efektywność operacyjną** i **kontrolę jakości** na wczesnym etapie, jednocześnie pozostawiając otwartą drogę do zwiększenia **udziału społeczności** w przyszłości.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Kultura jest większa niż kapitał*

## 🧾 Licencja

Licencja MIT © 2026 İlhan Art Gallery Initiative

Zobacz [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) dla pełnych warunków.

---

## 💬 Podziękowania

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Ten projekt został opracowany z inicjatywy [İlhan Art Gallery], a kod źródłowy jest publicznie dostępny w celu zapewnienia przejrzystości.**

**PROTOKÓŁ V1.0 // OPIECZĘTOWANY SHA-512.**

*© 2026 İLHAN ART | WSZYSTKIE PRAWA DO DZIEŁ, OBRAZÓW I IDEI ZASTRZEŻONE.*

---
