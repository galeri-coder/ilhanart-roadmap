# 📜 Thuật ngữ & Bảng từ kỹ thuật 🇻🇳

> **Phiên bản giao thức:** 1.0 (Ổn định)  
> **Tầm nhìn mạng:** 2025 → 3000 Lưu trữ  
> **Hệ sinh thái:** [PoArt] + [FPP] + [Michelangelo] + [Tầng Văn hóa]  
> **Trạng thái:** **HARD_LOCKED** (Tài liệu đang hoạt động)  
> **Tính toàn vẹn:** Niêm phong SHA-512 (Tương thích với công chứng kỹ thuật số)

---

## 🔰 Tổng quan Kiến trúc Phân tầng

| Tầng | Mục đích | Giao thức |
|:--|:--|:--|
| **L1** | Xác thực lao động | **PoArt (Proof of Art)** |
| **L2** | Lòng trung thành / Kinh tế | **FPP (Foundational Pillar Protocol)** |
| **L3** | Quản trị | **Khung Michelangelo (Động cơ Meritocracy)** |
| **L4** | Tích hợp văn hóa | **Tầng & Đặc quyền Văn hóa** |

Cấu trúc này bao quát toàn bộ sự hợp nhất giữa kỹ thuật và triết học của hệ sinh thái trong bốn tầng cơ bản.  
Người dùng mới có thể hiểu toàn bộ kiến trúc trong **2 phút** thông qua bảng này.

---

## 🧩 Cấp độ Thành viên — “Primer → Texture → Impasto”

| Cấp độ | Định nghĩa | Cơ sở Kỹ thuật |
|:--|:--|:--|
| **Primer (Cơ bản)** | Cấp nhập môn. Đã hoàn thành xác thực cơ bản nhưng chưa tích lũy ma sát thời gian (TWAB). | `0 < TWAB ≤ 10⁰` |
| **Texture (Kết cấu)** | Thành viên hoạt động tích cực, có số dư được tích lũy theo thời gian. | `10⁰ < TWAB ≤ 10²` |
| **Impasto (Lớp dày)** | Thành viên cốt lõi có điểm TWAB cao nhất, duy trì chu kỳ 365 ngày. | `TWAB > 10²` |

### Công thức xác định cấp độ

$$
\text{Tier}(u)=
\begin{cases}
\text{Primer},&0<\text{TWAB}_u\le10^0\\
\text{Texture},&10^0<\text{TWAB}_u\le10^2\\
\text{Impasto},&\text{TWAB}_u>10^2
\end{cases}
$$

---

## 📑 Mục lục

1. Trụ cột của Giao thức (Pillars of the Protocol)  
2. Vai trò & Thực thể (Roles & Entities)  
3. Chỉ số Kinh tế & Quản trị (Economic & Governance Metrics)  
4. Bảo mật & Xác thực (Security & Validation)  
5. Xác thực & Tính bền vững (Validation & Persistence)  
6. Giám sát Phi tập trung (Decentralized Supervision)  
7. Khung Michelangelo (Meritocracy Engine)  
8. Hệ số Nhân văn hóa & Cấp bậc (Cultural Multipliers & Ranking Levels)  
9. Ngưỡng & Chỉ số Mạng (Cut-off Thresholds & Network Metrics)  
10. Khung Trí tuệ (Intellectual Framework)  
11. Chống Sybil Nâng cao (Advanced Sybil Resistance)  
12. Di sản & Quản trị Thế hệ (Generational Legacy & Governance)  
13. Tầng Đặc quyền Văn hóa & Tích hợp Thế giới thực (Cultural Privilege Layers & Real-World Integration)  
14. Máy Trạng thái (State Machine)  
15. Tối thiểu On-chain / Tối đa Off-chain  
16. Cơ chế Kháng cáo & Tin cậy (Appeals / Mercii & Trust Mechanism)  
17. Mô hình Mối đe dọa (Threat Model & Counter Layers)  
18. Tuyên ngôn Quản trị Toàn cầu (Manifesto)  
19. Lộ trình & Ghi chú Tương lai (Roadmap & Future Notes)

---

## 🏛️ 1) Trụ cột của Giao thức (Pillars of the Protocol)

### **[PoArt] Proof of Art (v1.0)**

* **Định nghĩa:** Giao thức cốt lõi xác minh không chỉ tác phẩm nghệ thuật cuối cùng mà còn toàn bộ quá trình sáng tạo dựa trên dữ liệu kỹ thuật.  
* **Vấn đề được giải quyết:** Khi các công cụ AI tạo sinh phát triển, việc chứng minh lao động con người trong không gian kỹ thuật số trở nên khó khăn — làm giảm giá trị của nghệ thuật.  
* **Cách hoạt động:** Khi nghệ sĩ sáng tạo, họ nộp **Gói Bằng chứng (Evidence Pack)** ghi lại mọi giai đoạn. Giao thức đóng dấu thời gian dữ liệu này trên blockchain.  
* **Ví dụ:** Nếu một nghệ sĩ vẽ trong 40 giờ, nhật ký phát sóng, video tua nhanh (timelapse) và dấu vân tay kỹ thuật số sẽ được xác minh bởi [PoArt]. Không chỉ là “bức tranh hoàn chỉnh” mà là “40 giờ lao động con người” được lưu trữ vĩnh viễn.

---

### **[FPP] Foundational Pillar Protocol (v1.0)**

* **Định nghĩa:** Hệ thống xây dựng trụ cột kinh tế, quản trị và xã hội cho toàn bộ hệ sinh thái — thưởng cho lòng trung thành và sự đóng góp dài hạn.  
* **Vấn đề được giải quyết:** Xóa bỏ sự bất công trong thế giới crypto nơi “ai có tiền nhiều thì có quyền nhiều”, và ngăn chặn đầu cơ phá hoại hệ thống.  
* **Cách hoạt động:** Quyền biểu quyết và quản trị của người dùng được xác định bởi thời gian nắm giữ tài sản, không chỉ là số lượng.  
* **Ví dụ:** Một “cá voi” nắm giữ 1 triệu token mới vào hệ thống có quyền lực ít hơn thành viên trung thành nắm 100 token trong một năm.

---

## 👥 2) Vai trò & Thực thể (Roles & Entities)

Giao thức xác định rõ ràng “ai có thể làm gì” để giảm thiểu hiểu lầm và lạm dụng quyền.

- **Nghệ sĩ:** Tạo Evidence Pack cho [PoArt], khởi tạo đăng ký, và ký nhịp tim hằng năm (heartbeat).  
- **Người bảo trợ (Patron):** Được xếp hạng trong [FPP] dựa trên lòng trung thành và đóng góp; có quyền giám sát và phủ quyết (veto).  
- **Trình xác minh (Validator):** Xem xét Evidence Pack, đánh dấu mâu thuẫn và tham gia quá trình phủ quyết / kháng cáo.  
- **Công chứng viên kỹ thuật số (Digital Notary):** Xác minh bằng chứng + đồng thuận + dấu thời gian, ghi vào Sổ đăng ký Công khai (Public Registry).  
- **Public Registry:** Tầng lưu trữ danh tính vĩnh viễn cho tất cả bản ghi đã được xác minh (Verified / Legacy / Revoked).  
- **Lưu trữ bằng chứng (IPFS / Arweave / Archive):** Lưu dữ liệu thô ngoài chuỗi (off-chain); chỉ lưu gốc mật mã (hash root) trên blockchain.

---

## 📊 3) Chỉ số Kinh tế & Quản trị (Economic & Governance Metrics)

Phần này xác định mô hình toán học và giới hạn thời gian để đảm bảo ổn định kinh tế cũng như công bằng trong quản trị.  
Mục tiêu là hạn chế ảnh hưởng ngắn hạn của vốn bằng **ma sát thời gian**, đồng thời làm cho lòng trung thành dài hạn có thể đo lường và kiểm chứng được.

---

### 3.1) Cửa sổ thời gian (Time Windows) và định nghĩa Epoch

Trong giao thức này, thời gian không chỉ được xác định bởi một “epoch” mà bởi **ba cửa sổ khác nhau**, mỗi cửa sổ có mục đích riêng.

#### 3.1.1) Epoch Hoạt động (Operational Epoch)
Chu kỳ cơ bản cho báo cáo và cập nhật định kỳ.

- **Mặc định:** **7 ngày**  
- **Chức năng:** Báo cáo và cập nhật hàng tuần.

#### 3.1.2) Cửa sổ Bảo vệ Biểu quyết Quan trọng (Critical Vote Guard Window)
Xác định khoảng thời gian lịch sử được tính khi xác định quyền biểu quyết.

- **Lookback:** **30 ngày**  
- **Chức năng:** Ngăn chặn việc “mua quyền biểu quyết” ngay trước khi diễn ra cuộc bỏ phiếu quan trọng.  

> **Quy tắc:** Trong các cuộc biểu quyết quan trọng, sử dụng **lookback 30 ngày** thay vì **epoch 7 ngày**.

#### 3.1.3) Chu kỳ Toàn vẹn (Integrity Cycle)
- **Thời gian:** **365 ngày**  
- **Chức năng:** Gia hạn hàng năm thông qua xác minh Evidence Pack.  
> **Ghi chú v1.0:** Tham số 7 & 30 ngày được mã hóa cứng (hard-coded).

---

### 3.2) TWAB (Time-Weighted Average Balance)

TWAB là chỉ số chính đo lường **lòng trung thành** và **sự ổn định** của ví trong hệ sinh thái.

$$
\text{TWAB}=\frac{\sum_{i=1}^{n}(\text{Balance}_i\times\Delta t_i)}{\sum_{i=1}^{n}\Delta t_i}
$$

$\Delta t_i$ đại diện cho khoảng thời gian mà số dư được nắm giữ.

**Chỉ số thô tùy chọn:**

$$
\text{TWA}=\sum_{i=1}^{n}(\text{Balance}_i\times\Delta t_i)
$$

---

### 3.3) Quyền Biểu quyết (Voting Power)

$$
\text{VotingPower}=f(\text{TWAB},\text{EpochRules},\text{StatusTier})
$$

**Hiệu ứng Guard Window:** Trong các cuộc biểu quyết quan trọng, dùng dữ liệu 30 ngày lookback.

---

### 3.4) Điểm số Logarit (Logarithmic Power Scoring)

$$
\text{Score}=\log_{10}(\text{TWAB}+1)
$$

$$
\text{VotingPower}=\text{Score}\times g(\text{EpochRules},\text{StatusTier})
$$

| Số dư (TWAB) | Điểm ($\log_{10}$) | Phân tích Quyền lực |
|:--|:--|:--|
| 10 | 1.04 | Ảnh hưởng ban đầu |
| 1,000 | 3.00 | Tăng 100× số dư ≈ +3 điểm |
| 1,000,000 | 6.00 | Tăng 100,000× ≈ +6 điểm |

> **Mô phỏng:**  
> Để xem mô phỏng sức mạnh biểu quyết logarit, truy cập [PoArt Simulation Console](https://galeri-coder.github.io/ilhanart-protocol/[PoArt]/).

---

### 3.5) Tương thích FPP v1.0

- **Epoch Hoạt động:** 7 ngày  
- **Guard Window:** 30 ngày  
- **Chu kỳ Toàn vẹn:** 365 ngày  

Việc xác minh hàng năm bắt buộc thông qua Evidence Pack.

---

## 🛡️ 4) Bảo mật & Xác thực (Security & Validation)

### 4.1) Kho Thiên niên kỷ (Millennium Vault, Epoch 10 năm)

* **Định nghĩa:** Tài sản bị khóa trong thời gian ≥1 năm, trở thành hầm danh tiếng cao nhất trong hệ thống.  
* **Vấn đề được giải quyết:** Bảo vệ khỏi đầu cơ ngắn hạn và phá vỡ tầm nhìn dài hạn.  
* **Giải pháp:** Chỉ những người khóa tài sản ≥1 năm và có trạng thái “Pillar” mới có quyền tham gia quyết định trọng yếu.

---

### 4.2) Gói Bằng chứng (Evidence Pack)

**Định nghĩa:**  
Bộ dữ liệu kỹ thuật bắt buộc được sử dụng để xác minh trong [PoArt].

#### Nội dung Bắt buộc (Bộ ba Bằng chứng)
1. **Nhật ký trực tiếp:** Bản ghi phát sóng trực tiếp trong quá trình sáng tạo.  
2. **Video Time-lapse:** Quay toàn bộ quá trình sáng tác.  
3. **Dấu vân tay kỹ thuật số:** Hash được ký bởi ví của nghệ sĩ.

---

#### Củng cố v1.0 (Tầng Toàn vẹn Chuỗi)

Bộ ba này là cần thiết nhưng chưa đủ; mối liên kết giữa các tệp cũng phải được niêm phong:

4. **Bản kê Manifest:**  
   Dữ liệu thiết bị, độ phân giải, tốc độ khung hình, danh sách tệp, và checksum.

5. **Merkle Root / Chuỗi Hash:**  

$$
\text{EvidenceRoot} = \text{MerkleRoot}(\text{AllFiles})
$$

6. **Khung thử thách ngẫu nhiên (Tuỳ chọn):**  
   Kiểm tra ngẫu nhiên yếu tố con người trong quá trình phát sóng.  
   Ví dụ: cầm vật thể cụ thể hoặc viết từ khóa đặc biệt.  
   Làm tăng chi phí cho các cuộc tấn công AI / deepfake.

---

**Vấn đề được giải quyết:**  
Cung cấp câu trả lời kỹ thuật cho câu hỏi: *“Tác phẩm này có thực sự do con người tạo ra không?”*

---

### 4.3) Phòng chống Sybil & Flash-loan

* **Định nghĩa:** Bảo vệ toán học chống lại tài khoản bot và các cuộc tấn công vay nhanh.  
* **Giải pháp:** TWAB + Guard Window trong [FPP] khiến chuyển động vốn ngắn hạn không còn tác dụng trong quản trị.

---

### 4.4) Công chứng viên kỹ thuật số (Digital Notary: Dấu Niêm phong Giao thức)

* **Định nghĩa:** Cơ chế tự vận hành xác thực dữ liệu [PoArt] và [FPP], sau đó đóng dấu vào **Sổ đăng ký Công khai**.

### Vấn đề được giải quyết

1. **Quyền lực tập trung:** Loại bỏ sự thiên vị chủ quan.  
2. **Thao túng dữ liệu:** Bản ghi được xác minh không thể bị chỉnh sửa.  
3. **Gatekeeping:** Nghệ sĩ được tiếp cận kho lưu trữ toàn cầu dựa trên bằng chứng, không dựa vào thị hiếu cá nhân.

### Chu trình Xác thực (Bộ lọc Ba tầng)

- **Độ đầy đủ Evidence Pack:** Bộ ba + Manifest + EvidenceRoot  
- **Giám sát Dân chủ:** Veto / Quorum  
- **Chữ ký Mã hóa:** Xác minh SHA-512

### Dấu Niêm phong Toán học

$$
\text{NotarySeal}=\text{Hash}(\text{EvidenceRoot}+\text{VoterConsensus}+\text{TimeStamp})
$$

### Kết quả (2026–3000)
Các tác phẩm có dấu NotarySeal trở thành một phần của **di sản văn hóa nhân loại**.

---

## 🏛️ 5) Xác thực & Tính bền vững (Validation & Persistence)

### 5.1) Xác minh ví lạnh 365 ngày (Cold Wallet Verification)

**Định nghĩa:**  
Tài sản được giữ liên tục trong ví lạnh trong **365 ngày**.

**Vấn đề được giải quyết:**
1. Giao dịch giả (Wash Trading)  
2. Áp lực đầu cơ  
3. Rủi ro bảo mật ví nóng  

---

#### Cập nhật v1.0: “Thang phạt” thay thế “Đặt lại cứng”

Thay vì đặt lại toàn bộ TWAB khi có giao dịch sớm, hệ thống áp dụng cơ chế **phạt giảm dần**:

**Vi phạm lần 1 (chuyển trước 365 ngày):**

$$
\text{EffectiveTWAB} = \text{TWAB} \times 0.20
$$

**Vi phạm lần 2:**

$$
\text{EffectiveTWAB} = \text{TWAB} \times 0.05
$$

**Vi phạm lần 3:**  
Trạng thái bị **Thu hồi (Revoked)**.

> Thang phạt này ngăn thao túng rút/nạp nhanh mà không phạt nặng người dùng trung thực.

---

## 🗳️ 6) Giám sát Phi tập trung (Decentralized Supervision)

### 6.1) Cơ chế Phủ quyết Cộng đồng (Community Veto Mechanism, Ngưỡng 40%)

* **Định nghĩa:** Hệ thống dân chủ cho phép thiểu số chất lượng cao ngăn chặn các đăng ký hoặc thay đổi giao thức mới.

#### Cập nhật v1.0: “Quorum + Veto” Khóa kép

- **Quorum (Tỷ lệ tham gia tối thiểu):** Ít nhất **25%** tổng quyền biểu quyết đang hoạt động phải tham gia.  
- **Ngưỡng Veto:** Hợp lệ khi đạt **40% tổng quyền biểu quyết**.

**Vấn đề được giải quyết:**
1. Tấn công Sybil  
2. Tham nhũng hoặc cấu kết trong biểu quyết  
3. Mua quyền biểu quyết hàng loạt  

* **Ví dụ:** Nếu một tác phẩm AI được nộp dưới danh nghĩa “nghệ sĩ thật”, cộng đồng có thể sử dụng quyền phủ quyết 40% để ngăn chặn việc xác nhận tác phẩm đó.

---

### 6.2) Quản trị Khẩn cấp / Hội đồng Dự phòng (Emergency Governance / Fallback Council)

**Mục đích:** Ngăn chặn bế tắc khi tỷ lệ tham gia thấp.

**Định nghĩa:**

$$
\text{Deadlock}=(\text{ParticipationRate}<25\%)\land(\text{ProposalTimeout}>7\text{ days})
$$

Khi `Deadlock = TRUE`:

1. **Fallback Council** (10% thành viên Impasto hàng đầu) được trao quyền tạm thời.  
2. Quyết định cần có `Council Consensus ≥ ⅔`.  
3. Nếu không được phê chuẩn qua trưng cầu dân ý trong 30 ngày, quyết định sẽ bị hủy tự động.  
4. Tất cả quyết định được ghi lại bằng hàm băm SHA-512 trong **Sổ Khẩn cấp (Emergency Ledger)**.

---

## ⚙️ 7) Khung Michelangelo (Meritocracy Engine)

### 7.1) Triết lý Michelangelo

* **Định nghĩa:** Động cơ danh tiếng và xếp hạng của hệ sinh thái Ilhan Art.  
* **Khẩu hiệu:** *“Bạn không thể mua đường lên đỉnh.”*  
* **Ví dụ:** Một “cá voi” với hàng triệu token sẽ không thể vượt qua người đã cống hiến cho văn hóa suốt nhiều năm.

---

### 7.2) Công thức Trạng thái: Thời gian × Đóng góp

$$
\text{Status}=\text{HoldingTime}\times\text{CulturalContribution}
$$

* **HoldingTime:** Số ngày tài sản được giữ trong ví lạnh liên tục.  
* **CulturalContribution:** Các đóng góp hữu hình như dịch thuật, giám tuyển, triển lãm hoặc phát triển.  
* **Vấn đề được giải quyết:** Loại bỏ “người nắm giữ thụ động” không đóng góp cho cộng đồng.

---

## 📊 8) Hệ số Nhân văn hóa & Cấp bậc (Cultural Multipliers & Ranking Levels)

### 8.1) Hệ số Nhân văn hóa (Cultural Multiplier)

* **Định nghĩa:** Hệ thống thưởng bổ sung cho đóng góp văn hóa.  
* **Ứng dụng:**
  - **Impasto (JP/TR/EN):** Dịch các văn bản khoa học / triết học / nghệ thuật (+4.500 điểm ví dụ).  
  - **Texture:** Giám sát chất lượng đăng ký và tham gia phủ quyết.  
  - **Hạ tầng:** Đóng góp mã nguồn, tài liệu, hỗ trợ hệ thống.  

* **Ví dụ:** 1.000 ngày nắm giữ + một bản dịch lớn có thể vượt qua hàng nghìn người dùng khác.

---

### 8.2) Cấp bậc (Ranking Levels)

| Cấp | Phạm vi / Điểm | Vai trò & Quyền lực |
|:--|:--|:--|
| **Impasto (≥100k)** | Cấp Hiến pháp | Định hình chiến lược & phí dài hạn |
| **Texture (50k–99k)** | Cấp Giám tuyển | Giám sát, biểu quyết, và điều phối nội dung |
| **Primer (<50k)** | Cấp Thành viên | Đề xuất & biểu quyết cơ bản |

> Cấp bậc được cập nhật động theo hoạt động và độ ổn định đóng góp trong [FPP].

---

## 📈 9) Ngưỡng & Chỉ số Mạng (Cut-off Thresholds & Network Metrics)

### 9.1) Ngưỡng gia nhập (Entry Thresholds)

Ngưỡng được đặt ra khi hệ thống đạt độ ổn định nhất định.

- **Ngưỡng Impasto:** **≥ 100.000 điểm**  
- **Top 100 gia nhập:** **≥ 45.000 điểm**

* **Vấn đề được giải quyết:** Duy trì chất lượng của hệ thống, tránh tràn ngập người tham gia không đóng góp thực sự.

---

### 9.2) TWAB Toàn mạng (Network TWAB)

* **Định nghĩa:** Tổng năng lực TWAB của toàn bộ hệ sinh thái (ví dụ: 4.2M Network TWAB).  
* **Chức năng:** Giá trị càng cao, hệ thống càng khó bị thao túng.  
* **Thống kê 24 giờ:** Tổng số đăng ký [PoArt] mới trong 24 giờ qua.

---
## 🎨 10) Khung Trí tuệ (Intellectual Framework)

### 10.1) IPOW: Bằng chứng Công việc Trí tuệ (Intellectual Proof of Work)

* **Định nghĩa:** Động cơ danh tiếng thưởng dựa trên đóng góp trí tuệ như nghệ thuật, giáo dục và dịch thuật — chứ không chỉ nắm giữ tài sản.  
* **Vấn đề được giải quyết:** Chống lại văn hóa “staking thụ động”.  
* **Ví dụ:** Ví có 1 triệu token nhưng không đóng góp trí tuệ sẽ được đánh giá thấp hơn ví có 100 token nhưng tích cực tham gia dịch thuật hoặc viết tài liệu.

---

### 10.2) Bộ lọc Trung thực Trí tuệ (Intellectual Honesty Filter)

* **Định nghĩa:** Cơ chế xác minh xem người dùng có thực sự hiểu chủ đề trước khi được phép biểu quyết.  
* **Vấn đề được giải quyết:** Biểu quyết mù quáng, spam AI, và thao túng tự động.

#### Cập nhật v1.0: Bằng chứng về Hiểu biết (Proof of Understanding)

Thay vì bài kiểm tra trắc nghiệm cổ điển, hệ thống yêu cầu người dùng chứng minh hiểu biết thực sự:

**Tùy chọn A (Tóm tắt):** Tóm tắt đề xuất trong 100 từ.  
**Tùy chọn B (Phân tích rủi ro):** Xác định hai rủi ro và giải thích một.  
**Tùy chọn C (Phản biện):** Nêu lý do logic nếu không đồng ý.

Module này kiểm tra hiểu biết thực sự và ngăn bot tự động tham gia biểu quyết.

---

## 🛡️ 11) Chống Sybil Nâng cao (Advanced Sybil Resistance)

### 11.1) Cơ chế Turnstile

* **Định nghĩa:** Ngưỡng tối thiểu để tham gia (ví dụ: 250 token ILHAN).  
* **Triết lý:** “Không phải bức tường, mà là cánh cửa quay.”  
* **Vấn đề được giải quyết:** Ngăn tạo hàng nghìn tài khoản giả.  
* **Ví dụ:** Tấn công 10.000 bot trở nên phi kinh tế vì mỗi tài khoản cần nắm 250 token.

---

### 11.2) Bộ lọc Ví Zombie (Zombie Wallet Filter)

* **Định nghĩa:** Yêu cầu hoạt động định kỳ để chứng minh ví vẫn đang sử dụng.  
* **Quy tắc:** Ví không hoạt động bị xóa khỏi sổ đăng ký toàn cầu dù có điểm cao.  
* **Mục tiêu:** Duy trì hệ thống chỉ gồm người dùng thật đang sống và đóng góp.

---

## 🧬 12) Di sản & Quản trị Thế hệ (Generational Legacy & Governance)

* **Định nghĩa:** Truyền lại danh tiếng và quyền cho người thừa kế của thành viên Impasto duy trì trạng thái trong thời gian dài.  
* **Vấn đề được giải quyết:** Bảo đảm giá trị văn hóa không biến mất khi một thành viên qua đời.  
* **Triển khai:** Quyền này mở cho người chứng minh lòng trung thành ≥4 năm và được ghi trên blockchain.

---

### 12.2) Quyền Quản trị Nghị viện (Parliamentary Governance Rights)

| Cấp | Phạm vi | Quyền & Chức năng |
|:--|:--|:--|
| **Impasto (≥100k)** | Hiến pháp | Chính sách, chiến lược, phí |
| **Texture (50k–99k)** | Giám tuyển | Giám sát, bỏ phiếu, quản lý |
| **Primer (<50k)** | Cơ bản | Đề xuất nhỏ & quyết định phụ |

* **Vấn đề được giải quyết:** Thay thế dân chủ ngẫu nhiên bằng hệ thống meritocracy dựa trên công trạng và đóng góp.

---

## 🌍 13) Tầng Đặc quyền Văn hóa & Tích hợp Thế giới thực  
(Cultural Privilege Layers & Real-World Integration)

> **Ghi chú:** Các đặc quyền này sẽ được triển khai giai đoạn 2026–2030 như một phần của “Lộ trình Tương lai”.

---

### 13.1) Quyền Triển lãm Hàng năm (Annual Exhibition Right)

* **Định nghĩa:** Quyền triển lãm tác phẩm được xác minh bởi [PoArt] tại Ilhan Art Gallery trong 1 tuần mỗi năm.  
* **Vấn đề được giải quyết:** Giảm chi phí cao cho nghệ sĩ độc lập khi tiếp cận không gian vật lý.  
* **Triển khai:** Người đạt đủ điều kiện có thể đặt lịch qua hệ thống và sử dụng không gian dựa trên điểm danh tiếng văn hóa.

---

### 13.2) Giá Nghệ thuật Động (Dynamic Art Pricing)

* **Định nghĩa:** Hệ thống API xác định mức chiết khấu dựa trên trạng thái văn hóa của người dùng.  
* **Cấu trúc:**  
  - **Impasto (≥100k):** Giảm giá 50%+  
  - **Texture (50k–99k):** Giảm giá 30%  
  - **Primer (<50k):** Giảm giá 10%  
* **Triết lý:** “Không mặc cả — giá trị đến từ công sức.”  
* **Mục tiêu:** Thúc đẩy công bằng qua sự minh bạch thuật toán và ghi nhận văn hóa.

---

### 13.3) Tích hợp Hệ sinh thái Vật lý (Physical Ecosystem Integration)

- Hiệu sách, quán cà phê, trung tâm văn hóa  
- Mã QR xác minh trạng thái & quy đổi đặc quyền  

---

### 13.4) Lao động vượt Trên Tư bản (Labor Over Capital)

* **Định nghĩa:** Đặc quyền thực không dựa trên vốn, mà dựa trên **đóng góp văn hóa và độ bền thời gian**.  

**Công thức Toán học:**

$$
\text{ClaimRight} \propto \text{CulturalScore} + \log_{10}(\text{Balance})
$$

Điều này có nghĩa là quyền của cá nhân tăng theo đóng góp văn hóa,  
trong khi tài sản chỉ ảnh hưởng theo dạng logarit — làm cho **lao động con người có giá trị hơn tư bản**.

**Ví dụ:**  
Người dùng có 250 token nhưng tích cực đóng góp có quyền cao hơn người có 100.000 token nhưng không hoạt động.

---

## 🧩 14) Máy Trạng thái (State Machine)

Quy trình của [PoArt] và trạng thái trong [FPP] tuân theo chuỗi sau:

1. **Draft** (Bản nháp)  
2. **Submitted** (Đã nộp)  
3. **Under Review** (Đang xem xét)  
4. **Challenged** (Bị khiếu nại)  
5. **Verified** (Được xác nhận / Có NotarySeal)  
6. **Renew Due** (Đến hạn gia hạn)  
7. **Legacy Archive** (Lưu trữ di sản)  
8. **Revoked** (Bị thu hồi / Hết hiệu lực)

> Luồng này giúp theo dõi rõ ràng trạng thái hiện tại của mỗi đăng ký.

---

## 🔗 15) Tối thiểu On-chain / Tối đa Off-chain  
(Minimal On-chain / Maximal Off-chain)

### Dữ liệu On-chain

- EvidenceRoot (Merkle Root)  
- NotarySeal  
- TimeStamp  
- Signer (Nghệ sĩ / Chủ sở hữu)  
- Trạng thái (Verified / Legacy / Revoked)  
- Giấy phép (ví dụ: Move Permit)

### Dữ liệu Off-chain

- Video gốc  
- Time-lapse  
- Ghi chú kỹ thuật  
- Manifest chi tiết  
- Lưu trữ (IPFS / Arweave)

**Mục tiêu:** Tăng khả năng kiểm chứng mà không làm blockchain quá tải.

---

## 🏛️ 16) Cơ chế Kháng cáo & Lòng tin (Appeals / Mercii & Trust Layer)

Cơ chế kháng cáo hoạt động như hàng rào niềm tin thể chế trong hệ thống.

- **Bộ lọc chiến lược:** Kháng cáo phải dựa trên bằng chứng, không phải cảm xúc.  
- **Quyền Veto cộng đồng:** 40% Veto + Quorum kép.  
- **Chống Bot / Chống Sybil:** Xác minh thông qua staking hoặc định danh Solana.  
- **Đóng băng Evidence Pack:** Khi kháng cáo mở, toàn bộ bằng chứng bị khóa bằng “time-lock”.  
- **Minh bạch:** Mọi vụ kháng cáo đều được công khai kèm mốc thời gian.

---

## 🧨 17) Mô hình Mối đe dọa (Threat Model & Counter Layers)

| Mối đe dọa | Lớp bảo vệ |
|:--|:--|
| **Tấn công Sybil** | Turnstile + Bộ lọc Zombie + Quorum |
| **Flash-loan** | TWAB + Guard Window + Điểm logarit |
| **Chi phối cá voi (Whale Domination)** | Điểm logarit + TWAB |
| **Giao dịch giả (Wash Trading)** | Kiểm tra ví lạnh + Thang phạt |
| **Cấu kết (Collusion)** | Veto + Kiểm tra Evidence Pack + Minh bạch |
| **Chỉnh sửa dữ liệu** | EvidenceRoot + Chữ ký SHA-512 + NotarySeal |
| **Mua phiếu / Hối lộ** | Time-lock + Quorum + Điểm danh tiếng |
| **Deepfake / giả mạo AI** | Khung kiểm thử ngẫu nhiên + Manifest + Chuỗi Hash |

---

## ⚖️ 18) Tuyên ngôn Quản trị Toàn cầu  
(Global Governance Manifesto)

> **Ghi chú Tầm nhìn:** Cấu trúc toán học được phát triển bởi [FPP] và [PoArt]  
> Không chỉ dành cho nghệ thuật — mà là **một mô hình quản trị mới có thể sửa chữa những hệ thống chính trị toàn cầu đã thất bại**.

---

### 18.1) Kết thúc chế độ tài phiệt (End of Plutocracy)

* **Định nghĩa:** Plutocracy = Quyền lực được quyết định bởi sự giàu có.  
* **Giải pháp của giao thức:** Chấm điểm logarit làm giảm ảnh hưởng của vốn — khiến thời gian và nỗ lực trở thành nền tảng quyền lực.  
* **Lý do:** Tương lai thuộc về người tạo giá trị trí tuệ, không chỉ người giàu.

---

### 18.2) Nghị viện Công đức (The Meritocratic Parliament)

Thay thế nền chính trị đại chúng và tiền bạc  
bằng cấu trúc trao quyền cho người hiểu tài liệu và đóng góp trí tuệ thông qua IPOW.

---

### 18.3) An ninh Bầu cử (Election Security)

- **Turnstile:** Ngăn bot chiếm quyền biểu quyết.  
- **TWAB:** Loại bỏ hành vi “mua phiếu” ngắn hạn.  
- **40% Veto + Quorum:** Bảo đảm thiểu số vẫn có quyền kiểm soát.

---

### 18.4) Kết luận: Cứu Lấy Tương Lai (Saving the Future)

Hệ thống này trao phần thưởng cho **nỗ lực có thể chứng minh**,  
không phải cho sự giả dối.  
Thành công thuộc về người lên kế hoạch theo thế kỷ,  
không phải người nghĩ theo tuần.  
Và giảm lỗi con người bằng **quản trị có thể kiểm chứng bằng toán học**.

---

## 📅 19) Lộ trình & Ghi chú Tương lai (Roadmap & Future Notes)

Toàn bộ tài liệu này hợp thành tầm nhìn dài hạn của hệ sinh thái **Ilhan Art**, kéo dài từ **2026 đến 3000**.  
Mỗi phiên bản mới (v1.1, v1.2, …) mở rộng hệ thống kỹ thuật, bao gồm **kết nối API**, **điểm POS thực**, và **liên kết thực tế**.

---

### Hướng phát triển chính

1. **v1.1 (2027):**  
   - Tích hợp hệ thống danh tiếng Off-chain  
   - Module Heartbeat bán tự động để gia hạn hằng năm  
   - Tỷ lệ phạt TWAB động  

2. **v1.2 (2028):**  
   - Ra mắt **Cơ chế xác minh văn hóa thực (RCV)**  
   - Mở rộng hợp tác giữa phòng trưng bày nghệ thuật và nền tảng NFT lai  
   - Thêm **Thẻ xác minh (Proof Card)** với mã QR  

3. **v1.3 (2029):**  
   - Tích hợp **AI Assisted Verification** cho kiểm chứng video & dấu vân tay số  
   - Tầng bảo mật SHA-512 đa cấp cho Notary & Validator  

4. **v1.4 (2030):**  
   - Kích hoạt **Quản trị Toàn cầu (Global Governance)** cho nghệ thuật  
   - Xây dựng mạng lưới văn hóa & meritocracy quốc tế  

---

### Tầm nhìn Di sản (Legacy Vision)

> Hệ thống này không chỉ là giao thức — mà là **sự biểu hiện của ý thức văn hóa nhân loại.**  
> Viết lại định nghĩa về giá trị, liêm chính và nghệ thuật.

Nguyên tắc bất biến:

- **Nghệ thuật là bằng chứng của lao động, không phải ảo giác.**  
- **Quyền lực phải phát sinh từ thời gian và công đức, không phải tài sản.**  
- **Mỗi tầng văn hóa là một mã sống.**

---

## 🔐 Chữ ký Băm (v1.0 Hard-Locked)

SHA-512 | Metadata | TimeStamp | Digital Notary
