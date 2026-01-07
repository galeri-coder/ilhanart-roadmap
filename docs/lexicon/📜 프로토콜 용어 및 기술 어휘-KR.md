---
title: "일한 아트 프로토콜 (Ilhan Art Protocol)"
version: "1.0 (안정 버전)"
status: "HARD_LOCKED"
integrity: "SHA-512"
ecosystem: "[PoArt] + [FPP] + [Michelangelo] + [Cultural Layers]"
last_updated: "2026-01-07"
---

# 📜 프로토콜 용어 및 기술 어휘 🇰🇷
> **프로토콜 버전:** 1.0 (안정)  
> **네트워크 비전:** 2025 → 3000 글로벌 아카이브  
> **에코시스템:** [PoArt] + [FPP] + [Michelangelo] + [Cultural Layers]  
> **상태:** **HARD_LOCKED** (운영 중 문서)  
> **무결성:** SHA-512 해시 서명 (디지털 공증 호환)

---

## 🔰 계층형 아키텍처 개요 (Layered Architecture Overview)

| 계층 | 목적 | 프로토콜 |
|:--|:--|:--|
| **L1** | 인간 노동 증명 | **[PoArt] Proof of Art** |
| **L2** | 충성도 및 경제 구조 | **[FPP] Foundational Pillar Protocol** |
| **L3** | 거버넌스 및 평가 엔진 | **[Michelangelo Framework]** |
| **L4** | 문화 통합 및 현실 연계 | **Cultural Layers & Privileges** |

---

## 🧩 멤버십 구조 — “Primer → Texture → Impasto”

| 등급 | 정의 | 기술 기반 |
|:--|:--|:--|
| **Primer (기초)** | 검증 완료 후 초기 등급. 시간가중평균잔고(TWAB)가 아직 낮음. | `0 < TWAB ≤ 10⁰` |
| **Texture (중간)** | 일정 수준의 TWAB을 유지하며 지속적으로 참여하는 회원. | `10⁰ < TWAB ≤ 10²` |
| **Impasto (상급)** | 365일 이상 지속 보유하며 최고 TWAB 점수를 달성한 회원. | `TWAB > 10²` |

$$
\text{Tier}(u)=
\begin{cases}
\text{Primer},&0<\text{TWAB}_u\le10^0\\
\text{Texture},&10^0<\text{TWAB}_u\le10^2\\
\text{Impasto},&\text{TWAB}_u>10^2
\end{cases}
$$

> 모든 등급은 시간적 안정성과 문화적 기여도에 따라 동적으로 조정된다.

---

## 🏛️ 1) 프로토콜의 기둥 (Pillars of the Protocol)

### **[PoArt] 예술 증명 프로토콜 (Proof of Art, v1.0)**
**정의:** 작품의 완성 결과뿐 아니라 **창작 과정 전체**를 기술적 데이터로 검증하는 시스템.  
**문제 해결:** 생성형 AI로 인해 인간의 창작 노동이 식별되지 않음 → 진정한 예술 가치의 하락.  
**작동 방식:** 예술가는 창작 과정의 각 단계를 포함한 **증거 팩(Evidence Pack)** 을 생성하고,  
프로토콜은 이를 타임스탬프와 함께 블록체인에 봉인한다.  
**예시:** 40시간 동안 제작된 그림은 영상, 로그, 해시 서명을 통해 ‘결과물’뿐 아니라 **인간의 40시간 노동 자체**를 증명한다.

---

### **[FPP] 기본 기둥 프로토콜 (Foundational Pillar Protocol, v1.0)**
**정의:** 충성도와 지속적 참여를 보상하는 거버넌스·경제 시스템.  
**해결 대상:** 단기 투기와 자본 집중으로 인한 거버넌스 왜곡.  
**원리:** 영향력은 보유 금액이 아닌 **보유 기간과 안정성**에 의해 결정된다.  
**예시:** 1백만 토큰을 보유한 신규 투자자보다, 100토큰을 1년 유지한 파트론이 더 높은 발언권을 가진다.

---

## 👥 2) 역할 및 엔티티 (Roles & Entities)

- **아티스트 (Artist):** [PoArt] 증거 팩을 제작하고 연간 검증을 수행.  
- **파트론 (Patron):** [FPP] 내에서 충성도 및 기여도를 기반으로 영향력 획득.  
- **검증자 (Validator):** 증거 팩의 무결성을 검토하고 이상을 표시.  
- **디지털 공증인 (Digital Notary):** 증거 + 합의 + 타임스탬프를 검증하여 공공 레지스트리에 기록.  
- **공공 레지스트리 (Public Registry):** Verified / Legacy / Revoked 상태를 영구 보존.  
- **증거 저장소 (Evidence Storage):** IPFS 또는 Arweave 기반 오프체인 저장. 해시 루트만 온체인 기록.

---

## 📊 3) 경제 및 거버넌스 지표 (Economic & Governance Metrics)

### 3.1) 시간 윈도우 및 에포크 정의 (Time Windows & Epochs)

| 유형 | 기간 | 목적 |
|:--|:--|:--|
| **운영 에포크 (Operational Epoch)** | 7일 | 주기적 업데이트 및 로그 동기화 |
| **보호 윈도우 (Guard Window)** | 30일 | 투표 직전의 자본 조작 방지 |
| **무결성 주기 (Integrity Cycle)** | 365일 | 연간 검증 및 재서명 수행 |

---

### 3.2) 시간가중평균잔고 (TWAB — Time Weighted Average Balance)

$$
TWAB = \frac{\sum_{i=1}^{n}(Balance_i \times \Delta t_i)}{\sum_{i=1}^{n}\Delta t_i}
$$  

**보조지표:**

$$
TWA = \sum_{i=1}^{n}(Balance_i \times \Delta t_i)
$$

> 시간 단위별 잔고 유지 비율을 계산하여 장기 참여의 정당성을 측정한다.

---

### 3.3) 투표 권한 함수 (Voting Power Function)

$$
VotingPower = f(TWAB, EpochRules, StatusTier)
$$  

> 보호 윈도우(30일) 내 기록이 유효한 투표권을 결정한다.

---

### 3.4) 로그 스코어링 모델 (Logarithmic Power Scoring)

$$
Score = \log_{10}(TWAB + 1)
$$  
$$
VotingPower = Score \times g(EpochRules, StatusTier)
$$

| TWAB | 로그 스코어 | 영향 수준 |
|:--|:--|:--|
| 10 | 1.04 | 기본 영향 |
| 1,000 | 3.00 | 중간 영향 |
| 1,000,000 | 6.00 | 최고 영향 |

> 시뮬레이션 콘솔에서 직접 계산 확인 가능:  
> [https://galeri-coder.github.io/ilhanart-protocol/[PoArt]/](https://galeri-coder.github.io/ilhanart-protocol/[PoArt]/)

## 🛡️ 4) 보안 및 검증 (Security & Validation) 🇰🇷

### 4.1) 밀레니엄 볼트 (Millennium Vault)
**정의:**  
연 단위로 자산을 잠그는 최상위 신뢰 계층 저장소.  
**목적:**  
단기 투기 자본의 영향을 제거하고, 2025~3000년의 장기 거버넌스 비전을 보존한다.  
**참여 조건:**  
[FPP] 내 “Foundational Pillar” 등급 보유자이면서, 최소 1년 이상의 잠금 주기를 완료한 회원만이 전략적 결정권을 가진다.

---

### 4.2) 증거 팩 (Evidence Pack)
**정의:**  
[PoArt] 검증 프로세스에서 제출이 필수적인 기술적 데이터 묶음.  
**목표:**  
예술 작품의 진위와 창작 과정을 기술적으로 증명하기 위한 필수 레이어.

#### 증명의 삼위일체 (Trinity of Proof)
1. **라이브 로그 (Live Logs):** 실시간 작업 영상 및 서버 기록.  
2. **타임랩스 영상 (Process Timelapse):** 제작 초기부터 결과물까지의 모든 프레임.  
3. **디지털 지문 (Digital Fingerprint):** 예술가 지갑 서명으로 생성된 해시값.  

---

#### 암호 무결성 계층 (Cryptographic Integrity Layer)
4. **캡처 매니페스트 (Capture Manifest):**  
   사용된 장비, 해상도, 프레임율, 파일 해시값 및 체크섬 포함.  

5. **머클 루트 / 해시 체인 (Merkle Root / Hash Chain):**
$$
EvidenceRoot = MerkleRoot(AllFiles)
$$
   모든 증거 파일은 단일 루트로 압축되어 불변의 해시 트리로 체인에 기록된다.  

6. **랜덤 챌린지 프레임 (Random Challenge Frames):**  
   창작 중 무작위 인증 요청(예: 특정 물체 제시, 문구 작성 등)을 통해  
   인간성과 실시간성을 증명 → Deepfake 또는 AI 위조를 방지.

**결과:**  
이 구조는 인간 창작 행위임을 기술적으로 입증하는 디지털 증명 체계이다.

---

### 4.3) Sybil 및 플래시론 공격 방어
**개념:**  
가짜 계정 및 대규모 임시 자본의 거버넌스 침투를 방지.  
**대응:**  
TWAB + Guard Window의 조합은 단기 자본 이동에 의한 투표 왜곡을 무효화한다.

---

### 4.4) 디지털 공증 (Digital Notary Seal)
**정의:**  
[PoArt] 및 [FPP]의 모든 검증 결과를 체인에 영구 보관하는 스마트 계약 기반 시스템.  

**3단계 검증 구조:**  
1. 증거 무결성 (Trinity + Manifest + EvidenceRoot)  
2. 커뮤니티 합의 (Veto / Quorum)  
3. 암호 서명 (SHA-512)  

**수학적 정의:**  
$$
NotarySeal = Hash(EvidenceRoot + VoterConsensus + TimeStamp)
$$

**효과:**  
모든 예술 작품은 이 서명 이후 **“문화적 진본 데이터 유닛”** 으로 불변화된다.  
→ 2026~3000년까지의 공증 유효성을 보장.

---

## 🏛️ 5) 검증 및 지속성 (Validation & Persistence) 🇰🇷

### 5.1) 365일 콜드월렛 검증 (Cold Wallet Validation)
**정의:**  
자산은 최소 365일 동안 하드웨어 지갑(Ledger, Trezor 등)에 연속 보관되어야 함.  

**방지 효과:**  
1. 워시 트레이딩 (Wash Trading)  
2. 단기 투기 압력  
3. 핫월렛 해킹 리스크  

---

#### 단계적 제재 구조 (Penalty Ladder)
**1차 위반:**  
$$
EffectiveTWAB = TWAB \times 0.20
$$  
**2차 위반:**  
$$
EffectiveTWAB = TWAB \times 0.05
$$  
**3차 위반:**  
상태 = Revoked (무효화)

> 실수에 대한 완전한 처벌을 피하면서도 투기적 거래를 억제하는 구조.

---

#### 안전 이동 예외 (Move Permit / Time-Lock)
- 이동 허가서(Move Permit) 요청 제출  
- 짧은 기간의 Time-Lock 발동  
- 커뮤니티 감시 (Veto + Quorum) 유지  
- 온체인에는 허가 및 신규 주소 링크만 기록  

---

### 5.2) 증거 팩 검증 절차 (Verification of Evidence Pack)
필수 요소:  
1. 실시간 로그  
2. 프로세스 영상  
3. 기술 메타데이터  
4. EvidenceRoot  

> 검증의 초점은 ‘결과물’이 아닌 **창작 과정** 그 자체에 있다.

---

### 5.3) 연간 하트비트 (365-Day Heartbeat)
- 모든 등록 기록은 1년마다 재서명 필수.  
- 만료 30일 전 자동 알림.  
- 미갱신 기록은 자동으로 “Legacy Archive” 상태로 전환.  

**목표:**  
데이터 신선도 유지 및 휴면 아카이브의 정리.

---

## 🗳️ 6) 분산형 감독 시스템 (Decentralized Supervision) 🇰🇷

### 6.1) 커뮤니티 거부 메커니즘 (Community Veto Mechanism)
**정의:**  
최소 40%의 TWAB 비중으로 소수 집단이 제안을 거부할 수 있는 민주적 보호장치.  

**조건:**  
- Quorum ≥ 25% 활성 참여율  
- Veto ≥ 40% 가중 TWAB  

**방어 대상:**  
1. Sybil 공격  
2. 담합 및 매수  
3. 투표 조작  

> 예시: AI 생성 작품이 [PoArt] 인증을 받더라도,  
> 40% TWAB 거부로 온체인 기록이 차단될 수 있다.

---

### 6.2) 비상 거버넌스 및 대체 평의회 (Emergency Governance / Fallback Council)
**목적:**  
참여율 저하로 인한 의사결정 정지(Deadlock)를 해소.

**논리식:**  
$$
Deadlock = (ParticipationRate < 25\%) \land (ProposalTimeout > 7\,days)
$$

**조건 충족 시:**  
1. 상위 10% Impasto 회원으로 평의회를 구성.  
2. 의결은 최소 2/3 이상의 합의 필요.  
3. 30일 내 커뮤니티 투표로 재확인되지 않으면 자동 무효.  
4. 모든 과정은 SHA-512 서명과 함께 **Emergency Ledger**에 기록.

---

## ⚙️ 7) 미켈란젤로 프레임워크 (The Michelangelo Framework, Meritocracy Engine) 🇰🇷

### 7.1) 미켈란젤로 철학 (Michelangelo Philosophy)
**정의:**  
[Ilhan Art] 에코시스템의 실력 기반 거버넌스 엔진.  
자본 중심 구조 대신 문화적 기여를 통한 정당성을 부여.  

**원칙:**  
“돈이 아닌 노동과 문화가 정상에 오른다.”

**목적:**  
지식·예술적 기여를 재정 자본보다 우선시하는 공정한 생태계 구축.  

**예시:**  
1,000,000 토큰을 보유하지만 비활성인 투자자보다,  
지속적으로 번역·교육·큐레이션을 수행하는 사용자가 더 높은 지위를 획득.

---

### 7.2) 상태 공식 (Status Formula)
$$
Status = HoldingTime \times CulturalContribution
$$

- **HoldingTime:** 콜드월렛에서 지속 보유한 일수.  
- **CulturalContribution:** 번역, 교육, 문서화, 코드 기여, 큐레이션 등.  
**목적:**  
시간과 지적 노력을 결합하여 진정한 기여 기반 정당성을 산출한다.

---

## 📊 8) 문화 승수 및 등급 체계 (Cultural Multipliers & Rank Tiers) 🇰🇷

### 8.1) 문화 승수 (Cultural Multiplier)
**정의:**  
장기적인 문화 기여를 정량화하고 보상하는 지표.  
**적용 영역:**  
| 분야 | 설명 | 가중치(점수) |
|:--|:--|:--|
| 번역 (Translation) | 예술·철학 문헌의 번역 활동 | +4,500 |
| 큐레이션 (Curation) | 검증 및 전시 기획, 기록 보존 | +2,000 |
| 인프라 (Infrastructure) | 코드, 문서화, 오픈소스 구축 | +3,000 |
| 교육 (Education) | 강의, 콘텐츠 확산, 학술 지원 | +1,500 |

**수학적 모델:**  
$$
FinalScore = BaseScore \times (1 + CulturalMultiplier)
$$

> 경제적 보유 뿐 아니라, 문화적 노력 또한 영향력을 산출하는 주요 요소로 통합된다.

---

### 8.2) 등급 계층 (Rank Tiers)
**정의:**  
[Ilhan Art Protocol] 내 모든 거버넌스 권한은 아래의 3단계 구조에 따라 정의된다.

| 등급 | 점수 범위 / 자격 | 권한 및 역할 |
|:--|:--|:--|
| **Impasto (≥100k)** | 헌법 계층 | 전략 수립, 수수료 조정, 에코시스템 방향 설정 |
| **Texture (50k–99k)** | 큐레이션 계층 | 검토, 큐레이션, 투표 관리 |
| **Primer (<50k)** | 기초 계층 | 제안 제출 및 소규모 결정 참여 |

> 등급은 고정되지 않으며, TWAB와 문화 기여도에 따라 지속적으로 재평가된다.

---

## 📈 9) 임계값 및 네트워크 지표 (Cut-off Thresholds & Network Metrics) 🇰🇷

### 9.1) 진입 임계값 (Entry Thresholds)
**정의:**  
네트워크 내 품질 유지와 거버넌스 희석 방지를 위한 최소 진입 기준.  

| 구분 | 필요 점수 | 설명 |
|:--|:--|:--|
| **Impasto** | ≥100,000 | 완전한 거버넌스 권한 부여 |
| **Top 100** | ≥45,000 | 주요 정책 참여자 |
| **Entry** | ≥250 | 최소 참여 기준선 |

**목표:**  
네트워크 확장 시에도 영향력 비율을 유지하고 투기적 참여를 차단한다.

---

### 9.2) 네트워크 TWAB 지수 (Network TWAB Index)
**정의:**  
전체 사용자 TWAB 합산값을 네트워크 안정성 지표로 사용.  
**의미:**  
값이 높을수록 시스템이 안정적이며, 외부 조작에 대한 저항력이 커진다.  
**갱신 주기:**  
24시간마다 새로운 [PoArt] 검증 레코드와 함께 자동 갱신.

---

## 🎨 10) 지적 프레임워크 (Intellectual Framework) 🇰🇷

### 10.1) 지적 작업 증명 (IPOW — Intellectual Proof of Work)
**정의:**  
금융 스테이킹을 넘어선 고가치 **지적·문화적 노동**을 측정하는 시스템.  
**메커니즘:**  
번역, 코드 작성, 아카이브 구축, 교육, 연구 등을 모두 문화적 노동으로 간주.  

**예시:**  
- 1,000,000 토큰 보유, 기여 없음 → 낮은 등급  
- 100 토큰 보유, 문서 번역 지속 → 높은 등급  

**목표:**  
지적 노력과 창작 활동을 네트워크의 핵심 가치로 편입.

---

### 10.2) 지적 성실성 필터 (Intellectual Honesty Filter)
**정의:**  
투표나 제안 제출 전에 참여자가 내용 이해도를 입증하도록 하는 검증 메커니즘.  
**목적:**  
AI 자동투표, 무지성 참여, 스팸 제안 등을 방지.  

**v1.0 절차:**  
A. 제안을 100자 이내로 요약.  
B. 잠재 리스크 2개와 그 중 1개의 이유 명시.  
C. 반대 의견 1개 제시.  

> “기억 기반”이 아닌 “이해 기반”의 거버넌스를 실현하기 위한 인지적 필터.

---

## 🛡️ 11) 고급 Sybil 저항 메커니즘 (Advanced Sybil Resistance) 🇰🇷

### 11.1) 턴스타일 메커니즘 (Turnstile Mechanism)
**정의:**  
시스템 진입 최소 조건으로 250 ILHAN 토큰이 필요.  
**철학:** “벽이 아니라 개찰구를 설치하라.”  
**목적:**  
대량 봇 계정 생성을 경제적으로 불가능하게 만든다.  
**예시:**  
10,000개의 봇 계정을 만들려면 2,500,000 토큰이 필요 → 비현실적 공격 비용.

---

### 11.2) 좀비 지갑 필터 (Zombie Wallet Filter)
**정의:**  
365일마다 지갑의 디지털 서명을 통해 ‘생존 신호(heartbeat)’를 전송해야 함.  
**규칙:**  
미서명 지갑은 자동으로 네트워크에서 제거.  
**목표:**  
실제 활동 중인 인간 사용자만이 네트워크에 잔존하도록 보장.

---

## 🧬 12) 세대 유산 및 거버넌스 (Generational Legacy & Governance) 🇰🇷

### 12.1) 세대 상속 (Generational Inheritance)
**정의:**  
연속 4년(1,460일) 이상 활동한 Impasto 회원은 공식 상속인을 지정할 수 있다.  
**목표:**  
회원의 사망, 분실, 비활동으로 인한 문화 자산 손실 방지.  
**절차:**  
- 연속 4년 이상의 활동 기록 확보 후 기능 활성화.  
- 상속은 다중 서명(multisig)으로 체인 상에서 검증 및 봉인.  

---

### 12.2) 의회형 거버넌스 권리 (Parliamentary Governance Rights)
**정의:**  
문화·기술·전략 세 분야로 나뉜 의회형 권한 구조.

| 등급 | 권한 영역 | 책임 |
|:--|:--|:--|
| **Impasto (≥100k)** | 헌법 / 전략 | 프로토콜 정책, 수수료, 전략 방향 결정 |
| **Texture (50k–99k)** | 관리 / 큐레이션 | 검증, 큐레이션, 투표 감독 |
| **Primer (<50k)** | 제안 / 미시적 관리 | 소규모 제안 제출 및 참여 |

> 감정적 다수결 대신, 지식과 기여를 기반으로 한 **실력 민주주의** 구현.

---

## 🌍 13) 문화 특권 계층 및 현실 통합 (Cultural Privilege Layers & Real-World Integration) 🇰🇷

> 주의: 본 장은 2026–2030 하이브리드 통합 로드맵의 일부로,  
> 디지털 거버넌스와 물리적 문화 생태계를 연결하기 위한 설계를 다룬다.

---

### 13.1) 연간 전시권 (Annual Exhibition Right)
**정의:**  
[PoArt] 검증과 [FPP] 평판 점수를 충족한 아티스트/파트론은  
매년 **Ilhan Art Gallery**에서 7일간 전시를 열 수 있는 권리를 가진다.  

**목적:**  
자본 중심이 아닌 문화적 공로를 기반으로 한 **민주적 전시 접근권** 보장.  

**메커니즘:**  
- 온체인 캘린더를 통해 자동 예약  
- 전시 슬롯은 문화 기여도와 신뢰 점수에 따라 자동 배분  
- 임대료 없음, 시스템 수수료 최소화  

---

### 13.2) 동적 예술 가격 시스템 (Dynamic Art Pricing, JSON-Linked Discounts)
**정의:**  
회원의 문화적 등급에 따라 자동으로 가격이 조정되는 API 기반 할인 시스템.  

| 등급 | 할인율 |
|:--|:--|
| **Impasto (≥100k)** | 50% 이상 |
| **Texture (50k–99k)** | 30% |
| **Primer (<50k)** | 10% |

**철학:**  
“흥정이 아닌, 증명된 가치에 따라 거래하라.”  

**기술 구조:**  
- 가격 데이터는 JSON 포맷으로 스마트 계약과 연동  
- API는 [FPP] 지수 및 CulturalMultiplier를 참조하여 실시간 산출  

---

### 13.3) 물리 생태계 통합 (Physical Ecosystem Integration)
**정의:**  
[Ilhan Art Protocol]이 실제 도시 문화망과 상호 작용하도록 설계된 오프체인 연계 레이어.  

**구성 요소:**  
- 제휴 네트워크: 서점, 카페, 예술 센터, 갤러리  
- QR 인증: 오프라인 공간에서 지갑 및 지위 검증  
- JSON API: 실시간 회원 검증 및 권한 확인  

**효과:**  
디지털 정체성이 현실의 문화 경험으로 확장되어,  
“웹3 문화 시민권” 개념을 실질적으로 구현한다.

---

### 13.4) 자본보다 노동 (Labor Over Capital)
**정의:**  
경제적 부보다 인간의 창의적 노동을 우선시하는 가치 알고리즘.  

**공식:**  
$$
ClaimRight \propto CulturalScore + \log_{10}(Balance)
$$

**예시:**  
- 사용자 A: 250 ILHAN + 지속적 창작 → 높은 ClaimRight  
- 사용자 B: 100,000 ILHAN + 비활동 → 낮은 ClaimRight  

**철학:**  
투표, 전시, 경제 보상 모두 “기여에 의한 정당성”으로 재조정된다.  
→ **플루토크라시(자본 지배)**에서 **노동 민주제(Laborocracy)**로 전환.

---

## 🧩 14) 기록 상태 기계 (State Machine — Lifecycle of a Record) 🇰🇷

### 프로세스 흐름 (Process Flow)
1. **Draft (초안)** → 로컬 생성  
2. **Submitted (제출됨)** → 체인 업로드  
3. **Under Review (검토 중)** → 검증자 확인  
4. **Challenged (이의 제기됨)** → 이의 발생  
5. **Verified (검증 완료)** → [Digital Notary] 서명 부여  
6. **Renew Due (갱신 예정)** → 연간 알림  
7. **Legacy Archive (보관 상태)** → 미갱신 아카이브  
8. **Revoked (취소됨)** → 규정 위반 혹은 다중 제재  

---

### 상태 전이 규칙 (State Transition Rules)

| 현재 상태 | 다음 상태 | 조건 |
|:--|:--|:--|
| Draft | Submitted | 아티스트 업로드 완료 |
| Submitted | Under Review | 검증자 승인 |
| Under Review | Verified | 합의율 ≥ 66% |
| Under Review | Challenged | 이의 발생 |
| Challenged | Revoked | 이의 승인 |
| Challenged | Verified | 커뮤니티 재검증 통과 |
| Verified | Legacy | 연간 서명 미실시 |
| Legacy | Revoked | 연간 감시 실패 |

> 모든 상태는 체인에서 추적 가능하며, 투명한 감사 기록으로 남는다.

---

## 🔗 15) 최소 온체인 / 최대 오프체인 (Minimal On-chain / Maximal Off-chain) 🇰🇷

### 온체인 데이터
- EvidenceRoot (Merkle Root)  
- NotarySeal  
- TimeStamp  
- Signer (서명자 주소)  
- Status (Verified / Legacy / Revoked)  
- Permit (이동 또는 상속 기록)

### 오프체인 데이터
- 원본 영상, 오디오, 타임랩스  
- 기술 로그 및 메타데이터  
- 캡처 매니페스트  
- IPFS / Arweave 아카이브  

**목표:**  
검증 가능성을 유지하면서 체인 부하 최소화.  
**무결성:**  
요청 시 SHA-512 서명을 통해 오프체인 데이터 교차 검증 가능.

---

## 🏛️ 16) 항소 및 이의 절차 (Appeals & Objection Mechanism) 🇰🇷

### 16.1) 원칙 (Principles)
- **증거 기반:** 모든 항소는 구체적 데이터와 함께 제출되어야 함.  
- **감정 배제:** 모욕적·비논리적 주장은 자동 기각.  
- **투명성:** 항소 진행 전 단계가 타임스탬프와 함께 공개됨.  
- **동결 규칙:** 조사 중 Evidence Pack은 변경 불가 상태로 잠금.

---

### 16.2) 커뮤니티 보호 장치 (Community Safeguards)
- 거부 한계: 40% TWAB 가중  
- 정족수(Quorum): ≥ 25% 참여  
- Sybil 방어: Turnstile + 스테이킹 검증  
- AI 차단: 자연어 필터로 스팸 항소 제거  

---

### 16.3) 항소 생명 주기 (Appeal Lifecycle)
1. 항소 시작 (Initiated)  
2. 증거 동결 (Evidence Freeze)  
3. 커뮤니티 검토 (Review)  
4. 7일간 투표 (Vote)  
5. 결과 봉인 (SHA-512 Hash)  

> 모든 항소 결과는 공공 레지스트리와 연결되어 투명하게 기록된다.

---

## 🧨 17) 위협 모델 및 대응 체계 (Threat Model & Countermeasures) 🇰🇷

| 위협 | 대응 메커니즘 |
|:--|:--|
| Sybil 공격 | Turnstile + Zombie Filter + Quorum |
| 플래시론 공격 | TWAB + Guard Window + 로그 스코어링 |
| 대규모 고래 지배 | 로그 기반 가중치 + TWAB 안정화 |
| 워시 트레이딩 | 콜드월렛 검증 + 단계적 제재 |
| 담합 및 매수 | Veto + 투명 감사 원장 |
| 데이터 변조 | EvidenceRoot + SHA-512 + NotarySeal |
| 투표 매수 | Time-lock + 가중 정당성 평가 |
| Deepfake 위조 | 랜덤 챌린지 프레임 + 해시 연쇄 |

> 모든 방어 규칙은 [FPP] 내 버전 관리 체계 하에 보존된다.

---

## ⚖️ 18) 최종 선언 — 글로벌 거버넌스 청사진 (Final Manifesto — Blueprint for Global Governance) 🇰🇷

> “예술은 프로토타입이며, 거버넌스는 그 캔버스이다.”

[PoArt]와 [FPP]의 융합을 통해,  
문화적 진정성과 민주적 정당성이 동일한 수학적 구조로 보호될 수 있음을 입증한다.

---

### 18.1) 부의 지배의 종말 (End of Plutocracy)
**문제:**  
부와 자본 집중이 거버넌스를 왜곡함.  
**해결:**  
- 로그 스코어 모델로 부의 영향력 제한  
- 시간과 노동을 합법성의 핵심으로 재정의  

**원칙:**  
소유 ≠ 창작 → 기여가 정당성을 만든다.

---

### 18.2) 실력주의 의회 (Meritocratic Parliament)
- 대중 인기나 자본이 아닌, 이해와 기여로 대표 구성  
- 거버넌스를 ‘숙련된 행위’로 정의  
- 정치적 감정보다 기술적 책임을 중시  

---

### 18.3) 선거 무결성 (Electoral Integrity — SHA-512 기반)
- **Turnstile:** 봇 기반 유권자 생성 방지  
- **TWAB:** 단기 토큰 이동 무력화  
- **Veto + Quorum:** 소수 감시권 확보  

> 암호적 수학에 의해 지탱되는 새로운 디지털 헌법의 설계.

---

### 18.4) 미래 선언 (Manifesto — Saving the Future)
**정의:**  
이 프로토콜은 단순한 예술 인증 체계가 아니라,  
천년 단위의 문명 모델을 위한 사회·경제적 원형이다.  

**비전:**  
- 검증된 노력 > 단기 이익  
- 장기적 지속성 > 즉각적 만족  
- 수학적 공정성 > 정치적 편향  

> “자동화의 시대, 인간의 가치는 창조하려는 의지에서 비롯된다.”

---

## 📅 19) 로드맵 및 미래 계획 (Roadmap & Future Notes) 🇰🇷

| 단계 | 연도 | 주요 내용 |
|:--|:--|:--|
| **v1.0** | 2026 | 핵심 검증 및 공증 모듈 확립 |
| **v1.1** | 2027 | 공공 API 및 시뮬레이션 콘솔 |
| **v1.2** | 2028 | 현실 연계 (POS / QR 통합) |
| **v2.0** | 2030 | 자동 거버넌스 및 교차 프로토콜 인덱싱 |

**목표:**  
2026–3000년까지 이어지는 *Ilhan Art Millennium Vision*의  
기술적·문화적 기반을 확립한다.

---

## 🔐 해시 서명 (Hash Signature, v1.0 Hard-Locked) 🇰🇷
- 커뮤니티 감시 상시 활성화  
- 허가된 주소 및 기록만 체인에 봉인  

**시간 파라미터:**  
- Operational Epoch: 7일  
- Guard Window: 30일  
- Integrity Cycle: 365일  

**연간 재검증:**  
모든 Evidence Pack에 대해 SHA-512로 시행.

---
