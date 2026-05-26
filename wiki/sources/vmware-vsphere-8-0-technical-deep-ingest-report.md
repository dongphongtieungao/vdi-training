---
id: source-vmware-vsphere-8-0-technical-deep-ingest-report
title: VMware vSphere 8.0 - Technical Deep Ingest Report for VDI Training
type: source
created: 2026-05-26
updated: 2026-05-26
authors:
  - VMware
year: 2026
importance: 5
urls: []
raw_paths:
  - raw/sources/vmware-vsphere-8-0.txt
provenance: replayable
confidence: high
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

Báo cáo này là bản technical deep ingest tổng hợp cho source VMware vSphere 8.0, được viết để phục vụ bộ tài liệu đào tạo VDI cho system engineer. Báo cáo không thay thế raw source và không copy dài nội dung vendor. Nó đóng vai trò lớp tri thức trung gian giữa source 15MB và các tài liệu training trong `wiki/topics`.

Trọng tâm của báo cáo là biến nội dung vSphere thành tri thức vận hành: engineer cần hiểu nguyên lý nào, kiểm tra thành phần nào, metric/log/evidence nào cần lấy, failure mode nào hay gặp trong môi trường VDI, change nào có blast radius lớn, rollback cần gì, và thông tin khách hàng nào còn phải xác nhận.

## Length and Depth Control

| Trường | Giá trị |
|---|---|
| Target minimum length | 50,000 characters |
| Actual estimated length | 53,933 characters measured after final edit |
| Meets minimum length | Yes |
| If No, Depth Exception reason | Not applicable |

## Source Inventory

| Trường | Giá trị |
|---|---|
| Raw file | `raw/sources/vmware-vsphere-8-0.txt` |
| File size | 15,820,476 bytes |
| Estimated lines | 162,031 text lines by PowerShell Measure; 243,951 logical lines by Node newline split |
| Estimated characters | 15,069,560 characters by PowerShell Measure; 15,790,036 characters by Node raw string length |
| Source type | Vendor documentation corpus, release notes, platform administration, installation, upgrade, operations and monitoring documentation |
| Product/platform | VMware vSphere 8.0, ESXi, vCenter Server, VMware Host Client, vSphere Client, VMware Aria Operations plug-in |
| Version | vSphere 8.0 family |
| Ingest mode | Technical deep ingest report plus shard pages and coverage ledger |

## Coverage Ledger

| Chapter | Title | Line range | Extracted into | Main knowledge | Status |
|---|---|---:|---|---|---|
| CH00 | Front matter and table of contents | 1-6195 | [[sources/vmware-vsphere-8-0]] | Source structure, section boundaries, chapter map | Extracted |
| CH01 | Release Notes | 6196-73043 | [[sources/vmware-vsphere-8-0-part-01-release-and-lifecycle]] | Release notes, known issues, compatibility, patch lifecycle | Extracted |
| CH02 | ESXi Installation and Setup / ESXi Upgrade | 73044-90797 | [[sources/vmware-vsphere-8-0-part-02-esxi-install-upgrade]] | ESXi host requirements, install, firewall, syslog, upgrade, support bundle | Extracted |
| CH03 | vCenter Server Installation and Setup / Upgrade | 90798-103073 | [[sources/vmware-vsphere-8-0-part-03-vcenter-install-upgrade]] | VCSA, backup/restore, upgrade, integration dependency | Extracted |
| CH04 | vSphere Authentication / Host and Cluster Lifecycle | 103074-123608 | [[sources/vmware-vsphere-8-0-part-04-authentication-lifecycle]] | Identity source, SSO, roles, permissions, lifecycle, remediation | Extracted |
| CH05 | vCenter Server Configuration / Host Management / VM Administration | 123609-150042 | [[sources/vmware-vsphere-8-0-part-05-vcenter-host-vm-admin]] | VM lifecycle, template, snapshot, VMware Tools, inventory, tasks/events | Extracted |
| CH06 | Host Profiles / Networking | 150043-165229 | [[sources/vmware-vsphere-8-0-part-06-host-profiles-networking]] | Host Profiles, vSwitch, vDS, port groups, VMkernel, rollback | Extracted |
| CH07 | vSphere Storage | 165230-182830 | [[sources/vmware-vsphere-8-0-part-07-storage]] | Datastore, VMFS, NFS, vSAN, VVols, storage policy, multipathing, latency | Extracted |
| CH08 | vSphere Security / Resource Management / Availability | 182831-221104 | [[sources/vmware-vsphere-8-0-part-08-security-resource-availability]] | RBAC, certificates, CPU/memory, DRS, HA, admission control, FT | Extracted |
| CH09 | Monitoring and Performance / Host Client / Aria Operations | 221105-243951 | [[sources/vmware-vsphere-8-0-part-09-monitoring-host-client-aria]] | Alarms, tasks, events, performance charts, syslog, Host Client, Aria | Extracted |

## Technical Executive Summary

VMware vSphere 8.0 trong bối cảnh VDI là lớp nền vận hành các desktop VM, management VM, template, datastore, network và cluster capacity. Nguyên lý kỹ thuật cốt lõi không nằm ở một tính năng đơn lẻ, mà ở quan hệ giữa control plane và runtime plane: vCenter điều phối inventory, task, policy, lifecycle và permission; ESXi thực thi workload; datastore và network cung cấp đường sống cho VM; monitoring cung cấp bằng chứng; HA/DRS/resource management quyết định khả năng chịu lỗi và cân bằng tải. Tác giả/vendor tiếp cận bằng cách chia documentation thành release notes, cài đặt, nâng cấp, authentication, lifecycle, VM administration, networking, storage, security, resource management, availability và monitoring. Với system engineer vận hành VDI quy mô 1500-2000+ máy, tri thức này quan trọng vì lỗi VDI không luôn nằm ở Horizon/CVAD. Một login chậm, launch fail, VDA/Horizon Agent unreachable, black screen hoặc mass disconnect có thể bắt nguồn từ host, datastore, vCenter task, RBAC, port group, storage path, patch regression hoặc thiếu evidence monitoring.

## In-depth Technical Insights

### Insight 1 - Core Principle Analysis

| Mục | Nội dung |
|---|---|
| Diễn giải | Nguyên lý cốt lõi của vSphere trong VDI là phân tách nhưng liên kết chặt chẽ giữa control plane và execution plane. vCenter là nơi điều phối inventory, task, permission, lifecycle và automation. ESXi là nơi VM chạy thật. Storage và network là data plane dependency cho VM. Monitoring là evidence plane giúp chứng minh trạng thái. |
| Cơ sở lý thuyết | Không có công thức toán học trong source; nền tảng là kiến trúc hệ thống phân lớp, dependency chain và state-based operations. Nếu một state trong chain sai, ví dụ VM off, datastore latency cao, port group sai, service account thiếu quyền, vCenter task fail, thì VDI platform phía trên có thể biểu hiện lỗi mặc dù broker hoặc gateway vẫn hoạt động. |
| Ví dụ minh họa | Khi user báo không launch được desktop, engineer mới thường nhìn ngay vào broker. Nhưng source vSphere cho thấy cần kiểm tra thêm VM power state, vCenter task, host state, datastore, network mapping và permission. Nếu VM không power on do datastore full, lỗi gốc nằm ở storage/vSphere, không phải entitlement. |
| Ý nghĩa với VDI | Với 1500-2000+ VDI, một lỗi ở vSphere có thể không ảnh hưởng một user mà ảnh hưởng hàng trăm VM theo host, datastore, cluster, port group hoặc pool. Engineer phải biết map user symptom về infrastructure boundary. |

### Insight 2 - Pedagogical Approach Analysis

| Mục | Nội dung |
|---|---|
| Cấu trúc logic | Vendor documentation đi từ release/lifecycle đến install/upgrade, sau đó vào authentication, management, VM administration, networking, storage, security, resource, availability và monitoring. Đây là logic từ nền tảng hạ tầng đến vận hành và evidence. |
| Điểm mạnh | Cấu trúc theo domain giúp engineer tra cứu đúng vùng: patch thì đọc release/lifecycle, VM issue thì đọc VM administration, performance thì đọc storage/resource/monitoring, access/automation issue thì đọc authentication/RBAC. |
| Điểm có thể gây khó hiểu | Người mới dễ bị ngợp vì tài liệu không viết theo luồng VDI end-to-end. Source mô tả vSphere chung, không nói trực tiếp “khi Horizon launch fail thì làm gì”. Do đó cần layer training chuyển ngôn ngữ vendor sang symptom-based operations. |
| Cách giải thích thay thế | Dạy theo câu hỏi vận hành: user bị gì, affected scope là gì, object vSphere nào liên quan, metric/log nào chứng minh, change gần nhất là gì, escalation cho team nào. Sau đó mới quay lại vendor chapter để giải thích cơ chế. |

### Insight 3 - Practical Application and Industry Relevance

| Mục | Nội dung |
|---|---|
| Case Study 1 | Một tổ chức chạy Horizon trên HCI gặp login chậm lúc 8h sáng. Broker health bình thường, nhưng datastore latency tăng cùng lúc nhiều VM boot/login. Tri thức từ storage, monitoring và resource management giúp engineer chứng minh gốc issue là storage/capacity thay vì Horizon Connection Server. |
| Case Study 2 | Một môi trường CVAD dùng VMware bị launch fail sau khi security team thay role service account trong vCenter. Citrix Delivery Controller báo không power được machine. Tri thức từ authentication/RBAC và vCenter tasks giúp xác định permission denied ở object scope vCenter, không phải lỗi VDA. |
| Công cụ / phần mềm liên quan | vSphere Client, ESXi Host Client, VMware Aria Operations, syslog hoặc Aria Operations for Logs, Horizon Console, Citrix Studio, Citrix Director, monitoring dashboard, backup platform, ticket/change system. |
| Tầm quan trọng với engineer | Engineer phải hiểu vSphere để không troubleshoot VDI trong silo. VDI là service nhiều lớp; nếu không đọc được vCenter task, datastore metric, HA alarm, port group mapping hoặc RBAC evidence thì escalation sẽ yếu và RCA thiếu cơ sở. |

## Role in the Learning Pathway

| Hướng kết nối | Nội dung |
|---|---|
| Kết nối ngược | Source này dựa trên kiến thức nền về VDI, VM, hypervisor, identity, network, storage, monitoring và change management. Người học cần hiểu desktop VM, broker, agent, profile, session và access flow trước khi đi sâu vào vSphere. |
| Kết nối xuôi | Đây là nền cho troubleshooting playbook, performance/capacity, patch/upgrade, backup/recovery, HA/DR, RBAC, support escalation và daily operations. |
| Prerequisites | Kiến thức cơ bản về virtualization, VM lifecycle, vCenter/ESXi, datastore, VLAN/port group, AD/SSO, monitoring metric và incident/change process. |
| Learning outcome | Đọc xong, engineer phải biết phân tích lỗi VDI có thể bắt nguồn từ vSphere, biết lấy evidence ở vCenter/ESXi/datastore/network/monitoring, biết đánh giá impact của change và biết khi nào escalation. |

## Points of Caution and Potential Misconceptions

| Misconception / Caution | Vì sao dễ sai | Cách hiểu đúng | Mẹo học / vận hành |
|---|---|---|---|
| “User launch fail chắc chắn là lỗi broker.” | User-facing symptom xuất hiện ở Horizon/CVAD nên dễ đổ lỗi platform VDI. | Broker chỉ là một lớp. VM power state, vCenter task, datastore, network, agent và permission đều có thể gây launch fail. | Luôn tách lỗi thành login, entitlement, launch, protocol, session runtime và infra task. |
| “vCenter down thì toàn bộ VDI down ngay.” | vCenter là trung tâm quản trị nên dễ nghĩ nó nằm trong mọi data path. | Session đang chạy có thể vẫn tiếp tục, nhưng provisioning, power operation, image publish, maintenance và inventory task bị ảnh hưởng. | Phân biệt data plane của user session và control plane của operations. |
| “Snapshot là backup.” | Snapshot dễ tạo và rollback nhanh nên hay bị dùng sai. | Snapshot là trạng thái tạm thời; để lâu gây tăng datastore và rủi ro performance. Backup/recovery cần quy trình riêng. | Luôn hỏi snapshot dùng cho change nào, retention bao lâu, rollback đã test chưa. |
| “Datastore còn dung lượng là storage ổn.” | Capacity dễ nhìn hơn latency/path/IOPS. | Storage health cần xem capacity, latency, IOPS, throughput, path, backend event, snapshot growth. | Khi login chậm hoặc boot storm, xem latency theo thời điểm, không chỉ free space. |
| “HA bật nghĩa là DR đã ổn.” | HA và DR đều nói về availability nên dễ nhầm. | HA xử lý lỗi cục bộ; DR xử lý mất site/dữ liệu và cần RPO/RTO/validation riêng. | DR test phải kiểm tra user login/launch/profile/app access, không chỉ VM powered on. |

## Key Terminology and Formulas

| Thuật ngữ / Ký hiệu | Định nghĩa / Diễn giải ngắn gọn | Bối cảnh sử dụng |
|---|---|---|
| ESXi | Hypervisor chạy trực tiếp trên host vật lý để chạy VM. | Kiểm tra host, VM placement, maintenance, patch, hardware issue. |
| vCenter Server | Control plane quản trị ESXi, cluster, VM, datastore, network, roles và tasks. | Provisioning, image publish, power operation, inventory, RBAC. |
| vCenter Server Appliance / VCSA | Appliance VM chạy vCenter services. | Backup/restore, upgrade, service health. |
| Datastore | Nơi lưu VM files, disks, snapshots, logs. | Storage capacity, latency, power/provision/snapshot issue. |
| VMFS / NFS / vSAN / VVols | Các loại hoặc mô hình datastore/storage backend. | Phân tích storage issue và ownership. |
| Snapshot | Trạng thái tạm thời của VM tại một thời điểm. | Master image, rollback ngắn hạn, consolidation risk. |
| VMware Tools | Guest tools giúp vSphere hiểu và thao tác guest OS tốt hơn. | VM state, graceful shutdown, monitoring, operations. |
| vSwitch / vDS | Virtual switch tiêu chuẩn hoặc distributed switch. | Network mapping, port group, uplink, VLAN. |
| Port group | Nhóm cấu hình mạng cho VM/VMkernel adapter. | Agent unreachable, wrong VLAN, VDI network mapping. |
| VMkernel adapter | Interface dùng cho management, vMotion, storage hoặc host services. | Host management, storage network, vMotion issue. |
| DRS | Distributed Resource Scheduler, cân bằng workload theo tài nguyên. | Capacity, maintenance, performance. |
| vSphere HA | Cơ chế restart VM khi host failure trong cluster. | Availability, failover validation. |
| Admission Control | Cơ chế giữ lại capacity cho HA failover. | HA design và capacity planning. |
| Resource pool | Vùng phân bổ tài nguyên với shares/limits/reservations. | Performance and capacity issue. |
| Role / Permission | Mô hình quyền trong vSphere. | Service account, admin access, RBAC. |
| Task / Event | Dấu vết hành động và sự kiện trong vCenter. | Evidence/RCA/change validation. |
| Alarm | Cảnh báo trong vSphere. | Monitoring and daily operations. |
| Syslog | Hệ thống ghi log tập trung hoặc host logging. | Incident evidence and escalation. |
| Support bundle | Gói log/diagnostic cho vendor hoặc platform escalation. | Host/vCenter issue escalation. |

Không có công thức toán học trong source này; các thuật ngữ vận hành quan trọng được liệt kê ở bảng trên.

## Knowledge Atoms

| ID | Knowledge atom | Loại tri thức | Vì sao quan trọng trong VDI | Source locator | Dùng cho topic |
|---|---|---|---|---|---|
| KA-001 | vSphere là lớp nền cho desktop VM, management VM, template, datastore, cluster và network port group. | Architecture | VDI không vận hành độc lập khỏi hypervisor. | Full source, CH02-CH09 | [[topics/7_Hypervisor_and_HCI_Operations_Guide]] |
| KA-002 | Release notes cần được xem như risk register trước patch. | Change | Patch sai có thể ảnh hưởng cả cluster/pool. | CH01, lines 6196-73043 | [[topics/21_VDI_Patch_and_Upgrade_Guide]] |
| KA-003 | Known issues trong release notes là evidence khi lỗi xuất hiện sau change. | Troubleshooting | Giúp phân biệt regression với lỗi cấu hình VDI. | CH01 | [[topics/18_VDI_Troubleshooting_Playbook]] |
| KA-004 | ESXi host là boundary ảnh hưởng một nhóm VM. | Architecture | Incident có thể gom theo host. | CH02 | [[topics/17_VDI_Incident_Classification_Guide]] |
| KA-005 | ESXi firewall và network service ảnh hưởng management/monitoring/storage path. | Operation | Host có thể unreachable hoặc thiếu monitoring. | CH02 | [[topics/9_Network_Operations_for_VDI]] |
| KA-006 | Syslog phải được cấu hình trước incident. | Evidence | Không có log thì RCA yếu. | CH02, CH09 | [[topics/15_VDI_Monitoring_and_Alerting_Guide]] |
| KA-007 | Support bundle là evidence chuẩn khi escalate host issue. | Support | Vendor cần log đầy đủ. | CH02 | [[topics/25_VDI_Support_and_Escalation_Guide]] |
| KA-008 | vCenter là operations control plane, không nhất thiết là user data path. | Architecture | Giúp phân biệt session đang chạy với provisioning failure. | CH03 | [[topics/1_VDI_Foundation_Overview]] |
| KA-009 | vCenter backup/restore phải validate Horizon/CVAD integration. | Recovery | Restore vCenter không đủ nếu VDI task vẫn fail. | CH03 | [[topics/22_VDI_Backup_and_Recovery_Guide]] |
| KA-010 | vCenter task/event là evidence chính cho power/provision/image operation. | Evidence | Cần task error để phân tuyến đúng. | CH03, CH05 | [[topics/25_VDI_Support_and_Escalation_Guide]] |
| KA-011 | Identity source/SSO/certificate ảnh hưởng admin access và automation. | Security | Lỗi có thể làm mất khả năng xử lý incident. | CH03, CH04, CH08 | [[topics/6_Identity_and_Domain_Integration_Guide]] |
| KA-012 | vSphere permission phải đúng cả role và scope. | RBAC | Service account có quyền sai scope vẫn task fail. | CH04 | [[topics/24_VDI_Access_Control_and_RBAC_Guide]] |
| KA-013 | Lifecycle remediation có thể reboot host hoặc thay desired state. | Change | Có blast radius lớn trong VDI. | CH04 | [[topics/20_VDI_Change_Management_Guide]] |
| KA-014 | Compliance report là precheck trước cluster remediation. | Operation | Host drift gây patch không đồng nhất. | CH04 | [[topics/21_VDI_Patch_and_Upgrade_Guide]] |
| KA-015 | VM power state là check đầu khi launch fail. | Troubleshooting | Broker đúng nhưng VM không chạy thì user vẫn fail. | CH05 | [[topics/18_VDI_Troubleshooting_Playbook]] |
| KA-016 | VMware Tools status ảnh hưởng guest operations. | Operation | Shutdown/reboot/status có thể sai nếu Tools lỗi. | CH05 | [[topics/7_Hypervisor_and_HCI_Operations_Guide]] |
| KA-017 | Template/snapshot là nền của master image workflow. | Image | Image publish/rollback phụ thuộc snapshot đúng. | CH05 | [[topics/12_Master_Image_Management_Guide]] |
| KA-018 | Snapshot không phải backup dài hạn. | Backup | Để lâu gây datastore growth/performance risk. | CH05, CH07 | [[topics/22_VDI_Backup_and_Recovery_Guide]] |
| KA-019 | Port group mapping quyết định VM thuộc network nào. | Network | Sai port group làm Agent/VDA không register. | CH06 | [[topics/9_Network_Operations_for_VDI]] |
| KA-020 | Distributed switch change có blast radius nhiều host. | Change | Một lỗi vDS có thể ảnh hưởng nhiều pool. | CH06 | [[topics/20_VDI_Change_Management_Guide]] |
| KA-021 | VMkernel network khác VM network. | Architecture | Cần tách management/storage/vMotion khỏi desktop traffic. | CH06 | [[topics/7_Hypervisor_and_HCI_Operations_Guide]] |
| KA-022 | Host Profile chuẩn hóa nhưng cũng có thể nhân rộng cấu hình sai. | Operation | Apply sai có thể ảnh hưởng nhiều host. | CH06 | [[topics/20_VDI_Change_Management_Guide]] |
| KA-023 | Datastore full có thể gây power/provision/snapshot fail. | Troubleshooting | Pool thiếu máy hoặc update fail. | CH07 | [[topics/8_Storage_Operations_for_VDI]] |
| KA-024 | Storage latency ảnh hưởng trực tiếp login/launch/user experience. | Performance | Login storm làm issue lan rộng. | CH07 | [[topics/19_VDI_Performance_and_Capacity_Guide]] |
| KA-025 | Storage policy quyết định placement/compliance. | Operation | Sai policy có thể đặt VM sai tier/resilience. | CH07 | [[topics/11_VDI_Provisioning_and_Allocation_Guide]] |
| KA-026 | Multipathing/path state là evidence khi storage chập chờn. | Evidence | Một path lỗi có thể gây latency thay vì outage rõ. | CH07 | [[topics/25_VDI_Support_and_Escalation_Guide]] |
| KA-027 | RBAC ảnh hưởng trực tiếp VDI automation. | Security | Quyền thiếu làm task fail; quyền thừa gây rủi ro. | CH08 | [[topics/24_VDI_Access_Control_and_RBAC_Guide]] |
| KA-028 | CPU/memory contention có thể làm VDI chậm dù broker khỏe. | Performance | User experience phụ thuộc host resource. | CH08 | [[topics/19_VDI_Performance_and_Capacity_Guide]] |
| KA-029 | DRS placement ảnh hưởng balancing và maintenance. | Availability | Host imbalance gây performance issue. | CH08 | [[topics/23_VDI_High_Availability_and_Disaster_Recovery_Guide]] |
| KA-030 | HA admission control quyết định failover capacity. | HA/DR | HA bật nhưng thiếu capacity vẫn không cứu được service. | CH08 | [[topics/23_VDI_High_Availability_and_Disaster_Recovery_Guide]] |
| KA-031 | Alarms là tín hiệu đầu của host/datastore/network/HA issue. | Monitoring | Phát hiện trước khi user report. | CH09 | [[topics/15_VDI_Monitoring_and_Alerting_Guide]] |
| KA-032 | Tasks/events tạo timeline cho RCA. | Evidence | Giúp biết lỗi xảy ra sau action nào. | CH09 | [[topics/17_VDI_Incident_Classification_Guide]] |
| KA-033 | Performance charts giúp correlate symptom với metrics. | Troubleshooting | Tránh kết luận thiếu dữ liệu. | CH09 | [[topics/19_VDI_Performance_and_Capacity_Guide]] |
| KA-034 | Host Client hữu ích khi cần kiểm tra host trực tiếp. | Operation | Khi vCenter hạn chế, có thể lấy host evidence. | CH09 | [[topics/7_Hypervisor_and_HCI_Operations_Guide]] |
| KA-035 | Aria Operations nếu có giúp correlation/capacity trend. | Monitoring | Phù hợp môi trường VDI lớn. | CH09 | [[topics/15_VDI_Monitoring_and_Alerting_Guide]] |
| KA-036 | Evidence phải có time window và timezone. | Support | Sai thời gian làm correlation sai. | CH09 | [[topics/25_VDI_Support_and_Escalation_Guide]] |

## Architecture Knowledge

### Layered Architecture View for VDI

| Lớp | Thành phần vSphere | Vai trò trong VDI | State cần quan sát | Rủi ro khi lỗi |
|---|---|---|---|---|
| Control plane | vCenter Server, vSphere Client, tasks, events, roles | Quản trị inventory, host, cluster, VM, datastore, network, template, snapshot | Service health, task success, permission, certificate, SSO | Provisioning fail, image publish fail, host maintenance blocked |
| Execution plane | ESXi host | Chạy desktop VM và management VM | Connected state, hardware, CPU/memory, NIC/HBA, syslog | Mass disconnect theo host, VM power issue |
| Storage plane | Datastore, VMFS/NFS/vSAN/VVols, policy, path | Lưu VM disks, snapshots, template, logs | Capacity, latency, IOPS, path state, snapshot growth | Login chậm, VM stun, datastore full, snapshot fail |
| Network plane | vSwitch, vDS, port group, uplink, VMkernel | Kết nối VM tới VLAN, broker, DC, profile, app, storage/management | Port group, VLAN, uplink, packet loss, VMkernel status | Agent unreachable, disconnect, wrong network |
| Security plane | SSO, identity source, roles, permissions, certificates | Kiểm soát ai được thao tác và trust path | Role scope, certificate expiry, login events | Permission denied, admin lockout, automation fail |
| Availability plane | DRS, HA, admission control, FT | Cân bằng tải và failover | Cluster capacity, HA alarms, DRS recommendations | Failover không đủ capacity, performance imbalance |
| Evidence plane | Alarms, tasks, events, performance charts, syslog, support bundle | Chứng minh trạng thái và nguyên nhân | Alert trend, event timeline, log availability | RCA yếu, escalation thiếu dữ liệu |

### Control Plane vs Data Plane

Trong VDI, vCenter thường không nằm trong protocol path của user session. User có thể đang kết nối desktop qua Horizon Blast hoặc Citrix ICA/HDX trong khi vCenter gặp issue. Tuy nhiên, vCenter lại rất quan trọng cho operations: tạo VM, power on/off, update image, snapshot, migrate, host maintenance, inventory, permissions. Đây là điểm người mới thường nhầm. Khi vCenter down, không nên lập tức kết luận toàn bộ VDI service đã down; cần kiểm tra user session hiện hữu, broker health, gateway health và các operation đang cần vCenter.

### Dependency Chain for Common VDI Operations

| Operation | vSphere dependency | Nếu dependency lỗi | Evidence |
|---|---|---|---|
| User launch desktop | VM power state, VM network, Agent/VDA service, datastore availability | Launch fail, black screen, unavailable desktop | VM state, task/event, datastore metric, port group |
| Image publish | Template/golden image, snapshot, datastore, network mapping, vCenter task | Pool update fail, mass unavailable desktops | Snapshot tree, task error, image version |
| Provisioning new VDI | vCenter service account, folder/resource pool/datastore/network inventory | Machine creation fail | Permission error, inventory path, task log |
| Host maintenance | DRS/HA capacity, vMotion/network/storage path | Session disruption, evacuation fail | Maintenance task, host events, cluster capacity |
| DR validation | vCenter restore, host connected, datastore visible, network mapping, broker integration | VM up but VDI unusable | Restore record, login/launch test, integration status |

## Operational Knowledge

### Daily and Incident Operations

| Tác vụ vận hành | Trigger | Precheck | Cách kiểm tra high-level | Expected normal | Abnormal signal | Evidence | Escalation |
|---|---|---|---|---|---|---|---|
| Kiểm tra host health | Daily / user impact by group | Danh sách cluster/host chạy VDI | vSphere Client cluster/host summary | Hosts connected, no critical hardware alarms | Host not responding, hardware/NIC/HBA alarms | Host screenshot, events, affected VM list | Virtualization/HCI owner |
| Kiểm tra datastore | Daily / login slow / provisioning fail | Xác định datastore chứa pool/image/profile nếu có | Datastore monitor: capacity, latency, IOPS | Capacity healthy, latency stable | Full/near full, latency spike, path issue | Capacity/latency chart, datastore name | Storage/HCI owner |
| Kiểm tra VM state | Launch fail / pool capacity issue | User, pool, desktop VM name | VM summary, tasks/events, Tools status | VM powered on, Tools OK, no failed task | Powered off, task failed, Tools not running | VM state, task error, timestamp | VDI platform / virtualization |
| Kiểm tra port group/network | Agent unreachable / disconnect | Failed VM vs working VM | VM NIC, port group, VLAN, uplink health | Correct port group, reachable broker/DC | Wrong network, uplink errors, packet loss | VM NIC config, network events | Network/virtualization |
| Kiểm tra vCenter tasks/events | Any operation failure | Time window and affected object | Tasks/Events tab | Tasks success or expected warning | Permission denied, timeout, host/datastore error | Task ID/error, event timeline | Platform owner |
| Kiểm tra RBAC/service account | Provisioning/power fail | Service account name and object scope | Permissions at vCenter/folder/cluster/datastore/network | Correct role/scope | Permission denied | Role screenshot/export, task error | Security/platform |
| Kiểm tra HA/DRS | Host issue / maintenance / capacity incident | Cluster policy and affected workload | HA/DRS alarms, recommendations, capacity | HA healthy, DRS balanced | HA warning, imbalance, admission issue | HA event, capacity summary | Platform/DR owner |
| Kiểm tra monitoring evidence | RCA / escalation | Incident time window | Alarms, events, performance charts, syslog | Evidence covers incident time | No data, wrong window, missing syslog | Evidence package | Monitoring owner |

### Operational Normal vs Abnormal Signals

| Area | Normal | Abnormal | Cách diễn giải |
|---|---|---|---|
| Host | Connected, no critical alarms, stable resource | Not responding, hardware fault, NIC/HBA errors | Khoanh vùng affected VDI theo host. |
| vCenter | Services healthy, tasks complete | vSphere Client inaccessible, tasks fail | Tách user session data plane khỏi operations control plane. |
| Datastore | Capacity and latency stable | Full, high latency, path down, consolidation warning | Gắn với login/launch/power/image symptom. |
| Network | Correct port group, stable uplinks | Wrong VLAN, uplink errors, management loss | So sánh working/failing VM và host. |
| RBAC | Service account tasks work | Permission denied | Kiểm tra role and scope, không chỉ username. |
| HA/DRS | Cluster balanced, sufficient failover | Admission warning, DRS imbalance | Đánh giá capacity before change. |
| Monitoring | Alarms/events/logs available | Missing time window, no syslog | Không kết luận root cause nếu thiếu evidence. |

## Troubleshooting Knowledge

| Failure mode | User symptom | Platform signal | Likely layer | First checks | Evidence package | Do not do | Escalation condition |
|---|---|---|---|---|---|---|---|
| Host failure | Many users disconnect or desktops unavailable | Host not responding, HA event | ESXi/HCI | Map users/VMs to host, check host events, check HA | Host events, affected VM list, HA task, support bundle | Do not reboot randomly without owner approval | Host hardware/path issue, many VMs affected |
| Datastore latency | Slow login, black screen, app lag | Datastore latency spike, VM stun | Storage/HCI | Check datastore metrics, backup window, session count | Latency chart, IOPS, affected datastore/pool | Do not delete snapshots blindly | Latency/capacity beyond agreed threshold |
| Datastore full | Power/provision/snapshot fail | Task error, low free space | Storage | Check datastore free, snapshot tree, failed task | Capacity chart, task error, snapshot list | Do not expand/delete without change | Production datastore near full |
| Permission denied | Pool/catalog power/provision fail | vCenter task permission denied | RBAC | Check service account role and scope | Task error, role assignment, object path | Do not grant global admin as quick fix | Security approval needed or broad automation fail |
| Wrong port group | VDA/Agent not registered, no DC/broker reachability | VM NIC mapped wrong | Network | Compare failed vs working VM NIC, VLAN, route | VM network config, ping/path, port group | Do not mass edit without pilot | Multiple new VMs affected |
| vCenter down | Operations fail, sessions may continue | vSphere Client inaccessible | vCenter | Check VCSA health, DNS/cert/time, services | Browser/API error, service status | Do not assume all VDI down | vCenter service outage |
| Snapshot issue | Image update fail, datastore grows | Consolidation warning, snapshot tree deep | VM/storage | Check snapshot tree, backup task, datastore | Snapshot list, task logs, capacity | Do not delete random files on datastore | Snapshot affects production pool |
| Patch regression | Issues after ESXi/vCenter update | Build change, known issue match | Lifecycle | Check release notes, affected build, pilot scope | Build before/after, known issue locator | Do not continue rollout | Repeated issue on pilot/cluster |
| HA failover insufficient | Some desktops do not restart after host failure | HA/admission/capacity warnings | HA/capacity | Check HA events, cluster capacity, admission policy | HA event, failed VM restart list | Do not declare HA success by partial restart | RTO/RPO or failover target missed |
| Missing evidence | No reliable RCA | No logs/metrics for window | Monitoring | Check alarms, events, syslog, retention | Evidence gap report | Do not invent root cause | Monitoring owner must remediate |

## Monitoring and Evidence

| Evidence type | Nguồn | Khi nào lấy | Dùng để chứng minh điều gì | Lưu ý |
|---|---|---|---|---|
| vCenter Tasks | vSphere Client | VM operation, image publish, provisioning fail | Action failed where and why | Include task ID/time/object |
| vCenter Events | vSphere Client | RCA and timeline | What happened around incident/change | Align timezone |
| Host events/logs | ESXi/vCenter/syslog | Host issue, disconnect, hardware/path issue | Host-level failure signal | Support bundle for vendor |
| Datastore metrics | vSphere/Aria/storage tool | Slow login, VM stun, provisioning fail | Capacity/latency/IOPS correlation | Need threshold from customer |
| Network config | vSphere networking view | Agent unreachable, wrong VLAN | VM/port group/uplink mapping | Compare working vs failing |
| Performance charts | vSphere/Aria | CPU/memory/storage/network performance issue | Trend and spike correlation | Save time window |
| Alarms | vSphere/monitoring | Daily operations and incident start | Early warning and severity | Avoid alert fatigue |
| RBAC evidence | vCenter permissions | Permission denied | Role/scope mismatch | Avoid showing secrets |
| Change record | ITSM/CAB | Post-change incident | What changed and who approved | Link with task/event |
| Backup/restore record | Backup platform/vCenter | Recovery validation | Backup exists and restore tested | Need customer process |

## Change, Patch and Rollback

| Change type | Risk | Blast radius | Precheck | Rollback point | Postcheck | Stop condition |
|---|---|---|---|---|---|---|
| ESXi patch/upgrade | Host reboot, driver regression, datastore/network issue | Host or cluster | Release notes, host health, capacity, active sessions | Vendor rollback path, bootbank, maintenance backout | Host connected, VDI login/launch, datastore/network clear | Pilot host fails or critical alarms |
| vCenter upgrade | API/task changes, integration failure | Operations control plane | vCenter backup, service health, Horizon/CVAD integration | VCSA backup/restore | vSphere Client, tasks, integrations | Backup missing or task errors |
| vDS/port group change | Management loss, VM unreachable | Multiple hosts/pools | Export config, pilot host, rollback path | Previous vDS config | Agent registration, network reachability | Management path unstable |
| Datastore expansion/migration | VM stun, placement error, performance issue | Datastore/pool | Capacity/latency, backup window, active sessions | Previous placement/policy | Latency stable, VM tasks success | Latency spike or task fail |
| RBAC/service account change | Automation failure or overprivilege | VDI operations | Export role/scope, test account | Previous role mapping | Test power/provision task | Permission denied |
| HA/DRS policy change | Failover/capacity imbalance | Cluster | Current HA/DRS config, capacity | Previous config | HA/DRS healthy, test scenario | HA warning/admission issue |
| Snapshot/image operation | Datastore growth, rollback failure | Pool/image | Snapshot plan, datastore capacity, pilot | Previous snapshot/image | Pilot login/launch | Snapshot task fail or datastore pressure |
| Monitoring/alert change | Missed alert or noisy alert | Operations team | Current alert route, test notification | Previous alert config | Test alert and evidence visibility | Critical alarms not routed |

## Backup, Recovery, HA and DR

### Backup Objects

| Object | Vì sao cần backup | Recovery validation |
|---|---|---|
| vCenter Server Appliance | Control plane for vSphere operations | vSphere Client login, hosts connected, datastore visible, Horizon/CVAD integration task |
| vCenter configuration and certificates | Trust and integration continuity | Certificate valid, integrations not broken |
| Master image/template | Restore image pipeline | New/pilot desktop provision and launch |
| VM configuration for critical management VMs | Recover management plane | Services start and dependencies work |
| Documentation/change evidence | Rebuild operational knowledge | Runbook usable during incident |

### HA/DR Validation Logic

HA validation phải đi qua service path, không chỉ infrastructure state. Nếu một host failure xảy ra và HA restart VM, engineer vẫn cần kiểm tra desktop pool availability, broker sees machine, Agent/VDA registered, user can launch, profile loads, application backend reachable. Nếu chỉ kiểm tra VM powered on, DR/HA validation vẫn thiếu.

### RPO/RTO

Source không nêu RPO/RTO cụ thể cho môi trường khách hàng. Giá trị này là `Need Customer Confirmation`. Training phải dạy engineer không tự bịa RPO/RTO; phải hỏi customer hoặc lấy từ SLA/DR design.

## Security and RBAC

| Role | Quyền nên có | Quyền không nên có nếu không cần | Evidence/Audit |
|---|---|---|---|
| Helpdesk | Read session/VM status, basic console view nếu được phê duyệt | Snapshot, delete VM, host/network/storage config | Ticket, view-only audit |
| System Engineer | Read vCenter, collect evidence, operate scoped VM tasks theo runbook | Global admin, certificate/private key access | Task/event, change ticket |
| Platform Admin | Host/cluster/datastore/network/HA/DRS/config changes | Không bypass change approval | Change record, vCenter events |
| Security Admin | RBAC, certificate policy, audit review | Không vận hành VM/pool nếu ngoài scope | Permission change logs |
| Customer Operator | Theo quyền customer phê duyệt | Không cấp quyền không trace được | Approval trail |

Security insight quan trọng là least privilege không có nghĩa là thiếu quyền vận hành. Nếu service account Horizon/CVAD thiếu quyền cần thiết ở folder/resource pool/datastore/network scope, automation fail. Nếu cấp global admin để “cho nhanh”, rủi ro audit và blast radius tăng. Training cần dạy engineer đọc task permission denied và kiểm tra role/scope chính xác.

## Scenario Based Extraction

| Scenario | Bối cảnh | Triệu chứng | Câu hỏi cho engineer | Phân tích mong đợi | Evidence cần lấy | Escalation |
|---|---|---|---|---|---|---|
| CH01 Patch regression | Pilot ESXi vừa update. | User trên host pilot disconnect hoặc launch chậm. | Lỗi có match known issues không? | Đối chiếu build và release notes, dừng rollout nếu lặp lại. | Build before/after, affected VM list, host events, release note locator. | Virtualization/vendor |
| CH02 Host failure | Một host not responding. | Nhiều desktop unavailable. | Affected scope theo host hay cluster? | Map VM-host, xem HA events, host logs. | Host event, HA event, support bundle. | HCI/virtualization |
| CH03 vCenter down | vSphere Client không vào được. | Existing sessions có thể chạy, operations fail. | Đây là data plane hay control plane issue? | Tách user session path khỏi operations path. | VCSA health, broker integration errors, tasks. | Platform/vCenter |
| CH04 RBAC cleanup | Security thay role service account. | Provisioning/power task fail. | Role thiếu hay scope sai? | Kiểm tra permission ở object liên quan. | Task permission denied, role mapping, change. | Security/platform |
| CH05 Image publish fail | Master image update. | Pool update fail. | Snapshot/template/datastore/network đúng chưa? | Kiểm tra source image and task chain. | Snapshot tree, task error, datastore free. | VDI platform/virtualization |
| CH06 Wrong port group | New VDI không registered. | Agent/VDA unreachable. | VM NIC mapping có sai không? | So sánh failed vs working VM port group/VLAN. | VM NIC config, port group, route. | Network/platform |
| CH07 Storage latency | Sáng cao điểm login chậm. | Logon duration tăng. | Datastore latency có spike không? | Correlate session count, datastore latency, backup window. | Latency/IOPS chart, session count, backup jobs. | Storage/capacity |
| CH08 HA capacity miss | Host failure. | Một số desktop không restart. | Admission control/spare capacity đủ không? | Xem HA events and cluster capacity. | HA event, capacity summary, failed restart list. | DR/platform |
| CH09 Evidence gap | Incident đã qua. | Không xác định được root cause. | Monitoring có đủ time window không? | Xác định missing syslog/metric/alert route. | Evidence gap report, monitoring config. | Monitoring owner |

## Training Conversion Notes

| Training asset | Nội dung lấy từ source | Topic đích |
|---|---|---|
| Concept explanation | vSphere as VDI infrastructure layer | [[topics/7_Hypervisor_and_HCI_Operations_Guide]] |
| Architecture diagram | Control plane, execution plane, storage, network, security, availability, evidence | [[topics/2_Customer_VDI_Landscape_Overview]] |
| Access flow support | VM network path, broker/agent reachability, port group/VLAN | [[topics/5_VDI_Access_Flow_Design]] |
| Daily checklist | Host, datastore, VM state, tasks/events, alarms, HA/DRS | [[topics/16_Daily_Operations_Checklist]] |
| Troubleshooting table | Host, datastore, permission, network, vCenter, snapshot, HA, monitoring gaps | [[topics/18_VDI_Troubleshooting_Playbook]] |
| Performance module | CPU/memory/storage latency/DRS/resource pools | [[topics/19_VDI_Performance_and_Capacity_Guide]] |
| Change guide | ESXi/vCenter/network/storage/RBAC/HA change controls | [[topics/20_VDI_Change_Management_Guide]] |
| Patch guide | Release notes, pilot, build evidence, rollback | [[topics/21_VDI_Patch_and_Upgrade_Guide]] |
| Backup guide | VCSA, template/image, restore validation | [[topics/22_VDI_Backup_and_Recovery_Guide]] |
| HA/DR guide | HA admission, DRS, failover validation | [[topics/23_VDI_High_Availability_and_Disaster_Recovery_Guide]] |
| RBAC guide | Role/scope/service account/audit | [[topics/24_VDI_Access_Control_and_RBAC_Guide]] |
| Escalation guide | Evidence package by layer | [[topics/25_VDI_Support_and_Escalation_Guide]] |
| Knowledge base | Repeatable symptom patterns | [[topics/26_VDI_Operational_Knowledge_Base]] |
| Glossary | ESXi, vCenter, datastore, port group, DRS, HA | [[topics/27_VDI_Glossary_and_Concept_Dictionary]] |

## Chapter Deep Insights

### CH01 - Release Notes and Lifecycle

**Core principle:** Release notes are operational risk intelligence. They are not a passive appendix. For VDI, release notes decide whether a patch should proceed, which known issues to watch, what compatibility must be checked, and how to interpret failures after change.

**Pedagogical insight:** Vendor writes release notes by product build and issue class. Training should translate that into a patch-readiness checklist: component, current build, target build, known issues, affected features, workaround, rollback, pilot criteria, stop condition.

**Industry relevance:** In enterprise VDI, patch windows are limited and blast radius is large. A known storage or networking issue in ESXi can become a VDI incident. Engineers must document release note review as change evidence.

**Misconceptions:** The common mistake is treating release notes as optional. Another mistake is reading only resolved issues and ignoring known issues. A third is not preserving before/after build numbers.

**Training outcome:** Engineer can read release notes and produce risk notes for change advisory review.

### CH02 - ESXi Install and Upgrade

**Core principle:** ESXi is the execution boundary for VM workloads. Host readiness combines hardware compatibility, system storage, firewall, logging, patch state, licensing, network/storage path and maintenance capacity.

**Pedagogical insight:** Vendor begins with requirements and setup because a bad foundation creates operational failure later. Training should present ESXi as a living operational object: health, maintenance, logs, patch, capacity and evidence.

**Industry relevance:** In VDI, one ESXi host might carry many desktops. Maintenance without checking active sessions or cluster capacity can become a user-impacting incident. Syslog and support bundles are non-negotiable for RCA.

**Misconceptions:** Engineers may assume vCenter alarm is enough and skip host-level logs. They may also patch hosts without mapping VDI workload placement. Another mistake is treating host reboot as isolated.

**Training outcome:** Engineer can prepare ESXi maintenance with precheck, impact assessment, rollback evidence and postcheck.

### CH03 - vCenter Install and Upgrade

**Core principle:** vCenter is not always in the user session path, but it is central to operations. It controls tasks, inventory, APIs, permissions and integration points.

**Pedagogical insight:** Vendor focuses on deployment, backup/restore and upgrade. Training should translate that into operational dependency: what breaks when vCenter is down, what does not immediately break, and what must be validated after restore.

**Industry relevance:** Horizon and CVAD can depend on vCenter for provisioning, image update and VM power operations. Restore that ignores VDI integration is incomplete.

**Misconceptions:** A frequent error is declaring vCenter restore successful after vSphere Client login only. Another is assuming existing VDI sessions prove vCenter is healthy.

**Training outcome:** Engineer can validate vCenter recovery from a VDI operations perspective.

### CH04 - Authentication and Lifecycle

**Core principle:** Operations are constrained by identity and state. vSphere does not only ask “what action”; it asks “who can do it, where, and under what lifecycle state.”

**Pedagogical insight:** Vendor separates authentication from lifecycle, but training should connect them: remediation or automation fails if identity, permission or object scope is wrong.

**Industry relevance:** Service accounts for Horizon/CVAD must have correct role and scope. Lifecycle remediation can affect many hosts. Both are common roots of VDI operations failure.

**Misconceptions:** Engineers often check only username and not object scope. Another mistake is treating lifecycle remediation as a routine background action rather than a change with blast radius.

**Training outcome:** Engineer can diagnose permission denied task and review remediation risk.

### CH05 - vCenter, Host and VM Administration

**Core principle:** VDI workloads are VM objects. VM power state, VMware Tools, template, snapshot, network mapping, datastore and vCenter tasks define whether a desktop can be created, updated and launched.

**Pedagogical insight:** Vendor teaches object operations. Training should teach symptom translation: launch fail maps to VM state/task/network/storage; image publish maps to template/snapshot/datastore; unregistered maps to VM network/agent.

**Industry relevance:** This is the most direct bridge from vSphere to Horizon/CVAD operations. Almost every VDI provisioning or image incident leaves evidence here.

**Misconceptions:** Snapshot-as-backup is the most dangerous. Another is ignoring vCenter task details and only looking at the VDI console error.

**Training outcome:** Engineer can inspect VM object evidence before escalation.

### CH06 - Host Profiles and Networking

**Core principle:** vSphere networking is object mapping plus physical path. VM NICs connect to port groups, port groups sit on switches, switches use uplinks, and VMkernel adapters serve management/storage/vMotion paths.

**Pedagogical insight:** Vendor describes configuration components. Training must convert this to end-to-end VDI reachability: client/broker/agent/DC/profile/app backend are separate path checks.

**Industry relevance:** Wrong port group or VLAN after provisioning is a common cause of Agent/VDA unregistered. Distributed switch change has large blast radius.

**Misconceptions:** Ping alone is not a network RCA. Another mistake is confusing VM network with VMkernel management/storage network.

**Training outcome:** Engineer can package network evidence for VDI escalation.

### CH07 - Storage

**Core principle:** Storage health is multi-dimensional: capacity, latency, IOPS, throughput, path, policy, snapshot and backend state. Capacity alone is not health.

**Pedagogical insight:** Vendor describes many storage technologies. Training should group them by operational symptom: power/provision fail, login slow, VM stun, snapshot issue, backup contention.

**Industry relevance:** VDI creates bursty workloads: boot storm, logon storm, profile load and image update. Storage issues are often misreported as desktop or broker problems.

**Misconceptions:** “Datastore has free space so storage is fine” is false. Another mistake is deleting snapshots or VM files manually during pressure.

**Training outcome:** Engineer can correlate storage metrics with VDI symptoms.

### CH08 - Security, Resource Management and Availability

**Core principle:** Availability is a combination of access control, resource sufficiency and failover policy. HA cannot compensate for bad capacity planning, wrong permissions or resource starvation.

**Pedagogical insight:** Vendor documents security, resource and availability separately. Training should connect them because VDI incidents often cross these boundaries.

**Industry relevance:** CPU/memory contention creates poor user experience. HA admission control decides failover capacity. RBAC controls automation. Certificate issues affect trust and access.

**Misconceptions:** HA enabled does not mean DR ready. Another mistake is assuming performance issue always comes from storage or broker while CPU/memory/resource pool is the root.

**Training outcome:** Engineer can review capacity, RBAC and HA as one operational risk picture.

### CH09 - Monitoring, Host Client and Aria

**Core principle:** Evidence precedes conclusion. Monitoring, alarms, tasks, events, performance charts and logs are the evidence plane of VDI operations.

**Pedagogical insight:** Vendor describes monitoring tools. Training should teach evidence discipline: define time window, affected objects, metrics, logs and change timeline.

**Industry relevance:** In enterprise support, escalation without evidence wastes time. Aria or equivalent tools can reveal trends that vSphere Client snapshots miss.

**Misconceptions:** Screenshot of an error is not RCA. Another mistake is checking metrics after the fact without retention or correct time window.

**Training outcome:** Engineer can build an evidence package that routes incident to the right owner.

## Need Customer Confirmation

| Nhóm | Câu hỏi cụ thể |
|---|---|
| Version | Production đang dùng ESXi/vCenter build nào? Có mixed-version cluster không? |
| HCI/Cluster | HCI vendor nào? Có bao nhiêu cluster/host? Cluster nào chạy Horizon, cluster nào chạy CVAD? |
| vCenter topology | Có một hay nhiều vCenter? Có Enhanced Linked Mode không? |
| Identity/RBAC | Horizon/CVAD service accounts có role gì và scope ở đâu? Ai approve thay đổi quyền? |
| Storage | Datastore type là VMFS, NFS, vSAN hay VVols? Threshold latency/capacity là gì? |
| Network | Port group/VLAN mapping cho VDI, management, storage, vMotion, profile/app path như thế nào? |
| Monitoring | Có dùng VMware Aria Operations không? Syslog target ở đâu? Retention bao lâu? |
| Change | ESXi/vCenter patch process, pilot criteria, stop condition, rollback owner là ai? |
| Backup | VCSA backup schedule/location/restore test gần nhất? Master image/template backup thế nào? |
| HA/DR | HA admission policy, DRS mode, RPO/RTO, DR drill frequency là gì? |
| Support | Escalation path giữa VDI, virtualization, storage, network, security và vendor ra sao? |

## Related Sources

- [[sources/vmware-vsphere-8-0]]
- [[sources/vmware-vsphere-8-0-part-01-release-and-lifecycle]]
- [[sources/vmware-vsphere-8-0-part-02-esxi-install-upgrade]]
- [[sources/vmware-vsphere-8-0-part-03-vcenter-install-upgrade]]
- [[sources/vmware-vsphere-8-0-part-04-authentication-lifecycle]]
- [[sources/vmware-vsphere-8-0-part-05-vcenter-host-vm-admin]]
- [[sources/vmware-vsphere-8-0-part-06-host-profiles-networking]]
- [[sources/vmware-vsphere-8-0-part-07-storage]]
- [[sources/vmware-vsphere-8-0-part-08-security-resource-availability]]
- [[sources/vmware-vsphere-8-0-part-09-monitoring-host-client-aria]]
- [[sources/horizon-8-architecture]]
- [[sources/citrix-virtual-apps-and-desktops-7-2603]]
- [[sources/vcenter-server-installation-and-setup]]

## Related Concepts

- [[concepts/vmware-vsphere]]
- [[concepts/esxi]]
- [[concepts/vcenter-server]]
- [[concepts/vcenter-server-appliance]]
- [[concepts/datastore]]
- [[concepts/snapshot]]
- [[concepts/virtual-machine]]
- [[concepts/virtual-networking]]
- [[concepts/high-availability]]
- [[concepts/backup-and-recovery]]
- [[concepts/capacity-management]]
- [[concepts/lifecycle-management]]
- [[concepts/monitoring-and-logs]]
- [[concepts/identity-and-access-management]]

## Chapter Ingest Report

- Source: `raw/sources/vmware-vsphere-8-0.txt`
- Total chapters detected: 10 including front matter/TOC
- Chapters extracted: 10
- Chapters out of scope: 0
- Chapters meeting 50,000 character minimum: 1 consolidated report
- Chapters with Depth Exception: 9 shard pages remain below 50,000 characters and should be expanded one by one if strict per-shard compliance is required
- Source overview page: [[sources/vmware-vsphere-8-0]]
- Shard pages created: 9
- Deep report created: [[sources/vmware-vsphere-8-0-technical-deep-ingest-report]]
- Concepts created: 0 in this step
- Concepts updated: existing concept references were updated in prior vSphere ingest step
- Topics mapped: 7, 8, 9, 11, 12, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27
- Broken links: None at creation time after link check
- wiki/log.md touched: No

## Length Compliance

| Chapter / Report | Actual estimated length | Meets 50,000 chars | Depth Exception / Action |
|---|---:|---|---|
| Consolidated technical deep ingest report | 53,933 characters measured after final edit | Yes | Primary report for `lumi-ask` deep retrieval |
| CH01 release/lifecycle shard | Below 50,000 | No | Expand in next pass if strict per-chapter 50k is required |
| CH02 ESXi install/upgrade shard | Below 50,000 | No | Expand in next pass if strict per-chapter 50k is required |
| CH03 vCenter install/upgrade shard | Below 50,000 | No | Expand in next pass if strict per-chapter 50k is required |
| CH04 authentication/lifecycle shard | Below 50,000 | No | Expand in next pass if strict per-chapter 50k is required |
| CH05 vCenter/host/VM admin shard | Below 50,000 | No | Expand in next pass if strict per-chapter 50k is required |
| CH06 networking shard | Below 50,000 | No | Expand in next pass if strict per-chapter 50k is required |
| CH07 storage shard | Below 50,000 | No | Expand in next pass if strict per-chapter 50k is required |
| CH08 security/resource/availability shard | Below 50,000 | No | Expand in next pass if strict per-chapter 50k is required |
| CH09 monitoring/Host Client/Aria shard | Below 50,000 | No | Expand in next pass if strict per-chapter 50k is required |

## Full Report Self Review

- [x] Source Inventory included.
- [x] Coverage Ledger included.
- [x] Technical Executive Summary included.
- [x] In-depth Technical Insights included.
- [x] Role in the Learning Pathway included.
- [x] Points of Caution and Potential Misconceptions included.
- [x] Key Terminology and Formulas included.
- [x] Knowledge Atoms included.
- [x] Architecture Knowledge included.
- [x] Operational Knowledge included.
- [x] Troubleshooting Knowledge included.
- [x] Monitoring and Evidence included.
- [x] Change, Patch and Rollback included.
- [x] Backup, Recovery, HA and DR included.
- [x] Security and RBAC included.
- [x] Scenario Based Extraction included.
- [x] Training Conversion Notes included.
- [x] Need Customer Confirmation included.
- [x] Length Compliance included.
- [x] No customer-specific facts fabricated.
- [x] No secrets or credentials requested.
- [x] `wiki/log.md` not touched.
