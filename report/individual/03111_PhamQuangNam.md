# Báo cáo cá nhân — HoVaTen-MSSV

Đổi tên file theo quy tắc `MSSV_HoTen.md`. Ví dụ: `20241234_NguyenVanAn.md`.

Dữ liệu: 12 ảnh người COCO val2017 (Lin et al., 2014) và 8 ảnh chân dung Wikimedia Commons, chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên: Phạm Quang Nam 
- MSSV: 2A202603111
- Email: quangnam97425@gmail.com
- Link repository:
- Phiên bản CVAT (Help → About): 2.74.1
- Máy: hệ điều hành Window10 · RAM 16 GB · chạy CVAT chế độ đầy đủ
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): có
- Giờ bắt đầu: 17h00
- Giờ kết thúc: 18h40

## 1. Kiểm tra label (CP0)

| Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| `person` | 1 | 17 | đúng | đúng |  |
| `face` | 1 | 13 | đúng | đúng | |

Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu)? Có

Cách đổi cờ `occluded` / `outside` cho **một điểm** trên phiên bản CVAT này (một câu):
Ấn chuột trái vào điểm muốn đổi và di chuyển chuột tới 1 panel mini chứa các lựa chọn để đồi
...

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| `easy` | 5 | 5 | 0 | 0 | 15 |
| `occluded` | 3 | 7 | 0 | 0 | 15 |
| `back` | 2 | 4 | 0 | 0 | 5 |
| `small` | 1 | 1 | 0 | 0 | 3 |
| `crowd` | 1 | 3 | 0 | 0 | 12 |
| `faces` | 8 | 8 | — | 0 | 20 |

- Số ảnh người đã xong ở mốc phút 105: 10 / 10
- Thời gian thực tế (phút): CP1 45p · CP2 20p · CP3 20p
- Ảnh tốn thời gian nhất là ảnh nào, vì sao?
Ảnh 000000542160.jps tốn nhiều thời gian nhất, là vì trong ảnh có 3 người cự ly gần với nhau, nhiều hơn so với các ảnh khác
Tư thế từng người đưa ra từng thử thách khác nhau trong việc làm skeleton.  
...

## 3. Bảng ca khó (CP1, CP2)

Mỗi điểm bạn phân vân một dòng, nhất là phân vân giữa `v = 1` và `v = 0`, hoặc không chắc hướng người.

| Ảnh | Người / mặt | Điểm | Cờ đã chọn | Phân vân giữa | Lý do chọn |
|---|---|---|---:|---|---|
| 000000022857.jpg | Người | 13 | 2, 1, 0 | 0 và 1 | Chọn 0 vì không xác định được vị trí có thể của đồi gối |
| face_324513.jpg | mặt | 11 | 2, 1 | 0 và 1 | Chọn 1 vì theo guideline mặc dù không thấy rõ vị trí có thể của mắt |
| 000000542160.jpg | Người | 14 | 2, 1, 0 | 0 và 1 | Chọn 0 vì không xác định được găng tay là của người nào đang cầm |

## 4. Bảng tự review (CP3)

Đi từ ảnh cuối về ảnh đầu. 5 ảnh người (ít nhất 2 ảnh `back` hoặc `crowd`) và 3 ảnh mặt. Ít nhất 8 dòng, kể cả dòng `ok`. Ghi lỗi trước, sửa sau.

Mã lỗi dùng đúng một trong: `lr_swap`, `vis_flag`, `position`, `missing`, `extra`, `ok`.

| Ảnh | Người / mặt | Điểm | Mã lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|---|
| 000000022857.jpg | Người | 13 | 0 | ok | |
| 000000043968.jpg | Người | 9 | 0 | ok | |
| 000000269462.jpg | Người | 13 | 3 | extra | đẫ sửa |
| 000000307757.jpg | Người | 17 | 0 | ok | |
| 000000324953.jpg | Người | 17 | 0 | ok | |
| face_143959.jpg | mặt | 13 | 0 | ok | |
| face_147624.jpg | mặt | 13 | 0 | ok | |
| face_324513.jpg | mặt | 13 | 0 | ok | |

Tổng hợp số lỗi theo mã:

| `lr_swap` | `vis_flag` | `position` | `missing` | `extra` | `ok` |
|---:|---:|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 | 3 | 7 |

Điểm còn phân vân giữa `v = 1` và `v = 0` (ghi cả hai lựa chọn và lý do chọn):

...

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

Tự kiểm tay trong file JSON:

| File | Người / mặt kiểm (ảnh, thứ tự) | Số phần tử `keypoints` | Điểm `outside` ra `v = 0`, `occluded` ra `v = 1`? | `num_keypoints` khớp? |
|---|---|---:|---|---|
| `HoVaTen_persons.zip` | Người, 1| 13 | 4, 4 | 13 |
| `HoVaTen_persons.zip` | Người, 2 | 9 | 0, 5 | 17 |
| `HoVaTen_faces.zip` | Mặt, 5 | 13 | 0 | 13 |

Sau khi xuất, CVAT ghi `occluded` thành `v = ___` và `outside` thành `v = ___`. Tọa độ của điểm `outside` trong file là `0, 0` hay tọa độ cũ? ___

Hai job đã chuyển sang completed trên CVAT? Có

Dán phần **TÓM TẮT** in ra từ `src/check_submission.py`:

```text
File person: PhamQuangNam_persons.zip
  Số ảnh: 12 · số skeleton `person`: 21 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000022857=2, 000000043968=1, 000000091637=2, 000000177338=2, 000000184224=1, 000000240340=1, 000000269462=3, 000000307757=2, 000000324953=2, 000000451084=1, 000000463932=1, 0000
00542160=3
  Cờ v: v=2 231 (65%) · v=1 37 (10%) · v=0 89 (25%)
  num_keypoints trung bình: 12.8
- File face: PhamQuangNam_faces.zip
  Số ảnh: 8 · số skeleton `face`: 8 · mỗi annotation 39 số
  Skeleton theo ảnh: face_143959=1, face_147624=1, face_223746=1, face_324513=1, face_425647=1, face_442231=1, face_469647=1, face_562485=1
  Cờ v: v=2 93 (89%) · v=1 11 (11%) · v=0 0 (0%)
  num_keypoints trung bình: 13.0
- Ghi chú: 89 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 3
Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)
```

Các `[CẢNH BÁO]` còn giữ nguyên và lý do:
[CẢNH BÁO] 000000043968.jpg #1: cặp knee, ankle nằm ngược phía so với các cặp còn lại. Có thể đổi trái/phải một cặp (`lr_swap`), hoặc tay / chân bắt chéo thật: kiểm lại.
[CẢNH BÁO] 000000463932.jpg #1: cặp eye nằm ngược phía so với các cặp còn lại. Có thể đổi trái/phải một cặp (`lr_swap`), hoặc tay / chân bắt chéo thật: kiểm lại.
[CẢNH BÁO] 000000542160.jpg #2: trái/phải không nhất quán giữa các cặp điểm (ear, hip so với knee, ankle). Kiểm `lr_swap`.
...

## 6. Ảnh chụp màn hình

1. Label `person` trong label constructor (đủ 17 điểm có tên):

   ![Label person](images/1_label_person.png)

2. Một người quay lưng đã gán, cờ đã đặt:

   ![Người quay lưng](images/2_nguoi_quay_lung.png)

3. Một khuôn mặt đã gán 13 điểm, phóng to vùng mắt:

   ![Khuôn mặt phóng to](images/3_mat_phong_to.png)

4. Một đoạn JSON xuất của một người:

   ![JSON export](images/4_json_export.png)

Nguồn ảnh: COCO val2017 / Wikimedia Commons.

## 7. Tự đánh giá

1. Lỗi bạn mắc nhiều nhất hôm nay, và cách bạn sẽ tránh ở dự án thật:
Không gặp lỗi.

2. Một quy tắc bạn đề xuất thêm vào guideline (kèm ảnh ví dụ nếu có):
Không có thêm quy tắc nào để đề xuất thêm do ảnh được đưa đã áp đúng đủ với guideline

3. Nhãn của bạn đi vào model ở đâu? Chọn một lỗi bạn đã sửa và nói nó sẽ làm model học sai thế nào (heatmap, trọng số trong loss, hay bước lật ảnh):
Lỗi đã sửa: Nhầm lẫn giữa keypoint mắt trái và mắt phải khi annotation khuôn mặt.

Nhãn đi vào model ở đâu: Các tọa độ keypoint được sử dụng làm Ground Truth để tạo heatmap trong quá trình training.

Ảnh hưởng nếu không sửa: Nếu mắt trái bị gán nhầm thành mắt phải, heatmap Ground Truth sẽ được tạo ở vị trí không chính xác cho từng loại keypoint. Model sẽ học sai vị trí của mắt trái và mắt phải, khiến dự đoán facial landmarks kém chính xác hơn.

## 8. Khó khăn và lỗi kỹ thuật

...

## Bonus (nếu làm)

### B1 — 3 ảnh người khó thêm

| Ảnh | Số skeleton | Số người dưới 60 px | Ca khó nhất |
|---|---:|---:|---|
| | | | |
| | | | |
| | | | |

Kết quả `src/check_submission.py` cho `HoVaTen_bonus_persons.zip`:

```text
(dán ở đây)
```

### B2 — 5 ảnh khuôn mặt đen trắng / hồng ngoại

Ảnh không màu khó hơn ở điểm nào? Kính râm trên ảnh hồng ngoại có còn là `v = 1` không?
Ảnh không màu nó khó hơn ở chỗ là khó phân biệt người với nền hơn, các chi tiết trên cơ thể hoặc trên mặt có thể bị hòa trộn do không có màu sắc đa dạng.
Người cũng có thể bị hòa trộn với chi tiết của background, và nếu mà hình ảnh có chất lượng kém hoặc nhỏ, việc phân biệt và gắn skeleton trở nên khó hơn

Kính râm trên ảnh hồng ngoại vẫn để là 'v = 1' trong trường hợp vẫn có thể định dạng được mắt theo guideline.
...

### B3 — Model so với nhãn của tôi (không tính điểm)

- Demo đã dùng:
- Ảnh đã thử:

1. Model có trả điểm cho khớp bị che, hay khớp ngoài ảnh không? Confidence ở các điểm đó thế nào?

   ...

2. Với người quay lưng, model có đổi trái/phải không?

   ...

3. Bộ điểm của model có giống 17 điểm COCO không?

   ...

## 9. Tài liệu tham khảo và công cụ AI đã dùng

...
