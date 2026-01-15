# 📚 术语与概念词汇表
> **"理解本协议的语言，就是理解其愿景。"**

## ⚙️ PoArt取证引擎（PFE）v1.0：核心基础设施

**PoArt取证引擎（PFE）** 是代表[PoArt]协议背后核心逻辑和技术操作的主层。这个"取证引擎"将艺术作品的原始生产数据转化为可验证且不可变的**数字证据**。

### 🧩 为什么叫"PoArt取证"？

- **PoArt（艺术证明）：** 引擎的重点是将数字资产的价值不与投机挂钩，而是与**可验证的生产过程**挂钩。
- **取证（Forensic）验证：**
  - **技术定义：** 一种算法和记录链方法，用于验证生产过程数据（笔触、延时摄影、日志）未被篡改。
  - **哲学层面：** 对抗人工智能的"即时输出"生产；将包含**时间、努力和决策成本**的人类生产转化为可测量的现实。

> 注：区块链（如Solana）集成不是PFE的核心；它将作为单独的**链锚定层（Chain Anchor Layer）** 用于验证/注册目的。

### 🛠️ v1.0技术范围

**PoArt取证引擎（PFE）v1.0** 建立在**3个主要支柱**之上，而非复杂的金融模型：

1. **哈希与封印（Hashing & Sealing）：**  
   PFE确定性地处理证据包中的所有元素（艺术作品文件、视频、JSON/日志、签名等），生成唯一的**NotarySeal**值。

   **核心概念（v1.0）：**
   - **FileHash（作品指纹）：** 从艺术作品文件字节生成的哈希。
   - **EvidenceRoot（证据包根）：** 代表证据包完整性的根摘要（Merkle根或规范清单哈希）。
   - **NotarySeal（最终封印/PFE输出）：** 从EvidenceRoot + 时间 + 签名组合生成的最终封印。

   **公式（对投资者清晰可见）：**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **规范有效载荷定义（v1.0）：**
   
   - **EvidenceRootPayload：**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload：**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > 注：PFE输出指的是**NotarySeal**。**SignerSignature**机制将在第二阶段（通过Solana钱包适配器）激活；当前v1.0使用系统自身的证明签名。证明公钥在注册表的`issuer.attestation_pubkey`字段中发布。

2. **索引（Indexing）存档：**  
   记录哪个钱包、在什么日期、为哪件艺术作品提交了**劳动证明（Labor Proof）**；存入透明且可查询的记录层。  
   *（此层可以是数据库；链集成单独定义为"链锚定层"。）*

3. **验证（Verification）：**  
   当艺术作品的真实性受到质疑时，PFE重新处理原始证据；数学上确定性地测试计算出的**EvidenceRoot / NotarySeal**值是否与存档记录匹配。

---

### 🧮 PoArt价值定理（The Value Theorem）

[PoArt]协议将数字资产的价值（$V$）不与主观市场认知相关联，而是与**生产过程的物理现实**相关联。

人工智能（AI）即时给出结果（$t \to 0$），摧毁了过程。[PoArt]将价值视为**时间、劳动和自主性**组成部分的积累。

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### 变量定义

- **$\int dt$（过程积累）：**  
  价值不是瞬间的"输出"；它是在$t_{\text{start}}$和$t_{\text{end}}$之间积累的**过程**。随着持续时间减少（AI生产），积分结果趋近于0。

- **$P_{\text{labor}}(t)$（瞬时劳动力）：**  
  代表生产时刻消耗的精神和体力努力强度。可证明的努力增加时，被积函数增大。  
  > 注：该术语实际上可以通过"可测量/可证明的劳动信号"进行标准化。

- **$I_{\text{agency}}(t)$（自主性系数）：**  
  生产者承担风险和做出决策的能力。取值在$0$到$1$之间。
  - **AI（$I \approx 0$）：** 执行命令，不承担风险，不付出代价。
  - **人类（$I \to 1$）：** 改变决定，犹豫，承担风险。

- **$U_{\text{irreversible}}$（不可逆转的独特性）：**  
  数字生产中可以撤销（`Ctrl+Z`）；而物理生产中（涂在画布上的颜料、雕刻的大理石、直播中的手势）无法回退。这种**不可逆转性**是在作品中创造"独特性"（非同质化特征）的额外术语。

### 🔎 案例分析：AI"即时输出"vs. 人类"证明过程"

以下场景展示了**PoArt价值定理**在实践中的运作方式，以及为什么AI生产在[PoArt]标准中得分较低。

#### 场景A：用AI在10秒内生产视觉作品

- **持续时间（$\Delta t$）：** $10$秒（几乎没有过程）
- **劳动力（$P_{\text{labor}}$）：** $1$单位（仅命令输入）
- **自主性系数（$I_{\text{agency}}$）：** $0.01$（无风险，无成本）
- **不可逆转性（$U_{\text{irreversible}}$）：** $0$（可逆/可复制）

**结果：**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **评论：** 即使输出完美无瑕；由于没有经历过程且不包含自主性/风险，[PoArt]价值趋近于$0$。

#### 场景B：直播中6小时的物理生产

- **持续时间（$\Delta t$）：** $6$小时（$21{,}600$秒）
- **劳动力（$P_{\text{labor}}$）：** $0.5$单位（体力和脑力努力的连续性）
- **自主性系数（$I_{\text{agency}}$）：** $0.9$（改变决定、承担风险、不可逆转的选择）
- **不可逆转性（$U_{\text{irreversible}}$）：** $>0$（物理痕迹无法撤销）

**结果：**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **评论：** 随着过程延长和自主性（风险）增加，价值累积增长。$U_{\text{irreversible}}$术语是在作品中创造"独特性"（非同质化特征）的额外贡献。

---

### ✅ 结论：证明约束价值（Proof-Bound Value）

该定理将[PoArt]的价值主张从"点赞"或"市场叙事"中移除，并将其与**可证明的生产现实**联系起来。

1. **没有过程就没有价值：**  
   AI在即时输出中（$t \to 0$）摧毁了过程。随着过程窗口缩小，积分结果数学上必然缩小：
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **自主性和风险是乘数：**  
   [PoArt]不仅测量"花费的时间"；还测量该时间内真实的决策、风险和成本层面。没有风险的生产（AI）价值较低：
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **独特性是物理证据，而非营销：**  
   物理生产中的不可逆转痕迹（画布笔触、大理石碎片）超出了数字`Ctrl+Z`逻辑。这种不可逆转性（$U_{\text{irreversible}}$）在本体论上使作品独特化。

> **🔐 总结：** 尽管价值定理作为测量可能看起来不确定（即使在现实生活中无法100%测量），但该公式的目的是展示变量的结构和方向。在AI时代，稀缺的不是"图像"，而是**可证明的劳动、时间和自主性。** [PoArt]测量这种稀缺性并通过**证据包**进行认证。

### 🏛️ "引擎"概念的重要性

从Pump.fun或类似平台产生的代币往往只是**"访问票"**。**PoArt取证引擎（PFE）** 是确定该票保护哪些权利、如何记录劳动以及如何使艺术/科学/技术永久化的**宪法逻辑层**。

> **注：** 我们在Pump.fun上启动该项目的原因是我们没有足够的流动性和追随者数量。使用现有数据在战略上是最正确的举措，尽管质量不是最高的。无论预算和资源如何，在GitHub上定义该引擎的逻辑证明该项目不仅仅是金融投机，而是长期的**软件基础设施**和**数字国家图书馆**愿景。

---

## 🎨 [PoArt] 劳动证明协议（Proof of Art Protocol v1.0）

> **"真实艺术家，真实生产，真实价值。"**

该协议是针对围绕加密生态系统的匿名诈骗者、5分钟内生产的人工智能视觉作品和"拉高出货"文化而开发的**生物学和智力防御机制**。

---

## a) 什么是[PoArt]？（哲学和技术定义）

**艺术证明 [PoArt]；** 是一种机构验证标准，保证区块链上资产背后的价值不基于投机，而是基于可验证的**人类劳动**、**时间**和**体力能量**。

正如比特币通过*"电力和处理器功率"* **（工作量证明）** 产生价值；[PoArt]兼容项目通过*"艺术技能和人类时间"*产生价值。

它消除了Pump.fun和DEX平台上的*"开发者卖出，项目结束"*风险；因为这里的价值不在代码中，而在**生产的连续性**中。

> **[PoArt]不会告诉参与者"相信我们"；它说"这是证据，用你的眼睛看，用你的数学验证。"**

---

## b) [PoArt] 五大支柱标准（The 5 Pillars of Truth）

这5项是项目必须通过的不可操纵过滤器，才能获得[PoArt]印章。

### 1) 实时身份证明（Live Identity Proof）

- **问题：** 加密世界充满了身份不明的匿名创始人（开发者），他们收钱后放弃项目。
- **[PoArt] 解决方案：** 生产者不仅证明身份证，还证明**生产时刻的存在**。这包括不是预先录制的视频，而是与社区互动并满足即时特定请求的直播会话。  
  （例如：*"在画布右角写上今天的日期和当前区块号"*）
- **座右铭：** *"机器人可以制作图片，但机器人不会出汗，不能即兴创作。"*

### 2) 劳动与过程证明（Labor & Process Proof）

- **问题：** 2秒内生产的AI（人工智能）视觉作品与2个月完成的油画在数字世界中受到相同的"jpeg"待遇。
- **[PoArt] 解决方案：** 艺术作品的"怀孕和分娩"过程被记录。草图阶段、颜料层、累计花费的小时以及艺术家创作该作品时经历的物理过程被记录。这为代币增加了**"时间成本"**。资产的生产越困难，其价值越稳固。

### 3) 美学价值证明（Aesthetic Value Proof）

- **问题：** "模因"文化无视美学和艺术深度，只关注即时喜剧，导致短命的"炒作"项目。
- **[PoArt] 解决方案：** 项目必须具备学术艺术标准、色彩理论、构图规则和材料知识（厚涂、纹理等）。内容不应仅仅逗乐；应在观众中激发钦佩并具有**收藏价值**。

### 4) 概念新颖性（Conceptual Novelty）

- **问题：** 数千种相互复制、远离创造力的狗/猫币。
- **[PoArt] 解决方案：** 项目必须建立一座有意义地结合艺术、科学、哲学或技术的新桥梁。  
  （例如：将古典大卫雕塑与加密市场数据结合；通过此处理人类感知"变成石头"的想法，并能够用科学来源支持它。）  
  作品不仅是视觉盛宴；还必须是让人思考**科学、哲学或技术**的智力挑战。

> [!IMPORTANT]
> **参考示例（拉斯帕尔米塔斯效应）：**  
> 在墨西哥与犯罪作斗争的拉斯帕尔米塔斯社区，200多座房屋被改造成巨大的彩虹盛宴。这种美学干预的结果是，社区的犯罪率在一定程度上下降，年轻人开始从事艺术而不是帮派。美学变化重新编码了人们对环境和彼此的尊重（社会凝聚力）。
>
> **期望：** 进入[PoArt]名单的项目；就像上面的例子一样，必须包含超越纯视觉美学的社会学、科学或哲学因果关系。由于"时间"是唯一无法用金钱购买的资产，在该协议中，时间必须作为抵押品进行质押和证明。项目的概念基础必须如此强大和普遍，以至于即使在多年后可能的CTO（社区接管）场景中，社区也可以接管这一遗产，自主地继续项目的创新潜力。

### 5) 非算法自主性（Non-Algorithmic Agency）

- **问题：** 完美但没有灵魂、重复的数字生产。
- **[PoArt] 解决方案：** 人类可以犯错、承担风险并经历情绪波动的独特自主性必须在作品中感受到。笔触中的不确定性、材料的意外反应以及艺术家的即时决定是将作品与"机器生产"区分开来的**生物签名**。

---

## c) 验证与反欺诈机制

该系统确保项目不仅在"开始时"而且"永远"保持可靠和活力。

### 📦 证据包（Evidence Pack - The Digital Twin）

每个[PoArt]认证艺术作品背后都有一个投资者可以下载的加密和时间戳数据包：

- **RAW视频记录：** 生产时刻的不间断原始镜头。
- **元数据分析：** 文件创建日期、使用的设备信息和位置数据。
- **物理参考：** 艺术作品在物理世界中存在的证据  
  （例如：艺术作品旁边的当前报纸或当时的区块链数据）。

> *一致性注释：* "证据包"短语连接到前面章节的**证据包→EvidenceRoot→NotarySeal**链；即包的完整性由可验证的封印表示。

### 🔄 365天续订（The Sustainability Protocol）

- **革命性特征：** 在加密项目中，"开发者"（Dev）将代币推向市场，通常在1-2个月后消失（软跑路）。[PoArt]使这成为不可能。
- **规则：** "认证艺术家"（Verified Artist）状态不是终身的。仅有效**1年**。
- **操作：** 艺术家/开发者每365天必须向社区提供**新的、重大的和可证明的作品**。
- **示例场景：** 您在2026年启动了项目。2027年1月，系统发出"证明期限已到"警告。如果艺术家没有呈现新的展览、新的物理作品或新的技术集成，项目的"信任徽章"就会下降。
- **结果：** 该系统确保**内容永不失去相关性**，投资者永不经历*"开发者还在吗？"*的恐惧。项目变成了一个活生生的工作室。

### 🚩 红旗协议（Red Flag Protocol）

**在社区或算法检测到任何欺诈（AI使用、被盗作品、操纵视频）的情况下：**

1. 证书立即标记为**"作废"（VOID）**。
2. 证据包公开标记为**"假"**。
3. 项目被添加到[PoArt]黑名单。这强化了在去中心化世界中**声誉是唯一货币**的现实。

---

## d) 结论：不是赌场，是博物馆

**Pump.fun和去中心化交易所（DEX）现在不幸地是赌场；灯光闪烁，每个人都追逐快速收益，庄家（诈骗者）总是赢。我们在这里启动项目的原因是缺乏足够的预算和通过直播接触现有受众。**

**[PoArt]是建在这个赌场中间的堡垒。**

- 🎰 赌场基于纸牌游戏；我们基于**物理现实**。
- 🃏 赌场对作弊开放；我们对**透明证据**开放。
- ⏳ 赌场是暂时的；我们专注于**艺术和科学的永恒**。

**使用该协议的代币不仅仅是一个"币"；它是一个背后包含汗水、颜料、代码和哲学的数字股票证书。**
---

## 🗳️ 6) 治理与公共注册表（Governance & Public Registry）

**本节的目的是：将[PoArt]标准从"对人的信任"平面转变为通过注册 + 验证 + 社区监督的可持续公共基础设施。**

### 6.1 公共注册表（Public Registry）

- **公共注册表：** 所有批准的数据记录在`ilhanart.org/registry`（或GitHub注册表）地址。

**注册逻辑（推荐标准 - JSON路径格式）：**

进入注册表的每条记录都携带这些最低可验证核心字段：

- **身份与状态：**
  - `certificate_id`（可读参考）
  - `status`（active / void）
  - `void_reason`（如有）
  - `visibility`（private / masked / public）
  - `created_at`（时间戳）

- **发行机构：**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **艺术作品信息：**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet`（如可能；用于代币持有者身份）
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **取证数据：**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **密码学证据：**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **治理：**
  - `governance.decision`
  - `governance.review_notes`

注册表可以有两层：
- **1)** 人类可读索引（网页列表/搜索/过滤）
- **2)** 机器可读清单（JSON记录；用于PFE验证）

**这里的"记录"通过PFE的证据包→EvidenceRoot→NotarySeal链变得可验证。注册表提供验证目标，而非"声明"。**

---

### 6.2 PoArt认证申请流程

**PoArt认证申请由伊尔汗艺术画廊根据5个PoArt标准进行评估。社区反馈被考虑在内，但最终决定属于策展团队。决定以透明方式解释并记录在ilhanart.org/registry。**

#### 申请流程

**申请：**
- 艺术家/项目提交PoArt认证申请
- 准备证据包（视频记录、元数据、直播链接）
- 申请发送至伊尔汗艺术画廊

**审查（30天）：**
- 画廊团队详细检查证据包
- 检查所有5个PoArt标准：
  1. 实时身份证明
  2. 劳动与过程证明
  3. 美学价值证明
  4. 概念新颖性
  5. 非算法自主性
- 艺术家访谈（可选）

**社区咨询：**
- 证据包在申请过程中公开分享
- 社区可以通过Discord和ilhanart.org/applications提供反馈
- 代币持有者（最低10,000 $CULTURE）可以特别提出建议
- **所有反馈在审查过程中都会被考虑**
- **但最终决定取决于策展评估**

**决定：**
- 画廊批准或拒绝申请
- 决定理由以透明方式解释
- 如果批准 → PoArt认证徽章
- 如果拒绝 → 6个月后可以重新申请

**透明度：**
- 所有申请和决定记录在ilhanart.org/registry
- 决定记录公开发布：
  - 申请日期
  - 审查过程摘要
  - 决定（批准/拒绝）
  - 决定理由（简要说明）
  - 社区反馈摘要（匿名）

#### 为什么策展决定？

**质量控制：**  
PoArt认证状态是具有高标准的徽章。策展评估保证这些标准的维护。

**防止投机操纵：**  
使用Pump.fun代币进行完整的链上治理（例如：Realms、DAO投票）在技术上是不可能的。链下投票系统容易受到鲸鱼操纵和协同攻击。策展决定消除了这种风险。

**操作效率：**  
快速清晰的决策流程，而不是复杂的投票机制。艺术家在30天内得到结果。

**社区参与：**  
社区反馈完全被考虑并影响决策过程。但最终决定属于受保护免受操纵的策展团队。

**未来：**  
一旦项目成熟（2027+），社区咨询机制可以加强。但策展标准保护保持永久。

---

### 6.3 代币效用（Token Utility）

**$CULTURE代币持有者提供的好处：**

**1. 画廊活动优先访问：**
- 伊尔汗艺术画廊实体展览开幕
- 艺术家会面和工作室参观
- 私人收藏观看

**2. PoArt注册表完全访问：**
- 所有认证艺术作品的详细记录
- 证据包的完整版本
- 取证验证工具

**3. NFT铸造优先权：**
- 当PoArt认证作品作为NFT铸造时的白名单访问
- 早期铸造机会
- 特殊收藏NFT

**4. 咨询投票：**
- PoArt认证申请中的咨询权
- 访问社区反馈渠道
- 参与治理讨论

**5. 独家内容：**
- 工作室幕后内容
- 艺术家访谈和过程视频
- 技术文档访问

**注：**  
代币持有者提供咨询投票。最终决定属于策展团队。选择此结构是为了防止鲸鱼操纵和投机攻击。没有质押奖励，因为我们寻求长期文化参与者，而不是短期雇佣兵资本。

---

### 6.4 元数据同步（Metadata Sync）（与物理世界对齐）

- **元数据同步：** 注册表中的技术数据必须与物理资产100%匹配。

**技术上定义"100%匹配"（建议清晰度）：**

- **最低匹配（强制性）：**
  - 注册表的`asset.fingerprints.sha256/sha512`与手头文件的哈希必须**完全相同**。
  - 注册表的`proof.notary_seal`重新生成时（如果证据包存在）必须**完全相同**。

- **物理参考匹配（证据类型）：**
  - 直播中展示的物理作品 + 日期/区块参考等证据必须与证据包一致。

- **隐私合规：**
  - 在`masked`可见性中，IP/位置等字段按照**掩码标准**发布。

---

### 6.5 争议、审查和撤销（Dispute & Revocation）

注册表不仅是"批准"机制；它是**对抗欺诈的活监督**机制。

- 当争议启动时，记录可以进入**"审查"**模式。
- 如果检测到欺诈，则标记为`status: void`并添加理由：
  - `void_reason`（AI使用/盗窃/操纵等）
  - `revoked_at`（撤销时间）
- 撤销决定的来源在注册表中清晰可见：
  - 策展审查/社区争议/取证分析备注（适用者）

> **此部分是"红旗协议"部分中VOID概念在注册表上的对应物。**

---

### 6.6 示例注册表记录（机器可读）
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

> *注：`asset.fingerprints.sha512`和其他哈希值为显示目的而缩短；在实际实现中，使用完整长度的十六进制字符串。*

---

## 7) 🔐 技术封印（NOTARY SEAL）

**由PoArt取证引擎（PFE）v1.0生成的不可动摇的封印算法：**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] 数字公证与取证证据协议（Beta v1.0）

> **"文化大于资本。从今天保护您的艺术作品，将其带到明天。"**

---

## 为什么公开？

真正的安全来自透明度。得益于我们的**公共注册表**系统，世界上任何地方的任何人都可以在几秒钟内验证他们手中的文件是否原创，无需任何权威机构。

---

## 🧩 为什么有多个"可见性模块"？

这是代码中最关键的部分（可见性选择菜单）。这些选项允许用户平衡**"隐私vs.透明度"**：

### 🔒 私有（Private）

- **场景：** 艺术家还不想发布作品，但想加上时间戳来证明"我在这个日期制作了这个"。
- **代码的作用：** 将数据写入数据库，但标记`visibility: "private"`标签。将来编写"公共读取"策略时，通过说`WHERE visibility = 'public'`可以向公众隐藏这些记录。

### 🕶️ 掩码（Masked）

- **场景：** 艺术家想要透明度，但担心找到家庭地址（IP位置）。
- **代码的作用：** JavaScript端的`maskIP`和`maskLoc`函数工作。将IP地址转换为`88.241.***.***`形式，将位置转换为`***/TR`形式，并将审查版本发送到数据库。
- **隐私注意：** 掩码在浏览器中完成；Supabase看不到真实位置。**但是：** 如果使用ipapi.co等第三方API进行位置数据，这些提供商在请求时会看到IP地址。
- **掩码模式下的封印：** EvidenceRoot和NotarySeal计算使用掩码取证数据完成；因此验证保持确定性。

### 🌍 公开（Public）

- **场景：** 完全透明。根据[PoArt]标准，清楚地声明作品在哪里、何时、从哪个网络生产。

---

## 💡 技术创新

PoArt不仅仅是文件上传系统。它是一个在一个锅中融合三个不同技术层并带来新标准的**"取证监管链"（Forensic Chain of Custody）** 引擎。

**本节中描述为"引擎"的层对应于先前术语中的PoArt取证引擎（PFE）核心。**

### 1) 客户端哈希（Client-Side Hashing）（最大隐私）

您的艺术作品文件永远不会上传到服务器。我们基于浏览器（客户端）的引擎在您自己的计算机上计算文件的哈希（数字摘要）。只有此指纹和元数据发送到服务器。

> **隐私注意：** 艺术作品文件不会上传到服务器，因此受到保护。但是，根据所选的可见性模式（private/masked/public）共享取证数据（IP/位置）。

### 2) 取证数据融合（Forensic Data Fusion）（取证力量）

它远不止普通的时间戳。系统将这些数据组合成单个"创世封印"：

- **数字摘要（SHA-512）：** 使用密码学摘要（SHA-512）标准，即使作品的一个像素改变，也会破坏的数字指纹。
- **位置与时间：** 交易发生的毫秒精度日期、国家、城市和地区数据。
- **设备身份：** 操作系统、浏览器和设备类型（用户代理分析）。

---

## 🛡️ 使用案例和好处

如果您是艺术家、作家或设计师，说"我之前做过这个"是不够的，您需要证明它。

**使用PoArt封印的作品：**

- **数学证明：** 如果您的文件的一个像素改变，系统会理解。操纵是不可能的。
- **法律依据：** 作品在什么日期、在哪个城市、从哪个设备封印被记录。
- **即时证书：** 在几秒钟内生成专门为您定制的带有QR码和封印的**"资产身份证书"**。

---

## ⚙️ 系统架构和技术特性

该系统设计在"无服务器"架构上，专注于高性能和可扩展性。

| 层 | 技术 | 描述 |
|----|------|------|
| **密码学** | SHA-256 & SHA-512 | 双层密码学摘要 |
| **数据库** | Supabase (PostgreSQL) | JSONB数据结构，RLS策略 |
| **取证数据** | ipapi.co API | IP/位置/时间三位一体 |
| **渲染** | html2canvas + jsPDF | 客户端PNG/PDF生成 |
| **前端** | Vanilla JavaScript | 零框架依赖 |
| **安全** | 客户端哈希 | 文件永不到达服务器 |

### 突出功能

| 功能 | 详情 | 竞争对手中？ |
|------|------|------------|
| **拖放UI** | 文件拖放，即时预览 | ❌ 大多数没有 |
| **多格式导出** | PNG、JSON、PDF - 一键 | ⚠️ 有限 |
| **实时预览** | 实时证书预览 | ❌ 无 |
| **隐私控制** | Private/Masked/Public选项 | ❌ 无 |
| **客户端哈希** | 文件永不到达服务器 | ✅ 只有少数 |
| **取证元数据** | IP、位置、设备、时间 - 全部 | ❌ 碎片化 |
| **QR验证** | 即时验证QR码 | ⚠️ 有限 |
| **速率限制** | 垃圾邮件保护（RLS + 客户端） | ❌ 大多数没有 |

---

## 🗺️ 路线图："无需信任"的未来

当前版本**(Beta v1.0)** 经过优化，为最终用户提供最大速度、简单界面和免费访问。但我们的最终愿景是过渡到即使数据库管理员（我们）也无法干预的结构。

### 阶段1：Beta v1.0（目前在线）

**基础设施：**
- 云数据库（Supabase）
- 链下注册表（PostgreSQL + IPFS备份）
- 画廊自我证明（集中但透明）

**代币：**
- 平台：Pump.fun
- 流动性：Raydium（自动）
- 治理：仅咨询（社区咨询）

**目的：**
- 速度，消除用户体验障碍
- 提供"无摩擦"安全
- 社区建设

**代币效用（v1.0）：**
- 画廊活动优先访问
- PoArt注册表查看
- 咨询投票权

---

### 🚀 阶段2：去中心化权威（2026 Q2-Q4）

此阶段涵盖从完全"客户端"操作结构到更安全和去中心化结构的过渡。

| 功能 | 带来什么？ | 技术栈 | 预计时间 |
|------|----------|--------|---------|
| **边缘函数插入** | 垃圾邮件阻止 + API密钥安全 | Supabase Edge (Deno) | 2026 Q2 |
| **钱包签名** | 去中心化身份 | Solana钱包适配器 | 2026 Q2 |
| **IPFS/Arweave备份** | 去中心化存档 | IPFS SDK + Pinata | 2026 Q3 |
| **撤销机制** | 假证书撤销 | DB模式更新 | 2026 Q2 |
| **审计日志** | 取证查询记录 | 自定义日志表 | 2026 Q3 |
| **OpenTimestamps** | 比特币锚定 | OTS JavaScript | 2026 Q4 |

**代币治理（v2.0）：**
- 链下投票（Discord/网页） + 钱包签名
- 社区代表选举（前90天）
- 多重签名操作钱包控制
- 加权咨询投票（有鲸鱼上限）

**不可变性：**
- 使用IPFS哈希的注册表备份
- 比特币时间戳锚定
- 跨链验证准备

---

### 阶段3：完全去中心化（2027+）

| 功能 | 目标 | 预计时间 |
|------|------|---------|
| **链上注册表** | Solana链上记录 | 2027 Q1 |
| **增强代币效用** | NFT铸造，高级功能 | 2027 Q1 |
| **多链支持** | Ethereum、Polygon、Base | 2027 Q2 |
| **DID集成** | 去中心化身份 | 2027 Q3 |
| **社区治理** | 加强咨询系统 | 2027 Q4 |
| **法律认可** | 土耳其法院有效性 | 2027-2028 |
| **开发者API** | 公共API端点 | 2027 Q3 |

**治理演变：**
- v3.0：混合模型（策展 + 社区加权）
- 2028+：完全社区治理（可选）
- 策展质量控制始终保持

---

## 🧬 协议数据结构（JSON Schema）

**每个[PoArt]证书都有一个按照以下标准生成的可移植和可验证的JSON身份卡。**

> **注：** 此身份JSON格式是呈现给用户的证书格式。在注册表记录中，使用`registry.asset`而不是`identity.asset_data`（映射：`identity.asset_data` == `registry.asset`）。
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

// 规范取证字符串生成（v1.0：固定字段顺序 + UTF-8 + \n分隔符）
// 阶段2注：将过渡到RFC 8785（JCS）的规范JSON
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal生产过程（完全确定性）
```javascript
// 1. FileHash计算（客户端）
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

// 3. EvidenceRoot创建（使用规范编码）
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal生成（使用相同时间戳）
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// 掩码辅助函数（IPv4和IPv6支持）
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4检查
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6或未知格式
  return "***";
}
```

### 验证流程（两级）

#### 快速验证（Quick Verify）
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
      message: "✅ 原创 - 文件哈希匹配"
    };
  } else {
    return {
      valid: false,
      message: "❌ 假冒 - 文件已被操纵"
    };
  }
}
```

#### 完全验证（Full Verify）
```javascript
// 重新生成并验证EvidenceRoot和NotarySeal
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // 从注册表获取
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash检查（快速红旗）
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ 假冒 - 文件哈希不匹配" };
  }

  // 2) 重新生成EvidenceRoot（使用注册表中存储的取证）
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ 不匹配 - EvidenceRoot不成立" };
  }

  // 3) 重新生成NotarySeal（使用相同时间戳 + signer_sig）
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ 不匹配 - NotarySeal不成立" };
  }

  // 可选：在阶段2还用attestation_pubkey验证signer_sig
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ 签名无效" };

  return { valid: true, message: "✅ 原创 - 完全验证通过" };
}
```

> **重要说明：**
> - **快速验证：** 仅检查文件哈希以供快速使用。
> - **完全验证：** 验证协议的所有层（EvidenceRoot + NotarySeal）。
> - 所有哈希操作以确定性方式完成，使用固定编码和分隔符。
> - **v1.0规范化标准：** 固定字段顺序 + UTF-8编码 + `\n`分隔符。
> - **阶段2计划：** 使用RFC 8785（JCS - JSON规范化方案）过渡到规范JSON。
> - 在掩码模式下，EvidenceRoot和NotarySeal计算使用掩码取证完成。
> - 整个过程中使用单一时间戳（取证 + NotarySeal）；确保确定性。
> - **取证字段名：** `ip_masked`、`location`、`device`、`timestamp`（代码和注册表完全兼容）。
> - **注册表路径：** `certificate.asset.fingerprints`（与验证代码完全兼容）。
> - **注册表中的signer_sig：** `proof.signer_sig`字段是完全验证所必需的。
> - SignerSignature机制将在阶段2通过Solana钱包适配器激活；在v1.0中，可以使用`attestation_pubkey`进行验证。

---

## 📊 竞争对手分析（更新版）

PoArt定位于完成现有解决方案缺陷的"最佳点"。

| 功能 | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **成本** | 🆓 免费 | 🆓 | 💰 付费 | ⚠️ 免费增值 | 💰 | 💰 | 💰 | 💰 |
| **拖放UI** | ✅ 非常简单 | ❌ CLI | ⚠️ 中等 | ⚠️ 中等 | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **多格式导出** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **实时预览** | ✅ 实时 | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **隐私控制** | ✅ 3种模式 | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **客户端哈希** | ✅ 隐私 | ✅ | ❌ 上传 | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **取证元数据** | ✅ 完整 | ❌ | ❌ | ⚠️ 有限 | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR验证** | ✅ 即时 | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **速率限制** | ✅ RLS+客户端 | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **区块链锚定** | 🔄 路线图 | ✅ 比特币 | ✅ 以太坊 | ✅ 多链 | ✅ | ✅ | ✅ | ✅ |
| **开源** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **土耳其语支持** | ✅ 原生 | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**图例：**
- ✅ : 完全支持/可用
- ⚠️ : 有限/付费计划中
- ❌ : 无/不支持
- 🔄 : 路线图中（开发中）
- 🆓 : 完全免费
- 💰 : 付费/需要订阅

### 竞争对手的弱点，PoArt的优势

| 弱点 | 竞争对手 | PoArt |
|------|----------|-------|
| **使用难度** | CLI、API知识、需要钱包 | 拖放，3次点击完成 |
| **成本障碍** | $50-500/月订阅 | 100%免费 |
| **隐私** | 文件上传到服务器 | 客户端，文件永不离开 |
| **取证数据** | 仅时间戳 | IP、位置、设备、时间 - 全部 |
| **土耳其语支持** | 无或非常有限 | 原生语言支持 |
| **开源** | 黑盒 | GitHub上所有代码开放 |

---

## 📈 使用统计（2026 Q1目标）

| 指标 | 目标 | 状态 |
|------|------|------|
| **总证书数** | 1,000 | 🔄 进行中 |
| **活跃用户** | 500 | 🔄 进行中 |
| **验证次数** | 5,000 | 🔄 进行中 |
| **正常运行时间** | 99.9% | ✅ 活跃 |
| **平均响应时间** | <200ms | ✅ 最佳 |

---

## 🌍 社区与支持

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **网站:** [ilhanart.org](https://ilhanart.org)
- **电子邮件:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 贡献者

PoArt协议在开源社区的贡献下继续发展。

**贡献方式：**
1. Fork仓库
2. 创建功能分支（`git checkout -b feature/amazing-feature`）
3. 提交更改（`git commit -m 'Add amazing feature'`）
4. 推送到分支（`git push origin feature/amazing-feature`）
5. 开启Pull Request

### 🛠️ 我们现在需要什么？（寻求帮助）

对于PoArt协议**阶段2**开发，我们期待在以下领域有经验的开发者的贡献：

* **Supabase边缘函数：** 将垃圾邮件保护移至服务器端。
* **Solana Web3.js：** 钱包签名集成。
* **IPFS / Arweave：** 存档和固定服务集成。
* **社区工具：** Discord机器人、投票系统、分析仪表板。

> 在添加功能之前，请在"Issues"选项卡中开始讨论。

---

## 💬 最后说明

### Pump.fun与现实

该项目在Pump.fun上启动是因为：
- ✅ 流动性访问（Raydium自动迁移）
- ✅ 现有社区访问
- ✅ 低启动成本

但让我们澄清：
- **代币价格**不是艺术成功的指标
- **运营预算**的代币价值很重要（画廊、展览、基础设施）
- **成功指标：** 认证艺术作品 + 社区参与 + 实体访客

### 治理与去中心化

**v1.0现实（2026）：**
- 注册表：链下（PostgreSQL + IPFS备份）
- 证明：画廊自签名（集中但透明）
- 治理：仅咨询（策展最终决定）
- 代币效用：画廊访问 + 注册表 + NFT优先权

**v2.0+愿景（2027+）：**
- 注册表：链上（Solana）
- 签名：基于钱包（去中心化）
- 治理：混合（社区咨询 + 策展质量）
- 代币效用：增强功能 + 高级访问

此结构在早期阶段提供**运营效率**和**质量控制**，同时为未来增加**社区参与**保持开放路径。

---

**[PoArt] 艺术证明协议 v1.0**  
*"文化 > 资本" // Culture > Capital*

## 🧾 许可证

MIT许可证 © 2026 伊尔汗艺术画廊倡议

查看 [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) 了解完整条款。

---

## 💬 致谢

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**该项目由[伊尔汗艺术画廊]倡议开发，源代码为透明度而公开。**

**协议 V1.0 // 用SHA-512封印。**

*© 2026 伊尔汗艺术 | 保留艺术作品、视觉作品和创意的所有权利。*

---
