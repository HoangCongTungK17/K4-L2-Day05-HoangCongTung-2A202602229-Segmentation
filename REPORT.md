# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602229
- Ngày / CVAT local: 17/09/2026 / Local
- Công cụ đã dùng: AI Model (Auto-segmentation)

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh số 1, chiếc xe ô tô nằm ở giữa bức ảnh.
- Class và quy tắc tôi dùng để chọn biên: Class `car`. Tôi dùng quy tắc bám sát mép thân xe, không lấy phần bóng râm dưới mặt đường.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: Công cụ AI gợi ý bị lẹm ra ngoài và thỉnh thoảng gộp 2 xe đứng sát nhau. Tôi đã xóa mask lỗi và tách chúng ra thành các object riêng biệt.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task `medium_instance`, ảnh số 1, vùng gần 2 chiếc xe đỗ sát nhau.
- Lỗi thuộc loại: gộp-tách — AI gộp 2 chiếc xe sát nhau thành 1 mask duy nhất.
- Bằng chứng tôi nhìn thấy: Trong cột Objects List chỉ thấy 1 object nhưng khi bấm vào thì vùng màu bao phủ cả 2 chiếc xe.
- Quy tắc và hành động sửa: Theo quy tắc "hai vật cùng lớp sát nhau vẫn là hai instance", tôi đã xóa mask lỗi đó và dùng Polygon vẽ lại thành 2 object riêng biệt cho từng chiếc xe.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại thành `medium_instance.zip`.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `medium_instance` ảnh 2, bóng râm dưới gầm xe | Bóng râm thuộc về class `car` hay thuộc về `road`? | Quy tắc: mask chỉ bao phần thân xe nhìn thấy, không lấy bóng râm | Quyết định: không tô bóng râm vào mask xe, để phần đó thuộc `road` |
| `hard_panoptic` ảnh 1, phần cây che khuất mái nhà | Pixel giao giữa `vegetation` và `building` thuộc về cái nào? | Vẽ từ xa tới gần: building ở phía xa hơn, vegetation ở gần hơn | Quyết định: gán phần cây che khuất là `vegetation` vì nó ở lớp trước |
| `cp6_coverage` ảnh 1, vùng đường chân trời mờ | Đường viền mờ giữa `sky` và `building` rất khó phân định | Nhìn theo đường nét kiến trúc của tòa nhà làm ranh giới | Quyết định: bám theo mái nhà làm ranh giới, phần mờ không chắc gán cho `sky` |
