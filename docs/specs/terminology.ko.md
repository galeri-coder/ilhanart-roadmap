# 📚 용어 및 개념 사전
> **"이 프로토콜의 언어를 이해하는 것은 그 비전을 이해하는 것입니다."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: 핵심 인프라

**PoArt Forensic Engine (PFE)**는 [PoArt] 프로토콜 뒤에 있는 핵심 로직과 기술적 작동을 나타내는 메인 레이어입니다. 예술 작품의 원시 생산 데이터를 가져와 검증 가능하고 변경 불가능한 **디지털 증거**로 변환하는 "포렌식 엔진"입니다.

### 🧩 왜 "PoArt Forensic"인가?

- **PoArt (Proof of Art):** 엔진의 초점은 디지털 자산의 가치를 투기가 아닌 **증명 가능한 생산 과정**에 연결하는 것입니다.
- **Forensic (포렌식 검증):**
  - **기술적 정의:** 생산 과정과 관련된 데이터(붓 터치, 타임랩스, 로그)가 조작되지 않았음을 검증하기 위한 알고리즘 및 기록 체인 접근 방식.
  - **철학적 레이어:** 인공지능의 "즉각적인 출력" 생산에 대항하여; **시간, 노력, 결정 비용**을 포함하는 인간의 생산을 측정 가능한 현실로 변환한다는 주장.

> 참고: 블록체인(예: Solana) 통합은 PFE의 핵심이 아니며; 검증/레지스트리를 위해 별도로 정의될 **Chain Anchor Layer**로 처리됩니다.

### 🛠️ v1.0 기술 범위

**PoArt Forensic Engine (PFE) v1.0**은 복잡한 금융 모델 대신 다음 **3가지 주요 기둥** 위에 구축되었습니다:

1. **Hashing & Sealing (해싱 및 봉인):**  
   PFE는 Evidence Pack 내의 모든 요소(작품 파일, 비디오, JSON/로그, 서명 등)를 결정론적으로 처리하고 고유한 **NotarySeal** 값을 생성합니다.

   **핵심 개념 (v1.0):**
   - **FileHash (작품 지문):** 작품 파일의 바이트에서 생성된 해시.
   - **EvidenceRoot (증거 패키지 루트):** Evidence Pack의 무결성을 나타내는 루트 요약(Merkle root 또는 canonical manifest hash).
   - **NotarySeal (최종 봉인 / PFE 출력):** EvidenceRoot + 시간 + 서명의 조합에서 생성된 최종 봉인.

   **공식 (투자자에게 명확하게 표시):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Canonical Payload 정의 (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > 참고: PFE 출력으로 언급되는 값은 **NotarySeal**입니다. **SignerSignature** 메커니즘은 Phase 2에서 (Solana Wallet Adapter와 함께) 활성화됩니다; 현재 v1.0은 시스템 자체의 attestation 서명을 사용합니다. Attestation 공개 키는 레지스트리의 `issuer.attestation_pubkey` 필드에 게시됩니다.

2. **Indexing (인덱싱):**  
   어떤 지갑이, 어떤 날짜에, 어떤 작품에 대해 **Labor Proof (노동 증명)**를 제출했는지를 투명하고 쿼리 가능한 기록 레이어에 기록합니다.  
   *(이 레이어는 데이터베이스일 수 있으며; 체인 통합은 별도로 "Chain Anchor Layer"로 정의됩니다.)*

3. **Verification (검증):**  
   작품의 진위가 질문될 때, PFE는 원시 증거를 재처리합니다; 계산된 **EvidenceRoot / NotarySeal** 값이 아카이브의 기록과 일치하는지 수학적 확실성으로 테스트합니다.

---

### 🧮 PoArt 가치 정리 (The Value Theorem)

[PoArt] 프로토콜은 디지털 자산의 가치($V$)를 주관적인 시장 인식이 아닌 **생산 과정의 물리적 현실**과 연결합니다.

인공지능(AI)은 결과를 즉시 제공하여($t \to 0$) 과정을 파괴합니다. [PoArt]는 가치를 **시간, 노동, 의지** 구성 요소의 축적으로 간주합니다.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### 변수 정의

- **$\int dt$ (과정 축적):**  
  가치는 즉각적인 "출력"이 아닙니다; $t_{\text{start}}$와 $t_{\text{end}}$ 사이에 축적되는 **과정**입니다. 시간이 줄어들면(AI 생산), 적분 결과는 0에 가까워집니다.

- **$P_{\text{labor}}(t)$ (순간 노동 강도):**  
  생산 순간에 소비된 정신적, 물리적 노력의 강도를 나타냅니다. 증명 가능한 노력이 증가하면 피적분함수가 커집니다.  
  > 참고: 이 용어는 실제로 "측정 가능/증명 가능한 노동 신호"를 통해 정규화될 수 있습니다.

- **$I_{\text{agency}}(t)$ (의지 계수):**  
  생산자의 위험 감수 및 의사 결정 능력입니다. $0$과 $1$ 사이의 값을 취합니다.
  - **AI ($I \approx 0$):** 명령을 실행하고, 위험을 감수하지 않으며, 대가를 지불하지 않습니다.
  - **인간 ($I \to 1$):** 결정을 바꾸고, 망설이며, 위험을 감수합니다.

- **$U_{\text{irreversible}}$ (되돌릴 수 없는 고유성):**  
  디지털 생산에서는 실행 취소(`Ctrl+Z`)가 가능하지만; 물리적 생산에서는(캔버스에 바른 페인트, 조각된 대리석, 라이브 방송의 제스처) 되돌릴 수 없습니다. 이 **비가역성**은 작품에 "고유성"(대체 불가능한 특성)을 만드는 추가 항입니다.

### 🔎 사례 분석: AI "즉각적 출력" vs. 인간 "증명된 과정"

다음 시나리오는 **PoArt 가치 정리**가 실제로 어떻게 작동하는지, 그리고 왜 AI 생산물이 [PoArt] 표준에서 낮은 점수를 받는지 보여줍니다.

#### 시나리오 A: AI로 10초 만에 이미지 생성

- **시간 ($\Delta t$):** $10$초 (과정이 거의 없음)
- **노동 강도 ($P_{\text{labor}}$):** $1$ 단위 (명령 작성만)
- **의지 계수 ($I_{\text{agency}}$):** $0.01$ (위험 없음, 대가 없음)
- **비가역성 ($U_{\text{irreversible}}$):** $0$ (실행 취소 가능 / 복사 가능)

**결과:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **해석:** 출력이 완벽하더라도; 과정이 경험되지 않고 의지/위험을 포함하지 않기 때문에 [PoArt] 가치는 $0$에 가까워집니다.

#### 시나리오 B: 라이브 스트림에서 6시간 물리적 생산

- **시간 ($\Delta t$):** $6$시간 ($21{,}600$초)
- **노동 강도 ($P_{\text{labor}}$):** $0.5$ 단위 (물리적, 정신적 노력의 연속성)
- **의지 계수 ($I_{\text{agency}}$):** $0.9$ (결정 변경, 위험 감수, 되돌릴 수 없는 선택)
- **비가역성 ($U_{\text{irreversible}}$):** $>0$ (물리적 흔적은 실행 취소 불가)

**결과:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **해석:** 과정이 길어지고 의지(위험)가 증가할수록 가치는 누적적으로 증가합니다. $U_{\text{irreversible}}$ 항은 작품에 "고유성"(대체 불가능한 특성)을 만드는 추가 기여입니다.

---

### ✅ 결론: 증명으로 가치 잠금 (Proof-Bound Value)

이 정리는 [PoArt]의 가치 주장을 "좋아요" 또는 "시장 내러티브"에서 **증명 가능한 생산 사실**로 전환합니다.

1. **과정 없이는 가치가 생성되지 않음:**  
   AI는 즉각적인 출력($t \to 0$)으로 과정을 파괴합니다. 과정 창이 좁아지면 적분 결과는 수학적 필연성으로 줄어듭니다:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **의지와 위험은 승수:**  
   [PoArt]는 "소비된 시간"뿐만 아니라; 그 시간 동안의 실제 결정, 위험, 대가 레이어도 측정합니다. 위험을 감수하지 않는(AI) 생산의 가치는 낮습니다:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **고유성은 마케팅이 아닌 물리적 증거:**  
   물리적 생산에서 되돌릴 수 없는 흔적(캔버스 터치, 대리석 균열)은 디지털의 `Ctrl+Z` 논리 밖에 있습니다. 이 비가역성($U_{\text{irreversible}}$)은 작품을 존재론적으로 고유하게 만듭니다.

> **🔐 요약:** 가치 정리가 측정으로서 불확실해 보이더라도(실제 생활에서 100% 일치를 측정할 수 없더라도), 이 공식의 목적은 변수의 구성과 방향을 보여주는 것입니다. AI 시대에 희귀한 것은 "이미지"가 아니라; **증명 가능한 노동, 시간, 의지**입니다. [PoArt]는 이 희소성을 측정하고 **Evidence Pack**으로 등록합니다.

### 🏛️ "Engine"(엔진) 개념의 중요성

Pump.fun 또는 유사한 플랫폼에서 출시된 토큰은 종종 단지 **"입장권"**에 불과합니다. **PoArt Forensic Engine (PFE)**는 그 티켓이 어떤 권리를 보호하는지, 노동이 어떻게 기록될 것인지, 예술/과학/기술이 어떻게 영구화될 것인지를 결정하는 **헌법적 논리 레이어**입니다.

> **참고:** 우리가 이 프로젝트를 Pump.fun에서 시작한 이유는 충분한 유동성과 팔로워 수를 가지지 못했기 때문입니다. 기존 데이터를 사용하는 것이 전략적으로 최고 품질은 아니더라도 가장 올바른 조치였습니다. 예산과 자원에 관계없이 GitHub에서 이 엔진의 논리를 정의하는 것은 프로젝트가 단순한 금융 투기가 아니라 장기적인 **소프트웨어 인프라**이자 **디지털 국립 도서관** 비전임을 증명합니다.

---

## 🎨 [PoArt] 노동 증명 프로토콜 (Proof of Art Protocol v1.0)

> **"진정한 아티스트, 진정한 생산, 진정한 가치."**

이 프로토콜은 암호화폐 생태계를 뒤덮는 익명의 사기꾼들, 5분 만에 생산된 AI 이미지, "펌프 앤 덤프" 문화에 대항하여 개발된 **생물학적이고 지적인 방어 메커니즘**입니다.

---

## a) [PoArt]란? (철학적 및 기술적 정의)

**Proof of Art [PoArt];**는 블록체인 자산 뒤의 가치가 투기가 아닌 검증 가능한 **인간 노동**, **시간**, **물리적 에너지**에 의해 보장된다는 것을 보증하는 기관 검증 표준입니다.

비트코인이 *"전기와 처리 능력"* **(Proof of Work)**으로 가치를 생성하는 것처럼; [PoArt] 호환 프로젝트는 *"소비된 재능과 인간 시간"*으로 가치를 생성합니다. 시간을 "스테이크"합니다.

Pump.fun 및 DEX 플랫폼의 *"개발자(Dev)가 팔면, 프로젝트 끝"* 위험을 제거합니다; 여기서 가치는 코드가 아닌 **생산의 연속성**에 있기 때문입니다.

> **[PoArt]는 참가자에게 "우리를 믿으세요"라고 말하지 않습니다; "여기 증거가 있습니다, 눈으로 보고, 수학으로 검증하세요"라고 말합니다.**

---

## b) [PoArt] 5대 표준 (The 5 Pillars of Truth)

이 5가지 항목은 프로젝트가 [PoArt] 봉인을 받기 위해 통과해야 하는 조작 불가능한 필터입니다.

### 1) 라이브 신원 증명 (Live Identity Proof)

- **문제:** 암호화폐 세계는 익명의 창립자(Dev)가 돈을 모으고 프로젝트를 버리는 것으로 가득합니다.
- **[PoArt] 솔루션:** 생산자는 신분증뿐만 아니라 **생산 순간의 존재**를 증명합니다. 이것은 미리 녹화된 비디오가 아닌, 커뮤니티와 상호작용하고 즉각적인 특정 요청을 이행하는 라이브 스트림 세션을 포함합니다.  
  (예: *"캔버스 오른쪽 모서리에 오늘 날짜와 현재 블록 번호를 쓰세요"*)
- **모토:** *"봇은 그림을 그릴 수 있지만 봇은 땀을 흘리고 즉흥적으로 할 수 없습니다."*

### 2) 노동 및 과정 증명 (Labor & Process Proof)

- **문제:** 2초 만에 생성된 AI 이미지와 2개월에 걸쳐 만든 유화가 디지털 세계에서 같은 "jpeg" 취급을 받는 것.
- **[PoArt] 솔루션:** 작품의 "임신과 출산" 과정이 기록됩니다. 스케치 단계, 페인트 레이어, 누적된 시간, 아티스트가 작품을 만들면서 겪은 물리적 과정이 문서화됩니다. 이것은 토큰에 **"시간 비용" (Time Cost)**을 추가합니다. 자산 생산이 어려울수록 가치는 더 견고합니다.

### 3) 미적 가치 증명 (Aesthetic Value Proof)

- **문제:** "밈" 문화가 미학과 예술적 깊이를 무시하고 순간적인 코미디에만 집중하여 수명이 짧은 "하이프" 프로젝트를 만드는 것.
- **[PoArt] 솔루션:** 프로젝트는 학술적 예술 표준, 색상 이론, 구성 규칙, 재료 지식(임파스토, 텍스처 등)을 갖추어야 합니다. 콘텐츠는 웃기게만 해서는 안 됩니다; 시청자에게 경외심을 불러일으키고 **컬렉션 가치**를 가져야 합니다.

### 4) 개념적 혁신 (Conceptual Novelty)

- **문제:** 서로 복사한, 창의성이 부족한 수천 개의 개/고양이 코인.
- **[PoArt] 솔루션:** 프로젝트는 예술, 과학, 철학 또는 기술을 의미 있는 구조로 결합하는 새로운 다리를 구축해야 합니다.  
  (예: 고전 다비드 상과 암호화폐 시장 데이터를 결합; 인간 인식이 "돌로 변하는" 아이디어를 처리하고 이를 과학적 출처로 증명할 수 있는 것.)  
  작품은 단순한 시각적 향연이 아니어야 합니다; **과학, 철학 또는 기술**에 대해 생각하게 하는 지적 도전이어야 합니다.

> [!IMPORTANT]
> **참고 예시 (Las Palmitas 효과):**  
> 범죄와 싸우는 멕시코의 Las Palmitas 지역에서 200개 이상의 집이 거대한 무지개 축제로 변형되었습니다. 이 미적 개입 후 지역의 범죄율이 어느 정도 감소했고, 청소년들은 갱 대신 예술에 관심을 갖기 시작했습니다. 미적 변화는 사람들의 환경과 서로에 대한 존경(사회적 결속)을 재프로그래밍했습니다.
>
> **기대:** [PoArt] 목록에 들어갈 프로젝트는 위의 예시처럼 순수한 시각적 미학을 넘어 사회학적, 과학적 또는 철학적 인과 관계를 포함해야 합니다. "시간"은 돈으로 살 수 없는 유일한 자산이기 때문에 이 프로토콜에서 시간은 담보로 스테이크되고 증명되어야 합니다. 프로젝트의 개념적 기반은 너무 강력하고 보편적이어서 수년 후 가능한 CTO(Community Take Over) 시나리오에서도 커뮤니티가 이 유산을 물려받아 프로젝트의 혁신적 잠재력을 자율적으로 계속할 수 있어야 합니다.

### 5) 비알고리즘적 의지 (Non-Algorithmic Agency)

- **문제:** 완벽하지만 영혼이 없는, 반복적인 디지털 생산물.
- **[PoArt] 솔루션:** 실수를 할 수 있고, 위험을 감수하며, 감정적 변동을 경험하는 인간의 독특한 의지가 작품에서 느껴져야 합니다. 붓 터치의 불확실성, 재료의 예상치 못한 반응, 아티스트의 즉각적인 결정은 작품을 "기계 생산"과 구별하는 **생물학적 서명**입니다.

---

## c) 검증 및 위조 방지 메커니즘

이 시스템은 프로젝트가 "처음에만"이 아니라 "영원히" 신뢰할 수 있고 살아있도록 보장합니다.

### 📦 증거 패키지 (Evidence Pack - The Digital Twin)

모든 [PoArt] 인증 작품 뒤에는 투자자가 다운로드할 수 있는 암호화되고 타임스탬프가 찍힌 데이터 패키지가 있습니다:

- **RAW 비디오 녹화:** 생산 순간의 중단 없는 원시 영상.
- **메타데이터 분석:** 파일 생성 날짜, 사용된 장치 정보, 위치 데이터(도시-국가).
- **물리적 참조:** 작품이 물리적 세계에 존재한다는 증거  
  (예: 작품 옆에 놓인 현재 신문 또는 그 순간의 블록체인 데이터).

> *일관성 참고:* "증거 패키지"라는 용어는 이전 섹션의 **Evidence Pack → EvidenceRoot → NotarySeal** 체인에 연결됩니다; 즉 패키지의 무결성은 검증 가능한 봉인으로 표현됩니다.

### 🔄 365일 갱신 (The Sustainability Protocol)

- **혁명적 기능:** 암호화폐 프로젝트에서 "Dev"(개발자)는 토큰을 시장에 출시하고 보통 1-2개월 후 사라집니다(Soft Rug). [PoArt]는 이것을 불가능하게 만듭니다.
- **규칙:** "Verified Artist"(검증된 아티스트) 상태는 영구적이지 않습니다. **1년**만 유효합니다.
- **운영:** 아티스트/개발자는 365일마다 커뮤니티에 **새롭고, 크고, 증명 가능한 작품**을 제출해야 합니다.
- **예시 시나리오:** 2026년에 프로젝트를 시작했습니다. 2027년 1월에 시스템은 "증거 기간 만료" 경고를 제공합니다. 아티스트가 새 전시회, 새 물리적 작품 또는 새 기술 통합을 제시하지 않으면 프로젝트의 "신뢰 배지"가 떨어집니다.
- **결과:** 이 시스템은 **콘텐츠가 절대 구식이 되지 않도록** 보장하고 투자자가 *"개발자가 아직 여기 있나요?"*라는 두려움을 겪지 않도록 합니다. 프로젝트는 살아있는 스튜디오가 됩니다.

### 🚩 레드 플래그 프로토콜 (Red Flag Protocol)

**커뮤니티나 알고리즘에 의해 위조(AI 사용, 도난 작품, 조작된 비디오)가 감지되면:**

1. 인증서는 즉시 **"무효" (VOID)**로 표시됩니다.
2. 증거 패키지는 공개적으로 **"가짜"**로 라벨링됩니다.
3. 프로젝트는 [PoArt] 블랙리스트에 올라갑니다. 이것은 탈중앙화된 세계에서 **평판이 유일한 화폐**라는 사실을 강화합니다.
4. 어떤 출판물에서도 [PoArt] 문구를 포함할 수 없습니다; 유일한 유효 소스는 https://www.ilhanart.org/public-registry

---

## d) 결론: 카지노가 아닌 박물관

**Pump.fun과 탈중앙화 거래소(DEX)는 현재 안타깝게도 카지노입니다; 불빛이 깜박이고, 모두가 빠른 이익을 쫓으며, 하우스(사기꾼)가 항상 이깁니다. 우리가 여기서 프로젝트를 시작한 이유는 이 곳을 개선하려고 노력하고 있기 때문이며, 라이브 스트림을 통해 기존 청중에게 도달할 기존 데이터와 환경이 있기 때문입니다.**

**[PoArt]는 이 카지노 한가운데 지어진 요새입니다.**

- 🎰 카지노는 종이 게임에 의존합니다; 우리는 **물리적 현실**에 의존합니다.
- 🃏 카지노는 속임수에 열려 있습니다; 우리는 **투명한 증거**에 열려 있습니다.
- ⏳ 카지노는 일시적입니다; 우리는 **예술과 과학의 영원함**에 집중합니다.

**이 프로토콜을 사용하는 토큰은 단순한 "코인"이 아닙니다; 그 뒤에 땀, 페인트, 코드, 철학을 담은 디지털 주식입니다.**

---

## 🗳️ 6) 거버넌스 및 공개 레지스트리 (Governance & Public Registry)

**이 섹션의 목적: [PoArt] 표준을 "개인 신뢰" 평면에서 등록 + 검증 + 커뮤니티 감독이 있는 지속 가능한 공공 인프라로 전환하는 것입니다.**

### 6.1 Public Registry (공개 레지스트리)

- **Public Registry:** 모든 승인된 데이터는 `ilhanart.org/registry`(또는 GitHub Registry)에 기록됩니다.

**등록 로직 (권장 표준 - JSON 경로 형식):**

레지스트리에 들어가는 각 레코드는 최소한 다음과 같은 검증 가능한 핵심 필드를 포함합니다:

- **신원 및 상태:**
  - `certificate_id` (읽을 수 있는 참조)
  - `status` (active / void)
  - `void_reason` (있는 경우)
  - `visibility` (private / masked / public)
  - `created_at` (타임스탬프)

- **발급 기관:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **작품 정보:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (가능한 경우; 토큰 홀더 신원용)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **포렌식 데이터:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **암호화 증명:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **거버넌스:**
  - `governance.decision`
  - `governance.review_notes`

레지스트리는 두 개의 레이어를 가질 수 있습니다:
- **1)** 사람이 읽을 수 있는 인덱스 (웹 목록 / 검색 / 필터)
- **2)** 기계가 읽을 수 있는 매니페스트 (JSON 레코드; PFE 검증용)

**여기서 "레코드"는 PFE의 Evidence Pack → EvidenceRoot → NotarySeal 체인으로 검증 가능합니다. 레지스트리는 "주장"이 아닌 검증 대상을 제공합니다.**

---

### 6.2 PoArt Verified 신청 프로세스

**PoArt Verified 신청은 İlhanArt Gallery에서 5가지 PoArt 표준에 따라 평가됩니다. 커뮤니티 피드백이 고려되지만 최종 결정은 큐레이터 팀에 달려 있습니다. 결정은 투명하게 발표되고 ilhanart.org/registry에 기록됩니다.**

#### 신청 프로세스

**신청:**
- 아티스트/프로젝트가 PoArt Verified 신청을 제출합니다
- Evidence Pack이 준비됩니다 (비디오 녹화, 메타데이터, 라이브 스트림 링크)
- 신청서가 İlhanArt Gallery에 제출됩니다

**검토 (30일):**
- 갤러리 팀이 Evidence Pack을 상세히 검토합니다
- 5가지 PoArt 표준이 모두 확인됩니다:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- 아티스트와 인터뷰 (선택사항)

**커뮤니티 자문:**
- Evidence Pack은 신청 과정에서 공개적으로 공유됩니다
- 커뮤니티는 ilhanart.org를 통해 피드백을 제공할 수 있습니다
- 토큰 홀더(최소 10,000 $CULTURE)는 특히 제안을 제공할 수 있습니다
- **모든 피드백은 검토 과정에서 고려됩니다**
- **그러나 최종 결정은 큐레이터 평가에 달려 있습니다**

**결정:**
- 갤러리가 신청을 승인하거나 거부합니다
- 결정 이유가 투명하게 발표됩니다
- 승인되면 → PoArt Verified 배지
- 거부되면 → 6개월 후 다시 신청 가능

**투명성:**
- 모든 신청 및 결정은 ilhanart.org/registry에 기록됩니다
- 결정 기록이 공개적으로 게시됩니다:
  - 신청 날짜
  - 검토 과정 요약
  - 결정 (Approved / Rejected)
  - 결정 이유 (간단한 설명)
  - 커뮤니티 피드백 요약 (익명)

#### 왜 큐레이터 결정인가?

**품질 관리:**  
PoArt Verified 상태는 높은 표준을 가진 배지입니다. 큐레이터 평가는 이러한 표준이 유지되도록 보장합니다.

**투기적 조작 방지:**  
Pump.fun 토큰으로 전체 온체인 거버넌스(예: Realms, DAO 투표)는 기술적으로 불가능합니다. 오프체인 투표 시스템은 고래 조작과 조율된 공격에 취약합니다. 큐레이터 결정은 이 위험을 제거합니다.

**운영 효율성:**  
복잡한 투표 메커니즘 대신 빠르고 명확한 결정 과정. 아티스트는 30일 이내에 결과를 받습니다.

**커뮤니티 참여:**  
커뮤니티 피드백은 완전히 고려되며 결정 과정에 영향을 미칩니다. 그러나 최종 결정은 조작으로부터 보호된 큐레이터 팀에 달려 있습니다.

**미래:**  
프로젝트가 성숙해지면(2027+), 커뮤니티 자문 메커니즘이 강화될 수 있습니다. 그러나 큐레이터 표준 보호는 영구적입니다.

---

### 6.3 토큰 유틸리티 (Token Utility)

**$CULTURE 토큰 홀더에게 제공되는 혜택:**

**1. 갤러리 이벤트 우선 접근:**
- İlhanArt Gallery에서 연간 1주 전시 권리 (권리 양도 가능)
- Drop painting 할인
- 갤러리 그림 10%~30% 할인 권리

**2. PoArt Registry 전체 접근:**
- 모든 인증된 작품의 상세 기록
- Evidence Pack의 전체 버전
- 포렌식 검증 도구


**3. Advisory Voting:**
- PoArt Verified 신청에 대한 자문 권리
- 커뮤니티 피드백 채널 접근
- 거버넌스 토론 참여

**4. 독점 콘텐츠:**
- 스튜디오 비하인드 신 콘텐츠
- 아티스트 인터뷰 및 과정 비디오
- 기술 문서 접근

**참고:**  
토큰 홀더는 advisory vote(자문 투표)를 합니다. 최종 결정은 큐레이터 팀에 있습니다. 이 구조는 고래 조작과 투기적 공격을 방지하기 위해 선택되었습니다. 스테이킹 보상이 없는 이유는 단기 용병 자본이 아닌 장기 문화 참여자를 찾고 있기 때문입니다.

---

### 6.4 Metadata Sync (물리적 세계와의 동기화)

- **Metadata Sync:** 레지스트리의 기술 데이터는 물리적 자산과 100% 일치해야 합니다.

**"100% 일치"를 기술적으로 정의 (권장 명확성):**

- **최소 일치 (필수):**
  - 레지스트리의 `asset.fingerprints.sha256/sha512`는 손에 있는 파일의 해시와 **정확히 동일**해야 합니다.
  - 레지스트리의 `proof.notary_seal`이 재생성될 때(Evidence Pack이 있는 경우) **정확히 동일**해야 합니다.

- **물리적 참조 일치 (증거 유형):**
  - 라이브 스트림에서 표시된 물리적 작품 + 날짜/블록 참조와 같은 증거는 Evidence Pack과 일치해야 합니다.

- **프라이버시 준수:**
  - `masked` 가시성의 IP/위치와 같은 필드는 **마스킹 표준에 따라** 게시됩니다.

---

### 6.5 이의, 검토 및 취소 (Dispute & Revocation)

레지스트리는 "승인" 메커니즘만이 아니라; **위조에 대한 살아있는 감시** 메커니즘입니다.

- 이의가 시작되면 레코드가 **"review"** 모드로 전환될 수 있습니다.
- 위조가 감지되면 `status: void`로 표시되고 이유가 추가됩니다:
  - `void_reason` (AI 사용 / 도난 / 조작 등)
  - `revoked_at` (취소 시간)
- 취소 결정의 출처가 레지스트리에 명확하게 표시됩니다:
  - 큐레이터 검토 / 커뮤니티 이의 / 포렌식 분석 노트 (적용되는 것)

> **이 부분은 레지스트리에서 "Red Flag Protocol" 섹션의 VOID 개념에 해당합니다.**

---

### 6.6 예시 레지스트리 레코드 (기계 판독용)
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

> *참고: `asset.fingerprints.sha512` 및 기타 해시 값은 프레젠테이션 목적으로 단축되었습니다; 실제 구현에서는 전체 길이의 16진수 문자열이 사용됩니다.*

---

## 7) 🔐 기술 봉인 (NOTARY SEAL)

**PoArt Forensic Engine (PFE) v1.0**에 의해 생성된 흔들리지 않는 봉인 알고리즘:

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# [PoArt] 디지털 공증 및 포렌식 증거 프로토콜 (Beta v1.0)

> **"문화는 자본보다 큽니다. 오늘부터 작품을 보호하고 내일로 가져가세요."**

---

## 왜 공개인가?

진정한 보안은 투명성에서 옵니다. **Public Registry (공개 레지스트리)** 시스템 덕분에 세계 어디에서나 누구든지 손에 있는 파일이 원본인지 아닌지를 몇 초 안에 어떤 기관도 필요 없이 확인할 수 있습니다.

---

## 🧩 왜 여러 "가시성 모듈"이 있는가?

이것이 코드의 가장 중요한 부분입니다 (visibility 선택 메뉴). 이 옵션들은 사용자가 **"프라이버시 vs. 투명성"** 균형을 설정할 수 있게 합니다:

### 🔒 비공개 (Private)

- **시나리오:** 아티스트가 아직 작품을 공개하고 싶지 않지만 "나는 이 날짜에 이것을 만들었다"를 증명하기 위해 타임스탬프를 찍고 싶습니다.
- **코드가 하는 일:** 데이터를 데이터베이스에 쓰지만 `visibility: "private"` 라벨을 붙입니다. 나중에 "Public Read" 정책을 작성할 때 `WHERE visibility = 'public'`을 사용하여 이 레코드를 공개에서 숨길 수 있습니다.

### 🕶️ 마스킹됨 (Masked)

- **시나리오:** 아티스트가 투명성을 원하지만 집 주소(IP 위치)가 발견되는 것을 두려워합니다.
- **코드가 하는 일:** JavaScript 측에서 `maskIP`와 `maskLoc` 함수가 실행됩니다. IP 주소를 `88.241.***.***` 형식으로, 위치를 `***/TR` 형식으로 변환하고 검열된 버전을 데이터베이스로 보냅니다.
- **프라이버시 참고:** 마스킹은 브라우저에서 수행되며, Supabase는 실제 위치를 보지 못합니다. **그러나:** ipapi.co와 같은 타사 API가 위치 데이터에 사용되면 이 제공자들은 요청 시점에 IP 주소를 봅니다.
- **Masked 모드 봉인:** EvidenceRoot와 NotarySeal 계산은 마스킹된 forensics 데이터로 수행됩니다; 따라서 검증이 결정론적으로 유지됩니다.

### 🌍 공개 (Public)

- **시나리오:** 완전한 투명성. [PoArt] 표준에 따라 작품이 어디서, 언제, 어떤 네트워크에서 생산되었는지 공개적으로 선언됩니다.

---

## 💡 기술 혁신

PoArt는 단순한 파일 업로드 시스템이 아닙니다. 세 가지 다른 기술 레이어를 하나의 도가니에서 녹여 새로운 표준을 제시하는 **"포렌식 증거 체인" (Forensic Chain of Custody)** 엔진입니다.

**이 섹션에서 "엔진"으로 설명된 레이어는 이전 용어의 PoArt Forensic Engine (PFE) 코어에 해당합니다.**

### 1) Client-Side Hashing (최대 프라이버시)

작품 파일은 절대 서버에 업로드되지 않습니다. 브라우저 기반(Client-side) 엔진이 파일의 해시(디지털 요약)를 컴퓨터에서 계산합니다. 서버로는 이 지문과 메타데이터만 전송됩니다.

> **프라이버시 참고:** 작품 파일은 서버에 업로드되지 않으며 이 방식으로 보호됩니다. 그러나 forensics 데이터(IP/위치)는 선택된 가시성 모드(private/masked/public)에 따라 공유됩니다.

### 2) Forensic Data Fusion (포렌식 파워)

이것은 일반적인 타임스탬프보다 훨씬 많습니다. 시스템은 다음 데이터를 하나의 "Genesis Seal"에 결합합니다:

- **디지털 요약 (SHA-512):** 작품의 한 픽셀이라도 변경되면 깨지는 디지털 지문, 암호화 요약(SHA-512) 표준 사용.
- **위치 및 시간:** 거래가 수행된 밀리초 정밀도의 날짜, 국가, 도시 및 지역 데이터.
- **장치 신원:** 운영 체제, 브라우저 및 장치 유형 (User-Agent 분석).

---

## 🛡️ 사용 사례 및 혜택

아티스트, 작가 또는 디자이너라면 "나는 이것을 먼저 만들었다"라고 말하는 것만으로는 충분하지 않습니다, 증명해야 합니다.

**PoArt로 봉인된 작품:**

- **수학적 증명:** 파일의 한 픽셀이라도 변경되면 시스템이 감지합니다. 조작은 불가능합니다.
- **법적 근거:** 작품이 어떤 날짜에, 어떤 도시에서, 어떤 장치에서 봉인되었는지 기록됩니다.
- **즉시 인증서:** 몇 초 안에 QR 코드와 봉인이 있는 고유한 **"자산 신원 인증서"**를 생성합니다.

---

## ⚙️ 시스템 아키텍처 및 기술 사양

시스템은 높은 성능과 확장성에 초점을 맞춘 "Serverless" 아키텍처에서 설계되었습니다.

| 레이어 | 기술 | 설명 |
|--------|------|------|
| **암호화** | SHA-256 & SHA-512 | 이중 레이어 암호화 요약 |
| **데이터베이스** | Supabase (PostgreSQL) | JSONB 데이터 구조, RLS 정책 |
| **포렌식 데이터** | ipapi.co API | IP/위치/시간 트리플 |
| **렌더링** | html2canvas + jsPDF | Client-side PNG/PDF 생성 |
| **프론트엔드** | Vanilla JavaScript | 프레임워크 의존성 없음 |
| **보안** | Client-side hashing | 파일이 절대 서버에 업로드되지 않음 |

### 주요 기능

| 기능 | 세부사항 | 경쟁사? |
|------|----------|---------|
| **Drag & Drop UI** | 파일 드래그 앤 드롭, 즉시 미리보기 | ❌ 대부분 없음 |
| **Multi-Format Export** | PNG, JSON, PDF - 원클릭 | ⚠️ 제한적 |
| **Real-Time Preview** | 인증서 라이브 미리보기 | ❌ 없음 |
| **Privacy Controls** | Private/Masked/Public 옵션 | ❌ 없음 |
| **Client-Side Hashing** | 파일이 절대 서버로 가지 않음 | ✅ 일부만 |
| **Forensic Metadata** | IP, 위치, 장치, 시간 - 모두 포함 | ❌ 부분적 |
| **QR Verification** | 즉시 검증 QR 코드 | ⚠️ 제한적 |
| **Rate Limiting** | 스팸 보호 (RLS + Client) | ❌ 대부분 없음 |

---

## 🗺️ 로드맵: "Trustless" 미래

현재 버전 **(Beta v1.0)**은 최종 사용자에게 최대 속도, 쉬운 인터페이스, 무료 접근을 제공하도록 최적화되어 있습니다. 그러나 우리의 궁극적인 비전은 데이터베이스 관리자(우리)도 개입할 수 없는 구조로 전환하는 것입니다.

### Phase 1: Beta v1.0 (현재 활성화)

**인프라:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + IPFS backup)
- Gallery self-attestation (중앙화되지만 투명)

**토큰:**
- Platform: Pump.fun
- Liquidity: Raydium (automatic)
- Governance: Advisory only (커뮤니티 자문)

**목표:**
- 속도, UX 장벽 제거
- "마찰 없는" 보안 제공
- 커뮤니티 구축

**Token Utility (v1.0):**
- 갤러리 이벤트 우선 접근
- PoArt Registry 보기
- Advisory voting 권리

---

### 🚀 Phase 2: Decentralized Authority (2026 Q2-Q4)

이 단계는 완전히 "Client-Side"로 작동하는 구조에서 더 안전하고 탈중앙화된 구조로의 전환을 다룹니다.

| 기능 | 얻는 것? | Tech Stack | ETA |
|------|----------|------------|-----|
| **Edge Function INSERT** | 스팸 차단 + API Key 보안 | Supabase Edge (Deno) | Q2 2026 |
| **Wallet Signature** | 탈중앙화 신원 | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | 탈중앙화 아카이브 | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | 가짜 인증서 취소 | DB Schema Update | Q2 2026 |
| **Audit Log** | 포렌식 쿼리 기록 | Custom logs 테이블 | Q3 2026 |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain voting (x/web) + wallet signature
- Community representatives 선출 (첫 90일)
- Multi-sig operations wallet 제어
- Weighted advisory voting (whale cap 포함)

**Immutability:**
- IPFS 해시로 registry backup
- Bitcoin timestamp anchoring
- Cross-chain verification 준비

---

### Phase 3: 완전 탈중앙화 (2027+)

| 기능 | 목표 | ETA |
|------|------|-----|
| **On-Chain Registry** | Solana on-chain 기록 | Q1 2027 |
| **Enhanced Token Utility** | NFT mint, 고급 기능 | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **DID Integration** | 탈중앙화 신원 | Q3 2027 |
| **Community Governance** | 강화된 advisory system | Q4 2027 |
| **Legal Recognition** | 터키 법원에서의 유효성 | 2027-2028 |
| **API for Developers** | Public API endpoint | Q3 2027 |

**Governance Evolution:**
- v3.0: Hybrid model (큐레이터 + community weighted)
- 2028+: Full community governance (선택사항)
- 큐레이터 품질 관리는 항상 유지

---

## 🧬 프로토콜 데이터 구조 (JSON Schema)

**모든 [PoArt] 인증서는 다음 표준에서 생성된 휴대 가능하고 검증 가능한 JSON 신원 카드를 가집니다.**

> **참고:** 이 Identity JSON 형식은 사용자에게 제시되는 인증서 형식입니다. 레지스트리 레코드에서는 `identity.asset_data` 대신 `registry.asset`이 사용됩니다 (매핑: `identity.asset_data` == `registry.asset`).
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

## 🔬 기술 심층: 봉인 알고리즘

### 결정론적 해시 함수
```javascript
// 헬퍼 함수: Digest를 hex 문자열로 변환
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// String을 byte array로 변환
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Canonical forensics 문자열 생성 (v1.0: 고정 필드 순서 + UTF-8 + \n 구분자)
// Phase 2 참고: RFC 8785 (JCS)로 canonical JSON으로 전환 예정
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### NotarySeal 생성 프로세스 (완전 결정론적)
```javascript
// 1. FileHash 계산 (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Forensic 데이터 수집 (단일 timestamp 사용)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // 단일 timestamp 생성
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // 동일한 timestamp
  };
  
  return { forensics, timestamp };
}

// 3. EvidenceRoot 생성 (canonical encoding으로)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. NotarySeal 생성 (동일한 timestamp 사용)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// 마스킹 헬퍼 함수 (IPv4 및 IPv6 지원)
function maskIP(ip) {
  if (!ip) return "***";
  
  // IPv4 확인
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 또는 알 수 없는 형식
  return "***";
}
```

### 검증 흐름 (두 단계)

#### Quick Verify (빠른 검증)
```javascript
// 파일 해시만 확인 (빠른 레드 플래그)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Registry에서 가져오기
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // 해시 비교
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ 원본 - 파일 해시 일치"
    };
  } else {
    return {
      valid: false,
      message: "❌ 가짜 - 파일이 조작됨"
    };
  }
}
```

#### Full Verify (전체 검증)
```javascript
// EvidenceRoot와 NotarySeal을 재생성하여 검증
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Registry에서 가져오기
  const cert = await fetchFromRegistry(certificateId);

  // 1) FileHash 확인 (빠른 레드 플래그)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ 가짜 - 파일 해시 불일치" };
  }

  // 2) EvidenceRoot 재생성 (registry에 저장된 forensics로)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ 불일치 - EvidenceRoot가 맞지 않음" };
  }

  // 3) NotarySeal 재생성 (동일한 timestamp + signer_sig로)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ 불일치 - NotarySeal이 맞지 않음" };
  }

  // 선택사항: Phase 2에서 attestation_pubkey로 signer_sig도 검증
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ 서명 무효" };

  return { valid: true, message: "✅ 원본 - Full Verify 통과" };
}
```

> **중요 참고:**
> - **Quick Verify:** 빠른 사용을 위해 파일 해시만 확인.
> - **Full Verify:** 프로토콜의 모든 레이어(EvidenceRoot + NotarySeal) 검증.
> - 모든 해시 작업은 고정 인코딩과 구분자로 결정론적으로 수행됩니다.
> - **v1.0 canonicalization 표준:** 고정 필드 순서 + UTF-8 인코딩 + `\n` 구분자.
> - **Phase 2 계획:** RFC 8785 (JCS - JSON Canonicalization Scheme)로 canonical JSON으로 전환.
> - Masked 모드에서 EvidenceRoot와 NotarySeal 계산은 마스킹된 forensics로 수행됩니다.
> - 단일 timestamp가 전체 프로세스(forensics + NotarySeal)에서 사용됩니다; 결정론성이 보장됩니다.
> - **Forensics 필드 이름:** `ip_masked`, `location`, `device`, `timestamp` (코드와 registry 완전 호환).
> - **Registry 경로:** `certificate.asset.fingerprints` (verify 코드와 완전 호환).
> - **Registry의 signer_sig:** `proof.signer_sig` 필드는 Full Verify에 필요합니다.
> - SignerSignature 메커니즘은 Phase 2에서 Solana Wallet Adapter로 활성화됩니다; v1.0에서는 `attestation_pubkey`로 검증 가능.

---

## 📊 경쟁사 분석 (업데이트됨)

PoArt는 기존 솔루션의 부족함을 보완하는 "Sweet Spot"에 위치합니다.

| 기능 | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **비용** | 🆓 무료 | 🆓 | 💰 유료 | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ 매우 쉬움 | ❌ CLI | ⚠️ 보통 | ⚠️ 보통 | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ 라이브 | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3가지 모드 | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ 프라이버시 | ✅ | ❌ 업로드 | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ 완전 | ❌ | ❌ | ⚠️ 제한적 | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ 즉시 | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 로드맵 | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **터키어 지원** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**설명:**
- ✅ : 전체 지원 / 사용 가능
- ⚠️ : 제한적 / 유료 플랜에서
- ❌ : 없음 / 지원되지 않음
- 🔄 : 로드맵에 (개발 중)
- 🆓 : 완전 무료
- 💰 : 유료 / 구독 필요

### 경쟁사 부족함, PoArt 강점

| 부족함 | 경쟁사 | PoArt |
|--------|--------|-------|
| **사용 어려움** | CLI, API 지식, 지갑 필요 | 드래그 앤 드롭, 3클릭으로 완료 |
| **비용 장벽** | $50-500/월 구독 | 100% 무료 |
| **프라이버시** | 파일이 서버에 업로드됨 | Client-side, 파일이 절대 가지 않음 |
| **포렌식 데이터** | timestamp만 | IP, 위치, 장치, 시간 - 모두 |
| **터키어 지원** | 없거나 매우 제한적 | Native 언어 지원 |
| **오픈 소스** | 블랙박스 | GitHub에서 모든 코드 공개 |

---

## 📈 사용 통계 (2026 Q1 목표)

| 지표 | 목표 | 상태 |
|------|------|------|
| **총 인증서** | 1,000 | 🔄 진행 중 |
| **활성 사용자** | 500 | 🔄 진행 중 |
| **검증 수** | 5,000 | 🔄 진행 중 |
| **Uptime** | %99.9 | ✅ 활성 |
| **Avg Response Time** | <200ms | ✅ 최적 |

---

## 🌍 커뮤니티 & 지원

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 기여자

PoArt 프로토콜은 오픈 소스 커뮤니티의 기여로 계속 발전하고 있습니다.

**기여하려면:**
1. Fork 하세요
2. Feature branch 생성 (`git checkout -b feature/amazing-feature`)
3. Commit (`git commit -m 'Add amazing feature'`)
4. Push (`git push origin feature/amazing-feature`)
5. Pull Request 열기

### 🛠️ 지금 무엇이 필요한가요? (도움 요청)

PoArt 프로토콜 **Phase 2** 개발을 위해 다음 분야에서 경험 있는 개발자의 기여를 기다리고 있습니다:

* **Supabase Edge Functions:** 스팸 보호를 서버 측으로 이동.
* **Solana Web3.js:** Wallet Signing 통합.
* **IPFS / Arweave:** 아카이브 및 pinning 서비스 통합.
* **Community Tools:** X 투표, voting systems, analytics dashboard.

> 기능을 추가하기 전에 "Issues" 탭에서 토론을 시작해 주세요.

---

## 💬 마무리 노트

### Pump.fun과 현실

이 프로젝트는 Pump.fun에서 시작되었습니다 왜냐하면:
- ✅ 유동성 접근 (Raydium automatic migration)
- ✅ 기존 커뮤니티 접근
- ✅ 낮은 시작 비용

그러나 명확히 합시다:
- **토큰 가격**은 예술적 성공의 지표가 아닙니다
- **운영 예산**에는 토큰 가치가 중요합니다 (갤러리, 전시회, 인프라)
- **성공 지표:** Authenticated artworks + community engagement + 물리적 방문자

### 거버넌스와 탈중앙화

**v1.0 현실 (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (중앙화되지만 투명)
- Governance: Advisory only (큐레이터 최종 결정)
- Token utility: Gallery access + registry + NFT priority

**v2.0+ 비전 (2027+):**
- Registry: On-chain (Solana)
- Signatures: Wallet-based (탈중앙화)
- Governance: Hybrid (community advisory + curatorial quality)
- Token utility: Enhanced features + advanced access

이 구조는 초기 단계에서 **운영 효율성**과 **품질 관리**를 제공하면서 미래에 **커뮤니티 참여**를 높이는 길을 열어둡니다.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // 문화는 자본보다 큽니다*

## 🧾 라이선스

MIT License © 2026 İlhan Art Gallery Initiative

전체 조건은 [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE)를 참조하세요.

---

## 💬 크레딧

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**이 프로젝트는 [İlhan Art Gallery] 이니셔티브로 개발되었으며, 소스 코드는 투명성을 위해 공개되어 있습니다.**

**PROTOCOL V1.0 // SHA-512로 봉인됨.**

*© 2026 İLHAN ART | 작품, 이미지 및 아이디어의 모든 권리가 보호됩니다.*

---
