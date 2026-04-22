# RE-ROS — Real Estate Revenue Operating System
## Specification

**Version:** 1.0  
**Ngày:** 2026-04-22  
**BA:** Claude (AI Business Analyst)  
**Status:** 🟡 Chờ khách confirm  

---

## 1. Tổng quan

### 1.1. Mục đích

RE-ROS (Real Estate Revenue Operating System) là hệ thống tích hợp quản lý toàn diện dành cho doanh nghiệp môi giới bất động sản, bao gồm CRM bán hàng, marketing automation, quản lý nội dung, vận hành hợp đồng và lớp AI hỗ trợ tăng trưởng. Hệ thống chuẩn hóa toàn bộ vòng đời khách hàng từ Lead → Deal → Contract → After-sale, đồng thời tối ưu hiệu suất đội sale và hiệu quả marketing trên một nền tảng dữ liệu thống nhất.

Mục tiêu cốt lõi là biến RE-ROS thành "hệ điều hành tăng trưởng" cho doanh nghiệp — nơi mọi hoạt động bán hàng, marketing và vận hành đều có thể đo lường, tối ưu và tự động hóa theo dữ liệu thực tế.

### 1.2. Đối tượng người dùng

- **Primary:** Nhân viên sale BĐS (Sale Member, Sale Leader) — làm việc cả tại văn phòng lẫn ngoài thực địa, thường xuyên dùng điện thoại, cần giao diện đơn giản để cập nhật lead nhanh
- **Secondary:** Marketing team (quản lý campaign, content, landing page), bộ phận vận hành (hợp đồng, thanh toán, hoa hồng), Ban điều hành (xem báo cáo tổng hợp)
- **External:** Affiliate/Referrer bên ngoài (KOL, môi giới tự do), Khách hàng mua bất động sản

### 1.3. Mục tiêu kinh doanh

- Theo dõi và cải thiện tỉ lệ chuyển đổi Lead → Deal (có báo cáo đo đếm được theo thời gian thực)
- Đo và giảm thời gian xử lý lead trung bình (từ lúc lead vào đến lúc được liên hệ lần đầu)
- Chuẩn hóa quy trình bán hàng để giảm phụ thuộc vào kinh nghiệm cá nhân của từng sale
- Tự động hóa phân bổ lead và nhắc lịch chăm sóc, giảm lead bị bỏ sót
- Minh bạch hóa hoa hồng theo cấu trúc MLM, tránh tranh chấp nội bộ
- Tạo nền tảng nội dung SEO để giảm CPL từ paid ads về trung hạn

### 1.4. Phạm vi

**In-scope (phải làm — theo phase):**

*Phase 1 — Hệ thống quản lý lõi:*
- Quản lý user & phân quyền
- Quản lý Lead (toàn bộ vòng đời)
- Quản lý dự án & sản phẩm BĐS
- Customer 360
- Sale Kit (tài liệu tư vấn)
- Quản lý hợp đồng & thanh toán manual
- Quản lý hoa hồng MLM
- Calendar & Site Visit (đặt lịch xem nhà)
- Workflow automation cơ bản
- Dashboard & báo cáo (role-based, real-time, export Excel/PDF)

*Phase 2 — Tích hợp ngoài & Marketing:*
- Đồng bộ lead từ Facebook/Google Ads (webhook + CSV import)
- Landing page system
- Campaign management
- Omnichannel chat (Zalo OA, Messenger, Website chat)
- Affiliate / Referral system
- Email cá nhân qua Gmail Workspace
- Google Calendar sync

*Phase 3 — Website vệ tinh & SEO:*
- CMS Global
- 5 website vệ tinh (domain riêng)
- SEO targeting vùng ven: Tây Ninh, Long An, Bình Dương, Đồng Nai

*Phase 4+ — AI & Intelligence (sau phase 3):*
- Lead Scoring tự động
- AI Sales Assistant
- AI Content Engine
- Market Intelligence

**Out-of-scope (KHÔNG làm ở phase này):**
- Tích hợp ngân hàng / cổng thanh toán online (VNPay, MoMo...)
- ERP kế toán đầy đủ, webhook sang hệ thống kế toán
- Mobile app native (sẽ bổ sung sau)
- Multi-tenant / SaaS (hệ thống chỉ cho 1 công ty)
- E-signature điện tử (DocuSign, VNPT eContract)

---

## 2. Yêu cầu chức năng

### 2.1. User roles

| Role | Quyền hạn | Ghi chú |
|------|-----------|---------|
| Super Admin | Toàn quyền hệ thống: cấu hình, xem mọi dữ liệu, quản lý tất cả user | 1 tài khoản duy nhất hoặc rất hạn chế |
| Admin | Quản lý vận hành: user, dự án, hợp đồng, hoa hồng, báo cáo toàn hệ thống | Hoa hồng Admin chỉ nhận khi Sales do Admin recruit |
| Sale Leader | Quản lý đội sale, xem KPI nhóm, phân bổ lead thủ công, xem báo cáo nhóm | Hoa hồng 1–2% từ deal của nhóm mình |
| Sale Member | Tiếp nhận lead, chăm sóc, cập nhật trạng thái, tạo booking, xem KPI cá nhân | Hoa hồng 5% từ deal tự kiếm |
| Marketing | Quản lý campaign, landing page, content, theo dõi lead source | Không truy cập hợp đồng / hoa hồng |

### 2.2. Danh sách tính năng (Feature List)

Ưu tiên MoSCoW: **M** (Must) / **S** (Should) / **C** (Could) / **W** (Won't this phase)

| # | Feature | Priority | Phase |
|---|---------|----------|-------|
| F01 | Quản lý user & phân quyền (RBAC) | M | 1 |
| F02 | Quản lý Lead — vòng đời đầy đủ | M | 1 |
| F03 | Phân bổ lead (tự động rule-based + thủ công) | M | 1 |
| F04 | Quản lý dự án & sản phẩm BĐS | M | 1 |
| F05 | Customer 360 | M | 1 |
| F06 | Quản lý hợp đồng | M | 1 |
| F07 | Tracking thanh toán (manual) | M | 1 |
| F08 | Quản lý hoa hồng MLM | M | 1 |
| F09 | Calendar & Site Visit | M | 1 |
| F10 | Workflow automation cơ bản | M | 1 |
| F11 | Dashboard & Báo cáo (role-based, real-time) | M | 1 |
| F12 | Export báo cáo (Excel, PDF) | M | 1 |
| F13 | Sale Kit (tài liệu tư vấn dùng chung) | S | 1 |
| F14 | KPI tracking & hoạt động sale | S | 1 |
| F15 | Đồng bộ lead từ FB/GG Ads (webhook + CSV) | M | 2 |
| F16 | Landing page system | M | 2 |
| F17 | Campaign management | M | 2 |
| F18 | Omnichannel chat (Zalo OA, Messenger, Web) | M | 2 |
| F19 | Affiliate / Referral system | S | 2 |
| F20 | Email cá nhân qua Gmail Workspace | S | 2 |
| F21 | Google Calendar sync | S | 2 |
| F22 | CMS Global | M | 3 |
| F23 | 5 Website vệ tinh (domain riêng, SEO) | M | 3 |
| F24 | Lead Scoring (AI) | C | 4+ |
| F25 | AI Sales Assistant | C | 4+ |
| F26 | AI Content Engine | C | 4+ |
| F27 | Market Intelligence | C | 4+ |

---

### 2.3. Chi tiết từng tính năng

---

#### F01 — Quản lý User & Phân quyền (RBAC)

**User story:**
> Là **Super Admin**, tôi muốn **tạo, chỉnh sửa, khóa tài khoản cho từng vai trò và gán sale vào dự án**, để **kiểm soát truy cập và phân công làm việc theo dự án**.

**Acceptance criteria:**
- [ ] Tạo / sửa / khóa tài khoản với đầy đủ thông tin (họ tên, email, SĐT, vai trò)
- [ ] Gán 1 user vào nhiều dự án
- [ ] Mỗi role chỉ thấy menu và dữ liệu thuộc quyền mình
- [ ] Đặt lại mật khẩu (admin gửi link reset qua email)
- [ ] Audit log ghi nhận ai tạo / sửa / khóa tài khoản nào, lúc nào

**Edge cases:**
- Khóa tài khoản sale đang có lead đang xử lý → lead phải được reassign trước khi khóa hoặc cảnh báo admin
- Thay đổi role của user đang login → áp dụng ngay lần reload tiếp theo

---

#### F02 — Quản lý Lead (vòng đời đầy đủ)

**User story:**
> Là **Sale Member**, tôi muốn **xem toàn bộ lead được gán cho mình, cập nhật trạng thái và ghi chú sau mỗi tương tác**, để **không bỏ sót khách hàng tiềm năng nào**.

**Vòng đời Lead:**
```
New → Contacted → Qualified → Booking → Negotiation → Won → Lost
```

**Acceptance criteria:**
- [ ] Nhận lead từ nhiều nguồn: ads webhook, landing page form, nhập tay, CSV import
- [ ] Mỗi lead có: thông tin liên hệ, nguồn, dự án quan tâm, trạng thái, sale phụ trách, lịch sử hoạt động
- [ ] Ghi nhận hoạt động: call (thời lượng, kết quả), note, lịch hẹn
- [ ] Nhắc lịch chăm sóc: nếu lead chưa được tương tác trong X ngày (cấu hình được) → thông báo cho sale
- [ ] Tag & phân loại lead tự do (ví dụ: "nóng", "chờ vay vốn", "tái tiếp cận")
- [ ] Tìm kiếm & lọc lead theo: trạng thái, nguồn, dự án, sale phụ trách, tag, khoảng thời gian
- [ ] Bulk action: chuyển trạng thái hàng loạt, reassign hàng loạt

**Edge cases:**
- Lead trùng SĐT / email → hệ thống cảnh báo duplicate, cho phép merge hoặc bỏ qua
- Lead từ webhook lỗi format → vào hàng đợi lỗi, admin xử lý thủ công
- Lead Won → tự động trigger tạo hợp đồng (hoặc gợi ý)

---

#### F03 — Phân bổ Lead (Auto + Manual)

**User story:**
> Là **Sale Leader**, tôi muốn **cấu hình quy tắc phân bổ lead tự động theo dự án**, để **đảm bảo lead luôn được tiếp nhận ngay mà không cần tôi can thiệp thủ công mỗi lần**.

**Acceptance criteria:**
- [ ] Cấu hình rule phân bổ tự động (ít nhất: round-robin, theo dự án, theo workload)
- [ ] Phân bổ thủ công: Leader hoặc Admin kéo thả / chọn sale từ dropdown
- [ ] Thông báo cho sale ngay khi được gán lead mới (in-app + email/Zalo)
- [ ] Lead chưa được assign sau X phút → leo thang thông báo lên Leader

---

#### F04 — Quản lý Dự án & Sản phẩm BĐS

**User story:**
> Là **Admin**, tôi muốn **tạo và quản lý danh mục dự án cùng từng sản phẩm (căn/lô)**, để **sale có thể tra cứu thông tin chính xác và tôi kiểm soát được tình trạng tồn kho**.

**Acceptance criteria:**
- [ ] Tạo / sửa / ẩn dự án với: tên, loại (căn hộ / đất nền / nhà phố / chung cư), vị trí, mô tả, hình ảnh, tài liệu
- [ ] Gán sale vào dự án (1 sale có thể thuộc nhiều dự án)
- [ ] Tạo sản phẩm theo dự án: mã căn/lô, diện tích, giá, tầng/vị trí, hình ảnh mặt bằng
- [ ] Trạng thái sản phẩm: **Available / Reserved / Sold** — cập nhật tự động khi có booking/hợp đồng
- [ ] Xem tổng quan tồn kho theo dự án (bao nhiêu Available / Reserved / Sold)

---

#### F05 — Customer 360

**User story:**
> Là **Sale Member**, tôi muốn **xem toàn bộ lịch sử tương tác, lead, hợp đồng của một khách hàng trên 1 màn hình**, để **không phải lục tìm nhiều nơi khi tư vấn lại**.

**Acceptance criteria:**
- [ ] Tổng hợp: thông tin cá nhân, lịch sử tương tác (call, note, chat), lead history, hợp đồng đã ký, lịch thanh toán
- [ ] Timeline dạng feed, sắp xếp từ mới → cũ
- [ ] Tìm kiếm khách hàng theo tên, SĐT, email

---

#### F06 — Quản lý Hợp đồng

**User story:**
> Là **bộ phận Vận hành**, tôi muốn **tạo hợp đồng từ deal đã chốt, upload file PDF đã ký và theo dõi trạng thái**, để **có hồ sơ pháp lý đầy đủ và dễ tra cứu**.

**Acceptance criteria:**
- [ ] Tạo hợp đồng từ lead Won: tự động điền thông tin khách + sản phẩm
- [ ] Download template hợp đồng chuẩn (file cố định, không chỉnh sửa trong hệ thống)
- [ ] Upload file PDF hợp đồng đã ký scan
- [ ] Trạng thái hợp đồng: **Draft → Signed → Cancelled**
- [ ] Thay đổi trạng thái sản phẩm sang Sold khi hợp đồng Signed
- [ ] Tìm kiếm hợp đồng theo: khách hàng, dự án, sale, trạng thái, khoảng thời gian

---

#### F07 — Tracking Thanh toán (Manual)

**User story:**
> Là **bộ phận Vận hành**, tôi muốn **theo dõi từng đợt thanh toán theo hợp đồng và nhận nhắc lịch khi đến hạn**, để **không để khách trễ hạn mà team không biết**.

**Acceptance criteria:**
- [ ] Cấu hình lịch thanh toán nhiều đợt theo hợp đồng (số đợt, ngày hạn, số tiền mỗi đợt)
- [ ] Ghi nhận thanh toán thủ công: ngày, số tiền, hình thức (chuyển khoản), ghi chú
- [ ] Nhắc lịch tự động trước X ngày đến hạn (thông báo cho vận hành + sale)
- [ ] Trạng thái đợt thanh toán: Pending / Paid / Overdue
- [ ] Export lịch thanh toán ra Excel

---

#### F08 — Quản lý Hoa hồng MLM

**User story:**
> Là **Admin**, tôi muốn **cấu hình chính sách hoa hồng theo cấu trúc MLM và hệ thống tự tính khi hợp đồng hoàn thành**, để **minh bạch thu nhập cho toàn đội sale và tránh tranh chấp**.

**Cấu trúc hoa hồng (mặc định, cấu hình được):**

| Tầng | Nhận khi | Tỉ lệ mặc định |
|------|---------|----------------|
| Sale Member | Tự kiếm khách | 5% |
| Sale Leader | Từ deal của nhóm mình quản lý | 1–2% |
| Admin | Chỉ khi sale do Admin recruit trực tiếp | 0.5% |
| Referrer (Affiliate) | Referral dẫn đến hợp đồng | 0.5% |

**Acceptance criteria:**
- [ ] Cấu hình tỉ lệ % cho từng tầng (Admin có thể thay đổi)
- [ ] Tự động tính hoa hồng khi hợp đồng chuyển sang trạng thái Signed
- [ ] Hiển thị bảng hoa hồng theo: deal, sale, tháng
- [ ] Phân biệt hoa hồng "đã duyệt" / "chờ duyệt" / "đã thanh toán" (manual approval)
- [ ] Export báo cáo hoa hồng ra Excel
- [ ] Sale tự xem hoa hồng của mình; Admin/Leader xem được toàn bộ

**Edge cases:**
- Hợp đồng Cancelled → hoa hồng đã tính bị thu hồi / đánh dấu void
- Sale chuyển nhóm giữa chừng → hoa hồng thuộc về nhóm cũ (tại thời điểm deal)

---

#### F09 — Calendar & Site Visit

**User story:**
> Là **Sale Member**, tôi muốn **đặt lịch xem nhà cho khách và đồng bộ với Google Calendar**, để **không bị trùng lịch và khách nhận được nhắc nhở tự động**.

**Acceptance criteria:**
- [ ] Tạo lịch site visit từ màn hình lead: chọn ngày giờ, dự án, sản phẩm cụ thể
- [ ] Sync lịch sang Google Calendar của sale phụ trách
- [ ] Gửi thông báo nhắc nhở cho khách (email / Zalo — phase 2)
- [ ] Quản lý tour: nhiều khách, nhiều sale, cùng 1 dự án, 1 ngày
- [ ] Xem lịch sale theo ngày/tuần (view dạng calendar)

---

#### F10 — Workflow Automation cơ bản

**User story:**
> Là **Sale Leader**, tôi muốn **cấu hình quy tắc tự động cho các sự kiện thường gặp**, để **đội sale không phải làm thủ công các tác vụ lặp đi lặp lại**.

**Acceptance criteria (rule-based, không code):**
- [ ] Lead mới vào → tự động assign theo rule đã cấu hình
- [ ] Lead chưa tương tác sau X ngày → nhắc sale qua thông báo
- [ ] Booking confirmed → tự động gửi tài liệu Sale Kit cho khách (phase 2 — cần tích hợp email/Zalo)
- [ ] Hợp đồng Signed → tự động tạo lịch thanh toán (nếu template lịch đã cấu hình)
- [ ] Giao diện cấu hình rule dạng "Nếu [sự kiện] thì [hành động]" — không cần viết code

---

#### F11 — Dashboard & Báo cáo (Role-based, Real-time)

**User story:**
> Là **Sale Leader**, tôi muốn **xem dashboard tổng quan hiệu suất nhóm mình theo thời gian thực**, để **có thể can thiệp kịp thời khi nhóm đang trễ KPI**.

**Acceptance criteria:**

*Super Admin / Admin:*
- [ ] Doanh thu theo dự án, theo tháng/quý/năm
- [ ] Conversion funnel toàn hệ thống (Lead → Contacted → Qualified → Won)
- [ ] Hiệu suất từng sale (số lead, booking, deal, hoa hồng)
- [ ] Hiệu quả marketing (CPL, nguồn lead, conversion theo nguồn)
- [ ] Tỉ lệ chuyển đổi, thời gian xử lý lead trung bình

*Sale Leader:*
- [ ] Dashboard nhóm: số lead mới, đang xử lý, won/lost trong kỳ
- [ ] KPI từng member trong nhóm
- [ ] Lead sắp hết hạn chăm sóc (cần theo dõi)

*Sale Member:*
- [ ] Dashboard cá nhân: lead của mình, lịch hôm nay, hoa hồng tháng này
- [ ] Mục tiêu vs. thực tế (nếu được cấu hình KPI)

*Marketing:*
- [ ] Số lead theo chiến dịch, nguồn, landing page
- [ ] CPL theo campaign, conversion rate

**Tất cả dashboard:** Cập nhật real-time (hoặc delay tối đa 5 phút), lọc được theo khoảng thời gian, dự án.

---

#### F12 — Export Báo cáo (Excel, PDF)

**Acceptance criteria:**
- [ ] Mọi bảng báo cáo đều có nút Export Excel (.xlsx)
- [ ] Dashboard tổng hợp có thể xuất PDF (snapshot tại thời điểm export)
- [ ] Báo cáo hoa hồng tháng: export Excel với đầy đủ chi tiết từng deal

---

#### F13 — Sale Kit

**User story:**
> Là **Sale Member**, tôi muốn **truy cập nhanh tài liệu tư vấn (bảng giá, brochure, chính sách) ngay trong hệ thống**, để **không phải lục tìm trong email hay Zalo nhóm**.

**Acceptance criteria:**
- [ ] Admin upload và quản lý tài liệu: Brochure, Bảng giá, Chính sách, Script tư vấn, FAQ — gắn theo dự án
- [ ] Sale xem và download tài liệu theo dự án mình được gán
- [ ] Tài liệu có version (upload mới → đánh dấu "mới nhất", giữ lại bản cũ để tham chiếu)

---

#### F14 — KPI Tracking & Hoạt động Sale

**Acceptance criteria:**
- [ ] Admin / Leader cấu hình KPI tháng cho từng sale: số lead, số booking, doanh thu
- [ ] Hệ thống tự động đối chiếu KPI vs. thực tế theo ngày/tuần/tháng
- [ ] Ghi nhận hoạt động: số cuộc gọi, số lần chăm sóc, số site visit

---

#### F15 — Đồng bộ Lead từ Facebook/Google Ads

**Acceptance criteria:**
- [ ] Kết nối webhook nhận lead từ Facebook Lead Ads và Google Ads
- [ ] Import lead từ file CSV (mapping cột linh hoạt)
- [ ] Tự động gắn tag nguồn (campaign name, ad set, ad) khi lead vào
- [ ] Lead lỗi format / thiếu thông tin → vào hàng đợi xử lý thủ công
- [ ] Có thể tạo "campaign" trong hệ thống để ghi nhận nguồn và theo dõi performance

---

#### F16 — Landing Page System

**Acceptance criteria:**
- [ ] Tạo landing page từ template có sẵn (kéo thả hoặc chọn layout)
- [ ] Gắn form capture lead vào landing page
- [ ] Gán sale owner nhận lead từ từng landing page
- [ ] Tracking: lượt xem, submit form, conversion rate
- [ ] Mỗi landing page có URL riêng, có thể custom slug

---

#### F17 — Campaign Management

**Acceptance criteria:**
- [ ] Tạo campaign với: tên, kênh (FB/GG/Zalo/SEO...), ngân sách, ngày chạy
- [ ] Liên kết landing page, lead source với campaign
- [ ] Theo dõi: CPL, số lead, số booking, số deal từ campaign
- [ ] So sánh hiệu quả giữa các campaign

---

#### F18 — Omnichannel Chat (Zalo OA, Messenger, Website)

**Acceptance criteria:**
- [ ] Gom hội thoại từ Zalo OA (via API), Facebook Messenger, Website live chat vào 1 inbox
- [ ] Gán sale phụ trách từng hội thoại
- [ ] Lưu toàn bộ lịch sử hội thoại theo khách hàng (liên kết với Customer 360)
- [ ] Gắn tag, ghi note trên hội thoại
- [ ] Thông báo cho sale khi có tin nhắn mới chưa xử lý
- [ ] Chuyển hội thoại giữa các sale

---

#### F19 — Affiliate / Referral System

**Acceptance criteria:**
- [ ] Đăng ký affiliate: cả nội bộ (sale giới thiệu chéo) và bên ngoài (KOL, môi giới tự do) — có form đăng ký + admin approval
- [ ] Tạo link referral cá nhân hóa cho từng affiliate
- [ ] Tracking attribution: lead từ link referral được gắn cho affiliate đó trong 100 ngày
- [ ] Tính hoa hồng affiliate 0.5% khi hợp đồng từ lead đó hoàn thành
- [ ] Affiliate xem được: số lead tạo ra, số deal thành công, hoa hồng tích lũy (portal riêng hoặc view hạn chế)
- [ ] Payout manual: admin xác nhận và ghi nhận đã thanh toán

---

#### F20 — Email cá nhân qua Gmail Workspace

**Acceptance criteria:**
- [ ] Sale kết nối tài khoản Gmail Workspace cá nhân
- [ ] Gửi email trực tiếp cho khách từ trong hệ thống (lưu lịch sử trong Customer 360)
- [ ] Không phải email marketing hàng loạt — chỉ email 1-1

---

#### F21 — Google Calendar Sync

**Acceptance criteria:**
- [ ] Lịch site visit và lịch chăm sóc từ hệ thống sync sang Google Calendar của sale
- [ ] Thay đổi lịch trong hệ thống → cập nhật Google Calendar tương ứng

---

#### F22 — CMS Global (Phase 3)

**Acceptance criteria:**
- [ ] Quản lý bài viết SEO: tạo, chỉnh sửa, publish, unpublish
- [ ] Phân loại theo chủ đề, dự án, từ khóa SEO
- [ ] Quản lý hình ảnh và video tập trung
- [ ] Publish nội dung đồng thời lên nhiều website vệ tinh

---

#### F23 — 5 Website vệ tinh (Phase 3)

**Acceptance criteria:**
- [ ] Tạo và quản lý 5 website riêng biệt, mỗi site có domain riêng
- [ ] SEO targeting vùng ven: Tây Ninh, Long An, Bình Dương, Đồng Nai (và 1 vùng còn lại cần xác nhận)
- [ ] Đồng bộ nội dung từ CMS Global xuống từng site
- [ ] Tối ưu SEO on-page: sitemap, schema, meta tags, tốc độ tải trang
- [ ] Form lead trên website → đẩy vào CRM với tag nguồn

---

## 3. Yêu cầu phi chức năng

### 3.1. Performance
- Response time API: < 500ms cho 95% request thông thường
- Xử lý tối đa 1.000 lead/ngày
- Hỗ trợ 1.000 concurrent users
- Trang web tải: < 3 giây trên 4G

### 3.2. Security
- RBAC (Role-Based Access Control) — mỗi role chỉ truy cập dữ liệu thuộc phạm vi mình
- Audit log đầy đủ: ghi nhận mọi thao tác thay đổi dữ liệu (ai, làm gì, lúc nào)
- HTTPS bắt buộc cho toàn bộ traffic
- Tuân thủ Nghị định 13/2023/NĐ-CP về bảo vệ dữ liệu cá nhân:
  - Có cơ chế ghi nhận consent của khách hàng
  - Quyền xóa dữ liệu cá nhân theo yêu cầu
  - Data retention policy rõ ràng (xem mục 5.3)
- Dữ liệu nhạy cảm (mật khẩu, token) được mã hóa

### 3.3. Compatibility
- Browser: Chrome (latest-2), Safari (latest-2), Firefox (latest-2), Edge (latest)
- Mobile: Responsive web — từ màn hình 375px (iPhone SE) trở lên
- Không yêu cầu native app ở phase này

### 3.4. Availability
- Uptime target: 99% (~7.3 giờ downtime/tháng)
- Backup dữ liệu tự động hàng ngày, giữ 30 ngày
- Logging hệ thống để hỗ trợ debug và audit

### 3.5. Scalability
- Kiến trúc module hóa: có thể bổ sung module mới (AI, mobile app) mà không ảnh hưởng core
- Deploy trên cloud Việt Nam (VNG Cloud, FPT Cloud, hoặc tương đương)

### 3.6. Ngôn ngữ
- Tiếng Việt 100% (giao diện, thông báo, báo cáo)

---

## 4. Giao diện & UX

### 4.1. Screen / Page list (Phase 1)

| # | Tên màn | Mô tả | Platform |
|---|---------|-------|----------|
| S01 | Login | Đăng nhập | Web + Mobile web |
| S02 | Dashboard | Tổng quan theo role | Web + Mobile web |
| S03 | Lead List | Danh sách lead, filter, search | Web + Mobile web |
| S04 | Lead Detail | Chi tiết lead + timeline + ghi hoạt động | Web + Mobile web |
| S05 | Customer 360 | Hồ sơ khách hàng đầy đủ | Web |
| S06 | Project List | Danh sách dự án | Web |
| S07 | Project Detail | Chi tiết dự án + danh sách sản phẩm | Web |
| S08 | Product List | Bảng căn/lô với trạng thái tồn kho | Web |
| S09 | Contract List | Danh sách hợp đồng | Web |
| S10 | Contract Detail | Chi tiết hợp đồng + lịch thanh toán | Web |
| S11 | Commission Report | Báo cáo hoa hồng theo deal/sale/tháng | Web |
| S12 | Calendar | Lịch site visit + lịch chăm sóc | Web + Mobile web |
| S13 | User Management | Quản lý tài khoản (Admin) | Web |
| S14 | Sale Kit | Thư viện tài liệu theo dự án | Web + Mobile web |
| S15 | Settings | Cấu hình hệ thống (workflow, commission policy...) | Web |
| S16 | Reports | Các loại báo cáo + export | Web |

### 4.2. User flow chính

**Flow 1: Lead vào → Chốt Deal**
```
Lead webhook/form/manual 
→ Auto-assign đến Sale 
→ Sale cập nhật trạng thái: Contacted → Qualified 
→ Đặt lịch site visit 
→ Booking 
→ Negotiation 
→ Won 
→ Tạo hợp đồng → Upload PDF ký → Signed 
→ Hệ thống tính hoa hồng
```

**Flow 2: Marketing → Lead vào CRM**
```
Campaign chạy Ads 
→ Khách click → Landing page 
→ Form submit → Lead vào CRM (tag campaign nguồn) 
→ Auto-assign
```

**Flow 3: Affiliate dẫn Lead**
```
Affiliate có link riêng 
→ Khách click link (cookie 100 ngày) 
→ Khách submit form / liên hệ 
→ Lead vào CRM, gắn affiliate nguồn 
→ Nếu hợp đồng ký → hệ thống tính hoa hồng affiliate 0.5%
```

**Flow 4: After-sale**
```
Hợp đồng Signed 
→ Tạo lịch thanh toán 
→ Nhắc lịch tự động 
→ Vận hành ghi nhận từng đợt thanh toán 
→ Báo cáo công nợ
```

### 4.3. Design reference
- Chưa có Figma / mockup — cần khách cung cấp hoặc xác nhận để team design thực hiện
- Ưu tiên UX: đơn giản, tối thiểu thao tác cho sale ngoài thực địa dùng mobile web

---

## 5. Dữ liệu

### 5.1. Entity chính

| Entity | Mô tả | Thuộc tính chính |
|--------|-------|-----------------|
| User | Nhân viên hệ thống | id, name, email, phone, role, status, projects[] |
| Lead | Khách hàng tiềm năng | id, name, phone, email, source, status, assigned_to, project_id, tags[], activities[] |
| Project | Dự án BĐS | id, name, type, location, status, sales[], products[] |
| Product | Căn/lô trong dự án | id, project_id, code, area, price, floor, status (Available/Reserved/Sold) |
| Contract | Hợp đồng mua bán | id, lead_id, product_id, customer_info, status, file_url, payment_schedule[] |
| Payment | Đợt thanh toán | id, contract_id, amount, due_date, paid_date, status |
| Commission | Hoa hồng | id, contract_id, user_id, role, rate, amount, status |
| Campaign | Chiến dịch marketing | id, name, channel, budget, start_date, end_date, landing_pages[] |
| LandingPage | Trang thu lead | id, campaign_id, url, form_fields[], assigned_sale |
| Affiliate | Đối tác referral | id, name, type (internal/external), link, attribution_window |
| Activity | Log hoạt động trên lead | id, lead_id, user_id, type (call/note/chat/visit), content, timestamp |

### 5.2. Data flow

```
[Ads/Landing/Manual] → Lead → [Assign] → Sale Activity → [Won] 
                                                            ↓
                                                        Contract → Payment tracking
                                                            ↓
                                                        Commission (tính tự động)
                                                            ↓
                                                        Dashboard & Report
```

### 5.3. Data retention
- Dữ liệu lead & khách hàng: giữ tối thiểu 5 năm (hoặc theo quy định pháp lý hiện hành)
- Hợp đồng & thanh toán: giữ vĩnh viễn (hoặc 10 năm theo quy định lưu trữ hợp đồng BĐS Việt Nam)
- Audit log: giữ 2 năm
- Xóa dữ liệu cá nhân theo yêu cầu (GDPR/NĐ13): thực hiện trong 30 ngày, ghi nhận yêu cầu xóa

---

## 6. Tích hợp

### 6.1. Third-party services

| Service | Mục đích | Phase | Bắt buộc? |
|---------|----------|-------|-----------|
| Facebook Lead Ads API | Nhận lead tự động qua webhook | 2 | Có |
| Google Ads API | Nhận lead + tracking conversion | 2 | Có |
| Zalo Official Account API | Omnichannel chat + thông báo | 2 | Có |
| Facebook Messenger | Omnichannel chat | 2 | Có |
| Google Calendar API | Sync lịch site visit | 2 | Should |
| Gmail / Google Workspace | Gửi email 1-1 từ hệ thống | 2 | Should |
| Vietnamese Cloud Provider | Hosting (VNG Cloud / FPT Cloud / tương đương) | 1 | Có |

### 6.2. API nội bộ
- Không có hệ thống cũ cần kết nối — xây dựng hoàn toàn mới

---

## 7. Platform mong muốn

| Platform | Cần? | Ghi chú |
|----------|------|---------|
| Backend (API) | ✅ | Luôn cần |
| Web App (Admin + Operations + Marketing) | ✅ | Full features |
| Mobile Web (Responsive) | ✅ | Tối ưu cho Sale ngoài thực địa — truy cập qua browser |
| Mobile App Native (iOS/Android) | ❌ | Out-of-scope phase này, sẽ bổ sung sau |
| Admin Panel | ✅ | Tích hợp trong web app, phân quyền theo role |
| Website vệ tinh (5 site) | ✅ | Phase 3 — domain riêng, SEO |

---

## 8. Kế hoạch phase (đề xuất)

> Đây là đề xuất từ góc nhìn BA. PO/Tech Lead sẽ điều chỉnh khi đánh giá khả thi trong timeline & budget thực tế.

### Phase 1 — MVP (Core System)
**Mục tiêu:** Hệ thống quản lý lõi vận hành được — sale dùng hàng ngày, lãnh đạo xem báo cáo  
**Features:** F01, F02, F03, F04, F05, F06, F07, F08, F09, F10, F11, F12, F13, F14  
**Timeline mong muốn từ khách:** 3 tháng  
**Budget mong muốn từ khách:** 500.000.000 VND  

### Phase 2 — External Integrations & Marketing
**Mục tiêu:** Tự động hóa nguồn lead, omnichannel, affiliate  
**Features:** F15, F16, F17, F18, F19, F20, F21  
**Timeline:** Chưa xác định  

### Phase 3 — Satellite Websites & SEO
**Mục tiêu:** Xây dựng kênh organic bất động sản vùng ven  
**Features:** F22, F23 (5 sites: Tây Ninh, Long An, Bình Dương, Đồng Nai + 1 vùng cần xác nhận)  
**Timeline:** Chưa xác định  

### Phase 4+ — AI & Intelligence
**Mục tiêu:** Tối ưu hóa dựa trên dữ liệu + AI  
**Features:** F24, F25, F26, F27  
**Timeline:** Sau Phase 3  

---

## 9. Rủi ro & Giả định

### 9.1. Rủi ro từ góc nhìn business

| Rủi ro | Impact | Mitigation |
|--------|--------|------------|
| Budget 500tr cho Phase 1 có thể chật với scope 14 feature | Cao | Tech Lead đánh giá lại scope, có thể cắt F13, F14 sang Phase 2 |
| Timeline 3 tháng cho Phase 1 là aggressive | Cao | PO/Tech Lead cần đánh giá và ưu tiên Must-have vs. Should |
| Phụ thuộc Zalo OA API: Zalo thay đổi chính sách/API | Trung bình | Có fallback (Messenger/email) trong giai đoạn chờ |
| Tuân thủ NĐ13/2023: cần tư vấn pháp lý cụ thể về data retention & consent | Cao | Cần xác nhận với luật sư/DPO trước khi phát triển |
| 5 website vệ tinh SEO: hiệu quả SEO phụ thuộc content và thời gian | Trung bình | Cần team content chuẩn bị trước khi launch Phase 3 |

### 9.2. Giả định (cần khách confirm)

1. **Giả định:** Rule phân bổ lead tự động là round-robin trong nhóm sale của dự án — khách sẽ cung cấp chi tiết logic cụ thể hơn
2. **Giả định:** Quy trình onboard affiliate bên ngoài: nộp form thông tin → Admin duyệt → phát link → tracking
3. **Giả định:** Website vệ tinh thứ 5 (ngoài Tây Ninh, Long An, Bình Dương, Đồng Nai) — cần xác nhận địa bàn
4. **Giả định:** Không cần migrate dữ liệu từ hệ thống cũ — bắt đầu hoàn toàn mới
5. **Giả định:** Khách cung cấp tài khoản Zalo OA và Facebook Business đã setup sẵn

### 9.3. Phụ thuộc

- Khách cung cấp: tài khoản Zalo OA API, Facebook Business Manager, Google Ads Account trước Phase 2
- Khách cung cấp: domain cho 5 website vệ tinh trước Phase 3
- Design team cần cung cấp Figma / mockup trước khi dev frontend
- Content team chuẩn bị nội dung SEO trước khi ra mắt Phase 3

---

## 10. Open questions (chưa chốt)

- [ ] **Website vệ tinh thứ 5:** Địa bàn SEO ngoài Tây Ninh, Long An, Bình Dương, Đồng Nai là tỉnh/thành nào?
- [ ] **Rule phân bổ lead:** Ngoài round-robin, có cần phân bổ theo hiệu suất (sale đang làm tốt nhận nhiều hơn) hay theo workload (sale ít lead hơn được ưu tiên)?
- [ ] **KPI mặc định cho sale:** Ai đặt KPI — leader hay admin? Có KPI theo dự án không?
- [ ] **Design reference:** Khách có brand color / logo / moodboard để đội design tham chiếu không?
- [ ] **Giao tiếp dự án:** Kênh confirm thay đổi requirement giữa khách và team sẽ qua đâu (email, Zalo nhóm, Slack)?

---

## 11. Glossary

| Thuật ngữ | Định nghĩa |
|-----------|-----------|
| Lead | Khách hàng tiềm năng chưa ký hợp đồng |
| Deal | Lead đã đạt trạng thái Won (chốt thành công) |
| Booking | Bước đặt cọc / giữ sản phẩm, trước khi ký hợp đồng chính thức |
| CPL | Cost Per Lead — chi phí trung bình để có 1 lead |
| ROAS | Return On Ad Spend — doanh thu / chi phí quảng cáo |
| MLM | Multi-Level Marketing — cấu trúc hoa hồng đa tầng |
| Attribution window | Khoảng thời gian tính hoa hồng cho affiliate từ lần click đầu tiên |
| Site Visit | Lịch đưa khách đi xem dự án / căn hộ thực tế |
| Sale Kit | Bộ tài liệu tư vấn chuẩn (brochure, bảng giá, chính sách) |
| Vòng đời Lead | Các trạng thái từ lúc lead vào đến khi Won hoặc Lost |
| Omnichannel | Gom nhiều kênh chat (Zalo, Messenger, Web) vào 1 inbox |
| Affiliate | Đối tác (nội bộ hoặc bên ngoài) dẫn lead để nhận hoa hồng |
| Responsive web | Giao diện web tự điều chỉnh hiển thị phù hợp màn hình mobile |
| CMS | Content Management System — hệ thống quản lý nội dung website |
| RBAC | Role-Based Access Control — phân quyền theo vai trò |

---

## 12. Changelog

| Version | Ngày | Thay đổi | Author |
|---------|------|----------|--------|
| 1.0 | 2026-04-22 | Initial draft từ biz_model.md + qna.txt | Claude (AI BA) |

---

**Signoff:**
- [ ] Khách hàng đã đọc và đồng ý
- [ ] Ngày confirm: ________
- [ ] Tên người confirm: ________
