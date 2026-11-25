# Bộ Câu Hỏi & Trả Lời Bảo Vệ Dự Án (Bản Dễ Hiểu – Dễ Thuộc)

Tài liệu này tổng hợp **32 câu hỏi thường gặp nhất** khi bảo vệ đồ án **Hệ thống Quản lý Đào tạo & Đăng ký Học phần (UniCourse / Aetheria)**.  
Mỗi câu đều chia 2 phần:
- **Trả lời nhanh (1–2 câu):** Ngắn gọn, tự nhiên để nói trôi chảy ngay khi thầy/cô hỏi.
- **Nói thêm nếu bị hỏi sâu:** Ý chi tiết vừa đủ, dùng ngôn ngữ đời thường, tránh thuật ngữ khó nhớ.

---

## Phần 1: Tổng quan dự án & Công nghệ

### Câu 1: Dự án của em làm về gì và giải quyết vấn đề gì?
- **Trả lời nhanh:** Dạ dự án của em là hệ thống quản lý đào tạo và đăng ký học phần trực tuyến cho trường đại học, giúp sinh viên đăng ký môn, giảng viên nhập điểm và phòng đào tạo quản lý toàn bộ quy trình trên một nền tảng thống nhất.
- **Nói thêm nếu bị hỏi sâu:** Hệ thống thay thế việc quản lý rời rạc bằng Excel/giấy tờ, tự động kiểm tra các lỗi hay gặp khi đăng ký môn như trùng lịch, thiếu môn tiên quyết, quá tín chỉ hay hết chỗ, giúp giảm tải cho phòng đào tạo và hạn chế sai sót.

### Câu 2: Hệ thống có mấy vai trò người dùng? Mỗi vai trò làm được gì?
- **Trả lời nhanh:** Dạ có 3 vai trò chính là **Sinh viên**, **Giảng viên** và **Quản trị viên (Phòng Đào tạo)**.
- **Nói thêm nếu bị hỏi sâu:**
  - **Sinh viên:** Xem tổng quan tín chỉ/GPA, lập kế hoạch môn dự kiến, đăng ký/hủy học phần, xem thời khóa biểu, xem điểm, điểm danh, phúc khảo điểm, xuất bảng điểm PDF và hỏi Trợ lý AI.
  - **Giảng viên:** Xem lớp mình phụ trách, điểm danh sinh viên, gửi thông báo nghỉ học/lớp học, nhập điểm (hoặc import file Excel) và gửi duyệt bảng điểm, xem thống kê điểm của lớp.
  - **Quản trị viên:** Quản lý khoa, ngành, môn học, phòng học, học kỳ, đợt đăng ký; mở/hủy lớp học phần; duyệt và công bố bảng điểm; quản lý tài khoản sinh viên/giảng viên; xem biểu đồ thống kê và nhật ký hệ thống.

### Câu 3: Điểm nổi bật của hệ thống so với một web đăng ký môn học cơ bản là gì?
- **Trả lời nhanh:** Ngoài đăng ký môn và nhập điểm cơ bản, hệ thống có thêm các tính năng thực tế như chống đăng ký vượt sĩ số khi nhiều người bấm cùng lúc, quy trình duyệt bảng điểm nhiều bước, cảnh báo học tập sớm, xuất bảng điểm PDF có mã xác thực chống giả mạo và Trợ lý AI tra cứu dữ liệu thật của từng tài khoản.
- **Nói thêm nếu bị hỏi sâu:** Hệ thống còn có nhật ký theo dõi thao tác (Audit Log), phát hiện hành vi bất thường (như đăng nhập sai nhiều lần hoặc hủy môn hàng loạt) và chạy kiểm thử tự động từ code đến giao diện trên GitHub Actions.

### Câu 4: Dự án sử dụng những công nghệ gì? Vì sao chọn bộ công nghệ đó?
- **Trả lời nhanh:** Backend dùng **Java 21 + Spring Boot 3.4**, Frontend dùng **React 18 + Tailwind CSS**, cơ sở dữ liệu là **MySQL 8.4**, đóng gói bằng **Docker** và kiểm thử tự động bằng **GitHub Actions**.
- **Nói thêm nếu bị hỏi sâu:**
  - **Spring Boot:** Mạnh về xử lý nghiệp vụ, bảo mật (Spring Security + JWT) và quản lý giao dịch dữ liệu (Transaction) rất ổn định cho bài toán đăng ký môn.
  - **React + Vite + Tailwind CSS:** Giao diện mượt, chuyển trang nhanh, dễ làm responsive trên cả máy tính và điện thoại.
  - **MySQL:** Phù hợp dữ liệu có cấu trúc chặt chẽ như sinh viên, môn học, lớp, điểm số và hỗ trợ khóa dữ liệu tốt khi nhiều người đăng ký cùng lúc.
  - **Docker:** Giúp chạy giống hệt nhau trên máy cá nhân và trên server, không bị lỗi "máy em chạy được mà máy thầy không chạy".

### Câu 5: Kiến trúc tổng thể hệ thống chạy như thế nào?
- **Trả lời nhanh:** Hệ thống chạy theo mô hình Client–Server tách biệt: người dùng mở trình duyệt vào Frontend (React), mọi yêu cầu dữ liệu được gửi qua API (JSON) về Backend (Spring Boot) xử lý rồi lưu xuống MySQL.
- **Nói thêm nếu bị hỏi sâu:** Khi triển khai bằng Docker Compose, có 3 container chính: **Nginx/Frontend** phục vụ giao diện web và chuyển tiếp các đường dẫn `/api` sang **Backend**, còn Backend kết nối vào container **MySQL** để đọc/ghi dữ liệu.

---

## Phần 2: Nghiệp vụ Đăng ký học phần & Xử lý đồng thời

### Câu 6: Khi sinh viên bấm "Đăng ký" một lớp học phần, hệ thống kiểm tra những gì?
- **Trả lời nhanh:** Hệ thống kiểm tra 6 điều kiện: trạng thái học vụ của sinh viên, đúng thời gian/đợt đăng ký, chưa đăng ký trùng môn đó, không trùng lịch học với môn khác, đã qua môn tiên quyết, lớp còn chỗ và không vượt quá số tín chỉ tối đa của học kỳ.
- **Nói thêm nếu bị hỏi sâu:** Trên giao diện, hệ thống kiểm tra trước (pre-check) để báo rõ lý do bị chặn ngay trên từng dòng lớp học phần cho sinh viên biết, còn ở Backend vẫn kiểm tra lại lần nữa trước khi lưu vào database để đảm bảo an toàn tuyệt đối.

### Câu 7: Nếu 50 sinh viên cùng bấm đăng ký vào 1 lớp chỉ còn đúng 1 chỗ cuối cùng thì xử lý thế nào?
- **Trả lời nhanh:** Dạ em dùng cơ chế **khóa bi quan (khóa dòng dữ liệu trong database)** khi xử lý đăng ký, bắt các yêu cầu vào cùng một lớp phải xếp hàng xử lý lần lượt từng người một.
- **Nói thêm nếu bị hỏi sâu:** Người đầu tiên vào sẽ khóa dòng dữ liệu của lớp đó lại, kiểm tra thấy còn 1 chỗ, ghi nhận đăng ký và trừ chỗ về 0 rồi mới mở khóa. 49 người xếp hàng phía sau khi được mở khóa sẽ thấy sĩ số đã đầy (`conLai = 0`) nên nhận thông báo "Lớp đã đủ sĩ số", tuyệt đối không bao giờ bị âm chỗ hay vượt sĩ số. Nhóm cũng đã viết script giả lập 50 request đồng thời để kiểm chứng cơ chế này.

### Câu 8: Hệ thống kiểm tra trùng lịch học như thế nào?
- **Trả lời nhanh:** Mỗi lớp có thông tin **Thứ**, **Tiết bắt đầu** và **Số tiết** (từ đó suy ra tiết kết thúc). Khi đăng ký lớp mới, hệ thống so với tất cả các lớp sinh viên đã đăng ký trong cùng học kỳ: nếu cùng Thứ và khoảng tiết bị giao nhau thì báo trùng lịch.

### Câu 9: Môn tiên quyết, học lại và học cải thiện được xử lý ra sao?
- **Trả lời nhanh:** Nếu môn A yêu cầu phải qua môn B trước (tiên quyết), sinh viên chưa có điểm đạt (>= 5.0) môn B thì không đăng ký được môn A. Nếu sinh viên đã học một môn rồi, điểm dưới 5.0 thì được xếp vào diện **học lại**, còn từ 5.0 trở lên mà muốn nâng điểm thì đăng ký **học cải thiện**.

### Câu 10: Khi sinh viên hủy đăng ký môn học, hệ thống có quy tắc gì?
- **Trả lời nhanh:** Chỉ được hủy khi đang trong thời gian mở đăng ký/hủy; khi hủy thành công, hệ thống cộng trả lại 1 chỗ trống cho lớp và ghi nhận lịch sử hủy kèm lý do (nếu có).
- **Nói thêm nếu bị hỏi sâu:** Hệ thống còn kiểm tra quy tắc tín chỉ tối thiểu: sinh viên có thể hủy hết toàn bộ môn (về 0 tín chỉ), hoặc giữ tổng tín chỉ không thấp hơn mức tối thiểu quy định của học kỳ.

### Câu 11: Chức năng "Kế hoạch học tập (Giỏ dự kiến)" dùng để làm gì?
- **Trả lời nhanh:** Nó giống như "giỏ hàng" trước khi thanh toán: sinh viên chọn thử các lớp vào giỏ để xem trước thời khóa biểu dự kiến và tổng số tín chỉ có bị trùng hay vượt giới hạn không, ưng ý rồi mới bấm xác nhận đăng ký thật.

### Câu 12: Quản trị viên có thể chia đợt đăng ký theo đối tượng không?
- **Trả lời nhanh:** Có ạ. Phòng đào tạo có thể tạo nhiều đợt đăng ký trong cùng một học kỳ, giới hạn theo **tất cả sinh viên**, theo **khóa học**, theo **ngành**, hoặc theo **lớp hành chính**, và có thể gia hạn hoặc đóng sớm khi cần.

---

## Phần 3: Điểm số, Phê duyệt & Cảnh báo học vụ

### Câu 13: Quy trình nhập điểm của giảng viên đến khi sinh viên xem được điểm gồm mấy bước?
- **Trả lời nhanh:** Dạ gồm 5 trạng thái nối tiếp nhau: **Nhập nháp** → **Chờ duyệt** → **Đã duyệt** → **Công bố** → **Khóa**. Sinh viên chỉ nhìn thấy điểm chính thức khi bảng điểm đã ở trạng thái **Công bố** hoặc **Khóa**.
- **Nói thêm nếu bị hỏi sâu:** Giảng viên nhập điểm trên web hoặc import từ file Excel rồi bấm "Gửi duyệt". Phòng đào tạo kiểm tra nếu sai thì "Trả về" để giảng viên sửa lại; nếu đúng thì bấm "Phê duyệt" và "Công bố" cho sinh viên xem, sau đó "Khóa" lại để không ai tự ý sửa điểm được nữa (muốn sửa phải mở khóa có lý do và được ghi log).

### Câu 14: Vì sao phải làm quy trình duyệt điểm nhiều bước như vậy mà không cho giảng viên nhập xong là sinh viên thấy luôn?
- **Trả lời nhanh:** Để đảm bảo tính chính xác và minh bạch trong đào tạo: tránh trường hợp giảng viên mới nhập nháp một nửa hoặc nhập nhầm đã lộ ra cho sinh viên, đồng thời có khâu kiểm soát của Phòng Đào tạo trước khi công bố chính thức.

### Câu 15: Điểm tổng kết, điểm đạt và GPA tính như thế nào?
- **Trả lời nhanh:** Điểm tổng kết thang 10 tính từ điểm quá trình và điểm cuối kỳ; mức điểm đạt mặc định là **5.0**. Từ điểm thang 10 hệ thống quy đổi sang thang 4 (A, B, C, D, F) để tính GPA trung bình theo số tín chỉ của từng môn.

### Câu 16: Chức năng Phúc khảo điểm hoạt động thế nào?
- **Trả lời nhanh:** Sau khi bảng điểm được công bố và còn trong thời hạn phúc khảo, sinh viên có thể gửi đơn phúc khảo kèm lý do. Phòng đào tạo xem danh sách đơn, xử lý duyệt hoặc từ chối và cập nhật lại kết quả cho sinh viên.

### Câu 17: Cảnh báo học tập sớm hoạt động như thế nào?
- **Trả lời nhanh:** Hệ thống có bộ quy tắc tự động quét dữ liệu để phát hiện sớm sinh viên có nguy cơ: điểm quá trình thấp, nghỉ học quá nhiều buổi, GPA tụt giảm hoặc tiến độ tích lũy tín chỉ chậm, từ đó hiển thị nhắc nhở để sinh viên và giảng viên kịp thời cải thiện.
- **Nói thêm nếu bị hỏi sâu:** Cảnh báo này chỉ mang tính nhắc nhở và hỗ trợ, tuyệt đối không tự ý khóa tài khoản hay đổi trạng thái học tập của sinh viên.

### Câu 18: Bảng điểm xác thực (Verifiable Transcript) chống làm giả bằng cách nào?
- **Trả lời nhanh:** Khi xuất bảng điểm chính thức, hệ thống tạo một phiên bản snapshot dữ liệu kèm **mã xác thực** và mã/link tra cứu công khai. Người ngoài (như nhà tuyển dụng) chỉ cần vào trang xác thực nhập mã là kiểm tra được bảng điểm đó có đúng là bản thật do trường cấp và còn hiệu lực hay không.

---

## Phần 4: Bảo mật, Phân quyền & Giám sát hệ thống

### Câu 19: Hệ thống đăng nhập và phân quyền hoạt động như thế nào?
- **Trả lời nhanh:** Khi đăng nhập đúng tài khoản/mật khẩu, server tạo một chuỗi **JWT Token** (chứa thông tin người dùng và vai trò) trả về cho trình duyệt. Các lần gọi API sau, trình duyệt gửi kèm token này, Backend kiểm tra token hợp lệ và đúng vai trò mới cho thực hiện.
- **Nói thêm nếu bị hỏi sâu:** Mọi API đều chặn theo vai trò (ví dụ sinh viên cố tình gọi API nhập điểm của giảng viên hoặc API quản trị của Admin thì bị server trả lỗi `403 Forbidden` ngay).

### Câu 20: Mật khẩu người dùng được lưu trong database như thế nào?
- **Trả lời nhanh:** Mật khẩu được băm một chiều bằng thuật toán **BCrypt**, tuyệt đối không lưu mật khẩu dạng chữ thường trong database. Khi đổi mật khẩu phải nhập đúng mật khẩu cũ mới cho đổi.

### Câu 21: Tính năng "đăng nhập 1 nơi tại một thời điểm" (phiên đơn) hoạt động ra sao?
- **Trả lời nhanh:** Mỗi tài khoản lưu một mã phiên đăng nhập mới nhất. Nếu tài khoản đang đăng nhập ở máy A mà có người đăng nhập ở máy B, mã phiên mới sẽ ghi đè mã cũ, khiến máy A khi thao tác tiếp sẽ bị đẩy ra màn hình đăng nhập với thông báo "Tài khoản đã được đăng nhập ở nơi khác".

### Câu 22: Nếu Admin khóa tài khoản của một sinh viên đang đăng nhập thì chuyện gì xảy ra?
- **Trả lời nhanh:** Sinh viên đó bị chặn ngay lập tức ở request tiếp theo, không cần phải đợi JWT token hết hạn.
- **Nói thêm nếu bị hỏi sâu:** Bình thường JWT chỉ hết hạn sau 24 giờ, nên để khắc phục nhược điểm đó, Backend kiểm tra thêm trạng thái hoạt động của tài khoản (kết hợp bộ nhớ đệm **Caffeine Cache** để tra cực nhanh mà không làm chậm database).

### Câu 23: Hệ thống chống spam hoặc dò mật khẩu (brute-force) bằng cách nào?
- **Trả lời nhanh:** Hệ thống áp dụng **giới hạn tần suất gọi API (Rate Limiting)**, đặc biệt cho đường dẫn đăng nhập và chat AI. Nếu một địa chỉ IP gửi quá số lượt cho phép trong 1 phút sẽ bị tạm chặn và trả lỗi quá nhiều yêu cầu (`429 Too Many Requests`).

### Câu 24: Nhật ký hoạt động (Audit Log) và Cảnh báo Audit dùng để làm gì?
- **Trả lời nhanh:** Mọi thao tác quan trọng (tạo/sửa/xóa lớp, duyệt/mở khóa điểm, khóa tài khoản, đăng nhập thất bại...) đều được server tự động ghi lại (ai làm, lúc nào, thay đổi từ giá trị cũ sang giá trị mới là gì) và không ai sửa xóa được. Nếu phát hiện bất thường (như đăng nhập sai liên tục hoặc hủy đăng ký hàng loạt), hệ thống tự tạo cảnh báo Audit cho Admin kiểm tra.

---

## Phần 5: Trợ lý AI, Thông báo & Tác vụ nền

### Câu 25: Trợ lý AI trong hệ thống hoạt động thế nào? Có sợ AI trả lời bừa không?
- **Trả lời nhanh:** Trợ lý AI hỗ trợ hỏi đáp bằng tiếng Việt theo đúng vai trò đang đăng nhập (xem lịch học/lịch dạy hôm nay, tìm lớp còn chỗ, kiểm tra điều kiện đăng ký...). Dữ liệu AI trả lời được lấy trực tiếp từ database thật của chính người dùng đó, chứ không cho AI tự bịa số liệu.
- **Nói thêm nếu bị hỏi sâu:** AI không bao giờ được tự ý thay mặt sinh viên bấm đăng ký hay hủy môn làm thay đổi dữ liệu ngầm; nếu người dùng muốn đăng ký qua chat thì hệ thống chỉ kiểm tra điều kiện và hướng dẫn rõ ràng.

### Câu 26: Hệ thống Thông báo hoạt động thế nào và tránh gửi trùng ra sao?
- **Trả lời nhanh:** Khi có sự kiện như đăng ký thành công, hủy lớp, nghỉ học hoặc công bố điểm, hệ thống tạo thông báo hiện trên chuông thông báo của người dùng (và hỗ trợ gửi email nếu cấu hình). Mỗi thông báo gắn một khóa chống trùng (`idempotency key`) để dù có bấm lặp lại hay chạy lại job cũng không gửi 2 lần giống nhau.

### Câu 27: Hệ thống có các tác vụ tự động chạy ngầm không?
- **Trả lời nhanh:** Có ạ. Ví dụ tác vụ tự động kiểm tra các đợt đăng ký sắp đóng để gửi thông báo nhắc sinh viên, hoặc cơ chế thử lại (retry) khi gửi email thất bại, và có khóa phân tán để tránh 2 server chạy trùng một job.

---

## Phần 6: Kiểm thử, CI/CD, Triển khai & Hướng phát triển

### Câu 28: Nhóm đã kiểm thử hệ thống bằng những cách nào?
- **Trả lời nhanh:** Nhóm kiểm thử đủ 4 lớp: **Unit/Integration Test** cho Backend (JUnit 5 + Mockito), **E2E Test** tự động bấm giao diện trình duyệt (Playwright), **Load Test** giả lập nhiều người dùng đồng thời (Node.js) và **kiểm thử thủ công/QA** đầy đủ cả 3 vai trò Sinh viên – Giảng viên – Admin.
- **Nói thêm nếu bị hỏi sâu:** Nhờ kiểm thử kỹ cả 3 vai trò trên môi trường chạy thật, nhóm đã phát hiện và sửa được các lỗi thực tế như: lỗi 500 khi kiểm tra điều kiện các học kỳ cũ (`UnexpectedRollbackException`), lỗi sai múi giờ UTC so với giờ Việt Nam, lỗi gọi trùng tiền tố API, phân trang bảng 500 sinh viên để không lag trình duyệt, v.v.

### Câu 29: Quy trình CI/CD của dự án chạy những gì?
- **Trả lời nhanh:** Mỗi khi nhóm đẩy code hoặc merge vào nhánh `dev`/`main`, **GitHub Actions** tự động chạy 3 bước:
  1. Build và chạy toàn bộ test Backend.
  2. Build bản production Frontend.
  3. Khởi động hệ thống và chạy bộ test giao diện E2E bằng Playwright.
  Tất cả phải xanh hết thì mới đảm bảo code an toàn để đóng gói Docker image và triển khai.

### Câu 30: Nếu muốn chạy dự án trên máy khác hoặc triển khai lên server thì làm thế nào?
- **Trả lời nhanh:** Chỉ cần cài Docker, tạo file `.env` từ `.env.example` và chạy 1 lệnh `docker compose up --build` là cả MySQL, Backend và Frontend tự động dựng lên và kết nối với nhau. Có sẵn dữ liệu mẫu tự động nạp (khi `SEED_ENABLED=true`) để test ngay.

### Câu 31: Sao lưu và khôi phục dữ liệu (Backup & Restore) làm thế nào?
- **Trả lời nhanh:** Dữ liệu MySQL được lưu trong Docker Volume riêng để không bị mất khi tắt container, và có tài liệu hướng dẫn xuất file sao lưu (`mysqldump`) định kỳ để khôi phục lại nhanh chóng nếu gặp sự cố.

### Câu 32: Hạn chế hiện tại của dự án và hướng phát triển tiếp theo là gì?
- **Trả lời nhanh:**
  - **Hạn chế:** Chưa tích hợp cổng thanh toán học phí trực tuyến (hiện mới tập trung quản lý đào tạo & học phần), chưa có ứng dụng mobile riêng (mới tối ưu web responsive trên trình duyệt điện thoại), và việc gửi email thực tế phụ thuộc vào cấu hình SMTP của nhà trường.
  - **Hướng phát triển:** Bổ sung module tính và thanh toán học phí online, tích hợp đăng nhập một lần (SSO) của trường, và nâng cấp thông báo đẩy (push notification) trên mobile.
