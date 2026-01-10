# 📚 用語・概念用語集
> **「このプロトコルの言語を理解することは、そのビジョンを理解することである。」**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: コアインフラストラクチャ

**PoArt Forensic Engine (PFE)** は、[PoArt]プロトコルの背後にある中心的なロジックと技術的な動作を表すメインレイヤーです。これは、芸術作品の生の制作データを取得し、検証可能で不変な**デジタル証拠**に変換する「フォレンジックエンジン」です。

### 🧩 なぜ「PoArt Forensic」なのか?

- **PoArt (Proof of Art):** エンジンの焦点は、デジタル資産の価値を投機ではなく、**実証可能な制作プロセス**に結び付けることです。
- **Forensic (フォレンジック検証):**
  - **技術的定義:** 制作プロセスのデータ(筆致、タイムラプス、ログ)が改ざんされていないことを検証するためのアルゴリズムと記録チェーンのアプローチ。
  - **哲学的レイヤー:** AIの「即座の出力」生産に対して、**人間の時間、努力、意思決定コスト**を測定可能な現実に変換するという主張。

> 注意: ブロックチェーン統合(例: Solana)はPFEのコアではありません; 検証/登録目的のために**Chain Anchor Layer**として別途定義されます。

### 🛠️ 技術的範囲 v1.0

**PoArt Forensic Engine (PFE) v1.0** は、複雑な金融モデルではなく、以下の**3つの主要な柱**に基づいて構築されています:

1. **Hashing & Sealing (封印):**  
   PFEは、Evidence Pack内のすべての要素(作品ファイル、ビデオ、JSON/ログ、署名など)を決定論的に処理し、一意の**NotarySeal**値を生成します。

   **中核概念 (v1.0):**
   - **FileHash (作品フィンガープリント):** 作品ファイルのバイトから生成されたハッシュ。
   - **EvidenceRoot (証拠パックルート):** Evidence Packの完全性を表すルートダイジェスト(Merkleルートまたは正規マニフェストハッシュ)。
   - **NotarySeal (最終封印 / PFE出力):** EvidenceRoot + 時間 + 署名の組み合わせから生成される最終封印。

   **数式 (投資家に明確に表示):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **正規ペイロード定義 (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > 注意: PFE出力として参照される値は**NotarySeal**です。**SignerSignature**メカニズムはフェーズ2(Solana Wallet Adapterを使用)で有効化されます; 現在のv1.0では、システム独自の証明署名が使用されます。証明公開鍵は`issuer.attestation_pubkey`フィールドの下でレジストリに公開されます。

2. **Indexing (アーカイブ):**  
   どのウォレットが、どの日付に、どの作品のために**Proof of Labor (労働の証明)**を透明で照会可能なレジストリレイヤーに提出したかを記録します。  
   *(このレイヤーはデータベースである可能性があります; チェーン統合は「Chain Anchor Layer」として別途定義されます。)*

3. **Verification (検証):**  
   作品の真正性が疑問視されると、PFEは生の証拠を再処理します; 計算された**EvidenceRoot / NotarySeal**値がアーカイブ記録と一致するかを数学的にテストします。

---

### 🧮 PoArt 価値定理 (The Value Theorem)

[PoArt]プロトコルは、デジタル資産の価値($V$)を主観的な市場認識ではなく、**制作プロセスの物理的現実**に結び付けます。

人工知能(AI)は、結果を即座に提供することでプロセスを破壊します($t \to 0$)。しかし、[PoArt]は、価値を**時間、労働、意志**のコンポーネントの蓄積として扱います。

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### 変数の定義

- **$\int dt$ (プロセスの蓄積):**  
  価値は即座の「出力」ではありません; それは$t_{\text{start}}$と$t_{\text{end}}$の間に蓄積される**プロセス**です。期間が減少すると(AI生産)、積分結果は0に近づきます。

- **$P_{\text{labor}}(t)$ (瞬間的労働力):**  
  生産の瞬間に費やされる精神的・身体的努力の強度を表します。実証可能な努力が増加すると、被積分関数が成長します。  
  > 注意: この項は、実際には「測定可能/実証可能な労働信号」を通じて正規化できます。

- **$I_{\text{agency}}(t)$ (意志係数):**  
  生産者のリスクを取り、意思決定を行う能力。$0$と$1$の間の値を取ります。
  - **AI ($I \approx 0$):** コマンドを実行し、リスクを取らず、コストを支払いません。
  - **人間 ($I \to 1$):** 決定を変更し、躊躇し、リスクを取ります。

- **$U_{\text{irreversible}}$ (不可逆的独自性):**  
  デジタル生産では元に戻す(`Ctrl+Z`)ことが可能ですが、物理的生産(キャンバスに塗られた絵の具、彫られた大理石、ライブ配信でのジェスチャー)では後戻りはありません。この**不可逆性**は、作品に「独自性」(非代替性)を生み出す追加項です。

### 🔎 ケース分析: AI「即座の出力」vs. 人間「証明されたプロセス」

次のシナリオは、**PoArt 価値定理**が実際にどのように機能し、なぜAI生産が[PoArt]基準で低いスコアを得るかを示しています。

#### シナリオ A: AIによる10秒のビジュアル生産

- **期間 ($\Delta t$):** $10$ 秒 (無視できるプロセス)
- **労働力 ($P_{\text{labor}}$):** $1$ ユニット (コマンドを書くだけ)
- **意志係数 ($I_{\text{agency}}$):** $0.01$ (リスクなし、コストなし)
- **不可逆性 ($U_{\text{irreversible}}$):** $0$ (可逆的 / コピー可能)

**結果:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **コメント:** 出力が完璧であっても; [PoArt]の価値は$0$に近づきます。なぜなら、プロセスが経験されず、意志/リスクが関与していないからです。

#### シナリオ B: ライブ配信での6時間の物理的生産

- **期間 ($\Delta t$):** $6$ 時間 ($21{,}600$ 秒)
- **労働力 ($P_{\text{labor}}$):** $0.5$ ユニット (身体的・精神的努力の継続性)
- **意志係数 ($I_{\text{agency}}$):** $0.9$ (決定を変更し、リスクを取り、不可逆的な選択)
- **不可逆性 ($U_{\text{irreversible}}$):** $>0$ (物理的痕跡は元に戻せません)

**結果:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **コメント:** プロセスが長くなり、意志(リスク)が増加すると、価値は累積的に蓄積されます。$U_{\text{irreversible}}$項は、作品に「独自性」(非代替性)を生み出す追加の寄与です。

---

### ✅ 結論: 証明に結び付けられた価値 (Proof-Bound Value)

この定理は、[PoArt]の価値主張を「いいね」や「市場の物語」であることから抽出し、**実証可能な生産現実**に結び付けます。

1. **プロセスなし、価値なし:**  
   AIは即座の出力でプロセスを破壊します($t \to 0$)。プロセスウィンドウが狭まると、積分結果は必然的に減少します:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **意志とリスクは乗数:**  
   [PoArt]は「費やされた時間」だけでなく、その時間における決定、リスク、コストの実際のレイヤーも測定します。リスクを取らない生産(AI)は低い価値を持ちます:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **独自性は物理的証明であり、マーケティングではない:**  
   物理的生産における不可逆的な痕跡(キャンバスのストローク、大理石の破片)は、デジタルの`Ctrl+Z`論理の外にあります。この不可逆性($U_{\text{irreversible}}$)は、作品を存在論的に独自化します。

> **🔐 要約:** 価値定理は測定として不確実に見えるかもしれませんが(その現実世界の対応物が完全に測定できない場合でも)、この式の目的は変数の構成と方向を示すことです。AI時代において希少なのは「画像」ではなく、**実証可能な労働、時間、意志**です。[PoArt]はこの希少性を測定し、**Evidence Pack**で記録します。

### 🏛️ 「エンジン」概念の重要性

Pump.funや類似のプラットフォームから出現するトークンは、しばしば単なる**「アクセスチケット」**です。しかし、**PoArt Forensic Engine (PFE)**は、このチケットがどの権利を保護するか、労働がどのように記録されるか、芸術/科学/技術がどのように永続化されるかを決定する**憲法的論理レイヤー**です。

> **注意:** Pumpfunでこのプロジェクトを立ち上げた理由は、十分な流動性と十分なフォロワーがなかったためです。既存のデータを使用することは、最高品質ではなくても、戦略的に正しい動きでした。予算とリソースに関係なく、GitHubでこのエンジンのロジックを定義することは、プロジェクトが単なる金融投機ではなく、**ソフトウェアインフラストラクチャ**と**デジタル国立図書館**の長期ビジョンであることを証明しています。

---

## 🎨 [PoArt] 労働証明プロトコル (Proof of Art Protocol v1.0)

> **「本物のアーティスト、本物の制作、本物の価値。」**

このプロトコルは、暗号エコシステムを取り巻く匿名の詐欺師、5分で生産されたAIビジュアル、「Pump & Dump」文化に対して開発された**生物学的・知的防御メカニズム**です。

---

## a) [PoArt]とは何か? (哲学的・技術的定義)

**Proof of Art [PoArt];** は、ブロックチェーン上の資産の背後にある価値が投機ではなく、検証可能な**人間の労働**、**時間**、**物理的エネルギー**に基づいていることを保証する制度的検証基準です。

Bitcoinが*「電気とプロセッサパワー」* **(Proof of Work)**で価値を生成するように、[PoArt]準拠プロジェクトは*「芸術的スキルと人間の時間」*で価値を生成します。

Pump.funやDEXプラットフォームでの*「開発者が売却し、プロジェクトが終了」*のリスクを排除します; なぜなら、ここでは価値はコードではなく、**制作の継続性**にあるからです。

> **[PoArt]は参加者に「私たちを信頼して」とは言いません; 「ここに証拠があります、目で見て、数学で検証してください」と言います。**

---

## b) [PoArt] 5本柱基準 (真実の5本柱)

これらの5つの要素は、プロジェクトが[PoArt]シールを受け取るために合格しなければならない、操作不可能なフィルターです。

### 1) ライブ身元証明

- **問題:** 暗号世界は、不明確な身元を持つ匿名の創設者(開発者)で溢れており、彼らはお金を集めてプロジェクトを放棄します。
- **[PoArt]ソリューション:** 生産者は、身分証明書だけでなく、**生産の瞬間における存在**を証明します。これには、コミュニティとの相互作用が発生し、特定の即座のリクエストが満たされるライブストリームセッションが含まれます。事前録画されたビデオではありません。  
  (例: *「今日の日付と現在のブロック番号をキャンバスの右隅に書いてください」*)
- **モットー:** *「ボットは描けますが、ボットは汗をかかず、即興できません。」*

### 2) 労働とプロセスの証明

- **問題:** 2秒で生産されたAI(人工知能)ビジュアルが、デジタル世界で2か月かけて作られた油絵と同じ「jpeg」扱いを受けています。
- **[PoArt]ソリューション:** 作品の「妊娠と誕生のプロセス」が記録されます。スケッチ段階、ペイントレイヤー、累積された費やされた時間、アーティストが作品を作成する際に経験した物理的プロセスが文書化されます。これは、トークンに**「時間コスト」**を追加します。資産の生産が困難であればあるほど、その価値は堅固です。

### 3) 美的価値の証明

- **問題:** 即座のコメディだけに焦点を当て、美学と芸術的深さを無視する「ミーム」文化は、短命な「ハイプ」プロジェクトにつながります。
- **[PoArt]ソリューション:** プロジェクトは、学術的な芸術基準、色彩理論、構成規則、素材知識(インパスト、テクスチャーなど)を持たなければなりません。コンテンツは笑わせるだけでなく、視聴者に賞賛を呼び起こし、**収集価値**を持つべきです。

### 4) 概念的新規性

- **問題:** 創造性のない何千もの犬/猫コインのコピー。
- **[PoArt]ソリューション:** プロジェクトは、芸術、科学、哲学、技術を意味のある構造で組み合わせる新しい橋を構築しなければなりません。  
  (例: 古典的なダビデ彫刻を暗号市場データと組み合わせる; 人間の知覚が「石になる」というアイデアをこれを通じて処理し、科学的ソースで基礎を固める。)  
  作品は視覚的な祭典だけでなく、**科学、哲学、技術**について考えさせる知的挑戦でもあるべきです。

> [!IMPORTANT]
> **参考例 (ラス・パルミタス効果):** メキシコの犯罪に悩まされていたラス・パルミタス地区で、200以上の家が巨大な虹のスペクタクルに変わりました。この美的介入の結果、地区の犯罪率はある程度減少し、若者はギャングではなく芸術に関わり始めました。美的変化は、人々の環境と互いへの尊重を再コード化しました(社会的結束)。
>
> **期待:** [PoArt]リストに入るプロジェクトは、上記の例のように、純粋な視覚美学を超えた社会学的、科学的、哲学的な因果関係を含む必要があります。時間はお金で買えない唯一の資産であるため、このプロトコルでは時間を担保としてステーキングすることで証明する必要があります。プロジェクトの概念的基盤は非常に強力で普遍的でなければならず、数年後の可能性のあるCTO(Community Take Over)シナリオでも、コミュニティがこの遺産を継承してプロジェクトの革新的可能性を自律的に継続できるようにする必要があります。

### 5) 非アルゴリズム的意志

- **問題:** 完璧だが魂のないデジタル生産が互いに繰り返されます。
- **[PoArt]ソリューション:** 間違いを犯し、リスクを取り、感情的な変動を経験できる人間の独自の意志が作品に感じられる必要があります。筆致の不確実性、素材の予期しない反応、アーティストの即座の決定は、作品を「機械生産」から分離する**生物学的署名**です。

---

## c) 検証および詐欺防止メカニズム

このシステムは、プロジェクトが「最初」だけでなく「永遠に」信頼性があり生き続けることを保証します。

### 📦 証拠パック - デジタルツイン

すべての[PoArt]認定作品の背後には、投資家がダウンロードできる暗号化されタイムスタンプされたデータパッケージがあります:

- **RAWビデオ録画:** 制作の瞬間の中断のない生映像。
- **メタデータ分析:** ファイル作成日、使用されたデバイス情報、位置データ。
- **物理的参照:** 作品が物理世界に存在する証拠  
  (例: 作品の横にあるその瞬間の現在の新聞またはブロックチェーンデータ)。

> *一貫性注意:* 「証拠パック」という用語は、前のセクションの**証拠パック → EvidenceRoot → NotarySeal**チェーンに接続されます; つまり、パッケージの完全性は検証可能なシールで表されます。

### 🔄 365日更新 (持続可能性プロトコル)

- **革命的機能:** 暗号プロジェクトでは、「開発者」がトークンを発行し、通常1〜2か月後に消えます(ソフトラグ)。[PoArt]はこれを不可能にします。
- **ルール:** 「検証済みアーティスト」ステータスは生涯ではありません。**1年**のみ有効です。
- **運用:** アーティスト/開発者は、365日ごとにコミュニティに**新しい、重要で実証可能な作品**を提示する必要があります。
- **例シナリオ:** 2026年にプロジェクトを開始しました。2027年1月、システムは「証明期間が期限切れ」の警告を出します。アーティストが新しい展示会、新しい物理的作品、新しい技術統合を提示しない場合、プロジェクトの「信頼バッジ」が低下します。
- **結果:** このシステムは、**コンテンツが決して関連性を失わない**こと、投資家が*「開発者はまだいますか?」*という恐怖を経験しないことを保証します。プロジェクトは生きたスタジオになります。

### 🚩 レッドフラグプロトコル

**コミュニティまたはアルゴリズムによって検出された詐欺の場合(AI使用、盗まれた作品、操作されたビデオ):**

1. 証明書は直ちに**「VOID」(無効)**としてマークされます。
2. 証拠パックは公に**「偽物」**とラベル付けされます。
3. プロジェクトは[PoArt]ブラックリストに載せられます。これは、分散型世界では**評判が唯一の通貨**であることを強化します。

---

## d) 結論: カジノではなく、博物館

**Pump.funと分散型取引所(DEX)は残念ながら今カジノです; ライトが点滅し、誰もが速い利益を追いかけ、ハウス(詐欺師)が常に勝ちます。ここでプロジェクトを開始した理由は、十分な予算がなく、ライブストリームを通じて既存のオーディエンスにリーチするための環境があったためです。**

**[PoArt]は、このカジノの真ん中に建てられた要塞です。**

- 🎰 カジノはカードゲームに基づいています; 私たちは**物理的現実**に基づいています。
- 🃏 カジノは詐欺に開かれています; 私たちは**透明な証拠**に開かれています。
- ⏳ カジノは一時的です; 私たちは**芸術と科学の永遠性**に焦点を当てています。

**このプロトコルを使用するトークンは、単なる「コイン」ではありません; それは汗、絵の具、コード、哲学を含むデジタル資本です。**

---

## 🗳️ 6) ガバナンスと公開レジストリ

**このセクションの目的: [PoArt]基準を「個人への信頼」の平面から、レジストリ + 検証 + コミュニティ監視を備えた持続可能な公共インフラストラクチャに変換すること。**

### 6.1 公開レジストリ

- **公開レジストリ:** すべての承認されたデータは`ilhanart.org/registry`(またはGitHub Registry)に記録されます。

**レジストリロジック (推奨標準 - JSONパス形式):**

レジストリに入る各エントリは、これらの最小限の検証可能なコアフィールドを持っています:

- **身元とステータス:**
  - `certificate_id` (読み取り可能な参照)
  - `status` (active / void)
  - `void_reason` (該当する場合)
  - `visibility` (private / masked / public)
  - `created_at` (タイムスタンプ)

- **発行機関:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **作品情報:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (可能な場合; トークンゲート身元用)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **フォレンジックデータ:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **暗号証明:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **ガバナンス:**
  - `governance.decision`
  - `governance.veto_threshold`

レジストリは2つのレイヤーを持つことができます:
- **1)** 人間が読めるインデックス (Webリスト / 検索 / フィルター)
- **2)** 機械が読めるマニフェスト (JSONレコード; PFE検証用)

**この「エントリ」は、PFEの証拠パック → EvidenceRoot → NotarySealチェーンを通じて検証可能になります。レジストリは「主張」ではなく、検証目標を提供します。**

---

### 6.2 40%コミュニティ拒否権 (トークンゲートガバナンス)

- **40%コミュニティ拒否権:** ステータス付与の1か月前に投票が始まります; **トークンゲート(Solana検証済み)**コミュニティの40%の反対は申請を無効にします。

**投票フロー (推奨される明確なプロセス):**
- **申請ウィンドウ:** 候補プロジェクトが「PoArt候補登録」を開きます(候補レコードは「保留中」ステータスで表示されます)。
- **審査期間:** コミュニティは30日間証拠を調査します(証拠パック + ライブストリーム録画 + メタデータ)。
- **トークンゲート検証:** Solana検証済みウォレットで投票が行われます(例: 特定のトークン/NFT所有権 + ウォレット署名)。
- **拒否権ルール:** 投票の40%が**反対(いいえ / 拒否権)**の場合、申請は却下されます。
- **透明性:** 投票結果は「決定レコード」としてレジストリに保存されます(日付、比率、スナップショットID)。

---

### 6.3 メタデータ同期 (物理世界との整合)

- **メタデータ同期:** レジストリの技術データは物理エンティティと100%一致する必要があります。

**「100%一致」の技術的定義 (推奨される明確性):**
- **最小一致 (必須):**
  - レジストリの`asset.fingerprints.sha256/sha512`は、問題のファイルのハッシュと**同一**である必要があります。
  - レジストリの`proof.notary_seal`が再現されるとき(証拠パックが存在する場合)、それは**同一**である必要があります。
- **物理的参照一致 (証明タイプ):**
  - ライブストリームで示された物理的作品 + 日付/ブロック参照および類似の証拠は、証拠パックと一貫している必要があります。
- **プライバシーコンプライアンス:**
  - `masked`可視性のIP/位置などのフィールドは、**マスキング基準に従って**公開されます。

---

### 6.4 紛争と取り消し

レジストリは単なる「承認」メカニズムではありません; それは**詐欺に対する生きた監査メカニズム**です。

- 紛争が開始されると、エントリは**「review」(審査)**モードに配置できます。
- 詐欺が検出された場合、理由を追加して`status: void`としてマークされます:
  - `void_reason` (AI使用 / 盗難 / 操作など)
  - `revoked_at` (取り消し時間)
- 取り消し決定のソースはレジストリに明確に表示されます:
  - コミュニティ投票 / 承認された委員会 / フォレンジック調査ノート(該当するもの)

> **このセクションは、「レッドフラグプロトコル」セクションのVOID概念のレジストリ対応物です。**

---

### 6.5 レジストリエントリの例 (機械可読)
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
> *注意: `asset.fingerprints.sha512`およびその他のハッシュ値は表示目的で省略されています; 実際の実装では、完全長の16進文字列が使用されます。*

---

## 7) 🔐 技術的封印 (NOTARY SEAL)

**PoArt Forensic Engine (PFE) v1.0**によって生成される揺るぎない封印アルゴリズム:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] デジタル公証・フォレンジック証拠プロトコル (Beta v1.0)

> **「文化は資本よりも偉大です。今日あなたの作品を保護し、明日に運びます。」**

---

## なぜ公開?

真のセキュリティは透明性から来ます。私たちの**公開レジストリ**システムのおかげで、世界中の誰でも、権威を必要とせずに、数秒でファイルがオリジナルかどうかを確認できます。

---

## 🧩 なぜ複数の「可視性モジュール」?

これはコードの最も重要な部分です(可視性選択メニュー)。これらのオプションにより、ユーザーは**「プライバシー vs. 透明性」**のバランスを取ることができます:

### 🔒 プライベート

- **シナリオ:** アーティストはまだ作品を公開したくないが、「この日付にこれを作った」ことを証明するためにタイムスタンプを押したい。
- **コードの動作:** データをデータベースに書き込みますが、`visibility: "private"`とスタンプします。後で「Public Read」ポリシーを書くときに、`WHERE visibility = 'public'`でこれらのレコードを公開から隠すことができます。

### 🕶️ マスク

- **シナリオ:** アーティストは透明性を望んでいますが、自宅の住所(IP位置)が見つかることを恐れています。
- **コードの動作:** `maskIP`と`maskLoc`関数はJavaScript側で動作します。IPアドレスを`88.241.***.***`形式に、位置を`***/TR`形式に変換し、検閲されたバージョンをデータベースに送信します。
- **プライバシー注意:** マスキングはブラウザで行われ、Supabaseは実際の位置を見ません。**ただし:** ipapi.coなどのサードパーティAPIが位置データに使用される場合、これらのプロバイダーはリクエスト時にIPアドレスを見ます。
- **マスクモードでの封印:** EvidenceRootとNotarySealの計算は、マスクされたフォレンジックデータで行われます; したがって、検証は決定論的のままです。

### 🌍 公開

- **シナリオ:** 完全な透明性。[PoArt]基準に従って、どこで、いつ、どのネットワークから作品が制作されたかが明確に宣言されます。

---

## 💡 技術革新

PoArtは単なるファイルアップロードシステムではありません。それは、3つの異なる技術レイヤーを1つの鍋で融合させる新しい基準をもたらす**「フォレンジック保管チェーン」**エンジンです。

**このセクションで「エンジン」として説明されているレイヤーは、以前の用語でのPoArt Forensic Engine (PFE)コアに対応しています。**

### 1) クライアント側ハッシング (最大のプライバシー)

あなたのアートワークファイルはサーバーにアップロードされません。私たちのブラウザベース(クライアント側)エンジンは、あなた自身のコンピューター上でファイルのハッシュ(デジタルダイジェスト)を計算します。このフィンガープリントとメタデータのみがサーバーに送信されます。

> **プライバシー注意:** 作品ファイルはサーバーにアップロードされず、この方法で保護されます。ただし、フォレンジックデータ(IP/位置)は、選択された可視性モード(プライベート/マスク/公開)に従って共有されます。

### 2) フォレンジックデータ融合 (フォレンジック力)

普通のタイムスタンプをはるかに超えています。システムは、これらのデータを単一の「創世記封印」に組み合わせます:

- **デジタルダイジェスト (SHA-512):** 作品の1ピクセルでも変更されると壊れる暗号ダイジェスト(SHA-512)標準を使用したデジタルフィンガープリント。
- **位置と時間:** ミリ秒精度の日付、トランザクションの国、都市、地区データ。
- **デバイス身元:** オペレーティングシステム、ブラウザ、デバイスタイプ(User-Agent分析)。

---

## 🛡️ ユースケースと利点

あなたがアーティスト、作家、デザイナーであるなら、「私はこれを以前に作った」と言うだけでは十分ではありません; それを証明する必要があります。

**PoArtで封印する作品:**

- **数学的証明:** ファイルの1ピクセルでも変更されると、システムはそれを知っています。操作は不可能です。
- **法的基盤:** どの日付に、どの都市で、どのデバイスから作品が封印されたかが記録されます。
- **即座の証明書:** QRコード付きで封印された特別な**「資産身元証明書」**を数秒で生成します。

---

## ⚙️ システムアーキテクチャと技術的特徴

システムは「サーバーレス」アーキテクチャで設計されており、高性能とスケーラビリティに焦点を当てています。

| レイヤー | 技術 | 説明 |
|--------|-----------|-------------|
| **暗号化** | SHA-256 & SHA-512 | 二重層暗号ダイジェスト |
| **データベース** | Supabase (PostgreSQL) | JSONBデータ構造、RLSポリシー |
| **フォレンジックデータ** | ipapi.co API | IP/位置/時間の三位一体 |
| **レンダリング** | html2canvas + jsPDF | クライアント側PNG/PDF生成 |
| **フロントエンド** | Vanilla JavaScript | ゼロフレームワーク依存 |
| **セキュリティ** | クライアント側ハッシング | ファイルはサーバーに行かない |

### 目立つ特徴

| 機能 | 詳細 | 競合他社では? |
|---------|-------|-----------------|
| **ドラッグ&ドロップUI** | ファイルをドラッグ&ドロップ、即座にプレビュー | ❌ ほとんどで欠落 |
| **マルチフォーマットエクスポート** | PNG、JSON、PDF - ワンクリック | ⚠️ 制限あり |
| **リアルタイムプレビュー** | ライブ証明書プレビュー | ❌ なし |
| **プライバシーコントロール** | プライベート/マスク/公開オプション | ❌ なし |
| **クライアント側ハッシュ** | ファイルはサーバーに行かない | ✅ 一部のみ |
| **フォレンジックメタデータ** | IP、位置、デバイス、時間 - すべて一緒 | ❌ 断片化 |
| **QR検証** | 即座の検証QRコード | ⚠️ 制限あり |
| **レート制限** | スパム保護 (RLS + クライアント) | ❌ ほとんどで欠落 |

---

## 🗺️ ロードマップ: 「トラストレス」な未来

現在のバージョン **(Beta v1.0)** は、エンドユーザーに最大速度、簡単なインターフェース、無料アクセスを提供するように最適化されています。しかし、私たちの究極のビジョンは、データベース管理者(私たち)でさえ干渉できない構造への移行です。

### フェーズ1: ベータ (現在ライブ)

- **インフラストラクチャ:** クラウドデータベース (Supabase)。
- **目的:** 速度、UX(ユーザーエクスペリエンス)バリアの除去、適応。「摩擦のない」セキュリティを提供。

### 🚀 フェーズ2: (バックエンド / Edge Function要件)

このフェーズは、完全に「クライアント側」で動作する構造から、より安全で管理可能な「サーバー側権限」構造への移行をカバーします。

| 要素 | 何をもたらすか? | 技術スタック | 優先度 |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Function** | スパム防止 + APIキーセキュリティ | Supabase Edge (Deno) | 🔴 高 |
| **ウォレット署名** | 暗号認証 | Solana Wallet Adapter | 🟡 中 |
| **IPFS/Arweaveバックアップ** | 分散不変性 | IPFS SDK + Pinata | 🟢 低 |
| **取り消しメカニズム** | 偽証明書キャンセル | DBスキーマ更新 | 🔴 高 |
| **監査ログ** | フォレンジッククエリレコード | カスタムログテーブル | 🟡 中 |
| **OpenTimestamps** | Bitcoinアンカリング | OTS JavaScript | 🟢 低 |
| **DID統合** | 分散型身元 | ION/Ceramic | 🟢 低 |

### フェーズ3: 完全な分散化 (長期)

| 機能 | 目標 | ETA |
|---------|------|-----|
| **ブロックチェーンレジストリ** | Ethereum/Solanaオンチェーン登録 | 2026年第4四半期 |
| **DAOガバナンス** | コミュニティ管理 | 2027年第1四半期 |
| **マルチチェーンサポート** | Polygon、Arbitrum、Base | 2027年第2四半期 |
| **法的認識** | トルコの裁判所での有効性 | 2027-2028 |
| **開発者向けAPI** | パブリックAPIエンドポイント | 2026年第3四半期 |

---

## 📊 競合分析 (更新)

PoArtは、既存のソリューションの欠陥を補完する「スイートスポット」に位置しています。

| 機能 | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **コスト** | 🆓 無料 | 🆓 | 💰 有料 | ⚠️ フリーミアム | 💰 | 💰 | 💰 | 💰 |
| **ドラッグ&ドロップUI** | ✅ 非常に簡単 | ❌ CLI | ⚠️ 中程度 | ⚠️ 中程度 | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **マルチフォーマットエクスポート** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **リアルタイムプレビュー** | ✅ ライブ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **プライバシーコントロール** | ✅ 3モード | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **クライアント側ハッシュ** | ✅ プライバシー | ✅ | ❌ アップロード | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **フォレンジックメタデータ** | ✅ 完全 | ❌ | ❌ | ⚠️ 制限あり | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR検証** | ✅ 即座 | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **レート制限** | ✅ RLS+クライアント | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **ブロックチェーンアンカリング** | 🔄 ロードマップ | ✅ Bitcoin | ✅ Ethereum | ✅ マルチ | ✅ | ✅ | ✅ | ✅ |
| **オープンソース** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **トルコ語サポート** | ✅ ネイティブ | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**凡例:**
- ✅ : 完全サポート / 利用可能
- ⚠️ : 制限あり / 有料プランで
- ❌ : なし / サポートされていない
- 🔄 : ロードマップ内 (開発中)
- 🆓 : 完全無料
- 💰 : 有料 / サブスクリプション必要

### 競合の欠点、PoArtの強み

| マイナス | 競合 | PoArt |
|-------|-------------|-------|
| **使用難易度** | CLI、API知識、ウォレット必要 | ドラッグ&ドロップ、3クリックで完了 |
| **コストバリア** | $50-500/月のサブスクリプション | 100%無料 |
| **プライバシー** | ファイルがサーバーにアップロード | クライアント側、ファイルは行かない |
| **フォレンジックデータ** | タイムスタンプのみ | IP、位置、デバイス、時間 - すべて |
| **トルコ語サポート** | なしまたは非常に限定的 | ネイティブ言語サポート |
| **オープンソース** | クローズドボックス | すべてのコードがGitHubでオープン |

---

## 🧬 プロトコルデータ構造 (JSON Schema)

**各[PoArt]証明書には、次の標準で生成されたポータブルで検証可能なJSON身元カードがあります。**

> **注意:** この身元JSON形式は、ユーザーに提示される証明書形式です。レジストリレコードでは、`identity.asset_data`の代わりに`registry.asset`が使用されます(マッピング: `identity.asset_data` == `registry.asset`)。
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

## 🔬 技術的深さ: 封印アルゴリズム

### 決定論的ハッシュ関数
```javascript
// ヘルパー関数: ダイジェストを16進文字列に変換
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// 文字列をバイト配列に変換
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// 正規フォレンジック文字列生成 (v1.0: 固定フィールド順序 + UTF-8 + \n区切り)
// フェーズ2注意: RFC 8785 (JCS)を使用した正規JSONへの移行
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal生成プロセス (完全に決定論的)
```javascript
// 1. FileHash計算 (クライアント側)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. フォレンジックデータ収集 (単一タイムスタンプ使用)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // 単一タイムスタンプ生成
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // 同じタイムスタンプ
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot作成 (正規エンコーディングで)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal生成 (同じタイムスタンプ使用)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// マスキングヘルパー関数 (IPv4およびIPv6サポート)
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4チェック
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6または不明な形式
  return "***";
}
```

### 検証フロー (2レベル)

#### Quick Verify (クイック検証)
```javascript
// ファイルハッシュのみを検証 (クイックレッドフラグ)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // レジストリから取得
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // ハッシュ比較
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ オリジナル - ファイルハッシュが一致"
    };
  } else {
    return {
      valid: false,
      message: "❌ 偽物 - ファイルが操作されています"
    };
  }
}
```

#### Full Verify (完全検証)
```javascript
// EvidenceRootとNotarySealを再生成して検証
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // レジストリから取得
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash検証 (クイックレッドフラグ)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ 偽物 - ファイルハッシュが一致しません" };
  }

  // 2) EvidenceRoot再生成 (レジストリに保存されたフォレンジックデータで)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ 一致しません - EvidenceRootが保持されません" };
  }

  // 3) NotarySeal再生成 (同じタイムスタンプ + signer_sigで)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ 一致しません - NotarySealが保持されません" };
  }

  // オプション: フェーズ2で、attestation_pubkeyでsigner_sigも検証
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ 無効な署名" };

  return { valid: true, message: "✅ オリジナル - 完全検証合格" };
}
```

> **重要な注意事項:**
> - **Quick Verify:** クイック使用のためにファイルハッシュのみを検証します。
> - **Full Verify:** プロトコルのすべてのレイヤーを検証します(EvidenceRoot + NotarySeal)。
> - すべてのハッシュ操作は、固定エンコーディングと区切り文字で決定論的に実行されます。
> - **v1.0正規化標準:** 固定フィールド順序 + UTF-8エンコーディング + `\n`区切り。
> - **フェーズ2計画:** RFC 8785 (JCS - JSON Canonicalization Scheme)を使用した正規JSONへの移行。
> - マスクモードでは、EvidenceRootとNotarySealの計算はマスクされたフォレンジックデータで行われます; したがって、検証は決定論的のままです。
> - プロセス全体で単一のタイムスタンプが使用されます(フォレンジック + NotarySeal); 決定論が保証されます。
> - **フォレンジックフィールド名:** `ip_masked`、`location`、`device`、`timestamp` (コードとレジストリ完全互換)。
> - **レジストリパス:** `certificate.asset.fingerprints` (検証コードと完全互換)。
> - **レジストリのsigner_sig:** `proof.signer_sig`フィールドはFull Verifyに必要です。
> - SignerSignatureメカニズムはフェーズ2でSolana Wallet Adapterで有効化されます; v1.0では、`attestation_pubkey`で検証を実行できます。

---

## 📈 使用統計 (2026年第1四半期目標)

| メトリック | 目標 | ステータス |
|--------|--------|--------|
| **総証明書数** | 1,000 | 🔄 進行中 |
| **アクティブユーザー** | 500 | 🔄 進行中 |
| **検証数** | 5,000 | 🔄 進行中 |
| **稼働時間** | 99.9% | ✅ アクティブ |
| **平均応答時間** | <200ms | ✅ 最適 |

---

## 🌍 コミュニティとサポート

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org

---

## 🙏 貢献者

PoArtプロトコルは、オープンソースコミュニティの貢献により発展を続けています。

**貢献するには:**
1. リポジトリをフォーク
2. 機能ブランチを作成 (`git checkout -b feature/amazing-feature`)
3. コミット (`git commit -m 'Add amazing feature'`)
4. プッシュ (`git push origin feature/amazing-feature`)
5. プルリクエストを開く

### 🛠️ 今必要なもの? (支援要請)

PoArtプロトコルは、**フェーズ2**開発のために以下の分野で経験豊富な開発者を探しています:

* **Supabase Edge Functions:** スパム保護をサーバー側に移動。
* **Solana Web3.js:** ウォレット署名統合。
* **IPFS / Arweave:** アーカイブおよびピンニングサービス統合。

> 機能を追加する前に「Issues」タブでディスカッションを開始してください。

---

**[PoArt] Proof of Art Protocol v1.0**  
*「文化 > 資本」*

## 🧾 ライセンス

MITライセンス © 2026 İlhan Art Gallery Initiative

完全な条件については[![ライセンス](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE)を参照してください。

---

## 💬 クレジット

![バージョン](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![セキュリティ](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![プラットフォーム](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![ライセンス](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**このプロジェクトは[İlhan Art Gallery]イニシアチブによって開発されており、そのソースコードは透明性のために公開されています。**

**プロトコル V1.0 // SHA-512で封印**

*© 2026 İLHAN ART | アートワーク、ビジュアル、アイデアのすべての権利を保有。*

---
