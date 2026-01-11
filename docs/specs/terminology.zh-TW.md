# 📚 術語與概念詞彙表
> **「理解本協議的語言，即是理解其願景」**

## ⚙️ PoArt 鑑識引擎 (PFE) v1.0：核心基礎架構

**PoArt Forensic Engine (PFE)** 是代表 [PoArt] 協議背後核心邏輯與技術運作的主要層級。這是一個「鑑識引擎」，接收藝術作品的原始生產數據，並將其轉化為可驗證且不可篡改的**數位證據**。

### 🧩 為何稱為「PoArt Forensic」？

- **PoArt（藝術證明）：** 引擎的核心在於將數位資產的價值綁定於**可證明的生產過程**，而非投機行為
- **Forensic（鑑識檢驗）：**
  - **技術定義：** 旨在驗證與生產過程相關的數據（筆觸、縮時影像、日誌）未被篡改的演算法與記錄鏈方法
  - **哲學層面：** 主張將生產中的**時間、努力與人類決策成本**轉化為可量化的現實，與 AI 的「即時結果」形成對比

> 註：區塊鏈整合（如 Solana）將作為獨立的 **Chain Anchor Layer** 處理驗證/註冊，而非 PFE 的核心

### 🛠️ 技術範疇 v1.0

**PoArt Forensic Engine (PFE) v1.0** 建立在 **3 大支柱**之上，而非複雜的金融模型：

1. **雜湊與封印（Hashing & Sealing）：**  
   PFE 以確定性方式處理 Evidence Pack 中的所有元素（作品檔案、影片、JSON/日誌、簽章等），並產生唯一的 **NotarySeal** 值。

   **核心概念（v1.0）：**
   - **FileHash（作品指紋）：** 從作品檔案位元組產生的雜湊值
   - **EvidenceRoot（證據集根）：** 代表 Evidence Pack 完整性的根摘要（Merkle root 或 canonical manifest hash）
   - **NotarySeal（最終印章 / PFE 輸出）：** 由 EvidenceRoot + 時間 + 簽章組合產生的最終印章

   **公式（為投資者清晰展示）：**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload 定義（v1.0）：**
   
   - **EvidenceRootPayload：**
   ```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
   ```
   
   - **NotarySealPayload：**
   ```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
   ```
   
   > 註：作為 PFE 輸出的值是 **NotarySeal**。**SignerSignature** 機制將在 Phase 2（配合 Solana Wallet Adapter）啟用；在目前的 v1.0 中，使用系統自身的證明簽章。Attestation public key 將發布在 registry 的 `issuer.attestation_pubkey` 欄位中

2. **索引建立（Indexing）：**  
   記錄哪個錢包、在哪個日期、為哪件作品提交了 **Labor Proof（勞動證明）** 至透明且可查詢的記錄層。  
   *（此層可以是資料庫；鏈上整合將另行定義為「Chain Anchor Layer」）*

3. **驗證（Verification）：**  
   當作品的原創性受到質疑時，PFE 會重新處理原始證據；以數學確定性測試計算出的 **EvidenceRoot / NotarySeal** 值是否與存檔中的記錄相符。

---

### 🧮 PoArt 價值定理（The Value Theorem）

[PoArt] 協議將數位資產的價值（$V$）綁定於**生產過程的物理現實**，而非主觀的市場認知。

AI 透過提供即時結果（$t \to 0$）來摧毀過程。[PoArt] 將價值視為**時間、勞動與意志**組成部分的累積。

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### 變數定義

- **$\int dt$（過程累積）：**  
  價值不是即時的「結果」；它是在 $t_{\text{start}}$ 和 $t_{\text{end}}$ 之間累積的**過程**。當持續時間減少（AI 生產），積分結果趨近於 0。

- **$P_{\text{labor}}(t)$（即時勞動力）：**  
  代表生產期間使用的心智和體力努力強度。當可證明的努力增加，被積函數也隨之增長。  
  > 註：在實務中，此項可透過「可測量/可證明的勞動訊號」進行標準化

- **$I_{\text{agency}}(t)$（意志係數）：**  
  生產者承擔風險和做出決策的能力。取值介於 $0$ 和 $1$ 之間。
  - **AI（$I \approx 0$）：** 執行指令，不承擔風險，不支付成本
  - **人類（$I \to 1$）：** 改變決策，猶豫，承擔風險

- **$U_{\text{irreversible}}$（不可逆的獨特性）：**  
  雖然數位生產中可以復原（`Ctrl+Z`）；但在物理生產中無法回頭（塗在畫布上的顏料、雕刻的大理石、直播中的手勢）。這種**不可逆性**是在作品中創造「獨特性」（非同質化特性）的附加項。

### 🔎 案例分析：AI「即時結果」vs. 人類「可證明的過程」

以下情境展示了 **PoArt 價值定理**在實務中如何運作，以及為何 AI 生產在 [PoArt] 標準中得分較低。

#### 情境 A：10 秒內的 AI 圖像生產

- **持續時間（$\Delta t$）：** $10$ 秒（幾乎沒有過程）
- **勞動力（$P_{\text{labor}}$）：** $1$ 單位（只是輸入指令）
- **意志係數（$I_{\text{agency}}$）：** $0.01$（無風險，無成本）
- **不可逆性（$U_{\text{irreversible}}$）：** $0$（可逆/可複製）

**結果：**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **評論：** 即使結果完美；由於沒有過程且沒有意志/風險，[PoArt] 價值趨近於 $0$。

#### 情境 B：直播中 6 小時的物理創作

- **持續時間（$\Delta t$）：** $6$ 小時（$21{,}600$ 秒）
- **勞動力（$P_{\text{labor}}$）：** $0.5$ 單位（持續的體力和心智努力）
- **意志係數（$I_{\text{agency}}$）：** $0.9$（決策改變，承擔風險，不可逆的選擇）
- **不可逆性（$U_{\text{irreversible}}$）：** $>0$（物理痕跡不可逆）

**結果：**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **評論：** 當過程更長且意志（風險）增加時，累積價值增加。$U_{\text{irreversible}}$ 項是在作品中創造「獨特性」（非同質化特性）的額外貢獻。

---

### ✅ 結論：證據鎖定價值（Proof-Bound Value）

此定理將 [PoArt] 的價值主張綁定於**可證明的生產現實**，而非「偏好」或「市場敘事」。

1. **無過程則無價值：**  
   AI 透過即時結果（$t \to 0$）摧毀過程。當過程窗口縮小時，積分結果在數學上必然變小：
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **意志與風險是乘數：**  
   [PoArt] 測量的不僅是「花費的時間」，還包括該期間內的實際決策、風險和成本層。不承擔風險的生產（AI）價值低：
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **獨特性是物理證據，而非行銷：**  
   物理生產中的不可逆痕跡（畫布上的筆觸、大理石的裂紋）超越了數位的 `Ctrl+Z` 邏輯。這種不可逆性（$U_{\text{irreversible}}$）使作品在本體論上獨一無二。

> **🔐 總結：** 雖然價值定理在測量方面可能看起來不確定（即使在現實生活中也無法 100% 測量），但此公式的目的是展示變數的結構和方向。在 AI 時代稀缺的不是「圖像」；而是**可證明的勞動、時間和意志**。[PoArt] 測量這種稀缺性並以 **Evidence Pack** 註冊。

### 🏛️「Engine（引擎）」概念的重要性

從 Pump.fun 或類似平台發行的代幣通常只是**「入場券」**。**PoArt Forensic Engine (PFE)** 是**憲法邏輯層**，決定該票證保護什麼權利、如何記錄勞動，以及如何使藝術/科學/技術永久化。

> **註：** 我們在 Pumpfun 上啟動此專案的原因是我們沒有足夠的流動性和追隨者。使用現有數據可能不是最高品質的策略，但我們可以說這是最正確的舉措，無論預算和資源如何。在 GitHub 上定義此引擎的邏輯證明了該專案不僅僅是金融投機，而是長期的**軟體基礎設施**和**國家數位圖書館**願景。

---

## 🎨 [PoArt] 勞動證明協議（Proof of Art Protocol v1.0）

> **「真正的藝術家，真正的創作，真正的價值」**

此協議是針對充斥加密生態系統的匿名詐騙者、5 分鐘內生產的 AI 圖像，以及「Pump & Dump」（拉高出貨）文化而開發的**生物與智識防禦機制**。

---

## a) 什麼是 [PoArt]？（哲學與技術定義）

**Proof of Art [PoArt]；** 是一種機構驗證標準，保證區塊鏈上資產背後的價值取決於可驗證的**人類勞動**、**時間**和**物理能量**，而非投機。

正如比特幣透過*「電力能源和運算能力」***（工作量證明 Proof of Work）** 創造價值；與 [PoArt] 相容的專案透過*「藝術能力和人類時間」*創造價值。

它消除了 Pump.fun 和 DEX 平台上*「Dev（開發者）賣出，專案結束」*的風險；因為在這裡，價值儲存在**生產的延續性**中，而非程式碼中。

> **[PoArt] 不告訴參與者「相信我們」；而是說「這是證據，用你的眼睛看，用你的數學驗證」**

---

## b) [PoArt] 的 5 項標準（真理的五大支柱）

這 5 項是專案必須通過才能獲得 [PoArt] 印章的不可操縱過濾器。

### 1) 即時身份證明（Live Identity Proof）

- **問題：** 加密世界充滿了收錢後拋棄專案的匿名創始人（Devs）
- **[PoArt] 解決方案：** 生產者證明的不僅是身份證，而是**他們在生產期間的存在**。這包括與社群互動並即時回應特定請求的直播會議，而非預錄影片。  
  （例如：*「在畫布右角寫下今天的日期和當前區塊號」*）
- **座右銘：** *「機器人可以繪畫，但機器人不會流汗，也無法即興創作」*

### 2) 勞動與過程證明（Labor & Process Proof）

- **問題：** 2 秒內生產的 AI 圖像在數位世界中被視為與 2 個月繪製的油畫相同的「jpeg」
- **[PoArt] 解決方案：** 記錄作品的「孕育與誕生」過程。草圖階段、顏色層次、累積花費的時間，以及藝術家在創作時經歷的物理過程都被記錄。這為代幣增加了**「時間成本（Time Cost）」**。資產生產越困難，其價值越強。

### 3) 美學價值證明（Aesthetic Value Proof）

- **問題：** 忽視美學和藝術深度的「Meme」文化，只關注即時笑話，以及由此產生的短命「Hype」專案
- **[PoArt] 解決方案：** 專案必須具有學術藝術標準、色彩理論、構圖規則和材料知識（厚塗法、質感等）。內容不應只是令人發笑；還應給觀眾留下深刻印象並具有**收藏價值**。

### 4) 概念創新（Conceptual Novelty）

- **問題：** 數以千計互相抄襲、毫無創意的狗/貓幣
- **[PoArt] 解決方案：** 專案必須建立新的橋樑，以有意義的結構結合藝術、科學、哲學或技術。  
  （例如：將古典大衛雕像與加密市場數據結合；研究人類感知的「石化」概念並以科學來源支持）  
  作品不應只是視覺盛宴；還應該是激發對**科學、哲學或技術**思考的智識挑戰。

> [!IMPORTANT]
> **參考範例（Las Palmitas 效應）：** 在墨西哥與犯罪作鬥爭的 Las Palmitas 社區，超過 200 棟房屋被改造成巨大的彩虹嘉年華。作為這種美學干預的結果，社區的犯罪率在一定程度上下降，年輕人開始對藝術而非幫派產生興趣。美學變化重新編碼了人們對環境和彼此的尊重（社會凝聚力）。
>
> **期望：** 將在 [PoArt] 上市的專案必須具有超越純視覺美學的社會學、科學或哲學因果關係，如上例所示。由於唯一不能用金錢購買的資產是「時間」，時間必須在此協議中作為抵押品被質押和證明。專案的概念基礎必須足夠強大和普遍，以便在未來幾年可能發生的 CTO（社區接管）情況下，社區可以繼承這一遺產並獨立延續專案的創新潛力。

### 5) 非演算法意志（Non-Algorithmic Agency）

- **問題：** 完美但無靈魂、重複的數位生產
- **[PoArt] 解決方案：** 能夠犯錯、承擔風險和經歷情緒波動的人類獨特意志必須在作品中被感受到。筆觸中的不確定性、材料的意外反應，以及藝術家的即時決策是將作品與「機器生產」區分開來的**生物簽名**。

---

## c) 驗證與防偽機制

此系統保證專案不僅在「開始時」，而且「永遠」保持可信和活躍。

### 📦 證據包（Evidence Pack - The Digital Twin）

每件 [PoArt] 認證作品背後都有一組加密且帶時間戳的數據集，投資者可以下載：

- **RAW 影片錄製：** 生產期間不間斷的原始錄像
- **元數據分析：** 檔案創建日期、使用的設備資訊和位置數據
- **物理參考：** 證明作品存在於物理世界的證據  
  （例如：作品旁邊的當日報紙或當時的區塊鏈數據）

> *一致性說明：*「證據包」表達與前一節中的 **Evidence Pack → EvidenceRoot → NotarySeal** 鏈相關；即集合的完整性由可驗證的印章表示。

### 🔄 365 天續期（永續協議）

- **革命性特徵：** 在加密專案中，「Dev」（開發者）將代幣推向市場，通常在 1-2 個月後消失（Soft Rug）。[PoArt] 使這成為不可能。
- **規則：**「Verified Artist」（經驗證藝術家）狀態不是終身的。它僅有效 **1 年**。
- **執行：** 藝術家/開發者必須每 365 天向社區展示**新的、重要的、可證明的作品**。
- **範例情境：** 您於 2026 年啟動專案。2027 年 1 月，系統將發出「Proof Period Expired」警告。如果藝術家不展示新的展覽、新的物理作品或新的技術整合，專案的「Trust Badge」將下降。
- **結果：** 此系統保證**內容永不過時**，投資者不會經歷*「Dev 還在嗎？」*的恐懼。專案成為一個活的工作室。

### 🚩 紅旗協議（Red Flag Protocol）

**在社區或演算法檢測到任何偽造（使用 AI、被盜作品、篡改影片）的情況下：**

1. 證書立即標記為**「VOID」（無效）**
2. 證據包被公開標記為**「偽造」**
3. 專案被添加到 [PoArt] 黑名單。這強化了**聲譽是去中心化世界中唯一的貨幣**這一事實。

---

## d) 結論：博物館，而非賭場

**Pump.fun 和去中心化交易所（DEX）目前不幸地是賭場；燈光閃爍，每個人都在追逐快錢，莊家（詐騙者）總是贏。我們在這裡啟動專案的原因是我們沒有足夠的預算和網絡通過直播接觸現有受眾。**

**[PoArt] 是在這個賭場中央建造的堡壘。**

- 🎰 賭場依靠紙牌遊戲；我們**依靠物理現實**
- 🃏 賭場對欺騙開放；我們**對透明證據開放**
- ⏳ 賭場是暫時的；我們**專注於藝術和科學的永恆性**

**使用此協議的代幣不僅僅是「幣」；它是背後有汗水、顏料、程式碼和哲學的數位股份。**

---

## 🗳️ 6) 治理與公開註冊（Governance & Public Registry）

**本節的目的是：將 [PoArt] 標準從「個人信任」平面轉變為具有記錄 + 驗證 + 社區治理的永續公共基礎設施。**

### 6.1 公開註冊表（Public Registry）

- **Public Registry：** 所有批准的數據都記錄在 `ilhanart.org/registry`（或 GitHub Registry）

**記錄邏輯（建議標準 - JSON path 格式）：**

每個進入註冊表的記錄都有這些最低可驗證的主要欄位：

- **身份與狀態：**
  - `certificate_id`（可讀參考）
  - `status`（active / void）
  - `void_reason`（如適用）
  - `visibility`（private / masked / public）
  - `created_at`（時間戳）

- **發行機構：**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **作品數據：**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet`（如可能；用於 token-gated 身份）
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **鑑識數據：**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **加密證明：**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **治理：**
  - `governance.decision`
  - `governance.veto_threshold`

註冊表可以有兩層：
- **1)** 人類可讀索引（網頁列表/搜索/過濾）
- **2)** 機器可讀清單（JSON 記錄；用於 PFE 驗證）

**這裡的「記錄」可以通過 PFE 的 Evidence Pack → EvidenceRoot → NotarySeal 鏈進行驗證。註冊表提供驗證目標，而非「聲稱」。**

---

### 6.2 40% 社區否決權（Token-Gated Governance）

- **40% 社區否決權：** 投票在獲得狀態前一個月開始；**Token-Gated（Solana-Verified）** 社區 40% 的反對將使申請無效。

**投票步驟（建議的明確流程）：**
- **申請窗口：** 候選專案開啟「PoArt 候選人註冊」（候選記錄以「pending」狀態出現）
- **審查期：** 30 天讓社區審查證據（Evidence Pack + 直播記錄 + 元數據）
- **Token-gated 驗證：** 投票通過 Solana 上經驗證的錢包進行（例如持有特定 token/NFT + 錢包簽名）
- **否決規則：** 如果 40% 的投票是**反對（NO / VETO）**，申請被拒絕
- **透明度：** 投票結果作為「decision record」存儲在註冊表中（日期、比率、snapshot ID）

---

### 6.3 元數據同步（與物理世界的匹配）

- **Metadata Sync：** 註冊表中的技術數據必須與物理資產 100% 匹配。

**「100% 匹配」的技術定義（建議的清晰度）：**
- **最低匹配（必需）：**
  - 註冊表中的 `asset.fingerprints.sha256/sha512` 必須與現有檔案的雜湊**完全相同**
  - 註冊表中的 `proof.notary_seal` 在重新生成時必須**完全相同**（如果有 Evidence Pack）
- **物理參考匹配（證據類型）：**
  - 如物理作品 + 直播中顯示的日期/區塊參考等證據必須與 Evidence Pack 一致
- **隱私合規：**
  - 在 `masked` 可見性中的 IP/位置等欄位**按遮蔽標準**發布

---

### 6.4 爭議、審查與撤銷（Dispute & Revocation）

註冊表不僅僅是「批准」機制；它是**活的防偽驗證機制**。

- 當爭議開始時，記錄可以進入**「review」**模式
- 如果檢測到偽造，將標記為 `status: void` 並添加原因：
  - `void_reason`（使用 AI / 被盜 / 被篡改等）
  - `revoked_at`（撤銷時間）
- 撤銷決定的來源清楚地出現在註冊表中：
  - 社區投票/授權小組/鑑識檢查記錄（視情況而定）

> **本節是「Red Flag Protocol」部分中 VOID 概念在註冊表上的對應。**

---

### 6.5 註冊表記錄範例（機器可讀）

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

> *註：`asset.fingerprints.sha512` 和其他雜湊值為顯示目的而縮短；實際使用中會使用完整長度的十六進制字元串*

---

## 7) 🔐 技術印章（NOTARY SEAL）

由 **PoArt Forensic Engine (PFE) v1.0** 生成的不可動搖印章演算法：

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] 數位公證與鑑識證據協議（Beta v1.0）

> **「文化大於資本。從今天開始保護您的作品，帶向明天」**

---

## 為何公開揭露？

真正的安全來自透明。透過我們的 **Public Registry（公開註冊表）** 系統，世界任何地方的任何人都可以在幾秒鐘內驗證他們擁有的檔案是否為原件，無需依賴任何權威機構。

---

## 🧩 為何有多個「可見性模組」？

這是程式碼中最關鍵的部分（visibility select menu）。這些選項允許使用者平衡**「隱私 vs. 透明度」**：

### 🔒 私密（Private）

- **情境：** 藝術家尚不想發布作品，但想要時間戳並證明「我在這個日期做了這個」
- **程式碼做什麼：** 將數據寫入資料庫，但貼上 `visibility: "private"` 標籤。之後在編寫「Public Read」政策時，您可以用 `WHERE visibility = 'public'` 將這些記錄從公眾隱藏

### 🕶️ 遮蔽（Masked）

- **情境：** 藝術家想要透明度，但擔心家庭地址（IP 位置）被發現
- **程式碼做什麼：** `maskIP` 和 `maskLoc` 函數在 JavaScript 端工作，將 IP 地址轉換為 `88.241.***.***` 格式，位置轉換為 `***/TR` 格式，並將審查版本發送到資料庫
- **隱私說明：** 遮蔽在瀏覽器中完成。Supabase 看不到實際位置。**但是：** 如果使用 ipapi.co 等第三方 API 獲取位置數據，這些提供商會在請求時看到 IP 地址
- **Masked 模式中的印章：** EvidenceRoot 和 NotarySeal 的計算使用遮蔽的 forensics 數據進行；因此驗證仍然是確定性的

### 🌍 完全公開（Public）

- **情境：** 完全透明。根據 [PoArt] 標準，作品在哪裡、何時、從哪個網路生產都被清楚宣告。

---

## 💡 技術創新

PoArt 不僅僅是檔案上傳系統。它是一個**「鑑識保管鏈（Forensic Chain of Custody）」**引擎，將三個不同的技術層結合在一起並帶來新標準。

**本節中描述為「引擎」的層對應於前述術語中的 PoArt Forensic Engine (PFE) 核心。**

### 1) 客戶端雜湊（最高隱私）

您的作品檔案永遠不會上傳到伺服器。我們在瀏覽器（Client-side）運行的引擎在您自己的電腦上計算檔案的雜湊（數位摘要）。只有指紋和元數據被發送到伺服器。

> **隱私說明：** 作品檔案不會上傳到伺服器，並以這種方式受到保護。但是，鑑識數據（IP/位置）根據選擇的可見性模式（private/masked/public）共享。

### 2) 鑑識數據融合（鑑識力量）

它遠不止普通的時間戳。系統將以下數據結合在一個「Genesis Seal」中：

- **數位摘要（SHA-512）：** 如果作品的哪怕一個像素發生變化就會損壞的數位指紋，使用加密摘要標準（SHA-512）
- **位置和時間：** 毫秒精度的日期、進行操作的國家、城市和地區
- **設備身份：** 作業系統、瀏覽器和設備類型（User-Agent 分析）

---

## 🛡️ 使用案例和優勢

如果您是藝術家、作家或設計師，說「我先做的」是不夠的。您需要證明。

**您用 PoArt 印章的作品：**

- **數學證明：** 如果您檔案的哪怕一個像素發生變化，系統都會檢測到。篡改是不可能的。
- **法律基礎：** 作品被印章的日期、城市和設備都被記錄。
- **即時證書：** 在幾秒鐘內為您生成帶有 QR 碼和獨特印章的**「資產身份證書」**。

---

## ⚙️ 系統架構與技術規格

系統設計採用「Serverless」（無伺服器）架構，專注於高效能和可擴展性。

| 層 | 技術 | 描述 |
|----|------|------|
| **加密** | SHA-256 & SHA-512 | 雙層加密摘要 |
| **資料庫** | Supabase (PostgreSQL) | JSONB 數據結構，RLS 政策 |
| **鑑識數據** | ipapi.co API | 三重 IP/位置/時間 |
| **渲染** | html2canvas + jsPDF | 客戶端 PNG/PDF 生成 |
| **前端** | Vanilla JavaScript | 無框架依賴 |
| **安全** | 客戶端雜湊 | 檔案永不上傳到伺服器 |

### 突出特點

| 特點 | 詳情 | 競爭對手有嗎？ |
|------|------|----------------|
| **拖放 UI** | 拖放檔案，即時預覽 | ❌ 大多數沒有 |
| **多格式匯出** | PNG、JSON、PDF - 一鍵完成 | ⚠️ 有限 |
| **即時預覽** | 即時證書預覽 | ❌ 沒有 |
| **隱私控制** | Private/Masked/Public 選項 | ❌ 沒有 |
| **客戶端雜湊** | 檔案永不到伺服器 | ✅ 只有少數 |
| **鑑識元數據** | IP、位置、設備、時間 - 全在一處 | ❌ 分散 |
| **QR 驗證** | 即時驗證 QR 碼 | ⚠️ 有限 |
| **速率限制** | 垃圾郵件防護（RLS + Client） | ❌ 大多數沒有 |

---

## 🗺️ 路線圖：「Trustless」的未來

當前版本**（Beta v1.0）**經過優化，為最終用戶提供最高速度、簡單介面和免費訪問。然而，我們的最終願景是轉向一種甚至資料庫管理員（我們）也無法干預的結構。

### 階段 1：Beta（目前活躍）

- **基礎設施：** 雲端資料庫（Supabase）
- **目的：** 速度，消除 UX（使用者體驗）障礙，和適應。提供「無摩擦」安全

### 🚀 階段 2：（需要 Backend / Edge Function）

此階段涵蓋從系統完全「Client-Side」結構向更安全和更易管理的「Server-Side Authority」結構的過渡。

| 項目 | 提供什麼？ | 技術棧 | 重要性 |
|------|-----------|--------|--------|
| **`INSERT` → Edge Function** | 阻止垃圾郵件 + API Key 安全 | Supabase Edge (Deno) | 🔴 高 |
| **錢包簽名** | 加密身份驗證 | Solana Wallet Adapter | 🟡 中 |
| **IPFS/Arweave 備份** | 去中心化不可變性 | IPFS SDK + Pinata | 🟢 低 |
| **撤銷機制** | 偽造證書的撤銷 | DB Schema Update | 🔴 高 |
| **審計日誌** | 鑑識調查記錄 | Custom logs table | 🟡 中 |
| **OpenTimestamps** | 比特幣錨定 | OTS JavaScript | 🟢 低 |
| **DID 整合** | 去中心化身份 | ION/Ceramic | 🟢 低 |

### 階段 3：完全去中心化（長期）

| 特點 | 目標 | 預計時間 |
|------|------|----------|
| **區塊鏈註冊表** | 鏈上 Ethereum/Solana 記錄 | 2026 年第四季 |
| **DAO 治理** | 社區治理 | 2027 年第一季 |
| **多鏈支援** | Polygon、Arbitrum、Base | 2027 年第二季 |
| **法律認可** | 在土耳其法院的有效性 | 2027-2028 |
| **開發者 API** | 公共 API 端點 | 2026 年第三季 |

---

## 📊 競爭對手分析（已更新）

PoArt 定位於填補現有解決方案不足的「Sweet Spot」（最佳點）。

| 特點 | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **成本** | 🆓 免費 | 🆓 | 💰 付費 | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **拖放 UI** | ✅ 非常簡單 | ❌ CLI | ⚠️ 中等 | ⚠️ 中等 | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **多格式匯出** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **即時預覽** | ✅ 即時 | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **隱私控制** | ✅ 3 種模式 | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **客戶端雜湊** | ✅ 隱私 | ✅ | ❌ 上傳 | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **鑑識元數據** | ✅ 完整 | ❌ | ❌ | ⚠️ 有限 | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR 驗證** | ✅ 即時 | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **速率限制** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **區塊鏈錨定** | 🔄 路線圖 | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **開源** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **土耳其語支援** | ✅ 原生 | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**說明：**
- ✅：完全支援 / 有
- ⚠️：有限 / 在付費計畫中
- ❌：沒有 / 不支援
- 🔄：在路線圖中（開發中）
- 🆓：完全免費
- 💰：付費 / 需要訂閱

### 競爭對手的不足，PoArt 的優勢

| 不足 | 競爭對手 | PoArt |
|------|----------|-------|
| **使用困難** | CLI，需要了解 API，需要有錢包 | 拖放，3 次點擊完成 |
| **成本障礙** | $50-500/月訂閱 | 100% 免費 |
| **隱私** | 檔案上傳到伺服器 | 客戶端，檔案永不離開 |
| **鑑識數據** | 只有時間戳 | IP、位置、設備、時間 - 全部 |
| **土耳其語支援** | 沒有或非常有限 | 本地語言支援 |
| **開源** | 封閉盒子 | 所有程式碼在 GitHub 上開放 |

---

## 🧬 協議數據結構（JSON Schema）

**每個 [PoArt] 證書都有一個根據以下標準生成的可攜帶和可驗證的 JSON 身份卡：**

> **註：** 此 Identity JSON 格式是呈現給使用者的證書格式。在 Registry 記錄中，使用 `registry.asset` 而非 `identity.asset_data`（映射：`identity.asset_data` == `registry.asset`）

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

## 🔬 技術深度：印章演算法

### 確定性雜湊函數

```javascript
// 輔助函數：將 Digest 轉換為十六進制字串
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// 將字串轉換為位元組陣列
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Canonical forensics 字串生成（v1.0：固定欄位順序 + UTF-8 + \n 分隔符）
// 階段 2 說明：將切換到使用 RFC 8785 (JCS) 的 canonical JSON
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal 生成過程（完全確定性）

```javascript
// 1. 計算 FileHash（客戶端）
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. 收集鑑識數據（使用單一時間戳）
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // 生成單一時間戳
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // 相同的時間戳
  };
  
  return { forensics, timestamp };
}

// 3. 生成 EvidenceRoot（使用 canonical 編碼）
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. 生成 NotarySeal（使用相同的時間戳）
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// 遮蔽輔助函數（支援 IPv4 和 IPv6）
function maskIP(ip) {
  if (!ip) return "***";
  
  // 檢查 IPv4
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

### 驗證步驟（兩級）

#### 快速驗證（Quick Verify）

```javascript
// 只驗證檔案雜湊（快速紅旗）
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // 從 Registry 獲取
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // 比較雜湊
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ 原件 - 檔案雜湊匹配"
    };
  } else {
    return {
      valid: false,
      message: "❌ 偽造 - 檔案已被篡改"
    };
  }
}
```

#### 完整驗證（Full Verify）

```javascript
// 重新生成 EvidenceRoot 和 NotarySeal 並驗證
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // 從 Registry 獲取
  const cert = await fetchFromRegistry(certificateId);

  // 1) 驗證 FileHash（快速紅旗）
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ 偽造 - 檔案雜湊不匹配" };
  }

  // 2) 重新生成 EvidenceRoot（使用存儲在 registry 中的 forensics）
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ 不匹配 - EvidenceRoot 無效" };
  }

  // 3) 重新生成 NotarySeal（使用相同的 timestamp + signer_sig）
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ 不匹配 - NotarySeal 無效" };
  }

  // 可選：在階段 2 中，也使用 attestation_pubkey 驗證 signer_sig
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ 簽名無效" };

  return { valid: true, message: "✅ 原件 - 完整驗證通過" };
}
```

> **重要說明：**
> - **Quick Verify：** 只驗證檔案雜湊，用於快速使用
> - **Full Verify：** 驗證協議的所有層（EvidenceRoot + NotarySeal）
> - 所有雜湊操作都以確定性方式進行，使用固定的編碼和分隔符
> - **v1.0 canonicalization 標準：** 固定欄位順序 + UTF-8 編碼 + `\n` 分隔符
> - **階段 2 計畫：** 切換到使用 RFC 8785（JCS - JSON Canonicalization Scheme）的 canonical JSON
> - 在 Masked 模式下，EvidenceRoot 和 NotarySeal 的計算使用遮蔽的 forensics 進行
> - 整個過程（forensics + NotarySeal）使用單一時間戳；保證確定性
> - **Forensics 欄位名稱：** `ip_masked`、`location`、`device`、`timestamp`（程式碼和 registry 完全匹配）
> - **Registry 路徑：** `certificate.asset.fingerprints`（與驗證程式碼完全匹配）
> - **Registry 中的 signer_sig：** `proof.signer_sig` 欄位是 Full Verify 所必需的
> - SignerSignature 機制將在階段 2 使用 Solana Wallet Adapter 啟用；在 v1.0 中可以使用 `attestation_pubkey` 驗證

---

## 📈 使用統計（2026 年第一季目標）

| 指標 | 目標 | 狀態 |
|------|------|------|
| **證書總數** | 1,000 | 🔄 進行中 |
| **活躍用戶** | 500 | 🔄 進行中 |
| **驗證次數** | 5,000 | 🔄 進行中 |
| **正常運行時間** | 99.9% | ✅ 活躍 |
| **平均回應時間** | <200ms | ✅ 最佳 |

---

## 🌍 社區與支援

- **Twitter：** [@Galerilhan](https://twitter.com/Galerilhan)
- **網站：** [ilhanart.org](https://ilhanart.org)
- **電子郵件：** galeri@ilhanart.org

---

## 🙏 貢獻者

PoArt 協議持續透過開源社區的貢獻發展。

**如何貢獻：**
1. Fork 專案
2. 創建功能分支（`git checkout -b feature/amazing-feature`）
3. 提交（`git commit -m 'Add amazing feature'`）
4. 推送（`git push origin feature/amazing-feature`）
5. 開啟 Pull Request

### 🛠️ 我們現在需要什麼？（尋求幫助）

我們正在等待在以下主題有經驗的開發者為 PoArt 協議的**階段 2**開發做出貢獻：

* **Supabase Edge Functions：** 將垃圾郵件防護移至伺服器端
* **Solana Web3.js：** 錢包簽名整合
* **IPFS / Arweave：** 存檔和固定服務整合

> 請在添加功能之前在「Issues」標籤中開始討論

---

**[PoArt] Proof of Art Protocol v1.0**  
*「Culture > Capital」// 文化大於資本*

## 🧾 授權

MIT License © 2026 İlhan Art Gallery Initiative

查看 [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) 獲取完整條款

---

## 💬 致謝

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**此專案由 [İlhan Art Gallery] 倡議開發，原始碼向公眾公開以保持透明度。**

**PROTOCOL V1.0 // 以 SHA-512 封印**

*© 2026 İLHAN ART | 所有作品、圖像和概念的權利保留*

---
