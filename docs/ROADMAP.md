# Lộ trình thực hiện

Theo kế hoạch gốc: 12/10/2026–20/12/2026, nhóm 4 sinh viên. Bảng này mô tả công việc dự kiến; chưa đánh dấu hoàn thành dựa trên ngày lịch.

| Tuần | Thời gian | Công việc và sản phẩm dự kiến |
| --- | --- | --- |
| 1 | 12–18/10/2026 | Khảo sát, chốt phạm vi/use case, ma trận quyền, tám ý định và đề cương thực nghiệm. |
| 2 | 19–25/10/2026 | Wireframe, ERD, kiến trúc, hợp đồng Java–Python; khởi tạo ba thành phần, migration, đăng nhập và phân quyền. |
| 3 | 26/10–01/11/2026 | Tổ chức, lớp/học sinh, phân công, liên kết phụ huynh; tin/tài liệu và gửi duyệt; truy xuất có metadata quyền. |
| 4 | 02–08/11/2026 | Chuyên cần, xin phép, lịch; tích hợp chat RAG có nguồn và bộ 240 câu hỏi phiên bản đầu. |
| 5 | 09–15/11/2026 | Điểm, thư viện, đăng ký/yêu cầu; hoàn thiện 1.200 mẫu và 120 câu ngoài phạm vi, huấn luyện baseline. |
| 6 | 16–22/11/2026 | Dashboard, lịch đăng, thông báo, tích hợp nội dung–AI; chạy thử learner 1/4/8 và kiểm tra giữa kỳ. |
| 7 | 23–29/11/2026 | Đề xuất phòng ban trên biểu mẫu, duyệt phản hồi, phiên bản dataset/checkpoint, rollback, tóm tắt và soạn nháp. |
| 8 | 30/11–06/12/2026 | Chạy đối chứng với ba seed; đánh giá RAG, phân quyền, forgetting, thời gian và bộ nhớ; phân tích kết quả. |
| 9 | 07–13/12/2026 | Kiểm thử xuyên suốt và tải, sửa lỗi, kiểm tra backup/restore, giao diện di động, Docker Compose và hướng dẫn. |
| 10 | 14–20/12/2026 | Đóng băng tính năng, nghiệm thu demo, đóng gói source/dữ liệu, hoàn thiện báo cáo, slide, video và hồ sơ nộp. |

Mốc giữa kỳ theo kế hoạch: **22/11/2026**. Sau tuần 8 ưu tiên kiểm thử, báo cáo và demo.

## Phân công dự kiến

| Thành viên theo phiếu | Trách nhiệm chính |
| --- | --- |
| TV1 | Java nền tảng: tài khoản, quyền, tổ chức, nội dung và API tích hợp; phối hợp database và triển khai. |
| TV2 | Java nghiệp vụ: học sinh/lớp, chuyên cần, điểm, lịch, thư viện và yêu cầu; phối hợp dữ liệu demo. |
| TV3 | React/Vite: cổng công khai, dashboard, biểu mẫu, chat và quản trị AI; kiểm thử giao diện. |
| TV4 | Python: ingestion, RAG, learner đa nhịp, đối chứng, dữ liệu và đánh giá nghiên cứu. |

Tên thành viên sẽ cập nhật theo phân công thực tế. Cả nhóm cùng kiểm tra dữ liệu, tích hợp hằng tuần và viết báo cáo phần phụ trách.

## Bộ sản phẩm nghiệm thu

- Mã nguồn React, Java và Python; migration, dữ liệu demo, cấu hình mẫu và Docker Compose.
- Đặc tả yêu cầu, use case, ERD, kiến trúc và hợp đồng API.
- Hướng dẫn triển khai và sử dụng theo vai trò.
- Corpus, dataset định tuyến, bộ câu hỏi, checkpoint và cấu hình thí nghiệm.
- Kết quả/biểu đồ nghiên cứu, biên bản kiểm thử, backup/restore và danh sách hạn chế.
- Báo cáo đồ án, slide, video demo và phiếu tiến độ để GVHD xác nhận.
