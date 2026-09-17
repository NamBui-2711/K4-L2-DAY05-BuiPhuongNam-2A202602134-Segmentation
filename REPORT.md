# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

- Mã học viên theo lớp: 2A202602134
- Ngày / CVAT local: 17/09/2026 /http://localhost:8080/
- Công cụ đã dùng: CVat, OpenCV tool 

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | Chưa có| 0 / 1 | 0 |
| cp2_slice | Chưa có| 0 / 1 | 0 |
| cp5_occlusion |Chưa có| 0 / 1 | 0 |
| cp3_thin | Chưa có| 0 / 1 | 0 |
| cp4_curb | Chưa có| 0 / 1 | 0 |
| cp6_coverage | Chưa có| 0 / 1 | 0 |
| **Tổng tối đa** | | | **82** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: ảnh đầu tiên, Person 5
- Class và quy tắc tôi dùng để chọn biên: `person`. Tôi vẽ mask theo đường biên phần người có thể nhìn thấy, bám sát hình dáng người và không vẽ sang các vật thể xung quanh.

- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: Với một số vật thể, tôi sử dụng OpenCV để hỗ trợ vẽ/chỉnh mask. Tôi vẫn kiểm tra lại biên của từng object trong CVAT trước khi Save.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task Medium/ ảnh đầu tiên/ Vùng giữa ảnh (Motorcycle 24)
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: Sai lớp
- Bằng chứng tôi nhìn thấy: Sau khi vẽ thấy màu sắc của cùng chiếc xe máy khác nhau nên đã kiểm tra lại.
- Quy tắc và hành động sửa: Sửa đúng tên lớp thành Motorcycle
- Sau sửa đã Save và export lại chưa? Rồi

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| 1. Ảnh có nhiều CAR được chở trên xe tải (Hard (Ảnh 2)) | Có thể coi cả cụm xe là một vùng CAR hoặc tách từng chiếc xe | Đây là instance segmentation nên mỗi chiếc CAR nhìn thấy được cần được xem là một instance riêng | Tôi tách từng chiếc CAR thành instance riêng; phần bị che khuất không tự đoán |
| 2. Vùng vegetation ở xa, nhiều cây/bụi liền sát nhau (Hard ảnh 2 Vegetation105) | Có thể tách từng cây/bụi thành các object riêng hoặc tô cả vùng vegetation liền nhau | Ở khoảng cách xa không thể xác định rõ ranh giới từng cây; cần dựa vào loại segmentation của task | Tôi không cố tách từng cây khi không xác định được biên; với semantic segmentation, tôi tô phần vùng vegetation có thể xác định rõ |
| 3. Object bị xe/người khác che khuất một phần | Có thể vẽ thêm phần bị che dựa trên suy đoán hoặc chỉ vẽ phần nhìn thấy | Biên của phần bị che không quan sát được trực tiếp | Tôi chỉ vẽ phần object quan sát được và không tự đoán phần bị che khuất |
