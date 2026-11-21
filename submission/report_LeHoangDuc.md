# Báo cáo cá nhân — Ngày 11

Họ tên: Lê Hoàng Đức   Mã học viên: 2A202603334  
Phiên bản CVAT (Help → About): 2.81.0 
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): ⟨bạn điền theo manifest⟩  
Thời điểm export (ngày giờ trên CVAT): cập nhật cuối trong XML là 21/11/2026 09:27:58 (front, job 17) và 09:29:40 (fisheye, job 18), giờ Việt Nam;   Số lần nộp lại sau Rework: 1

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | `lane`, `road_curb` là polyline; `crosswalk`, `drivable` là polygon; `traffic_light`, `traffic_sign` là rectangle |
| Thuộc tính và giá trị | Đúng | `lane`: position (L1, R1, L2, R2, other), style (solid, dashed), color (white, yellow, other), kind (single, double); `drivable`: area_type (direct, alternative); `traffic_light`: color, type, facing, edge_zone; `traffic_sign`: group (6 giá trị), facing, edge_zone. `edge_zone` là ô tick (checkbox), mặc định false |
| 4 tag ảnh | Đúng | `camera` (5 giá trị), `timeofday` (day, dusk, night), `weather` (clear, overcast, rain, fog, other), `source` (real, simulated); mỗi tag có thuộc tính select `value` |
Cách kết thúc polyline trên bản CVAT này: Bấm N
Cách đặt tag ảnh trên bản CVAT này: tag là label kiểu Tag (không vẽ hình), chọn giá trị ở thuộc tính `value`; trong XML thể hiện bằng thẻ `<tag label="camera">` kèm `<attribute name="value">`. 

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 38 | 14 | 7 | 28 | 28 | 37 |
| front-extra (đã làm 4 / 4) | 4 | 10 | 2 | 10 | 9 | 8 | 18 |
| fisheye | 8 | 8 | 13 | 8 | 10 | 3 | 8 |
| fisheye-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |



## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A08 | `lane` L1 | Một polyline hay tách hai khi vạch đổi từ liền sang đứt gần giao lộ | Tách 2 polyline (liền và đứt) | Do 2 kiểu khác nhau |
| A10 | tag `weather` | `clear` hay `rain` (mặt đường ướt rõ) | `clear` | Do trời đã quang đãng |



## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Nguyễn Đình Phú-2A202603333   Quyết định nhận được: **Rework** (1 lỗi nặng, 13/102 nhãn lỗi chính = 12,7 %, 1 lỗi nhẹ)  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-03 position | 1 | Đồng ý: A04 vạch phải phải là R2 | Đã sửa: XML hiện tại có R2 (trắng đôi) |
| QC1-05 vạch đứt, che | 1 | Đồng ý: A04 vàng đôi bị tách | Chưa: A04 vẫn còn 2 polyline L1 (double và single) |
| QC1-06 style, color, kind | 1 | ⟨xem lại A01 phóng to xem L2 có 2 nét không⟩ | Một phần: L2 đã là white; kind vẫn là single |
| QC1-08 đèn, màu | 5 | Đồng ý | Một phần: A10 đèn đỏ đã thêm (557,198)–(571,209); A08 hai đèn xanh (648,210) và (603,202) chưa thêm, box (518,179)–(540,203) vẫn gộp; B02 hộp góc phải đã có nhưng nhỏ hơn cụm Phú nêu |
| QC1-10 hình in, đủ biển | 6 | Đồng ý | Chưa đủ: A08 hai biển cấm cột phải (991,184) và (991,216) chưa thêm; A10 ba biển đang gộp thành 1 hộp cao (40,44)–(102,174), cần 3 hộp riêng; box 7 px (534,236)–(558,243) vẫn còn |
| QC1-11 fisheye | 1 | Đồng ý | Chưa: B02 box (103,111)–(163,202) vẫn `edge_zone` = false |




## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `LeHoangDuc_front` (job 17, 16 ảnh) | Có (XML đọc được, định dạng CVAT 1.1) | A01: ⟨số trên job⟩ / 9 | A02: ⟨số trên job⟩ / 6 | Có, 16/16 ảnh, `front` |
| `LeHoangDuc_fisheye` (job 18, 12 ảnh) | Có (XML đọc được, định dạng CVAT 1.1) | B01: ⟨số trên job⟩ / 5 | B02: ⟨số trên job⟩ / 6 | Có, 8/8 ảnh đã gán (B01–B02 `fisheye_front`, B03–B04 `fisheye_rear`, B05–B06 `fisheye_left`, B07–B08 `fisheye_right`); B09–B12 chưa gán |



## 6. Ảnh chụp màn hình
⟨bạn tự chụp⟩
1. Tab Labels của project.
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển).
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong.
4. Một đoạn XML có <polyline label="lane">.

## 7. Tự đánh giá 
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20: QC1-10 và QC1-08, tức bỏ sót biển và đèn (11 trên 15 lỗi trong phiếu), nhiều nhất ở A08 và A10 là ảnh đô thị nhiều biển và đèn nhỏ. Cách tránh: trước khi bấm Ctrl+S, quét ảnh theo từng cột (trái, giữa, phải) và đếm lại số đèn và biển; phóng to các cột có nhiều biển xếp dọc; xoá hộp cao dưới 8 px; một biển một hộp, không gộp.  
Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào: Nhãn `lane` đi vào mô hình nhận dạng làn, nhãn `drivable` đi vào phần vùng lái. Lỗi đã sửa: ở A04 vạch trắng bên phải bị gán L2 thay vì R2. Nếu không sửa, model học rằng vạch bên phải xe là làn bên trái, nhầm vị trí tương đối của xe so với làn, nên hệ thống giữ làn (LKA) có thể đánh giá sai xe đang lệch về phía nào.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
Ảnh A01, vạch L1 (nội suy tuyến tính theo y trên polyline; "-" là polyline không đi qua hàng đó):

| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của tôi | - | 157 | 203 | 250 | 297 |
| x của Phú | - | 155 | 202 | 250 | 297 |

Hai vạch khác để tham khảo:

| Vạch | y | 720 | 680 | 640 | 600 | 560 |
| --- | --- | ---: | ---: | ---: | ---: | ---: |
| R1 |  tôi | - | - | 599 | 542 | 485 |
| R1 | Phú | - | - | 600 | 542 | 484 |
| R2 |  tôi | - | 1177 | 1005 | 843 | 674 |
| R2 | Phú | - | 1169 | 1001 | 838 | 674 |



Trả lời 3 câu (bản nháp):

1. Với L1 của tôi (đầu xa dừng ở y ≈ 513), dừng sớm 40 px thì đầu xa lùi về y ≈ 553, vẫn phủ hàng 560 nên không hàng nào đổi. Với R1 (đầu xa ở y ≈ 524) thì lùi về ≈ 564, nên **hàng 560** đổi thành "không có làn". Hàng xa nhất là hàng đầu tiên mất.
2. Hàng 720 cả hai polyline L1 đều chưa tới (bắt đầu ở y ≈ 692), nên không so được; ở hàng 680 hai bạn lệch 2 px (L1) và 8 px (R2); ở hàng 560 lệch 0 px (L1 và R2) và 1 px (R1). Với LKA, lệch ở hàng gần xe (y lớn như 680) thường quan trọng hơn vì xe điều khiển theo vị trí làn ngay trước mũi xe
3. Cách tính nội suy theo y không đổi nếu đảo chiều, vì mỗi đoạn vẫn cho cùng một x tại cùng một y. Cái hỏng là các giả định về thứ tự điểm: script nào coi điểm đầu là điểm sát xe hoặc điểm cuối là điểm dừng sẽ đo sai chiều và điểm dừng, và `road_check` có kiểm "chiều" ở QC1-04. ⟨bạn kiểm lại bằng cách đọc code rowanchor⟩
