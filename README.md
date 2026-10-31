# Website THPT Phan Văn Hớn với AGENT

Đồ án chuyên ngành Công nghệ phần mềm xây dựng hệ sinh thái nhà trường: cổng thông tin, quản trị phòng ban, học vụ, học sinh và phụ huynh; tích hợp trợ lý AI có dẫn nguồn và mô-đun nghiên cứu học đa nhịp lấy ý tưởng từ Nested Learning.

**Trạng thái:** khởi tạo repository và tài liệu kế hoạch. Chưa triển khai ứng dụng; chưa có lệnh chạy hoặc bản demo.

## Tài liệu dự án

- [Kế hoạch gốc](Ke_hoach_Website_THPT_Phan_Van_Hon_AI_10_tuan.docx)
- [Lộ trình 10 tuần và phân công](docs/ROADMAP.md)

Kế hoạch gốc là căn cứ cho phạm vi dưới đây. Mốc thời gian và công nghệ được ghi theo tài liệu, không phải xác nhận tiến độ thực tế hoặc kết quả kiểm thử tương thích.

## Phạm vi phiên bản đầu

- Cổng thông tin: giới thiệu, tổ chức, tin tức, thông báo, tuyển sinh, lịch công tác và liên hệ.
- Tài khoản, xác minh email, phân quyền theo vai trò và phạm vi dữ liệu.
- Phòng ban, tổ chuyên môn, năm học, lớp, hồ sơ học sinh và liên kết phụ huynh được xác minh.
- Điểm danh theo ngày/buổi, đơn xin phép vắng hoặc trễ, điểm số cơ bản và lịch học.
- Thư viện số, nhu cầu mượn sách, đăng ký hoạt động và tiếp nhận yêu cầu.
- Soạn, duyệt, lên lịch xuất bản nội dung; thông báo trong hệ thống và email.
- Dashboard, báo cáo và nhật ký các thay đổi quan trọng.
- Trợ lý hỏi đáp có nguồn, đề xuất phòng ban, tóm tắt và soạn bản nháp.
- Nghiên cứu định tuyến học đa nhịp, phản hồi có duyệt, đối chứng và đánh giá khả năng quên.

Các chức năng nhận diện khuôn mặt, học bạ/xếp loại, tự động xếp thời khóa biểu, thanh toán, SMS/Zalo và tích hợp hệ thống trường thật thuộc giai đoạn mở rộng.

## Kiến trúc dự kiến

```text
Trình duyệt → Nginx → React / Java API
                              │
                              ├── PostgreSQL + pgvector
                              ├── Redis / MinIO
                              └── Python AI API + worker
```

Frontend gọi API Java. Java triển khai dạng một ứng dụng chia module, chịu trách nhiệm xác thực, quyết định quyền và xử lý nghiệp vụ. Python phụ trách truy xuất tài liệu, hỏi đáp, đề xuất phòng ban và thực nghiệm; không trực tiếp sửa điểm, chuyên cần, tài khoản hoặc trạng thái hồ sơ.

| Thành phần | Công nghệ trong kế hoạch |
| --- | --- |
| Frontend | React 19, Vite 8, TypeScript; Node.js 22.12 trở lên |
| Giao diện | Ant Design, React Router, TanStack Query, React Hook Form |
| Backend | Java 21, Spring Boot 4.1.1, Maven |
| Nền tảng Java | Spring Security, Spring Data JPA, Bean Validation, Flyway |
| AI | Python 3.12, FastAPI, PyTorch, Sentence Transformers, scikit-learn |
| Dữ liệu | PostgreSQL 17, pgvector |
| Phiên và tác vụ | Redis, Spring Session, RQ |
| Lưu file | MinIO |
| Triển khai demo | Docker Compose, Nginx |

Khi triển khai mã nguồn, dự kiến tổ chức `frontend/`, `backend/`, `ai-service/` và `infra/` trong cùng repository. Các thành phần này chưa được khởi tạo.

## Trọng tâm nghiên cứu AI

Encoder cố định `sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2` tạo embedding 384 chiều. Ba MLP độc lập `384 → 128 → ReLU → 8` học theo nhịp 1, 4 và 8 minibatch, tổng hợp bằng trung bình xác suất. Đây là vận dụng rút gọn ý tưởng CMS, chưa tái hiện toàn bộ HOPE.

- Tám ý định: tuyển sinh; giáo vụ; chuyên cần; chuyên môn và điểm; thư viện; văn phòng; ban giám hiệu; tài khoản và kỹ thuật.
- Dataset mục tiêu: 1.200 mẫu có nhãn và 120 câu ngoài phạm vi; tách theo nhóm tình huống để tránh rò rỉ dữ liệu.
- Đối chứng: MLP cố định, một nhịp, replay, MLP gần tương đương số tham số, ba MLP nhịp 1/1/1, nhịp 1/4/8 và bỏ khối chậm.
- Chạy ba seed 42, 43, 44; đo macro-F1, kết quả nhóm cũ/mới, forgetting, độ trễ và dung lượng checkpoint.
- Trợ lý RAG được đánh giá riêng bằng 240 câu hỏi; corpus mục tiêu tối thiểu 40 tài liệu với ít nhất 10 cặp phiên bản thay đổi.

Kết quả nghiên cứu phải được đo và báo cáo trung thực; kế hoạch không cam kết cấu hình đa nhịp vượt mọi baseline.

## Quy tắc triển khai theo kế hoạch

- Phiên đăng nhập dùng cookie HttpOnly, Secure, SameSite và chống CSRF; Java xác minh phạm vi trước khi trả dữ liệu.
- Phụ huynh chỉ xem học sinh được xác nhận liên kết; giáo viên chỉ thao tác lớp/môn được giao.
- Nội dung phải được duyệt trước khi xuất bản hoặc đưa vào kho tri thức. Nguồn hết hiệu lực hoặc bị thu hồi phải bị chặn.
- Điểm số và chuyên cần có kiểm tra phiên bản, nhật ký và lý do chỉnh sửa.
- AI đề xuất; người có quyền xác nhận nghiệp vụ. Phản hồi chỉ trở thành dữ liệu học sau khi duyệt.
- Dữ liệu demo dùng dữ liệu tổng hợp hoặc tài liệu phù hợp; không đưa hồ sơ học sinh thật vào repo hay corpus chung.
- API key đặt ở dịch vụ Python. Không commit secret, file `.env`, dữ liệu vận hành hoặc checkpoint lớn.
- Scheduler dùng múi giờ `Asia/Ho_Chi_Minh`.

## Kiểm thử dự kiến

Java dùng JUnit/Testcontainers; Python dùng pytest; frontend dùng Vitest/Playwright. Các nhóm nghiệm thu gồm phân quyền, quy trình duyệt, chống ghi đè, lịch đăng, nguồn AI, lỗi tích hợp và sao lưu/khôi phục.

Hiện repo chỉ có tài liệu nên chưa có bộ kiểm thử ứng dụng hoặc cấu hình CI.
