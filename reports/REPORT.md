# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Đinh Công Minh   Nhóm: K4-L2   Ngày: 16/09/2026

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 28 |
| v=2 / v=1 / v=0 | 367 / 78 / 31 |
| Thời gian trung bình mỗi ảnh | 4 phút/ảnh |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. left_ear (39%)
2. left_eye (29%)
3. left_wrist (25%)

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->

Không hoàn toàn. Hai khớp `left_ear` (39%) và `left_eye` (29%) có tỉ lệ v=1 cao chủ yếu do góc nhìn thị giác (người quay mặt nghiêng hoặc quay lưng) dẫn tới việc bị tóc hoặc sống mũi che khuất; tuy nhiên việc xác định vị trí giải phẫu của mắt và tai lại tương đối dễ dàng nhờ căn đối xứng qua trục mặt và sống mũi. Ngược lại, khớp thực sự khó gán nhất là khớp hông (`left_hip`/`right_hip`) và cổ tay (`left_wrist`): hông hoàn toàn không có mốc bề mặt nhìn thấy được khi mặc quần áo rộng hoặc áo khoác, buộc phải ước lượng vị trí xương chậu từ cạp quần và dáng đứng; còn cổ tay khi bị khuất sau lưng hoặc sau vật thể dễ gây tranh chấp giữa việc ước lượng vị trí (v=1) hay đánh mất dấu.

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | 0.9410 | 0.9532 |
| OKS@0.50 | 0.9655 | 0.9655 |
| OKS@0.75 | 0.9655 | 0.9655 |
| Lỗi `dao_trai_phai` | 0 | 0 |
| Lỗi `nham_nguoi` | 0 | 0 |
| Lỗi `xoa_khop_bi_che` | 0 | 0 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- train_09.jpg + người 1 + right_hip: dịch chuyển toạ độ điểm hông phải xuống dưới 42 px cho đúng tâm xương chậu giải phẫu, khắc phục cảnh báo lệch nhẹ.
- train_01.jpg + người 1 + left_wrist: kiểm tra lại vị trí cổ tay trái bị vạt áo che, căn chỉnh lại tọa độ ước lượng dựa theo trục cẳng tay và gắn đúng cờ v=1.
- train_13.jpg + người 2 + left_knee, left_ankle: rà soát lại toạ độ chân bị che khuất một phần bởi người đứng phía trước để khớp chuẩn với đường xương cẳng chân.

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

<!-- Nếu không có lỗi, ghi rõ “Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.” -->

Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh. Toàn bộ nhãn đã được kiểm tra kỹ lưỡng theo nguyên tắc đặt góc nhìn theo cơ thể người (không theo hướng nhìn của ảnh) và được kiểm chứng qua công cụ `visualize_pose.py` trước khi khoá nhãn.

## 3. Kiểm chéo

Bạn cùng nhóm: Đối chiếu theo Baseline / Cặp kiểm chéo

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn | Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| --- | ---: | ---: | ---: | --- |
| left_ear | 39% | 0% | 39% | Guideline chưa thống nhất rõ cách xử lý khi tai bị tóc/mũ che |
| left_eye | 29% | 0% | 29% | Guideline: góc nghiêng sống mũi che mắt một bên nên chấm v=1 hay bỏ qua |
| left_wrist | 25% | 0% | 25% | Gán sai: bên đối chiếu có xu hướng để v=0/xoá khớp thay vì v=1 ước lượng |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

- Với tai bị tóc hoặc mũ che một phần: nếu vẫn xác định được vị trí đầu và trục khuôn mặt qua mắt/mũi thì bắt buộc chấm điểm tại vị trí giải phẫu ước lượng và gắn cờ `v = 1` (Occluded); chỉ gắn `v = 0` (Outside) khi toàn bộ phần đầu đã bị cắt ra ngoài mép ảnh.

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 | 0.8450 | 0.8450 | 0.0000 |
| pose_mAP50-95 | 0.6853 | 0.6908 | +0.0055 |
| pose_precision | 0.9734 | 0.9792 | +0.0058 |
| pose_recall | 0.8462 | 0.8462 | 0.0000 |
| box_mAP50-95 | 0.8119 | 0.8041 | -0.0078 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?

`pose_mAP50-95` tăng từ 0.6853 lên 0.6908 (tăng +0.0055, tức +0.55%), đồng thời `pose_precision` tăng từ 0.9734 lên 0.9792 (+0.0058). Bộ 20 ảnh được gán nhãn nhất quán, không có lỗi đảo trái/phải và chấm đúng cờ v=1 cho khớp che khuất đã giúp model định vị keypoint chính xác hơn ở các ngưỡng OKS cao. Ngược lại, `box_mAP50-95` giảm nhẹ (-0.0078) do kích thước tập train quá nhỏ (20 ảnh) khiến model bị overfit nhẹ vào phân bố bounding box của tập này so với độ khái quát đa dạng của pretrain COCO gốc.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?

Chênh lệch giữa `box_mAP50-95` (0.8041) và `pose_mAP50-95` (0.6908) là 0.1133 (11.33%). Model tìm người dễ hơn tìm khớp rất nhiều. Lý do là bounding box chỉ cần bắt được vùng hình chữ nhật bao quanh cơ thể dựa trên các đặc trưng toàn cục (đầu, thân, chân) với dung sai diện tích IoU tương đối rộng. Ngược lại, pose estimation đòi hỏi xác định chính xác 17 toạ độ giải phẫu cục bộ (cổ tay, mắt cá, khớp hông...), các khớp này thường xuyên bị biến dạng phi tuyến tính theo cử động, bị che khuất và tính sai số khắt khe theo từng bán kính pixel của OKS.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):

Ở ảnh test có người ngồi khuất hoặc góc chụp chéo (ví dụ trường hợp các khớp chân bị che): Model mắc lỗi **lệch nhẹ** ở khớp cổ chân/mắt cá chân (chấm lệch 5-10 pixel so với mốc mắt cá thật do nếp gấp quần che khuất) và mắc lỗi **trượt hẳn** ở khớp cổ tay bị che sau lưng (model không bắt được manh mối thị giác nên đưa dự đoán trượt ra vùng nền bên hông).

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?

Ảnh có OKS thấp nhất giữa nhãn và model là `train_06.jpg` (OKS đạt mức xấp xỉ ~0.9041). Trong bức ảnh này, nhãn của tôi đúng hơn. Căn cứ vào thị giác: người trong ảnh có phần cánh tay và chân bị che khuất một phần do tư thế chuyển động; tôi đã dựa vào trục xương cẳng tay và hướng đầu gối để ước lượng vị trí giải phẫu gắn cờ v=1 hợp lý. Model do thiếu thông tin biên trực tiếp nên đã dự đoán điểm co cụm vào phần thân nhìn thấy được, dẫn tới lệch toạ độ so với giải phẫu học thực tế.

5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?

Có, ảnh `train_13.jpg` và `train_15.jpg` đều là những ảnh mà cả người gán lẫn model đều đạt điểm OKS thấp nhất (khoảng 0.89 - 0.90). Điều này chỉ ra rằng các bức ảnh này có **độ mơ hồ thị giác cao (high visual ambiguity)**: độ tương phản ánh sáng thấp, nhiều người đứng chồng lấn che khuất nhau, hoặc đối tượng nằm sát mép ảnh bị cắt ngang thân thể. Đây là các "hard cases" điển hình mà cả thị giác con người lẫn mạng nơ-ron đều gặp khó khăn nếu không có bối cảnh toàn vẹn.

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->

Trong ảnh `train_01.jpg`, người thứ 1, khớp cổ tay trái (`left_wrist`):
Khi gán nhãn, khớp cổ tay trái của nhân vật bị che khuất một phần bởi thân mình và vạt áo khoác khi tay buông tự nhiên hơi lùi về sau. Tuy nhiên, căn cứ thị giác cho thấy toàn bộ cẳng tay trên và khớp khuỷu tay trái (`left_elbow`, v=2) vẫn nhìn thấy rất rõ, đồng thời toàn bộ người này nằm trọn vẹn ở trung tâm bức ảnh chứ không hề chạm mép viền. Do khớp chắc chắn vẫn nằm trong không gian ảnh nhưng bị cản trở tầm nhìn bởi vật thể/thân mình, tôi quyết định chọn trạng thái `v = 1` (Occluded) và đặt chấm ước lượng theo trục kéo dài của cẳng tay, thay vì chọn `v = 0` (Outside).
