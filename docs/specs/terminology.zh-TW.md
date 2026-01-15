# 📚 術語與概念詞彙表
> **「理解本協定的語言，即理解其願景。」**

## ⚙️ PoArt 鑑證引擎 (PFE) v1.0：核心基礎設施

**PoArt 鑑證引擎 (PFE)** 代表 [PoArt] 協定背後的核心邏輯和技術運作的主要層級。這是將藝術作品的原始生產數據轉化為可驗證且不可變的**數位證據**的「鑑證引擎」。

### 🧩 為何稱為「PoArt 鑑證」？

- **PoArt（藝術證明）：** 引擎的焦點是將數位資產的價值綁定於**可證明的生產過程**，而非投機。
- **鑑證（司法驗證）：**
  - **技術定義：** 針對生產過程數據（筆觸、縮時攝影、日誌）未被操縱的驗證，採用演算法和記錄鏈方法。
  - **哲學層面：** 相對於人工智慧的「即時輸出」生產；將**人類的時間、努力和決策成本**的生產轉化為可衡量的真實性。

> 註：區塊鏈（例如 Solana）整合並非 PFE 的核心；而是作為驗證/註冊的單獨定義的**鏈錨定層**。

### 🛠️ v1.0 技術範疇

**PoArt 鑑證引擎 (PFE) v1.0** 建立在以下**三大支柱**之上，而非複雜的金融模型：

1. **雜湊與封印（Hashing & Sealing）：**  
   PFE 確定性地處理證據包中的所有元素（作品檔案、影片、JSON/日誌、簽名等），並生成唯一的 **NotarySeal** 值。

   **核心概念（v1.0）：**
   - **FileHash（作品指紋）：** 從作品檔案位元組生成的雜湊值。
   - **EvidenceRoot（證據包根）：** 代表證據包完整性的根摘要（Merkle root 或規範化清單雜湊）。
   - **NotarySeal（最終封印 / PFE 輸出）：** 從 EvidenceRoot + 時間 + 簽名組合生成的最終封印。

   **公式（對投資者清晰可見）：**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **規範化負載定義（v1.0）：**
   
   - **EvidenceRootPayload：**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload：**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > 註：作為 PFE 輸出的值指的是 **NotarySeal**。**SignerSignature** 機制將在第二階段（透過 Solana Wallet Adapter）啟動；目前 v1.0 使用系統自身的認證簽名。認證公鑰在註冊表的 `issuer.attestation_pubkey` 欄位中公佈。

2. **索引（Indexing）：**  
   記錄哪個錢包在何時為哪件作品提交了**勞動證明（Labor Proof）**；將其處理成透明且可查詢的記錄層。  
   *（此層可以是資料庫；鏈整合則另外定義為「鏈錨定層」。）*

3. **驗證（Verification）：**  
   當質疑作品的真實性時，PFE 重新處理原始證據；以數學確定性測試計算的 **EvidenceRoot / NotarySeal** 值是否與檔案記錄匹配。

---

### 🧮 PoArt 價值定理（The Value Theorem）

[PoArt] 協定將數位資產的價值（$V$）與主觀市場認知脫鉤，而與**生產過程的物理真實性**連結。

人工智慧（AI）透過即時給出結果（$t \to 0$）消滅了過程。[PoArt] 則將價值視為**時間、勞動和意志**成分的累積。

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### 變數定義

- **$\int dt$（過程累積）：**  
  價值不是即時的「輸出」（output）；而是在 $t_{\text{start}}$ 和 $t_{\text{end}}$ 之間累積的**過程**。當持續時間減少（AI 生產）時，積分結果趨近於 0。

- **$P_{\text{labor}}(t)$（瞬時勞動強度）：**  
  代表生產時刻消耗的心智和體力努力強度。當可證明的努力增加時，被積函數增大。  
  > 註：此項在實務上可透過「可測量/可證明的勞動訊號」進行標準化。

- **$I_{\text{agency}}(t)$（意志係數）：**  
  生產者承擔風險和做出決策的能力。取值介於 $0$ 與 $1$ 之間。
  - **AI（$I \approx 0$）：** 執行命令，不承擔風險，不付出代價。
  - **人類（$I \to 1$）：** 改變決定，猶豫不決，承擔風險。

- **$U_{\text{irreversible}}$（不可逆的獨特性）：**  
  在數位生產中可以撤銷（`Ctrl+Z`）；但在物理生產中（塗在畫布上的顏料、雕刻的大理石、直播中的手勢）無法回頭。這種**不可逆性**是在作品中創造「獨特性」（非同質化特徵）的額外項。

### 🔎 案例分析：AI「即時輸出」vs. 人類「證明過程」

以下情境展示了 **PoArt 價值定理**在實務中的運作方式，以及為何 AI 生產在 [PoArt] 標準中得分較低。

#### 情境 A：10 秒內使用 AI 生成視覺內容

- **持續時間（$\Delta t$）：** $10$ 秒（過程幾乎不存在）
- **勞動強度（$P_{\text{labor}}$）：** $1$ 單位（僅編寫命令）
- **意志係數（$I_{\text{agency}}$）：** $0.01$（無風險，無代價）
- **不可逆性（$U_{\text{irreversible}}$）：** $0$（可撤銷/可複製）

**結果：**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **評論：** 即使輸出完美；由於過程未經歷且不包含意志/風險，[PoArt] 價值趨近於 $0$。

#### 情境 B：直播中 6 小時的物理生產

- **持續時間（$\Delta t$）：** $6$ 小時（$21{,}600$ 秒）
- **勞動強度（$P_{\text{labor}}$）：** $0.5$ 單位（體力和心智努力的持續性）
- **意志係數（$I_{\text{agency}}$）：** $0.9$（改變決定、承擔風險、不可逆選擇）
- **不可逆性（$U_{\text{irreversible}}$）：** $>0$（物理痕跡無法撤銷）

**結果：**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **評論：** 隨著過程延長和意志（風險）增加，價值累積增長。$U_{\text{irreversible}}$ 項是在作品中創造「獨特性」（非同質化特徵）的額外貢獻。

---

### ✅ 結論：價值與證明的綁定（Proof-Bound Value）

此定理將 [PoArt] 的價值主張從「喜好」或「市場敘事」轉化為**可證明的生產真實性**。

1. **無過程則無價值：**  
   AI 在即時輸出（$t \to 0$）中消滅過程。當過程視窗縮小時，積分結果因數學必然性而減小：
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **意志和風險是乘數：**  
   [PoArt] 不僅測量「消耗的時間」；還測量該時間內的真實決策、風險和代價層次。不承擔風險（AI）的生產價值較低：
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **獨特性是物理證明，而非行銷：**  
   物理生產中的不可逆痕跡（畫布筆觸、大理石裂痕）超出數位世界的 `Ctrl+Z` 邏輯。這種不可逆性（$U_{\text{irreversible}}$）在本體論上使作品獨特化。

> **🔐 總結：** 雖然價值定理在測量上看似不確定（現實生活中無法 100% 精確測量），但此公式的目的是展示變數的結構和方向。在 AI 時代稀缺的不是「圖像」，而是**可證明的勞動、時間和意志**。[PoArt] 測量這種稀缺性並透過 **Evidence Pack** 進行認證。

### 🏛️ 「引擎」（Engine）概念的重要性

從 Pump.fun 或類似平台推出的代幣，通常只是**「准入票證」**。**PoArt 鑑證引擎 (PFE)** 則是決定該票證保護哪些權利、如何記錄勞動、以及如何永久保存藝術/科學/技術的**憲法邏輯層**。

> **註：** 我們在 Pump.fun 上啟動此專案的原因是我們沒有足夠的流動性和足夠的追隨者數量。利用現有數據，儘管策略上不是最優質，但可以說是最正確的舉動。無論預算和條件如何，在 GitHub 上定義此引擎的邏輯，證明了該專案不僅是金融投機，而是長期的**軟體基礎設施**和**數位國家圖書館**願景。

---

## 🎨 [PoArt] 勞動證明協定（Proof of Art Protocol v1.0）

> **「真正的藝術家，真正的生產，真正的價值。」**

此協定是針對包圍加密生態系統的匿名詐騙者、5 分鐘內生成的人工智慧圖像，以及「拉高出貨」（Pump & Dump）文化而開發的**生物和智識防禦機制**。

---

## a) [PoArt] 是什麼？（哲學與技術定義）

**藝術證明 [PoArt]；** 是一種機構驗證標準，確保區塊鏈上資產背後的價值不是基於投機，而是基於可驗證的**人類勞動**、**時間**和**體力能量**。

正如比特幣透過*「電力和處理器能力」* **(工作量證明)** 創造價值；[PoArt] 相容專案也透過*「藝術才能和人類時間」*創造價值。

消除了 Pump.fun 和 DEX 平台上的*「開發者（Dev）拋售，專案結束」*風險；因為這裡的價值不在程式碼中，而在**生產的持續性**中。

> **[PoArt] 不會對參與者說「相信我們」；而是說「這裡是證據，用你的眼睛看，用你的數學驗證」。**

---

## b) [PoArt] 五大標準（The 5 Pillars of Truth）

這 5 項是專案獲得 [PoArt] 印章必須通過的不可操縱過濾器。

### 1) 即時身份證明（Live Identity Proof）

- **問題：** 加密世界充斥著身份不明的匿名創始人（Dev），他們收錢後放棄專案。
- **[PoArt] 解決方案：** 生產者不僅證明身份證，還證明**生產時刻的存在**。這包括與社群互動並滿足即時特定要求的直播環節，而非預錄影片。  
  （例如：*「在畫布右角寫上今天的日期和當前區塊號」*）
- **格言：** *「機器人可以繪畫，但機器人不會流汗，也無法即興創作。」*

### 2) 勞動與過程證明（Labor & Process Proof）

- **問題：** 2 秒生成的 AI（人工智慧）圖像與 2 個月完成的油畫在數位世界中被視為相同的「jpeg」。
- **[PoArt] 解決方案：** 記錄作品的「懷孕和分娩」過程。記錄草圖階段、顏料層次、累積消耗的小時數，以及藝術家在創作過程中經歷的物理過程。這為代幣添加了**「時間成本」（Time Cost）**。資產的生產越困難，其價值越堅實。

### 3) 美學價值證明（Aesthetic Value Proof）

- **問題：** 「迷因」文化忽視美學和藝術深度，僅關注即時喜劇，導致短命的「炒作」專案。
- **[PoArt] 解決方案：** 專案應具備學術藝術標準、色彩理論、構圖規則和材料知識（Impasto、紋理等）。內容不應僅僅逗樂；應在觀眾中引起欽佩並具有**收藏價值**。

### 4) 概念創新（Conceptual Novelty）

- **問題：** 數千個互相複製、缺乏創造力的狗/貓幣。
- **[PoArt] 解決方案：** 專案應在有意義的結構中結合藝術、科學、哲學或技術，建立新的橋樑。  
  （例如：將古典大衛雕像與加密市場數據結合；透過此處理人類感知「石化」的概念，並能用科學資源證實。）  
  作品不僅是視覺盛宴；同時也是對**科學、哲學或技術**的智識挑戰。

> [!IMPORTANT]
> **參考範例（Las Palmitas 效應）：**  
> 在墨西哥與犯罪鬥爭的 Las Palmitas 社區，200 多棟房屋被轉化為巨大的彩虹盛宴。此美學干預後，社區犯罪率在一定程度上下降，年輕人開始關注藝術而非幫派。美學變化重新編碼了人們對環境和彼此的尊重（社會凝聚力）。
>
> **期望：** 將進入 [PoArt] 列表的專案；如同上述範例，應包含超越純視覺美學的社會學、科學或哲學因果關係。由於金錢無法購買的唯一資產是「時間」，在此協定中，時間必須作為抵押品進行質押並證明。專案的概念基礎應該如此強大和普遍；以至於多年後即使可能發生 CTO（社群接管）情境，社群也能繼承此遺產，自主地延續專案的創新潛力。

### 5) 非演算法意志（Non-Algorithmic Agency）

- **問題：** 完美但無靈魂、重複彼此的數位生產。
- **[PoArt] 解決方案：** 人類能犯錯、承擔風險並經歷情感波動的獨特意志應在作品中被感受到。筆觸中的不確定性、材料的意外反應和藝術家的即時決策，是將作品與「機器生產」區分開來的**生物簽名**。

---

## c) 驗證與防偽機制

此系統確保專案不僅在「開始時」，而且「永遠」保持可信賴和活躍。

### 📦 證據包（Evidence Pack - The Digital Twin）

每件 [PoArt] 認證作品背後都有一個加密和時間戳記的數據包，供投資者下載：

- **RAW 影片記錄：** 生產時刻的連續原始影像。
- **元資料分析：** 檔案創建日期、使用的裝置資訊和位置數據。
- **物理參考：** 證明作品在物理世界中存在的證據  
  （例如：作品旁邊的當前報紙或當時的區塊鏈數據）。

> *一致性註記：* 「證據包」表述連接到先前部分的 **Evidence Pack → EvidenceRoot → NotarySeal** 線路；即包的完整性可透過可驗證的封印表示。

### 🔄 365 天更新（The Sustainability Protocol）

- **革命性特徵：** 在加密專案中，「Dev」（開發者）將代幣推向市場，通常在 1-2 個月後消失（軟性拉高出貨）。[PoArt] 使這不可能。
- **規則：** 「Verified Artist」（認證藝術家）身份不是終身的。僅有效 **1 年**。
- **運作：** 藝術家/開發者每 365 天必須向社群提交**新的、重大且可證明的作品**。
- **範例情境：** 您在 2026 年啟動專案。2027 年 1 月，系統發出「證明期限已過」警告。如果藝術家未提交新展覽、新物理作品或新技術整合，專案的「信任徽章」將下降。
- **結果：** 此系統確保**內容永不過時**，投資者無需擔心*「開發者還在嗎？」*。專案變成一個活躍的工作室。

### 🚩 紅旗（Red Flag Protocol）

**當社群或演算法偵測到任何欺詐行為（AI 使用、盜竊作品、操縱影片）時：**

1. 證書立即標記為 **「無效」（VOID）**。
2. 證據包公開標記為 **「假貨」**。
3. 專案被列入 [PoArt] 黑名單。這鞏固了在去中心化世界中**聲譽是唯一貨幣**的事實。

---

## d) 結論：非賭場，而是博物館

**Pump.fun 和去中心化交易所（DEX）目前遺憾地是賭場；燈光閃爍，每個人都追求快速獲利，莊家（詐騙者）總是贏。我們在此啟動專案的原因是我們沒有足夠的預算，以及透過直播接觸現有觀眾。**

**[PoArt] 是建在這個賭場中心的堡壘。**

- 🎰 賭場依賴紙牌遊戲；我們依賴**物理真實性**。
- 🃏 賭場易受欺騙；我們對**透明證據**開放。
- ⏳ 賭場是暫時的；我們專注於**藝術和科學的永恆性**。

**使用此協定的代幣不僅是「幣」；它是背後包含汗水、顏料、程式碼和哲學的數位股票。**

---

## 🗳️ 6) 治理與公共註冊（Governance & Public Registry）

**本節的目的是：將 [PoArt] 標準從「對人的信任」層面提升，透過記錄 + 驗證 + 社群監督轉化為可持續的公共基礎設施。**

### 6.1 公共註冊（Public Registry）

- **公共註冊：** 所有批准的數據記錄在 `ilhanart.org/registry`（或 GitHub Registry）位址。

**記錄邏輯（建議標準 - JSON 路徑格式）：**

進入註冊的每條記錄至少包含以下可驗證的核心欄位：

- **身份與狀態：**
  - `certificate_id`（可讀參考）
  - `status`（active / void）
  - `void_reason`（如有）
  - `visibility`（private / masked / public）
  - `created_at`（時間戳記）

- **發行機構：**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **作品資訊：**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet`（如可能；用於代幣持有者身份）
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **鑑證數據：**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **密碼學證明：**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **治理：**
  - `governance.decision`
  - `governance.review_notes`

註冊可能有兩層：
- **1)** 人類可讀索引（網頁列表/搜尋/篩選）
- **2)** 機器可讀清單（JSON 記錄；用於 PFE 驗證）

**這裡的「記錄」透過 PFE 的 Evidence Pack → EvidenceRoot → NotarySeal 鏈變得可驗證。註冊提供驗證目標，而非「主張」。**

---

### 6.2 PoArt Verified 申請流程

**PoArt Verified 申請由伊爾汗藝術畫廊根據 5 項 PoArt 標準進行評估。社群反饋會被考慮，但最終決定屬於策展團隊。決定以透明方式解釋並記錄在 ilhanart.org/registry。**

#### 申請流程

**申請：**
- 藝術家/專案提交 PoArt Verified 申請
- 準備證據包（影片記錄、元資料、直播連結）
- 將申請發送至伊爾汗藝術畫廊

**審查（30 天）：**
- 畫廊團隊詳細審查證據包
- 檢查所有 5 項 PoArt 標準：
  1. 即時身份證明
  2. 勞動與過程證明
  3. 美學價值證明
  4. 概念創新
  5. 非演算法意志
- 與藝術家面談（選擇性）

**社群諮詢：**
- 證據包在申請過程中公開分享
- 代幣持有者（最少 10,000 $CULTURE）特別可提供建議
- **所有反饋在審查過程中都會被考慮**
- **但最終決定取決於策展評估**

**決定：**
- 畫廊批准或拒絕申請
- 以透明方式解釋決定理由
- 如獲批准 → PoArt Verified 徽章
- 如被拒絕 → 6 個月後可重新申請

**透明度：**
- 所有申請和決定記錄在 ilhanart.org/registry
- 決定記錄公開發布：
  - 申請日期
  - 審查過程摘要
  - 決定（批准/拒絕）
  - 決定理由（簡要說明）
  - 社群反饋摘要（匿名）

#### 為何採用策展決定？

**品質控制：**  
PoArt Verified 身份是具有高標準的徽章。策展評估確保維護這些標準。

**防止投機操縱：**  
Pump.fun 代幣無法實現完全鏈上治理（例如：Realms、DAO 投票）。鏈下投票系統易受鯨魚操縱和協同攻擊。策展決定消除了這種風險。

**營運效率：**  
快速明確的決策過程，而非複雜的投票機制。藝術家在 30 天內得到結果。

**社群參與：**  
社群反饋完全被考慮並影響決策過程。但最終決定屬於免受操縱的策展團隊。

**未來：**  
當專案成熟（2027+）時，社群諮詢機制可以加強。但策展標準保護是永久性的。

---

### 6.3 代幣效用（Token Utility）

**$CULTURE 代幣持有者獲得的權益：**

**1. 畫廊活動優先准入：**
- 伊爾汗藝術畫廊實體展覽開幕
- 藝術家聚會和工作室參觀
- 特殊收藏觀賞

**2. PoArt 註冊完整准入：**
- 所有認證作品的詳細記錄
- 證據包的完整版本
- 鑑證驗證工具

**3. NFT 鑄造優先權：**
- PoArt Verified 作品鑄造為 NFT 時的白名單准入
- 早期鑄造機會
- 特殊收藏 NFT

**4. 諮詢投票：**
- PoArt Verified 申請的諮詢權
- 准入社群反饋管道
- 參與治理討論

**5. 獨家內容：**
- 工作室幕後內容
- 藝術家訪談和過程影片
- 技術文件准入

**註：**  
代幣持有者投諮詢票（advisory vote）。最終決定屬於策展團隊。這種結構是為了防止鯨魚操縱和投機攻擊而選擇的。沒有質押獎勵，因為我們尋求長期文化參與者，而非短期傭兵資本。

---

### 6.4 元資料同步（Metadata Sync）

- **元資料同步：** 註冊中的技術數據必須與物理實體 100% 匹配。

**技術上定義「100% 匹配」（建議明確性）：**

- **最低匹配（必需）：**
  - 註冊中的 `asset.fingerprints.sha256/sha512` 與手頭檔案的雜湊值必須**完全相同**。
  - 重新生成註冊中的 `proof.notary_seal`（如有證據包）時必須**完全相同**。

- **物理參考匹配（證明類型）：**
  - 直播中展示的物理作品 + 日期/區塊參考等證據應與證據包一致。

- **隱私合規：**
  - 在 `masked` 可見性下，IP/位置等欄位應**符合遮罩標準**發布。

---

### 6.5 爭議、審查與撤銷（Dispute & Revocation）

註冊不僅是「批准」機制；也是**對抗欺詐的活性監督**機制。

- 提出爭議時，記錄可轉入 **「審查」** 模式。
- 如偵測到欺詐，標記為 `status: void` 並添加理由：
  - `void_reason`（AI 使用/盜竊/操縱等）
  - `revoked_at`（撤銷時間）
- 撤銷決定的來源在註冊中清楚可見：
  - 策展審查/社群爭議/鑑證分析註記（適用者）

> **此部分是「紅旗協定」部分中 VOID 概念在註冊上的對應。**

---

### 6.6 範例註冊記錄（機器可讀）
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

> *註：`asset.fingerprints.sha512` 和其他雜湊值為展示目的而縮短；實際應用中使用完整長度的十六進制字元串。*

---

## 7) 🔐 技術封印（NOTARY SEAL）

**PoArt 鑑證引擎 (PFE) v1.0** 生成的不可動搖封印演算法：

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] 數位公證與鑑證協定（Beta v1.0）

> **「文化大於資本。今天保護您的作品，帶到明天。」**

---

## 為何公開？

真正的安全來自透明度。透過我們的 **公共註冊（Public Registry）** 系統，世界任何地方的人都可以在幾秒鐘內驗證手中檔案是否為原創，無需任何機構。

---

## 🧩 為何有多個「可見性模組」？

這是程式碼最關鍵的部分（可見性選擇選單）。這些選項讓使用者能夠平衡**「隱私 vs. 透明度」**：

### 🔒 私密（Private）

- **情境：** 藝術家尚未想發布作品，但想加蓋時間戳記證明「我在這個日期創作了這個」。
- **程式碼執行：** 將數據寫入資料庫但標記 `visibility: "private"`。未來編寫「Public Read」政策時，透過 `WHERE visibility = 'public'` 可以向公眾隱藏這些記錄。

### 🕶️ 遮罩（Masked）

- **情境：** 藝術家想要透明度，但擔心家庭住址（IP 位置）被發現。
- **程式碼執行：** JavaScript 端執行 `maskIP` 和 `maskLoc` 函數。將 IP 位址轉換為 `88.241.***.***` 形式，位置轉換為 `***/TR` 形式，並將審查後的版本發送到資料庫。
- **隱私註記：** 遮罩在瀏覽器中完成，Supabase 不會看到真實位置。**但是：** 如果位置數據使用 ipapi.co 等第三方 API，這些提供者在請求時會看到 IP 位址。
- **遮罩模式下的封印：** EvidenceRoot 和 NotarySeal 計算使用遮罩後的鑑證數據進行；因此驗證保持確定性。

### 🌍 公開（Public）

- **情境：** 完全透明。根據 [PoArt] 標準，作品的製作地點、時間和網路清楚聲明。

---

## 💡 技術創新

PoArt 不僅是檔案上傳系統。它是在一個坩堝中融合三種不同技術層、帶來新標準的**「鑑證監管鏈」（Forensic Chain of Custody）**引擎。

**本節作為「引擎」解釋的層對應於先前術語中的 PoArt 鑑證引擎 (PFE) 核心。**

### 1) 用戶端雜湊（Client-Side Hashing）（最大隱私）

您的作品檔案永遠不會上傳到伺服器。我們的引擎在瀏覽器端（Client-side）運行，在您自己的電腦上計算檔案的雜湊值（數位摘要）。僅將此指紋和元資料發送到伺服器。

> **隱私註記：** 作品檔案不上傳到伺服器，以此方式受到保護。但鑑證數據（IP/位置）根據所選可見性模式（private/masked/public）共享。

### 2) 鑑證數據融合（Forensic Data Fusion）（鑑證能力）

遠超普通時間戳記（Timestamp）。系統將以下數據融合在單一「創世封印」中：

- **數位摘要（SHA-512）：** 使用密碼學摘要（SHA-512）標準，即使作品的一個像素改變也會破壞的數位指紋。
- **位置與時間：** 進行操作的毫秒精確日期、國家、城市和地區數據。
- **裝置身份：** 作業系統、瀏覽器和裝置類型（User-Agent 分析）。

---

## 🛡️ 使用場景與效益

如果您是藝術家、作家或設計師，僅說「我早就做過這個」是不夠的，您需要證明。

**使用 PoArt 封印的作品：**

- **數學證明：** 即使檔案的一個像素改變，系統也會偵測到。操縱不可能。
- **法律依據：** 記錄作品在哪個日期、哪個城市、哪個裝置上封印。
- **即時證書：** 幾秒鐘內生成專屬、帶 QR 碼和封印的 **「資產身份證書」**。

---

## ⚙️ 系統架構與技術特性

系統在「無伺服器」（Serverless）架構上設計，專注於高效能和可擴展性。

| 層級 | 技術 | 說明 |
|------|------|------|
| **密碼學** | SHA-256 & SHA-512 | 雙層密碼學摘要 |
| **資料庫** | Supabase (PostgreSQL) | JSONB 資料結構、RLS 政策 |
| **鑑證數據** | ipapi.co API | IP/位置/時間三元組 |
| **渲染** | html2canvas + jsPDF | 用戶端 PNG/PDF 生成 |
| **前端** | Vanilla JavaScript | 零框架依賴 |
| **安全性** | 用戶端雜湊 | 檔案永不上傳到伺服器 |

### 突出特點

| 特性 | 詳情 | 競爭對手有嗎？ |
|------|------|---------------|
| **拖放 UI** | 拖放檔案，即時預覽 | ❌ 大多數沒有 |
| **多格式匯出** | PNG、JSON、PDF - 一鍵完成 | ⚠️ 有限 |
| **即時預覽** | 證書即時預覽 | ❌ 沒有 |
| **隱私控制** | Private/Masked/Public 選項 | ❌ 沒有 |
| **用戶端雜湊** | 檔案永不到達伺服器 | ✅ 僅少數有 |
| **鑑證元資料** | IP、位置、裝置、時間 - 全部 | ❌ 片段化 |
| **QR 驗證** | 即時驗證 QR 碼 | ⚠️ 受限 |
| **速率限制** | 垃圾郵件保護（RLS + Client） | ❌ 大多數沒有 |

---

## 🗺️ 路線圖：「無信任」未來

當前版本 **(Beta v1.0)** 針對為終端使用者提供最大速度、簡易介面和免費訪問而最佳化。但我們的最終願景是過渡到資料庫管理員（我們）也無法干預的結構。

### 第一階段：Beta v1.0（目前上線）

**基礎設施：**
- 雲端資料庫（Supabase）
- 鏈下註冊（PostgreSQL + IPFS 備份）
- 畫廊自我認證（中心化但透明）

**代幣：**
- 平台：Pump.fun
- 流動性：Raydium（自動）
- 治理：僅諮詢（社群諮詢）

**目標：**
- 速度，消除 UX 障礙
- 提供「無摩擦」安全
- 建立社群

**代幣效用（v1.0）：**
- 畫廊活動優先准入
- PoArt 註冊查看
- 諮詢投票權

---

### 🚀 第二階段：去中心化權威（2026 Q2-Q4）

此階段涵蓋系統從完全「用戶端」運作結構過渡到更安全和去中心化的結構。

| 特性 | 帶來什麼？ | 技術堆疊 | 預計時間 |
|------|----------|----------|---------|
| **邊緣函數 INSERT** | 垃圾郵件阻止 + API 金鑰安全 | Supabase Edge (Deno) | Q2 2026 |
| **錢包簽名** | 去中心化身份 | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave 備份** | 去中心化存檔 | IPFS SDK + Pinata | Q3 2026 |
| **撤銷機制** | 假證書撤銷 | 資料庫架構更新 | Q2 2026 |
| **稽核日誌** | 鑑證查詢記錄 | 自訂日誌表 | Q3 2026 |
| **OpenTimestamps** | 比特幣錨定 | OTS JavaScript | Q4 2026 |

**代幣治理（v2.0）：**
- 社群代表選舉（前 90 天）
- 多重簽名操作錢包控制
- 加權諮詢投票（有鯨魚上限）

**不可變性：**
- 使用 IPFS 雜湊值的註冊備份
- 比特幣時間戳記錨定
- 跨鏈驗證準備

---

### 第三階段：完全去中心化（2027+）

| 特性 | 目標 | 預計時間 |
|------|------|---------|
| **鏈上註冊** | Solana 鏈上記錄 | Q1 2027 |
| **增強代幣效用** | NFT 鑄造、進階功能 | Q1 2027 |
| **多鏈支援** | Ethereum、Polygon、Base | Q2 2027 |
| **DID 整合** | 去中心化身份 | Q3 2027 |
| **社群治理** | 強化諮詢系統 | Q4 2027 |
| **法律認可** | 土耳其法院有效性 | 2027-2028 |
| **開發者 API** | 公共 API 端點 | Q3 2027 |

**治理演化：**
- v3.0：混合模式（策展 + 社群加權）
- 2028+：完全社群治理（選擇性）
- 策展品質控制永遠保留

---

## 🧬 協定數據結構（JSON Schema）

**每個 [PoArt] 證書都有以下標準產生的可攜帶且可驗證的 JSON 身份證。**

> **註：** 此 Identity JSON 格式是呈現給使用者的證書格式。在註冊記錄中，使用 `registry.asset` 而非 `identity.asset_data`（對應：`identity.asset_data` == `registry.asset`）。
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

---

## 🔬 技術深度：封印演算法

### 確定性雜湊函數
```javascript
// 輔助函數：將摘要轉換為十六進制字串
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// 將字串轉換為位元組陣列
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// 規範化鑑證字串生成（v1.0：固定欄位順序 + UTF-8 + \n 分隔符）
// 第二階段註記：將過渡到 RFC 8785 (JCS) 的規範化 JSON
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal 生產過程（完全確定性）
```javascript
// 1. FileHash 計算（用戶端）
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. 鑑證數據收集（單一時間戳記使用）
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // 單一時間戳記生成
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // 相同時間戳記
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot 建立（使用規範化編碼）
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal 生成（使用相同時間戳記）
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// 遮罩輔助函數（IPv4 和 IPv6 支援）
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4 檢查
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 或未知格式
  return "***";
}
```

### 驗證流程（兩級）

#### 快速驗證（Quick Verify）
```javascript
// 僅檢查檔案雜湊值（快速紅旗）
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // 從註冊取得
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // 雜湊比較
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ 原創 - 檔案雜湊值匹配"
    };
  } else {
    return {
      valid: false,
      message: "❌ 假貨 - 檔案已被操縱"
    };
  }
}
```

#### 完全驗證（Full Verify）
```javascript
// 重新生成並驗證 EvidenceRoot 和 NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // 從註冊取得
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash 檢查（快速紅旗）
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ 假貨 - 檔案雜湊值不匹配" };
  }

  // 2) 重新生成 EvidenceRoot（使用註冊中儲存的鑑證）
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ 不匹配 - EvidenceRoot 不成立" };
  }

  // 3) 重新生成 NotarySeal（使用相同時間戳記 + signer_sig）
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ 不匹配 - NotarySeal 不成立" };
  }

  // 選擇性：在第二階段還用 attestation_pubkey 驗證 signer_sig
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ 簽名無效" };

  return { valid: true, message: "✅ 原創 - 完全驗證通過" };
}
```

> **重要註記：**
> - **快速驗證：** 僅檢查檔案雜湊值以供快速使用。
> - **完全驗證：** 驗證協定的所有層級（EvidenceRoot + NotarySeal）。
> - 所有雜湊操作以確定性方式完成，使用固定編碼和分隔符。
> - **v1.0 規範化標準：** 固定欄位順序 + UTF-8 編碼 + `\n` 分隔符。
> - **第二階段計劃：** 使用 RFC 8785 (JCS - JSON Canonicalization Scheme) 過渡到規範化 JSON。
> - 在遮罩模式下，EvidenceRoot 和 NotarySeal 計算使用遮罩鑑證完成。
> - 整個過程中使用單一時間戳記（鑑證 + NotarySeal）；確保確定性。
> - **鑑證欄位名：** `ip_masked`、`location`、`device`、`timestamp`（程式碼和註冊完全相容）。
> - **註冊路徑：** `certificate.asset.fingerprints`（與驗證程式碼完全相容）。
> - **註冊中的 signer_sig：** `proof.signer_sig` 欄位是完全驗證所必需的。
> - SignerSignature 機制將在第二階段透過 Solana Wallet Adapter 啟動；在 v1.0 中，可以使用 `attestation_pubkey` 進行驗證。

---

## 📊 競爭對手分析（更新版）

PoArt 定位於完成現有解決方案缺陷的「最佳點」。

| 特性 | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **成本** | 🆓 免費 | 🆓 | 💰 付費 | ⚠️ 免費增值 | 💰 | 💰 | 💰 | 💰 |
| **拖放 UI** | ✅ 非常簡單 | ❌ CLI | ⚠️ 中等 | ⚠️ 中等 | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **多格式匯出** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **即時預覽** | ✅ 即時 | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **隱私控制** | ✅ 3 種模式 | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **用戶端雜湊** | ✅ 隱私 | ✅ | ❌ 上傳 | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **鑑證元資料** | ✅ 完整 | ❌ | ❌ | ⚠️ 有限 | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR 驗證** | ✅ 即時 | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **速率限制** | ✅ RLS+用戶端 | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **區塊鏈錨定** | 🔄 路線圖 | ✅ 比特幣 | ✅ 以太坊 | ✅ 多鏈 | ✅ | ✅ | ✅ | ✅ |
| **開源** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **繁體中文支援** | ✅ 原生 | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**圖例：**
- ✅：完全支援/可用
- ⚠️：有限/付費方案中
- ❌：無/不支援
- 🔄：路線圖中（開發中）
- 🆓：完全免費
- 💰：付費/需要訂閱

### 競爭對手的弱點，PoArt 的優勢

| 弱點 | 競爭對手 | PoArt |
|------|----------|-------|
| **使用難度** | CLI、API 知識、需要錢包 | 拖放，3 次點擊完成 |
| **成本障礙** | $50-500/月訂閱 | 100% 免費 |
| **隱私** | 檔案上傳到伺服器 | 用戶端，檔案永不離開 |
| **鑑證數據** | 僅時間戳記 | IP、位置、裝置、時間 - 全部 |
| **繁體中文支援** | 無或非常有限 | 原生語言支援 |
| **開源** | 黑盒 | GitHub 上所有程式碼開放 |

---

## 📈 使用統計（2026 Q1 目標）

| 指標 | 目標 | 狀態 |
|------|------|------|
| **總證書數** | 1,000 | 🔄 進行中 |
| **活躍使用者** | 500 | 🔄 進行中 |
| **驗證次數** | 5,000 | 🔄 進行中 |
| **正常運行時間** | 99.9% | ✅ 活躍 |
| **平均回應時間** | <200ms | ✅ 最佳 |

---

## 🌍 社群與支援

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **網站:** [ilhanart.org](https://ilhanart.org)
- **電子郵件:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 貢獻者

PoArt 協定在開源社群的貢獻下繼續發展。

**貢獻方式：**
1. Fork 儲存庫
2. 建立功能分支（`git checkout -b feature/amazing-feature`）
3. 提交更改（`git commit -m 'Add amazing feature'`）
4. 推送到分支（`git push origin feature/amazing-feature`）
5. 開啟 Pull Request

### 🛠️ 我們現在需要什麼？（尋求協助）

對於 PoArt 協定**第二階段**開發，我們期待在以下領域有經驗的開發者的貢獻：

* **Supabase 邊緣函數：** 將垃圾郵件保護移至伺服器端。
* **Solana Web3.js：** 錢包簽名整合。
* **IPFS / Arweave：** 存檔和固定服務整合。

> 在添加功能之前，請在「Issues」標籤中開始討論。

---

## 💬 最後說明

### Pump.fun 與現實

該專案在 Pump.fun 上啟動是因為：
- ✅ 流動性訪問（Raydium 自動遷移）
- ✅ 現有社群訪問
- ✅ 低啟動成本

但讓我們澄清：
- **代幣價格**不是藝術成功的指標
- **營運預算**的代幣價值很重要（畫廊、展覽、基礎設施）
- **成功指標：** 認證藝術作品 + 社群參與 + 實體訪客

### 治理與去中心化

**v1.0 現實（2026）：**
- 註冊：鏈下（PostgreSQL + IPFS 備份）
- 證明：畫廊自簽名（中心化但透明）
- 治理：僅諮詢（策展最終決定）
- 代幣效用：畫廊訪問 + 註冊 + NFT 優先權

**v2.0+ 願景（2027+）：**
- 註冊：鏈上（Solana）
- 簽名：基於錢包（去中心化）
- 治理：混合（社群諮詢 + 策展品質）
- 代幣效用：增強功能 + 進階訪問

此結構在早期階段提供**營運效率**和**品質控制**，同時為未來增加**社群參與**保持開放路徑。

---

**[PoArt] 藝術證明協定 v1.0**  
*「文化 > 資本」// Culture > Capital*

## 🧾 授權

MIT 授權 © 2026 伊爾汗藝術畫廊倡議

查看 [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) 了解完整條款。

---

## 💬 致謝

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**該專案由[伊爾汗藝術畫廊]倡議開發，原始碼為透明度而公開。**

**協定 V1.0 // 用 SHA-512 封印。**

*© 2026 伊爾汗藝術 | 保留藝術作品、視覺作品和創意的所有權利。*

---
