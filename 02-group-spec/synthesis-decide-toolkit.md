# Toolkit — Từ Evidence Đến Build Slice

Dùng sau khi nhóm đã có evidence. Mục tiêu là chốt một build slice đủ nhỏ cho Day 06.

## 1. Gom evidence thành cụm

Gom theo **workflow/pain**, không gom theo tên feature.

- **"Sợ thành phần ẩn"**: Người dùng không thể tự biết liệu nước dùng có pha xương vịt, tôm hay hải sản để làm ngọt hay không. Ví dụ: Bún Thang dùng gà/nước dùng gà (an toàn cho dị ứng vịt) nhưng Miến Măng Vịt lại dùng thịt/nước dùng vịt (nguy hiểm). Các loại gia vị bản địa (nước mắm, tôm khô) thường bị ẩn trong nước sốt mà mắt thường không nhìn thấy được.
- **"Quá tải thông tin"**: Một menu có tới hàng chục đến hàng trăm món. Người dùng phải đi hỏi ChatGPT từng món một ("Bún thang có vịt không?", "Cháo sườn có thành phần gì?") rồi tự tổng hợp. Việc tra cứu thủ công 1-1 này mất cả buổi tối và cực kỳ phiền phức khi đứng trực tiếp tại quán ăn.
- **"Rào cản ngôn ngữ và văn hóa"**: Khách du lịch nước ngoài không biết tiếng Việt để hỏi bồi bàn, hoặc bồi bàn/phục vụ không hiểu rõ độ nghiêm trọng của dị ứng chéo hay các thành phần ngầm, dẫn đến rủi ro giao tiếp rất cao.

## 2. Viết insight

Form:

```text
User [khách du lịch bị dị ứng thực phẩm] không chỉ cần [dịch menu hay biết tên món ăn bằng tiếng Anh].
Họ thật ra cần [sự an tâm tuyệt đối và hỗ trợ ra quyết định ẩm thực siêu tốc, an toàn khi đứng trước một menu xa lạ],
vì [họ luôn thường trực nỗi sợ về các thành phần ẩn nguy hại và việc tự tra cứu thủ công từng món qua ChatGPT là quá mất thời gian, không hiệu quả trong thực tế].
```

## 3. Viết opportunity

Form:

```text
Cơ hội là dùng AI để [tự động hóa việc phân tích thành phần món ăn (nước dùng, gia vị, chất dị ứng) và so khớp với hồ sơ dị ứng cá nhân trên diện rộng],
giúp user [lập tức nhận diện điểm tương thích (Food Compatibility Score) của nhà hàng, danh sách món Xanh/Đỏ/Vàng và được đề xuất địa điểm an toàn nhất xung quanh],
trong khi vẫn kiểm soát [rủi ro sức khỏe bằng cách đưa ra cảnh báo "cần xác nhận lại" (màu Vàng) đối với các món có nguy cơ dị ứng chéo cao và sinh thẻ Flashcard giao tiếp song ngữ].
```

## 4. Chọn build slice

Build slice tốt phải qua 5 câu hỏi:

| Câu hỏi | Đạt khi |
|---|---|
| User cụ thể chưa? | Khách du lịch nước ngoài hoặc người nước ngoài tại Việt Nam có tiền sử dị ứng thực phẩm cụ thể (Thịt vịt, Hải sản, Tôm cua, Đậu phộng, Sữa, Gluten). |
| Task đủ hẹp chưa? | Demo được trong 3 phút: Người dùng chọn Allergy Profile (ví dụ: Duck, Shrimp) -> Nhập địa điểm "Hồ Gươm, Hà Nội" -> AI trả về danh sách nhà hàng chấm điểm Compatibility Score, kèm chi tiết menu phân loại Xanh (An toàn), Đỏ (Nguy hiểm) và Vàng (Cảnh báo). |
| AI decision rõ chưa? | Rõ. AI đóng vai trò Knowledge & Scoring Engine: Tự động phân tích sâu thành phần món ăn -> Đối chiếu hồ sơ dị ứng -> Tính điểm tương thích nhà hàng -> Gợi ý món nên thử và tránh. |
| Failure path rõ chưa? | Rõ. Test case AI báo an toàn nhưng thực tế có rủi ro dị ứng chéo (ví dụ: Phở trộn báo an toàn đậu phộng nhưng quán rắc thêm đậu phộng trang trí). Cách xử lý: Đưa ra cảnh báo Vàng, Disclaimer rõ ràng và cung cấp Flashcard giao tiếp song ngữ (Anh - Việt) để check trực tiếp với nhân viên. |
| Có evidence không? | Có. Từ sự bất tiện khi dùng ChatGPT hỏi đáp 1-1 và sự thiếu sót của Yelp/Tripadvisor khi chỉ gắn nhãn thô sơ (Gluten-free, Vegan) mà không hỗ trợ các dị ứng cụ thể. |

## 5. Quyết định: giữ, giảm scope, hay đổi hướng?

| Tình huống | Quyết định |
|---|---|
| Evidence yếu, user mơ hồ | Giữ nguyên ý tưởng vì nỗi đau dị ứng thực phẩm ảnh hưởng trực tiếp đến tính mạng du khách và chưa có giải pháp tự động hóa triệt để. |
| Ý tưởng quá rộng | CẮT GIẢM scope Day 06: Không build chức năng Scan OCR quét ảnh menu, không định vị GPS thực tế, không làm Login tài khoản. Chỉ sử dụng Mock Database gồm 3 nhà hàng với menu tĩnh ở Hà Nội để chứng minh luồng Scoring Engine. |
| AI không cần thiết | AI là bắt buộc vì cần khả năng suy luận ngữ nghĩa của LLM để bóc tách thành phần ẩn trong món ăn Việt Nam (ví dụ: hiểu Bún Thang dùng nước dùng gà, Miến Vịt dùng nước dùng vịt). |
| Rủi ro cao | Giảm thiểu bằng cách luôn hiển thị Disclaimer, thiết kế nhãn Cảnh báo (Vàng) cho các món nghi ngờ và tự động sinh Thẻ Flashcard song ngữ để người dùng xác thực trực tiếp với bồi bàn. |
| Không demo được trong 1 ngày | Tập trung build luồng cốt lõi: Thiết lập Allergy Profile -> Nhập địa điểm -> Hiển thị danh sách nhà hàng được chấm điểm -> Xem chi tiết món ăn được gán nhãn màu sắc rõ ràng. |

## 6. Câu chốt cuối

Điền câu này trước khi rời lớp:

```text
Dựa trên [khó khăn của khách du lịch bị dị ứng khi tra cứu menu và thành phần ẩn bằng ngoại ngữ],
nhóm sẽ build [hệ thống đối chiếu hồ sơ dị ứng với menu nhà hàng (Allergy Food Navigator AI)],
cho [khách du lịch nước ngoài hoặc người nước ngoài tại Việt Nam],
để giải quyết [nỗi lo chọn nhầm món có thành phần dị ứng ẩn và sự bất tiện khi phải hỏi ChatGPT từng món ăn],
bằng cách AI [tự động phân tích sâu các thành phần ẩn (nước dùng, gia vị, dầu ăn) và chấm điểm an toàn tổng quan cho nhà hàng],
và sẽ test failure path [AI phân tích thiếu rủi ro dị ứng chéo do thói quen chế biến ngầm, khắc phục bằng cảnh báo Vàng và Thẻ Flashcard giao tiếp song ngữ].
```

## 7. Backlog

Những thứ **không build trong Day 06**:

- Chức năng Scan OCR (chụp ảnh menu dịch chữ, Day 06 chỉ dùng text/menu có sẵn).

- Hệ thống user login và quản lý tài khoản người dùng dài hạn.
- Cơ chế cho phép chủ nhà hàng đăng ký và tự cập nhật menu (Restaurant Portal).
- Thu thập dữ liệu menu thực tế từ hàng trăm nhà hàng ngoài thực tế.