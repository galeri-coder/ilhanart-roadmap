# 📚 Từ Điển Thuật Ngữ và Khái Niệm Kỹ Thuật
> **"Hiểu ngôn ngữ của giao thức này có nghĩa là hiểu tầm nhìn của nó."**

## ⚙️ PoArt Forensic Engine (PFE) v1.0: Kiến Trúc Cơ Bản

**PoArt Forensic Engine (PFE)** là lớp trung tâm đại diện cho logic và hoạt động kỹ thuật đằng sau giao thức [PoArt]. Đây là một "động cơ pháp y" lấy dữ liệu sản xuất nghệ thuật thô và chuyển đổi nó thành **bằng chứng kỹ thuật số** có thể xác minh và không thể thay đổi.

### 🧩 Tại Sao "PoArt Forensic"?

- **PoArt (Bằng Chứng Nghệ Thuật):** Mục đích của động cơ là kết nối giá trị của tài sản kỹ thuật số không phải với ước tính, mà với **quy trình sản xuất có thể xác minh**.
- **Forensic (Xác Minh Khoa Học):**
  - **Định Nghĩa Kỹ Thuật:** Phương pháp thuật toán và chuỗi bản ghi để xác minh rằng dữ liệu quy trình sản xuất (nét cọ, video thời gian, bản ghi) không bị thao túng.
  - **Mức Độ Triết Học:** Tuyên bố chuyển đổi **chi phí thời gian con người, lao động và quyết định** thành sự thật có thể đo lường, trái ngược với sản xuất "kết quả tức thì" của AI.

> Lưu ý: Tích hợp blockchain (ví dụ: Solana) không phải là phần cốt lõi của PFE; nó sẽ được mô tả riêng như **lớp neo chuỗi** cho mục đích xác minh/đăng ký.

### 🛠️ Phạm Vi Kỹ Thuật v1.0

**PoArt Forensic Engine (PFE) v1.0** được xây dựng trên **3 trụ cột chính** sau đây thay vì các mô hình tài chính phức tạp:

1. **Hashing & Sealing (Niêm Phong):**  
   PFE xử lý tất cả các yếu tố trong gói bằng chứng (tệp tác phẩm, video, JSON/bản ghi, chữ ký, v.v.) theo cách xác định và tạo ra giá trị **NotarySeal** duy nhất.

   **Khái Niệm Chính (v1.0):**
   - **FileHash (Dấu Vân Tay Kỹ Thuật Số Của Tác Phẩm):** Hash được tạo từ byte của tệp tác phẩm.
   - **EvidenceRoot (Gốc Gói Bằng Chứng):** Tóm tắt gốc đại diện cho tính toàn vẹn của gói bằng chứng (gốc Merkle hoặc hash của biểu diễn chính tắc).
   - **NotarySeal (Con Dấu Cuối Cùng / Đầu Ra PFE):** Con dấu cuối cùng được tạo từ sự kết hợp EvidenceRoot + thời gian + chữ ký.

   **Công Thức (hiển thị rõ ràng cho nhà đầu tư):**
   
   $$\text{FileHash}_{512} = \text{SHA-512}(\text{ArtworkFileBytes})$$
   
   $$\text{NotarySeal} = \text{SHA-512}(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp})$$
   
   **Định Nghĩa Payload Chính Tắc (v1.0):**
   
   - **EvidenceRootPayload:**
```
   file_sha512:{sha512}\nforensics:{canonicalForensics(forensics)}
```
   
   - **NotarySealPayload:**
```
   evidence_root:{evidence_root}\nsigner_sig:{signer_sig}\ntimestamp:{timestamp}
```
   
   > Lưu ý: Giá trị được đề cập làm đầu ra PFE là **NotarySeal**. Quy trình **SignerSignature** sẽ được kích hoạt ở giai đoạn 2 (với Solana Wallet Adapter); trong phiên bản v1.0 hiện tại, chữ ký chứng thực hệ thống được sử dụng. Khóa công khai chứng thực được công bố trong sổ đăng ký dưới trường `issuer.attestation_pubkey`.

2. **Indexing (Lưu Trữ):**  
   Viết vào lớp sổ đăng ký rõ ràng và có thể truy vấn ví nào, vào ngày nào, đã gửi **bằng chứng công việc** cho tác phẩm nào.  
   *(Lớp này có thể là cơ sở dữ liệu; tích hợp chuỗi được mô tả riêng như "lớp neo chuỗi".)*

3. **Verification (Xác Minh):**  
   Khi câu hỏi về tính hợp lệ của tác phẩm nảy sinh, PFE xử lý lại bằng chứng thô; xác minh toán học rằng các giá trị được tính toán **EvidenceRoot / NotarySeal** khớp với các bản ghi được lưu trữ.

---

### 🧮 Định Lý Giá Trị PoArt (The Value Theorem)

Giao thức [PoArt] không kết nối giá trị ($V$) của tài sản kỹ thuật số với nhận thức thị trường mơ hồ, mà với **thực tế vật lý của quy trình sản xuất**.

Trí tuệ nhân tạo (AI) phá hủy quy trình bằng cách cung cấp kết quả tức thì ($t \to 0$). [PoArt], tuy nhiên, duy trì giá trị như sự tích lũy của các yếu tố **thời gian, lao động và quyền năng**.

$$V_{\text{PoArt}} = \int_{t_{\text{start}}}^{t_{\text{end}}} \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt + U_{\text{irreversible}}$$

#### Định Nghĩa Biến Số

- **$\int dt$ (Tích Lũy Quy Trình):**  
  Giá trị không phải là "kết quả tức thì"; đây là một **quy trình** được tích lũy giữa $t_{\text{start}}$ và $t_{\text{end}}$. Khi giai đoạn co lại (sản xuất AI), kết quả tích phân tiến gần đến 0.

- **$P_{\text{labor}}(t)$ (Sức Lao Động Tức Thì):**  
  Đại diện cho cường độ lao động tinh thần và vật chất được tiêu tốn trong quá trình sản xuất. Khi lao động có thể xác minh tăng lên, tích phân tăng lên.  
  > Lưu ý: Thuật ngữ này có thể được khái quát hóa một cách thực tế bằng "tín hiệu lao động có thể đo lường/có thể xác minh".

- **$I_{\text{agency}}(t)$ (Yếu Tố Quyền Năng):**  
  Khả năng của người sáng tạo để chấp nhận rủi ro và đưa ra quyết định. Lấy giá trị giữa $0$ và $1$.
  - **AI ($I \approx 0$):** Thực hiện lệnh, không chấp nhận rủi ro, không trả giá.
  - **Con người ($I \to 1$):** Thay đổi quyết định, do dự, chấp nhận rủi ro.

- **$U_{\text{irreversible}}$ (Tính Độc Đáo Không Thể Đảo Ngược):**  
  Mặc dù trong sản xuất kỹ thuật số việc hủy bỏ có thể thực hiện được (`Ctrl+Z`), trong sản xuất vật lý (sơn được áp dụng trên canvas, đá được chạm khắc, hành động trong phát sóng trực tiếp) không có cách nào để quay lại. **Bản chất không thể đảo ngược** này là một thành viên bổ sung tạo ra "tính độc đáo" (đặc điểm không thể thay đổi) trong tác phẩm.

### 🔎 Phân Tích Trường Hợp: AI "Kết Quả Tức Thì" vs Con Người "Quy Trình Được Xác Minh"

Kịch bản sau đây cho thấy **Định Lý Giá Trị PoArt** hoạt động như thế nào trong thực tế và tại sao sản xuất AI nhận được điểm thấp hơn trên thang đo [PoArt].

#### Kịch Bản A: Sản Xuất Cảnh 10 Giây Với AI

- **Giai Đoạn ($\Delta t$):** $10$ giây (quy trình ngắn)
- **Sức Lao Động ($P_{\text{labor}}$):** $1$ đơn vị (chỉ viết lệnh)
- **Yếu Tố Quyền Năng ($I_{\text{agency}}$):** $0.01$ (không có rủi ro, không có chi phí)
- **Bản Chất Không Thể Đảo Ngược ($U_{\text{irreversible}}$):** $0$ (có thể đảo ngược / có thể sao chép)

**Kết Quả:**

$$V_{\text{AI}} \approx \int_{0}^{10} (1 \cdot 0.01) \, dt + 0 = 0.1$$

> **Bình Luận:** Mặc dù kết quả hoàn hảo; giá trị [PoArt] tiến gần đến $0$ bởi vì không có quy trình nào sống sót và không có quyền năng/rủi ro nào liên quan.

#### Kịch Bản B: Sản Xuất Vật Lý 6 Giờ Trong Phát Sóng Trực Tiếp

- **Giai Đoạn ($\Delta t$):** $6$ giờ ($21{,}600$ giây)
- **Sức Lao Động ($P_{\text{labor}}$):** $0.5$ đơn vị (lao động vật chất và tinh thần liên tục)
- **Yếu Tố Quyền Năng ($I_{\text{agency}}$):** $0.9$ (quyết định thay đổi, chấp nhận rủi ro, lựa chọn không thể đảo ngược)
- **Bản Chất Không Thể Đảo Ngược ($U_{\text{irreversible}}$):** $>0$ (dấu hiệu vật lý không thể trả lại)

**Kết Quả:**

$$V_{\text{Human}} \approx \int_{0}^{21600} (0.5 \cdot 0.9) \, dt + U_{\text{irreversible}} \approx 9720 + U_{\text{irreversible}}$$

> **Bình Luận:** Với việc mở rộng quy trình và tăng quyền năng (rủi ro), giá trị được thu thập dưới dạng tích lũy. Thành viên $U_{\text{irreversible}}$ là đóng góp bổ sung tạo ra "tính độc đáo" (đặc điểm không thể thay đổi) trong tác phẩm.

---

### ✅ Kết Luận: Giá Trị Gắn-Bằng Chứng (Proof-Bound Value)

Định lý này kéo tuyên bố giá trị của [PoArt] ra khỏi "sở thích" hoặc "câu chuyện thị trường" và kết nối nó với **thực tế sản xuất có thể xác minh**.

1. **Không Có Quy Trình, Không Có Giá Trị:**  
   AI phá hủy quy trình với kết quả tức thì ($t \to 0$). Khi cửa sổ quy trình co lại, kết quả tích phân phải giảm:
   
   $$\Delta t \downarrow \ \Rightarrow\ \int \left(P(t) \cdot I(t)\right) dt \to 0$$

2. **Quyền Năng và Rủi Ro Là Hệ Số Nhân:**  
   [PoArt] không chỉ đo "thời gian đã tiêu tốn" mà còn mức độ quyết định thực tế, rủi ro và giá trong thời gian đó. Sản xuất không có rủi ro (AI) ít giá trị hơn:
   
   $$V_{\text{PoArt}} \propto \int \left(P_{\text{labor}}(t) \cdot I_{\text{agency}}(t)\right) dt$$

3. **Tính Độc Đáo Là Bằng Chứng Vật Lý, Không Phải Tiếp Thị:**  
   Dấu hiệu không thể đảo ngược trong sản xuất vật lý (nét vẽ trên canvas, mảnh đá) nằm ngoài logic `Ctrl+Z` kỹ thuật số. Bản chất không thể đảo ngược này ($U_{\text{irreversible}}$) làm cho tác phẩm trở nên độc đáo thông qua sự tồn tại.

> **🔐 Tóm Tắt:** Định lý giá trị có thể có vẻ như là phép đo sự không chắc chắn (mặc dù tương đương thế giới thực không thể được đo đầy đủ), mục đích của công thức này là thiết lập các biến số và chỉ ra hướng. Trong thời đại AI, điều hiếm không phải là "hình ảnh" mà là **công việc có thể xác minh, thời gian và quyền năng**. [PoArt] đo sự hiếm này và viết nó với **gói bằng chứng**.

### 🏛️ Tầm Quan Trọng Của Khái Niệm "Động Cơ"

Token đến từ Pump.fun hoặc các nền tảng tương tự thường chỉ là **"vé vào cửa"**. **PoArt Forensic Engine (PFE)**, tuy nhiên, là **lớp logic hiến pháp** quyết định vé này bảo vệ những quyền nào, tác phẩm sẽ được viết như thế nào và nghệ thuật/khoa học/công nghệ sẽ được bảo tồn như thế nào.

> **Lưu ý:** Lý do chúng tôi bắt đầu dự án này tại Pumpfun là do thiếu ngân sách đủ và không có môi trường để tiếp cận khán giả hiện tại thông qua phát sóng trực tiếp. Việc sử dụng dữ liệu hiện tại là một bước đúng đắn về mặt chiến lược, mặc dù không phải chất lượng cao nhất. Bất kể ngân sách và nguồn lực, việc xác định logic của động cơ này trên GitHub chứng minh rằng dự án không chỉ là một đánh giá tài chính, mà là tầm nhìn dài hạn của **cơ sở hạ tầng phần mềm** và **thư viện kỹ thuật số quốc gia**.

---

## 🎨 Giao Thức [PoArt] Bằng Chứng Công Việc (Proof of Art Protocol v1.0)

> **"Nghệ sĩ thực sự, sản xuất thực sự, giá trị thực sự."**

Giao thức này là một **quy trình bảo vệ sinh học và trí tuệ** được phát triển chống lại những kẻ lừa đảo ẩn danh bao quanh hệ sinh thái crypto, chống lại hình ảnh AI được tạo trong 5 phút, và chống lại văn hóa "Pump & Dump".

---

## a) [PoArt] Là Gì? (Định Nghĩa Triết Học và Kỹ Thuật)

**Bằng Chứng Nghệ Thuật [PoArt];** là tiêu chuẩn chứng nhận thể chế đảm bảo rằng giá trị đằng sau tài sản trên blockchain không dựa trên ước tính, mà dựa trên **lao động con người**, **thời gian** và **năng lượng vật lý có thể xác minh**.

Bitcoin *"bằng điện và sức mạnh bộ xử lý"* **(bằng chứng công việc)** tạo ra giá trị, tương tự các dự án kết nối với [PoArt] *"bằng kỹ năng nghệ thuật và thời gian con người"* tạo ra giá trị.

Điều này loại bỏ rủi ro *"Developer bán, dự án kết thúc"* trên các nền tảng Pump.fun và DEX; bởi vì ở đây giá trị không ở trong mã mà ở trong **tính liên tục của sản xuất**.

> **[PoArt] không nói với người tham gia "hãy tin chúng tôi"; nó nói "đây là bằng chứng, hãy xem bằng mắt của bạn, xác minh bằng toán học của bạn."**

---

## b) Tiêu Chuẩn 5-Trụ Cột Của [PoArt] (5 Trụ Cột Sự Thật)

5 mục này là các bộ lọc không thể thay đổi mà dự án phải vượt qua để nhận được con dấu [PoArt].

### 1) Bằng Chứng Danh Tính Trực Tiếp

- **Vấn Đề:** Thế giới crypto đầy rẫy những người sáng lập ẩn danh (Devs) với danh tính mơ hồ thu tiền và bỏ dự án.
- **Giải Pháp [PoArt]:** Người sáng tạo không chỉ xác minh danh tính mà còn **sự hiện diện trong quá trình sản xuất**. Điều này bao gồm các phiên phát sóng trực tiếp nơi cuộc trò chuyện với cộng đồng được thực hiện và các yêu cầu cụ thể được thực hiện ngay lập tức, không phải video được ghi trước.  
  (Ví dụ, *"Viết ngày hôm nay và số khối hiện tại ở góc phải của canvas"*)
- **Khẩu Hiệu:** *"Bot có thể vẽ nhưng bot không đổ mồ hôi và không thể ứng biến."*

### 2) Bằng Chứng Công Việc và Quy Trình

- **Vấn Đề:** Hình ảnh AI (trí tuệ nhân tạo) được tạo trong 2 giây nhận được cùng đối xử "jpeg" trong thế giới kỹ thuật số với bức tranh sơn dầu được tạo trong 2 tháng.
- **Giải Pháp [PoArt]:** Quy trình "mang thai và sinh nở" của tác phẩm được viết. Giai đoạn phác thảo, giai đoạn vẽ, số giờ tích lũy đã tiêu tốn và quy trình vật lý mà nghệ sĩ trải qua khi tạo tác phẩm được viết. Điều này thêm **"giá thời gian"** vào token. Sản xuất tài sản khó, giá trị của nó mạnh mẽ.

### 3) Bằng Chứng Giá Trị Thẩm Mỹ

- **Vấn Đề:** Văn hóa "meme" chỉ tập trung vào tiếng cười tức thì trong khi vẻ đẹp và chiều sâu nghệ thuật bị bỏ qua, đó là lý do cho các dự án "Hype" ngắn hạn.
- **Giải Pháp [PoArt]:** Dự án phải có tiêu chuẩn nghệ thuật học thuật, lý thuyết màu sắc, quy tắc sáng tác và kiến thức vật liệu (Impasto, Texture, v.v.). Nội dung không chỉ phải làm bạn cười; nó phải tạo ra sự ngưỡng mộ ở người xem và có **giá trị sưu tập**.

### 4) Đổi Mới Khái Niệm

- **Vấn Đề:** Hàng nghìn bản sao của token chó/mèo không có sự sáng tạo.
- **Giải Pháp [PoArt]:** Dự án phải tạo ra một cây cầu mới kết nối nghệ thuật, khoa học, triết học hoặc công nghệ trong một cấu trúc có ý nghĩa.  
  (Ví dụ, kết nối tượng David cổ đại với dữ liệu thị trường crypto; xử lý ý tưởng "biến đổi con người thành đá" thông qua điều này và đặt nền tảng nó với các nguồn khoa học.)  
  Tác phẩm không chỉ phải là một lời mời thị giác mà còn là một **thách thức trí tuệ** kích thích suy nghĩ về khoa học, triết học hoặc công nghệ.

> [!IMPORTANT]
> **Ví Dụ Đáng Nhớ (Hiệu Ứng Las Palmitas):** Ở khu vực Las Palmitas ở Mexico, bị tội phạm hành hạ, hơn 200 ngôi nhà đã biến thành một triển lãm cầu vồng khổng lồ. Kết quả của sự can thiệp vẻ đẹp này, tỷ lệ tội phạm trong khu vực giảm đáng kể, và thanh niên bắt đầu tham gia vào nghệ thuật thay vì băng đảng tội phạm. Sự chuyển đổi của vẻ đẹp đã viết lại sự tôn trọng của mọi người đối với môi trường và lẫn nhau (hội nhập xã hội).
>
> **Kỳ Vọng:** Dự án tham gia danh sách [PoArt] phải, giống như ví dụ trên, có mối quan hệ nhân quả xã hội, khoa học hoặc triết học ngoài vẻ đẹp thị giác. Thời gian là vốn duy nhất không thể mua bằng tiền do đó, trong giao thức này phải được xác minh bằng cách đặt thời gian làm bảo đảm. Cơ sở khái niệm của dự án phải đủ mạnh và phổ quát để, ngay cả nhiều năm sau, trong tình huống CTO (Community Takeover) có thể xảy ra, cộng đồng có thể tiếp tục năng lực sáng tạo của dự án một cách độc lập trong khi kế thừa di sản này.

### 5) Không Phải Thuật Toán Mà Là Quyền Năng

- **Vấn Đề:** Sản xuất kỹ thuật số lặp lại hoàn hảo nhưng không có linh hồn.
- **Giải Pháp [PoArt]:** Quyền năng độc đáo của con người có thể mắc lỗi, chấp nhận rủi ro và trải nghiệm thay đổi cảm xúc phải được cảm nhận trong tác phẩm. Sự không chắc chắn trong nét cọ, phản ứng đột ngột của vật liệu và quyết định tức thời của nghệ sĩ là **chữ ký sinh học** phân biệt tác phẩm với "sản xuất cơ khí".

---

## c) Quy Trình Xác Minh và Ngăn Chặn Gian Lận

Hệ thống này đảm bảo rằng dự án vẫn đáng tin cậy và sống động không chỉ "ngay từ đầu" mà "luôn luôn".

### 📦 Gói Bằng Chứng - Song Sinh Kỹ Thuật Số

Đằng sau mỗi tác phẩm được phê duyệt bởi [PoArt] có một gói dữ liệu được mã hóa và đánh dấu thời gian mà nhà đầu tư có thể tải xuống:

- **Bản Ghi Video RAW:** Phim thô liên tục của thời gian sản xuất.
- **Phân Tích Metadata:** Ngày tạo tệp, thông tin về các công cụ được sử dụng và dữ liệu vị trí.
- **Tham Chiếu Vật Lý:** Bằng chứng rằng tác phẩm tồn tại trong thế giới vật lý  
  (Ví dụ, báo hiện tại hoặc dữ liệu blockchain của thời gian đó bên cạnh tác phẩm).

> *Lưu Ý Tuân Thủ:* Thuật ngữ "gói bằng chứng" trong các phần trước kết nối với chuỗi **gói bằng chứng → EvidenceRoot → NotarySeal**; nghĩa là, tính toàn vẹn của gói được đại diện bởi con dấu có thể xác minh.

### 🔄 Gia Hạn 365 Ngày (Giao Thức Bền Vững)

- **Tính Năng Cách Mạng:** Trong các dự án crypto "Dev" (Developer) thường phát hành token và thường biến mất sau 1-2 tháng (soft rug). [PoArt] làm cho điều này trở nên không thể.
- **Quy Tắc:** Trạng thái "nghệ sĩ đã xác minh" không phải là suốt đời. Chỉ **1 năm** có hiệu lực.
- **Hoạt Động:** Nghệ sĩ/developer phải trình bày **tác phẩm mới quan trọng và có thể xác minh** cho cộng đồng mỗi 365 ngày.
- **Ví Dụ Kịch Bản:** Bắt đầu dự án vào năm 2026. Vào tháng 1 năm 2027, hệ thống đưa ra cảnh báo "bằng chứng đã hết hạn". Nếu nghệ sĩ không trình bày một triển lãm mới, tác phẩm vật lý mới hoặc tích hợp kỹ thuật mới thì "huy hiệu tin cậy" của dự án sẽ giảm.
- **Kết Quả:** Hệ thống này đảm bảo **nội dung không bao giờ mất tính liên quan** và nhà đầu tư không bao giờ sợ *"Developer vẫn còn ở đây chứ?"*. Dự án trở thành một studio sống động.

### 🚩 Giao Thức Cờ Đỏ

**Trong mọi tình huống gian lận được phát hiện bởi cộng đồng hoặc thuật toán (sử dụng AI, tác phẩm bị đánh cắp, video bị thao túng):**

1. Chứng chỉ ngay lập tức được đánh dấu là **"VOID" (vô hiệu)**.
2. Các gói bằng chứng được đánh dấu công khai là **"giả mạo"**.
3. Dự án được đưa vào danh sách đen [PoArt]. Điều này trong thế giới phi tập trung, **danh tiếng là tiền tệ** củng cố.

---

## d) Kết Luận: Không Phải Casino, Mà Là Bảo Tàng

**Pump.fun và các sàn giao dịch phi tập trung (DEX) thật không may bây giờ là casino; đèn nhấp nháy, mọi người đều đuổi theo lợi nhuận nhanh chóng, và nhà (kẻ lừa đảo) luôn thắng. Lý do chúng tôi bắt đầu dự án này ở đây là do thiếu ngân sách đủ và không có môi trường để tiếp cận khán giả hiện tại thông qua phát sóng trực tiếp.**

**[PoArt] là pháo đài được xây dựng giữa casino này.**

- 🎰 Casino dựa trên trò chơi bài; chúng tôi **dựa trên thực tế vật lý**.
- 🃏 Casino mở cửa cho gian lận; chúng tôi **mở cửa cho bằng chứng rõ ràng**.
- ⏳ Casino là tạm thời; chúng tôi **tập trung vào sự bất diệt của nghệ thuật và khoa học**.

**Token sử dụng giao thức này không chỉ là "đồng xu"; đây là vốn kỹ thuật số với mồ hôi, màu sắc, mã và tầm nhìn.**

---

## 🗳️ 6) Quản Trị và Sổ Đăng Ký Công Khai

**Mục đích của phần này: Chuyển đổi tiêu chuẩn [PoArt] từ mức "tin tưởng vào con người" thành cơ sở hạ tầng công cộng bền vững với sổ đăng ký + xác minh + giám sát cộng đồng.**

### 6.1 Sổ Đăng Ký Công Khai

- **Sổ Đăng Ký Công Khai:** Tất cả dữ liệu được phê duyệt được viết tại `ilhanart.org/registry` (hoặc GitHub Registry).

**Logic Sổ Đăng Ký (tiêu chuẩn được đề xuất - ở định dạng đường dẫn JSON):**

Mỗi mục nhập vào sổ đăng ký có các trường cốt lõi tối thiểu có thể xác minh này:

- **Danh Tính và Trạng Thái:**
  - `certificate_id` (tham chiếu có thể đọc)
  - `status` (active / void)
  - `void_reason` (nếu có)
  - `visibility` (private / masked / public)
  - `created_at` (dấu thời gian)

- **Cơ Quan Phát Hành:**
  - `issuer.name`
  - `issuer.location`
  - `issuer.attestation_pubkey`

- **Thông Tin Tác Phẩm:**
  - `asset.title`
  - `asset.creator`
  - `asset.creator_wallet` (nếu có thể; để nhận dạng với cổng token)
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
  - `governance.veto_threshold`

Sổ đăng ký có thể có hai cấp:
- **1)** Chỉ mục có thể đọc bởi con người (danh sách web / tìm kiếm / lọc)
- **2)** Biểu diễn có thể đọc bởi máy (bản ghi JSON; để xác minh PFE)

**"Đăng ký" này trở nên có thể xác minh thông qua chuỗi PFE gói bằng chứng → EvidenceRoot → NotarySeal. Sổ đăng ký cung cấp mục tiêu xác minh, không phải "tuyên bố".**

---

### 6.2 Quyền Phủ Quyết 40% Cộng Đồng (Quản Trị Cổng-Token)

- **Quyền Phủ Quyết 40% Cộng Đồng:** Bỏ phiếu bắt đầu một tháng trước khi cấp trạng thái; **40% cộng đồng cổng-token (được xác minh với Solana)** phủ quyết hủy bỏ đơn đăng ký.

**Luồng Bỏ Phiếu (quy trình rõ ràng được đề xuất):**
- **Cửa Sổ Đăng Ký:** Dự án ứng cử viên mở "đăng ký ứng cử viên PoArt" (bản ghi ứng cử viên xuất hiện với trạng thái "pending").
- **Giai Đoạn Xem Xét:** Cộng đồng xem xét bằng chứng lên đến 30 ngày (gói bằng chứng + bản ghi phát sóng trực tiếp + metadata).
- **Xác Minh Cổng-Token:** Bỏ phiếu được thực hiện với ví Solana được xác minh (ví dụ quyền sở hữu token/NFT cụ thể + chữ ký ví).
- **Quy Tắc Phủ Quyết:** Nếu 40% phiếu bầu là **phản đối (không / phủ quyết)** thì đơn đăng ký bị hủy bỏ.
- **Minh Bạch:** Kết quả bỏ phiếu được lưu trong sổ đăng ký dưới dạng "bản ghi quyết định" (ngày, tỷ lệ, ID hình ảnh).

---

### 6.3 Đồng Bộ Metadata (Căn Chỉnh Với Thế Giới Vật Lý)

- **Đồng Bộ Metadata:** Dữ liệu kỹ thuật trong sổ đăng ký phải khớp 100% với thực thể vật lý.

**Định Nghĩa Kỹ Thuật "100% Căn Chỉnh" (minh bạch được đề xuất):**
- **Căn Chỉnh Tối Thiểu (bắt buộc):**
  - `asset.fingerprints.sha256/sha512` trong sổ đăng ký phải **giống hệt** với hash của tệp được thảo luận.
  - `proof.notary_seal` trong sổ đăng ký được tạo lại (nếu gói bằng chứng tồn tại), phải **giống hệt**.
- **Căn Chỉnh Tham Chiếu Vật Lý (loại bằng chứng):**
  - Tác phẩm vật lý + ngày/tham chiếu khối được hiển thị trong phát sóng trực tiếp và bằng chứng tương tự phải khớp với gói bằng chứng.
- **Tuân Thủ Quyền Riêng Tư:**
  - Các trường như IP/vị trí trong khả năng hiển thị `masked` được công bố **theo tiêu chuẩn che dấu**.

---

### 6.4 Tranh Chấp và Hủy Bỏ

Sổ đăng ký không chỉ là quy trình "phê duyệt"; đây là **quy trình xem xét sống động** chống lại gian lận.

- Khi tranh chấp bắt đầu, mục nhập có thể được đặt trong trạng thái **"review" (xem xét)**.
- Khi gian lận được phát hiện, nó được đánh dấu là `status: void` và lý do được thêm vào:
  - `void_reason` (sử dụng AI / trộm cắp / thao túng, v.v.)
  - `revoked_at` (thời gian hủy bỏ)
- Nguồn quyết định hủy bỏ rõ ràng trong sổ đăng ký:
  - Bỏ phiếu cộng đồng / ủy ban chính thức / ghi chú điều tra khoa học (có thể áp dụng)

> **Phần này là song sinh sổ đăng ký của khái niệm VOID trong phần "Giao Thức Cờ Đỏ".**

---

### 6.5 Ví Dụ Mục Nhập Sổ Đăng Ký (có thể đọc bởi máy)
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
> *Lưu ý: `asset.fingerprints.sha512` và các giá trị hash khác được rút gọn cho mục đích hiển thị; trong triển khai thực tế, chuỗi thập lục phân có độ dài đầy đủ được sử dụng.*

---

## 7) 🔐 Con Dấu Kỹ Thuật (NOTARY SEAL)

**Thuật toán con dấu không thể thay đổi được tạo bởi PoArt Forensic Engine (PFE) v1.0:**

$$\text{NotarySeal} = \text{SHA-512}\left(\text{EvidenceRoot} \mid \text{SignerSignature} \mid \text{TimeStamp}\right)$$

---

# Giao Thức [PoArt] Công Chứng Kỹ Thuật Số và Bằng Chứng Khoa Học (Beta v1.0)

> **"Văn hóa lớn hơn vốn. Bảo vệ tác phẩm của bạn hôm nay, chuyển giao ngày mai."**

---

## Tại Sao Công Khai?

Bảo mật thực sự đến từ sự minh bạch. Nhờ hệ thống **sổ đăng ký công khai** của chúng tôi, bất kỳ ai ở bất kỳ đâu trên thế giới đều có thể xác minh trong vài giây liệu tệp có thật hay không, mà không cần quyền.

---

## 🧩 Tại Sao Nhiều "Mô-đun Khả Năng Hiển Thị"?

Đây là phần quan trọng nhất của mã (menu tùy chọn khả năng hiển thị). Các tùy chọn này cho phép người dùng tạo ra sự cân bằng trong **"quyền riêng tư vs minh bạch"**:

### 🔒 Riêng Tư

- **Kịch Bản:** Nghệ sĩ chưa muốn công bố tác phẩm, nhưng muốn đánh dấu thời gian để chứng minh "Tôi đã làm điều này vào ngày này".
- **Mã làm gì:** Viết dữ liệu vào cơ sở dữ liệu nhưng đánh dấu con dấu là `visibility: "private"`. Sau này khi bạn viết chính sách "đọc công khai", bạn có thể ẩn các bản ghi này khỏi mọi người với `WHERE visibility = 'public'`.

### 🕶️ Che Dấu

- **Kịch Bản:** Nghệ sĩ muốn minh bạch nhưng lo lắng rằng địa chỉ nhà của họ (vị trí IP) sẽ được biết.
- **Mã làm gì:** Các hàm `maskIP` và `maskLoc` hoạt động ở phía JavaScript. Điều này thay đổi địa chỉ IP sang định dạng `88.241.***.***`, vị trí sang định dạng `***/TR`, và gửi phiên bản được kiểm duyệt đến cơ sở dữ liệu.
- **Sự Thật Về Quyền Riêng Tư:** Che dấu được thực hiện trong trình duyệt, Supabase không thấy vị trí thực. **Nhưng:** Nếu các API của bên thứ ba như ipapi.co được sử dụng cho dữ liệu vị trí, các nhà cung cấp này thấy địa chỉ IP tại thời điểm yêu cầu.
- **Niêm Phong Trong Chế Độ Che Dấu:** Tính toán EvidenceRoot và NotarySeal được thực hiện với dữ liệu pháp y được che dấu; do đó xác minh vẫn xác định.

### 🌍 Công Khai

- **Kịch Bản:** Minh bạch hoàn toàn. Theo tiêu chuẩn [PoArt], ở đâu, khi nào, từ mạng nào tác phẩm được tạo được tuyên bố công khai.

---

## 💡 Đổi Mới Kỹ Thuật

PoArt không chỉ là hệ thống tải lên tệp. Đây là động cơ **"chuỗi chăm sóc khoa học"** trộn ba mức kỹ thuật khác nhau trong một nồi để mang lại tiêu chuẩn mới.

**Lớp được mô tả là "động cơ" trong phần này phù hợp với cốt lõi của PoArt Forensic Engine (PFE) trong các thuật ngữ trước đó.**

### 1) Hashing Phía-Khách Hàng (Quyền Riêng Tư Tối Đa)

Tệp mảnh nghệ thuật của bạn không được tải lên máy chủ. Động cơ dựa trên trình duyệt (phía-khách hàng) của chúng tôi tính toán hash của tệp (tóm tắt kỹ thuật số) trên chính máy tính của bạn. Chỉ dấu vân tay kỹ thuật số này và metadata được gửi đến máy chủ.

> **Sự Thật Về Quyền Riêng Tư:** Tệp tác phẩm không được tải lên máy chủ và do đó an toàn. Tuy nhiên, dữ liệu pháp y (IP/vị trí) được chia sẻ theo chế độ khả năng hiển thị được chọn (riêng tư/che dấu/công khai).

### 2) Hợp Nhất Dữ Liệu Pháp Y (Sức Mạnh Khoa Học)

Nhiều hơn là dấu thời gian đơn giản. Hệ thống kết nối các dữ liệu này trong "con dấu gốc":

- **Tóm Tắt Kỹ Thuật Số (SHA-512):** Dấu vân tay kỹ thuật số sử dụng tiêu chuẩn tóm tắt mật mã (SHA-512) bị vỡ nếu một pixel của tác phẩm thay đổi.
- **Vị Trí và Thời Gian:** Mã hóa dữ liệu ngày, quốc gia, thành phố và khu vực với độ chính xác mili giây.
- **Nhận Dạng Thiết Bị:** Hệ điều hành, trình duyệt và loại thiết bị (phân tích User-Agent).

---

## 🛡️ Trường Hợp Sử Dụng và Lợi Ích

Nếu bạn là nghệ sĩ, nhà văn hoặc nhà thiết kế, nói "Tôi đã làm điều này đầu tiên" là không đủ; bạn phải chứng minh.

**Tác phẩm của bạn được niêm phong với PoArt:**

- **Bằng Chứng Toán Học:** Nếu ngay cả một pixel của tệp của bạn thay đổi, hệ thống biết. Thao túng là không thể.
- **Cơ Sở Pháp Lý:** Được viết vào ngày nào, tại thành phố nào, từ thiết bị nào tác phẩm được niêm phong.
- **Chứng Chỉ Tức Thì:** Tạo ra **"chứng chỉ danh tính tài sản"** đặc biệt, mã QR và con dấu cho bạn trong vài giây.

---

## ⚙️ Kiến Trúc Hệ Thống và Tính Năng Kỹ Thuật

Hệ thống được thiết kế trên kiến trúc "serverless", tập trung vào hiệu suất cao và khả năng mở rộng.

| Lớp | Công Nghệ | Mô Tả |
|--------|-----------|-------------|
| **Mã Hóa** | SHA-256 & SHA-512 | Tóm tắt mật mã hai lớp |
| **Cơ Sở Dữ Liệu** | Supabase (PostgreSQL) | Cấu trúc dữ liệu JSONB, chính sách RLS |
| **Dữ Liệu Pháp Y** | ipapi.co API | Tam giác IP/vị trí/thời gian |
| **Trình Bày** | html2canvas + jsPDF | Tạo PNG/PDF phía-khách hàng |
| **Frontend** | Vanilla JavaScript | Không phụ thuộc framework |
| **Bảo Mật** | Hashing Phía-Khách Hàng | Tệp không bao giờ đến máy chủ |

### Tính Năng Đáng Chú Ý

| Tính Năng | Mô Tả | Ở Đối Thủ? |
|---------|-------|-----------------|
| **UI Kéo và Thả** | Kéo và thả tệp, xem trước tức thì | ❌ Ở hầu hết không có |
| **Xuất Đa Định Dạng** | PNG, JSON, PDF - bằng một cú nhấp chuột | ⚠️ Hạn chế |
| **Xem Trước Thời Gian Thực** | Xem trước chứng chỉ trực tiếp | ❌ Không có |
| **Kiểm Soát Quyền Riêng Tư** | Tùy chọn riêng tư/che dấu/công khai | ❌ Không có |
| **Hash Phía-Khách Hàng** | Tệp không bao giờ đến máy chủ | ✅ Chỉ ở một số |
| **Metadata Pháp Y** | IP, vị trí, thiết bị, thời gian - tất cả cùng nhau | ❌ Tách biệt |
| **Xác Minh QR** | Xác minh tức thì mã QR | ⚠️ Hạn chế |
| **Giới Hạn Tốc Độ** | Bảo vệ spam (RLS + khách hàng) | ❌ Ở hầu hết không có |

---

## 🗺️ Lộ Trình: Tương Lai "Không Cần Tin Tưởng"

Phiên bản hiện tại **(Beta v1.0)** được thiết kế để cung cấp cho người dùng cuối tốc độ tối đa, giao diện dễ dàng và truy cập miễn phí. Tầm nhìn cuối cùng của chúng tôi, tuy nhiên, là chuyển đổi sang cấu trúc mà người quản lý cơ sở dữ liệu (chúng tôi) thậm chí không thể can thiệp.

### Giai Đoạn 1: Beta (Hiện tại trực tiếp)

- **Cơ Sở Hạ Tầng:** Cơ sở dữ liệu đám mây (Supabase).
- **Mục Đích:** Tốc độ, loại bỏ rào cản UX (trải nghiệm người dùng) và tuân thủ. Cung cấp bảo mật "không ma sát".

### 🚀 Giai Đoạn 2: (Yêu Cầu Backend / Edge Function)

Giai đoạn này bao gồm chuyển đổi từ cấu trúc quản lý đầy đủ "phía-khách hàng" sang cấu trúc "quyền phía-máy chủ" an toàn hơn và có thể kiểm soát được.

| Mục | Điều gì mang lại? | Ngăn Xếp Kỹ Thuật | Ưu Tiên |
|-------|---------------|------------|---------|
| **`INSERT` → Edge Function** | Ngăn chặn spam + bảo mật khóa API | Supabase Edge (Deno) | 🔴 Cao |
| **Chữ Ký Ví** | Xác minh mật mã | Solana Wallet Adapter | 🟡 Trung Bình |
| **Sao Lưu IPFS/Arweave** | Tính bất biến phi tập trung | IPFS SDK + Pinata | 🟢 Thấp |
| **Quy Trình Hủy Bỏ** | Hủy bỏ chứng chỉ giả | Cập nhật lược đồ DB | 🔴 Cao |
| **Nhật Ký Xem Xét** | Bản ghi điều tra khoa học | Bảng bản ghi đặc biệt | 🟡 Trung Bình |
| **OpenTimestamps** | Neo Bitcoin | OTS JavaScript | 🟢 Thấp |
| **Tích Hợp DID** | Danh tính phi tập trung | ION/Ceramic | 🟢 Thấp |

### Giai Đoạn 3: Phi Tập Trung Hoàn Toàn (Dài Hạn)

| Tính Năng | Mục Tiêu | ETA |
|---------|------|-----|
| **Sổ Đăng Ký Blockchain** | Đăng ký on-chain Ethereum/Solana | Q4 2026 |
| **Quản Trị DAO** | Quản trị cộng đồng | Q1 2027 |
| **Hỗ Trợ Đa Chuỗi** | Polygon, Arbitrum, Base | Q2 2027 |
| **Công Nhận Pháp Lý** | Tính hợp lệ tại tòa án Thổ Nhĩ Kỳ | 2027-2028 |
| **API cho Developer** | Điểm cuối API công khai | Q3 2026 |

---

## 📊 Phân Tích Đối Thủ (Đã Cập Nhật)

PoArt đứng ở "Sweet Spot" trong khi lấp đầy khoảng trống của các giải pháp hiện tại.

| Tính Năng | **PoArt** | OpenTime-stamps | Verisart / Artory | Origin-Stamp | Myco | Chroni-cled | 證 Proof | Trust-Stamp |
|---------|:---------:|:---------------:|:-----------------:|:------------:|:----:|:-----------:|:--------:|:-----------:|
| **Chi Phí** | 🆓 Miễn phí | 🆓 | 💰 Trả phí | ⚠️ Freemium | 💰 | 💰 | 💰 | 💰 |
| **UI Kéo & Thả** | ✅ Rất dễ | ❌ CLI | ⚠️ Trung bình | ⚠️ Trung bình | ⚠️ | ⚠️ | ❌ | ⚠️ |
| **Xuất Đa Định Dạng** | ✅ PNG/PDF/JSON | ❌ | ⚠️ PDF | ⚠️ PDF | ❌ | ❌ | ❌ | ⚠️ |
| **Xem Trước Thời Gian Thực** | ✅ Trực tiếp | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Kiểm Soát Quyền Riêng Tư** | ✅ 3 chế độ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Hash Phía-Khách Hàng** | ✅ Quyền riêng tư | ✅ | ❌ Tải lên | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| **Metadata Pháp Y** | ✅ Đầy đủ | ❌ | ❌ | ⚠️ Hạn chế | ❌ | ⚠️ | ❌ | ⚠️ |
| **Xác Minh QR** | ✅ Tức thì | ❌ | ✅ | ✅ | ⚠️ | ✅ | ⚠️ | ✅ |
| **Giới Hạn Tốc Độ** | ✅ RLS+khách hàng | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ | ⚠️ |
| **Neo Blockchain** | 🔄 Lộ trình | ✅ Bitcoin | ✅ Ethereum | ✅ Đa | ✅ | ✅ | ✅ | ✅ |
| **Mã Nguồn Mở** | ✅ GitHub | ✅ | ❌ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| **Hỗ Trợ Tiếng Việt** | ✅ Bản địa | ❌ | ❌ | ❌ | ❌ | ❌ | ⚠️ | ❌ |

**Chú Thích:**
- ✅ : Hỗ trợ đầy đủ / có sẵn
- ⚠️ : Hạn chế / trong gói trả phí
- ❌ : Không có / không được hỗ trợ
- 🔄 : Trong lộ trình (đang phát triển)
- 🆓 : Hoàn toàn miễn phí
- 💰 : Trả phí / cần đăng ký

---

**Giao Thức [PoArt] Bằng Chứng Nghệ Thuật v1.0**  
*"Văn Hóa > Vốn"*

## 🧾 Giấy Phép

Giấy phép MIT © 2026 Ilhan Art Gallery Initiative

Để biết các điều khoản đầy đủ, xem [![Giấy phép](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)](https://github.com/galeri-coder/galeri-coder.github.io/blob/main/LICENSE).

---

## 💬 Lời Cảm Ơn

![Phiên bản](https://img.shields.io/badge/version-v1.0_Beta-blue?style=for-the-badge) ![Bảo mật](https://img.shields.io/badge/security-Forensic_Standard-success?style=for-the-badge) ![Nền tảng](https://img.shields.io/badge/platform-Web_%2F_Serverless-orange?style=for-the-badge) ![Giấy phép](https://img.shields.io/badge/license-MIT-lightgrey?style=for-the-badge)

**Dự án này được phát triển bởi sáng kiến [Ilhan Art Gallery], và mã nguồn của nó có sẵn công khai vì lý do minh bạch.**

**Giao Thức V1.0 // Được Niêm Phong Với SHA-512**

*© 2026 İLHAN ART | Bảo lưu mọi quyền đối với tác phẩm nghệ thuật, hình ảnh và ý tưởng.*

---
