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
- **Xuất Excel (.xlsx)**: nút “Excel” ở từng xét nghiệm hoặc “Xuất tất cả Excel” trong mục Dữ liệu; gồm 4 sheet (Kết quả, Thống kê, Sự kiện, Khai báo). Cũng có CSV và sao lưu/nạp JSON.
- **Báo cáo in / lưu PDF** (nút “Báo cáo” trên đầu trang): chọn phạm vi (xét nghiệm, thiết bị, toàn phòng) và kỳ (tháng này, tháng trước, 30 ngày, tất cả). Có biểu đồ, thống kê, danh sách vi phạm kèm hành động khắc phục, sự kiện thiết bị và ô ký tên. Bấm “In / Lưu PDF”.
- **Dùng được trên điện thoại**: giao diện thu gọn (nút ☰ mở danh sách thiết bị), biểu đồ vuốt ngang được, ô nhập chữ lớn. Đồng bộ với máy tính qua GitHub như mô tả bên dưới.

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
- **Sửa kết quả đã nhập**: bấm ✎ ở dòng kết quả (đổi giá trị, ngày giờ, lý do chạy, người thực hiện, ghi chú, hành động khắc phục). Sự kiện thiết bị cũng sửa được bằng ✎. Mọi lần sửa/xóa được ghi vào “Nhật ký chỉnh sửa” dưới bảng kết quả.
- **Sửa Mean / SD / TEa** (nút “Mean/SD/TEa”) có hai chế độ tách biệt: *Sửa lại cho đúng* (nhập sai, áp dụng cả kết quả cũ, biểu đồ liền mạch, không có vạch TS) và *Thông số mới từ bây giờ* (đổi lô, tính lại mean/SD: kết quả cũ giữ thông số cũ, vạch giới hạn đổi bậc tại đường TS và ghi chú trên biểu đồ). Nút “Khai báo” chỉ còn dùng cho tên, đơn vị, thang, quy tắc và thêm/xóa mức; mean/SD/lô/TEa của mức đã có kết quả được khóa ở đó. Thay đổi trong quy trình chạy QC (bảo trì, hiệu chuẩn…) vẫn ghi bằng “＋ Sự kiện”.
- Biểu đồ z-score trải đều theo từng lần chạy; biểu đồ Levey-Jennings vẽ vạch giới hạn dạng bậc thang, có ghi sẵn “TB … · SD …” của từng đoạn.

## Dùng trên điện thoại và đồng bộ với máy tính

1. Mở địa chỉ GitHub Pages của app trên điện thoại (cùng link với máy tính).
2. **Dữ liệu / GitHub**: nhập cấu hình repo dữ liệu và token (mỗi thiết bị nhập một lần), bấm **Tải từ GitHub**.
3. iPhone: Safari → Chia sẻ → “Thêm vào MH chính”. Android: Chrome → ⋮ → “Thêm vào màn hình chính”.
4. Nhập kết quả trên điện thoại rồi bật “Tự động đẩy” (hoặc bấm Đẩy lên GitHub). Máy tính bàn mở app sẽ tự hỏi cập nhật bản mới.
5. In PDF trên điện thoại: mở Báo cáo → In / Lưu PDF (iPhone: Chia sẻ → In, rồi chụm hai ngón để xem PDF và lưu).

Lưu ý: token lưu trên điện thoại, nên đặt khóa màn hình; nếu mất máy, thu hồi token trong GitHub. Không nên nhập cùng lúc trên hai thiết bị.

## Cài như một ứng dụng (Windows, Mac, điện thoại)

App là PWA nên cài được từ trình duyệt, miễn phí, không cần file .exe/.dmg.

1. Upload **toàn bộ** các file này vào repo app (cùng thư mục gốc): `index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`, `apple-touch-icon.png` (và README.md).
2. Mở https://batukinh.github.io/IQC-BTK/ bằng **Chrome hoặc Edge**, bấm biểu tượng “Cài đặt” (hình màn hình có mũi tên) ở cuối thanh địa chỉ → Cài đặt. Mac + Safari: Chia sẻ → Thêm vào Dock. iPhone: Safari → Chia sẻ → Thêm vào MH chính. Android: Chrome → ⋮ → Cài đặt ứng dụng.
3. App có biểu tượng riêng, mở trong cửa sổ riêng và mở được khi mất mạng. Khi có mạng, app tự lấy bản mới nhất.

Lưu ý: dữ liệu của bản cài và của tab trình duyệt thường dùng chung một nơi lưu trên cùng máy, nhưng mỗi máy/điện thoại có dữ liệu riêng, đồng bộ qua GitHub. Sau khi cập nhật app, nếu chưa thấy thay đổi, đóng hẳn app rồi mở lại (hoặc Ctrl+F5).

## Nhập dữ liệu từ Excel / CSV

**Dữ liệu → Nhập từ Excel / CSV…** (hoặc bấm “Tải file Excel mẫu” để lấy file đúng định dạng). Hỗ trợ `.xlsx` và `.csv`; chưa hỗ trợ `.xls` cũ (mở bằng Excel, lưu lại thành .xlsx).

Chỉ cần **một bảng**, mỗi dòng là một kết quả QC, hàng đầu là tiêu đề:

| Cột | Bắt buộc | Ghi chú |
|---|---|---|
| Thiết bị, Xét nghiệm, Mức | Có | Chưa có trong app thì tự tạo |
| Ngày giờ | Có | Ô ngày giờ của Excel hoặc chữ dd/mm/yyyy hh:mm |
| Kết quả | Có | Số (định lượng) hoặc chữ trong thang (định tính, thang đo) |
| Loại | Nên có | Định lượng / Định tính / Thang đo; bỏ trống thì đoán theo kết quả |
| Mean, SD | Định lượng | Ghi ở dòng đầu của mỗi mức là đủ; SD > 0 |
| Số lô, Đơn vị, TEa, Đơn vị TEa | Không | TEa ghi số, Đơn vị TEa là % hoặc đơn vị đo |
| Kết quả mong đợi, Thang kết quả, Sai lệch cho phép (bậc) | Định tính / thang đo | Thang: các giá trị từ thấp đến cao, cách nhau bằng dấu phẩy |
| Lý do chạy QC, Người thực hiện, Ghi chú, Hành động khắc phục | Không | |

- Trước khi nhập, app hiện bản xem trước (số kết quả, thiết bị/xét nghiệm/mức mới, dòng lỗi kèm số dòng). Dòng lỗi bị bỏ qua, dòng đúng vẫn nhập.
- Dữ liệu hiện có được giữ nguyên, chỉ thêm. Dòng trùng (cùng xét nghiệm, mức, thời gian, kết quả) bị bỏ qua nên nhập lại cùng file không bị nhân đôi.
- File do chính app xuất (Xuất Excel) nhập lại được, gồm cả sheet “Khai báo” và “Sự kiện”.
- Nếu một mức có mean/SD khác nhau giữa các dòng, kết quả cũ giữ thông số riêng của dòng đó và nằm ở chuỗi biểu đồ riêng (giống khi đổi lô).
