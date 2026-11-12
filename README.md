# PHÂN TÍCH: LỰA CHỌN ZERO-SHOT VS FEW-SHOT TRONG LỌC PHẢN HỒI KHÁCH HÀNG

## BƯỚC 1: THIẾT KẾ 2 PHƯƠNG ÁN PROMPT

### 1. Phương án 1 – Zero-shot Prompt

**Prompt:**

Bạn là nhân viên phân loại phản hồi khách hàng của cửa hàng.

Hãy phân loại tin nhắn khách hàng vào đúng một trong ba nhóm:

- TÍCH CỰC: Khách khen sản phẩm ngon, giá rẻ.
- TIÊU CỰC: Khách phàn nàn giao hàng chậm hoặc thái độ phục vụ tệ.
- CẦN HỖ TRỢ: Khách hỏi địa chỉ cửa hàng hoặc hỏi giá.

Yêu cầu:
- Đọc và hiểu ý nghĩa toàn bộ câu.
- Không chỉ dựa vào từ ngữ riêng lẻ.
- Chú ý phát hiện câu mỉa mai.
- Chỉ trả về tên nhóm phân loại.

Tin nhắn khách hàng: "Quán phục vụ chu đáo quá, bắt khách đợi hẳn 1 tiếng!"

### 2. Phương án 2 – Few-shot Prompt

**Prompt:**

Bạn là nhân viên phân loại phản hồi khách hàng của cửa hàng.

Hãy phân loại tin nhắn vào một trong ba nhóm: TÍCH CỰC, TIÊU CỰC, CẦN HỖ TRỢ.

**Ví dụ mẫu:**

Ví dụ 1:
- Tin nhắn: "Đồ ăn rất ngon, giá cả lại hợp lý!"
- Kết quả: TÍCH CỰC.
- Lý do: Khách hàng khen chất lượng và giá sản phẩm.

Ví dụ 2:
- Tin nhắn: "Giao hàng quá chậm, nhân viên còn có thái độ không tốt!"
- Kết quả: TIÊU CỰC.
- Lý do: Khách hàng phàn nàn về giao hàng và thái độ phục vụ.

Ví dụ 3:
- Tin nhắn: "Quán phục vụ chu đáo quá, bắt khách đợi hẳn 1 tiếng!"
- Kết quả: TIÊU CỰC.
- Lý do: Đây là câu mỉa mai, khách hàng thực chất đang phàn nàn vì phải chờ đợi quá lâu.

**Yêu cầu:**
- Phân tích ý nghĩa toàn bộ câu, không chỉ dựa vào từ khóa.
- Nhận diện ngữ cảnh và câu mỉa mai.
- Phân loại theo các ví dụ mẫu.
- Chỉ trả về tên nhóm phân loại.

Tin nhắn cần phân loại: "Quán phục vụ chu đáo quá, bắt khách đợi hẳn 1 tiếng!"

## BƯỚC 2: BẢNG SO SÁNH TRADE-OFF

| Tiêu chí | Zero-shot | Few-shot |
|---|---|---|
| Độ dễ hiểu | Cao, dễ viết nhanh | Trung bình, cần chuẩn bị ví dụ |
| Tốn Token | Ít Token hơn | Nhiều Token hơn |
| Xử lý câu mỉa mai | Dễ nhầm nếu không có ví dụ | Tốt hơn nhờ ví dụ mẫu |
| Tốc độ xây dựng prompt | Nhanh | Chậm hơn |
| Độ nhất quán | Có thể thay đổi giữa các trường hợp | Thường nhất quán hơn nếu ví dụ tốt |
| Khả năng mở rộng | Dễ bổ sung quy tắc | Cần bổ sung ví dụ tương ứng |

## BƯỚC 3: THỬ NGHIỆM THỰC TẾ

**Tin nhắn kiểm thử:**

"Quán phục vụ chu đáo quá, bắt khách đợi hẳn 1 tiếng!"

| Phương án | Kết quả phân loại | Đánh giá |
|---|---|---|
| Zero-shot | TÍCH CỰC (có thể xảy ra nếu AI hiểu sai từ ngữ) | Chưa đáng tin cậy khi gặp câu mỉa mai |
| Few-shot | TIÊU CỰC | Chính xác theo ngữ cảnh và ví dụ mẫu |

**Kết quả:** Few-shot phù hợp hơn với bài toán phân loại phản hồi khách hàng MartX vì có ví dụ mẫu giúp AI nhận diện câu mỉa mai và hiểu đúng ý định của khách hàng.

## KẾT LUẬN

Zero-shot phù hợp với nhiệm vụ đơn giản, quy tắc rõ ràng và cần tiết kiệm Token. Few-shot phù hợp với nhiệm vụ có nhiều tình huống đặc biệt, cần tăng tính nhất quán và xử lý ngữ cảnh như câu mỉa mai.

Đối với MartX, nên ưu tiên Few-shot để nâng cao độ chính xác trong phân loại phản hồi khách hàng.
