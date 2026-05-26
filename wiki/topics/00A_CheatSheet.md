# 00A — VDI Quick Reference Cheat Sheet
## Thông tin ăn liền cho kỹ sư mới — Cả hai nền tảng

> Tài liệu này không thay thế tài liệu đào tạo chi tiết.  
> Dùng để tra cứu nhanh, định hướng ban đầu, và biết cần đọc file nào tiếp theo.  
> Tham chiếu đầy đủ: `wiki/topics/` từ file 01 đến 28.

---

## PHẦN 1 — KEYWORD QUAN TRỌNG

### 🔵 Omnissa Horizon

| Keyword | Là gì (1 dòng) | Khi lỗi liên quan |
|---|---|---|
| **Connection Server** | Broker của Horizon — nhận authen, chọn VM, điều phối session | Login fail, resource không enumerate, session fail |
| **Unified Access Gateway (UAG)** | Gateway bên ngoài — reverse proxy cho Horizon qua internet | External user không vào được |
| **Horizon Agent** | Agent cài trong VM — giao tiếp với Connection Server | Desktop unavailable, unregistered |
| **Desktop Pool** | Nhóm VM cùng loại cấp cho user | Không đủ máy, launch fail hàng loạt |
| **Entitlement** | Quyền user/group truy cập pool | User không thấy desktop |
| **Blast Extreme** | Display protocol của Horizon (thay PCoIP) | Session lag, màn hình đen, audio lỗi |
| **vCenter / ESXi** | Hypervisor/HCI quản lý VM bên dưới | VM off, task fail, host contention |
| **Instant Clone** | Cơ chế tạo VM nhanh từ parent VM | Clone fail, domain join lỗi |
| **Horizon Console** | Web UI quản trị Horizon | Công cụ chính để xem pool, session, machine state |

**Đọc thêm:** `03_Omnissa_Horizon_Architecture_Overview.md`

---

### 🟠 Citrix CVAD

| Keyword | Là gì (1 dòng) | Khi lỗi liên quan |
|---|---|---|
| **Delivery Controller** | Broker của Citrix — authen, chọn VDA, điều phối session | Login fail, launch fail, catalog không load |
| **StoreFront** | Portal web người dùng đăng nhập và thấy app/desktop | User không thấy resource, login lỗi |
| **Citrix Gateway** | Gateway bên ngoài — SSL VPN / proxy cho Citrix qua internet | External user không vào được |
| **Virtual Delivery Agent (VDA)** | Agent cài trong VM — giao tiếp với Delivery Controller | Desktop unavailable, unregistered |
| **Machine Catalog** | Tập hợp VM cùng loại/cùng image | VDA unregistered hàng loạt sau image update |
| **Delivery Group** | Gán machine + quyền user cho nhóm cụ thể | User không thấy desktop, launch fail |
| **Application Group** | Nhóm published app riêng (tùy chọn) | App không hiện hoặc hiện sai nhóm |
| **Site Database** | Database SQL lưu cấu hình toàn site | Site không hoạt động nếu DB lỗi |
| **HDX / ICA** | Display protocol của Citrix | Session lag, display lỗi, redirect không hoạt động |
| **Citrix Director** | Web UI monitoring — session, failed logon, VDA state | Công cụ chính để diagnose user/session |
| **Citrix Studio** | Web UI quản trị — Catalog, DG, policy | Công cụ chính để cấu hình resource |

**Đọc thêm:** `04_Citrix_CVAD_Architecture_Overview.md`

---

### ⚪ Keyword dùng chung (cả hai nền tảng)

| Keyword | Ý nghĩa |
|---|---|
| **Active Directory / AD** | Danh tính user, group, computer account, GPO |
| **DNS** | Phân giải tên broker, gateway, DC, profile share |
| **Datastore / Storage Repository** | Nơi lưu VM disk, image, profile |
| **Profile (FSLogix/CPM)** | Dữ liệu cá nhân user — setting, desktop, app data |
| **Session** | Kết nối giữa client và VM trong nền tảng VDI |
| **Registration** | Trạng thái Agent/VDA đã kết nối thành công với broker |
| **Load Balancer (LB)** | Phân tải giữa nhiều Connection Server hoặc Delivery Controller |
| **MFA / Conditional Access** | Xác thực đa yếu tố cho login từ ngoài vào |

---

## PHẦN 2 — TẠO MỘT VDI (Quy trình cốt lõi)

### Quy trình chung (áp dụng cả hai nền tảng)

```
1. Xác nhận request: user nào, loại VDI gì, pool/catalog nào, approval chưa
2. Precheck: capacity (CPU/RAM/storage), image được duyệt, network/DHCP, naming
3. Tạo máy: tăng count trong pool/catalog hoặc tạo manual theo SOP
4. Xác nhận: VM powered on → domain joined → Agent/VDA registered
5. Gán quyền: thêm user vào AD group hoặc entitlement/Delivery Group
6. Kiểm thử: user (hoặc test account) thấy resource và launch được
7. Lưu evidence: before/after count, registration state, launch screenshot, ticket ID
```

---

### 🔵 Horizon — Tạo desktop trong pool

| Bước | Làm gì | Kiểm tra gì |
|---|---|---|
| 1 | Mở Horizon Console → Desktop Pool → Edit → tăng Max Machines | Pool settings |
| 2 | Theo dõi vCenter task: clone VM, customize, domain join | vCenter Tasks/Events |
| 3 | Xác nhận Horizon Agent registered trong pool machine list | Pool > Machines tab |
| 4 | Thêm user/group vào pool Entitlement | Pool > Entitlements tab |
| 5 | Đăng nhập Horizon Client / portal → xác nhận thấy desktop | User perspective |
| 6 | Launch test → xác nhận session active | Session tab trong Console |

**Cần biết:** Horizon dùng Instant Clone hoặc Full Clone (cần xác nhận với khách hàng).  
**Đọc thêm:** `14_Omnissa_Desktop_Pool_and_Entitlement_Guide.md`, `11_VDI_Provisioning_and_Allocation_Guide.md`

---

### 🟠 Citrix — Tạo machine trong Machine Catalog + Delivery Group

| Bước | Làm gì | Kiểm tra gì |
|---|---|---|
| 1 | Citrix Studio → Machine Catalog → Add Machines → chọn số lượng | Catalog task progress |
| 2 | Theo dõi hypervisor task: clone/provision VM, domain join | vCenter hoặc XenServer |
| 3 | Xác nhận VDA registered trong Catalog machine list | Catalog > Machines |
| 4 | Thêm machine vào Delivery Group (nếu chưa tự động) | DG > Machines tab |
| 5 | Thêm user/group vào Delivery Group | DG > Access Policy |
| 6 | Đăng nhập StoreFront → xác nhận user thấy desktop/app | User perspective |
| 7 | Launch test → xác nhận session active trong Director | Citrix Director |

**Cần biết:** Citrix dùng MCS hoặc Citrix Provisioning/PVS hoặc Manual (cần xác nhận với khách hàng).  
**Đọc thêm:** `13_Citrix_Machine_Catalog_and_Delivery_Group_Guide.md`, `11_VDI_Provisioning_and_Allocation_Guide.md`

---

## PHẦN 3 — MẠNG VÀ AUTHENTICATION

### Luồng kết nối nội bộ (Internal)

```
User (LAN)
  → DNS resolve tên portal/broker
  → Xác thực AD (username/password + MFA nếu có)
  → Broker chọn VM sẵn sàng
  → Kết nối trực tiếp tới Agent/VDA trong VM
  → Session bắt đầu
```

### Luồng kết nối bên ngoài (External)

```
User (Internet)
  → DNS public resolve tên gateway (UAG hoặc Citrix Gateway)
  → TLS certificate check
  → Xác thực AD + MFA (qua Gateway hoặc IdP)
  → Gateway forward tới Broker (Connection Server / Delivery Controller)
  → Broker chọn VM
  → Kết nối tunneled qua Gateway → Agent/VDA
  → Session bắt đầu
```

---

### 🔵 Horizon — Các cổng mạng cốt lõi

| Đoạn | Cổng | Giao thức |
|---|---|---|
| Client → UAG | 443 | HTTPS (auth + tunnel) |
| UAG → Connection Server | 443, 8443 | HTTPS |
| Client → VM (Blast internal) | 8443 | Blast/TCP |
| Client → VM (Blast external, qua UAG) | 443 | Blast/TCP tunnel |
| Connection Server → vCenter | 443 | HTTPS |
| Horizon Agent → Connection Server | 4001 | JMS/SSL |

### 🟠 Citrix — Các cổng mạng cốt lõi

| Đoạn | Cổng | Giao thức |
|---|---|---|
| Client → Citrix Gateway | 443 | HTTPS (SSL) |
| Gateway → StoreFront | 443 | HTTPS |
| Gateway → Delivery Controller (STA) | 80/443 | HTTP/HTTPS |
| Client → VDA (HDX direct internal) | 1494, 2598 | ICA / CGP |
| Client → VDA (HDX qua Gateway) | 443 | SSL tunnel |
| VDA → Delivery Controller | 80 | XML |
| Delivery Controller → SQL | 1433 | SQL |

---

### Authentication — Các lớp

| Lớp | Thành phần | Lỗi thường thấy |
|---|---|---|
| **Domain credential** | Active Directory DC | Account locked, wrong password, DC unreachable |
| **DNS** | DC DNS, split DNS | Portal không resolve, broker không tìm thấy |
| **Certificate (TLS)** | Gateway, StoreFront, Connection Server | Certificate expired, chain lỗi, client warning |
| **MFA / Conditional Access** | RADIUS, Okta, Azure AD MFA, TOTP | MFA timeout, IdP lỗi, external-only bị block |
| **Token / STA** | Secure Ticket Authority (Citrix) / Tunnel | Launch fail sau authen thành công |
| **Kerberos / NTLM** | Windows session trong VM | Lỗi login Windows sau khi VDI mở |

**Đọc thêm:** `05_VDI_Access_Flow_Design.md`, `06_Identity_and_Domain_Integration_Guide.md`, `09_Network_Operations_for_VDI.md`

---

## PHẦN 4 — CÁC LỖI QUAN TRỌNG (Critical — Ảnh hưởng lớn)

### 🔴 Lỗi ảnh hưởng diện rộng — Cả hai nền tảng

| Lỗi | Dấu hiệu | Nguyên nhân thường gặp | Hành động ngay |
|---|---|---|---|
| **Broker/Control plane down** | Toàn bộ user không login được | Service crash, DB lỗi, patch lỗi | Kiểm tra service health, event log broker; không restart vội |
| **AD/DNS outage** | Cả Horizon lẫn Citrix đều fail authen | DC unreachable, DNS TTL, replication | Kiểm tra DC ping, nslookup; gọi IAM team ngay |
| **Profile share unavailable** | Login được nhưng tất cả user temporary profile | File share down, storage path lỗi, permission | Kiểm tra share path, storage health, network to share |
| **Datastore full / Critical** | Provisioning fail, VM không boot | Snapshot tồn đọng, growth không kiểm soát | Dừng provisioning mới; alert storage owner ngay |
| **Certificate expired (Gateway)** | External user toàn bộ không vào được | Cert hết hạn hoặc chain lỗi | Kiểm tra cert expiry; escalate network/security ngay |
| **License limit reached** | User authen được nhưng launch fail với lỗi license | License count đạt limit | Kiểm tra license dashboard; escalate platform owner |

---

### 🔵 Horizon — Lỗi quan trọng riêng

| Lỗi | Dấu hiệu | Hành động |
|---|---|---|
| **Connection Server cluster down** | Toàn site không login | Kiểm tra service trên từng CS; kiểm tra event log |
| **UAG service fail** | External user toàn bộ fail | Kiểm tra UAG admin UI; service health; backend targets |
| **vCenter connectivity lost** | Pool không provisioning được, VM power lỗi | Kiểm tra Connection Server → vCenter connection trong Console |
| **HCI cluster contention** | Nhiều VM chậm đồng thời cùng cluster | Kiểm tra host CPU/memory/network; vCenter alarms |

---

### 🟠 Citrix — Lỗi quan trọng riêng

| Lỗi | Dấu hiệu | Hành động |
|---|---|---|
| **Delivery Controller service fail** | Launch fail toàn site | Kiểm tra service Broker Service, Configuration Service; event log |
| **Site Database unavailable** | Studio/Director không load, site không hoạt động | Kiểm tra SQL server, kết nối DB từ Delivery Controller |
| **StoreFront farm unreachable** | User login portal lỗi | Kiểm tra StoreFront service, server group, LB probe |
| **Citrix Gateway STA fail** | External authen OK nhưng launch timeout | Kiểm tra STA URL cấu hình, STA service trên Delivery Controller |

**Đọc thêm:** `17_VDI_Incident_Classification_Guide.md` (Phần 4.7 — Platform scope)

---

## PHẦN 5 — LỖI THƯỜNG XUYÊN XẢY RA (Daily/Weekly)

### Bảng 10 lỗi thường gặp nhất — Cả hai nền tảng

| # | Triệu chứng | Scope | Kiểm tra đầu tiên | File tham chiếu |
|---|---|---|---|---|
| 1 | User login được nhưng không thấy desktop/app | 1 user | AD group membership, entitlement/DG mapping | 18-Playbook5, 26-KB2 |
| 2 | Một VDA/Horizon Agent unregistered | 1 machine | VM power, Agent service, DNS, domain join | 18-Playbook7+8, 26-KB4 |
| 3 | Login chậm đầu giờ sáng | Pool / Site | Profile path, storage latency, DC auth latency | 18-Playbook9, 08, 26-KB6 |
| 4 | Màn hình đen sau khi launch | 1 user / Pool | Profile, display policy, image/agent version | 18-Playbook10, 26-KB5 |
| 5 | Session disconnect ngẫu nhiên | 1 user | Network latency/loss, protocol config, client | 18-Playbook11, 09 |
| 6 | Printer không redirect | 1 user | Citrix/Horizon policy, client driver, GPO scope | 26-KB8, 10 |
| 7 | USB không nhận | 1 user | Policy, client capability, security block | 10, 26-KB8 |
| 8 | Temporary profile (mất setting) | 1 user | Profile path/lock/permission, storage | 18-Playbook12, 26-KB7 |
| 9 | External user không launch (internal OK) | Gateway scope | Gateway/LB, cert, STA/tunnel, firewall | 18-Playbook6, 05, 09 |
| 10 | User mới onboard không thấy resource | 1 user | AD group chưa đúng, AD replication delay | 11-Scenario1, 17-Scenario1 |

---

### 🔵 Horizon — Lỗi thường gặp riêng

| Triệu chứng | Nguyên nhân thường gặp | Kiểm tra |
|---|---|---|
| Desktop state "Already Used" không thoát | Session orphan | Console > Sessions > Force logoff |
| Pool available = 0 nhưng total cao | Máy ở maintenance/off/unregistered | Console > Pool > Machines > lọc state |
| Horizon Client lỗi certificate | Cert self-signed hoặc chain thiếu | Cài trusted CA trên endpoint |
| Blast session lag nặng | Bandwidth thiếu, UDP bị chặn | Kiểm tra firewall UDP 8443; chuyển TCP |

---

### 🟠 Citrix — Lỗi thường gặp riêng

| Triệu chứng | Nguyên nhân thường gặp | Kiểm tra |
|---|---|---|
| Citrix Receiver/Workspace lỗi "Cannot complete your request" | STA fail, Gateway path lỗi | Kiểm tra STA trên Gateway config |
| VDA registered nhưng Delivery Group hiện "Not registered" | Machine không trong DG hoặc DG disabled | Studio > Delivery Group > Machine state |
| Director thấy failed logon tăng | Authen lỗi hoặc DC/StoreFront lỗi | Kiểm tra Event log trên StoreFront và DC |
| App published nhưng user không thấy | App không trong DG user được gán | Studio > Delivery Group > Applications |

**Đọc thêm:** `26_VDI_Operational_Knowledge_Base.md`, `18_VDI_Troubleshooting_Playbook.md`

---

## PHẦN 6 — CẢNH BÁO VÀ ISSUE CÓ THỂ GÂY LỖI HÀNG LOẠT

> **Nguyên tắc vàng:** Khi thấy bất kỳ cảnh báo nào dưới đây, **dừng change đang chạy**, thu evidence, và báo cáo trước khi tiếp tục.

---

### ⚠️ Cảnh báo quan trọng nhất — Cả hai nền tảng

| Cảnh báo | Ngưỡng nguy hiểm | Hậu quả nếu bỏ qua | Hành động |
|---|---|---|---|
| **Datastore / Storage full** | > 85–90% | Provisioning fail, VM không checkpoint, logon fail | Dừng tạo VM mới; alert storage owner ngay |
| **Storage latency cao** | > 20–30ms liên tục | Boot storm, logon storm, session kém ổn định | Alert storage/hypervisor; xem snapshot tồn đọng |
| **Snapshot tồn đọng** | Snapshot > vài ngày trên production pool | Datastore đầy dần, VM performance giảm | Không xóa vội; phối hợp platform owner |
| **Nhiều Agent/VDA unregistered cùng lúc** | > 5–10% pool/catalog | User mất truy cập hàng loạt | Dừng rollout; kiểm tra image/DNS/broker ngay |
| **Certificate sắp hết hạn** | < 30 ngày | External access down toàn bộ khi hết hạn | Lên lịch gia hạn; alert network/security |
| **License sắp đạt limit** | > 90% | User mới không launch được | Alert platform owner và vendor |
| **Boot/Logon storm sắp xảy ra** | Onboarding lớn hoặc reboot batch | Storage IOPS saturation, session fail | Chia batch nhỏ; không reboot đồng loạt |
| **AD replication bất thường** | Event ID 1311, 1566 | User không thấy resource dù đã gán group | Alert IAM team; không tự sửa DNS |

---

### 🔵 Horizon — Cảnh báo riêng

| Cảnh báo | Hậu quả | Hành động |
|---|---|---|
| **Horizon Agent version mismatch** sau image update | Desktop state lỗi, launch fail hàng loạt | Dừng publish image mới; rollback image cũ |
| **Connection Server event log đầy lỗi authen** | Dấu hiệu tấn công hoặc misconfigure MFA | Kiểm tra event log, alert security |
| **UAG tunnel service restart liên tục** | External user mất kết nối ngắt quãng | Kiểm tra UAG admin, backend target health |
| **vCenter task queue đầy** | Provisioning chậm, clone timeout | Giảm concurrency; alert hypervisor owner |

---

### 🟠 Citrix — Cảnh báo riêng

| Cảnh báo | Hậu quả | Hành động |
|---|---|---|
| **VDA version mismatch với Delivery Controller** | VDA unregistered sau upgrade | Kiểm tra compatibility matrix trước upgrade |
| **Site Database latency cao** | Studio/Director chậm, session assignment lỗi | Alert SQL/DBA team; không restart Delivery Controller vội |
| **StoreFront subscription store lỗi** | User mất app favorited, resource enumerate chậm | Kiểm tra StoreFront event log, server group sync |
| **MCS provisioning task fail liên tiếp** | Catalog không mở rộng được khi cần | Kiểm tra hypervisor connection, storage, permission |
| **Citrix Director alert "Machines Failed"** tăng đột biến | Dấu hiệu image lỗi hoặc storage/network issue | Xem Director trend; cross-check với recent change |

---

### 🛑 Stop Condition — Khi nào phải DỪNG ngay

```
DỪNG ngay nếu:
  □ Số lượng unregistered machine tăng sau khi bắt đầu rollout/change
  □ Storage latency tăng đột biến trong khi đang provisioning
  □ Failed session rate tăng sau image publish
  □ External access toàn bộ fail sau certificate/gateway change
  □ Site database không reachable sau patch
  □ AD/DNS có alert trong khi đang thực hiện change lớn

→ Dừng change, lưu evidence, gọi change owner và platform lead
→ Không retry hàng loạt khi chưa rõ nguyên nhân
```

---

## Tra cứu nhanh — File cần mở

| Cần gì | Mở file |
|---|---|
| Keyword Horizon | `03_Omnissa_Horizon_Architecture_Overview.md` |
| Keyword Citrix | `04_Citrix_CVAD_Architecture_Overview.md` |
| Từ điển thuật ngữ | `27_VDI_Glossary_and_Concept_Dictionary.md` |
| Tạo VDI Horizon | `14_Omnissa_Desktop_Pool_and_Entitlement_Guide.md` |
| Tạo VDI Citrix | `13_Citrix_Machine_Catalog_and_Delivery_Group_Guide.md` |
| Luồng mạng / authen | `05_VDI_Access_Flow_Design.md` |
| Cổng firewall | `09_Network_Operations_for_VDI.md` |
| Phân loại lỗi | `17_VDI_Incident_Classification_Guide.md` |
| Playbook xử lý | `18_VDI_Troubleshooting_Playbook.md` |
| KB lỗi thường gặp | `26_VDI_Operational_Knowledge_Base.md` |
| Cảnh báo / Change risk | `20_VDI_Change_Management_Guide.md` |
| Storage / Boot storm | `08_Storage_Operations_for_VDI.md` |
