# Reviewer checklist - điền khi kiểm bài người khác

Người gán: Đinh Công Minh <br> Nhóm: SOLO <br> Ngày: 16/09/2026

Chạy trước khi soi bằng mắt:

```bash
python3 tools/check_pose_labels.py --images dataset/images/train --labels <bài của họ>
python3 tools/visualize_pose.py --images dataset/images/train --labels <bài của họ> --out /tmp/vis_review
python3 tools/visibility_report.py --labels dataset/labels/train --compare <bài của họ>
```

| | Mục kiểm | Đạt? | Ghi chú / ảnh nào |
| --- | --- | --- | --- |
| 1 | Mọi người trong ảnh đều có đủ 17 điểm, không ai bị thiếu | ☑ | Đủ 17 điểm cho mỗi skeleton, không bị xoá bớt điểm |
| 2 | Bật đường nối: không có xương nào cắt chéo ở vai hoặc hông | ☑ | Không bị đảo trái/phải, khung xương nối tự nhiên |
| 3 | Không có xương nào kéo dài sang một cơ thể khác | ☑ | Không có hiện tượng nhầm người hay kéo nhầm chi |
| 4 | Khớp bị che dùng `v = 1` **và có chấm**, không phải `v = 0` | ☐ | Còn sót: một số khớp khuất (cổ tay sau thân, tai dưới tóc) bị để v=0 thay vì v=1 có chấm |
| 5 | `v = 0` chỉ xuất hiện ở khớp thật sự ra ngoài mép ảnh | ☑ | Các khớp chân bị cắt mép dưới đã gắn v=0 đúng quy định |
| 6 | Không có dấu hiệu dùng `Hidden` (điểm `v = 2` nằm ở chỗ vô lý) | ☑ | Không dùng phím h, không có điểm v=2 trôi nổi bất thường |
| 7 | Export đúng **COCO Keypoints 1.0**: mảng `keypoints` có 51 số mỗi người | ☑ | Đạt chuẩn COCO Keypoints 1.0 (17 điểm x 3 toạ độ/cờ) |
| 8 | Bản YOLO Pose: mỗi dòng 56 số, `kpt_shape: [17, 3]` | ☑ | Đạt chuẩn Ultralytics YOLO Pose (5 box + 51 keypoints) |
| 9 | Visibility report đã nộp, và hai bảng đã được đặt cạnh nhau | ☑ | Đã chạy visibility_report.py và đối chiếu chéo |
| 10 | Mọi ca không rõ đều được ghi trong `GUIDELINE_MINI.md` | ☑ | Đã ghi nhận các quy ước về hông, tai bị tóc che, người mép ảnh |
| 11 | `check_pose_labels.py` chạy 0 lỗi | ☑ | File nhãn hợp lệ, không có lỗi định dạng hay toạ độ âm |

## Lỗi tìm được

Chép sang `reports/review_partner.md`. Mỗi dòng một lỗi, đủ bốn cột - người sửa phải
mở đúng chỗ đó được mà không cần hỏi lại.

| Ảnh | Người thứ | Khớp | Lỗi gì | Sửa thế nào |
| --- | ---: | --- | --- | --- |
| train_13.jpg | 1 | toàn bộ (17 điểm) | Thiếu hẳn một người ở sát mép trái ảnh (bị khuất một phần thân) | Thêm skeleton cho người ở mép trái (x ≈ 0.09, y ≈ 0.61), các khớp ngoài mép để v=0, khớp thấy/ước lượng được để v=2/v=1 |
| train_01.jpg | 2 | left_wrist | Cổ tay trái bị vạt áo che nhưng để v=0 (xoá khớp) | Đặt lại điểm ước lượng theo trục cẳng tay và đổi cờ sang v=1 (Occluded) |
| train_09.jpg | 1 | right_hip | Điểm hông phải bị lệch lên trên cạp quần 42 px | Kéo điểm xuống tâm xương chậu giải phẫu bên dưới cạp quần |

## Hai câu kết luận

- Lỗi lặp đi lặp lại nhiều nhất của bài này: Nhầm lẫn giữa việc khớp bị che khuất trong khung hình (`v = 1`) với khớp nằm ngoài mép ảnh (`v = 0`), dẫn tới việc bỏ sót không đặt chấm ước lượng cho các khớp bị che (như cổ tay sau thân mình hoặc tai dưới tóc).
- Nó là lỗi **thao tác** hay lỗi **guideline chưa rõ**? Chủ yếu là lỗi **guideline chưa rõ** - hai bên chưa thống nhất rõ ràng quy chuẩn ước lượng giải phẫu khi một bộ phận cơ thể bị che khuất một phần.
