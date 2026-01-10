# 📚 术语与概念词汇表
> **"理解本协议的语言，就是理解其愿景。"**

## ⚙️ PoArt 取证引擎 (PFE) v1.0：核心基础设施

**PoArt 取证引擎 (PFE)** 是代表 [PoArt] 协议背后核心逻辑和技术运作的主层。这是将艺术作品的原始生产数据转化为可验证且不可变的**数字证据**的"取证引擎"。

### 🧩 为什么称为"PoArt 取证"？

- **PoArt (艺术证明)：** 引擎的重点是将数字资产的价值绑定到**可证明的生产过程**，而非投机行为。
- **取证（取证验证）：**
  - **技术定义：** 一种算法和记录链方法，用于验证生产过程数据（笔触、延时摄影、日志）未被篡改。
  - **哲学层面：** 针对人工智能的"即时输出"生产，将**人类时间、努力和决策成本**转化为可测量现实的主张。

> 注：区块链（如 Solana）集成不是 PFE 的核心；它将作为单独定义的**链锚定层**用于验证/注册表目的。

### 🛠️ v1.0 技术范围

**PoArt 取证引擎 (PFE) v1.0** 建立在以下 **3 大支柱**之上，而非复杂的金融模型：

1. **哈希与封印（封印）：**  
   PFE 以确定性方式处理证据包中的所有元素（作品文件、视频、JSON/日志、签名等），并生成唯一的 **NotarySeal** 值。

   **核心概念 (v1.0)：**
   - **FileHash（作品指纹）：** 从作品文件字节生成的哈希。
   - **EvidenceRoot（证据包根）：** 代表证据包完整性的根摘要（Merkle 根或规范清单哈希）。
   - **NotarySeal（最终封印 / PFE 输出）：** 从 EvidenceRoot + 时间 + 签名组合生成的最终封印。

   **公式（投资者可清晰看到）：**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **规范载荷定义 (v1.0)：**
   
   - **EvidenceRootPayload：**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload：**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > 注：作为 PFE 输出提及的值是 **NotarySeal**。**SignerSignature** 机制将在阶段 2（通过 Solana 钱包适配器）激活；当前 v1.0 使用系统自己的认证签名。认证公钥在注册表的 `issuer.attestation_pubkey` 字段中发布。

2. **索引（归档）：**  
   将哪个钱包、在什么日期、为哪件作品提交了**劳动证明**记录到透明且可查询的注册层。  
   *（此层可以是数据库；链集成则单独定义为"链锚定层"。）*

3. **验证：**  
   当作品的真实性受到质疑时，PFE 重新处理原始证据；以数学确定性测试计算的 **EvidenceRoot / NotarySeal** 值是否与存档记录匹配。

---

### 🧮 PoArt 价值定理（价值定理）

[PoArt] 协议将数字资产的价值 ($V$) 关联到**生产过程的物理现实**，而非主观市场认知。

人工智能（AI）通过即时交付结果 ($t \to 0$) 消灭了过程。而 [PoArt] 则将价值视为**时间、劳动和意志**组成部分的积累。

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### 变量定义

- **$\int dt$（过程积累）：**  
  价值不是即时"输出"；它是在 $t_{\text{start}}$ 和 $t_{\text{end}}$ 之间积累的**过程**。随着持续时间减少（AI 生产），积分结果趋近于 0。

- **$P_{\text{labor}}(t)$（瞬时劳动力）：**  
  代表生产时刻消耗的精神和体力努力强度。可证明的努力增加，被积函数就会增大。  
  > 注：此术语在实践中可以通过"可测量/可证明的劳动信号"进行标准化。

- **$I_{\text{agency}}(t)$（意志系数）：**  
  生产者的风险承担和决策能力。取值在 $0$ 和 $1$ 之间。
  - **AI ($I \approx 0$)：** 执行命令，不承担风险，不付出代价。
  - **人类 ($I \to 1$)：** 改变决定，犹豫不决，承担风险。

- **$U_{\text{irreversible}}$（不可逆的独特性）：**  
  虽然数字生产中可以撤销（`Ctrl+Z`）；但在物理生产中（涂在画布上的颜料、雕刻的大理石、直播中的手势）无法回头。这种**不可逆性**是在作品中创造"独特性"（非同质化特征）的额外术语。

### 🔎 案例分析：AI "即时输出" vs. 人类 "经证明的过程"

以下场景展示了 **PoArt 价值定理**在实践中的工作原理，以及为什么 AI 生产在 [PoArt] 标准中得分较低。

#### 场景 A：使用 AI 在 10 秒内生成视觉内容

- **持续时间 ($\Delta t$)：** $10$ 秒（几乎没有过程）
- **劳动力 ($P_{\text{labor}}$)：** $1$ 单位（仅编写命令）
- **意志系数 ($I_{\text{agency}}$)：** $0.01$（无风险，无代价）
- **不可逆性 ($U_{\text{irreversible}}$)：** $0$（可逆 / 可复制）

**结果：**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **评论：** 即使输出完美；由于没有经历过程且不涉及意志/风险，[PoArt] 价值趋近于 $0$。

#### 场景 B：直播中 6 小时的物理生产

- **持续时间 ($\Delta t$)：** $6$ 小时（$21{,}600$ 秒）
- **劳动力 ($P_{\text{labor}}$)：** $0.5$ 单位（体力和脑力努力的连续性）
- **意志系数 ($I_{\text{agency}}$)：** $0.9$（改变决定、承担风险、不可逆选择）
- **不可逆性 ($U_{\text{irreversible}}$)：** $>0$（物理痕迹无法撤销）

**结果：**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **评论：** 随着过程延长和意志（风险）增加，价值累积增长。$U_{\text{irreversible}}$ 术语是在作品中创造"独特性"（非同质化特征）的额外贡献。

---

### ✅ 结论：价值与证明绑定（证明绑定价值）

该定理将 [PoArt] 的价值主张从"点赞"或"市场叙事"中提取出来，绑定到**可证明的生产现实**。

1. **没有过程就没有价值：**  
   AI 通过即时输出 ($t \to 0$) 消灭过程。随着过程窗口缩小，积分结果必然缩小：
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **意志和风险是乘数：**  
   [PoArt] 不仅测量"花费的时间"，还测量该时间内的真实决策、风险和成本层。不承担风险（AI）的生产价值较低：
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **独特性是物理证明，而非营销：**  
   物理生产中的不可逆痕迹（画布笔触、大理石碎片）超出了数字世界的 `Ctrl+Z` 逻辑。这种不可逆性 ($U_{\text{irreversible}}$) 在本体论上使作品独特化。

> **🔐 总结：** 尽管价值定理作为测量可能看起来不确定（即使在现实世界中其 100% 对应物无法完全测量），该公式的目的是展示变量的配置和方向。在 AI 时代，稀缺的不是"图像"，而是**可证明的劳动、时间和意志**。[PoArt] 测量这种稀缺性，并通过 **证据包** 进行登记。

### 🏛️ "引擎"概念的重要性

从 Pump.fun 或类似平台出现的代币通常只是**"访问票"**。然而，**PoArt 取证引擎 (PFE)** 是确定该票保护哪些权利、如何记录劳动以及如何延续艺术/科学/技术的**宪法逻辑层**。

> **注：** 我们在 Pumpfun 上启动该项目的原因是我们没有足够的流动性和足够的关注者数量。使用现有数据在战略上是正确的举措，即使不是最高质量。无论预算和资源如何，在 GitHub 上定义该引擎的逻辑都证明该项目不仅仅是金融投机，而是长期的**软件基础设施**和**数字国家图书馆**愿景。

---

## 🎨 [PoArt] 劳动证明协议（艺术证明协议 v1.0）

> **"真正的艺术家，真正的生产，真正的价值。"**

该协议是针对围绕加密生态系统的匿名诈骗者、5 分钟内生成的人工智能视觉内容以及"拉高出货"文化开发的**生物和智力防御机制**。

---

## a) 什么是 [PoArt]？（哲学和技术定义）

**艺术证明 [PoArt]；** 是一种机构验证标准，保证区块链上资产背后的价值基于可验证的**人类劳动**、**时间**和**物理能量**，而非投机。

正如比特币用*"电力和处理器功率"* **（工作量证明）** 生成价值一样；符合 [PoArt] 的项目也用*"艺术技能和人类时间"*生成价值。

它消除了 Pump.fun 和 DEX 平台上*"开发者抛售，项目结束"*的风险；因为这里的价值不在代码中，而在**生产的连续性**中。

> **[PoArt] 不对参与者说"信任我们"；它说"这是证据，用你的眼睛看，用你的数学验证。"**

---

## b) [PoArt] 五大标准（真理的五大支柱）

这 5 项是项目必须通过的不可操纵的过滤器才能获得 [PoArt] 印章。

### 1) 实时身份证明

- **问题：** 加密世界充满了身份不明的匿名创始人（开发者）收集资金并放弃项目。
- **[PoArt] 解决方案：** 生产者不仅证明身份证，还证明**生产时刻的存在**。这包括与社区互动并满足特定即时请求的直播会话，而非预录视频。  
  （例如：*"在画布右角写上今天的日期和当前区块号"*）
- **座右铭：** *"机器人可以绘画，但机器人不会流汗，也不能即兴发挥。"*

### 2) 劳动与过程证明

- **问题：** 2 秒内生成的 AI（人工智能）视觉内容与 2 个月内制作的油画在数字世界中获得相同的"jpeg"对待。
- **[PoArt] 解决方案：** 记录作品的"怀孕和分娩"过程。记录草图阶段、颜料层、累计花费的小时数以及艺术家在创作作品时经历的物理过程。这为代币增加了**"时间成本"**。资产的生产越困难，其价值就越稳固。

### 3) 美学价值证明

- **问题：** "表情包"文化仅关注即时喜剧而忽视美学和艺术深度，导致短命的"炒作"项目。
- **[PoArt] 解决方案：** 项目必须具备学术艺术标准、色彩理论、构图规则和材料知识（厚涂、纹理等）。内容不应仅仅逗笑；它应该激发观众的钦佩并具有**收藏价值**。

### 4) 概念新颖性

- **问题：** 数千种缺乏创造力的山寨狗/猫币。
- **[PoArt] 解决方案：** 项目必须以有意义的结构建立艺术、科学、哲学或技术之间的新桥梁。  
  （例如：将古典大卫雕塑与加密市场数据结合；通过此处理人类感知"变成石头"的想法，并用科学来源证实。）  
  作品不应仅仅是视觉盛宴；它还应该是激发对**科学、哲学或技术**思考的智力挑战。

> [!IMPORTANT]
> **参考示例（Las Palmitas 效应）：** 在墨西哥犯罪肆虐的 Las Palmitas 社区，200 多栋房屋被改造成巨大的彩虹盛宴。由于这种美学干预，该社区的犯罪率在一定程度上下降，青少年开始参与艺术而不是帮派。美学变化重新编码了人们对环境和彼此的尊重（社会凝聚力）。
>
> **期望：** 进入 [PoArt] 列表的项目；就像上面的例子一样，必须包含超越纯粹视觉美学的社会学、科学或哲学因果关系。由于时间是唯一无法用金钱购买的资产，在该协议中，时间必须通过作为抵押品质押来证明。项目的概念基础必须如此强大和普遍，即使在多年后可能的 CTO（社区接管）场景中，社区也可以通过继承这一遗产自主继续项目的创新潜力。

### 5) 非算法意志

- **问题：** 完美但没有灵魂、相互重复的数字生产。
- **[PoArt] 解决方案：** 人类可以犯错、承担风险并经历情绪波动的独特意志必须在作品中感受到。笔触中的不确定性、材料的意外反应以及艺术家的即时决策是将作品与"机器生产"区分开来的**生物签名**。

---

## c) 验证与反欺诈机制

该系统确保项目不仅在"开始时"而且"永远"保持可靠和活跃。

### 📦 证据包 - 数字孪生

每件 [PoArt] 认证作品背后都有一个投资者可以下载的加密和时间戳数据包：

- **RAW 视频录音：** 生产时刻的不间断原始镜头。
- **元数据分析：** 文件创建日期、使用的设备信息和位置数据。
- **物理参考：** 作品存在于物理世界的证据  
  （例如：作品旁边的当前报纸或该时刻的区块链数据）。

> *一致性说明：* "证据包"术语连接到前面部分的 **证据包 → EvidenceRoot → NotarySeal** 链；即包的完整性由可验证的封印表示。

### 🔄 365 天续订（可持续性协议）

- **革命性特征：** 在加密项目中，"开发者"发布代币，通常在 1-2 个月后消失（软跑路）。[PoArt] 使这变得不可能。
- **规则：** "已验证艺术家"身份不是终身的。仅 **1 年** 有效。
- **操作：** 艺术家/开发者每 365 天必须向社区展示**新的、重大且可证明的作品**。
- **示例场景：** 您在 2026 年启动了项目。2027 年 1 月，系统发出"证明期已过期"警告。如果艺术家没有展示新展览、新物理作品或新技术集成，项目的"信任徽章"就会下降。
- **结果：** 该系统确保**内容永不失去相关性**，投资者永远不会经历*"开发者还在吗？"*的恐惧。项目变成了一个活的工作室。

### 🚩 红旗协议

**在社区或算法检测到任何欺诈（AI 使用、被盗作品、操纵视频）的情况下：**

1. 证书立即标记为 **"无效"（VOID）**。
2. 证据包公开标记为**"假冒"**。
3. 项目被列入 [PoArt] 黑名单。这强化了在去中心化世界中**声誉是唯一货币**的事实。

---

## d) 结论：不是赌场，而是博物馆

**Pump.fun 和去中心化交易所（DEX）目前不幸是赌场；灯光闪烁，每个人都在追求快速收益，庄家（诈骗者）总是赢。我们在这里启动项目的原因是缺乏足够的预算以及通过直播接触现有受众的环境。**

**[PoArt] 是建在这个赌场中间的堡垒。**

- 🎰 赌场基于纸牌游戏；我们基于**物理现实**。
- 🃏 赌场容易作弊；我们开放**透明证据**。
- ⏳ 赌场是暂时的；我们专注于**艺术和科学的永恒**。

**使用该协议的代币不仅仅是"币"；它是包含汗水、颜料、代码和哲学的数字股权。**

---

## 🗳️ 6) 治理与公共注册表

**本节的目的是：将 [PoArt] 标准从"信任个人"层面转变为通过注册 + 验证 + 社区监督的可持续公共基础设施。**

### 6.1 公共注册表

- **公共注册表：** 所有批准的数据记录在 `ilhanart.org/registry`（或 GitHub 注册表）。

**注册逻辑（建议的标准 - JSON 路径格式）：**

进入注册表的每条记录都携带这些最低可验证核心字段：

- **身份与状态：**
  - `certificate_id`（可读参考）
  - `status`（active / void）
  - `void_reason`（如果适用）
  - `visibility`（private / masked / public）
  - `created_at`（时间戳）

- **发行机构：**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **作品信息：**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet`（如果可能；用于代币门控身份）
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **取证数据：**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **加密证明：**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **治理：**
  - `governance.decision`
  - `governance.veto_threshold`

注册表可以有两层：
- **1)** 人类可读索引（网络列表 / 搜索 / 过滤）
- **2)** 机器可读清单（JSON 记录；用于 PFE 验证）

**此处的"记录"通过 PFE 的证据包 → EvidenceRoot → NotarySeal 链变得可验证。注册表提供验证目标，而非"声明"。**

---

### 6.2 40% 社区否决权（代币门控治理）

- **40% 社区否决权：** 在获得身份前一个月开始投票；**代币门控（Solana 验证）**社区的 40% 反对使申请无效。

**投票流程（建议的明确流程）：**
- **申请窗口：** 候选项目开启"PoArt 候选注册"（候选注册以"待定"状态显示）。
- **审查期：** 社区审查证据 30 天（证据包 + 直播录音 + 元数据）。
- **代币门控验证：** 投票通过 Solana 验证的钱包进行（例如特定代币/NFT 所有权 + 钱包签名）。
- **否决规则：** 如果 40% 的投票是**反对（NO / VETO）**，申请被拒绝。
- **透明度：** 投票结果作为"决策记录"存储在注册表中（日期、比率、快照 ID）。

---

### 6.3 元数据同步（与物理世界对齐）

- **元数据同步：** 注册表中的技术数据必须与物理实体 100% 匹配。

**技术上定义"100% 匹配"（建议的清晰度）：**
- **最低匹配（强制性）：**
  - 注册表中的 `asset.fingerprints.sha256/sha512` 必须与手头文件的哈希**完全相同**。
  - 注册表中的 `proof.notary_seal` 重新生成时（如果存在证据包）必须**完全相同**。
- **物理参考匹配（证明类型）：**
  - 直播中显示的物理作品 + 日期/区块参考和类似证明必须与证据包一致。
- **隐私合规：**
  - `masked` 可见性中的 IP/位置等字段按照**掩码标准**发布。

---

### 6.4 争议与撤销

注册表不仅仅是"批准"机制；它是**针对欺诈的实时审计**机制。

- 启动争议时，记录可以置于 **"审查"** 模式。
- 如果检测到欺诈，则标记为 `status: void` 并添加原因：
  - `void_reason`（AI 使用 / 盗窃 / 操纵等）
  - `revoked_at`（撤销时间）
- 撤销决定的来源在注册表中清晰可见：
  - 社区投票 / 授权委员会 / 取证调查说明（适用者）

> **本节是"红旗协议"部分中 VOID 概念在注册表上的对应部分。**

---

### 6.5 示例注册表记录（机器可读）
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
> *注：`asset.fingerprints.sha512` 和其他哈希值为显示目的而缩写；在实际实现中，使用全长十六进制字符串。*

---

## 7) 🔐 技术封印（NOTARY SEAL）

**PoArt 取证引擎 (PFE) v1.0** 生成的不可动摇的封印算法：

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] 数字公证与取证协议（Beta v1.0）

> **"文化大于资本。今天保护您的作品，明天传承。"**

---

## 为什么公开？

真正的安全来自透明。借助我们的**公共注册表**系统，世界任何地方的任何人都可以在几秒钟内验证文件是否原始，无需任何权威机构。

---

## 🧩 为什么有多个"可见性模块"？

这是代码最关键的部分（可见性选择菜单）。这些选项允许用户平衡**"隐私 vs. 透明"**：

### 🔒 私有（Private）

- **场景：** 艺术家还不想发布作品，但想加时间戳证明"我在这个日期制作了这个"。
- **代码的作用：** 将数据写入数据库但标记 `visibility: "private"`。稍后编写"公共读取"策略时，可以通过 `WHERE visibility = 'public'` 从公众中隐藏这些记录。

### 🕶️ 掩码（Masked）

- **场景：** 艺术家想要透明但担心找到家庭地址（IP 位置）。
- **代码的作用：** `maskIP` 和 `maskLoc` 函数在 JavaScript 端工作。将 IP 地址转换为 `88.241.***.***` 格式，位置转换为 `***/TR` 格式，并将审查版本发送到数据库。
- **隐私说明：** 掩码在浏览器中完成，Supabase 看不到真实位置。**但是：** 如果使用 ipapi.co 等第三方 API 获取位置数据，这些提供商会在请求时看到 IP 地址。
- **掩码模式下的封印：** EvidenceRoot 和 NotarySeal 计算使用掩码的取证数据完成；因此验证保持确定性。

### 🌍 公开（Public）

- **场景：** 完全透明。根据 [PoArt] 标准，明确声明作品在哪里、何时、从哪个网络生产。

---

## 💡 技术创新

PoArt 不仅仅是文件上传系统。它是一个**"取证保管链"**引擎，通过在一个锅中融合三个不同的技术层来带来新标准。

**本节描述为"引擎"的层对应于先前术语中的 PoArt 取证引擎 (PFE) 核心。**

### 1) 客户端哈希（最大隐私）

您的作品文件永远不会上传到服务器。我们的浏览器基础（客户端）引擎在您自己的计算机上计算文件的哈希（数字摘要）。只有此指纹和元数据发送到服务器。

> **隐私说明：** 作品文件不上传到服务器，以这种方式受到保护。但是，取证数据（IP/位置）根据选择的可见性模式（private/masked/public）共享。

### 2) 取证数据融合（取证力量）

远远超过普通时间戳。系统将这些数据组合在单个"创世封印"中：

- **数字摘要（SHA-512）：** 使用加密摘要（SHA-512）标准的数字指纹，即使作品的一个像素发生变化也会破坏。
- **位置与时间：** 交易的毫秒精度日期、国家、城市和地区数据。
- **设备身份：** 操作系统、浏览器和设备类型（用户代理分析）。

---

## 🛡️ 用例和好处

如果您是艺术家、作家或设计师，说"我早些时候做了这个"是不够的；您需要证明它。

**您用 PoArt 封印的作品：**

- **数学证明：** 如果您文件的一个像素发生变化，系统就会知道。操纵是不可能的。
- **法律依据：** 作品在什么日期、哪个城市、从哪个设备封印都有记录。
- **即时证书：** 在几秒钟内为您生成专门的、带 QR 码和封印的**"资产身份证书"**。

---

## ⚙️ 系统架构和技术特点

该系统设计在"无服务器"架构上，专注于高性能和可扩展性。

| 层 | 技术 | 描述 |
|--------|-----------|----------|
| **加密** | SHA-256 & SHA-512 | 双层加密摘要 |
| **数据库** | Supabase (PostgreSQL) | JSONB 数据结构，RLS 策略 |
| **取证数据** | ipapi.co API | IP/位置/时间三位一体 |
| **渲染** | html2canvas + jsPDF | 客户端 PNG/PDF 生成 |
| **前端** | Vanilla JavaScript | 零框架依赖 |
| **安全** | 客户端哈希 | 文件永不进入服务器 |

### 突出特点

| 功能 | 详情 | 竞争对手中？ |
|---------|-------|-------------|
| **拖放 UI** | 文件拖放，即时预览 | ❌ 大多数缺失 |
| **多格式导出** | PNG、JSON、PDF - 一键 | ⚠️ 有限 |
| **实时预览** | 实时证书预览 | ❌ 无 |
| **隐私控制** | Private/Masked/Public 选项 | ❌ 无 |
| **客户端哈希** | 文件永不进入服务器 | ✅ 仅在少数中 |
| **取证元数据** | IP、位置、设备、时间 - 全部在一起 | ❌ 分散 |
| **QR 验证** | 即时验证 QR 码 | ⚠️ 有限 |
| **速率限制** | 垃圾邮件保护（RLS + 客户端） | ❌ 大多数缺失 |

---

## 🗺️ 路线图："无信任"未来

当前版本 **(Beta v1.0)** 已优化，为最终用户提供最大速度、简单界面和免费访问。然而，我们的最终愿景是过渡到数据库管理员（我们）也无法干预的结构。

### 阶段 1：Beta（目前上线）

- **基础设施：** 云数据库（Supabase）。
- **目的：** 速度，消除 UX（用户体验）障碍和适应。提供"无摩擦"安全。

### 🚀 阶段 2：（后端 / Edge 功能要求）

该阶段涵盖从完全"客户端"工作结构到更安全和可管理的"服务器端权威"结构的过渡。

| 项目 | 带来什么？ | 技术栈 | 优先级 |
|-------|---------------|------------|---------|
| **`INSERT` → Edge 功能** | 垃圾邮件预防 + API 密钥安全 | Supabase Edge (Deno) | 🔴 高 |
| **钱包签名** | 加密认证 | Solana 钱包适配器 | 🟡 中 |
| **IPFS/Arweave 备份** | 去中心化不变性 | IPFS SDK + Pinata | 🟢 低 |
| **撤销机制** | 假证书取消 | DB Schema 更新 | 🔴 高 |
| **审计日志** | 取证查询记录 | 自定义日志表 | 🟡 中 |
| **OpenTimestamps** | 比特币锚定 | OTS JavaScript | 🟢 低 |
| **DID 集成** | 去中心化身份 | ION/Ceramic | 🟢 低 |

### 阶段 3：完全去中心化（长期）

| 功能 | 目标 | ETA |
|---------|------|-----|
| **区块链注册表** | 以太坊/Solana 链上注册 | 2026 年第四季度 |
| **DAO 治理** | 社区管理 | 2027 年第一季度 |
| **多链支持** | Polygon、Arbitrum、Base | 2027 年第二季度 |
| **法律认可** | 土耳其法院有效性 | 2027-2028 |
| **开发者 API** | 公共 API 端点 | 2026 年第三季度 |

---

## 📊 竞争分析（已更新）

PoArt 定位在完成现有解决方案缺陷的"最佳点"上。

| 功能 | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **成本** | 🆓 免费 | 🆓 | 💰 付费 | ⚠️ 免费增值 | 💰 | 💰 | 💰 | 💰 |
| **拖放 UI** | ✅ 非常简单 | ❌ CLI | ⚠️ 中等 | ⚠️ 中等 | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **多格式导出** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **实时预览** | ✅ 实时 | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **隐私控制** | ✅ 3 种模式 | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **客户端哈希** | ✅ 隐私 | ✅ | ❌ 上传 | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **取证元数据** | ✅ 完整 | ❌ | ❌ | ⚠️ 有限 | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR 验证** | ✅ 即时 | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **速率限制** | ✅ RLS+客户端 | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **区块链锚定** | 🔄 路线图 | ✅ 比特币 | ✅ 以太坊 | ✅ 多链 | ✅ | ✅ | ✅ | ✅ |
| **开源** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **土耳其语支持** | ✅ 原生 | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**图例：**
- ✅ : 完全支持 / 可用
- ⚠️ : 有限 / 在付费计划中
- ❌ : 无 / 不支持
- 🔄 : 在路线图中（开发中）
- 🆓 : 完全免费
- 💰 : 付费 / 需要订阅

### 竞争对手的缺陷，PoArt 的优势

| 缺点 | 竞争对手 | PoArt |
|-------|----------|-------|
| **使用难度** | CLI、API 知识、需要钱包 | 拖放，3 次点击完成 |
| **成本障碍** | $50-500/月订阅 | 100% 免费 |
| **隐私** | 文件上传到服务器 | 客户端，文件永不离开 |
| **取证数据** | 仅时间戳 | IP、位置、设备、时间 - 全部 |
| **土耳其语支持** | 无或非常有限 | 原生语言支持 |
| **开源** | 封闭盒子 | GitHub 上所有代码开放 |

---

## 🧬 协议数据结构（JSON Schema）

**每个 [PoArt] 证书都有以下标准生成的可移植和可验证的 JSON 身份证。**

> **注：** 此身份 JSON 格式是呈现给用户的证书格式。在注册表记录中，使用 `registry.asset` 而不是 `identity.asset_data`（映射：`identity.asset_data` == `registry.asset`）。
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

## 🔬 技术深度：封印算法

### 确定性哈希函数
```javascript
// 辅助函数：将摘要转换为十六进制字符串
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// 将字符串转换为字节数组
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// 规范取证字符串生成（v1.0：固定字段顺序 + UTF-8 + \n 分隔符）
// 阶段 2 注：将过渡到 RFC 8785 (JCS) 的规范 JSON
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal 生成过程（完全确定性）
```javascript
// 1. FileHash 计算（客户端）
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. 取证数据收集（单一时间戳使用）
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // 单一时间戳生成
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // 相同时间戳
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot 创建（使用规范编码）
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal 生成（相同时间戳使用）
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// 掩码辅助函数（IPv4 和 IPv6 支持）
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4 检查
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

### 验证流程（两个级别）

#### Quick Verify（快速验证）
```javascript
// 仅检查文件哈希（快速红旗）
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // 从注册表获取
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // 哈希比较
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ 原始 - 文件哈希匹配"
    };
  } else {
    return {
      valid: false,
      message: "❌ 假冒 - 文件已被篡改"
    };
  }
}
```

#### Full Verify（完整验证）
```javascript
// 重新生成并验证 EvidenceRoot 和 NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // 从注册表获取
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash 检查（快速红旗）
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ 假冒 - 文件哈希不匹配" };
  }

  // 2) 重新生成 EvidenceRoot（使用注册表中存储的取证）
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ 不匹配 - EvidenceRoot 不成立" };
  }

  // 3) 重新生成 NotarySeal（使用相同的 timestamp + signer_sig）
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ 不匹配 - NotarySeal 不成立" };
  }

  // 可选：在阶段 2 中，还使用 attestation_pubkey 验证 signer_sig
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ 签名无效" };

  return { valid: true, message: "✅ 原始 - 完整验证通过" };
}
```

> **重要说明：**
> - **Quick Verify：** 仅检查文件哈希以便快速使用。
> - **Full Verify：** 验证协议的所有层（EvidenceRoot + NotarySeal）。
> - 所有哈希操作都以确定性方式完成，使用固定编码和分隔符。
> - **v1.0 规范化标准：** 固定字段顺序 + UTF-8 编码 + `\n` 分隔符。
> - **阶段 2 计划：** 使用 RFC 8785（JCS - JSON 规范化方案）过渡到规范 JSON。
> - 在掩码模式下，EvidenceRoot 和 NotarySeal 计算使用掩码的取证完成。
> - 整个过程使用单一时间戳（取证 + NotarySeal）；保证确定性。
> - **取证字段名称：** `ip_masked`、`location`、`device`、`timestamp`（代码和注册表完全兼容）。
> - **注册表路径：** `certificate.asset.fingerprints`（与验证代码完全兼容）。
> - **注册表中的 signer_sig：** `proof.signer_sig` 字段是 Full Verify 所需的。
> - SignerSignature 机制将在阶段 2 通过 Solana 钱包适配器激活；在 v1.0 中，可以使用 `attestation_pubkey` 进行验证。

---

## 📈 使用统计（2026 年第一季度目标）

| 指标 | 目标 | 状态 |
|--------|-------|--------|
| **总证书数** | 1,000 | 🔄 进行中 |
| **活跃用户** | 500 | 🔄 进行中 |
| **验证次数** | 5,000 | 🔄 进行中 |
| **正常运行时间** | 99.9% | ✅ 活跃 |
| **平均响应时间** | <200ms | ✅ 最佳 |

---

## 🌍 社区与支持

- **Twitter：** [@Galerilhan](https://twitter.com/Galerilhan)
- **网站：** [ilhanart.org](https://ilhanart.org)
- **电子邮件：** galeri@ilhanart.org

---

## 🙏 贡献者

PoArt 协议在开源社区的贡献下继续发展。

**要贡献：**
1. Fork 仓库
2. 创建功能分支（`git checkout -b feature/amazing-feature`）
3. 提交（`git commit -m 'Add amazing feature'`）
4. 推送（`git push origin feature/amazing-feature`）
5. 开启 Pull Request

### 🛠️ 我们现在需要什么？（呼吁帮助）

PoArt 协议正在寻找以下领域经验丰富的开发人员进行**阶段 2** 开发：

* **Supabase Edge 功能：** 将垃圾邮件保护移至服务器端。
* **Solana Web3.js：** 钱包签名集成。
* **IPFS / Arweave：** 归档和固定服务集成。

> 在添加功能之前，请在"Issues"选项卡中发起讨论。

---

**[PoArt] 艺术证明协议 v1.0**  
*"文化 > 资本"*

## 🧾 许可证

MIT 许可证 © 2026 İlhan 艺术画廊倡议

查看 [![许可证](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) 了解完整条款。

---

## 💬 致谢

![版本](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![安全](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![平台](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![许可证](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**该项目由 [İlhan 艺术画廊] 倡议开发，其源代码为透明起见公开可用。**

**协议 V1.0 // 使用 SHA-512 封印**

*© 2026 İLHAN ART | 保留艺术作品、视觉内容和创意的所有权利。*

---
