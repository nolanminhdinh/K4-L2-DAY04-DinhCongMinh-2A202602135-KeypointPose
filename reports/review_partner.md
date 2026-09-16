# Review Partner - Báo cáo lỗi bài đối chiếu

Người gán: Đinh Công Minh <br> Nhóm: SOLO <br> Ngày: 16/09/2026

## Danh sách lỗi tìm được

| Ảnh | Người thứ | Khớp | Lỗi gì | Sửa thế nào |
| --- | ---: | --- | --- | --- |
| train_13.jpg | 1 | toàn bộ (17 điểm) | Thiếu hẳn một người ở sát mép trái ảnh (bị khuất một phần thân) | Thêm skeleton cho người ở mép trái (x ≈ 0.09, y ≈ 0.61), các khớp ngoài mép để v=0, khớp thấy/ước lượng được để v=2/v=1 |
| train_01.jpg | 2 | left_wrist | Cổ tay trái bị vạt áo che nhưng để v=0 (xoá khớp) | Đặt lại điểm ước lượng theo trục cẳng tay và đổi cờ sang v=1 (Occluded) |
| train_09.jpg | 1 | right_hip | Điểm hông phải bị lệch lên trên cạp quần 42 px | Kéo điểm xuống tâm xương chậu giải phẫu bên dưới cạp quần |

## Hai câu kết luận

- Lỗi lặp đi lặp lại nhiều nhất của bài này: Nhầm lẫn giữa việc khớp bị che khuất trong khung hình (`v = 1`) với khớp nằm ngoài mép ảnh (`v = 0`), dẫn tới việc bỏ sót không đặt chấm ước lượng cho các khớp bị che (như cổ tay sau thân mình hoặc tai dưới tóc).
- Nó là lỗi **thao tác** hay lỗi **guideline chưa rõ**? Chủ yếu là lỗi **guideline chưa rõ** - hai bên chưa thống nhất rõ ràng quy chuẩn ước lượng giải phẫu khi một bộ phận cơ thể bị che khuất một phần.
