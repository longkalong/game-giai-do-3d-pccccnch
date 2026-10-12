# Bàn giao và triển khai game PCCC 3D v1.261011-11

## Mục tiêu

Đưa bản game cục bộ mới nhất **v1.261011-11** lên repository `longkalong/game-giai-do-3d-pccccnch`, thay cho bản đang phát hành cũ. Bản v1.261011-11 đã tích lũy toàn bộ thay đổi từ v1.261011-6 đến v1.261011-11; không cần ghép từng bản trung gian.

## Bộ file cần nhận

Người triển khai cần được gửi kèm:

1. **File game mới nhất:** `game-gi-i-3d.html`
   - Đổi tên thành `index.html` khi đặt vào thư mục đang được GitHub Pages xuất bản.
   - Kích thước bản đã chốt: **140.412 byte**.
   - SHA-256: `c01543892ec72d9ae72c7d20362450e96f3ef940cf8881620134cd242bfc7b11`.
   - Trong thẻ `<title>` và huy hiệu giao diện phải hiện `v1.261011-11`.

2. **Thư mục model:** `assets/models/`
   - Nếu repository hiện tại đã có đủ model và tên file không đổi, chỉ cần thay `index.html`.
   - Nếu triển khai mới hoặc thiếu model, chép nguyên thư mục `assets/models/` vào đúng cấp bên cạnh `index.html`.
   - Giữ nguyên cả thư mục model cũ trong repository; không xóa file chỉ vì không thấy dùng ngay.

Các model mà bản HTML hiện tại gọi trực tiếp:

```text
assets/models/ban-do.glb
assets/models/ban-gaming.glb
assets/models/cua-thoat-hiem.glb
assets/models/ghe-gaming.glb
assets/models/hong-nuoc.glb
assets/models/imac-de-ban.glb
assets/models/iphone.glb
assets/models/lang-da-nang.glb
assets/models/may-in.glb
assets/models/ngon-lua-moi.glb
assets/models/tu-chua-chay.glb
assets/models/tu-dien.glb
assets/models/voi-chua-chay.glb
assets/models/xo-nuoc.glb
```

Ngoài ra, nếu repository đã có `lang-chua-chay.glb` thì giữ lại.

---

## Nội dung cập nhật theo phiên bản

### v1.261011-6

- Loại bỏ hoàn toàn đường vòi chạy dưới sàn ở hành lang và văn phòng.
- Làm lại nước phun từ đúng đầu lăng để dòng nước dễ nhìn thấy hơn.

### v1.261011-7

- Sau khi tủ họng nước đã mở, tủ trở thành đối tượng không tương tác: không prompt, không viền xanh, không tooltip và không thông báo lặp lại.
- Chuyển trọng tâm tương tác sang lăng và van.
- Thử nghiệm chùm nước xanh tập trung từ đầu lăng, sau đó nở rộng ở xa; loại bỏ cảm giác tia laser cứng.

### v1.261011-8

- Chỉ khi ngắm vào tủ đóng mới hiện prompt và viền của tủ.
- Mở tủ xong thì ngừng target tủ.
- Hiện rõ hai lựa chọn:
  - **1 — Lấy lăng vòi:** lăng biến mất khỏi giá treo và xuất hiện trên tay ở góc nhìn thứ nhất.
  - **2 — Mở van nước:** van nằm ngoài tủ, trên tường cạnh tủ.
- Khi lấy bình CO₂, bình bột hoặc bình nước, model bình xuất hiện trên tay và bình dưới sàn biến mất.

### v1.261011-9

- Sửa tình trạng đã lấy lăng nhưng bấm xịt không thấy nước.
- Trong mã hiện tại, chọn **1 — Lấy lăng vòi** đồng thời đặt van sang trạng thái mở để người chơi không bị kẹt. Vì giao diện lựa chọn tự ẩn khi van đã mở, bước 2 không còn là thao tác bắt buộc sau khi chọn 1.

### v1.261011-10

- Tăng độ mạnh và độ rõ của dòng nước phun từ lăng.

### v1.261011-11 — bản cần triển khai

- Nước bắn theo kiểu chùm “đạn nước”: các giọt xanh đậm bay nhanh, chụm sát ở đầu lăng và có quỹ đạo cong nhẹ.
- Tốc độ giọt nước khoảng **24–31 m/s**.
- Khi chạm sàn, tường, bàn, tủ, cửa hoặc vùng đám cháy, giọt nước chuyển sang pha văng tóe và không xuyên qua vật thể.
- Dòng nước nhìn thấy được cắt tại bề mặt va chạm.
- Có thể đứng xa để phun; cơ chế xác định trúng lửa được nới rộng, không đòi hỏi ngắm đúng từng pixel.
- Khi nước trúng vùng lửa và người chơi giữ phun, lửa giảm dần tới 0%.

---

## Trạng thái hành vi phải giữ nguyên

### Tủ họng nước

- Tủ đóng: chỉ hiện trạng thái target khi tâm ngắm trúng tủ.
- Sau khi mở: tủ không còn là target và không hiện lại prompt/viền/tooltip.
- Lăng và nhãn số 1 chỉ hiện khi tủ đã mở và người chơi chưa lấy lăng.
- Lấy lăng: lăng trên giá biến mất, lăng cầm tay xuất hiện.
- Van ở ngoài tủ; trạng thái mở van phải hiển thị rõ.

### Vật cầm trên tay

- Chỉ hiện một vật đang cầm tại một thời điểm.
- Cầm lăng thì lăng hiện ở góc nhìn thứ nhất.
- Lấy bình CO₂, bình bột hoặc bình nước thì bình tương ứng xuất hiện trên tay và model dưới sàn biến mất.

### Nước và dập lửa

- Không có bất kỳ đường vòi nào nằm trên sàn.
- Nước phải xuất phát từ đầu lăng, màu xanh đậm, nhìn như chùm giọt bắn nhanh chứ không phải một thanh laser thẳng.
- Giọt nước phải văng tóe ngay tại bề mặt va chạm.
- Phạm vi phun hữu dụng tới khoảng 30 m; vùng nhận trúng lửa rộng khoảng 2,4 m quanh tia ngắm để người chơi có thể đứng xa.
- Khi tia chạm vùng lửa, lửa giảm khoảng 25% mỗi giây và có thể về 0%.
- Bình CO₂/bột ở Level 1 chỉ hạ lửa tới 90%; nếu chưa dùng vòi, lửa có thể phát triển lại. Không thay đổi cơ chế này.

**Lưu ý quan trọng:** Yêu cầu ban đầu mô tả quy trình hai bước riêng biệt: số 1 lấy lăng, số 2 mở van. Tuy nhiên, mã v1.261011-11 hiện tự mở van ngay khi lấy lăng để xử lý lỗi “không có nước”, nên bảng lựa chọn đóng lại và số 2 không còn là bước bắt buộc. Người triển khai chỉ đẩy đúng v1.261011-11 thì không sửa logic này. Nếu chủ dự án muốn quay lại quy trình hai bước, hãy làm thành bản mới và vẫn phải bảo đảm sau bước 2 nước phun nhìn thấy rõ.

---

## Cấu trúc phát hành

Cấu trúc tối thiểu:

```text
<thư mục được GitHub Pages xuất bản>/
├── index.html
└── assets/
    └── models/
        ├── ban-do.glb
        ├── ban-gaming.glb
        ├── cua-thoat-hiem.glb
        ├── ghe-gaming.glb
        ├── hong-nuoc.glb
        ├── imac-de-ban.glb
        ├── iphone.glb
        ├── lang-da-nang.glb
        ├── may-in.glb
        ├── ngon-lua-moi.glb
        ├── tu-chua-chay.glb
        ├── tu-dien.glb
        ├── voi-chua-chay.glb
        └── xo-nuoc.glb
```

Bản HTML thử lần lượt hai đường dẫn model: `assets/models/` rồi `models/`. Nên dùng `assets/models/` theo cấu trúc trên. Nếu model không tải được, game giữ đồ họa khối cơ bản làm phương án dự phòng, nhưng đây không phải trạng thái phát hành mong muốn.

Game tải Three.js, GLTFLoader và font từ CDN nên khi kiểm thử cần có kết nối Internet.

---

## Cách triển khai bằng Git

### 1. Lấy repository

Nếu máy đã cài GitHub CLI và tài khoản có quyền ghi:

```bash
gh repo clone longkalong/game-giai-do-3d-pccccnch
cd game-giai-do-3d-pccccnch
```

Nếu đã có bản clone, vào thư mục đó rồi chạy:

```bash
git pull --ff-only
```

### 2. Xác định đúng nguồn GitHub Pages

Vào **Settings → Pages** trong repository, kiểm tra nhánh và thư mục đang được dùng để phát hành. Không tự đổi cấu hình Pages. Thay file trong đúng thư mục hiện đang xuất bản:

- Nếu Pages dùng thư mục gốc: thay `index.html` ở gốc repository.
- Nếu Pages dùng `/docs`: thay `docs/index.html` và đặt model tại `docs/assets/models/`.
- Nếu Pages dùng nhánh riêng: checkout đúng nhánh đó trước khi chép file.

### 3. Chép bản mới

- Đổi tên `game-gi-i-3d.html` thành `index.html`.
- Chép đè `index.html` cũ tại nguồn Pages.
- Bảo đảm thư mục `assets/models/` nằm cạnh `index.html` và đủ các model nêu trên.
- Không đổi tên file `.glb`; GitHub Pages phân biệt chữ hoa và chữ thường.

### 4. Commit và push

```bash
git status
git add index.html assets/models
git commit -m "Deploy game PCCC 3D v1.261011-11"
git push
```

Nếu nguồn Pages là `/docs`, thay hai đường dẫn trong lệnh `git add` bằng `docs/index.html` và `docs/assets/models`.

Không dùng `git push --force`.

### 5. Chờ triển khai hoàn tất

- Mở tab **Actions** hoặc trang **Deployments** của repository.
- Chỉ coi là hoàn tất khi tác vụ GitHub Pages báo thành công.
- Mở trang game ở cửa sổ riêng tư hoặc tải lại mạnh để tránh cache bản cũ.
- Kiểm tra huy hiệu giao diện phải ghi `v1.261011-11`.

---

## Kiểm thử bắt buộc sau triển khai

### Kiểm tra nhanh giao diện

- Mở game trên máy tính và điện thoại.
- Xác nhận màn hình chọn PC/Mobile và chọn level vẫn hoạt động.
- Xác nhận tiêu đề hoặc badge ghi `v1.261011-11`.
- Mở Developer Tools → Network, lọc `.glb`; không được có lỗi 404 đối với model.

### Kiểm tra luồng Level 1

1. Vào Level 1 và thực hiện phần đầu như bình thường.
2. Dùng bình CO₂ hoặc bình bột; xác nhận bình xuất hiện trên tay, biến mất dưới sàn và lửa chỉ giảm tới 90%.
3. Mở cửa, đi thật qua cửa ra hành lang.
4. Ngắm vào tủ họng nước; xác nhận tủ chỉ hiện khi đang target.
5. Mở tủ; xác nhận tủ lập tức mất target, không còn prompt hoặc viền xanh.
6. Xác nhận lựa chọn **1 — Lấy lăng vòi** và **2 — Mở van nước** hiện rõ.
7. Chọn 1; xác nhận lăng mất khỏi giá và xuất hiện trên tay.
8. Xác nhận không có đường vòi nào chạy trên sàn.
9. Giữ `F` trên máy tính hoặc nút **XỊT** trên điện thoại; nước phải xuất phát từ đầu lăng.
10. Bắn vào sàn, tường, bàn, tủ và cửa; từng giọt phải văng tóe ở điểm chạm, không xuyên vật thể.
11. Đứng xa, ngắm gần vùng đám cháy và giữ phun; lửa phải giảm đều tới 0% mà không cần ngắm chính xác tuyệt đối.
12. Xác nhận thắng khi lửa về 0%.

### Tiêu chí không đạt

Không phát hành nếu gặp một trong các lỗi sau:

- Trang vẫn hiện phiên bản cũ.
- Lăng đã lấy nhưng vẫn còn trên giá.
- Lăng hoặc bình không xuất hiện trên tay.
- Tủ đã mở nhưng vẫn bị target hoặc vẫn hiện prompt.
- Có vòi nằm dưới sàn.
- Bấm xịt không có nước.
- Nước thành một thanh laser thẳng, xuyên qua vật thể hoặc không văng tóe.
- Nước chạm lửa nhưng phần trăm lửa không giảm.
- Model `.glb` trả về 404.

---

## Xử lý sự cố

### Trang vẫn là bản cũ

- Kiểm tra commit mới đã nằm trên đúng nhánh Pages chưa.
- Kiểm tra workflow/deployment có thành công không.
- Mở cửa sổ riêng tư hoặc tải lại mạnh.
- Mở mã nguồn trang và tìm `v1.261011-11`; nếu không có, đang phát sai `index.html` hoặc sai nhánh/thư mục.

### Model không hiện

- Kiểm tra chính tả và chữ hoa/thường của tên `.glb`.
- Kiểm tra vị trí `assets/models/` so với `index.html`.
- Dùng Network để tìm lỗi 404.
- Không sửa đường dẫn trong HTML nếu chỉ cần chép đúng cấu trúc file.

### Không có nước

- Xác nhận giao diện đã hiện lăng trên tay.
- Xác nhận đang giữ `F` hoặc nút **XỊT**, không chỉ bấm một lần quá nhanh.
- Trong mã v1.261011-11, khi lấy lăng phải có `hasHoseNozzle=true` và tự chuyển `hoseValveOpen=true`.
- Logic tạo nước chỉ chạy khi `hasHoseNozzle && hoseValveOpen`; nếu một biến bị reset sau khi lấy lăng, nước sẽ không xuất hiện.

### Nước không dập được lửa

- Xác nhận cầu dao đã được ngắt theo luồng chơi.
- Kiểm tra `jetHitsFire` có chuyển sang đúng khi tia đi gần vùng lửa.
- Giữ vùng nhận trúng rộng; không thu hẹp thành ngắm chính xác từng pixel.
- Giữ tốc độ giảm lửa khoảng 25% mỗi giây khi vòi đang phun trúng.

---

## Hoàn tác an toàn

Nếu bản mới gây lỗi nghiêm trọng:

```bash
git log --oneline -5
DEPLOY_COMMIT=$(git log --grep="Deploy game PCCC 3D v1.261011-11" -1 --format=%H)
git revert "$DEPLOY_COMMIT"
git push
```

Dùng `git revert` để giữ lịch sử. Không xóa lịch sử và không force-push.

## Kết quả bàn giao mong đợi

Người triển khai gửi lại:

- Mã commit đã triển khai.
- Ảnh chụp badge `v1.261011-11` trên trang công khai.
- Ảnh hoặc video ngắn xác nhận: tủ mất target sau khi mở, lăng biến mất khỏi giá và hiện trên tay, nước bắn dạng giọt có văng tóe, lửa giảm tới 0%.
- Danh sách lỗi còn lại, nếu có.
