# Nội kiểm xét nghiệm (IQC)

App web một file (`index.html`, không cần cài đặt, không cần server) để theo dõi nội kiểm xét nghiệm cho nhiều thiết bị, mỗi thiết bị nhiều xét nghiệm.

## Tính năng

- **Thiết bị → Xét nghiệm → Mức nội kiểm** (số lô, mean, SD, đơn vị, TEa theo % hoặc theo đơn vị).
- 3 loại xét nghiệm:
  - **Định lượng**: biểu đồ Levey-Jennings từng mức (±1/2/3 SD) và biểu đồ z-score gộp các mức; quy tắc Westgard 1-2s (cảnh báo), 1-3s, 2-2s (trong mức và liên mức), R-4s, 4-1s, 10x (bật/tắt từng quy tắc); kiểm tra TEa; thống kê n, mean, SD, CV%, Bias%, Sigma.
  - **Định tính**: biểu đồ theo dõi kết quả so với kết quả mong đợi, tỷ lệ đạt.
  - **Định tính có thang đo** (vd Âm tính, ±, 1+, 2+, 3+): biểu đồ bậc thang, dải sai lệch cho phép (±n bậc), cảnh báo khi sát giới hạn hoặc lệch cùng phía 4 lần liên tiếp.
- Ghi **hành động khắc phục** cho kết quả vi phạm; xuất CSV; sao lưu/nạp JSON.
- Đồng bộ dữ liệu với repo GitHub (file `data.json`) ngay trong app.

## Đưa lên GitHub và dùng trên nhiều thiết bị

1. Tạo repo mới (ví dụ `iqc`), đưa 3 file `index.html`, `data.json`, `README.md` lên nhánh `main`.
2. Vào **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*, Branch = `main` / `(root)`. Sau ít phút app chạy tại `https://<tên-bạn>.github.io/iqc/`.
3. Tạo **fine-grained personal access token** (GitHub → Settings → Developer settings), chỉ chọn đúng repo này, quyền *Contents: Read and write*.
4. Mở app → **Dữ liệu / GitHub**, nhập repo (`tên-bạn/iqc`), nhánh, đường dẫn `data.json`, token → **Đẩy lên GitHub** / **Tải từ GitHub**. Bật “Tự động đẩy” nếu muốn mỗi lần nhập kết quả tự lưu lên repo.
5. Trên thiết bị khác: mở cùng địa chỉ, nhập cấu hình GitHub một lần, bấm **Tải từ GitHub**.

## Lưu ý

- Dữ liệu làm việc nằm trong trình duyệt (localStorage); GitHub là nơi sao lưu và đồng bộ. Khi dùng nhiều máy, luôn **Tải từ GitHub** trước khi nhập để tránh ghi đè.
- Token chỉ lưu trong trình duyệt của bạn. Không dùng repo public nếu dữ liệu nhạy cảm; hãy dùng repo **private** (khi đó GitHub Pages cần gói trả phí, hoặc chỉ mở `index.html` trực tiếp từ máy).
- `data.json` đi kèm là **dữ liệu mẫu** để thử; xóa bằng nút “Xóa toàn bộ dữ liệu” rồi đẩy lên để bắt đầu dữ liệu thật.
- Đổi mean/SD hoặc số lô của một mức sẽ mở chuỗi biểu đồ mới; kết quả cũ vẫn giữ thông số lúc nhập.
