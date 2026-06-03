# Template — Thin SPEC Cuối Day 05

Thin SPEC không phải PRD đầy đủ. Đây là bản cam kết đủ rõ để sáng Day 06 nhóm build ngay.

## 1. Track, product/app và user

**Track:** Healthcare & Food Safety  
**Product/app thật:** Allergy Food Navigator AI  
**User cụ thể:** Khách du lịch nước ngoài (như du khách người Mỹ) bị dị ứng thực phẩm nghiêm trọng (như dị ứng thịt vịt, hải sản, tôm cua, đậu phộng, sữa, gluten) khi đi du lịch và trải nghiệm ẩm thực tại Việt Nam.  
**Nhóm có phải user thật không? Nếu không, khác ở đâu?** Không. Nhóm là người địa phương (Việt Nam), hiểu rõ văn hóa chế biến và nguyên liệu ẩn trong ẩm thực Việt Nam, không gặp rào cản ngôn ngữ. Khách nước ngoài ngược lại hoàn toàn: họ mù tịt về nguyên liệu ẩn và không thể nói tiếng Việt để hỏi nhân viên nhà hàng.

## 2. Evidence summary

| Evidence | Nguồn | User/pain nói lên điều gì? | SPEC phải đổi gì? |
|---|---|---|---|
| AI dịch thô "Bún Thang" bỏ sót tôm khô trong nước dùng | Self-use (ChatGPT) | LLM thông thường dịch nghĩa bề mặt tên món ăn, bỏ sót các nguyên liệu ẩn (hidden ingredients). | Tích hợp cơ sở dữ liệu ẩm thực địa phương (Food Knowledge Base) để bóc tách thành phần ẩn. |
| Khách bị dị ứng nặng khi ăn Pho do lây nhiễm chéo tại bếp | Reddit r/vietnam | Nguy cơ lây nhiễm chéo và biến tấu công thức tại quán ăn thực tế rất cao. | Tạo thẻ Allergy Card bằng tiếng Việt để phục vụ/đầu bếp đối chiếu trực tiếp tại chỗ. |
| Spokin không có dữ liệu tại Việt Nam và Đông Nam Á | App Store Review | Các app dị ứng quốc tế thiếu hụt dữ liệu ẩm thực địa phương châu Á. | Tập trung tối ưu hóa dữ liệu và công thức các món ăn truyền thống & đường phố Việt Nam. |

## 3. Pain statement

```text
User khách du lịch nước ngoài bị dị ứng đang gặp khó ở bước chọn món ăn an toàn trên menu tại Việt Nam,
vì rào cản ngôn ngữ và không nhận biết được các nguyên liệu ẩn (hidden ingredients) trong nước dùng hoặc nước sốt,
dẫn tới nguy cơ ăn nhầm chất gây dị ứng dẫn đến sốc phản vệ hoặc phải từ bỏ cơ hội trải nghiệm ẩm thực địa phương.
Bằng chứng chính là các bài đăng trên Reddit r/vietnam và TripAdvisor về việc khách du lịch phải nhập viện khẩn cấp do ăn nhầm bún/phở có nước dùng ninh tôm hoặc lạc giã nhỏ trong nước sốt.
```

## 4. Build slice

```text
Cho khách du lịch bị dị ứng thực phẩm đang chọn món ăn tại nhà hàng Việt Nam,
prototype sẽ dùng AI để phân tích món ăn trên menu, bóc tách nguyên liệu ẩn bằng cách tham chiếu cơ sở dữ liệu ẩm thực, chấm điểm an toàn,
tạo ra một bản phân tích an toàn món ăn (Food Safety Report) kèm thẻ giao tiếp tiếng Việt (Allergy Card) cho đầu bếp,
và xử lý failure mode khi món ăn lạ hoặc viết tắt bằng cách hạ điểm tin cậy (low-confidence warning) và sinh thẻ câu hỏi kiểm chứng trực tiếp.
```

## 5. Auto/Aug decision

Chọn một:

* [x] **Augmentation:** AI gợi ý/draft/phân loại, user quyết cuối.
* [ ] **Conditional automation:** AI tự làm trong case hẹp; case mơ hồ/rủi ro chuyển người.
* [ ] **Automation:** AI tự quyết và tự hành động.

**Lý do chọn:** Do tính chất rủi ro cao liên quan trực tiếp đến sức khỏe và tính mạng của người dùng (sốc phản vệ), AI không được phép tự động ra quyết định thay mà chỉ đóng vai trò hỗ trợ phân tích thông tin và công cụ hỗ trợ giao tiếp. Quyết định cuối cùng về việc ăn hay không phải do người dùng và nhà hàng xác nhận.  
**Human role:** decider / reviewer / rescuer  

## 6. Four paths

| Path | Prototype phải thể hiện gì? |
|---|---|
| **Happy** | User dị ứng tôm nhập "Bún Thang" -> AI phân tích nước dùng bún thang truyền thống ninh từ tôm khô -> Báo đỏ (Nguy hiểm) -> Đề xuất "Phở Gà" thay thế (an toàn) và sinh Allergy Card hỏi quán: *"Món Bún Thang của quán có sử dụng tôm khô hay hải sản trong nước dùng không?"* |
| **Low-confidence** | User nhập tên món viết tắt hoặc không rõ ràng (ví dụ: "Bún h.thang") -> AI không chắc chắn món gì -> Cảnh báo màu vàng (Cần kiểm tra lại) -> Dự đoán các món khả thi và tạo thẻ hỏi đầu bếp: *"Đây có phải là món Bún Thang không? Bếp có dùng tôm khô không?"* |
| **Failure** | User nhập món "Gỏi cuốn" -> AI bóc tách nguyên liệu và báo an toàn (không tôm/lạc) nhưng quán ăn tự biến tấu thêm bơ đậu phộng vào nước sốt mà AI không biết -> User ăn phải lạc gây dị ứng. |
| **Correction** | Khi xảy ra sai sót, User báo lại: *"Quán này dùng nước chấm tương đậu phộng cho gỏi cuốn"* -> AI ghi nhận đính chính của user, cập nhật ngay vào cơ sở dữ liệu cục bộ của phiên dùng để các món tương tự sau đó tự động kích hoạt cảnh báo đậu phộng. |

## 7. Failure mode nguy hiểm nhất

```text
Nếu user ăn món ăn dựa hoàn toàn vào đánh giá của AI mà không xác nhận lại với quán,
AI có thể bỏ sót chất gây dị ứng do quán tự biến tấu công thức hoặc nhiễm chéo (cross-contamination) trong quá trình nấu,
hậu quả là user bị dị ứng nặng/sốc phản vệ.
Prototype sẽ xử lý bằng hiển thị Disclaimer bắt buộc xác nhận, và tự động tạo thẻ Allergy Card bằng tiếng Việt kèm nút check trực quan yêu cầu nhân viên quán ký/ấn xác nhận trước khi ăn.
Owner kiểm thử path này là Trần Minh Quang.
```

## 8. Owner plan cho sáng Day 06

| Thành viên | Việc phụ trách | Bằng chứng cần có trong repo |
|---|---|---|
| **Đỗ Quốc An** | Research / evidence | File `evidence-pack-template.md` hoàn chỉnh & file dữ liệu `food_knowledge_base.json`. |
| **Nguyễn Khánh Linh** | SPEC & Test / failure path | File `thin-spec-template.md` hoàn chỉnh & bộ test cases mô phỏng failure path. |
| **Trần Diệu Linh** | Prototype | Mã nguồn ứng dụng web/python (`app.py` hoặc UI prototype). |
| **Thân Minh Hiếu** | Demo script / repo | Video quay thử kịch bản demo (happy path & low confidence path) và tài liệu hướng dẫn chạy. |
