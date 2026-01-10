# 📚 ISICHAZAMAZWI SAMAGAMA OBUCHWEPHESHE NEMIQONDO
> **"Ukuqonda ulimi lwale nhlekelele kusho ukuqonda umbono wayo."**

## ⚙️ Injini Yophenyo ye-PoArt (PFE) v1.0: Ingqalasizinda Eyisisekelo

**Injini Yophenyo ye-PoArt (PFE)** iyisigaba esiyinhloko esimele ingqondo ephakathi kanye nokusebenza kobuchwepheshe ngemuva kohlelo lwe-[PoArt]. Lena yinjini "yophenyo" ethatha idatha engavuthiwe yokukhiqizwa komsebenzi wobuciko futhi iyiguqula ibe **ubufakazi bedijithali** obungaqinisekiswa futhi obungenakuguqulwa.

### 🧩 Kungani "PoArt Forensic"?

- **PoArt (Ubufakazi Bobuciko):** Injongo yenjini ukuxhuma inani le-asethi yedijithali kungeyona inkomba, kodwa **inqubo yokukhiqizwa engaqinisekiswa**.
- **Forensic (Ukuqinisekisa Kwesayensi):**
  - **Incazelo Yobuchwepheshe:** Indlela ye-algorithm kanye nochungechunge lwerekhodi lokuqinisekisa ukuthi idatha yenqubo yokukhiqizwa (ukupenda ngebrashi, ividiyo yesikhathi, amarekhodi) ayiphazanyisiwe.
  - **Isigaba Sefilosofi:** Isimangalo sokuguqula **isikhathi somuntu, umzamo, kanye nezindleko zokunquma** sibe yiqiniso elingakalwa, ngokumelene nokukhiqizwa kwe-AI "umphumela osheshayo".

> Qaphela: Ukuhlanganiswa kwe-blockchain (isibonelo, i-Solana) akuyona imbumbulu ye-PFE; kuzochazwa ngokwehlukile njenge **Isigaba Se-Chain Anchor** ngezinhloso zokuqinisekisa/ukubhalisa.

### 🛠️ Ububanzi Bobuchwepheshe v1.0

**Injini Yophenyo ye-PoArt (PFE) v1.0** yakhiwe phezu kwe **3 izinsika eziyinhloko** ezilandelayo kunokuba kube ngamamodeli ezezimali ayinkimbinkimbi:

1. **Hashing & Sealing (Ukuvalela):**  
   I-PFE isebenza ngokucacilelayo zonke izinto ku-Evidence Pack (ifayela lomsebenzi, ividiyo, i-JSON/irekhodi, isiginesha, njll.) futhi ikhiqize inani eliyingqayizivele le-**NotarySeal**.

   **Imiqondo Eyinhloko (v1.0):**
   - **FileHash (izigxivizo zeminwe yomsebenzi):** I-hash ekhiqizwe kusuka kuma-bytes efayela lomsebenzi.
   - **EvidenceRoot (impande yephakethe lobufakazi):** Isifinyezo sempande esimele ubuqotho be-Evidence Pack (impande ye-Merkle noma i-hash yesiboniso esiqondile).
   - **NotarySeal (uphawu lokugcina / okukhiphayo kwe-PFE):** Uphawu lokugcina olukhiqizwe kusukela enhlanganyeleni ye-EvidenceRoot + isikhathi + isiginesha.

   **Amafomula (ebonakala ngokucacile kubatshalizimali):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Izincazelo Ze-Payload Eqondile (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Qaphela: Inani elibhekiswa njengokukhiphayo kwe-PFE ngu-**NotarySeal**. Inqubo **SignerSignature** izovuswa eSigabeni 2 (nge-Solana Wallet Adapter); ku-v1.0 yamanje, kusetshenziswa isiginesha sokuqinisekisa sesistimu. Isihluthulelo somphakathi sokuqinisekisa sishicilelwa kurekhista ngaphansi kwensimu `issuer.attestation_pubkey`.

2. **Indexing (Ukugcina):**  
   Kubhalisa ukuthi yisiphi isikhwama, ngaluphi usuku, esithumele **Ubufakazi Bomsebenzi** kumuphi umsebenzi esigabeni srekhista esicacile futhi esingabuzwa.  
   *(Lesi sigaba singaba idathabheyisi; ukuhlanganiswa kochungechunge kuchazwa ngokwehlukile njenge-"Isigaba Se-Chain Anchor".)*

3. **Verification (Ukuqinisekisa):**  
   Uma ubuqotho bomsebenzi bubuzwa, i-PFE isebenza kabusha ubufakazi obungavuthiwe; ihlola ngokwezibalo ukuthi amanani e-**EvidenceRoot / NotarySeal** abalwe ayafana namarekhodi egcina.

---

### 🧮 Ithiyori Yenani Le-PoArt (The Value Theorem)

Uhlelo lwe-[PoArt] luhlanganisa inani ($V$) le-asethi yedijithali kungesona ukubona kwemakethe okungaqondakali, kodwa ku-**iqiniso lomzimba lenqubo yokukhiqizwa**.

I-Artificial Intelligence (AI) ibhubhisa inqubo ngokunikeza umphumela ngokushesha ($t \to 0$). I-[PoArt], nokho, iphatha inani njengokuqoqwa kwezingxenye **zesikhathi, umsebenzi, kanye nentando**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Izincazelo Zokuguquguquka

- **$\int dt$ (Ukuqoqwa Kwenqubo):**  
  Inani alikho "umphumela" osheshayo; yinqubo eqoqwe phakathi kuka-$t_{\text{start}}$ no-$t_{\text{end}}$. Njengoba ubude buncipha (ukukhiqizwa kwe-AI), umphumela we-integral usondela ku-0.

- **$P_{\text{labor}}(t)$ (Amandla Omsebenzi Ngokushesha):**  
  Umele ukuqina komzamo wengqondo nowomzimba oseziwe ngesikhathi sokukhiqizwa. Njengoba umzamo ongaqinisekiswa ukhula, i-integrand iyakhula.  
  > Qaphela: Leli gama lingalungiswa ngokwenza ngezimpawu zomsebenzi ezilinganiselwa/ezingaqinisekiswa.

- **$I_{\text{agency}}(t)$ (Isilinganiso Sentando):**  
  Amandla omkhiqizi wokuthatha ubungozi nokwenza izinqumo. Uthatha inani phakathi kuka-$0$ no-$1$.
  - **AI ($I \approx 0$):** Isebenzisa imiyalo, ayithathi ubungozi, ayikhokhi izindleko.
  - **Umuntu ($I \to 1$):** Ushintsha izinqumo, uyanqikaza, uthatha ubungozi.

- **$U_{\text{irreversible}}$ (Ukuhluka Okungabuyiselwa Emuva):**  
  Nakuba ukucela emuva (`Ctrl+Z`) kungenzeka ekukhiqizweni kwedijithali, ekukhiqizweni komzimba (upende olusetshenziswe kukanvesi, itshe elibaziwe, isenzo ekudlululisweni buqo) akukho indlela yokubuyela emuva. Lokhu **kungabuyiselwa emuva** kuwigama elengeziwe elidala "ukuhluka" (isimo esingashintshisani) emsebenzini.

### 🔎 Ukuhlaziywa Kwecala: I-AI "Umphumela Osheshayo" vs. Umuntu "Inqubo Eqinisekisiwe"

Isimo esilandelayo sibonisa ukuthi **Ithiyori Yenani Le-PoArt** isebenza kanjani ngokwenza futhi kungani ukukhiqizwa kwe-AI kuthola amanani aphansi ezingeni le-[PoArt].

#### Isimo A: Ukukhiqizwa Kokubona Ngemizuzwana 10 Nge-AI

- **Ubude ($\Delta t$):** $10$ imizuzwana (inqubo encane)
- **Amandla Omsebenzi ($P_{\text{labor}}$):** $1$ iyunithi (ukubhala imiyalo kuphela)
- **Isilinganiso Sentando ($I_{\text{agency}}$):** $0.01$ (akukho bungozi, azikho izindleko)
- **Ukungabuyiselwa Emuva ($U_{\text{irreversible}}$):** $0$ (kungabuyiselwa emuva / kungakopishwa)

**Umphumela:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Amazwana:** Noma umphumela uphelele; inani le-[PoArt] lisondela ku-$0$ ngoba akukho nqubo ebeshelwe futhi ayikho intando/ubungozi obubandakanyekile.

#### Isimo B: Ukukhiqizwa Komzimba Kwamahora 6 Ekudlululisweni Buqo

- **Ubude ($\Delta t$):** $6$ amahora ($21{,}600$ imizuzwana)
- **Amandla Omsebenzi ($P_{\text{labor}}$):** $0.5$ amayunithi (ukuqhubeka komzamo womzimba nowengqondo)
- **Isilinganiso Sentando ($I_{\text{agency}}$):** $0.9$ (ukushintsha izinqumo, ukuthatha ubungozi, ukukhetha okungabuyiselwa emuva)
- **Ukungabuyiselwa Emuva ($U_{\text{irreversible}}$):** $>0$ (izimpawu zomzimba azikwazi ukubuyiselwa emuva)

**Umphumela:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Amazwana:** Njengoba inqubo iba yinde futhi intando (ubungozi) ikhula, inani liqoqwa ngokuqoqanayo. Igama $U_{\text{irreversible}}$ lingumnikelo owengeziwe odala "ukuhluka" (isimo esingashintshisani) emsebenzini.

---

### ✅ Isiphetho: Inani Elihlanganiswe Nobufakazi (Proof-Bound Value)

Le thiyori ikhipha isimangalo senani le-[PoArt] ekubeni "ukuthanda" noma "indaba yemakethe" futhi ilihlanganisa ne-**qiniso lokukhiqizwa elingaqinisekiswa**.

1. **Ayikho Inqubo, Alikho Inani:**  
   I-AI ibhubhisa inqubo ngomphumela osheshayo ($t \to 0$). Njengoba iwindi lenqubo linciphayo, umphumela we-integral kumele unciphe:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Intando Nobungozi Bangaphindaphindwa:**  
   I-[PoArt] ayikali "isikhathi esichithiwe" kuphela kodwa nesigaba sangempela sokunquma, ubungozi, nezindleko kuleso sikhathi. Ukukhiqizwa okungathathi ubungozi (AI) kunani eliphansi:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Ukuhluka Kuyibufakazi Bomzimba, Kungesona Ukumaketha:**  
   Izimpawu ezingabuyiselwa emuva ekukhiqizweni komzimba (isibhakela sekanvesi, ucezu lwetshe) zingaphandle kwengqondo `Ctrl+Z` yedijithali. Lokhu kungabuyiselwa emuva ($U_{\text{irreversible}}$) kwenza umsebenzi uhluke nge-ontology.

> **🔐 ISIFINYEZO:** Nakuba ithiyori yenani ingase ibonakale inganqiniseki njengesilinganiso (noma ingqikithi yayo emhlabeni wangempela ingeke ilinganiswe ngokugcwele), injongo yale fomula ukubonisa ukumiswa nesikhombisa sokuguquguquka. Enkathini ye-AI, into enqabileyo akusona "isithombe" kodwa **umsebenzi ongaqinisekiswa, isikhathi, nentando.** I-[PoArt] ilinganisa lokhu kunqaba futhi ikubhale phansi nge-**Evidence Pack**.

### 🏛️ Ukubaluleka Komqondo "Wenjini"

Amathokheni avela ku-Pump.fun noma emapulatifomu afanayo ngokuvamile **"amathikithi okungena"** kuphela. **Injini Yophenyo ye-PoArt (PFE)**, nokho, **isigaba sengqondo yomthethosisekelo** esinquma ukuthi yiliphi ilungelo elileli thikithi elilivikela, indlela umsebenzi ozobhalwa ngayo kanye nendlela ubuciko/isayensi/ubuchwepheshe buzogcinwa ngayo.

> **Qaphela:** Isizathu esethula leli phrojekthi ku-Pumpfun ukuthi sasingenayo imali eyanele futhi asinabo abalandeli abanele. Ukusebenzisa idatha ekhona kwaba yisinyathelo esihle ngokweqhingasu, noma kungeyona ingqophelo ephezulu. Kungakhathaliseki isabelomali nezinsiza, ukuchaza ingqondo yale njini ku-GitHub kufakazela ukuthi iphrojekthi ayisona inkomba yezimali kuphela, kodwa umbono wesikhathi eside we-**ingqalasizinda yesofthiwe** kanye **nomtapo wolwazi wezwe ledijithali**.

---

## 🎨 UHLELO LWE-[PoArt] LOBUFAKAZI BOMSEBENZI (Proof of Art Protocol v1.0)

> **"Umculi Wangempela, Ukukhiqizwa Kwangempela, Inani Elingempela."**

Lolu hlelo **inqubo yokuvikela yemvelo nengqondo** ethuthukiswe ngokumelene nabaqambimanga abangaziwa abazungeze isimiso se-crypto, izithombe ze-AI ezikhiqizwa ngemizuzu 5, kanye namasiko "Pump & Dump".

---

## a) Kuyini I-[PoArt]? (Incazelo Yefilosofi Nobuchwepheshe)

**Ubufakazi Bobuciko [PoArt];** iwumaziso wokuqinisekisa wesiko oqinisekisa ukuthi inani ngemuva kwe-asethi ku-blockchain alisekelwe ekuqageleni, kodwa **emsebenzini womuntu**, **esikhathini**, kanye **namandla omzimba** angaqinisekiswa.

Njengoba i-Bitcoin ikhiqiza inani nge-*"Ugesi Namandla Weprosesa"* **(Ubufakazi Bomsebenzi)**, amaphrojekthi ahambisana ne-[PoArt] akhiqiza inani nge-*"Ikhono Lobuciko Nesikhathi Somuntu"*.

Isusa ubungozi *"Umthuthukisi uthengisile, iphrojekthi iphele"* emapulatifomu e-Pump.fun no-DEX; ngoba lapha inani alikho kukhodi, kodwa **ekuqhubekeni kokukhiqizwa**.

> **I-[PoArt] ayitsheli abahlanganyeli "Sithembe"; ithi "Nasi ubufakazi, bheka ngamehlo akho, qinisekisa ngesibalo sakho."**

---

## b) Izinga Lezinsika 5 Ze-[PoArt] (Izinsika 5 Zeqiniso)

Lezi zinto 5 zizihluzo ezingenakuphazanyiswa iphrojekthi okufanele idlule ukuthola uphawu lwe-[PoArt].

### 1) Ubufakazi Bobunikazi Buqo

- **Inkinga:** Umhlaba we-crypto ugcwele abasunguli abangaziwa (Devs) abanazo-ke izazisi ezingacacile abaqoqa imali futhi bashiye amaphrojekthi.
- **Isixazululo Se-[PoArt]:** Umkhiqizi ufakazela kungeyona incwadi yesazisi kuphela, kodwa **ukuba khona ngesikhathi sokukhiqizwa**. Lokhu kufaka izesesheni zokudlulisela buqo lapho ukuhlanganyela nomphakathi kwenzeka futhi izicelo ezithile ezisheshayo zenziwa, kungesona ividiyo ebeserekhode.  
  (Isibonelo, *"Bhala usuku lwanamuhla nenombolo yebulokhi yamanje ekhoneni elidla ngakwesokudla kwekanvesi"*)
- **Isilogeni:** *"Ama-Bots angadweba kodwa ama-bots awagcwali futhi awakwazi ukwenza improvisation."*

### 2) Ubufakazi Bomsebenzi Nenqubo

- **Inkinga:** Izithombe ze-AI (Artificial Intelligence) ezikhiqizwe ngemizuzwana 2 ezithola ukuphathwa okufanayo "jpeg" njengokudweba amafutha okwenziwe ezinyangeni 2 emhlabeni wedijithali.
- **Isixazululo Se-[PoArt]:** Inqubo "yokukhulelwa nokuzalwa" yomsebenzi ibhalwa phansi. Izinyathelo zokudweba, izigaba zokupenda, amahora aqoqiwe achithiwe nenqubo yomzimba umculi ahlangabezana nayo lapho edala umsebenzi kubhalwa phansi. Lokhu kwengeza **"Izindleko Zesikhathi"** kuthokeni. Kunzima kangakanani ukukhiqizwa kwe-asethi, kuqinile kangako inani layo.

### 3) Ubufakazi Benani Lobuhle

- **Inkinga:** Isiko "Lememe" eligxile kuhlekiso olusheshayo kuphela kuyilapho linganaki ubuhle nobujule bobuciko, okuholela kumaphrojekthi "Hype" esikhathi esifushane.
- **Isixazululo Se-[PoArt]:** Iphrojekthi kufanele ibe nezinga zobuciko zemfundo, ithiyori yombala, imithetho yokwakha, nolwazi lwezinto (Impasto, Texture, njll.). Okuqukethwe akufanele kukuhlekise kuphela; kufanele kukhuthaze ukumangala kubabukeli futhi kube **nenani lokuqoqwa**.

### 4) Ubuntsha Bomqondo

- **Inkinga:** Izinkulungwane zezinhlamvu zenja/ikati ezikopishiwe ngaphandle kobuciko.
- **Isixazululo Se-[PoArt]:** Iphrojekthi kufanele yakhe ibhuloho elisha elihlanganisa ubuciko, isayensi, ifilosofi noma ubuchwepheshe esakhiweni esinengqondo.  
  (Isibonelo, Ukuhlanganisa isithombe sakudala sikaDavid nedatha yemakethe ye-crypto; ukucubungula umqondo wokuthi ukuqonda komuntu "kuguquka ibe itshe" ngalokho futhi kusekelwe ngemithombo yesayensi.)  
  Umsebenzi akufanele ube ngumcimbi wokubona kuphela kodwa futhi inselelo yengqondo evusa ukucabanga mayelana **Nesayensi, Ifilosofi noma Ubuchwepheshe**.

> [!IMPORTANT]
> **Isibonelo Sesikhumbuzo (Umphumela We-Las Palmitas):** Esigodini se-Las Palmitas eMexico, esihlukuluzwa ubugebengu, izindlu ezingaphezu kuka-200 zaguqulwa zaba yinto enkulu yomchilo. Ngenxa yalo kungenelela kwangobuhle, amazinga obugebengu esigodini anciphile ngandlela thile, futhi abasha baqala ukuzibandakanya nobuciko kunokuba namaqembu obugebengu. Ukuguquka kwangobuhle kwabhala kabusha inhlonipho yabantu ngendawo yabo nomunye nomunye (Ukubambisana Komphakathi).
>
> **Okulindelwe:** Iphrojekthi engena ohlwini lwe-[PoArt] kufanele, njengasesibonelweni esingenhla, ibe nobudlelwano besizathu nomphumela womphakathi, wesayensi noma wefilosofi ngaphezu kobuhle bokukhanya nje. Njengoba isikhathi kuyiyona mpahla eyodwa engakwazi ukuthengwa ngemali, kulolu hlelo isikhathi kufanele sifakazelwe ngokusibeka njengesibambiso. Isisekelo somqondo wephrojekthi kufanele sibe namandla futhi sibe somhlaba wonke kangangokuthi noma esimweni se-CTO (Ukuthathwa Komphakathi) esingenzeka eminyakeni edlule, umphakathi ukwazi ukuqhubeka ngokuzimela namandla okusungula wephrojekthi ngokudla leli fa.

### 5) Intando Engeyona Ye-Algorithm

- **Inkinga:** Ukukhiqizwa kwedijithali okuphelele kodwa okungenayo umphefumulo oziphindaphindiyo.
- **Isixazululo Se-[PoArt]:** Intando eyingqayizivele yomuntu ongenza amaphutha, athathe ubungozi futhi abe nemizwa eguquguqukayo kufanele izwakale emsebenzini. Ukungaqiniseki ezibhakelweni zebrashi, ukusabela okungalindelekile kwezinto, nezinqumo ezisheshayo zomculi **Isiginesha Semvelo** esihlukanisa umsebenzi "Nokukhiqizwa Komshini".

---

## c) Inqubo Yokuqinisekisa Nokuvimbela Ukukhohlisa

Lolu hlelo luqinisekisa ukuthi iphrojekthi ihlala ithembekile futhi iphila kungeyona "ekuqaleni" kuphela kodwa "kuze kube phakade".

### 📦 Iphakethe Lobufakazi - Isibini Sedijithali

Ngemuva kwawo wonke umsebenzi oqinisekiswe nge-[PoArt] kukhona iphakethe ledatha elivaliwe elinesiginitsha sesikhathi abatshalizimali abangalidawnlowuda:

- **Ukurekhodwa Kwevidiyo RAW:** Ufilimu ongavuthiwe ongenako ukuqhawuka wesikhathi sokukhiqizwa.
- **Ukuhlaziywa Kwemethadatha:** Usuku lokudalwa kwefayela, ulwazi ngesixhobo esisetshenzisiwe nedatha yendawo.
- **Izinkomba Zomzimba:** Ubufakazi bokuthi umsebenzi ukhona emhlabeni womzimba  
  (Isibonelo, Iphephandaba lamanje noma idatha ye-blockchain yaleso sikhathi eduze nomsebenzi).

> *Iqiniso lokuhambelana:* Igama "elithi "iphakethe lobufakazi" lixhuma kuchungechunge **Iphakethe Lobufakazi → EvidenceRoot → NotarySeal** ezigabeni ezedlule; okusho ukuthi, ubuqotho bephakethe bumelwe ngophawu olungaqinisekiswa.

### 🔄 Ukuvuselelwa Kwezinsuku 365 (Uhlelo Lokuqhubeka)

- **Isici Soguquko:** Kumaphrojekthi e-crypto, "Dev" (Umthuthukisi) ukhipha ithokeni futhi ngokuvamile uyanyamalala ngemuva kwezinyanga 1-2 (Soft Rug). I-[PoArt] yenza lokhu kungenakwenzeka.
- **Umthetho:** Isimo "SomCuli Oqinisekisiwe" akuyona yempilo yonke. **Unyaka 1** kuphela osemthethweni.
- **Ukusebenza:** Umculi/umthuthukisi kufanele anikeze umphakathi **umsebenzi omusha obalulekile nongaqinisekiswa** zonke izinsuku 365.
- **Isibonelo Sesimo:** Uthule iphrojekthi ngo-2026. NgoJanuwari 2027, uhlelo lunikeza isexwayiso "Isikhathi Sobufakazi Siphele". Uma umculi engavezi umbukiso omusha, umsebenzi omusha womzimba noma ukuhlanganiswa kobuchwepheshe obusha, "Ibheji Yokwethembeka" yephrojekthi iyawa.
- **Umphumela:** Lolu hlelo luqinisekisa ukuthi **okuqukethwe akulahli ukufaneleka** nokuthi umtshalizimali akaze abe nolwesabo *"Ngabe umthuthukisi usekhona?"*. Iphrojekthi iba istudiyo esiphilayo.

### 🚩 Uhlelo Lwefulegi Ebomvu

**Esimweni sokukhohlisa okuthile okutholwe umphakathi noma ama-algorithms (ukusetshenziswa kwe-AI, umsebenzi ontshontshelwe, ividiyo ephazamisekile):**

1. Isitifiketi sibekwa uphawu ngokushesha njenge-**"VOID" (AKUNAMSEBENZI)**.
2. Amaphakethe obufakazi abhalwa uphawu esidlangalaleni njenge-**"Amanga"**.
3. Iphrojekthi ibekwa ohlwini olumnyama lwe-[PoArt]. Lokhu kuqinisa ukuthi emhlabeni owabiwe, **igama lihle yimali eyodwa**.

---

## d) Isiphetho: Akuyona I-Casino, Kodwa Imyuziyam

**I-Pump.fun Nezikhala Zokushintshanisa Ezingenalawulo (DEX) ngeshwa ziyi-casino manje; izibani ziyaphazima, wonke umuntu ulandela inzuzo esheshayo, futhi indlu (abaqambimanga) ihlale inqoba. Isizathu sokuqala iphrojekthi lapha ukuntuleka kwesabelomali eyanele kanye nokuba nendawo yokufinyelela izethameli ezikhona ngokudlulisela buqo.**

**I-[PoArt] iyinqaba eyakhiwe phakathi kwale casino.**

- 🎰 I-Casino isekelwe emidlalweni yamakhadi; thina sisekelwe **eqinisweni lomzimba**.
- 🃏 I-Casino ivulelwe ukukhohlisa; thina sivulelwe **ubufakazi obucacile**.
- ⏳ I-Casino yesikhashana; sigxile **ekuphakameni kobuciko nesayensi**.

**Ithokeni elisebenzisa lolu hlelo alikho nje "imali"; yimfuyo yedijithali equkethe ukugcwala, upende, ikhodi nefilosofi.**

---

## 🗳️ 6) UKUPHATHA NEREKHISTA LOMPHAKATHI

**Injongo yalesi sigaba ukuthi: ukuguqula izinga le-[PoArt] kusuka esigabeni "sokwethemba abantu" siye engqalasizindeni yomphakathi ezinzile nerekhista + ukuqinisekisa + ukubhekwa komphakathi.**

### 6.1 Irekhista Lomphakathi

- **Irekhista Lomphakathi:** Yonke idatha egunyaziwe ibhalwa ku-`ilhanart.org/registry` (noma ku-GitHub Registry).

**Ingqondo yerekhista (izinga elinconywayo - ngefomethi yendlela ye-JSON):**

Ngakunye ukubhaliswa okungena kurekhista kuthwala lezi zinsimu eziyinhloko ezingaqinisekiswa ezincane:

- **Ubunikazi Nesimo:**
  - `certificate_id` (inkomba efundekayo)
  - `status` (active / void)
  - `void_reason` (uma kusebenza)
  - `visibility` (private / masked / public)
  - `created_at` (uphawu lwesikhathi)

- **Isikhungo Esinikezayo:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Ulwazi Lomsebenzi:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (uma kungenzeka; ubunikazi obunomnyango wethokeni)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Idatha Yophenyo:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Ubufakazi Obuyi-Cryptographic:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Ukuphatha:**
  - `governance.decision`
  - `governance.veto_threshold`

Irekhista lingaba namazinga amabili:
- **1)** Inkomba efundeka abantu (uhlu lwewebhu / ukusesha / isihluzi)
- **2)** Isiboniso esifundeka yimishini (amarekhodi e-JSON; ukuqinisekisa kwe-PFE)

**Lokhu "kubhaliswa" kuba ngokungaqinisekiswa ngochungechunge Iphakethe Lobufakazi → EvidenceRoot → NotarySeal lwe-PFE. Irekhista lihlinzeka ngezinhloso zokuqinisekisa, hhayi "izimangalo".**

---

### 6.2 Ukukhansela Komphakathi Kwama-40% (Ukuphatha Nge-Token-Gated)

- **Ukukhansela Komphakathi Kwama-40%:** Ukuvota kuqala inyanga ngaphambi kokunikeza isimo; ukukhansela kwama-40% komphakathi **Onge-Token-Gated (oqinisekisiwe nge-Solana)** kuchitha isicelo.

**Ukuhamba kokuvota (inqubo ecacile elinconywayo):**
- **Iwindi lokufaka isicelo:** Iphrojekthi yomgqugquzeli ivula "ukubhaliswa komgqugquzeli we-PoArt" (amarekhodi omgqugquzeli abonakala esimweni "salinda").
- **Isikhathi sokubuyekeza:** Umphakathi uhlola ubufakazi izinsuku 30 (Iphakethe Lobufakazi + okurekhodiwe kokudlulisela buqo + imethadatha).
- **Ukuqinisekisa okune-token-gated:** Ukuvota kwenziwa ngezikhwama eziqinisekisiwe ze-Solana (isibonelo ukuba nomnikazi wethokeni/NFT ethile + isiginesha sekhwama).
- **Umthetho wokukhanselwa:** Uma ama-40% wamavoti **engukuphikisa (CHA / VETO)**, isicelo senqatshwa.
- **Ukucaca:** Umphumela wokuvota ugcinwa kurekhista njenge-"rekodi yokunquma" (usuku, inani, i-ID yesithombe).

---

### 6.3 Ukuvumelanisa Kwemethadatha (Ukuqondaniswa Nomhlaba Womzimba)

- **Ukuvumelanisa Kwemethadatha:** Idatha yobuchwepheshe kurekhista kufanele ilingane 100% ne-entity yomzimba.

**Ukuchaza ngobuchwepheshe "ukuqondana kwe-100%" (ukucaca okunconywayo):**
- **Ukuqondana okuphansi (kudingekayo):**
  - I-`asset.fingerprints.sha256/sha512` kurekhista kufanele **ifane** ne-hash yefayela elixoxwa ngalo.
  - Uma i-`proof.notary_seal` kurekhista ikhiqizwa kabusha (uma i-Evidence Pack ikhona), kufanele **ifane**.
- **Ukuqondana kwenkomba yomzimba (uhlobo lobufakazi):**
  - Umsebenzi womzimba + inkomba yosuku/ibulokhi eboniswe ekudlululisweni buqo nobufakazi obufanayo kufanele kuhambelane ne-Evidence Pack.
- **Ukuthobela ubumfihlo:**
  - Izinsimu ezifana ne-IP/indawo ekuboneni oku-`masked` zishicilelwa **ngokuya ngamazinga okufihla**.

---

### 6.4 Ukuphikisana Nokuchithwa

Irekhista akusona inqubo "yokuvuma" kuphela; **inqubo yokuhlola ephilayo ngokumelene nokukhohlis**a.

- Uma kuqalwa ukuphikisana, ukubhaliswa kungabekwa esimweni **"review" (ukubuyekeza)**.
- Uma kukhohliswa kutholakala, kubekwa uphawu njenge-`status: void` kunezizathu ezengeziwe:
  - `void_reason` (ukusetshenziswa kwe-AI / ukweba / ukuphazamisa, njll.)
  - `revoked_at` (isikhathi sokuchithwa)
- Umthombo wesinqumo sokuchithwa ucacile kurekhista:
  - ukuvota komphakathi / ikomidi eligunyaziwe / inothi yophenyo lwesayensi (okusebenzayo)

> **Lesi sigaba singumqondiso werekhista womqondo VOID esigabeni "Sohlelo Lwefulegi Ebomvu".**

---

### 6.5 Isibonelo Sokubhaliswa Kurekhista (Okufundeka Yimishini)
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
> *Qaphela: `asset.fingerprints.sha512` namanye amanani e-hash afinyeziwe ngezinhloso zokubonisa; ekusebenzeni kwangempela, kusetshenziswa izintambo ezigcwele ze-hexadecimal.*

---

## 7) 🔐 UPHAWU LOBUCHWEPHESHE (NOTARY SEAL)

I-algorithm yophawu olungaguquki olukhiqizwe yi-**Injini Yophenyo ye-PoArt (PFE) v1.0**:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Uhlelo Lwe-[PoArt] Lokubhalisa Kwedijithali Nobufakazi Besayensi (Beta v1.0)

> **"Isiko Sikhulu Kunomphahla. Vikela imisebenzi yakho namuhla, yithathe kususasa."**

---

## Kungani Umphakathi?

Ukuphepha kweqiniso kuvela ekucaceni. Ngombulelo kuhlelo lwethu **Lerekhista Lomphakathi**, noma ubani noma kuphi emhlabeni angaqinisekisa ukuthi ifayela liyiqiniso ngemizuzwana, ngaphandle kwesidingo sanoma yisiphi isikhungo.

---

## 🧩 Kungani "Amamojuli Okubonakalayo" Amaningi?

Lesi yingxenye ebaluleke kakhulu yekhodi (imenyu yokukheth okubonakala). Lezi zinketho zinikeza abasebenzisi amandla okulinganiselisisa **"Ubumfihlo vs. Ukucaca"**:

### 🔒 Okwangasese

- **Isimo:** Umculi akakafuni ukushicilela umsebenzi, kodwa ufuna ukuwubeka uphawu lwesikhathi ukufakazela "ngenza lokhu ngale suku".
- **Ikhodi Yenzani:** Ibhala idatha endaweni yokugcina idatha kodwa iphawula `visibility: "private"`. Kamuva lapho ubhala inqubomgomo "Yokufunda Komphakathi", ungakwazi ukufihla lawa marekhodi kubantu ngokusebenzisa `WHERE visibility = 'public'`.

### 🕶️ Okufihliwe

- **Isimo:** Umculi ufuna ukucaca kodwa uyesaba ukuthi ikheli lakhe lasekhaya (indawo ye-IP) lizotholakala.
- **Ikhodi Yenzani:** Imisebenzi `maskIP` ne-`maskLoc` isebenza ohlangothini lwe-JavaScript. Iguqula ikheli le-IP libe ifomethi `88.241.***.***`, indawo ibe ifomethi `***/TR`, futhi ithumela inguqulo ecetshisiwe endaweni yokugcina idatha.
- **Iqiniso Lobumfihlo:** Ukufihla kwenziwa kusiphequluli, i-Supabase ayiboni indawo yangempela. **Nokho:** Uma ama-API abanye njenge-ipapi.co esetshenziswa idatha yendawo, laba bahlinzeki babona ikheli le-IP ngesikhathi sesicelo.
- **Ukuvalela Emkhubeni Wokufihla:** Ukubalwa kwe-EvidenceRoot ne-NotarySeal kwenziwa ngedatha yophenyo efihlwe; ngakho ukuqinisekiswa kuhlala kunqunyiwe.

### 🌍 Umphakathi

- **Isimo:** Ukucaca okuphelele. Ngokuya ngamazinga e-[PoArt], kuphi, nini, kusuka kunethiwekhi yini umsebenzi ukhiqizwe kumenyezelwa ngokucacile.

---

## 💡 Ukusungulwa Kobuchwepheshe

I-PoArt ayisona uhlelo lokulayisha amafayela kuphela. Yinjini **"Yochungechunge Lokunakekelwa Kwesayensi"** eletha izinga elisha ngokuhlanganisa izigaba zobuchwepheshe ezintathu ezehlukene embizeni oyodwa.

**Isigaba esichazwa njenge-"njini" kulesi sigaba sihambisana nembumbulu Yenjini Yophenyo ye-PoArt (PFE) emagameni angaphambili.**

### 1) I-Hashing Yohlangothi Lweklayenti (Ubumfihlo Obuphakeme Kakhulu)

Amafayela akho omsebenzi wobuciko awagcinwa esiveni. Injini yethu esekwe kusiphequluli (uhlangothi lweklayenti) ibala i-hash (isifinyezo sedijithali) sefayela kukhompyutha yakho. Lokhu kugxivizo nemethadatha kuphela okuthunyelwa esiveni.

> **Iqiniso Lobumfihlo:** Ifayela lomsebenzi aligcinwa esiveni futhi livikelekile ngale ndlela. Nokho, idatha yophenyo (IP/indawo) yabelwana ngokuya nemodi yokubonakala ekhethiwe (okwangasese/okufihliwe/umphakathi).

### 2) Ukuhlanganiswa Kwedatha Yophenyo (Amandla Esayensi)

Okuningi kunophawu lwesikhathi olujwayelekile. Uhlelo luhlanganisa le datha "Ophawini Lokuqala" olulodwa:

- **Isifinyezo Sedijithali (SHA-512):** Izigxivizo zeminwe kusetshenziswa izinga lesifinyezo se-cryptographic (SHA-512) esizophuka uma nepikiseli elilodwa lomsebenzi lishintsha.
- **Indawo Nesikhathi:** Usuku ngokunembile kwemizuzwana eyikhulu, izwe, idolobha nedatha yesigodi sokuthengiselana.
- **Ubunikazi Besixhobo:** Uhlelo lokusebenza, isiphequluli kanye nohlobo lwesixhobo (ukuhlaziywa kwe-User-Agent).

---

## 🛡️ Izimo Zokusetshenziswa Nezinzuzo

Uma ungumculi, umbhali noma umdwebi, ukusho "Ngenze lokhu ngaphambili" akwanele; udinga ukufakazela.

**Umsebenzi owuvalela nge-PoArt:**

- **Ubufakazi Bezibalo:** Uma nepikiseli elilodwa lefayela lakho lishintsha, uhlelo luyazi. Ukuphazanyiswa akunakwenzeka.
- **Isisekelo Somthetho:** Lusuku luni, yidolobha elinjani, kusukela kusiphi isixhobo umsebenzi owuvalelwe phansi kubhalwa phansi.
- **Isitifiketi Ngokushesha:** Sikhiqiza **"Isitifiketi Sobunikazi Be-Asethi"** esikhethekile sakho ngemizuzwana, ngekhodi ye-QR futhi sivalelwe.

---

## ⚙️ Isakhiwo Sohlelo Nezici Zobuchwepheshe

Uhlelo luklanywe esakhiweni "Serverless", lugxile ekusebenzeni okuphezulu kanye namandla okwanda.

| Isigaba | Ubuchwepheshe | Incazelo |
|--------|-----------|-------------|
| **Ukubethela** | SHA-256 & SHA-512 | Isifinyezo se-cryptographic esineziqu ezimbili |
| **Idathabheyisi** | Supabase (PostgreSQL) | Isakhiwo sedatha ye-JSONB, izinqubomgomo ze-RLS |
| **Idatha Yophenyo** | ipapi.co API | Ukutathu kwe-IP/Indawo/Isikhathi |
| **Ukuboniswa** | html2canvas + jsPDF | Ukukhiqizwa kwe-PNG/PDF kohlangothi lweklayenti |
| **Frontend** | Vanilla JavaScript | Ukuncika kwe-framework ezero |
| **Ukuphepha** | I-Hashing yohlangothi lweklayenti | Ifayela aliyesiveni |

### Izici Ezibalulekile

| Isici | Imininingwane | Kubaqhudelani? |
|---------|-------|-----------------|
| **UI Hudula & Shiya** | Hudula futhi ushintshe ifayela, ukubuka ngokushesha | ❌ Akukho kwabaningi |
| **Ukuthumela Ngamafomethi Amaningi** | PNG, JSON, PDF - ukuthepha kanye | ⚠️ Okulinganiselwe |
| **Ukubuka Ngesikhathi Sangempela** | Ukubuka isitifiketi buqo | ❌ Lutho |
| **Izilawuli Zobumfihlo** | Izinketho Zokwangasese/Okufihliwe/Umphakathi | ❌ Lutho |
| **I-Hash Yohlangothi Lweklayenti** | Ifayela aliyesiveni | ✅ Kwabanye kuphela |
| **Imethadatha Yophenyo** | I-IP, indawo, isixhobo, isikhathi - konke ndawonye | ❌ Kuhlukanisiwe |
| **Ukuqinisekisa Nge-QR** | Ikhodi ye-QR yokuqinisekisa ngokushesha | ⚠️ Okulinganiselwe |
| **Ukunciphisa Isantya** | Ukuvikelwa kwe-spam (RLS + Iklayenti) | ❌ Akukho kwabaningi |

---

## 🗺️ Umfanekiso Wendlela: Ikusasa "Elingenathemba"

Inguqulo yamanje **(Beta v1.0)** ilungiselelwe ukunikeza abasebenzisi bokugcina isantya esiphakeme kakhulu, isixhumanisi esilula kanye nokufinyelela kwamahhala. Nokho, umbono wethu wokugcina ukushintshela esakhiweni lapho ngisho nomlawuli wedathabheyisi (thina) engenakuphazamisa khona.

### Isigaba 1: I-Beta (Iphila Manje)

- **Ingqalasizinda:** Idathabheyisi Yamafu (Supabase).
- **Injongo:** Isantya, ukususa imigoqo ye-UX (Okuhlangenwe Nakho Komsebenzisi) kanye nokuvumelaniswa. Ukunikeza ukuphepha "okungenakho ukuphazamisa".

### 🚀 Isigaba 2: (Izimfuneko Ze-Backend / Umsebenzi We-Edge)

Lesi sigaba sihlanganisa ukushintsha kusuka esakhiweni sokusebenza "ohlangothini lweklayenti" ngokugcwele kuye esakhiweni **"Segunya Lohlangothi Lweseva"** elinokuphepha okuningi futhi esingalawuleka.

| Into | Yini Eletha? | Isitaki Sobuchwepheshe | Okubalulekile |
|-------|---------------|------------|---------|
| **`INSERT` → Umsebenzi We-Edge** | Ukuvimbela i-spam + ukuphepha kwesihluthulelo se-API | Supabase Edge (Deno) | 🔴 Okuphakeme |
| **Isiginesha Sekhwama** | Ukuqinisekisa kwe-cryptographic | Solana Wallet Adapter | 🟡 Okuphakathi |
| **Isipele Se-IPFS/Arweave** | Ukungaguqulwa okwabiwe | IPFS SDK + Pinata | 🟢 Okuphansi |
| **Inqubo Yokuchithwa** | Ukuchitha isitifiketi esingamanga | Ukuvuselela Iskimu Se-DB | 🔴 Okuphakeme |
| **Ilogi Lokuhlola** | Irekhodi lombuzo wesayensi | Ithebula lamarekhodi elikhethekile | 🟡 Okuphakathi |
| **I-OpenTimestamps** | Iphini le-Bitcoin | OTS JavaScript | 🟢 Okuphansi |
| **Ukuhlanganiswa Kwe-DID** | Ubunikazi Obungalawulwa Phakathi | ION/Ceramic | 🟢 Okuphansi |

### Isigaba 3: Ukwabiwa Okuphelele (Isikhathi Eside)

| Isici | Injongo | ETA |
|---------|------|-----|
| **Irekhista Le-Blockchain** | Ukubhalisa ku-chain Ethereum/Solana | Q4 2026 |
| **Ukuphatha Kwe-DAO** | Ukuphatha komphakathi | Q1 2027 |
| **Ukusekela Ochungechungeni Oluningi** | Polygon, Arbitrum, Base | Q2 2027 |
| **Ukwamukelwa Ngokusemthethweni** | Ukusebenza ezinkantolo zaseTurkey | 2027-2028 |
| **I-API Yabathuthukisi** | Isiphetho se-API somphakathi | Q3 2026 |

---

## 📊 Ukuhlaziywa Kokuncintisana (Kubuyekeziwe)

I-PoArt imi ku-"Sweet Spot" egcwalisa ukuntuleka kwezixazululo ezikhona.

| Isici | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Izindleko** | 🆓 Mahhala | 🆓 | 💰 Okukhokhelwa | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI Hudula & Shiya** | ✅ Kulula Kakhulu | ❌ CLI | ⚠️ Okuphakathi | ⚠️ Okuphakathi | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Ukuthumela Ngamafomethi Amaningi** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Ukubuka Ngesikhathi Sangempela** | ✅ Buqo | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Izilawuli Zobumfihlo** | ✅ Izindlela 3 | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **I-Hash Yohlangothi Lweklayenti** | ✅ Ubumfihlo | ✅ | ❌ Layisha | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Imethadatha Yophenyo** | ✅ Okuphelele | ❌ | ❌ | ⚠️ Okulinganiselwe | ❌ | ⚠️ | ❌ | ⚠️ |
| **Ukuqinisekisa Nge-QR** | ✅ Ngokushesha | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Ukunciphisa Isantya** | ✅ RLS+Iklayenti | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Iphini Le-Blockchain** | 🔄 Umfanekiso Wendlela | ✅ Bitcoin | ✅ Ethereum | ✅ Okuningi | ✅ | ✅ | ✅ | ✅ |
| **Umthombo Ovulekile** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Ukusekela IsiTurkey** | ✅ Kwasemthonyameni | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Isihluthulelo:**
- ✅ : Ukusekela okuphelele / kuyatholakala
- ⚠️ : Okulinganiselwe / ezinhlelweni ezikhokhelwayo
- ❌ : Lutho / akusekelwe
- 🔄 : Kumfanekiso wendlela (kuthuthukiswa)
- 🆓 : Ngokuphelele mahhala
- 💰 : Kuyakhokhelwa / kudingeka ukubhalisa

### Ukuntuleka Kubaqhudelani, Amandla E-PoArt

| Okushiyekile | Abaqhudelani | PoArt |
|-------|-------------|-------|
| **Ubunzima Bokusetshenziswa** | CLI, ulwazi lwe-API, ikhwama liyadingeka | Hudula futhi ushintshe, kulungile ngothepha 3 |
| **Umgoqo Wezindleko** | Ukubhalisa $50-500/nyanga | 100% mahhala |
| **Ubumfihlo** | Ifayela lilayishwa esiveni | Uhlangothi lweklayenti, ifayela alizesiveni |
| **Idatha Yophenyo** | Uphawu lwesikhathi kuphela | I-IP, indawo, isixhobo, isikhathi - konke |
| **Ukusekela IsiTurkey** | Lutho noma okulinganiselwe kakhulu | Ukusekela ulimi lwendabuko |
| **Umthombo Ovulekile** | Ibhokisi elivaliwe | Lonke ikhodi livulekile ku-GitHub |

---

## 🧬 Isakhiwo Sedatha Lohlelo (JSON Schema)

**Yonke isitifiketi se-[PoArt] sinekhadimali lobunikazi le-JSON elithwelekayo nelingaqinisekiswa elikhiqizwe ngezinga elilandelayo.**

> **Qaphela:** Leli fomethi le-JSON lobunikazi yifomethi lesitifiketi elethulwa kubasebenzisi. Kumarekhodi erekhista, i-`registry.asset` isetshenziswa esikhundleni se-`identity.asset_data` (ukubeka imephu: `identity.asset_data` == `registry.asset`).
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

### Imisebenzi Ye-Hash Enqunyiwe
```javascript
// Imisebenzi Yokusiza: Guqula isifinyezo sibe i-hexadecimal string
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Guqula i-string ibe i-byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Ukukhiqizwa kwe-forensics string eqondile (v1.0: ukuhlela kwensimu okumisiwe + UTF-8 + isihlukanisi \n)
// Iqiniso Lesigaba 2: Ukushintshela ku-JSON eqondile nge-RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Inqubo Yokukhiqizwa Kwe-NotarySeal (Inqunyiwe Ngokuphelele)
```javascript
// 1. Ukubalwa Kwe-FileHash (uhlangothi lweklayenti)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Ukuqoqwa kwedatha yophenyo (ukusetshenziswa kophawu lwesikhathi olulodwa)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Ukukhiqizwa kophawu lwesikhathi olulodwa
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Uphawu lwesikhathi olufanayo
  };
  
  return { forensics, timestamp };
}

// 3. Ukwakhiwa Kwe-EvidenceRoot (ngokubethela okuqondile)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Ukukhiqizwa Kwe-NotarySeal (ukusetshenziswa kophawu lwesikhathi olufanayo)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Imisebenzi yokusiza yokufihla (ukusekela i-IPv4 ne-IPv6)
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

### Ukuhamba Kokuqinisekisa (Amazinga Amabili)

#### Quick Verify (Ukuqinisekisa Ngokushesha)
```javascript
// Qinisekisa i-hash yefayela kuphela (fulegi ebomvu esheshayo)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Thola kurekhista
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // Ukuqhathanisa i-hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Kwangempela - I-hash yefayela iyafana"
    };
  } else {
    return {
      valid: false,
      message: "❌ Amanga - Ifayela liphazanyisiwe"
    };
  }
}
```

#### Full Verify (Ukuqinisekisa Okuphelele)
```javascript
// Khiqiza kabusha futhi uqinisekise i-EvidenceRoot ne-NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Thola kurekhista
  const cert = await fetchFromRegistry(certificateId);

  // 1) Ukuqinisekisa Kwe-FileHash (fulegi ebomvu esheshayo)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Amanga - I-hash yefayela ayifani" };
  }

  // 2) Khiqiza kabusha i-EvidenceRoot (ngedatha yophenyo egcinwe kurekhista)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Ayifani - I-EvidenceRoot ayimi" };
  }

  // 3) Khiqiza kabusha i-NotarySeal (ngophawu lwesikhathi olufanayo + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Ayifani - I-NotarySeal ayimi" };
  }

  // Okukhethekayo: ESigabeni 2, qinisekisa futhi i-signer_sig nge-attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Isiginesha esingavumelekile" };

  return { valid: true, message: "✅ Kwangempela - Ukuqinisekisa okuphelele kuphumelele" };
}
```

> **Amaqiniso Abalulekile:**
> - **Quick Verify:** Iqinisekisa i-hash yefayela kuphela yokusetshenziswa okusheshayo.
> - **Full Verify:** Iqinisekisa zonke izigaba zohlelo (EvidenceRoot + NotarySeal).
> - Yonke imisebenzi ye-hash yenziwa ngokucacilelayo ngokubethela okumisiwe nezihlukanisi ezimisiwe.
> - **Izinga lokwenza kube ngukuqondile v1.0:** Ukuhlela kwensimu okumisiwe + ukubethela i-UTF-8 + isihlukanisi `\n`.
> - **Uhlelo Lwesigaba 2:** Ukushintshela ku-JSON eqondile nge-RFC 8785 (JCS - JSON Canonicalization Scheme).
> - Emkhubeni wokufihla, ukubalwa kwe-EvidenceRoot ne-NotarySeal kwenziwa ngedatha yophenyo efihlwe; ngakho ukuqinisekisa kuhlala kunqunyiwe.
> - Kusetshenziswa uphawu lwesikhathi olulodwa kuyo yonke inqubo (ophenyo + NotarySeal); ukunqunyelwa kuqinisekisiwe.
> - **Amagama ensimu yophenyo:** `ip_masked`, `location`, `device`, `timestamp` (ikhodi nerekhista kuyafana ngokuphelele).
> - **Indlela yerekhista:** `certificate.asset.fingerprints` (kuyafana ngokuphelele nekhodi yokuqinisekisa).
> - **signer_sig kurekhista:** Insimu `proof.signer_sig` iyadingeka ukuze Uqinisekise Okuphelele.
> - Inqubo Yesiginesha Yokusayina izovuswa eSigabeni 2 nge-Solana Wallet Adapter; ku-v1.0, ukuqinisekisa kungenzeka nge-`attestation_pubkey`.

---

## 📈 Izibalo Zokusetshenziswa (Izinhloso Ze-Q1 2026)

| Isilinganiso | Inhloso | Isimo |
|--------|--------|--------|
| **Isamba Sezitifiketi** | 1,000 | 🔄 Iyaqhubeka |
| **Abasebenzisi Abaphilayo** | 500 | 🔄 Iyaqhubeka |
| **Inani Lokuqinisekisa** | 5,000 | 🔄 Iyaqhubeka |
| **Isikhathi Sokusebenza** | 99.9% | ✅ Kuphila |
| **Isikhathi Semvumo Esimaphakathi** | <200ms | ✅ Okuhle Kakhulu |

---

## 🌍 Umphakathi Nokusekela

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Iwebhu:** [ilhanart.org](https://ilhanart.org)
- **I-imeyili:** galeri@ilhanart.org

---

## 🙏 Abanikeli

Uhlelo Lwe-PoArt luyaqhubeka nokuthuthuka ngemisebenzi evela emphakathini womthombo ovulekile.

**Ukuze unikele:**
1. Fork indawo yokugcina
2. Dala igatsha lesici (`git checkout -b feature/amazing-feature`)
3. Zibophezele (`git commit -m 'Add amazing feature'`)
4. Cindezela (`git push origin feature/amazing-feature`)
5. Vula Isicelo Sokudonsa

### 🛠️ Sidinga Ini Manje? (Ukubiza Usizo)

Uhlelo Lwe-PoArt lufuna abathuthukisi abanolwazi ezindaweni ezilandelayo zentuthuko **Yesigaba 2**:

* **Imisebenzi Yomaphethelweni Ye-Supabase:** Hambisa ukuvikelwa kwe-spam kwesehlakalo leseva.
* **I-Solana Web3.js:** Ukuhlanganiswa kwesiginesha sekhwama.
* **I-IPFS / Arweave:** Ukuhlanganiswa kwemisebenzi yokugcina nokuphina.

> Sicela uqale ingxoxo kuthebhu "Izinkinga" ngaphambi kokungeza isici.

---

**Uhlelo Lwe-[PoArt] Proof of Art v1.0**  
*"Isiko > Imali"*

## 🧾 Ilayisense

Ilayisense Ye-MIT © 2026 Ilhan Art Gallery Initiative

Bheka [![Ilayisense](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) ngezimo ezigcwele.

---

## 💬 Ukubongwa

![Inguqulo](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Ukuphepha](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Ipulatifomu](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![Ilayisense](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Leli phrojekthi lithuthukiswa yi-[Ilhan Art Gallery] initiative, futhi amakhodi womthombo wawo ayatholakala esidlangalaleni ngokucaca.**

**UHLELO V1.0 // KUVALELWE NGE-SHA-512**

*© 2026 İLHAN ART | WONKE AMALUNGELO AGODLIWE YEMISEBENZI YOBUCIKO, IZITHOMBE NEMIQONDO.*

---
