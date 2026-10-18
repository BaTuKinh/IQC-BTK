# Nội kiểm xét nghiệm (IQC)

App web một file (`index.html`), miễn phí, không cần cài đặt, không cần server. Theo dõi nội kiểm cho nhiều thiết bị, mỗi thiết bị nhiều xét nghiệm.

## Tính năng

- **Thiết bị → Xét nghiệm → Mức nội kiểm** (số lô, mean, SD, đơn vị, TEa theo % hoặc theo đơn vị).
- **Định lượng**: biểu đồ Levey-Jennings từng mức, biểu đồ z-score gộp các mức, quy tắc Westgard 1-2s (cảnh báo), 1-3s, 2-2s, R-4s, 4-1s, 10x (bật/tắt từng quy tắc), kiểm tra TEa, thống kê CV%, Bias%, Sigma.
- **Định tính**: so với kết quả mong đợi, tỷ lệ đạt.
- **Định tính có thang đo** (Âm tính, ±, 1+, 2+…): biểu đồ bậc thang, dải sai lệch cho phép (±n bậc), cảnh báo xu hướng.
- **Sự kiện thiết bị** (nút “＋ Sự kiện”): bảo trì, hiệu chuẩn, sửa chữa/thay linh kiện, đổi lô thuốc thử, đổi lô QC. Hiện thành vạch đứng có nhãn (BT, HC, SC, TT, LQ) trên biểu đồ và nằm xen trong bảng kết quả. Mặc định, hiệu chuẩn/sửa chữa/đổi lô sẽ **bắt đầu chuỗi quy tắc mới** (2-2s, 4-1s, 10x không đếm xuyên qua sự kiện); bảo trì định kỳ thì không.
- **Lý do chạy QC** khi nhập kết quả (Thường quy, Sau bảo trì, Sau hiệu chuẩn, Chạy lại sau khắc phục…). App tự gợi ý lý do sau khi bạn ghi sự kiện hoặc sau một lần QC vi phạm.
- **Gợi ý nguyên nhân và xử trí** (nút 💡) cho từng quy tắc vi phạm, kèm quy trình chung; **ghi hành động khắc phục** (nút ⚑) với các mẫu câu nhanh. Nội dung chỉ mang tính tham khảo, luôn ưu tiên SOP của phòng và hướng dẫn nhà sản xuất.
- Xuất CSV, sao lưu/nạp JSON, đồng bộ với GitHub.

## Cách dùng khuyến nghị: GitHub miễn phí, nhiều máy

Tách **app** (public, không chứa dữ liệu) và **dữ liệu** (private):

1. Repo `app` (**Public**): chỉ upload `index.html` và `README.md`. Bật Pages: Settings → Pages → Deploy from a branch → `main` / root. App chạy tại `https://<tên-bạn>.github.io/<tên-repo>/`.
2. Repo `data` (**Private**): để trống hoặc thêm `data.json`.
3. Tạo **fine-grained token** (GitHub → Settings → Developer settings → Personal access tokens), chọn đúng repo `data`, quyền *Contents: Read and write*.
4. Mở địa chỉ app trên máy tính bàn phòng lab → **Dữ liệu / GitHub**: nhập `tên-bạn/tên-repo-data`, nhánh `main`, đường dẫn `data.json`, dán token, bấm **Tải từ GitHub** (nếu đã có dữ liệu) hoặc **Đẩy lên GitHub**. Bật “Tự động đẩy” để mỗi lần lưu kết quả được sao lưu lên GitHub sau vài giây.
5. Các lần sau chỉ cần mở app: nếu GitHub có bản mới hơn, app tự hỏi và cập nhật.

### Chuyển dữ liệu đang có ở máy khác sang máy tính bàn

Trên máy cũ: **Dữ liệu / GitHub → Đẩy lên GitHub** (và nên **Tải xuống JSON** để sao lưu). Trên máy tính bàn: mở app, nhập cấu hình GitHub, bấm **Tải từ GitHub**. Không dùng GitHub: tải JSON ở máy cũ, mang sang bằng USB hoặc Drive, rồi **Nạp từ file JSON** ở máy mới.

## Lưu ý quan trọng

- Dữ liệu làm việc nằm trong trình duyệt của từng máy (localStorage); GitHub là bản đồng bộ/sao lưu. Đừng xóa dữ liệu duyệt web của trình duyệt đang dùng app mà chưa đẩy lên GitHub.
- Nên chọn **một máy chính** để nhập kết quả. Nếu nhập ở nhiều máy, app sẽ cảnh báo khi GitHub có bản mới hơn trước khi ghi đè, nhưng không tự gộp hai bản.
- Token chỉ lưu trong trình duyệt của máy đó. Mỗi người dùng nên có token riêng và được mời làm collaborator của repo dữ liệu; khi cần thu hồi chỉ cần gỡ collaborator hoặc xóa token.
- `data.json` đi kèm là **dữ liệu mẫu** để thử. Không đưa file này vào repo dữ liệu thật; dùng “Xóa toàn bộ dữ liệu trong trình duyệt” để bắt đầu từ trống.
- Đổi mean/SD hoặc số lô của một mức sẽ mở chuỗi biểu đồ mới; kết quả cũ vẫn giữ thông số lúc nhập.
