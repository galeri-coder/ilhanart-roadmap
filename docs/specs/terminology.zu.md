# 📚 ISICHAZAMAZWI SEMIBANDELA NEQOQA LEMIBONO
> **"Ukuqonda ulimi lwale protokholi, ukuqonda umbono wayo."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Ingqalasizinda Eyisisekelo

**I-PoArt Forensic Engine (PFE)**, iyingxenye eyinhloko emele umqondo oyisisekelo kanye nokusebenza kobuchwepheshe ngemuva kweprothikholi ye-[PoArt]. Lena yi-"njini yophenyo lwezomthetho" eguqula idatha yokukhiqizwa kwemisebenzi yobuciko ibe **ubufakazi bedijithali** obungaqinisekiswa futhi obungashintsheki.

### 🧩 Kungani "PoArt Forensic"?

- **PoArt (Proof of Art / Ubufakazi Bobuciko):** Ukugxila kwenjini ukuxhumanisa inani lempahla yedijithali hhayi nokuqagela; kodwa **ngenqubo yokukhiqiza engaqinisekiswa**.
- **Forensic (Ukuqinisekiswa Kwezomthetho):**
  - **Incazelo Yobuchwepheshe:** Indlela ye-algorithm nochungechunge lwerekhodi eliqinisekisa ukuthi idatha eqondene nenqubo yokukhiqiza (ukushaya kwebrashi, i-timelapse, ama-log) ayigudlulwanga.
  - **Izinga Lefilosofi:** Ngokuphikisana nokukhiqiza "okukhishwa ngokushesha" kwe-AI; ukuthi **umuntu udinga isikhathi, umzamo nenani lesinqumo** liguqulelwa eqinisweni elinganakwa.

> Qaphela: Ukuhlanganiswa kwe-blockchain (isib. i-Solana) akuyona ingxenye eyinhloko ye-PFE; kuphathwa njenge-**Chain Anchor Layer** ehlukile yokuqinisekisa/irekhodi.

### 🛠️ Ububanzi Bobuchwepheshe be-v1.0

**I-PoArt Forensic Engine (PFE) v1.0**, yakhiwe phezu **kwezinsika ezintathu eziyinhloko** esikhundleni samamodeli ezezimali ayinkimbinkimbi:

1. **Ukufaka Uphawu & Ukuvala (Hashing & Sealing):**  
   I-PFE icubungula zonke izinto eziku-Evidence Pack (ifayela lobuciko, ividiyo, i-JSON/log, isiginesha njll.) ngendlela enomthetho futhi ikhiqiza inani elilodwa le-**NotarySeal**.

   **Imibono eyisisekelo (v1.0):**
   - **FileHash (uphawu lweminwe lobuciko):** I-hash ekhiqizwa kusuka ku-bytes yefayela lobuciko.
   - **EvidenceRoot (impande yephakethe lobufakazi):** Isifinyezo sempande esimele ukuphelela kwe-Evidence Pack (i-Merkle root noma i-canonical manifest hash).
   - **NotarySeal (uphawu lokugcina / Okukhishwa yi-PFE):** Uphawu lokugcina olukhiqizwa ngokuhlanganisa i-EvidenceRoot + isikhathi + isiginesha.

   **Amafomula (abonakala ngokucacile kumtshalizimali):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Izincazelo ze-Canonical Payload (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Qaphela: Inani elichazwa njengokukhishwa yi-PFE yi-**NotarySeal**. Indlela ye-**SignerSignature** izoqala ukusebenza ku-Faz 2 (nge-Solana Wallet Adapter); ku-v1.0 yamanje kusetshenziswa isiginesha ye-attestation yesistimu. Ukhiye we-attestation ushicilelwa kurejista esigabeni se-`issuer.attestation_pubkey`.

2. **Ukufaka Kwirekhodi (Indexing):**  
   Irekhoda ukuthi yiliphi isikhwama, ngaluphi usuku, sinikeze **ubufakazi Bomsebenzi (Labor Proof)** obuphi ubuciko; esendaweni yerekhodi esobala nengabhekwa.  
   *(Lesi sigaba singaba yidatabase; ukuhlanganiswa nochungechunge kuphathwa ngokuhlukile njenge-"Chain Anchor Layer".)*

3. **Ukuqinisekisa (Verification):**  
   Uma kubuzwa ngobuqiniso bobuciko, i-PFE icubungula kabusha ubufakazi obungashintshiwe; ihlola ngokuqiniseka kwezibalo ukuthi amanani e-**EvidenceRoot / NotarySeal** abalwa ayahambisana yini nerekhodi ekukhwamasini.

---

### 🧮 I-Theorem Yenani ye-PoArt (The Value Theorem)

Iprothikholi ye-[PoArt] ixhumanisa inani lempahla yedijithali ($V$) hhayi ngokuqonda kwemakethe okungagcinile; kodwa **ngeqiniso elingokoqobo lenqubo yokukhiqiza**.

I-Artificial Intelligence (AI), ngokunikeza umphumela ngokushesha ($t \to 0$) ichitha inqubo. I-[PoArt] iphatha inani njenge; inqwaba **yesikhathi, umsebenzi nentando**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Izincazelo Zokuguquguquka

- **$\int dt$ (Inqwaba Yenqubo):**  
  Inani akuyona "okukhishwa" (output) okushesha; yi**nqubo** eqoqana phakathi kuka-$t_{\text{start}}$ no-$t_{\text{end}}$. Njengoba isikhathi sinciphisa (ukukhiqiza kwe-AI), umphumela we-integral usondela ku-0.

- **$P_{\text{labor}}(t)$ (Amandla Omsebenzi Wesikhathi):**  
  Imele ukujula komzamo wengqondo nowomzimba ochithwe ngesikhathi sokukhiqiza. Njengoba umzamo oqinisekiswa ukhula, i-integrand iyakhula.  
  > Qaphela: Le nkulumo, ekusebenzeni "izimpawu zomsebenzi ezingakalwa/eziqinisekiswa" ingahlelwa.

- **$I_{\text{agency}}(t)$ (Isikali Sentando):**  
  Ikhono lomkhiqizi lokuthatha ubungozi nokwenza izinqumo. Ithatha inani phakathi kuka-$0$ no-$1$.
  - **AI ($I \approx 0$):** Yenza imiyalo, ayithathi ubungozi, ayikhokhi inani.
  - **Umuntu ($I \to 1$):** Ushintsha isinqumo, uyangabaza, uthatha ubungozi.

- **$U_{\text{irreversible}}$ (Ukuhlukana Okungebuyiselwe Emuva):**  
  Ekukhiqizeni kwedijithali ukuhlehlisa (`Ctrl+Z`) kungenzeka; kodwa ekukhiqizeni ngokoqobo (upende oshaywe ekhwanvasini, itshe eliqoshiwe, isenzo sokusakaza bukhoma) akukho ukubuyela emuva. Lo **kungabuyiseki**, iyitemu eyengeziwe edala "ukuhlukana" (isimilo se-non-fungible) emsebenzini wobuciko.

### 🔎 Ukuhlaziywa Kwesimo: I-AI "Okukhishwa Ngokushesha" vs. Umuntu "Inqubo Ebufakaziwe"

Lesi simo silandelayo, sikhombisa ukuthi **i-Theorem Yenani ye-PoArt** isebenza kanjani ekusebenzeni kanye nokuthi kungani ukukhiqiza kwe-AI kuthola amaphuzu aphansi esilinganisweni se-[PoArt].

#### Isimo A: Ukukhiqiza Isithombe nge-AI ngamasekhondi ayi-10

- **Isikhathi ($\Delta t$):** Amasekhondi ayi-$10$ (inqubo cishe ayikho)
- **Amandla Omsebenzi ($P_{\text{labor}}$):** Iyunithi eli-$1$ (ukubhala umyalo kuphela)
- **Isikali Sentando ($I_{\text{agency}}$):** $0.01$ (akukho ubungozi, akukho inani)
- **Ukungabuyiseki ($U_{\text{irreversible}}$):** $0$ (kungahlehliswa / kungakopishwa)

**Umphumela:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Ukuphawula:** Noma okukhishwa kuphelele; ngenxa yokuthi inqubo ayenzekanga futhi ayiqukethe ntando/ubungozi, inani le-[PoArt] lisondela ku-$0$.

#### Isimo B: Ukukhiqiza Ngokoqobo Amahora ayi-6 Ekusakazeni Bukhoma

- **Isikhathi ($\Delta t$):** Amahora ayi-$6$ (amasekhondi ayi-$21{,}600$)
- **Amandla Omsebenzi ($P_{\text{labor}}$):** Amayunithi angu-$0.5$ (ukuqhubeka komzamo womzimba nowengqondo)
- **Isikali Sentando ($I_{\text{agency}}$):** $0.9$ (ukushintsha isinqumo, ukuthatha ubungozi, ukukhetha okungebuyiselwe emuva)
- **Ukungabuyiseki ($U_{\text{irreversible}}$):** $>0$ (izimpawu zokoqobo azihlehliselwa emuva)

**Umphumela:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Ukuphawula:** Njengoba inqubo iba yinde futhi intando (ubungozi) yanda, inani landa ngokuhlanganisa. Itemu ye-$U_{\text{irreversible}}$ iwumnikelo owengeziwe odala "ukuhlukana" (isimilo se-non-fungible) emsebenzini wobuciko.

---

### ✅ Isiphetho: Ukukhiya Inani Nobufakazi (Proof-Bound Value)

Le theorem, isusa isimangalo senani se-[PoArt] ekubeni "ukuthandwa" noma "indaba yemakethe" futhi isixhumanisa **neqiniso lokukhiqiza elingaqinisekiswa**.

1. **Akukho Nani Ngaphandle Kwenqubo:**  
   I-AI, ichitha inqubo ekukhishweni okushesha ($t \to 0$). Njengoba iwindi lenqubo linciphisa umphumela we-integral unciphisa ngesidingo sezibalo:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Intando Nobungozi Kuyisiphindaphindi:**  
   I-[PoArt] ayikali "isikhathi esichithiwe" kuphela; ikala nezinga lesinqumo sangempela, ubungozi nenani kuleso sikhathi. Inani lokukhiqiza okungathathi ubungozi (AI) liphansi:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Ukuhlukana, Akukhona Ukumaketha Kodwa Ubufakazi Bokoqobo:**  
   Ekukhiqizeni ngokoqobo izimpawu ezingehlehliselwa emuva (ukushaywa kwekhwanvasi, ukuphuka kwetshe), kungaphandle komqondo we-`Ctrl+Z` wedijithali. Lokhu kungabuyiseki ($U_{\text{irreversible}}$), kwenza umsebenzi wobuciko ube ohlukile ngokuphila.

> **🔐 ISIFINYEZO:** Noma i-theorem yenani ibonakala ingaqiniseki njengesilinganiso (noma eqinisweni impilo ayilinganiswa ngokugcwele nge-100%) inhloso yale fomula ukukhombisa ukwakheka nokubheka kokuguquguquka. Into eyivela kuphela esikhathini se-AI akuyona "isithombe"; **umsebenzi, isikhathi nentando engaqinisekiswa**. I-[PoArt] ikala lokhu kusweleka futhi ikubhalisa nge-**Evidence Pack**.

### 🏛️ Ukubaluleka Komqondo we-"Engine" (Injini)

Amathokheni aphuma ku-Pump.fun noma kumapulatifomu afanayo, ngokuvamile ayizinto ze-**"ithikithi lokungena"** kuphela. **I-PoArt Forensic Engine (PFE)** yi**ngxenye yomqondo womthetho oyisisekelo** enquma ukuthi yimaphi amalungelo lelo thikithi eliwavikelayo, ukuthi umsebenzi ubhalwa kanjani futhi ubuciko/isayensi/ubuchwepheshe bugcinwa kanjani njani.

> **Qaphela:** Isizathu sokuthi siqale lo msebenzi ku-Pump.fun ukuthi besingenalo ukwanela komfutho kanye nenani labalandeli. Noma ukusebenzisa idatha ekhona bekungeyona isu elimhlophe kakhulu, singathi bekuyisinyathelo esifanele. Ngaphandle kwesabelomali namathuba, ukuchaza umqondo wale njini ku-GitHub kuqinisekisa ukuthi lo msebenzi akuyona imikhuba yezezimali kuphela, kodwa yisakhiwo **sesoftware sesikhathi eside** nombono we-**mtatshana kazwelonke wedijithali**.

---

## 🎨 IPROTHIKHOLI YOBUFAKAZI BOMSEBENZI [PoArt] (Proof of Art Protocol v1.0)

> **"Umculi Wangempela, Ukukhiqiza Kwangempela, Inani Langempela."**

Le prothikholi; **indlela yokuzivikela ngokomzimba nangokomqondo** eyenziwe ukulwa nabakhohlisi abangaziwa abazungeze isimo se-crypto, izithombe ze-AI ezikhiqizwa ngemizuzu emi-5 nesiko le-"Pump & Dump".

---

## a) Yini i-[PoArt]? (Incazelo Yefilosofi Nobuchwepheshe)

**I-Proof of Art [PoArt];** iyisilinganiso sokuqinisekisa esihlangene esiqinisekisa ukuthi inani elingemuva kwempahla ku-blockchain, lisekelwe **emsebenzini womuntu oqinisekiswayo**, **esikhathini** nasendla **emandleni omzimba**, hhayi ekuqageleni.

Njengoba i-Bitcoin ikhiqiza inani nge-*"Ugesi Namandla Wesishintshi"* **(Proof of Work)**; imisebenzi ehambisana ne-[PoArt] nayo ikhiqiza inani nge-*"Ikhono Nesikhathi Somuntu Esichithwe"*. I-"Stake" isikhathi.

Isusa ubungozi be-*"Umcubunguli (Dev) uthengisile, umsebenzi uphelile"* kumapulatifomu e-Pump.fun ne-DEX; ngoba lapha inani alikho ekucodeni, likufihlwe **ekuqhubekeni kokukhiqiza**.

> **I-[PoArt] ayitsheli umbambi qhaza wayo ukuthi "Sithembe"; ithi "Nansi ubufakazi, bona ngamehlo akho, qinisekisa ngezibalo zakho".**

---

## b) Isilinganiso Se-[PoArt] Esihlanu (The 5 Pillars of Truth)

Lezi zinto ezi-5 ziyizihluzo ezingagudluleki umsebenzi okumele uwadlule ukuze uthole uphawu lwe-[PoArt].

### 1) Ubufakazi Bobunikazi Obuphilayo (Live Identity Proof)

- **Inkinga:** Umhlaba we-crypto ugcwele abasunguli abangaziwa (Devs) abaqoqa imali bese beshiya umsebenzi.
- **Isixazululo se-[PoArt]:** Umkhiqizi uqinisekisa hhayi ikhadi lomazisi kuphela, kodwa **ukuba khona kwakhe ngesikhathi sokukhiqiza**. Lokhu kufaka phakathi izingxoxo zokusakaza bukhoma lapho kuxoxiswana nomphakathi futhi kugcwaliswa izicelo eziqondile zangaleso sikhathi, hhayi amavidiyo athathwe ngaphambili.  
  (Isib: *"Bhala usuku lwanamuhla nenombolo yebulokhi yamanje ekhoneni langakwesokudla lekhwanvasi"*)
- **Isiqubulo:** *"Amarobothi angenza izithombe kodwa amarobothi awajuluki futhi awakwazi ukwenza izinto ngokushesha."*

### 2) Ubufakazi Bomsebenzi & Inqubo (Labor & Process Proof)

- **Inkinga:** Izithombe ze-AI ezikhiqizwa ngomzuzwana owe-2 nephenti lamafutha elenziwe ngenyanga ezi-2 ziphathwa ngokufanayo njengo-"jpeg" emhlabeni wedijithali.
- **Isixazululo se-[PoArt]:** Inqubo "yokukhulelwa nokuzalwa" yomsebenzi wobuciko ibhaliswa. Izigaba zomdwebo, izendlalelo zopende, amahora ahlanganiswe achithiwe nenqubo yomzimba umculi ayidlulile ngesikhathi edala lowo msebenzi wobuciko kubhaliwe. Lokhu kwengeza **"Izindleko Zesikhathi" (Time Cost)** ethokheni. Ngezinga ukukhiqiza kwempahla kunzima, inani layo liqine kangako.

### 3) Ubufakazi Benani Lobuhle (Aesthetic Value Proof)

- **Inkinga:** Isiko le-"Meme" elihlonipha ubuhle nobude bobuciko futhi ligxila ekuhlekiseni okushesha kuphela kanye nemisebenzi ye-"Hype" ephila isikhashana ngenxa yalokhu.
- **Isixazululo se-[PoArt]:** Umsebenzi kumele ube nezilinganiso zobuciko zezemfundo, ithiyori yombala, imithetho yokuhlelwa nolwazi lwezinto (i-Impasto, i-Texture njll.). Okuqukethwe akufanele kuhlekise kuphela; kumele kuvuse ukukhangwa kubabukeli futhi kube **nenani lokuqoqwa**.

### 4) Ukusungula Komqondo (Conceptual Novelty)

- **Inkinga:** Izinkulungwane zama-coin ezinja/izikati ezikopishana, ezikude nobuciko.
- **Isixazululo se-[PoArt]:** Umsebenzi kumele wakhe ibhuloho elisha elihlanganisa ubuciko, isayensi, ifilosofi noma ubuchwepheshe ngendlela enomqondo.  
  (Isib: Ukuhlanganisa isithombe sakudala sikaDavide nedatha yemakethe ye-crypto; ukusebenza phezu kombono wokuthi ukuqonda komuntu "kuphenduke itshe" futhi ukwazi ukusekela lokhu ngezinsiza zesayensi.)  
  Umsebenzi wobuciko, akuyona imibukiso nje kuphela; kumele futhi ube yinselelo yomqondo ecabangisa nge-**Sayensi, Ifilosofi noma Ubuchwepheshe**.

> [!IMPORTANT]
> **Isibonelo Sokubhekisa (Umthelela we-Las Palmitas):**  
> Endaweni ye-Las Palmitas eMexico ebihlushwa ubugebengu, izindlu ezingaphezu kuka-200 zaguqulwa zaba yimibukiso enkulu yothingo. Ngenxa yalokhu kuguqulwa kobuhle, amazinga obugebengu endaweni ehla ngezinga elithile, intsha yaqala ukuthanda ubuciko kuneziqumbi zobugebengu. Ushintsho lobuhle, lwabhala kabusha inhlonipho yabantu endaweni yabo nakomunye nomunye (Social Cohesion).
>
> **Ukulindela:** Umsebenzi ozongena ohlwini lwe-[PoArt]; njengesikhombelo esingenhla, kumele uqukathe ubudlelwano besizathu-nomphumela wezomphakathi, wesayensi noma wefilosofi ngaphezu kobuhle bokubukwa kuphela. Njengoba "Isikhathi" siyimpahla yodwa engathengeki ngemali, kuleli prothikholi isikhathi kumele si-stake njengesivikeleko futhi siqinisekiswe. Isisekelo somqondo somsebenzi kumele siqine futhi sivelele ngezinga lokuthi; noma ngomzuzu we-CTO (Community Take Over) eminyakeni ezayo, umphakathi ungathatha leli fa futhi uqhubeke namandla okusungula womsebenzi ngendlela ezimele.

### 5) Intando Engeyona Ye-Algorithm (Non-Algorithmic Agency)

- **Inkinga:** Ukukhiqiza kwedijithali okuphelele kodwa okungenamphefumulo, okuphindaphindiwe.
- **Isixazululo se-[PoArt]:** Intando yomuntu eyodwa engenza amaphutha, ethatha ubungozi nezigubhu zemizwa kumele izwakale emsebenzini wobuciko. Ukungaqiniseki ekushayeni kwebrashi, ukusabela okungalindelekile kwezinto kanye nezinqumo zesikhathi somculi, yi-**Siginesha Yoqobo** ehlukanisa umsebenzi wobuciko "Nokukhiqizwa Yinjini".

---

## c) Indlela Yokuqinisekisa & Yokulwa Nenkohliso

Le sistimu iqinisekisa ukuthi umsebenzi uhlala wethembekile futhi uphila hhayi "ekuqaleni" kuphela, kodwa "kuze kube phakade".

### 📦 Iphakethe Lobufakazi (Evidence Pack - The Digital Twin)

Ngemuva kwawo wonke umsebenzi wobuciko onesitifiketi se-[PoArt], kunephakethe ledatha efihlwe futhi enesiginisha sesikhathi abatshalizimali abangayidawniloda:

- **Okurekhodiwe Kwevidiyo Okungathintwanga:** Izithombe ezingathintwanga ezingaphuliwe zesikhathi sokukhiqiza.
- **Ukuhlaziya Kwe-Metadata:** Usuku lokwenziwa kwefayela, ulwazi lwedivayisi esetshenzisiwe nedatha yendawo (Idolobha-Izwe).
- **Izinsiza Zokoqobo:** Ubufakazi bokuthi umsebenzi wobuciko ukhona emhlabeni wokoqobo  
  (Isib: Iphephandaba lanamuhla noma idatha ye-blockchain yaleso sikhathi emi cisha komsebenzi wobuciko).

> *Qaphela ukuhambisana:* Inkulumo "iphakethe lobufakazi" ixhumana nomugqa we-**Evidence Pack → EvidenceRoot → NotarySeal** ezingxenyeni ezandulele; okusho ukuthi ukuphelela kwephakethe kumelwe ngophawu oluqinisekiswe.

### 🔄 Ukuvuselelwa Kwezinsuku Ezingu-365 (The Sustainability Protocol)

- **Isici Siguquko:** Emisebenzini ye-crypto "uDev" (Umthuthukisi) ukhipha ithokheni emakethe futhi ngokuvamile uyanyamalala ngemuva kwenyanga eyi-1-2 (Soft Rug). I-[PoArt] yenza lokhu kungenzeki.
- **Umthetho:** Isimo se-"Verified Artist" (Umculi Oqinisekisiwe) akuyona ingunaphakade. Kusebenza **unyaka owodwa** kuphela.
- **Indlela Yokusebenza:** Umculi/Umthuthukisi kumele anikezele emphakathini **umsebenzi wobuciko omusha, omkhulu noqinisekiswayo** njalo ezinsukwini ezingu-365.
- **Isimo Sesibonelo:** Waqala umsebenzi ngo-2026. NgoJanuwari 2027 isistimu inikezela isexwayiso "Isikhathi Sobufakazi Siphelile". Uma umculi enganikezeli umbukiso omusha, umsebenzi wobuciko omusha wokoqobo noma ukuhlanganiswa kobuchwepheshe obusha, "Ibheji Yokwethemba" yomsebenzi iyawa.
- **Umphumela:** Le sistimu iqinisekisa ukuthi **okuqukethwe akuphelelwa isikhathi** futhi umtshalizimali akabi nokwesaba *"Ingabe umthuthukisi usekhona?"*. Umsebenzi uba yistidiyo esiphilayo.

### 🚩 Ifulegi Elibomvu (Red Flag Protocol)

**Uma kwatholakala noma iyiphi inkohliso (ukusetshenziswa kwe-AI, umsebenzi wobuciko owebiwe, ividiyo eshintshiwe) ngumphakathi noma ngama-algorithm:**

1. Isitifiketi ngokushesha sibekwa uphawu lwe-**"KWENQATSHELWE" (VOID)**.
2. Amaphakethe obufakazi abekwa uphawu lwe-**"Inkohliso"** obala.
3. Umsebenzi ufakwa ohlwini olumnyama lwe-[PoArt]. Lokhu kuqinisekisa iqiniso lokuthi **igama yiyodwa imali** emhlabeni ongenaso isikhungo.
4. Akunakuleka ukufaka amazwi e-[PoArt] kunoma yikuphi ukushicilela, insiza eyodwa evumelekile ngu-https://www.ilhanart.org/public-registry

---

## d) Isiphetho: Imyuzimu, Hhayi Indawo Yokugembula

**I-Pump.fun ne-Decentralized Exchanges (DEX) ngamanje ngeshwa ziyizindawo zokugembula; izibani zicisha zivuke, wonke umuntu ufuna inzuzo esheshayo futhi ikhasino (abakhohlisi) lihlala linqoba. Isizathu esenza siqale umsebenzi lapha naso ukuthi sizama ukuthuthukisa lapha futhi ngoba sinedatha ekhona nabangane abazosisiza ukufinyelela izilaleli ezikhona ngokusakaza bukhoma.**

**I-[PoArt], yinqaba eyakhiwe phakathi kwale ndawo yokugembula.**

- 🎰 Indawo yokugembula incike emidlalweni yamakhadi; thina sincike **eqinisweni lokoqobo**.
- 🃏 Indawo yokugembula ivuleleke enkohliseni; thina sivuleleke **ebufakazini obucacile**.
- ⏳ Indawo yokugembula yesikhashana; thina sigxile **ekuphakameni kobuciko nesayensi**.

**Ithokheni esebenzisa le prothikholi, akuyona "coin" nje kuphela; isheya yedijithali equkethe umjuluko, upende, ikhodi nefilosofi ngemuva kwayo.**

---

## 🗳️ 6) UKUPHATHA & IREKHODI LOMPHAKATHI (Governance & Public Registry)

**Inhloso yalesi sigaba ithi: Ukususa isilinganiso se-[PoArt] esigabeni se-"themba abantu" futhi usiguqulele engqalasizinda yomphakathi eqhubekayo ne-rekhodi + qinisekisa + lawula komphakathi.**

### 6.1 Public Registry (Irekhodi Lomphakathi)

- **Public Registry:** Yonke idatha evunyiwe ibhaliswa ku-`ilhanart.org/registry` (noma i-GitHub Registry).

**Umqondo werekhodi (isilinganiso esiphakanyisiwe - ngefomethi ye-JSON path):**

Wonke amarekhodi angena kurejista athwala okungenani lezi zindawo eziyisisekelo eziqinisekiswayo:

- **Ubunikazi & Isimo:**
  - `certificate_id` (isibhekiso esifundekayo)
  - `status` (active / void)
  - `void_reason` (uma ikhona)
  - `visibility` (private / masked / public)
  - `created_at` (isitembu sesikhathi)

- **Isikhungo Esikhiphayo:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Ulwazi Lomsebenzi Wobuciko:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (uma kungenzeka; ukuze kuhlonzwe umphathi wethokheni)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Idatha Yezomthetho:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Ubufakazi be-Cryptographic:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Ukuphatha:**
  - `governance.decision`
  - `governance.review_notes`

Irekhodi lingaba nezigaba ezimbili:
- **1)** Inkomba efundwa ngumuntu (ukubala kwewebhu / ukusesha / ukuhlunga)
- **2)** I-manifest efundwa ngumshini (amarekhodi we-JSON; ukuze kuqinisekiswe i-PFE)

**"Irekhodi" lapha, liyaqinisekiswa ngochungechunge lwe-Evidence Pack → EvidenceRoot → NotarySeal lwe-PFE. Irekhodi alinikezi "isimangalo" kodwa linikeza umgomo wokuqinisekisa.**

---

### 6.2 Inqubo Yokufaka Isicelo Se-PoArt Verified

**Izicelo ze-PoArt Verified zihlolwa yi-Ilhan Art Gallery ngokwesilinganiso se-PoArt esi-5. Impendulo yomphakathi iyabhekwa, kodwa isinqumo sokugcina sincike eqenjini le-curator. Izinqumo zidalulwa obala futhi zibhaliswa ku-ilhanart.org/registry.**

#### Inqubo Yesicelo

**Isicelo:**
- Umculi/umsebenzi ufaka isicelo se-PoArt Verified
- I-Evidence Pack ilungiswa (okurekhodiwe kwevidiyo, i-metadata, izixhumanisi zokusakaza bukhoma)
- Isicelo sithunyelwa ku-Ilhan Art Gallery

**Ukuhlolwa (Izinsuku Ezingu-30):**
- Ithimba legallery lihlola i-Evidence Pack kabanzi
- Kuhlolwa zonke izilinganiso ze-PoArt ezi-5:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Umhlangano nomculi (uyinketho)

**Ukubonisana Nomphakathi:**
- I-Evidence Pack yabiwa obala ngesikhathi senqubo yesicelo
- Umphakathi ungaphendula nge-ilhanart.org
- Abaphathi bethokheni (okungenani i-10,000 $CULTURE) ikakhulukazi bangaphakamisa iziphakamiso
- **Zonke izimpendulo zibhekwa ngesikhathi senqubo yokuhlola**
- **Nokho isinqumo sokugcina sincike ekuhlolweni kwe-curator**

**Isinqumo:**
- Igallery ivuma noma yenqaba isicelo
- Isizathu sesinqumo sidalulwa obala
- Uma samukela → PoArt Verified badge
- Uma senqaba → Kungafakwa isicelo kabusha ngemuva kwezinyanga ezi-6

**Ukucaca:**
- Zonke izicelo nezinqumo zibhaliswa ku-ilhanart.org/registry
- Irekhodi lesinqumo lishicilelwa obala:
  - Usuku lwesicelo
  - Isifinyezo senqubo yokuhlola
  - Isinqumo (Samukela / Senqaba)
  - Isizathu sesinqumo (incazelo emfushane)
  - Isifinyezo sezimpendulo zomphakathi (ezingaziwa)

#### Kungani Isinqumo Se-Curator?

**Ukulawula Ikhwalithi:**  
Isimo se-PoArt Verified siyibheji enezindinganiso eziphakeme. Ukuhlolwa kwe-curator kuqinisekisa ukugcinwa kwalezi zindinganiso.

**Ukuvimbela Ukugudluzwa Kokuqagela:**  
Akukwazeki ngokobuchwepheshe ukuphatha ngokugcwele ku-on-chain (isib: i-Realms, i-DAO voting) namathokheni e-Pump.fun. Izinhlelo zokuvota ze-off-chain nazo zivuleleke ekugudluzweni kwe-whale nasekuhlaselweni okuhlelekile. Isinqumo se-curator sisusa lobu bungozi.

**Ukusebenza Ngokushesha:**  
Esikhundleni sezindlela zokuvota eziyinkimbinkimbi, inqubo yesinqumo esheshayo necacile. Abaculi bathola umphumela ezinsukwini ezingu-30.

**Ukubamba Iqhaza Komphakathi:**  
Impendulo yomphakathi ibhekwa ngokugcwele futhi ithinta inqubo yesinqumo. Nokho isinqumo sokugcina sincike ethimbeni le-curator elivikelwe ekugudluzweni.

**Ikusasa:**  
Lapho umsebenzi usuvuthiwe (2027+), indlela yokubonisana nomphakathi ingaqiniswa. Nokho ukuvikelwa kwesilinganiso se-curator kuhlala njalo.

---

### 6.3 Token Utility (Izindawo Zokusetshenziswa Kwethokheni)

**Izinzuzo ezinikwa abaphathi be-$CULTURE token:**

**1. Ukungena Okuqala Emicimbini Yegallery:**
- Ilungelo lokwenza umbukiso evikini eli-1 ngonyaka ku-Ilhan Art Gallery (ilungelo lingadluliselwa)
- Izaphulelo zokupenda okuwayo
- Ilungelo lesaphulelo esiphakathi kuka-10% no-30% ezithombeni egallery

**2. Ukungena Okuphelele Ku-PoArt Registry:**
- Amarekhodi abanzi awo wonke umsebenzi wobuciko oqinisekisiwe
- Izinguqulo eziphelele ze-Evidence Pack
- Amathuluzi okuqinisekisa ezomthetho

**3. Advisory Voting:**
- Ilungelo lokweluleka ezicesweni ze-PoArt Verified
- Ukungena emigudu yempendulo yomphakathi
- Ukubamba iqhaza ezingxoxweni zokuphatha

**4. Exclusive Content:**
- Okuqukethwe kwemuva kwesiteji sestidiyo
- Izingxoxo nabaculi namavidiyo enqubo
- Ukungena emibhalweni yobuchwepheshe

**Qaphela:**  
Abaphathi bethokheni banikeza ivoti lokweluleka (advisory vote). Isinqumo sokugcina ngesethimba le-curator. Le ndlela ikhethwe ukuvimbela ukugudluzwa kwe-whale nokuhlaselwa kokuqagela. Akukho umvuzo we-staking ngoba sifuna ababambi qhaza besiko besikhathi eside, hhayi imali ye-mercenary yesikhathi esifushane.

---

### 6.4 Metadata Sync (Ukuhambisana Nomhlaba Wokoqobo)

- **Metadata Sync:** Idatha yobuchwepheshe erejistini kumele ihambisane 100% nempahla yoqobo.

**Ukuchaza "ukuhambisana 100%" ngokobuchwepheshe (ukucacisa okuphakanyisiwe):**

- **Ukuhambisana okuncane (okudingekayo):**
  - I-`asset.fingerprints.sha256/sha512` erejistini ne-hash yefayela elikhona kumele kube **efanayo ngokuphelele**.
  - I-`proof.notary_seal` erejistini uma iphindwa (uma kukhona i-Evidence Pack) kumele ibe **efanayo ngokuphelele**.

- **Ukuhambisana kwesibhekiso sokoqobo (uhlobo lobufakazi):**
  - Ubufakazi obufana nomsebenzi wobuciko woqobo owaboniswa ekusakazeni bukhoma + isibhekiso sosuku/ibulokhi, kumele buhambisane ne-Evidence Pack.

- **Ukuhambisana nobumfihlo:**
  - Ngokubonakala kwe-`masked` izindawo ezifana ne-IP/indawo **zishicilelwa ngokwesilinganiso sokufihla**.

---

### 6.5 Ukuphikisa, Ukuhlola Nokususa (Dispute & Revocation)

Irekhodi, akuyona indlela "yokuvuma" kuphela; **yindlela yokulawula ephilayo ngokumelene nenkohliso**.

- Uma kuqalwa ukuphikisana irekhodi lingafakwa kumodi ye-**"review"**.
- Uma kutholakala inkohliso kubekwa uphawu lwe-`status: void` futhi kwengezwa isizathu:
  - `void_reason` (ukusetshenziswa kwe-AI / ukweba / ukugudluzwa njll.)
  - `revoked_at` (isikhathi sokususa)
- Umthombo wesinqumo sokususa ubonakala ngokucacile erejistini:
  - ukuhlolwa kwe-curatorial / ukuphikiswa komphakathi / iphawu lokuhlaziya kwezomthetho (okufanele)

> **Lesi sigaba sihambisana nomqondo we-VOID esigabeni se-"Red Flag Protocol" erejistini.**

---

### 6.6 Isibonelo Serekhodi Lerekhodi (Elifundwa ngumshini)
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

> *Qaphela: I-`asset.fingerprints.sha512` namanye amanani e-hash afinyeziwe ngenjongo yokubonisa; ekusebenzeni kwangempela kusetshenziswa uchungechunge oluphelele lwezinhlamvu ze-hexadecimal.*

---

## 7) 🔐 UPHAWU LOBUCHWEPHESHE (NOTARY SEAL)

**I-algorithm yophawu oluqinile ekhiqizwa yi-PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$
# [PoArt] Iprothikholi Ye-Digital Notary & Ubufakazi Bezomthetho (Beta v1.0)

> **"Isiko likhulu kunemali. Vikela imisebenzi yakho kusukela namuhla, uyiyise kusasa."**

---

## Kungani Ivulekele Umphakathi?

Ukuphepha kwangempela kuvela ekucaceni. Ngesikhathi se-**Public Registry (Irekhodi Elivulekele Umphakathi)** yethu, noma ubani nomaphi emhlabeni; angaqinisekisa ngomzuzwana uma ifayela elinesandla sakhe lingeyona yoqobo, ngaphandle kokudinga noma iliphi igunya.

---

## 🧩 Kungani Kukhona "Amamoduli Okubonakala" Amaningi?

Lena ingxenye ebaluleke kakhulu yekhodi (imenyu yokukhetha ukubonakala). Lezi zinketho zivumela abasebenzisi ukuthi babhalanse **"Ubumfihlo vs. Ukucaca"**:

### 🔒 Okuyimfihlo (Private)

- **Isimo:** Umculi akakafuni ukushicilela umsebenzi wobuciko kodwa ufuna ukufaka isitembu sosuku futhi afakazele "ngenze lokhu ngalolu suku".
- **Okwenziwa Yikhodi:** Ibhala idatha kudatabase kodwa ifaka uphawu lwe-`visibility: "private"`. Esikhathini esizayo lapho ubhala inqubomgomo ye-"Public Read" ungawufihla la marekhodi emphakathini ngokuthi `WHERE visibility = 'public'`.

### 🕶️ Okufihliwe (Masked)

- **Isimo:** Umculi ufuna ukucaca kodwa wesaba ukutholakala kwekheli lakhe lasekhaya (indawo ye-IP).
- **Okwenziwa Yikhodi:** Ohlangothini lwe-JavaScript imisebenzi ye-`maskIP` ne-`maskLoc` iyasebenza. Iguqula ikheli le-IP libe simo soku-`88.241.***.***`, indawo ibe simo soku-`***/TR` futhi ithumele inguqulo ehlanziwe kudatabase.
- **Iphawu Lobumfihlo:** Ukufihla kwenziwa esiphequluli, i-Supabase ayiboni indawo yangempela. **Nokho:** Uma kusetshenziswa ama-API angaphandle njenge-ipapi.co yedatha yendawo, laba banikeli babona ikheli le-IP ngesikhathi sesicelo.
- **Ukufaka Uphawu Kumodi Ye-Masked:** Ukubalwa kwe-EvidenceRoot ne-NotarySeal kwenziwa ngedatha ye-forensics efihliwe; ngakho-ke ukuqinisekiswa kuhlala ku-deterministic.

### 🌍 Okuvulekele Wonke Umuntu (Public)

- **Isimo:** Ukucaca okuphelele. Ngokwesilinganiso se-[PoArt], kuchazwa obala ukuthi umsebenzi wobuciko wenziwe kuphi, nini, kusuka kuluphi uhlelo lokuxhumana.

---

## 💡 Ukusungula Kobuchwepheshe

I-PoArt, akuyona nje isistimu yokulayisha ifayela. Iyinjini ye-**"Uchungechunge Lobufakazi Lwezomthetho" (Forensic Chain of Custody)** eletha isilinganiso esisha ngokuhlanganisa izingxenye zobuchwepheshe ezintathu ezahlukene embizeni eyodwa.

**Ingxenye echazwe njengo-"injini" kulesi sigaba, ihambisana nengxenye eyisisekelo ye-PoArt Forensic Engine (PFE) ngamagama angaphambili.**

### 1) Client-Side Hashing (Ubumfihlo Obukhulu)

Amafayela omsebenzi wakho awulayishwa kumseshi. Injini yethu esebenza esiphequluli (Client-side) ibala i-hash (isifinyezo sedijithali) yefayela ekhompyutheni yakho. Kumseshi kuthunyelwa kuphela lolu phawu lweminwe ne-metadata.

> **Iphawu Lobumfihlo:** Ifayela lomsebenzi wobuciko alilayishwa kumseshi futhi livikelwa ngale ndlela. Nokho idatha ye-forensics (IP/indawo) yabiwa ngokwemodi yokubonakala ekhethiwe (private/masked/public).

### 2) Forensic Data Fusion (Amandla Ezomthetho)

Ingaphezu kwesitembu sesikhathi (Timestamp) esivamile kakhulu. Isistimu ihlanganisa le datha kophawu lwe-"Genesis Seal" olulodwa:

- **Isifinyezo Sedijithali (SHA-512):** Uphawu lweminwe lwedijithali olukhiqizwe ngokusebenzisa isilinganiso sokuphatha se-SHA-512 oluzophuka noma iphikseli elilodwa lomsebenzi wobuciko lishintshwa.
- **Indawo & Isikhathi:** Usuku olunokunemba kwe-millisecond somsebenzi, idatha yezwe, idolobha nesifunda.
- **Ubunikazi Bedivayisi:** Uhlelo lokusebenza, isiphequluli nohlobo lwedivayisi (ukuhlaziya i-User-Agent).

---

## 🛡️ Izindawo Zokusetshenziswa Nezinzuzo

Uma ungumculi, umbhali noma umklami, ukuthi "Ngakwenza lokhu ngaphambili" akwanele, kumele ufakazele.

**Umsebenzi wobuciko owufake uphawu nge-PoArt:**

- **Ubufakazi Bezibalo:** Noma iphikseli elilodwa lefayela lakho lishintsha isistimu iyakubona. Ukugudluzwa akukwazeki.
- **Isisekelo Sezomthetho:** Kubhaliwe ukuthi umsebenzi wobuciko wafakwa uphawu ngaluphi usuku, kuliphi idolobha, kusuka kuliphi idivayisi.
- **Isitifiketi Ngokushesha:** Ngomzuzwana sikhiqiza **"Isitifiketi Sobunikazi Bempahla"** esiqondene nawe, esinophawu lwe-QR nesivaliwe.

---

## ⚙️ Isakhiwo Sesistimu Nezici Zobuchwepheshe

Isistimu yenzelwe phezu kwesakhiwo se-"Serverless" (Esingenamseshi), sigxile ekusebenzeni okuphezulu nasekukwazini ukukhula.

| Isigaba | Ubuchwepheshe | Incazelo |
|---------|---------------|----------|
| **Cryptography** | SHA-256 & SHA-512 | Isifinyezo sokufihla esiphindwe kabili |
| **Database** | Supabase (PostgreSQL) | Isakhiwo sedatha ye-JSONB, izinqubomgomo ze-RLS |
| **Idatha Yezomthetho** | ipapi.co API | Ukuthathu kwe-IP/Indawo/Isikhathi |
| **Rendering** | html2canvas + jsPDF | Ukukhiqiza i-PNG/PDF ohlangothini lwekhasimende |
| **Frontend** | Vanilla JavaScript | Ukuncika kwe-framework okuyiziro |
| **Ukuphepha** | Client-side hashing | Ifayela alilayishwa kumseshi |

### Izici Eziphawulekayo

| Isici | Imininingwane | Kubancintisani? |
|-------|---------------|-----------------|
| **Drag & Drop UI** | Hudula ifayela, ukubukela ngokushesha | ❌ Eziningi azinakho |
| **Multi-Format Export** | PNG, JSON, PDF - chofoza kanye | ⚠️ Kulinganiselwe |
| **Real-Time Preview** | Ukubukela isitifiketi bukhoma | ❌ Akukho |
| **Privacy Controls** | Izinketho ze-Private/Masked/Public | ❌ Akukho |
| **Client-Side Hashing** | Ifayela aliyi kumseshi | ✅ Ezimbalwa kuphela |
| **Forensic Metadata** | IP, indawo, idivayisi, isikhathi - konke ndawonye | ❌ Okuhlukanisiwe |
| **QR Verification** | Ikhodi ye-QR yokuqinisekisa ngokushesha | ⚠️ Kulinganiselwe |
| **Rate Limiting** | Ukuvikelwa kwi-spam (RLS + Client) | ❌ Eziningi azinakho |

---

## 🗺️ Imephu Yomzila: Ikusasa "Elingenakho Ukwethemba"

Inguqulo yamanje **(Beta v1.0)**, yenzelwe ukuze inikeze umsebenzisi wokugcina ijubane eliphezulu, isixhumi esikulula nokungena kwamahhala. Nokho umbono wethu wokugcina ukudlulela esakhiweni lapho noma umlawuli wedatabase (thina) engakwazi ukungenelela.

### Faz 1: Beta v1.0 (Manje Bukhoma)

**Ingqalasizinda:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + IPFS backup)
- Gallery self-attestation (esikhungweni kodwa ecacile)

**Ithokheni:**
- Ipulatifomu: Pump.fun
- Umfutho: Raydium (othomatic)
- Ukuphatha: Advisory kuphela (ukubonisana nomphakathi)

**Inhloso:**
- Ijubane, ukususa izithiyo ze-UX
- Ukuhlinzeka ngokuphepha "okungenamdweshu"
- Ukwakha umphakathi

**Token Utility (v1.0):**
- Ukungena okuqala emicimbini yegallery
- Ukubuka i-PoArt Registry
- Ilungelo le-advisory voting

---

### 🚀 Faz 2: Decentralized Authority (2026 Q2-Q4)

Le faz ihlanganisa ukudlula kwesistimu esakhiweni esisebenza "Client-Side" ngokuphelele, esakhiweni esiphephile kakhulu nesingenaso isikhungo.

| Isici | Kunikeza Ini? | Tech Stack | ETA |
|-------|---------------|------------|-----|
| **Edge Function INSERT** | Ukuvimbela i-spam + ukuphepha kwe-API Key | Supabase Edge (Deno) | Q2 2026 |
| **Wallet Signature** | Ubunikazi obungenaso isikhungo | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | Ukulondoloza okungenaso isikhungo | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | Ukususa isitifiketi samanga | DB Schema Update | Q2 2026 |
| **Audit Log** | Irekhodi lokuphenya kwezomthetho | Custom logs table | Q3 2026 |
| **OpenTimestamps** | Ukuxhuma ku-Bitcoin | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain voting (x/web) + siginesha yesikhwama
- Ukukhethwa kwabamele umphakathi (izinsuku ezingu-90 zokuqala)
- Ukulawula kwesikhwama sokusebenza se-multi-sig
- Weighted advisory voting (neqophelo le-whale)

**Immutability:**
- Ukusekela irekhodi ngama-hash e-IPFS
- Ukuxhuma isitembu sesikhathi se-Bitcoin
- Ukulungisela ukuqinisekisa kwe-cross-chain

---

### Faz 3: Ukungenaso Isikhungo Okuphelele (2027+)

| Isici | Umgomo | ETA |
|-------|--------|-----|
| **On-Chain Registry** | Irekhodi le-on-chain le-Solana | Q1 2027 |
| **Enhanced Token Utility** | I-NFT mint, izici ezithuthukisiwe | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **DID Integration** | Ubunikazi Obungenaso Isikhungo | Q3 2027 |
| **Community Governance** | Isistimu yokweluleka eqinisiwe | Q4 2027 |
| **Legal Recognition** | Ukuqinisekiswa ezinkantolo zaseTurkey | 2027-2028 |
| **API for Developers** | I-endpoint ye-API yomphakathi | Q3 2027 |

**Ukuguquka Kokuphatha:**
- v3.0: Imodeli exubile (curatorial + umphakathi osindayo)
- 2028+: Ukuphatha komphakathi okuphelele (okuyinketho)
- Ukulawula ikhwalithi ye-curatorial kuhlala njalo

---

## 🧬 Isakhiwo Sedatha Yeprothikholi (JSON Schema)

**Isitifiketi ngasinye se-[PoArt] sinekhadi lobunikazi le-JSON elithwetshulwayo neliqu qinisekiswayo elikhiqizwe kulesi silinganiso.**

> **Qaphela:** Le fomethi ye-Identity JSON ifomethi yesitifiketi enikezwa umsebenzisi. Kumarekhodi erejista kusetshenziswa i-`registry.asset` esikhundleni se-`identity.asset_data` (ukumapisha: `identity.asset_data` == `registry.asset`).
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

## 🔬 Ukujula Kobuchwepheshe: I-Algorithm Yophawu

### Imisebenzi Ye-Hash Enomthetho
```javascript
// Imisebenzi Yokusiza: Guqula i-digest ibe yithumbu le-hex
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Guqula ithumbu libe yi-byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Ukuphatha ithumbu le-canonical forensics (v1.0: ukuhlelwa kwezindawo okungashintshi + UTF-8 + \n delimiter)
// Iphawu le-Faz 2: Kuzodlulwa ku-canonical JSON nge-RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Inqubo Yokukhiqiza I-NotarySeal (Enomthetho Ngokuphelele)
```javascript
// 1. Ukubala i-FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Ukuqoqa idatha ye-Forensic (ukusetshenziswa kwesitembu sesikhathi esisodwa)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Ukukhiqiza isitembu sesikhathi esisodwa
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Isitembu sesikhathi esifanayo
  };
  
  return { forensics, timestamp };
}

// 3. Ukwakha i-EvidenceRoot (nge-canonical encoding)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Ukukhiqiza i-NotarySeal (ukusetshenziswa kwesitembu sesikhathi esifanayo)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Imisebenzi yokusiza yokufihla (ukwesekwa kwe-IPv4 ne-IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Ukuhlola i-IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // I-IPv6 noma ifomethi engaziwa
  return "***";
}
```

### Inqubo Yokuqinisekisa (Amazinga Amabili)

#### Quick Verify (Ukuqinisekisa Okusheshayo)
```javascript
// Kuhlola kuphela i-hash yefayela (ifulegi elibomvu elisheshayo)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Donsa kurekhodi
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Ukuqhathanisa ama-hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Okoqobo - I-hash yefayela iyahambisana"
    };
  } else {
    return {
      valid: false,
      message: "❌ Inkohliso - Ifayela ligudluziwe"
    };
  }
}
```

#### Full Verify (Ukuqinisekisa Okuphelele)
```javascript
// Iphinda ikhiqize i-EvidenceRoot ne-NotarySeal futhi iqinisekise
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Donsa kurekhodi
  const cert = await fetchFromRegistry(certificateId);

  // 1) Ukuhlola i-FileHash (ifulegi elibomvu elisheshayo)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Inkohliso - I-hash yefayela ayihambisani" };
  }

  // 2) Phinda ukhiqize i-EvidenceRoot (nge-forensics egcinwe kurekhodi)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Ayihambisani - I-EvidenceRoot ayifani" };
  }

  // 3) Phinda ukhiqize i-NotarySeal (ngesitembu sesikhathi esifanayo + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Ayihambisani - I-NotarySeal ayifani" };
  }

  // Okuyinketho: Ku-Faz 2 qinisekisa i-signer_sig nge-attestation_pubkey futhi
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Isiginesha ayivumelekile" };

  return { valid: true, message: "✅ Okoqobo - Full Verify idlulile" };
}
```

> **Amaphawu Abalulekile:**
> - **Quick Verify:** Ihlola kuphela i-hash yefayela ukusetshenziswa okusheshayo.
> - **Full Verify:** Iqinisekisa zonke izigaba zeprothikholi (EvidenceRoot + NotarySeal).
> - Yonke imisebenzi ye-hash yenziwa ngomthetho, nge-encoding ne-delimiter ezingashintshi.
> - **Isilinganiso se-canonicalization se-v1.0:** Ukuhlelwa kwezindawo okungashintshi + UTF-8 encoding + `\n` delimiter.
> - **Uhlelo lwe-Faz 2:** Ukudlulela ku-canonical JSON nge-RFC 8785 (JCS - JSON Canonicalization Scheme).
> - Kumodi ye-Masked, ukubalwa kwe-EvidenceRoot ne-NotarySeal kwenziwa nge-forensics efihliwe.
> - Isitembu sesikhathi esisodwa sisetshenziswa kuyo yonke inqubo (forensics + NotarySeal); ukuqinisekiswa kwe-deterministic kuqinisekiswa.
> - **Amagama ezindawo ze-Forensics:** `ip_masked`, `location`, `device`, `timestamp` (ikhodi nerekhodi kuhambisana ngokuphelele).
> - **Indlela ye-Registry:** `certificate.asset.fingerprints` (kuhambisana ngokuphelele nekhodi yokuqinisekisa).
> - **signer_sig eRekhodi:** Isigaba se-`proof.signer_sig` siyadingeka nge-Full Verify.
> - Indlela ye-SignerSignature izoqala ukusebenza ku-Faz 2 nge-Solana Wallet Adapter; ku-v1.0 ukuqinisekiswa kungenzeka nge-`attestation_pubkey`.

---

## 📊 Ukuhlaziywa Kwabancintisani (Kubuyekeziwe)

I-PoArt, imile ku-"Sweet Spot" (Indawo Enhle Kakhulu) egcwalisa izingqala zezixazululo ezikhona.

| Isici | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|-------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Izindleko** | 🆓 Mahhala | 🆓 | 💰 Ukukhokha | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Kulula Kakhulu | ❌ CLI | ⚠️ Maphakathi | ⚠️ Maphakathi | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Bukhoma | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ Amamodi ama-3 | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Ubumfihlo | ✅ | ❌ Layisha | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Kuphelele | ❌ | ❌ | ⚠️ Kulinganiselwe | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Ngokushesha | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Imephu | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Ukwesekwa KwesiZulu** | ✅ Okoqobo | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Incazelo:**
- ✅ : Ukwesekwa okuphelele / kukhona
- ⚠️ : Kulinganiselwe / ezinhlelweni zokukhokha
- ❌ : Akukho / akusekelwa
- 🔄 : Kumephu (kuthuthukiswa)
- 🆓 : Mahhala ngokuphelele
- 💰 : Ukukhokha / kudingeka ukubhalisa

### Izingqala Zabancintisani, Amandla e-PoArt

| Isiphazamiso | Abancintisani | PoArt |
|--------------|---------------|-------|
| **Ubunzima Bokusetshenziswa** | CLI, ulwazi lwe-API, kudingeka isikhwama | Hudula useke, kuphela ngokuchofoza oku-3 |
| **Isithiyo Sezindleko** | Ukubhalisa kwe-$50-500/ngenyanga | 100% mahhala |
| **Ubumfihlo** | Ifayela lilayishwa kumseshi | Client-side, ifayela aliyi |
| **Idatha Yezomthetho** | Isitembu sesikhathi kuphela | IP, indawo, idivayisi, isikhathi - konke |
| **Ukwesekwa KwesiZulu** | Akukho noma kulinganiselwe kakhulu | Ukwesekwa kolimi loqobo |
| **Umthombo Ovulekile** | Ibhokisi elivaliwe | Yonke ikhodi ivulekile ku-GitHub |

---

## 📈 Izibalo Zokusetshenziswa (Imigomo ye-2026 Q1)

| Isilinganiso | Umgomo | Isimo |
|--------------|--------|-------|
| **Izitifiketi Eziphelele** | 1,000 | 🔄 Inqubekela Phambili |
| **Abasebenzisi Abasebenzayo** | 500 | 🔄 Inqubekela Phambili |
| **Inani Lokuqinisekisa** | 5,000 | 🔄 Inqubekela Phambili |
| **Uptime** | 99.9% | ✅ Kusebenza |
| **Isikhathi Sokuphendula Esilinganiselwe** | <200ms | ✅ Kuhle Kakhulu |

---

## 🌍 Umphakathi & Ukwesekwa

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Iwebhu:** [ilhanart.org](https://ilhanart.org)
- **I-imeyili:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Abanikeli

Iprothikholi ye-PoArt iqhubeka nokuthuthuka ngeminikelo yomphakathi womthombo ovulekile.

**Ukunikela:**
1. Yenza i-Fork
2. Dala i-feature branch (`git checkout -b feature/amazing-feature`)
3. Yenza i-Commit (`git commit -m 'Add amazing feature'`)
4. Yenza i-Push (`git push origin feature/amazing-feature`)
5. Vula i-Pull Request

### 🛠️ Sidingani Manje? (Isicelo Sosizo)

Silindele iminikelo yabasunguli abanamava kulezi zihloko zokuthuthukisa **Faz 2** yeprothikholi ye-PoArt:

* **Supabase Edge Functions:** Ukuthuthisela ukuvikelwa kwe-spam ohlangothini lweseva.
* **Solana Web3.js:** Ukuhlanganiswa kokusayina kwesikhwama (Wallet Signing).
* **IPFS / Arweave:** Ukuhlanganiswa kwezinsizakalo zokulondoloza ne-pinning.
* **Community Tools:** Ukuvota kwe-X, izinhlelo zokuvota, i-analytics dashboard.

> Sicela uqale ingxoxo esigabeni se-"Issues" ngaphambi kokwengeza isici.

---

## 💬 Amaphawu Okugcina

### Pump.fun Neqiniso

Lo msebenzi waqalwa ku-Pump.fun ngoba:
- ✅ Ukungena komfutho (Raydium automatic migration)
- ✅ Ukungena emphakathini okhona
- ✅ Izindleko zokuqala eziphansi

Nokho ake sicacise:
- **Intengo yethokheni**, akuyona inkomba yempumelelo yobuciko
- **Isabelomali sokusebenza** inani lethokheni libalulekile (igallery, imibukiso, ingqalasizinda)
- **Izinkomba zempumelelo:** Imisebenzi yobuciko eqinisekisiwe + ukubamba iqhaza komphakathi + abavakashi boqobo

### Ukuphatha Nokungenaso Isikhungo

**Iqiniso le-v1.0 (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (esikhungweni kodwa ecacile)
- Ukuphatha: Advisory kuphela (isinqumo sokugcina se-curatorial)
- Token utility: Ukungena kugallery + registry + ukuqala kwe-NFT

**Umbono we-v2.0+ (2027+):**
- Registry: On-chain (Solana)
- Iziginesha: Ezisekelwe esikwameni (ezingenaso isikhungo)
- Ukuphatha: Okuxubile (ukweluleka komphakathi + ikhwalithi ye-curatorial)
- Token utility: Izici ezithuthukisiwe + ukungena okuthuthukisiwe

Le ndlela inikeza **ukusebenza ngokushesha** no**kulawula ikhwalithi** esigabeni sokuqala, ngesikhathi ivula indlela yokwandisa **ukubamba iqhaza komphakathi** esikhathini esizayo.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Isiko Likhulu Kunemali*

## 🧾 Ilayisensi

MIT License © 2026 İlhan Art Gallery Initiative

Bona [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) ukuze uthole imibandela ephelele.

---

## 💬 Ukubonga

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Lo msebenzi uthuthukiswe ngokuqalwa yi-[İlhan Art Gallery], futhi ikhodi yomthombo ivulekele umphakathi ngenjongo yokucaca.**

**IPROTHIKHOLI V1.0 // IFAKWE UPHAWU NGE-SHA-512.**

*© 2026 İLHAN ART | WONKE AMALUNGELO EMISEBENZI YOBUCIKO, IZITHOMBE NEMIBONO AGODLIWE.*

---
