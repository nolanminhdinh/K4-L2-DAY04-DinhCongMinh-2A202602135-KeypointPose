# Mini guideline - Cá nhân: Đinh Công Minh  |  người gán: Đinh Công Minh  |  ngày: 16/09/2026

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống | Luật bạn chọn | Vì sao |
| --- | --- | --- |
| Hông của người mặc quần áo dài | Gán point vào điểm cách cạp quần 1 khoảng đồng nhất giữa các ảnh | Thông thường hông sẽ nằm phía dưới cạp quần không quá xa |
| Tai bị tóc hoặc mũ bảo hiểm che một phần | Căn cứ theo vị trí của các phần tai nhìn thấy được để ước lượng gán điểm | vì các bộ phận trên cơ thể đều có vị trí cân đối, ở 1 số người có cơ thể lệch cũng ko bị quá nhiều |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | chỉ gán các bộ phận nhìn thấy, gán khuất khỏi cam với các bộ phận khác | các điểm không nhìn thấy không thể đoán được vì chiều dài cơ thể mỗi người là khác nhau không thể đo lường tương đối đoán để gán được |
| Cổ tay nằm sau tay lái / sau thân mình | gán điểm bị che khuất, vị trí thì dựa vào phần khuỷu tay hay vai và tư thế của dáng tay để đoán | Dựa theo hoạt động bình thường hành vi của con người để gán, các vị trí đặt tay thông thường, độ dài các bộ phận trên cơ thể người |
| Hai người chồng lên nhau | Dựa vào bộ phần có thể nhìn thấy được của người để xem xét vị trí của các điểm còn lại kết hợp với tư thế của người đó | Vì tư thế của con người đảm bảo hoạt động bình thường của cơ thể nên chỉ cần dựa vào phần cơ thể còn lại để gán|
| Người nhỏ đến mức nào thì không gán nữa | không thể nhìn thấy rõ tách biệt giữa các bộ phận trên cơ thể | vì khi đó việc đoán tạo ra nhãn không chắc chắn các điểm được đoán không có căn cứ sẽ làm cho AI học đoán mò sai lầm |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `______`, người thứ `___`, khớp `______`

- Mơ hồ ở chỗ nào:
- Bạn quyết thế nào:
- Vì sao:
- Nếu người khác quyết ngược lại thì model học sai cái gì:

### Ca 2 - ảnh `______`, người thứ `___`, khớp `______`

- Mơ hồ ở chỗ nào:
- Bạn quyết thế nào:
- Vì sao:
- Nếu người khác quyết ngược lại thì model học sai cái gì:

### Ca 3 - ảnh `______`, người thứ `___`, khớp `______`

- Mơ hồ ở chỗ nào:
- Bạn quyết thế nào:
- Vì sao:
- Nếu người khác quyết ngược lại thì model học sai cái gì:

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `______` (bạn `___%` / họ `___%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**:
- Luật mới bổ sung vào mục 2 sau khi thống nhất:
