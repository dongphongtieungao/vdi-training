# 00 — Hướng Dẫn Sử Dụng Bộ Tài Liệu Đào Tạo VDI

## 0. Bộ tài liệu này dành cho ai

Bộ tài liệu gồm **28 tài liệu đào tạo** trong thư mục `wiki/topics/`, hướng đến:

| Đối tượng | Mức độ phù hợp |
|---|---|
| System engineer mới chưa biết VDI | ✅ Đọc từ đầu theo roadmap tương ứng |
| Engineer đã biết Windows/VMware, chưa biết Citrix hoặc Horizon | ✅ Chọn roadmap nền tảng cần học |
| Helpdesk / L1 / L2 cần xử lý ticket VDI | ✅ Tập trung nhóm Operations & Support |
| Platform admin quản trị nền tảng VDI | ✅ Đọc đầy đủ cả hai roadmap |
| Engineer chuẩn bị tiếp nhận dự án VDI khách hàng | ✅ Bắt đầu với nhóm Foundation |

---

## 1. Tổng quan hai nền tảng trong bộ tài liệu

Khách hàng đang vận hành **hai hệ thống VDI độc lập**. Bộ tài liệu này phủ cả hai:

| | Omnissa Horizon | Citrix CVAD |
|---|---|---|
| Tên đầy đủ | Omnissa Horizon 8 (trước đây là VMware Horizon) | Citrix Virtual Apps and Desktops |
| Hạ tầng bên dưới | HCI (VMware ESXi / vCenter) | XenServer hoặc VMware ESXi |
| Quy mô | ~1500 đến 2000+ VDI | ~1500 đến 2000+ VDI |
| Broker / Control plane | Connection Server | Delivery Controller |
| Portal người dùng | Horizon Client / Browser | StoreFront |
| Gateway bên ngoài | Unified Access Gateway (UAG) | Citrix Gateway |
| Agent trong desktop | Horizon Agent | Virtual Delivery Agent (VDA) |
| Nhóm desktop | Desktop Pool | Machine Catalog + Delivery Group |
| Quyền truy cập | Entitlement | Delivery Group / Application Group |
| Display protocol | Blast Extreme | HDX / ICA |

> **Quan trọng:** Có những tài liệu **dùng chung** cho cả hai nền tảng (identity, storage, network, monitoring, incident, change, backup, RBAC, support). Có những tài liệu **riêng từng nền tảng** (kiến trúc, pool/catalog, provisioning cụ thể).

---

## 2. Cấu trúc bộ tài liệu theo nhóm chức năng

```
Nhóm 1 — FOUNDATION (Nền tảng chung)
  01, 02, 05, 06, 07, 08, 09, 10, 27

Nhóm 2 — HORIZON (Kiến trúc + Vận hành riêng)
  03, 14

Nhóm 3 — CITRIX (Kiến trúc + Vận hành riêng)
  04, 13

Nhóm 4 — PROVISIONING & IMAGE (Áp dụng cả hai)
  11, 12

Nhóm 5 — OPERATIONS (Vận hành hàng ngày)
  15, 16, 19, 20, 21, 22, 23

Nhóm 6 — INCIDENT & SUPPORT (Xử lý sự cố)
  17, 18, 25, 26

Nhóm 7 — GOVERNANCE & ONBOARDING
  24, 28
```

---

## 3. Roadmap A — Dành cho Omnissa Horizon Admin

> Dành cho engineer quản trị hệ thống Horizon trên HCI. Không cần đọc các tài liệu Citrix-specific ở bước đầu.

### Giai đoạn 1 — Hiểu nền tảng (1–2 ngày)

```
01_VDI_Foundation_Overview.md
  → Hiểu VDI là gì, các lớp kiến trúc, cách tư duy theo lớp khi xử lý lỗi

02_Customer_VDI_Landscape_Overview.md
  → Hiểu bức tranh chung: 2 hệ thống, quy mô, phạm vi vận hành

27_VDI_Glossary_and_Concept_Dictionary.md
  → Nắm thuật ngữ: Connection Server, UAG, Horizon Agent, Pool, Entitlement,
    Blast, vCenter, HCI, datastore, profile, session
```

### Giai đoạn 2 — Hiểu kiến trúc Horizon (1–2 ngày)

```
03_Omnissa_Horizon_Architecture_Overview.md  ← TRỌNG TÂM HORIZON
  → Connection Server, UAG, Horizon Agent, Desktop Pool, Entitlement,
    vCenter, ESXi, HCI, storage, network path, internal vs external flow

05_VDI_Access_Flow_Design.md
  → Luồng kết nối user nội bộ và bên ngoài qua Horizon

06_Identity_and_Domain_Integration_Guide.md
  → AD, DNS, GPO, computer account, Hybrid Entra ID, lỗi identity thường gặp
```

### Giai đoạn 3 — Hiểu hạ tầng bên dưới (1 ngày)

```
07_Hypervisor_and_HCI_Operations_Guide.md
  → ESXi, vCenter, HCI cluster, host, datastore, VM lifecycle, snapshot

08_Storage_Operations_for_VDI.md
  → Datastore, boot storm, logon storm, profile storage, latency, IOPS

09_Network_Operations_for_VDI.md
  → VLAN, firewall, DNS, certificate, load balancer, display protocol path
```

### Giai đoạn 4 — Quản trị Horizon cụ thể (1–2 ngày)

```
14_Omnissa_Desktop_Pool_and_Entitlement_Guide.md  ← TRỌNG TÂM HORIZON
  → Desktop pool, application pool, entitlement, Horizon Agent registration,
    pool availability, tình huống vận hành thường gặp

11_VDI_Provisioning_and_Allocation_Guide.md
  → Tạo mới VDI, cấp phát quyền, mở rộng pool, thu hồi VDI

12_Master_Image_Management_Guide.md
  → Quản lý master image cho Horizon: snapshot, publish, rollback
```

### Giai đoạn 5 — Policy và bảo mật (0.5 ngày)

```
10_VDI_Security_and_Policy_Management_Guide.md
  → Horizon Policy, clipboard, USB, drive mapping, session timeout,
    MFA, RBAC, audit log
```

### Giai đoạn 6 — Vận hành và monitoring (1–2 ngày)

```
15_VDI_Monitoring_and_Alerting_Guide.md
  → Chỉ số cần giám sát: broker, gateway, VDI, session, host, storage, network

16_Daily_Operations_Checklist.md
  → Checklist hàng ngày: health check, alert, session, registration, host, datastore

19_VDI_Performance_and_Capacity_Guide.md
  → CPU, memory, storage latency, IOPS, concurrent session, capacity trend
```

### Giai đoạn 7 — Xử lý sự cố Horizon (1–2 ngày)

```
17_VDI_Incident_Classification_Guide.md
  → Phân loại: 1 user → 1 pool → 1 gateway → 1 cluster → toàn platform

18_VDI_Troubleshooting_Playbook.md
  → Playbook: Login fail, No resource, Launch fail, Horizon Agent unreachable,
    Black screen, Disconnect, Login chậm, Profile issue
    ★ Tập trung Playbook 8: Horizon Agent unreachable/unregistered

26_VDI_Operational_Knowledge_Base.md
  → KB pattern nhanh: 10 loại lỗi thường gặp
```

### Giai đoạn 8 — Change, HA/DR và governance (1 ngày)

```
20_VDI_Change_Management_Guide.md
21_VDI_Patch_and_Upgrade_Guide.md
  → Patch Connection Server, UAG, Horizon Agent, vCenter, ESXi

22_VDI_Backup_and_Recovery_Guide.md
23_VDI_High_Availability_and_Disaster_Recovery_Guide.md
24_VDI_Access_Control_and_RBAC_Guide.md
25_VDI_Support_and_Escalation_Guide.md
28_VDI_Engineer_Onboarding_Guide.md
```

### Bản đồ tài liệu Horizon Admin

```
Nền tảng chung          Horizon-specific         Vận hành chung
─────────────────       ──────────────────       ──────────────────
01 Foundation      →    03 Horizon Arch     →    15 Monitoring
02 Landscape            14 Pool & Entitle        16 Daily Ops
27 Glossary        →    11 Provisioning     →    17 Incident Class
06 Identity             12 Master Image          18 Troubleshooting
07 Hypervisor/HCI                                19 Performance
08 Storage         →    (shared infra)     →    20 Change Mgmt
09 Network                                       21 Patch & Upgrade
10 Security                                      22 Backup
05 Access Flow                                   23 HA/DR
                                                 24 RBAC
                                                 25 Support
                                                 26 KB
                                                 28 Onboarding
```

---

## 4. Roadmap B — Dành cho Citrix CVAD Admin

> Dành cho engineer quản trị hệ thống Citrix CVAD. Không cần đọc các tài liệu Horizon-specific ở bước đầu.

### Giai đoạn 1 — Hiểu nền tảng (1–2 ngày)

```
01_VDI_Foundation_Overview.md
  → Hiểu VDI là gì, các lớp kiến trúc, cách tư duy theo lớp khi xử lý lỗi

02_Customer_VDI_Landscape_Overview.md
  → Hiểu bức tranh chung: 2 hệ thống, quy mô, phạm vi vận hành

27_VDI_Glossary_and_Concept_Dictionary.md
  → Nắm thuật ngữ: Delivery Controller, StoreFront, VDA, Machine Catalog,
    Delivery Group, Citrix Gateway, HDX/ICA, Site Database, License Server
```

### Giai đoạn 2 — Hiểu kiến trúc Citrix CVAD (1–2 ngày)

```
04_Citrix_CVAD_Architecture_Overview.md  ← TRỌNG TÂM CITRIX
  → Delivery Controller, StoreFront, Citrix Gateway, VDA, Site Database,
    License Server, Machine Catalog, Delivery Group, Application Group,
    XenServer / VMware ESXi, HDX/ICA, internal vs external flow

05_VDI_Access_Flow_Design.md
  → Luồng kết nối user nội bộ và bên ngoài qua Citrix

06_Identity_and_Domain_Integration_Guide.md
  → AD, DNS, GPO, computer account, Hybrid Entra ID, lỗi identity thường gặp
```

### Giai đoạn 3 — Hiểu hạ tầng bên dưới (1 ngày)

```
07_Hypervisor_and_HCI_Operations_Guide.md
  → XenServer hoặc ESXi/vCenter tùy triển khai, host, storage repository,
    VM lifecycle, snapshot, host pool

08_Storage_Operations_for_VDI.md
  → Storage repository (XenServer), datastore (VMware), boot storm,
    logon storm, profile storage, latency, IOPS

09_Network_Operations_for_VDI.md
  → VLAN, firewall, DNS, certificate, load balancer, HDX/ICA protocol path
```

### Giai đoạn 4 — Quản trị Citrix cụ thể (1–2 ngày)

```
13_Citrix_Machine_Catalog_and_Delivery_Group_Guide.md  ← TRỌNG TÂM CITRIX
  → Machine Catalog, Delivery Group, Application Group,
    VDA registration, entitlement, tình huống vận hành thường gặp

11_VDI_Provisioning_and_Allocation_Guide.md
  → Tạo mới VDI (MCS/PVS/manual), cấp phát quyền,
    mở rộng catalog, thu hồi VDI

12_Master_Image_Management_Guide.md
  → Quản lý master image cho Citrix: snapshot, publish catalog, rollback
```

### Giai đoạn 5 — Policy và bảo mật (0.5 ngày)

```
10_VDI_Security_and_Policy_Management_Guide.md
  → Citrix Policy, clipboard, USB, drive mapping, session timeout,
    MFA, RBAC, audit log
```

### Giai đoạn 6 — Vận hành và monitoring (1–2 ngày)

```
15_VDI_Monitoring_and_Alerting_Guide.md
  → Chỉ số cần giám sát: broker, gateway, VDA, session, host, storage, network
  → Citrix Director: failed session, VDA state, user experience trend

16_Daily_Operations_Checklist.md
  → Checklist hàng ngày: health check, alert, session, VDA registration, datastore

19_VDI_Performance_and_Capacity_Guide.md
  → CPU, memory, storage latency, IOPS, concurrent session, capacity trend
```

### Giai đoạn 7 — Xử lý sự cố Citrix (1–2 ngày)

```
17_VDI_Incident_Classification_Guide.md
  → Phân loại: 1 user → 1 Catalog/DG → 1 gateway → 1 cluster → toàn platform

18_VDI_Troubleshooting_Playbook.md
  → Playbook: Login fail, No resource, Launch fail, VDA unregistered,
    Black screen, Disconnect, Login chậm, Profile issue
    ★ Tập trung Playbook 7: Citrix VDA unregistered

26_VDI_Operational_Knowledge_Base.md
  → KB pattern nhanh: 10 loại lỗi thường gặp
```

### Giai đoạn 8 — Change, HA/DR và governance (1 ngày)

```
20_VDI_Change_Management_Guide.md
21_VDI_Patch_and_Upgrade_Guide.md
  → Patch Delivery Controller, StoreFront, Citrix Gateway, VDA,
    XenServer / ESXi / vCenter

22_VDI_Backup_and_Recovery_Guide.md
23_VDI_High_Availability_and_Disaster_Recovery_Guide.md
24_VDI_Access_Control_and_RBAC_Guide.md
25_VDI_Support_and_Escalation_Guide.md
28_VDI_Engineer_Onboarding_Guide.md
```

### Bản đồ tài liệu Citrix Admin

```
Nền tảng chung          Citrix-specific          Vận hành chung
─────────────────       ──────────────────       ──────────────────
01 Foundation      →    04 Citrix Arch      →    15 Monitoring
02 Landscape            13 Catalog & DG          16 Daily Ops
27 Glossary        →    11 Provisioning     →    17 Incident Class
06 Identity             12 Master Image          18 Troubleshooting
07 Hypervisor/HCI                                19 Performance
08 Storage         →    (shared infra)     →    20 Change Mgmt
09 Network                                       21 Patch & Upgrade
10 Security                                      22 Backup
05 Access Flow                                   23 HA/DR
                                                 24 RBAC
                                                 25 Support
                                                 26 KB
                                                 28 Onboarding
```

---

## 5. Roadmap C — Dành cho Helpdesk / L1 / L2

> Không cần đọc tài liệu kiến trúc sâu. Tập trung vào nhận diện lỗi, thu evidence và escalation.

```
Bước 1 — Hiểu cơ bản (nửa ngày)
  01_VDI_Foundation_Overview.md   → Phần 9: Cách đọc triệu chứng lỗi theo lớp
  27_VDI_Glossary_and_Concept_Dictionary.md   → Phần 11: Thuật ngữ dễ nhầm

Bước 2 — Phân loại sự cố (nửa ngày)
  17_VDI_Incident_Classification_Guide.md   → 3 câu hỏi phân loại đầu tiên

Bước 3 — Xử lý lỗi thường gặp (1 ngày)
  18_VDI_Troubleshooting_Playbook.md   → Chọn đúng playbook theo symptom
  26_VDI_Operational_Knowledge_Base.md → KB entry 10 loại lỗi phổ biến

Bước 4 — Hỗ trợ và chuyển tuyến (nửa ngày)
  25_VDI_Support_and_Escalation_Guide.md
  16_Daily_Operations_Checklist.md   → Kiểm tra nhanh hàng ngày
```

---

## 6. Danh sách tài liệu phân theo nền tảng

### Tài liệu dùng chung — Đọc bất kể nền tảng nào

| # | Tên file | Trọng tâm |
|---|---|---|
| 01 | 01_VDI_Foundation_Overview.md | Nền tảng VDI, cách tư duy theo lớp |
| 02 | 02_Customer_VDI_Landscape_Overview.md | Bức tranh 2 hệ thống khách hàng |
| 05 | 05_VDI_Access_Flow_Design.md | Luồng kết nối nội bộ và bên ngoài |
| 06 | 06_Identity_and_Domain_Integration_Guide.md | AD, DNS, GPO, identity |
| 07 | 07_Hypervisor_and_HCI_Operations_Guide.md | ESXi, vCenter, XenServer, HCI |
| 08 | 08_Storage_Operations_for_VDI.md | Storage, profile, boot/logon storm |
| 09 | 09_Network_Operations_for_VDI.md | Mạng, firewall, certificate, LB |
| 10 | 10_VDI_Security_and_Policy_Management_Guide.md | Policy, RBAC, MFA |
| 11 | 11_VDI_Provisioning_and_Allocation_Guide.md | Tạo mới, cấp phát, thu hồi VDI |
| 12 | 12_Master_Image_Management_Guide.md | Quản lý master image |
| 15 | 15_VDI_Monitoring_and_Alerting_Guide.md | Giám sát các lớp |
| 16 | 16_Daily_Operations_Checklist.md | Checklist hàng ngày |
| 17 | 17_VDI_Incident_Classification_Guide.md | Phân loại sự cố |
| 18 | 18_VDI_Troubleshooting_Playbook.md | Playbook xử lý 9 loại lỗi |
| 19 | 19_VDI_Performance_and_Capacity_Guide.md | Hiệu năng, capacity |
| 20 | 20_VDI_Change_Management_Guide.md | Quy trình thay đổi |
| 21 | 21_VDI_Patch_and_Upgrade_Guide.md | Patch và nâng cấp |
| 22 | 22_VDI_Backup_and_Recovery_Guide.md | Backup và phục hồi |
| 23 | 23_VDI_High_Availability_and_Disaster_Recovery_Guide.md | HA và DR |
| 24 | 24_VDI_Access_Control_and_RBAC_Guide.md | Phân quyền |
| 25 | 25_VDI_Support_and_Escalation_Guide.md | Hỗ trợ và escalation |
| 26 | 26_VDI_Operational_Knowledge_Base.md | KB lỗi thường gặp |
| 27 | 27_VDI_Glossary_and_Concept_Dictionary.md | Từ điển thuật ngữ |
| 28 | 28_VDI_Engineer_Onboarding_Guide.md | Lộ trình onboarding |

### Tài liệu riêng Omnissa Horizon

| # | Tên file | Trọng tâm |
|---|---|---|
| 03 | 03_Omnissa_Horizon_Architecture_Overview.md | Connection Server, UAG, Horizon Agent, Desktop Pool, HCI, vCenter |
| 14 | 14_Omnissa_Desktop_Pool_and_Entitlement_Guide.md | Desktop Pool, Application Pool, Entitlement, Horizon Agent registration |

### Tài liệu riêng Citrix CVAD

| # | Tên file | Trọng tâm |
|---|---|---|
| 04 | 04_Citrix_CVAD_Architecture_Overview.md | Delivery Controller, StoreFront, Citrix Gateway, VDA, Machine Catalog, Delivery Group, Site DB, License Server |
| 13 | 13_Citrix_Machine_Catalog_and_Delivery_Group_Guide.md | Machine Catalog, Delivery Group, Application Group, VDA registration |

---

## 7. Tra cứu nhanh theo tình huống

| Tình huống | Đọc ngay |
|---|---|
| User không thấy desktop | 18 Playbook 5, 26 KB-2, 17 Phần 4.1 |
| VDA unregistered hàng loạt | 18 Playbook 7, 13, 17 Phần 4.3 |
| Horizon Agent unreachable | 18 Playbook 8, 14, 17 Phần 4.3 |
| Login chậm đầu giờ | 18 Playbook 9, 08, 26 KB-6 |
| Màn hình đen | 18 Playbook 10, 26 KB-5 |
| External user không launch được | 18 Playbook 6, 09, 05, 17 Phần 4.5 |
| Image update gây lỗi hàng loạt | 12, 18 Scenario 4, 20, 17 Phần 4.3 |
| Profile / temporary profile | 18 Playbook 12, 26 KB-7, 08 |
| Certificate sắp hết hạn | 09, 20, 21 |
| Datastore gần đầy | 08, 19, 17 Phần 4.6 |
| Cấp quyền user mới | 11, 06, 13 (Citrix) hoặc 14 (Horizon) |
| Tạo mới VDI / mở rộng pool | 11, 12, 13 (Citrix) hoặc 14 (Horizon) |
| Cần hiểu keyword kỹ thuật nhanh | 27 Phần 3–10 |
| Chuẩn bị hỗ trợ khách hàng | 25, 17, 28 |

---

## 8. Nguyên tắc quan trọng khi đọc và dùng bộ tài liệu

1. **Tài liệu này là Lớp 1 — Foundation.** Nội dung kỹ thuật dựa trên wiki/sources đã ingest; không bịa topology, version, log path hay SLA của khách hàng.

2. **Phần "Need Customer Confirmation"** trong mỗi tài liệu là danh sách thông tin cần hỏi thêm trước khi biến tài liệu thành SOP thực tế.

3. **Khi xử lý lỗi thực tế,** luôn bắt đầu từ File 17 (phân loại scope) rồi chọn đúng playbook trong File 18, không tự quyết định hành động trước khi có evidence.

4. **Hai nền tảng có nhiều điểm chung** (identity, storage, network, monitoring, change). Khi lỗi xảy ra trên cả Horizon lẫn Citrix cùng lúc, thường nguyên nhân nằm ở shared dependency như AD/DNS, storage, hoặc network core.

5. **Glossary (File 27)** là điểm tra cứu nhanh khi gặp thuật ngữ lạ. Mỗi thuật ngữ có phần "Khi lỗi thường thấy" giúp kết nối ngay với troubleshooting.

---

## 9. Liên kết nội bộ

- [[topics/01_VDI_Foundation_Overview]] — Nền tảng bắt buộc
- [[topics/03_Omnissa_Horizon_Architecture_Overview]] — Horizon Roadmap bắt đầu
- [[topics/04_Citrix_CVAD_Architecture_Overview]] — Citrix Roadmap bắt đầu
- [[topics/17_VDI_Incident_Classification_Guide]] — Phân loại sự cố
- [[topics/18_VDI_Troubleshooting_Playbook]] — Playbook xử lý lỗi
- [[topics/27_VDI_Glossary_and_Concept_Dictionary]] — Từ điển thuật ngữ
- [[topics/28_VDI_Engineer_Onboarding_Guide]] — Lộ trình engineer mới
