---
id: source-vdi-training-idea
title: VDI Training Idea
type: source
created: 2026-05-22
updated: 2026-05-26
authors:
  - User
year: 2026
importance: 5
urls: []
raw_paths:
  - raw/sources/training_idea.md
provenance: replayable
confidence: high
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

`training_idea.md` là nguồn điều khiển bối cảnh quan trọng nhất của project. Nó mô tả mục tiêu xây dựng bộ tài liệu nghiên cứu/onboarding cho system engineer chuẩn bị vận hành hai hệ thống VDI quy mô lớn: Omnissa Horizon trên HCI và Citrix CVAD trên XenServer hoặc VMware ESXi, mỗi hệ thống khoảng 1500 đến hơn 2000 VDI. Source này định hình cách nhìn hệ thống theo lớp, phạm vi vận hành cần bao quát, lỗi thường gặp, hướng xử lý và các nhóm thông tin cần xác nhận thêm với khách hàng.

Đây không phải vendor manual. Đây là training design brief và customer-context source. Mọi topic trong `wiki/topics` phải dùng source này để giữ đúng bối cảnh, không biến tài liệu thành mô tả sản phẩm chung.

## Source Metadata

| Trường | Giá trị |
|---|---|
| Source file | `raw/sources/training_idea.md` |
| Source type | User-provided training idea / customer context brief |
| Platform | Omnissa Horizon, Citrix CVAD, HCI, ESXi, XenServer, AD, Storage, Network, Monitoring |
| Version covered | Customer-specific version Unknown |
| Primary training use | Scope, architecture lens, operational emphasis, gaps, customer context |
| Confidence | High for intended scope; Unknown for production facts not provided |

## Key Claims

- Khách hàng có hai hệ thống VDI khác nhau: Omnissa Horizon trên HCI và Citrix CVAD trên XenServer hoặc VMware ESXi.
- Quy mô mỗi hệ thống khoảng 1500-2000+ VDI nên engineer phải nhìn như một platform nhiều lớp, không chỉ nhìn từng VM.
- Tài liệu phải phục vụ vận hành thực tế: biết kiểm tra thành phần nào, lỗi thường nằm ở lớp nào, evidence nào cần lưu và khi nào escalation.
- Các lớp cần bao quát gồm user access, gateway, broker/control plane, session, identity, hypervisor/HCI, storage, network, policy, monitoring, incident, change, backup/HA/DR, RBAC và support.
- Không được bịa thông tin nội bộ khách hàng; version, topology, IP, hostname, tool, SLA, owner, HA/DR, access flow, profile solution đều cần xác nhận nếu chưa có.

## Evidence From Source

- Source nêu rõ mục tiêu tài liệu cho system engineer có mức kinh nghiệm khác nhau, gồm cả người mới với ảo hóa, Citrix, Horizon, network, storage.
- Source mô tả mô hình Horizon on HCI: Horizon Client, UAG, Connection Server, Horizon Agent, AD, vCenter/ESXi/HCI, storage/network.
- Source mô tả mô hình CVAD: Workspace App, StoreFront, Citrix Gateway, Delivery Controller, Site Database, VDA, Studio, Director, License Server, hypervisor.
- Source liệt kê các mảng kiến thức cần bao quát: identity, hypervisor/HCI, storage, network, policy/security, provisioning, image, monitoring, incident, change, backup/DR.
- Source nhấn mạnh cách xử lý lỗi theo lớp và không viết kiểu marketing.

## Key Architecture Knowledge

Mô hình đào tạo được source định nghĩa theo lớp:

1. User Access Layer: laptop, thin client, browser, Citrix Workspace App, Horizon Client.
2. Gateway Layer: Citrix Gateway hoặc Unified Access Gateway nếu có external access.
3. Portal/Broker Layer: StoreFront/Delivery Controller cho CVAD; Connection Server cho Horizon.
4. Desktop/Application Session Layer: VDI machine, VDA, Horizon Agent.
5. Identity Layer: AD, Domain Controller, DNS, Group Policy, Hybrid Microsoft Entra ID nếu có.
6. Hypervisor/HCI Layer: HCI, ESXi, vCenter, XenServer.
7. Storage Layer: datastore, profile storage, image storage, snapshot, backup.
8. Network Layer: VLAN, routing, firewall, LB, DNS, certificate, NAT, latency, bandwidth.
9. Governance/Operation Layer: policy, entitlement, monitoring, alert, incident, change, capacity, patching, image lifecycle.

## Operational Knowledge

| Mảng vận hành | Trọng tâm theo source | Cách dùng trong topic |
|---|---|---|
| Identity | DC, AD, DNS, GPO, group, computer account, Hybrid Entra ID nếu có | Topic 6, 10, 18 |
| Horizon | Connection Server, UAG, Agent, pool, entitlement, vCenter/HCI | Topic 3, 5, 14 |
| CVAD | StoreFront, Gateway, Delivery Controller, VDA, catalog/group, database | Topic 4, 5, 13 |
| Hypervisor/HCI | Host, cluster, datastore, snapshot, resource, VM lifecycle | Topic 7, 19, 20 |
| Storage | Capacity, latency, IOPS, profile/image storage, boot/logon storm | Topic 8, 19, 22 |
| Network | DNS, firewall, LB, certificate, routing, latency/loss | Topic 9, 18 |
| Monitoring | Session, VDI registration, broker/gateway/host/storage/network/profile | Topic 15, 16 |
| Incident | Phân loại theo phạm vi ảnh hưởng và lớp lỗi | Topic 17, 18, 25 |
| Change | Image, policy, entitlement, certificate, patch, host maintenance | Topic 20, 21 |

## Troubleshooting Knowledge

Source định hướng chẩn đoán theo lớp, không khẳng định nguyên nhân khi chưa có evidence:

| Triệu chứng | Lớp cần nghĩ tới | Evidence cần thu |
|---|---|---|
| Login fail | Identity, Gateway, Broker, DNS/cert | User/time/error, auth log, broker/gateway log |
| Không thấy desktop/app | Entitlement, AD group, Delivery Group/Pool | Assignment, AD group, resource visibility |
| Launch fail | Broker, VDA/Agent, network, hypervisor | Session error, VDA/Agent state, VM state |
| VDA/Horizon Agent unreachable | Agent, network, hypervisor, DNS/DC | Agent log, service state, route/DNS test |
| Login chậm | Profile, storage, GPO, network, host | Login duration, profile log, storage latency |
| Black screen/disconnect | Protocol, graphics, network, host resource | Client log, protocol metrics, host metrics |
| Profile issue | FSLogix/Profile solution, storage permission, capacity | Profile log, share ACL, VHD state |

## Monitoring and Evidence

Các chỉ số source yêu cầu đưa vào bộ đào tạo:

- Session count, failed session.
- VDI registered/unregistered.
- CPU, memory.
- Storage latency, datastore capacity, IOPS.
- Network latency, packet loss.
- Login duration, profile loading time.
- Broker service health.
- Gateway health.
- License status.
- Alert trend.

Evidence cần hướng dẫn engineer lưu:

- Timestamp, user, endpoint, VDI/session, platform.
- Screenshot lỗi và trạng thái console.
- Log broker/gateway/agent/hypervisor/storage/network liên quan.
- Metrics trước/trong/sau incident.
- Change record gần nhất.

## Change, Patch and Rollback Notes

Source yêu cầu mọi change VDI có:

- Precheck.
- Impact assessment.
- Maintenance window/communication.
- Rollback point.
- Postcheck.
- Evidence.

Các change trọng yếu:

- Master image update.
- Policy change.
- Entitlement change.
- Certificate/Gateway change.
- Broker patching.
- Host maintenance.
- Storage expansion.

## Backup, Recovery, HA and DR Notes

Source yêu cầu tài liệu phải bao quát:

- Configuration backup.
- Site database / monitoring database nếu có.
- Master image.
- Profile data.
- vCenter/gateway configuration.
- HA cho broker/gateway/database/storage/hypervisor/identity/profile.
- DR drill, RPO/RTO và validation.

## Security and RBAC Notes

Source yêu cầu phân biệt:

- System engineer.
- Helpdesk.
- Platform admin.
- Security admin/customer operator nếu có.
- Least privilege, audit log, approval cho thao tác rủi ro.

Không yêu cầu hoặc lưu secret, password, token, credential.

## Concepts to Create or Update

| Concept | Vì sao quan trọng | Source support |
|---|---|---|
| [[concepts/vdi-documentation-architecture]] | Khung lớp cho toàn bộ bộ tài liệu | Source trực tiếp |
| [[concepts/vdi-operational-readiness]] | Mục tiêu readiness trước khi vào khách hàng | Source trực tiếp |
| [[concepts/vdi-training-program]] | Thiết kế đào tạo theo topic | Source trực tiếp |
| [[concepts/vdi-connection-flow]] | Luồng truy cập là lõi troubleshooting | Source trực tiếp |
| [[concepts/incident-management]] | Phân loại và xử lý sự cố | Source trực tiếp |
| [[concepts/change-management]] | Kiểm soát thay đổi | Source trực tiếp |
| [[concepts/backup-and-recovery]] | Recovery/DR là phần bắt buộc | Source trực tiếp |
| [[concepts/identity-and-access-management]] | Identity là dependency nền | Source trực tiếp |

## Related Topic Mapping

| Topic document | Cách source này hỗ trợ |
|---|---|
| [[topics/1_VDI_Foundation_Overview]] | Định nghĩa VDI và lớp nền |
| [[topics/2_Customer_VDI_Landscape_Overview]] | Bối cảnh hai hệ thống khách hàng |
| [[topics/3_Omnissa_Horizon_Architecture_Overview]] | Horizon on HCI context |
| [[topics/4_Citrix_CVAD_Architecture_Overview]] | CVAD context |
| [[topics/5_VDI_Access_Flow_Design]] | Internal/external access flow |
| [[topics/6_Identity_and_Domain_Integration_Guide]] | AD/DC/DNS/GPO/Entra |
| [[topics/7_Hypervisor_and_HCI_Operations_Guide]] | ESXi/vCenter/XenServer/HCI |
| [[topics/8_Storage_Operations_for_VDI]] | Datastore/profile/image/storage storm |
| [[topics/9_Network_Operations_for_VDI]] | VLAN/firewall/LB/DNS/cert |
| [[topics/15_VDI_Monitoring_and_Alerting_Guide]] | Monitoring metrics |
| [[topics/17_VDI_Incident_Classification_Guide]] | Incident classification |
| [[topics/18_VDI_Troubleshooting_Playbook]] | Layered troubleshooting |
| [[topics/20_VDI_Change_Management_Guide]] | Change lifecycle |
| [[topics/28_VDI_Engineer_Onboarding_Guide]] | Learning path cho engineer |

## Need Customer Confirmation

- Version chính xác của Horizon, CVAD, vSphere, XenServer, FSLogix/profile solution.
- Sơ đồ topology, network zones, DMZ, LB, gateway, broker, database.
- Access flow nội bộ/bên ngoài thực tế.
- Monitoring tool, alert threshold và dashboard.
- HA/DR design, RPO/RTO, DR drill history.
- Storage design, profile path, image repository, backup tool.
- SLA, priority matrix, escalation path và ownership.
- Change process, CAB/approval, maintenance window.

## Related Sources

- [[sources/vdi-documentation-list-context]]
- [[sources/main-prompt]]
- [[sources/horizon-8-architecture]]
- [[sources/citrix-virtual-apps-and-desktops-7-2603]]
- [[sources/vmware-vsphere-8-0]]
- [[sources/xenserver-8-4]]
- [[sources/fslogix-documentation]]

## People

Nguồn do người dùng cung cấp; không nêu cá nhân tác giả ngoài project owner/user.

## Open Questions

- Source là định hướng đào tạo, không phải tài liệu thiết kế chi tiết. Cần workshop với khách hàng để xác nhận các gaps trước khi chuyển sang runbook production.
