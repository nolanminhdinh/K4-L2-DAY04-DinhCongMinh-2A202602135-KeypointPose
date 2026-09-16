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

### Ca 1 - ảnh `train_01.jpg`, người thứ `1`, khớp `left_wrist`

- Mơ hồ ở chỗ nào: Cổ tay trái bị vạt áo khoác và thân người che khuất khi tay buông tự nhiên hơi lùi về sau; phân vân giữa việc chọn `v=1` (Occluded - đặt chấm ước lượng) hay `v=0` (Outside/xoá khớp).
- Bạn quyết thế nào: Chọn `v = 1` và đặt chấm ước lượng tại vị trí tâm cổ tay giải phẫu dựa trên hướng kéo dài từ cẳng tay và khuỷu tay trái (`left_elbow`).
- Vì sao: Nhân vật nằm hoàn toàn ở trung tâm ảnh, không hề chạm mép viền; khuỷu tay và cẳng tay trên nhìn thấy rất rõ (`v = 2`), đảm bảo cổ tay chắc chắn vẫn nằm trong không gian ảnh và có căn cứ hình học để ước lượng.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu gán `v = 0` (hoặc xoá khớp), model sẽ học rằng các khớp bị che khuất thì biến mất khỏi khung hình, làm mất khả năng dự đoán khớp bị che (occluded keypoint estimation) trên ảnh thực tế.

### Ca 2 - ảnh `train_09.jpg`, người thứ `1`, khớp `right_hip`

- Mơ hồ ở chỗ nào: Người mặc áo thụng trùm qua cạp quần, không có bất kỳ mốc bề mặt nào của xương chậu; phân vân vị trí đặt chấm hông sao cho đúng tâm giải phẫu mà không bị kéo lệch lên eo hay xuống đùi.
- Bạn quyết thế nào: Chọn `v = 1` (hoặc ước lượng mốc thân), đặt chấm tại vị trí mốc mấu chuyển lớn xương đùi ước lượng nằm phía dưới cạp quần một khoảng cân đối với hông trái.
- Vì sao: Hông là điểm nối trọng yếu giữa thân và chân; dù bị quần áo che phủ, tư thế đứng thẳng cho phép suy đoán chính xác tâm xoay của khớp háng dựa vào trục chịu lực của chân phải.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu chấm tùy tiện theo nếp gấp áo hoặc kéo lệch lên thắt lưng, model sẽ học sai tỷ lệ khung xương (thân bị co ngắn hoặc chân bị kéo dài bất thường), làm giảm mạnh điểm OKS.

### Ca 3 - ảnh `train_13.jpg`, người thứ `1`, khớp `các khớp chi dưới (hông, gối, cổ chân)`

- Mơ hồ ở chỗ nào: Người đứng ở sát mép trái ảnh (`x ≈ 0.09`), chỉ nhìn thấy đầu và vai ngực, toàn bộ nửa dưới cơ thể bị cắt cụt ra ngoài khung ảnh; phân vân giữa việc bỏ qua người này hay gán skeleton, và các khớp chân bị cắt thì để cờ gì.
- Bạn quyết thế nào: Vẫn gán skeleton cho người này; các khớp thấy rõ ở thân trên gán `v = 2`/`v = 1`, còn toàn bộ các khớp chân bị cắt ra ngoài mép ảnh thì gắn cờ `v = 0` (Outside) và không đặt chấm.
- Vì sao: Đối tượng vẫn đủ kích thước nhận diện người trong ảnh; các khớp chân hoàn toàn nằm ngoài không gian bức ảnh (không có pixel nào chứa thông tin) nên bắt buộc tuân thủ định nghĩa `v = 0`.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu cố tình chấm điểm ước lượng trong ảnh cho các khớp đã rơi ra ngoài mép ảnh, model sẽ bị ép học sai tỷ lệ cơ thể (bị co rúm biến dạng vào trong khung) hoặc sinh ra dự đoán ảo trôi nổi ngoài thực tế.

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `left_ear` (bạn `39%` / họ `0%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**: Chủ yếu là **guideline chưa rõ** - hai bên chưa thống nhất rõ ràng quy chuẩn: khi tai bị tóc hoặc mũ che khuất một phần thì phải đặt chấm ước lượng với cờ `v = 1` hay coi là không nhìn thấy rồi để `v = 0`/`v = 2`.
- Luật mới bổ sung vào mục 2 sau khi thống nhất: Với tai bị tóc hoặc mũ che một phần: nếu vẫn xác định được trục khuôn mặt và vị trí tương đối qua mắt/mũi thì bắt buộc chấm điểm tại vị trí giải phẫu ước lượng và gắn cờ `v = 1` (Occluded); chỉ gắn `v = 0` (Outside) khi toàn bộ phần đầu đã bị cắt ra ngoài mép ảnh.
