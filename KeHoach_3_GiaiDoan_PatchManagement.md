KẾ HOẠCH 3 GIAI ĐOẠN TRIỂN KHAI GIÁM SÁT PATCH MANAGEMENT
## 🟢 GIAI ĐOẠN 1: TRIỂN KHAI NGAY (Immediate Enablement)
**Mục tiêu:** Thiết lập nhanh cơ bản để thu thập, hiển thị trạng thái patch của toàn bộ hệ thống.

**Hành động:**
- ✅ Onboard toàn bộ server vào Log Analytics Workspace
Azure VM: dùng VM Extension.
On-prem hoặc server không Internet-facing: dùng Azure Arc hoặc MMA agent.
- ✅ Cài đặt Azure Automation Update Management
Liên kết với Log Analytics để bật thu thập thông tin cập nhật.
- ✅ Tạo truy vấn KQL cơ bản
Tổng hợp số bản vá được cài mới (Added) và bị gỡ bỏ (Removed) theo từng máy chủ.
- ✅ Xây dựng Azure Workbook đơn giản
Bảng dữ liệu liệt kê trạng thái từng server.
Highlight server không có thay đổi patch.

## 🟡 GIAI ĐOẠN 2: TĂNG CƯỜNG & TÙY CHỈNH (Enhancement & Customization)
**Mục tiêu:** Tinh chỉnh và mở rộng dashboard, lọc theo nhóm máy chủ, phân tích sâu.

**Hành động:**
- 🔄 Gắn tag cho server theo nhóm (VD: Internet-facing, Internal, Prod, Dev...) để dễ lọc.
- 📊 Nâng cấp Workbook:
Thêm biểu đồ (bar chart, pie chart).
Tạo bộ lọc động (dropdown filters): theo nhóm server, thời gian.
- 🧠 Tùy chỉnh truy vấn KQL nâng cao:
So sánh số patch cũ → patch mới.
Truy vết server liên tục không thay đổi trong 2–3 cycles liên tiếp.
- 🧾 Tích hợp thêm thông tin từ Microsoft Defender for Endpoint (MDE) hoặc Update Compliance để phân tích trạng thái bảo mật liên quan.

## 🔵 GIAI ĐOẠN 3: TỰ ĐỘNG HÓA (Automation & Alerting)
**Mục tiêu:** Giảm thao tác thủ công, tự động cảnh báo và xuất báo cáo định kỳ.

**Hành động:**
- 🚨 Tạo Alert Rule trên Log Analytics:
Nếu TotalChanges == 0 hoặc không có bản vá mới trong 14 ngày → gửi cảnh báo qua email / Microsoft Teams.
- 📅 Tự động hóa báo cáo định kỳ:
Dùng Logic App hoặc Azure Function để gửi file PDF từ Workbook mỗi tuần/tháng.
- 🤖 Tích hợp với Runbook:
Tự động trigger Runbook (ví dụ: kiểm tra pending updates, kick off patch, gửi thông báo lên ITSM ticket).
- 🔁 Kết hợp dữ liệu với vulnerability scan từ MDE hoặc Qualys/Nessus nếu có → mapping patch status với lỗ hổng tồn tại.