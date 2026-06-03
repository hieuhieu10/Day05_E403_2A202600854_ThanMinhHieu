# Evidence Pack — Allergy Food Navigator AI

Nộp kèm thin SPEC cuối Day 05.

## 1. Nhóm và track

**Tên nhóm:** Little Evil Demons
**Track:** Track C
**Product/app đã chọn:** Allergy Food Navigator AI (AI Hỗ Trợ Khám Phá Ẩm Thực An Toàn Cho Người Dị Ứng)
**Build slice đang nghĩ:** Chức năng đối chiếu hồ sơ dị ứng (User Profile) với thực đơn nhà hàng (Restaurant Menu) để tính điểm an toàn (Scoring) và gợi ý món ăn.

## 2. Self-use evidence

Nhóm tự dùng app/workflow và ghi lại điểm gãy. (Trải nghiệm tìm nhà hàng an toàn hiện tại)

| Observation                                                                                                                                                                                               | Screenshot/link     | Path liên quan | Điều học được                                                                                                                                                  |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------- | -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tìm "nhà hàng an toàn cho người dị ứng đậu phộng" trên Google Maps ra kết quả chung chung, không có chi tiết thành phần món ăn.                                                                           | ![My Image](3.jpeg) | Failure        | Google Maps không hiểu sâu về thành phần món ăn, chỉ tìm text match trong review.                                                                              |
| Dùng Google Translate Camera để dịch một cái menu tiếng Việt: Món "Bánh xèo" dịch ra là "Sizzling pancake" hay "Nộm" dịch ra là "Salad" - không hề nói rõ có rắc đậu phộng hay mắm tôm ở trong hay không. | ![](2.jpg)          | Failure        | Dịch thuật (Translation) chỉ dịch bề mặt chữ, không giúp giải quyết rủi ro thành phần ẩn. User cần AI có khả năng suy luận nguyên liệu gốc (Knowledge Engine). |

## 3. User / review / social evidence

Nguồn có thể là review App Store/Play, group, comment, phỏng vấn nhanh, hoặc nguồn public khác.

| Quote / review / observation                                                                                                       | Nguồn  | User là ai?                  | Pain/failure mode                                                          |
| ---------------------------------------------------------------------------------------------------------------------------------- | ------ | ---------------------------- | -------------------------------------------------------------------------- |
| "Tôi bị dị ứng hải sản nặng, đến Việt Nam thấy món gì cũng sợ có nước mắm hoặc tôm khô cất giấu bên trong."                        | Reddit | Khách du lịch nước ngoài     | Sợ hãi không dám ăn, bỏ lỡ trải nghiệm ẩm thực địa phương, ăn cho qua bữa. |
| "Phải mang thẻ cảnh báo dị ứng dịch sang tiếng Việt đưa cho phục vụ, nhưng họ có vẻ không hiểu mức độ nghiêm trọng của nước dùng." | Reddit | Người nước ngoài sống tại VN | Bất đồng ngôn ngữ, rủi ro giao tiếp dẫn đến nguy hiểm sức khỏe thực sự.    |

## 4. Competitor / analog evidence

| App / mô hình tham khảo | Họ xử lý task này thế nào?                                                                                                                                                  | Pattern học được                                                                                                                                                                                        | Có áp dụng trong 1 ngày không?                            |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Tripadvisor / Yelp      | Tập trung vào tìm kiếm và đánh giá nhà hàng. Một số nơi hỗ trợ tag như "Vegetarian", "Vegan", "Gluten-Free", nhưng phụ thuộc vào thông tin nhà hàng hoặc cộng đồng cung cấp | Dữ liệu nhà hàng và menu rất hữu ích, nhưng chưa đủ để đánh giá rủi ro dị ứng ở cấp độ từng món ăn. Cần AI suy luận thành phần và chất gây dị ứng từ tên món, mô tả món và tri thức ẩm thực địa phương. | Có. Chỉ cần làm danh sách nhà hàng + điểm tương thích.    |
| ChatGPT                 | Trả lời dạng hội thoại 1-1 cho từng món.                                                                                                                                    | Hội thoại quá chậm. Ta cần biến AI từ "chatbot" thành "hệ thống chấm điểm tự động" (Scoring Engine).                                                                                                    | Có, chuyển từ giao diện chat sang giao diện Data/Card UI. |

## 5. Evidence -> Insight

```text
Evidence nổi bật nhất:
Người dùng phải tra cứu thủ công từng món ăn bằng Google Search hoặc Google Translate Camera, vừa chậm vừa dễ sót thành phần ẩn, dẫn đến việc họ thà chọn "ăn cho an toàn ở quán tây" thay vì khám phá món bản địa.

Insight:
User không chỉ gặp khó khăn ở việc dịch tên món ăn (surface problem).
Thật ra họ cần một "người bản địa am hiểu ẩm thực" hỗ trợ ra quyết định nhanh chóng để họ an tâm thưởng thức mà không sợ chết (trust & decision support).

Opportunity:
AI có thể giúp bằng cách tự động hóa hoàn toàn việc đối chiếu menu với hồ sơ dị ứng, tính điểm an toàn và phân loại món ăn (Xanh/Đỏ/Vàng) ngay lập tức, bỏ qua bước phải chat hội thoại.
```

## 6. Evidence đổi SPEC như thế nào?

- [x] Đổi user chính. (Từ user chung chung thành khách du lịch/người nước ngoài)
- [ ] Đổi pain statement.
- [x] Đổi build slice. (Chuyển từ Chatbot hỏi đáp sang Hệ thống AI Scoring/Routing ngầm)
- [ ] Đổi Auto/Aug decision.
- [ ] Đổi 4 paths.
- [ ] Đổi failure mode.
- [ ] Đổi owner/test plan.

Ghi rõ 1-2 thay đổi quan trọng:

```text
Trước evidence, nhóm định: Làm một Chatbot AI để user nhập tên món ăn và chat hỏi xem ăn được không.
Sau evidence, nhóm đổi thành: Hệ thống nhập Allergy Profile từ đầu, sau đó chọn nhà hàng, AI sẽ tự động phân tích toàn bộ menu, chấm điểm (Compatibility Score) và trả ra danh sách món Xanh/Đỏ.
Lý do: Tối ưu UX, USP khác biệt hoàn toàn với ChatGPT, biến AI thành Engine ra quyết định dựa trên dữ liệu.
```
