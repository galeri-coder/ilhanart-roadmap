---
title: "伊尔汗艺术协议 (Ilhan Art Protocol)"
version: "1.0 (稳定版)"
status: "HARD_LOCKED"
integrity: "SHA-512"
ecosystem: "[PoArt] + [FPP]"
last_updated: "2026-01-07"
---

# 📜 协议术语与技术词汇 (Protocol Terminology & Technical Lexicon)
> **协议版本:** 1.0 (稳定版)  
> **网络愿景:** 2025 → 3000 档案体系  
> **生态系统:** [PoArt] + [FPP]  
> **状态:** **HARD_LOCKED**（活动文档）  
> **完整性:** 采用 SHA-512 封印（兼容数字公证）

---

## 🏛️ 1）协议支柱 (Pillars of the Protocol)

### [PoArt] 艺术证明协议 (Proof of Art)
* **定义:** 核心协议，不仅验证艺术作品的最终成果，还验证整个创作过程的技术数据。  
* **解决问题:** 生成式人工智能的崛起使真实人类劳动难以验证，艺术的内在价值被削弱。  
* **工作方式:** 艺术家提交包含创作各阶段的 **证据包 (Evidence Pack)**，协议通过时间戳将其上链封存。  
* **示例:** 一幅耗时 40 小时的画作，包含视频日志、加速影像和数字指纹，证明结果和 40 小时的人类努力。

---

### [FPP] 基础支柱协议 (Foundational Pillar Protocol)
* **定义:** 构建生态系统的经济与社会“支柱”，奖励忠诚、持续性与贡献。  
* **解决问题:** 防止投机资本控制治理权。  
* **工作方式:** 治理权重取决于*持有稳定性*与*持有时长*，而非财富。  
* **示例:** 今天持有 1,000,000 代币的“鲸鱼”，可能不如连续持有 100 枚代币一年的“赞助人”拥有更高的投票权。

---

## 👥 2）角色与实体 (Roles & Entities)

定义“谁做什么”，消除模糊与滥用。  

- **艺术家 (Artist):** 负责生成 [PoArt] 证据包并进行年度验证。  
- **赞助人 (Patron):** 通过 [FPP] 的忠诚和贡献获得影响力；参与否决与策展。  
- **验证者 (Validator):** 审查证据包、标记不一致、协助异议处理。  
- **数字公证人 (Digital Notary):** 自动合约，验证共识、哈希和时间戳并封印至公共登记册。  
- **公共登记册 (Public Registry):** 永久记录层，显示 Verified / Legacy / Revoked 状态。  
- **证据存储 (Evidence Storage):** 离链存储于 IPFS / Arweave，仅加密根上链。

---

## 📊 3）经济与治理指标 (Economic & Governance Metrics)

### 3.1）时间周期 (Epoch & Time Windows)
定义治理与验证的时间维度。

| 类型 | 时长 | 目的 |
|:--|:--|:--|
| **运行周期 (Operational Epoch)** | 7 天 | 常规更新、日志与评分 |
| **关键防护窗口 (Guard Window)** | 30 天 | 抵御短期资本注入操控 |
| **完整性周期 (Integrity Cycle)** | 365 天 | 通过证据包进行年度验证 |

---

### 3.2）时间加权平均余额 (TWAB)
**数学模型:**  
$TWAB = \dfrac{\sum_{i=1}^{n}(Balance_i \times \Delta t_i)}{\sum_{i=1}^{n}\Delta t_i}$

**可选原始指标:**  
$TWA = \sum_{i=1}^{n}(Balance_i \times \Delta t_i)$

* **作用:** 衡量价值在系统中停留的时间与数量。  
* **效果:** 抑制“闪电”式影响；最后时刻的代币购买几乎不影响投票。

---

### 3.3）投票权函数 (Voting Power Function)
$VotingPower = f(TWAB, EpochRules, StatusTier)$

* **防护窗口影响:** 投票资格回溯 30 天。  
* **结果:** 时间的重要性高于财富的突增。

---

### 3.4）对数权力评分 (Logarithmic Power Scoring)
$Score = \log_{10}(TWAB + 1)$  
$VotingPower = Score \times g(EpochRules, StatusTier)$

| TWAB | 对数分数 | 治理权力 |
|:--|:--|:--|
| 10 | 1.04 | 入门级 |
| 1,000 | 3.00 | 中等影响力 |
| 1,000,000 | 6.00 | 上限平台期 |

> **模拟:**  
> 可通过 [PoArt 模拟控制台 (Simulation Console)](https://galeri-coder.github.io/ilhanart-protocol/[PoArt]/) 查看实时计算。

---

## 🛡️ 4）安全与验证 (Security & Validation)

### 4.1）千年金库 (Millennium Vault)
* **定义:** 最高级信誉仓库，资产锁定 1 年。  
* **目的:** 通过验证稳定性来维护长期愿景（2025 → 3000）。  
* **访问:** 仅持有 ≥ 1 年并拥有 [FPP] “支柱”身份者可参与关键投票。

---

### 4.2）证据包 (Evidence Pack)
验证 [PoArt] 的强制性技术数据集。

#### 必要组件：三位一体证明
1. **实时日志:** 创作过程的实时视频与服务器日志。  
2. **过程加速影像:** 从第一笔到最后一笔。  
3. **数字指纹:** 艺术家钱包签名的哈希确保真实性。  

#### 附加证明层
4. **采集清单:** 设备、分辨率、帧率与校验和。  
5. **Merkle 根 / 哈希链:**  
   $EvidenceRoot = MerkleRoot(AllFiles)$  
   所有文件折叠为一个根值，上链封印“唯一真相”。  
6. **随机挑战帧:** 随机人工验证防止伪造。  

* **结果:** 提供不可辩驳的技术证明，表明作品由人类创作。

---

### 4.3）Sybil 与闪电贷款防御
* 结合 TWAB 与防护窗口，使短期资本无效。  
* 防止机器人或贷款瞬时操控治理。

---

### 4.4）数字公证封印 (Digital Notary Seal)
$NotarySeal = Hash(EvidenceRoot + VoterConsensus + TimeStamp)$  

* 验证 [PoArt] 与 [FPP] 的完整性。  
* 封印至公共登记册。  
* 消除中心化或主观审查。  
* **遗产效应 (2026–3000):** 每件公证作品成为可验证的文化档案。

---

## 🏛️ 5）验证与持久性 (Validation & Persistence)

### 5.1）365天冷钱包连续验证
**定义:** 资产必须在验证的冷钱包中（如 Ledger, Trezor）连续保持 365 天。

**解决问题:**
1. 洗盘交易  
2. 投机压力  
3. 热钱包安全漏洞  

#### v1.0 更新 — “惩罚阶梯 (Penalty Ladder)”
逐步惩罚机制，兼顾严格与人性化。

**第一次违规 (未满365天):**  
$EffectiveTWAB = TWAB \times 0.20$

**第二次违规:**  
$EffectiveTWAB = TWAB \times 0.05$

**第三次:** 状态 = **撤销 (Revoked)**

> 防止“快进快出”的操控，同时保护真实用户进度。

#### 安全转移例外 (Move Permit / Time-Lock)
合法转移时：  
- 提交 **转移许可 (Move Permit)** 请求  
- 应用短期 **时间锁 (Time-Lock)**  
## 🗳️ 6）去中心化监督 (Decentralized Supervision)

### 6.1）社区否决机制 (Community Veto Mechanism, 40% 阈值)
* **定义:** 民主性安全阀，允许合格少数否决提案。  
* **双重锁定条件 (v1.0):**  
  - **法定人数 (Quorum):** 需 ≥25% 参与率  
  - **否决触发 (Veto Trigger):** 活跃权重总量 ≥40%  

**防护对象:**
1. Sybil 攻击  
2. 合谋操纵  
3. 投票贿赂  

> 示例: 如果验证者标记某 AI 生成作品为违规，只要 40% 活跃 TWAB 权重投否决，该提案将无法通过。

---

### 6.2）紧急治理 / 回退委员会 (Emergency Governance / Fallback Council)
防止参与率过低时的治理僵局。  

$Deadlock = (ParticipationRate < 25\%) \land (ProposalTimeout > 7\,days)$

若 `Deadlock = TRUE`:  
1. 前 10% “厚涂层 (Impasto)” 成员组成回退委员会。  
2. 决策需 ≥⅔ 共识。  
3. 必须在 30 天内由社区公投批准。  
4. 所有行动记录在 **紧急分类账 (Emergency Ledger, SHA-512)** 中。

---

## ⚙️ 7）米开朗基罗框架 (The Michelangelo Framework, Meritocracy Engine)

### 7.1）米开朗基罗哲学 (Michelangelo Philosophy)
* **定义:** 一种以文化贡献替代财富的排名与声誉系统。  
* **口号:** “你不能用金钱登顶。”  
* **目的:** 用努力取代富豪榜，建立基于劳动与文化的正当性。

---

### 7.2）身份等级公式 (Status Formula)
$Status = HoldingTime \times CulturalContribution$

- **HoldingTime:** 连续持有时间（天数）。  
- **CulturalContribution:** 包括翻译、策展、基础设施建设、教育等。  

**解决问题:** 鼓励经济与智识劳动并行的参与模式。

---

### 7.3）文化贡献领域 (Cultural Contribution Domains)

| 领域 | 描述 | 示例积分 |
|:--|:--|:--|
| 翻译 | 艺术、哲学、科学文献 | +4,500 |
| 策展 | 档案质量控制与监督 | +2,000 |
| 基础设施 | 代码、文档、维护 | +3,000 |
| 教育 | 公共讲座、媒体传播 | +1,500 |

> 综合权重每季度通过 [FPP] 重新计算，以保持公平。

---

### 7.4）声誉衰减 (Status Decay)
非活跃用户的声誉会随时间指数衰减：  

$StatusDecay = e^{-\lambda t}$  

其中 λ = 0.0005 / 天 (v1.0)。  

> 保持排名动态自清理，防止长期休眠占位。

---

## 📊 8）文化乘数与等级层级 (Cultural Multipliers & Ranking Levels)

### 8.1）文化乘数 (Cultural Multiplier)
* **定义:** 对为生态增长做出贡献者的最终加权奖励。  
* **领域:**  
  - 翻译  
  - 策展  
  - 基础设施  
  - 教育  
  - 治理参与  

数学模型：  
$FinalScore = BaseScore \times (1 + CulturalMultiplier)$

---

### 8.2）等级层级 (Rank Tiers)

| 等级 | 排名范围 | 权限 |
|:--|:--|:--|
| **传奇 (Legendary)** | 前 10 名 | 否决 + 战略投票权 |
| **高级 (Senior)** | 前 50 名 | 委员会参与权 |
| **资深 (Veteran)** | 前 100 名 | 审核与提案权 |
| **成员 (Member)** | 100 名外 | 基础参与权 |

> 等级根据活跃度与贡献流动态调整。

---

## 📈 9）阈值与网络指标 (Cut-off Thresholds & Network Metrics)

### 9.1）进入门槛 (Entry Thresholds)

| 类别 | 所需积分 | 描述 |
|:--|:--|:--|
| 传奇 (Legendary) | ≥100,000 | 完全治理权 |
| 前 100 | ≥45,000 | 积极治理参与者 |
| 入门 (Entry) | ≥250 | 基础门槛 |

**目标:** 确保网络增长时影响力保持比例分配。

---

### 9.2）网络 TWAB (Global Stability Index)
* **定义:** 所有参与者 TWAB 的聚合值。  
* **含义:** TWAB 越高，治理越难被操控。  
* **实时指标:** 每 24 小时更新一次 [PoArt] 新记录。
## 🎨 10）智识框架 (Intellectual Framework)

### 10.1）智识工作量证明 (IPOW — Intellectual Proof of Work)
* **定义:** 评估超越金融质押的高价值人类劳动。  
* **机制:** 奖励智识、创意与基础设施产出。  
* **示例:**  
  - 持有 1,000,000 代币但无贡献 → 等级低  
  - 持有 100 代币但持续翻译文档 → 等级高  

---

### 10.2）智识诚信过滤器 (Intellectual Honesty Filter)
* **定义:** 测量投票者在投票前是否真正理解提案内容。  
* **v1.0 模式:**  
  - **A)** 用 100 字以内总结提案  
  - **B)** 选择 2 个风险 + 提供 1 个理由  
  - **C)** 提交 1 个反对论点  

> 评估理解力而非记忆力；防止 AI 垃圾投票与盲目表决。

---

## 🛡️ 11）高级 Sybil 抵御机制 (Advanced Sybil Resistance)

### 11.1）闸机机制 (Turnstile Mechanism)
* **定义:** 设置最低进入门槛，防止零成本创建机器人账户。  
* **标准 (v1.0):** 250 ILHAN 代币。  
* **理念:** “闸机，而非高墙。”  
* **目的:** 增加经济摩擦，使大规模 Sybil 攻击变得不理性。  
* **示例:** 若有 10,000 个机器人钱包，需耗费 2.5M 代币，攻击成本过高而无意义。

---

### 11.2）僵尸钱包过滤器 (Zombie Wallet Filter)
* **定义:** 要求钱包定期通过签名心跳确认活跃状态。  
* **规则:** 非活跃钱包无论得分多少都会从全局注册表移除。  
* **目的:** 保证网络由*活跃参与者*构成。  
* **频率:** 默认每 365 天一次，可随 Epoch 规则调整。

---

## 🧬 12）代际传承与治理 (Generational Legacy & Governance)

### 12.1）代际继承 (Generational Inheritance)
* **定义:** 保持连续活跃 ≥4 年（1460 天）的传奇级成员可指定合法继承人。  
* **目的:** 防止因成员离世或失活导致文化与治理价值消失。  
* **实施:**  
  - 继承仅在连续 4 年证明活跃后生效。  
  - 继承验证通过多签名上链公证。

---

### 12.2）议会治理权 (Parliamentary Governance Rights)

| 等级 | 角色 | 权限 |
|:--|:--|:--|
| **厚涂层 (Impasto, ≥100k)** | 创始 / 宪法委员会 | 制定协议战略层方向 |
| **纹理层 (Texture, 50k–99k)** | 高级策展人 | 管理策展与审核 |
| **底漆层 (Primer, <50k)** | 普通成员 | 提案输入与小型投票 |

> 用结构化的精英民主取代混乱的民粹主义。

---

## 🌍 13）文化特权层与现实整合 (Cultural Privilege Layers & Real-World Integration)

> **说明:** 这些特权属于 2026–2030 混合物理-数字生态路线图的一部分。

---

### 13.1）年度展览权 (Annual Exhibition Right)
* **定义:** 高分艺术家或赞助人每年可获得伊尔汗艺术馆 7 天展期。  
* **目的:** 让展览机会民主化，消除经济门槛。  
* **机制:**  
  - 通过链上日历预约。  
  - 展期依据声誉而非资本分配。

---

### 13.2）动态艺术定价 (Dynamic Art Pricing, JSON-Linked Discounts)
* **定义:** 基于文化地位的动态折扣定价 API。  
* **结构:**  
  - 传奇 (Legendary) → 50%+  
  - 赞助人 (Patron) → 30%  
  - 成员 (Member) → 10%  
* **理念:** “无议价，唯实力。”

---

### 13.3）物理生态整合 (Physical Ecosystem Integration)
* 合作伙伴: 书店、咖啡馆、文化中心等。  
* 通过二维码扫描验证身份并领取现实特权。  
* 使用轻量 JSON API 实时验证。

---

### 13.4）劳动优先于资本 (Labor Over Capital, Meritocratic Access)
* **原则:** 在特权分配中，人类劳动比纯资本更有价值。  
* **数学模型:**  
  $ClaimRight \propto CulturalScore + \log_{10}(Balance)$  
* **示例:**  
  - 贡献者 A → 持有 250 代币并持续创作 → 高 ClaimRight  
  - 持币者 B → 持有 100,000 代币但无贡献 → 低 ClaimRight  

> 将体系从资本统治转变为*劳动统治 (Laborocracy)*。
## 🧩 14）状态机：记录生命周期 (State Machine, Lifecycle of a Record)

### 流程图 (Process Flow)
一个 [PoArt] 记录 + [FPP] 状态遵循不可逆流程：

1. **草稿 (Draft)** → 本地创建  
2. **已提交 (Submitted)** → 上传等待验证  
3. **审核中 (Under Review)** → 验证者检查证据  
4. **质疑中 (Challenged)** → 异议提出  
5. **已验证 (Verified)** → 由数字公证人 (Digital Notary) 加封  
6. **续签提醒 (Renew Due)** → 年度心跳提醒  
7. **遗产档案 (Legacy Archive)** → 过期归档  
8. **撤销 (Revoked)** → 多次违规或被否决  

---

### 状态转换规则 (State Transition Rules)

| 从 | 到 | 条件 |
|:--|:--|:--|
| Draft | Submitted | 艺术家上传完成 |
| Submitted | Under Review | 验证者接受 |
| Under Review | Verified | 共识 ≥ 66% |
| Under Review | Challenged | 提出异议 |
| Challenged | Revoked | 异议成立 |
| Challenged | Verified | 社区推翻否决 |
| Verified | Legacy | 心跳过期 |
| Legacy | Revoked | 审计失败 |

> 允许所有链上记录实现“我现在处于何阶段”的透明跟踪。

---

## 🔗 15）最小上链，最大离链 (Minimal On-chain / Maximal Off-chain)

### 上链数据 (On-chain Data)
- `EvidenceRoot` (Merkle 根)  
- `NotarySeal`  
- `TimeStamp`  
- `Signer` (签名者 / 艺术家或持有者)  
- `Status` (Verified / Legacy / Revoked)  
- `Permit` 记录 (转移许可 / 继承链接)

### 离链数据 (Off-chain Data)
- 原始视频  
- 加速影像  
- 技术日志  
- 元数据与清单  
- 大型档案 (IPFS / Arweave)

**目标:** 保证可验证性而不造成区块链膨胀。  
**完整性:** 可按请求执行 SHA-512 校验。

---

## 🏛️ 16）上诉与异议机制 (Appeals / Authority & Objection Mechanism)

**目的:** 确保系统具备公平性、透明性与程序正义。

---

### 16.1）核心原则 (Core Principles)
- **基于证据:** 上诉必须包含可验证数据。  
- **无情绪偏见:** 主观或诽谤性声明自动驳回。  
- **透明:** 所有上诉事件具时间戳并公开记录。  
- **冻结协议:** 被争议的证据包在调查期间上锁。

---

### 16.2）社区保障 (Community Safeguards)
- **否决阈值:** 40% 活跃 TWAB 权重。  
- **法定人数:** 最低参与 25%。  
- **反 Sybil 门槛:** 闸机机制 + 质押验证。  
- **AI 过滤:** 自然语言理由检测防止垃圾上诉。

---

### 16.3）上诉生命周期 (Appeal Lifecycle)
1. **发起上诉 (Appeal Initiated)** → 验证者或成员提出。  
2. **证据冻结 (Evidence Freeze)** → 相关文件锁定。  
3. **社区审查 (Community Review)** → 启动否决 / 法定程序。  
4. **决议投票 (Resolution Vote)** → 为期 7 天。  
5. **执行决策 (Decision Execution)** → 以 SHA-512 封印。

> 防止隐性审查与任意权力滥用。

---

## 🧨 17）威胁模型与对策 (Threat Model & Countermeasures)

| 威胁类型 | 对策 |
|:--|:--|
| Sybil 攻击 | 闸机机制 + 僵尸过滤 + 法定人数 |
| 闪电贷款操纵 | TWAB + 防护窗口 + 对数评分 |
| 鲸鱼主导 | 对数权重 + 时间加权平衡 |
| 洗盘交易 | 冷钱包验证 + 惩罚阶梯 |
| 合谋操控 | 否决 + 透明分类账 |
| 数据篡改 | EvidenceRoot + SHA-512 + NotarySeal |
| 投票贿赂 | 时间锁 + 权重法定验证 |
| 深度伪造 | 随机挑战帧 + 哈希链 |

> 每项防御机制都在 [FPP] 下定义并进行版本控制。

---

## ⚖️ 18）最终宣言：全球治理蓝图 (Final Word — A Blueprint for Global Governance)

> *“艺术是原型，治理是画布。”*

由 [PoArt] 与 [FPP] 共同构建的体系证明，  
同样的数学结构既能守护文化真相，也能修复民主制度。

---

### 18.1）终结富豪统治 (End of Plutocracy)
* **定义:** 由财富主导而非贡献主导的体系。  
* **协议回应:**  
  - 对数评分限制资本影响力。  
  - 时间与劳动成为合法性核心。  
* **原则:** 拥有 ≠ 创造；贡献定义合法性。

---

### 18.2）精英议会 (Meritocratic Parliament)
* 替代民粹与资本政治。  
* 赋权于理解协议与执行 IPOW 的人。  
* 将治理转变为一种*技艺*而非人气竞赛。

---

### 18.3）选举完整性 (Electoral Integrity, SHA-512 Security)
* **闸机机制 (Turnstile):** 防止机器人虚假公民扩张。  
* **TWAB:** 取消短期转账与买票效应。  
* **否决 + 法定机制:** 确保少数监督权。  

> 一部新型数字宪法，抵御操纵与篡改。

---

### 18.4）宣言：拯救未来 (Manifesto — Saving the Future)
此协议不仅是艺术体系的设计，  
更是未来千年的治理原型。  

它旨在构建这样的社会：  
- 经验证的努力 > 空洞财富  
- 长期愿景 > 即时满足  
- 数学公平 > 政治偏见  

> **“在自动化时代，人类的价值证明在于其创造的意愿。”**

---

## 📅 19）路线图与未来笔记 (Roadmap & Future Notes)

| 阶段 | 年份 | 重点 |
|:--|:--|:--|
| **v1.0** | 2026 | 核心验证与证明机制（当前规范） |
| **v1.1** | 2027 | 公共注册 API 与模拟控制台 |
| **v1.2** | 2028 | 合作伙伴整合 (POS / QR 系统) |
| **v2.0** | 2030 | 自动治理 + 跨协议索引机制 |

> 2026 → 3000 的时间线构成 “伊尔汗艺术千年愿景”，  
> 一个为数世纪持续性设计的文化、经济与伦理体系。

---

## 🔐 哈希签名 (Hash Signature, v1.0 Hard-Locked)


- 社区监督保持活跃  
- 仅记录许可与新地址关联上链
