# 📚 THUẬT NGỮ & KHÁI NIỆM - TỪ ĐIỂN
> **"Hiểu ngôn ngữ của giao thức này chính là hiểu tầm nhìn của nó."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Cơ Sở Hạ Tầng Cốt Lõi

**PoArt Forensic Engine (PFE)** đại diện cho tầng logic cốt lõi và hoạt động kỹ thuật đằng sau giao thức [PoArt]. Đây là "động cơ pháp y" nhận dữ liệu sản xuất thô của tác phẩm nghệ thuật và chuyển đổi nó thành **bằng chứng số** có thể xác minh và không thể thay đổi.

### 🧩 Tại Sao Gọi Là "PoArt Forensic"?

- **PoArt (Proof of Art - Bằng Chứng Nghệ Thuật):** Trọng tâm của động cơ là liên kết giá trị của tài sản số không phải với đầu cơ mà với **quy trình sản xuất có thể chứng minh được**.
- **Forensic (Xác Minh Pháp Y):**
  - **Định Nghĩa Kỹ Thuật:** Phương pháp tiếp cận thuật toán và chuỗi ghi chép để xác minh rằng dữ liệu liên quan đến quy trình sản xuất (nét cọ, timelapse, nhật ký) không bị thao túng.
  - **Tầng Triết Học:** Tuyên bố chuyển đổi sản xuất của con người có chứa **thời gian, nỗ lực và chi phí quyết định** thành thực tế có thể đo lường được, trái ngược với "đầu ra tức thì" của trí tuệ nhân tạo.

> Ghi chú: Tích hợp blockchain (ví dụ: Solana) không phải là lõi của PFE; nó được xử lý riêng như một **Chain Anchor Layer** để xác minh/đăng ký.

### 🛠️ Phạm Vi Kỹ Thuật v1.0

**PoArt Forensic Engine (PFE) v1.0** được xây dựng trên **3 trụ cột chính** thay vì các mô hình tài chính phức tạp:

1. **Hashing & Sealing (Băm & Niêm Phong):**  
   PFE xử lý tất cả các phần tử trong Evidence Pack (tệp tác phẩm, video, JSON/nhật ký, chữ ký, v.v.) một cách xác định và tạo ra giá trị **NotarySeal** duy nhất.

   **Các khái niệm cốt lõi (v1.0):**
   - **FileHash (dấu vân tay tác phẩm):** Hash được tạo từ byte của tệp tác phẩm.
   - **EvidenceRoot (gốc gói bằng chứng):** Tóm tắt gốc đại diện cho tính toàn vẹn của Evidence Pack (Merkle root hoặc canonical manifest hash).
   - **NotarySeal (con dấu cuối cùng / Đầu Ra PFE):** Con dấu cuối cùng được tạo từ sự kết hợp của EvidenceRoot + thời gian + chữ ký.

   **Công Thức (được trình bày rõ ràng cho nhà đầu tư):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Định Nghĩa Canonical Payload (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Ghi chú: Giá trị được gọi là đầu ra PFE là **NotarySeal**. Cơ chế **SignerSignature** sẽ được kích hoạt trong Giai đoạn 2 (với Solana Wallet Adapter); v1.0 hiện tại sử dụng chữ ký attestation của hệ thống. Khóa công khai attestation được công bố trong trường `issuer.attestation_pubkey` của registry.

2. **Indexing (Lập Chỉ Mục):**  
   Ghi lại ví nào đã gửi **Labor Proof (Bằng Chứng Lao Động)** cho tác phẩm nào vào ngày nào vào một tầng ghi chép minh bạch và có thể truy vấn.  
   *(Tầng này có thể là cơ sở dữ liệu; tích hợp chuỗi được định nghĩa riêng là "Chain Anchor Layer".)*

3. **Verification (Xác Minh):**  
   Khi tính xác thực của tác phẩm bị tra vấn, PFE xử lý lại bằng chứng thô; kiểm tra bằng sự chắc chắn toán học xem các giá trị **EvidenceRoot / NotarySeal** được tính toán có khớp với bản ghi trong kho lưu trữ hay không.

---

### 🧮 Định Lý Giá Trị PoArt (The Value Theorem)

Giao thức [PoArt] liên kết giá trị ($V$) của tài sản số không phải với nhận thức thị trường chủ quan mà với **thực tế vật lý của quy trình sản xuất**.

Trí tuệ nhân tạo (AI) phá hủy quy trình bằng cách cung cấp kết quả tức thì ($t \to 0$). [PoArt] xem xét giá trị như sự tích lũy của các thành phần **thời gian, lao động và ý chí**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Định Nghĩa Biến Số

- **$\int dt$ (Tích Lũy Quy Trình):**  
  Giá trị không phải là "đầu ra" tức thì; nó là một **quy trình** tích lũy giữa $t_{\text{start}}$ và $t_{\text{end}}$. Khi thời gian giảm (sản xuất AI), kết quả của tích phân tiến gần 0.

- **$P_{\text{labor}}(t)$ (Cường Độ Lao Động Tức Thì):**  
  Đại diện cho cường độ nỗ lực tinh thần và thể chất được chi tiêu tại thời điểm sản xuất. Khi nỗ lực có thể chứng minh tăng, tích phân tăng.  
  > Ghi chú: Thuật ngữ này có thể được chuẩn hóa thực tế thông qua "tín hiệu lao động có thể đo lường/chứng minh".

- **$I_{\text{agency}}(t)$ (Hệ Số Ý Chí):**  
  Năng lực chấp nhận rủi ro và ra quyết định của người sản xuất. Nhận giá trị giữa $0$ và $1$.
  - **AI ($I \approx 0$):** Thực hiện lệnh, không chấp nhận rủi ro, không trả giá.
  - **Con Người ($I \to 1$):** Thay đổi quyết định, do dự, chấp nhận rủi ro.

- **$U_{\text{irreversible}}$ (Tính Đặc Thù Không Thể Đảo Ngược):**  
  Trong sản xuất số, hoàn tác (`Ctrl+Z`) là có thể; nhưng trong sản xuất vật lý (sơn trên canvas, đá cẩm thạch được đẽo, cử chỉ trong phát sóng trực tiếp), không có sự quay lại. **Tính không thể đảo ngược** này là một thuật ngữ bổ sung tạo ra "tính đặc thù" (đặc tính không thể thay thế) trong tác phẩm.

### 🔎 Phân Tích Trường Hợp: AI "Đầu Ra Tức Thì" vs. "Quy Trình Có Chứng Minh" của Con Người

Kịch bản sau đây cho thấy **Định Lý Giá Trị PoArt** hoạt động như thế nào trong thực tế và tại sao các sản phẩm AI đạt điểm thấp theo tiêu chuẩn [PoArt].

#### Kịch Bản A: Sản Xuất Hình Ảnh AI trong 10 Giây

- **Thời Gian ($\Delta t$):** $10$ giây (gần như không có quy trình)
- **Cường Độ Lao Động ($P_{\text{labor}}$):** $1$ đơn vị (chỉ viết lệnh)
- **Hệ Số Ý Chí ($I_{\text{agency}}$):** $0.01$ (không rủi ro, không trả giá)
- **Tính Không Thể Đảo Ngược ($U_{\text{irreversible}}$):** $0$ (có thể hoàn tác / sao chép)

**Kết Quả:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Nhận Xét:** Ngay cả khi đầu ra hoàn hảo; vì quy trình không được trải nghiệm và không chứa ý chí/rủi ro, giá trị [PoArt] tiến gần $0$.

#### Kịch Bản B: Sản Xuất Vật Lý 6 Giờ Trên Livestream

- **Thời Gian ($\Delta t$):** $6$ giờ ($21{,}600$ giây)
- **Cường Độ Lao Động ($P_{\text{labor}}$):** $0.5$ đơn vị (tính liên tục của nỗ lực thể chất và tinh thần)
- **Hệ Số Ý Chí ($I_{\text{agency}}$):** $0.9$ (thay đổi quyết định, chấp nhận rủi ro, lựa chọn không thể đảo ngược)
- **Tính Không Thể Đảo Ngược ($U_{\text{irreversible}}$):** $>0$ (dấu vết vật lý không thể hoàn tác)

**Kết Quả:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Nhận Xét:** Khi quy trình kéo dài và ý chí (rủi ro) tăng, giá trị tăng tích lũy. Thuật ngữ $U_{\text{irreversible}}$ là đóng góp bổ sung tạo ra "tính đặc thù" (đặc tính không thể thay thế) trong tác phẩm.

---

### ✅ Kết Luận: Khóa Giá Trị Bằng Chứng Minh (Proof-Bound Value)

Định lý này chuyển tuyên bố giá trị của [PoArt] từ "thích" hoặc "câu chuyện thị trường" thành **thực tế sản xuất có thể chứng minh**.

1. **Không Có Quy Trình, Không Có Giá Trị:**  
   AI phá hủy quy trình với đầu ra tức thì ($t \to 0$). Khi cửa sổ quy trình thu hẹp, kết quả của tích phân giảm như một sự cần thiết toán học:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Ý Chí và Rủi Ro Là Hệ Số Nhân:**  
   [PoArt] đo không chỉ "thời gian đã chi tiêu" mà còn tầng quyết định, rủi ro và chi phí thực sự trong thời gian đó. Giá trị của sản xuất không chấp nhận rủi ro (AI) là thấp:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Tính Đặc Thù Là Bằng Chứng Vật Lý, Không Phải Marketing:**  
   Trong sản xuất vật lý, dấu vết không thể đảo ngược (nét canvas, vết nứt đá cẩm thạch) nằm ngoài logic `Ctrl+Z` của kỹ thuật số. Tính không thể đảo ngược này ($U_{\text{irreversible}}$) làm cho tác phẩm trở nên độc nhất về mặt bản thể học.

> **🔐 TÓM TẮT:** Mặc dù định lý giá trị có vẻ không chắc chắn như một phép đo (ngay cả khi nó không thể đo 100% trong cuộc sống thực), mục đích của công thức này là chỉ ra cấu trúc và hướng của các biến số. Những gì hiếm trong kỷ nguyên AI không phải là "hình ảnh" mà là **lao động, thời gian và ý chí có thể chứng minh**. [PoArt] đo sự khan hiếm này và ghi nhận nó với **Evidence Pack**.

### 🏛️ Tầm Quan Trọng của Khái Niệm "Engine" (Động Cơ)

Các token ra mắt từ Pump.fun hoặc các nền tảng tương tự thường chỉ là **"vé vào cửa"**. **PoArt Forensic Engine (PFE)** là **tầng logic hiến pháp** xác định những quyền mà vé đó bảo vệ, cách lao động sẽ được ghi lại, và cách nghệ thuật/khoa học/công nghệ sẽ được bảo tồn.

> **Ghi chú:** Lý do chúng tôi bắt đầu dự án này trên Pump.fun là vì chúng tôi không có đủ thanh khoản và số lượng người theo dõi. Sử dụng dữ liệu hiện có có thể không phải là chiến lược chất lượng nhất nhưng là động thái đúng đắn nhất. Bất kể ngân sách và nguồn lực, việc xác định logic của động cơ này trên GitHub chứng minh rằng dự án không chỉ là đầu cơ tài chính mà còn là **cơ sở hạ tầng phần mềm** dài hạn và tầm nhìn **thư viện số quốc gia**.

---

## 🎨 GIAO THỨC [PoArt] BẰNG CHỨNG LAO ĐỘNG (Proof of Art Protocol v1.0)

> **"Nghệ Sĩ Thật, Sản Xuất Thật, Giá Trị Thật."**

Giao thức này là **cơ chế phòng thủ sinh học và trí tuệ** được phát triển chống lại những kẻ lừa đảo ẩn danh tràn ngập hệ sinh thái tiền điện tử, hình ảnh AI được sản xuất trong 5 phút, và văn hóa "Pump & Dump" (Bơm và Đổ).

---

## a) [PoArt] Là Gì? (Định Nghĩa Triết Học và Kỹ Thuật)

**Proof of Art [PoArt];** là tiêu chuẩn xác minh thể chế đảm bảo rằng giá trị đằng sau tài sản trên blockchain được đảm bảo không phải bằng đầu cơ mà bằng **lao động con người** có thể xác minh, **thời gian** và **năng lượng vật lý**.

Cũng như Bitcoin tạo ra giá trị thông qua *"Điện và Sức Mạnh Xử Lý"* **(Proof of Work)**; các dự án tuân thủ [PoArt] tạo ra giá trị thông qua *"Tài Năng và Thời Gian Con Người Đã Chi Tiêu"*. Nó "Stake" Thời Gian.

Nó loại bỏ rủi ro *"Nhà phát triển (Dev) bán, dự án kết thúc"* trên Pump.fun và các nền tảng DEX; vì ở đây giá trị không nằm trong mã mà trong **tính liên tục của sản xuất**.

> **[PoArt] không nói với người tham gia "Hãy tin chúng tôi"; nó nói "Đây là bằng chứng, hãy nhìn bằng mắt của bạn, xác minh bằng toán học của bạn."**

---

## b) Tiêu Chuẩn 5 Trụ Cột [PoArt] (The 5 Pillars of Truth)

5 điều khoản này là các bộ lọc không thể thao túng mà một dự án phải vượt qua để nhận con dấu [PoArt].

### 1) Bằng Chứng Danh Tính Trực Tiếp (Live Identity Proof)

- **Vấn Đề:** Thế giới tiền điện tử đầy những người sáng lập ẩn danh (Dev) thu tiền và bỏ rơi dự án.
- **Giải Pháp [PoArt]:** Người sản xuất chứng minh không chỉ giấy tờ tùy thân mà còn **sự hiện diện tại thời điểm sản xuất**. Điều này bao gồm các phiên livestream nơi họ tương tác với cộng đồng và thực hiện các yêu cầu cụ thể tức thì, không phải video được ghi trước.  
  (Ví dụ: *"Viết ngày hôm nay và số block hiện tại ở góc phải của canvas"*)
- **Phương Châm:** *"Bot có thể vẽ tranh nhưng bot không thể đổ mồ hôi và ứng biến."*

### 2) Bằng Chứng Lao Động và Quy Trình (Labor & Process Proof)

- **Vấn Đề:** Hình ảnh AI được sản xuất trong 2 giây và tranh sơn dầu mất 2 tháng nhận cùng đối xử "jpeg" trong thế giới số.
- **Giải Pháp [PoArt]:** "Quá trình mang thai và sinh nở" của tác phẩm được ghi lại. Các giai đoạn phác thảo, lớp sơn, số giờ tích lũy đã chi tiêu và quy trình vật lý mà nghệ sĩ trải qua khi tạo tác phẩm được ghi nhận. Điều này thêm **"Chi Phí Thời Gian" (Time Cost)** vào token. Càng khó sản xuất tài sản, giá trị càng vững chắc.

### 3) Bằng Chứng Giá Trị Thẩm Mỹ (Aesthetic Value Proof)

- **Vấn Đề:** Văn hóa "Meme" bỏ qua thẩm mỹ và chiều sâu nghệ thuật, chỉ tập trung vào hài hước tức thì, dẫn đến các dự án "Hype" ngắn ngủi.
- **Giải Pháp [PoArt]:** Dự án phải có tiêu chuẩn nghệ thuật học thuật, lý thuyết màu sắc, quy tắc bố cục và kiến thức vật liệu (Impasto, Kết cấu, v.v.). Nội dung không chỉ làm cười; nó phải khơi dậy sự ngưỡng mộ ở người xem và mang **giá trị bộ sưu tập**.

### 4) Đổi Mới Ý Tưởng (Conceptual Novelty)

- **Vấn Đề:** Hàng nghìn coin chó/mèo sao chép lẫn nhau, thiếu sáng tạo.
- **Giải Pháp [PoArt]:** Dự án phải xây dựng cầu nối mới kết hợp nghệ thuật, khoa học, triết học hoặc công nghệ theo cách có ý nghĩa.  
  (Ví dụ: Kết hợp bức tượng David cổ điển với dữ liệu thị trường tiền điện tử; xử lý ý tưởng về nhận thức con người "hóa đá" và có thể chứng minh điều này bằng các nguồn khoa học.)  
  Tác phẩm phải không chỉ là tiệc thị giác; nó cũng phải là thách thức trí tuệ khiến người ta suy nghĩ về **Khoa Học, Triết Học hoặc Công Nghệ**.

> [!IMPORTANT]
> **Ví Dụ Tham Khảo (Hiệu Ứng Las Palmitas):**  
> Ở khu phố Las Palmitas của Mexico đang chiến đấu với tội phạm, hơn 200 ngôi nhà đã được chuyển đổi thành bữa tiệc cầu vồng khổng lồ. Sau sự can thiệp thẩm mỹ này, tỷ lệ tội phạm trong khu phố giảm ở mức độ nhất định, thanh niên bắt đầu quan tâm đến nghệ thuật thay vì băng đảng. Sự thay đổi thẩm mỹ đã lập trình lại sự tôn trọng của mọi người đối với môi trường và nhau (Gắn Kết Xã Hội).
>
> **Kỳ Vọng:** Một dự án muốn vào danh sách [PoArt] phải chứa mối quan hệ nhân quả xã hội học, khoa học hoặc triết học vượt ra ngoài thẩm mỹ thị giác thuần túy, giống như ví dụ trên. Vì "Thời gian" là tài sản duy nhất không thể mua bằng tiền, trong giao thức này, thời gian phải được stake như tài sản thế chấp và chứng minh. Nền tảng ý tưởng của dự án phải mạnh mẽ và phổ quát đến mức, ngay cả trong kịch bản CTO (Community Take Over) có thể xảy ra sau nhiều năm, cộng đồng có thể thừa hưởng di sản này và tiếp tục tiềm năng đổi mới của dự án một cách tự chủ.

### 5) Ý Chí Phi Thuật Toán (Non-Algorithmic Agency)

- **Vấn Đề:** Sản phẩm số hoàn hảo nhưng vô hồn, lặp lại.
- **Giải Pháp [PoArt]:** Ý chí độc đáo của con người có thể mắc lỗi, chấp nhận rủi ro và trải qua dao động cảm xúc phải được cảm nhận trong tác phẩm. Sự không chắc chắn trong nét cọ, phản ứng bất ngờ của vật liệu và quyết định tức thì của nghệ sĩ là **Chữ Ký Sinh Học** phân biệt tác phẩm với "Sản Phẩm Máy".

---

## c) Cơ Chế Xác Minh & Chống Giả Mạo

Hệ thống này đảm bảo dự án vẫn đáng tin cậy và sống động không chỉ "lúc đầu" mà "mãi mãi".

### 📦 Gói Bằng Chứng (Evidence Pack - The Digital Twin)

Đằng sau mỗi tác phẩm được chứng nhận [PoArt] có một gói dữ liệu được mã hóa và đóng dấu thời gian mà nhà đầu tư có thể tải xuống:

- **Bản Ghi Video RAW:** Cảnh quay thô không gián đoạn của thời điểm sản xuất.
- **Phân Tích Metadata:** Ngày tạo tệp, thông tin thiết bị sử dụng và dữ liệu vị trí (Thành Phố-Quốc Gia).
- **Tham Chiếu Vật Lý:** Bằng chứng rằng tác phẩm tồn tại trong thế giới vật lý  
  (Ví dụ: Báo hiện tại đặt cạnh tác phẩm hoặc dữ liệu blockchain tại thời điểm đó).

> *Ghi chú nhất quán:* Thuật ngữ "gói bằng chứng" liên kết với chuỗi **Evidence Pack → EvidenceRoot → NotarySeal** trong các phần trước; tức là tính toàn vẹn của gói được đại diện bằng con dấu có thể xác minh.

### 🔄 Gia Hạn 365 Ngày (The Sustainability Protocol)

- **Tính Năng Cách Mạng:** Trong các dự án tiền điện tử, "Dev" (Nhà Phát Triển) đưa token ra thị trường và thường biến mất sau 1-2 tháng (Soft Rug). [PoArt] làm điều này không thể.
- **Quy Tắc:** Trạng thái "Verified Artist" (Nghệ Sĩ Đã Xác Minh) không phải vĩnh viễn. Nó chỉ có hiệu lực **1 năm**.
- **Hoạt Động:** Nghệ sĩ/Nhà phát triển phải trình bày cho cộng đồng một **tác phẩm mới, lớn và có thể chứng minh** mỗi 365 ngày.
- **Kịch Bản Ví Dụ:** Bạn bắt đầu dự án vào năm 2026. Vào tháng 1 năm 2027, hệ thống đưa ra cảnh báo "Thời Hạn Bằng Chứng Đã Hết". Nếu nghệ sĩ không trình bày triển lãm mới, tác phẩm vật lý mới hoặc tích hợp công nghệ mới, "Huy Hiệu Tin Cậy" của dự án sẽ giảm.
- **Kết Quả:** Hệ thống này đảm bảo **nội dung không bao giờ lỗi thời** và nhà đầu tư không trải qua nỗi sợ *"Nhà phát triển còn ở đây không?"*. Dự án trở thành một studio sống.

### 🚩 Giao Thức Cờ Đỏ (Red Flag Protocol)

**Nếu bất kỳ giả mạo nào (sử dụng AI, tác phẩm bị đánh cắp, video bị thao túng) được phát hiện bởi cộng đồng hoặc thuật toán:**

1. Chứng chỉ ngay lập tức được đánh dấu là **"HỦY BỎ" (VOID)**.
2. Gói bằng chứng được gắn nhãn công khai là **"Giả"**.
3. Dự án được đưa vào danh sách đen [PoArt]. Điều này củng cố thực tế rằng trong thế giới phi tập trung, **danh tiếng là đơn vị tiền tệ duy nhất**.
4. Không thể bao gồm các tuyên bố [PoArt] trong bất kỳ ấn phẩm nào; nguồn hợp lệ duy nhất là https://www.ilhanart.org/public-registry

---

## d) Kết Luận: Không Phải Sòng Bạc, Mà Là Bảo Tàng

**Pump.fun và Sàn Giao Dịch Phi Tập Trung (DEX) hiện tại không may là sòng bạc; đèn nhấp nháy, mọi người theo đuổi lợi nhuận nhanh và nhà cái (kẻ lừa đảo) luôn thắng. Lý do chúng tôi bắt đầu dự án ở đây cũng là để cố gắng cải thiện nơi này, và vì chúng tôi có dữ liệu hiện có và môi trường để tiếp cận đối tượng hiện tại thông qua livestream.**

**[PoArt] là pháo đài được xây dựng giữa sòng bạc này.**

- 🎰 Sòng bạc dựa vào trò chơi giấy; chúng tôi dựa vào **thực tế vật lý**.
- 🃏 Sòng bạc mở cho gian lận; chúng tôi mở cho **bằng chứng minh bạch**.
- ⏳ Sòng bạc là tạm thời; chúng tôi tập trung vào **sự vĩnh cửu của nghệ thuật và khoa học**.

**Token sử dụng giao thức này không chỉ là "coin"; nó là cổ phiếu số chứa mồ hôi, sơn, mã và triết học đằng sau.**

---

## 🗳️ 6) QUẢN TRỊ VÀ ĐĂNG KÝ CÔNG CỘNG (Governance & Public Registry)

**Mục đích của phần này: Chuyển tiêu chuẩn [PoArt] từ mặt phẳng "tin tưởng cá nhân" sang cơ sở hạ tầng công cộng bền vững với đăng ký + xác minh + giám sát cộng đồng.**

### 6.1 Public Registry (Đăng Ký Công Cộng)

- **Public Registry:** Tất cả dữ liệu được phê duyệt được ghi lại tại `ilhanart.org/registry` (hoặc GitHub Registry).

**Logic đăng ký (tiêu chuẩn được đề xuất - định dạng đường dẫn JSON):**

Mỗi bản ghi nhập vào đăng ký mang các trường cốt lõi có thể xác minh tối thiểu sau:

- **Danh Tính & Trạng Thái:**
  - `certificate_id` (tham chiếu có thể đọc)
  - `status` (active / void)
  - `void_reason` (nếu có)
  - `visibility` (private / masked / public)
  - `created_at` (dấu thời gian)

- **Tổ Chức Phát Hành:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Thông Tin Tác Phẩm:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (nếu có thể; cho danh tính chủ sở hữu token)
  - `asset.fingerprints.sha256`
  - `asset.fingerprints.sha512`

- **Dữ Liệu Pháp Y:**
  - `forensics.ip_masked`
  - `forensics.location`
  - `forensics.device`
  - `forensics.timestamp`

- **Bằng Chứng Mật Mã:**
  - `proof.evidence_root`
  - `proof.signer_sig`
  - `proof.notary_seal`

- **Quản Trị:**
  - `governance.decision`
  - `governance.review_notes`

Đăng ký có thể có hai tầng:
- **1)** Chỉ mục dành cho người đọc (liệt kê web / tìm kiếm / bộ lọc)
- **2)** Manifest dành cho máy đọc (bản ghi JSON; để xác minh PFE)

**"Bản ghi" ở đây có thể xác minh được với chuỗi Evidence Pack → EvidenceRoot → NotarySeal của PFE. Đăng ký cung cấp mục tiêu xác minh, không phải "tuyên bố".**

---

### 6.2 Quy Trình Đăng Ký PoArt Verified

**Đơn đăng ký PoArt Verified được đánh giá bởi İlhanArt Gallery theo 5 tiêu chuẩn PoArt. Phản hồi cộng đồng được xem xét, nhưng quyết định cuối cùng thuộc về đội ngũ giám tuyển. Các quyết định được công bố minh bạch và ghi lại tại ilhanart.org/registry.**

#### Quy Trình Đăng Ký

**Đăng Ký:**
- Nghệ sĩ/dự án gửi đơn đăng ký PoArt Verified
- Evidence Pack được chuẩn bị (bản ghi video, metadata, liên kết livestream)
- Đơn đăng ký được gửi đến İlhanArt Gallery

**Xem Xét (30 Ngày):**
- Đội ngũ gallery xem xét Evidence Pack chi tiết
- Tất cả 5 tiêu chuẩn PoArt được kiểm tra:
  1. Live Identity Proof
  2. Labor & Process Proof
  3. Aesthetic Value Proof
  4. Conceptual Novelty
  5. Non-Algorithmic Agency
- Phỏng vấn với nghệ sĩ (tùy chọn)

**Tham Vấn Cộng Đồng:**
- Evidence Pack được chia sẻ công khai trong quá trình đăng ký
- Cộng đồng có thể cung cấp phản hồi qua ilhanart.org
- Chủ sở hữu token (tối thiểu 10,000 $CULTURE) đặc biệt có thể đưa ra đề xuất
- **Tất cả phản hồi được xem xét trong quá trình xem xét**
- **Tuy nhiên, quyết định cuối cùng thuộc về đánh giá giám tuyển**

**Quyết Định:**
- Gallery phê duyệt hoặc từ chối đơn đăng ký
- Lý do quyết định được công bố minh bạch
- Nếu được phê duyệt → Huy hiệu PoArt Verified
- Nếu bị từ chối → Có thể đăng ký lại sau 6 tháng

**Minh Bạch:**
- Tất cả đơn đăng ký và quyết định được ghi lại tại ilhanart.org/registry
- Bản ghi quyết định được công bố công khai:
  - Ngày đăng ký
  - Tóm tắt quá trình xem xét
  - Quyết định (Approved / Rejected)
  - Lý do quyết định (giải thích ngắn gọn)
  - Tóm tắt phản hồi cộng đồng (ẩn danh)

#### Tại Sao Quyết Định Giám Tuyển?

**Kiểm Soát Chất Lượng:**  
Trạng thái PoArt Verified là huy hiệu có tiêu chuẩn cao. Đánh giá giám tuyển đảm bảo các tiêu chuẩn này được duy trì.

**Ngăn Chặn Thao Túng Đầu Cơ:**  
Quản trị on-chain đầy đủ (ví dụ: Realms, DAO voting) không khả thi về mặt kỹ thuật với token Pump.fun. Các hệ thống bỏ phiếu off-chain dễ bị thao túng bởi cá voi và tấn công phối hợp. Quyết định giám tuyển loại bỏ rủi ro này.

**Hiệu Quả Vận Hành:**  
Quy trình quyết định nhanh chóng và rõ ràng thay vì các cơ chế bỏ phiếu phức tạp. Nghệ sĩ nhận kết quả trong vòng 30 ngày.

**Tham Gia Cộng Đồng:**  
Phản hồi cộng đồng được xem xét đầy đủ và ảnh hưởng đến quá trình quyết định. Tuy nhiên, quyết định cuối cùng thuộc về đội ngũ giám tuyển được bảo vệ khỏi thao túng.

**Tương Lai:**  
Khi dự án trưởng thành (2027+), cơ chế tham vấn cộng đồng có thể được tăng cường. Tuy nhiên, bảo vệ tiêu chuẩn giám tuyển là vĩnh viễn.

---

### 6.3 Token Utility (Tiện Ích Token)

**Lợi ích được cung cấp cho chủ sở hữu token $CULTURE:**

**1. Quyền Truy Cập Ưu Tiên Sự Kiện Gallery:**
- Quyền triển lãm 1 tuần mỗi năm tại İlhanArt Gallery (quyền có thể chuyển nhượng)
- Giảm giá drop painting
- Giảm giá từ 10% đến 30% cho tranh tại gallery

**2. Truy Cập Đầy Đủ PoArt Registry:**
- Bản ghi chi tiết của tất cả tác phẩm đã xác thực
- Phiên bản đầy đủ của Evidence Pack
- Công cụ xác minh pháp y


**3. Advisory Voting:**
- Quyền tư vấn trong đơn đăng ký PoArt Verified
- Truy cập kênh phản hồi cộng đồng
- Tham gia thảo luận quản trị

**4. Nội Dung Độc Quyền:**
- Nội dung hậu trường studio
- Phỏng vấn nghệ sĩ và video quy trình
- Truy cập tài liệu kỹ thuật

**Ghi Chú:**  
Chủ sở hữu token đưa ra advisory vote (phiếu tư vấn). Quyết định cuối cùng thuộc về đội ngũ giám tuyển. Cấu trúc này được chọn để ngăn chặn thao túng cá voi và tấn công đầu cơ. Không có staking reward vì chúng tôi tìm kiếm người tham gia văn hóa dài hạn, không phải vốn lính đánh thuê ngắn hạn.

---

### 6.4 Metadata Sync (Đồng Bộ Với Thế Giới Vật Lý)

- **Metadata Sync:** Dữ liệu kỹ thuật trong đăng ký phải khớp 100% với tài sản vật lý.

**Định nghĩa kỹ thuật "khớp 100%" (độ rõ ràng được đề xuất):**

- **Khớp tối thiểu (bắt buộc):**
  - `asset.fingerprints.sha256/sha512` trong đăng ký phải **giống hệt** hash của tệp trong tay.
  - `proof.notary_seal` trong đăng ký khi được tạo lại (nếu có Evidence Pack) phải **giống hệt**.

- **Khớp tham chiếu vật lý (loại bằng chứng):**
  - Bằng chứng như tác phẩm vật lý được hiển thị trong livestream + tham chiếu ngày/block phải nhất quán với Evidence Pack.

- **Tuân thủ quyền riêng tư:**
  - Các trường như IP/vị trí trong khả năng hiển thị `masked` được công bố **theo tiêu chuẩn che giấu**.

---

### 6.5 Khiếu Nại, Xem Xét và Thu Hồi (Dispute & Revocation)

Đăng ký không chỉ là cơ chế "phê duyệt"; nó là **cơ chế giám sát sống chống lại giả mạo**.

- Khi khiếu nại được bắt đầu, bản ghi có thể được đặt vào chế độ **"review"**.
- Nếu phát hiện giả mạo, nó được đánh dấu là `status: void` và lý do được thêm vào:
  - `void_reason` (sử dụng AI / bị đánh cắp / thao túng, v.v.)
  - `revoked_at` (thời gian thu hồi)
- Nguồn của quyết định thu hồi được hiển thị rõ ràng trong đăng ký:
  - xem xét giám tuyển / khiếu nại cộng đồng / ghi chú phân tích pháp y (tùy theo áp dụng)

> **Phần này là đối ứng của khái niệm VOID trong phần "Red Flag Protocol" trên đăng ký.**

---

### 6.6 Ví Dụ Bản Ghi Đăng Ký (Dành cho Máy Đọc)
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

> *Ghi chú: `asset.fingerprints.sha512` và các giá trị hash khác được rút ngắn cho mục đích trình bày; trong triển khai thực tế, chuỗi ký tự hexadecimal độ dài đầy đủ được sử dụng.*

---

## 7) 🔐 CON DẤU KỸ THUẬT (NOTARY SEAL)

**Thuật toán con dấu không thể lay chuyển được tạo bởi PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Giao Thức [PoArt] Công Chứng Số & Bằng Chứng Pháp Y (Beta v1.0)

> **"Văn hóa lớn hơn vốn. Bảo vệ tác phẩm của bạn từ hôm nay, mang đến ngày mai."**

---

## Tại Sao Công Khai?

Bảo mật thực sự đến từ sự minh bạch. Với hệ thống **Public Registry (Đăng Ký Công Khai)** của chúng tôi, bất kỳ ai ở bất kỳ đâu trên thế giới có thể xác minh trong vài giây liệu tệp trong tay họ có phải là bản gốc hay không, mà không cần bất kỳ cơ quan nào.

---

## 🧩 Tại Sao Có Nhiều "Mô-đun Khả Năng Hiển Thị"?

Đây là phần quan trọng nhất của mã (menu chọn visibility). Các tùy chọn này cho phép người dùng cân bằng **"Quyền Riêng Tư vs. Minh Bạch"**:

### 🔒 Riêng Tư (Private)

- **Kịch Bản:** Nghệ sĩ chưa muốn công bố tác phẩm nhưng muốn đóng dấu thời gian để chứng minh "tôi đã làm cái này vào ngày này".
- **Mã Làm Gì:** Ghi dữ liệu vào cơ sở dữ liệu nhưng gán nhãn `visibility: "private"`. Sau này khi viết chính sách "Public Read", bạn có thể ẩn các bản ghi này khỏi công chúng bằng cách sử dụng `WHERE visibility = 'public'`.

### 🕶️ Che Giấu (Masked)

- **Kịch Bản:** Nghệ sĩ muốn minh bạch nhưng lo ngại về việc tìm thấy địa chỉ nhà (vị trí IP).
- **Mã Làm Gì:** Các hàm `maskIP` và `maskLoc` chạy ở phía JavaScript. Chuyển đổi địa chỉ IP thành dạng `88.241.***.***`, vị trí thành dạng `***/TR` và gửi phiên bản đã kiểm duyệt đến cơ sở dữ liệu.
- **Ghi Chú Quyền Riêng Tư:** Việc che giấu được thực hiện trong trình duyệt, Supabase không thấy vị trí thực. **Tuy nhiên:** Nếu API bên thứ ba như ipapi.co được sử dụng cho dữ liệu vị trí, các nhà cung cấp này thấy địa chỉ IP tại thời điểm yêu cầu.
- **Niêm Phong Ở Chế Độ Masked:** Tính toán EvidenceRoot và NotarySeal được thực hiện với dữ liệu forensics đã che giấu; do đó xác minh vẫn xác định.

### 🌍 Công Khai (Public)

- **Kịch Bản:** Minh bạch hoàn toàn. Theo tiêu chuẩn [PoArt], nơi, thời gian và mạng nào tác phẩm được sản xuất được công bố rõ ràng.

---

## 💡 Đổi Mới Công Nghệ

PoArt không chỉ là hệ thống tải tệp. Nó là một động cơ **"Chuỗi Bảo Quản Bằng Chứng Pháp Y" (Forensic Chain of Custody)** mang đến tiêu chuẩn mới bằng cách kết hợp ba lớp công nghệ khác nhau trong một nồi nấu chảy.

**Lớp được mô tả là "động cơ" trong phần này tương ứng với lõi PoArt Forensic Engine (PFE) từ thuật ngữ trước đó.**

### 1) Client-Side Hashing (Quyền Riêng Tư Tối Đa)

Tệp tác phẩm của bạn không bao giờ được tải lên máy chủ. Động cơ dựa trên trình duyệt (Client-side) của chúng tôi tính toán hash (tóm tắt số) của tệp trên máy tính của bạn. Chỉ dấu vân tay này và metadata được gửi đến máy chủ.

> **Ghi Chú Quyền Riêng Tư:** Tệp tác phẩm không được tải lên máy chủ và được bảo vệ theo cách này. Tuy nhiên, dữ liệu forensics (IP/vị trí) được chia sẻ theo chế độ khả năng hiển thị đã chọn (private/masked/public).

### 2) Forensic Data Fusion (Sức Mạnh Pháp Y)

Nó nhiều hơn một dấu thời gian (Timestamp) thông thường. Hệ thống kết hợp các dữ liệu sau trong một "Genesis Seal" duy nhất:

- **Tóm Tắt Số (SHA-512):** Dấu vân tay số sẽ bị hỏng nếu ngay cả một pixel của tác phẩm thay đổi, sử dụng tiêu chuẩn tóm tắt mật mã (SHA-512).
- **Vị Trí & Thời Gian:** Ngày với độ chính xác mili giây khi giao dịch được thực hiện, dữ liệu quốc gia, thành phố và quận.
- **Danh Tính Thiết Bị:** Hệ điều hành, trình duyệt và loại thiết bị (phân tích User-Agent).

---

## 🛡️ Trường Hợp Sử Dụng và Lợi Ích

Nếu bạn là nghệ sĩ, nhà văn hoặc nhà thiết kế, nói "Tôi đã làm cái này trước" là không đủ, bạn cần chứng minh.

**Một tác phẩm được niêm phong với PoArt:**

- **Bằng Chứng Toán Học:** Hệ thống phát hiện nếu ngay cả một pixel của tệp bị thay đổi. Thao túng là không thể.
- **Cơ Sở Pháp Lý:** Tác phẩm được niêm phong vào ngày nào, ở thành phố nào, từ thiết bị nào được ghi lại.
- **Chứng Chỉ Tức Thì:** Tạo **"Chứng Chỉ Danh Tính Tài Sản"** với mã QR và con dấu duy nhất cho bạn trong vài giây.

---

## ⚙️ Kiến Trúc Hệ Thống và Thông Số Kỹ Thuật

Hệ thống được thiết kế trên kiến trúc "Serverless" (Không Máy Chủ), tập trung vào hiệu suất cao và khả năng mở rộng.

| Lớp | Công Nghệ | Mô Tả |
|-----|-----------|-------|
| **Mật Mã** | SHA-256 & SHA-512 | Tóm tắt mật mã hai lớp |
| **Cơ Sở Dữ Liệu** | Supabase (PostgreSQL) | Cấu trúc dữ liệu JSONB, chính sách RLS |
| **Dữ Liệu Pháp Y** | ipapi.co API | Bộ ba IP/Vị Trí/Thời Gian |
| **Rendering** | html2canvas + jsPDF | Sản xuất PNG/PDF phía client |
| **Frontend** | Vanilla JavaScript | Không phụ thuộc framework |
| **Bảo Mật** | Client-side hashing | Tệp không bao giờ được tải lên máy chủ |

### Các Tính Năng Nổi Bật

| Tính Năng | Chi Tiết | Ở Đối Thủ? |
|-----------|----------|------------|
| **Drag & Drop UI** | Kéo thả tệp, xem trước tức thì | ❌ Hầu hết không có |
| **Multi-Format Export** | PNG, JSON, PDF - một cú nhấp | ⚠️ Hạn chế |
| **Real-Time Preview** | Xem trước chứng chỉ trực tiếp | ❌ Không |
| **Privacy Controls** | Tùy chọn Private/Masked/Public | ❌ Không |
| **Client-Side Hashing** | Tệp không bao giờ đến máy chủ | ✅ Chỉ vài cái |
| **Forensic Metadata** | IP, vị trí, thiết bị, thời gian - tất cả trong một | ❌ Rời rạc |
| **QR Verification** | Mã QR xác minh tức thì | ⚠️ Hạn chế |
| **Rate Limiting** | Bảo vệ spam (RLS + Client) | ❌ Hầu hết không có |

---

## 🗺️ Lộ Trình: Tương Lai "Trustless"

Phiên bản hiện tại **(Beta v1.0)** được tối ưu hóa để cung cấp tốc độ tối đa, giao diện dễ sử dụng và truy cập miễn phí cho người dùng cuối. Tuy nhiên, tầm nhìn cuối cùng của chúng tôi là chuyển sang cấu trúc mà ngay cả quản trị viên cơ sở dữ liệu (chúng tôi) cũng không thể can thiệp.

### Giai Đoạn 1: Beta v1.0 (Hiện Đang Hoạt Động)

**Cơ Sở Hạ Tầng:**
- Cloud Database (Supabase)
- Off-chain registry (PostgreSQL + IPFS backup)
- Gallery self-attestation (tập trung nhưng minh bạch)

**Token:**
- Platform: Pump.fun
- Liquidity: Raydium (tự động)
- Governance: Advisory only (tư vấn cộng đồng)

**Mục Tiêu:**
- Tốc độ, loại bỏ rào cản UX
- Cung cấp bảo mật "không ma sát"
- Xây dựng cộng đồng

**Token Utility (v1.0):**
- Quyền truy cập ưu tiên sự kiện gallery
- Xem PoArt Registry
- Quyền advisory voting

---

### 🚀 Giai Đoạn 2: Decentralized Authority (Q2-Q4 2026)

Giai đoạn này bao gồm việc chuyển đổi từ cấu trúc hoàn toàn "Client-Side" sang cấu trúc an toàn và phi tập trung hơn.

| Tính Năng | Lợi Ích? | Tech Stack | ETA |
|-----------|----------|------------|-----|
| **Edge Function INSERT** | Chặn spam + bảo mật API Key | Supabase Edge (Deno) | Q2 2026 |
| **Wallet Signature** | Danh tính phi tập trung | Solana Wallet Adapter | Q2 2026 |
| **IPFS/Arweave Backup** | Lưu trữ phi tập trung | IPFS SDK + Pinata | Q3 2026 |
| **Revocation Mechanism** | Hủy bỏ chứng chỉ giả | DB Schema Update | Q2 2026 |
| **Audit Log** | Ghi chép truy vấn pháp y | Custom logs table | Q3 2026 |
| **OpenTimestamps** | Bitcoin anchoring | OTS JavaScript | Q4 2026 |

**Token Governance (v2.0):**
- Off-chain voting (x/web) + wallet signature
- Bầu đại diện cộng đồng (90 ngày đầu)
- Multi-sig operations wallet control
- Weighted advisory voting (với whale cap)

**Immutability:**
- Registry backup với IPFS hash
- Bitcoin timestamp anchoring
- Chuẩn bị cross-chain verification

---

### Giai Đoạn 3: Phi Tập Trung Hoàn Toàn (2027+)

| Tính Năng | Mục Tiêu | ETA |
|-----------|----------|-----|
| **On-Chain Registry** | Ghi chép on-chain Solana | Q1 2027 |
| **Enhanced Token Utility** | NFT mint, tính năng nâng cao | Q1 2027 |
| **Multi-Chain Support** | Ethereum, Polygon, Base | Q2 2027 |
| **DID Integration** | Danh Tính Phi Tập Trung | Q3 2027 |
| **Community Governance** | Hệ thống tư vấn được tăng cường | Q4 2027 |
| **Legal Recognition** | Hiệu lực tại tòa án Thổ Nhĩ Kỳ | 2027-2028 |
| **API for Developers** | Public API endpoint | Q3 2027 |

**Governance Evolution:**
- v3.0: Mô hình hybrid (giám tuyển + community weighted)
- 2028+: Full community governance (tùy chọn)
- Kiểm soát chất lượng giám tuyển luôn được bảo tồn

---

## 🧬 Cấu Trúc Dữ Liệu Giao Thức (JSON Schema)

**Mỗi chứng chỉ [PoArt] có một thẻ danh tính JSON di động và có thể xác minh được tạo theo tiêu chuẩn sau.**

> **Ghi chú:** Định dạng Identity JSON này là định dạng chứng chỉ được trình bày cho người dùng. Trong các bản ghi registry, `registry.asset` được sử dụng thay vì `identity.asset_data` (mapping: `identity.asset_data` == `registry.asset`).
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

## 🔬 Chiều Sâu Kỹ Thuật: Thuật Toán Niêm Phong

### Hàm Hash Xác Định
```javascript
// Hàm Trợ Giúp: Chuyển Digest thành chuỗi hex
async function digestToHex(algorithm, dataBytes) {
  const hashBuffer = await crypto.subtle.digest(algorithm, dataBytes);
  const hashArray = Array.from(new Uint8Array(hashBuffer));
  return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
}

// Chuyển String thành byte array
function stringToBytes(text) {
  return new TextEncoder().encode(text);
}

// Sản xuất chuỗi forensics canonical (v1.0: thứ tự trường cố định + UTF-8 + delimiter \n)
// Ghi chú Giai đoạn 2: Sẽ chuyển sang canonical JSON với RFC 8785 (JCS)
function canonicalForensics(forensicsData) {
  return JSON.stringify({
    ip_masked: forensicsData.ip_masked,
    location: forensicsData.location,
    device: forensicsData.device,
    timestamp: forensicsData.timestamp
  });
}
```

### Quy Trình Sản Xuất NotarySeal (Hoàn Toàn Xác Định)
```javascript
// 1. Tính FileHash (client-side)
async function computeFileHash(file) {
  const fileBuffer = await file.arrayBuffer();
  const fileBytes = new Uint8Array(fileBuffer);
  
  const sha256 = await digestToHex('SHA-256', fileBytes);
  const sha512 = await digestToHex('SHA-512', fileBytes);
  
  return { sha256, sha512 };
}

// 2. Thu thập dữ liệu Forensic (sử dụng một timestamp)
async function collectForensics(visibilityMode) {
  const timestamp = new Date().toISOString(); // Sản xuất một timestamp
  const ipData = await fetch('https://ipapi.co/json/').then(r => r.json());
  
  let forensics = {
    ip_masked: visibilityMode === 'masked' ? maskIP(ipData.ip) : ipData.ip,
    location: visibilityMode === 'masked' 
      ? `***/${ipData.country}` 
      : `${ipData.city}, ${ipData.country_name || ipData.country}`,
    device: navigator.userAgent,
    timestamp: timestamp // Cùng timestamp
  };
  
  return { forensics, timestamp };
}

// 3. Tạo EvidenceRoot (với canonical encoding)
async function computeEvidenceRoot(fileHash512, forensicsData) {
  const canonicalPayload = `file_sha512:${fileHash512}\nforensics:${canonicalForensics(forensicsData)}`;
  return await digestToHex('SHA-512', stringToBytes(canonicalPayload));
}

// 4. Sản xuất NotarySeal (sử dụng cùng timestamp)
async function computeNotarySeal(evidenceRoot, signerSignature, timestamp) {
  const sealPayload = `evidence_root:${evidenceRoot}\nsigner_sig:${signerSignature}\ntimestamp:${timestamp}`;
  return await digestToHex('SHA-512', stringToBytes(sealPayload));
}

// Hàm trợ giúp che giấu (hỗ trợ IPv4 và IPv6)
function maskIP(ip) {
  if (!ip) return "***";
  
  // Kiểm tra IPv4
  if (ip.includes(".")) {
    const parts = ip.split(".");
    if (parts.length === 4) {
      return `${parts[0]}.${parts[1]}.***.***`;
    }
  }
  
  // IPv6 hoặc định dạng không xác định
  return "***";
}
```

### Luồng Xác Minh (Hai Cấp Độ)

#### Quick Verify (Xác Minh Nhanh)
```javascript
// Chỉ kiểm tra hash tệp (cờ đỏ nhanh)
async function verifyQuick(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);
  
  // Lấy từ Registry
  const cert = await fetchFromRegistry(certificateId);
  const { sha512: originalHash } = cert.asset.fingerprints;
  
  // So sánh Hash
  if (userFileHash === originalHash) {
    return {
      valid: true,
      message: "✅ Bản gốc - Hash tệp khớp"
    };
  } else {
    return {
      valid: false,
      message: "❌ Giả - Tệp đã bị thao túng"
    };
  }
}
```

#### Full Verify (Xác Minh Đầy Đủ)
```javascript
// Tạo lại EvidenceRoot và NotarySeal để xác minh
async function verifyFull(file, certificateId) {
  const { sha512: userFileHash } = await computeFileHash(file);

  // Lấy từ Registry
  const cert = await fetchFromRegistry(certificateId);

  // 1) Kiểm tra FileHash (cờ đỏ nhanh)
  const originalHash = cert.asset.fingerprints.sha512;
  if (userFileHash !== originalHash) {
    return { valid: false, message: "❌ Giả - Hash tệp không khớp" };
  }

  // 2) Tạo lại EvidenceRoot (với forensics được lưu trong registry)
  const evidenceRoot = await computeEvidenceRoot(userFileHash, cert.forensics);
  if (evidenceRoot !== cert.proof.evidence_root) {
    return { valid: false, message: "❌ Không khớp - EvidenceRoot không đúng" };
  }

  // 3) Tạo lại NotarySeal (với cùng timestamp + signer_sig)
  const seal = await computeNotarySeal(
    evidenceRoot,
    cert.proof.signer_sig,
    cert.forensics.timestamp
  );

  if (seal !== cert.proof.notary_seal) {
    return { valid: false, message: "❌ Không khớp - NotarySeal không đúng" };
  }

  // Tùy chọn: Trong Giai đoạn 2, cũng xác minh signer_sig với attestation_pubkey
  // const sigValid = await verifySig(cert.issuer.attestation_pubkey, cert.proof.signer_sig, evidenceRoot);
  // if (!sigValid) return { valid: false, message: "❌ Chữ ký không hợp lệ" };

  return { valid: true, message: "✅ Bản gốc - Full Verify đã qua" };
}
```

> **Ghi Chú Quan Trọng:**
> - **Quick Verify:** Chỉ kiểm tra hash tệp cho sử dụng nhanh.
> - **Full Verify:** Xác minh tất cả các lớp của giao thức (EvidenceRoot + NotarySeal).
> - Tất cả hoạt động hash được thực hiện xác định với encoding và delimiter cố định.
> - **Tiêu chuẩn canonicalization v1.0:** Thứ tự trường cố định + encoding UTF-8 + delimiter `\n`.
> - **Kế hoạch Giai đoạn 2:** Chuyển sang canonical JSON với RFC 8785 (JCS - JSON Canonicalization Scheme).
> - Ở chế độ Masked, tính toán EvidenceRoot và NotarySeal được thực hiện với forensics đã che giấu.
> - Một timestamp được sử dụng trong toàn bộ quy trình (forensics + NotarySeal); đảm bảo tính xác định.
> - **Tên trường Forensics:** `ip_masked`, `location`, `device`, `timestamp` (mã và registry hoàn toàn tương thích).
> - **Đường dẫn Registry:** `certificate.asset.fingerprints` (hoàn toàn tương thích với mã verify).
> - **signer_sig trong Registry:** Trường `proof.signer_sig` là cần thiết cho Full Verify.
> - Cơ chế SignerSignature sẽ được kích hoạt trong Giai đoạn 2 với Solana Wallet Adapter; trong v1.0, xác minh có thể được thực hiện với `attestation_pubkey`.

---

## 📊 Phân Tích Đối Thủ (Đã Cập Nhật)

PoArt được định vị trên "Sweet Spot" (Điểm Lý Tưởng Nhất) hoàn thiện những thiếu sót của các giải pháp hiện có.

| Tính Năng | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|-----------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Chi Phí** | 🆓 Miễn Phí | 🆓 | 💰 Có Phí | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **Drag & Drop UI** | ✅ Rất Dễ | ❌ CLI | ⚠️ Trung Bình | ⚠️ Trung Bình | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Multi-Format Export** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Real-Time Preview** | ✅ Trực Tiếp | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Privacy Controls** | ✅ 3 Chế Độ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Client-Side Hash** | ✅ Quyền Riêng Tư | ✅ | ❌ Tải Lên | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Forensic Metadata** | ✅ Đầy Đủ | ❌ | ❌ | ⚠️ Hạn Chế | ❌ | ⚠️ | ❌ | ⚠️ |
| **QR Verification** | ✅ Tức Thì | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Rate Limiting** | ✅ RLS+Client | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Blockchain Anchor** | 🔄 Lộ Trình | ✅ Bitcoin | ✅ Ethereum | ✅ Multi | ✅ | ✅ | ✅ | ✅ |
| **Open Source** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Hỗ Trợ Tiếng Thổ Nhĩ Kỳ** | ✅ Native | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Giải Thích:**
- ✅ : Hỗ trợ đầy đủ / có sẵn
- ⚠️ : Hạn chế / trong các gói trả phí
- ❌ : Không / không được hỗ trợ
- 🔄 : Trong lộ trình (đang phát triển)
- 🆓 : Hoàn toàn miễn phí
- 💰 : Có phí / yêu cầu đăng ký

### Thiếu Sót Của Đối Thủ, Điểm Mạnh Của PoArt

| Thiếu Sót | Đối Thủ | PoArt |
|-----------|---------|-------|
| **Khó Sử Dụng** | CLI, cần kiến thức API, cần ví | Kéo thả, xong trong 3 cú nhấp |
| **Rào Cản Chi Phí** | Đăng ký $50-500/tháng | 100% miễn phí |
| **Quyền Riêng Tư** | Tệp được tải lên máy chủ | Client-side, tệp không bao giờ đi |
| **Dữ Liệu Pháp Y** | Chỉ timestamp | IP, vị trí, thiết bị, thời gian - tất cả |
| **Hỗ Trợ Tiếng Thổ Nhĩ Kỳ** | Không hoặc rất hạn chế | Hỗ trợ ngôn ngữ native |
| **Nguồn Mở** | Hộp đen | Tất cả mã mở trên GitHub |

---

## 📈 Thống Kê Sử Dụng (Mục Tiêu Q1 2026)

| Chỉ Số | Mục Tiêu | Trạng Thái |
|--------|----------|------------|
| **Tổng Chứng Chỉ** | 1,000 | 🔄 Đang Tiến Hành |
| **Người Dùng Hoạt Động** | 500 | 🔄 Đang Tiến Hành |
| **Số Lần Xác Minh** | 5,000 | 🔄 Đang Tiến Hành |
| **Uptime** | %99.9 | ✅ Hoạt Động |
| **Avg Response Time** | <200ms | ✅ Tối Ưu |

---

## 🌍 Cộng Đồng & Hỗ Trợ

- **Twitter:** [@Galerilhan](https://twitter.com/Galerilhan)
- **Web:** [ilhanart.org](https://ilhanart.org)
- **Email:** galeri@ilhanart.org
- **Instagram:** https://www.instagram.com/ilhanartgaleri

---

## 🙏 Người Đóng Góp

Giao thức PoArt tiếp tục phát triển với đóng góp của cộng đồng nguồn mở.

**Để đóng góp:**
1. Fork repo
2. Tạo feature branch (`git checkout -b feature/amazing-feature`)
3. Commit (`git commit -m 'Add amazing feature'`)
4. Push (`git push origin feature/amazing-feature`)
5. Mở Pull Request

### 🛠️ Chúng Tôi Cần Gì Ngay Bây Giờ? (Kêu Gọi Giúp Đỡ)

Giao thức PoArt đang chờ đợi đóng góp từ các nhà phát triển có kinh nghiệm trong các lĩnh vực sau cho việc phát triển **Giai Đoạn 2**:

* **Supabase Edge Functions:** Chuyển bảo vệ spam sang phía máy chủ.
* **Solana Web3.js:** Tích hợp Wallet Signing (Ký Ví).
* **IPFS / Arweave:** Tích hợp lưu trữ và dịch vụ pinning.
* **Community Tools:** Bỏ phiếu X, hệ thống voting, analytics dashboard.

> Vui lòng bắt đầu thảo luận trong tab "Issues" trước khi thêm tính năng.

---

## 💬 Ghi Chú Cuối

### Pump.fun và Thực Tế

Dự án này được bắt đầu trên Pump.fun vì:
- ✅ Truy cập thanh khoản (Raydium automatic migration)
- ✅ Truy cập cộng đồng hiện có
- ✅ Chi phí khởi đầu thấp

Tuy nhiên, hãy làm rõ:
- **Giá token** không phải là chỉ số thành công nghệ thuật
- **Ngân sách vận hành** cần giá trị token (gallery, triển lãm, cơ sở hạ tầng)
- **Chỉ số thành công:** Authenticated artworks + community engagement + khách tham quan vật lý

### Governance và Phi Tập Trung

**Thực Tế v1.0 (2026):**
- Registry: Off-chain (PostgreSQL + IPFS backup)
- Attestation: Gallery self-signed (tập trung nhưng minh bạch)
- Governance: Advisory only (quyết định cuối cùng giám tuyển)
- Token utility: Gallery access + registry + NFT priority

**Tầm Nhìn v2.0+ (2027+):**
- Registry: On-chain (Solana)
- Signatures: Wallet-based (phi tập trung)
- Governance: Hybrid (community advisory + curatorial quality)
- Token utility: Enhanced features + advanced access

Cấu trúc này cung cấp **hiệu quả vận hành** và **kiểm soát chất lượng** trong giai đoạn đầu, trong khi giữ mở con đường để tăng **sự tham gia của cộng đồng** trong tương lai.

---

**[PoArt] Proof of Art Protocol v1.0**  
*"Culture > Capital" // Văn Hóa Lớn Hơn Vốn*

## 🧾 Giấy Phép

MIT License © 2026 İlhan Art Gallery Initiative

Xem [![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE) để biết đầy đủ điều khoản.

---

## 💬 Credits

![Version](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Security](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Platform](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![License](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Dự án này được phát triển với sáng kiến [İlhan Art Gallery], mã nguồn được công khai vì sự minh bạch.**

**PROTOCOL V1.0 // ĐƯỢC NIÊM PHONG VỚI SHA-512.**

*© 2026 İLHAN ART | TẤT CẢ QUYỀN VỀ TÁC PHẨM, HÌNH ẢNH VÀ Ý TƯỞNG ĐƯỢC BẢO LƯU.*

---
