# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 28 skeleton, trung bình 15.89 khớp có v > 0 mỗi người
- Tổng: v=2 367 | v=1 78 | v=0 31

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 24 | 4 | 0 | 14% |
| 1 | left_eye | 20 | 8 | 0 | 29% |
| 2 | right_eye | 24 | 4 | 0 | 14% |
| 3 | left_ear | 17 | 11 | 0 | 39% |
| 4 | right_ear | 22 | 6 | 0 | 21% |
| 5 | left_shoulder | 27 | 1 | 0 | 4% |
| 6 | right_shoulder | 28 | 0 | 0 | 0% |
| 7 | left_elbow | 24 | 4 | 0 | 14% |
| 8 | right_elbow | 26 | 2 | 0 | 7% |
| 9 | left_wrist | 21 | 7 | 0 | 25% |
| 10 | right_wrist | 22 | 5 | 1 | 18% |
| 11 | left_hip | 22 | 5 | 1 | 18% |
| 12 | right_hip | 24 | 3 | 1 | 11% |
| 13 | left_knee | 17 | 5 | 6 | 18% |
| 14 | right_knee | 18 | 4 | 6 | 14% |
| 15 | left_ankle | 15 | 5 | 8 | 18% |
| 16 | right_ankle | 16 | 4 | 8 | 14% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
