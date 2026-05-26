---
id: source-vcenter-server-installation-and-setup
title: vCenter Server Installation and Setup
type: source
created: 2026-05-22
updated: 2026-05-26
authors:
  - VMware
year: 2026
importance: 4
urls: []
raw_paths:
  - raw/sources/vsphere-vcenter-802-installation-guide.txt
provenance: replayable
confidence: high
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

Tài liệu vCenter Server Installation and Setup cung cấp kiến thức về triển khai vCenter Server Appliance, yêu cầu DNS/storage/hardware, Enhanced Linked Mode, file-based backup/restore, image-based restore, thao tác sau triển khai và thu thập log khi lỗi installation/upgrade. Trong bối cảnh VDI, vCenter là dependency quan trọng của Horizon và có thể là hypervisor connection cho CVAD; vì vậy backup, restore, certificate/DNS/time và availability của vCenter ảnh hưởng trực tiếp đến provisioning, power operation, pool/catalog update và vận hành host/datastore.

## Source Metadata

| Trường | Giá trị |
|---|---|
| Source file | `raw/sources/vsphere-vcenter-802-installation-guide.txt` |
| Source type | Vendor installation and setup guide |
| Platform | VMware vCenter Server Appliance |
| Version covered | vCenter/vSphere 8.0.2 theo tên file |
| Primary training use | vCenter dependency, deployment prerequisites, backup/restore, troubleshooting logs |
| Confidence | High for vCenter setup knowledge; Unknown for customer vCenter design |

## Key Claims

- vCenter Server Appliance là VM được tối ưu để chạy vCenter và các thành phần quản trị đi kèm.
- Deploy vCenter cần chuẩn bị DNS, hardware/storage requirement, installer, deployment method và worksheet thông tin trước khi chạy.
- File-based backup/restore là nội dung trọng tâm cho recovery vCenter; restore gồm giai đoạn deploy appliance mới và transfer data.
- Enhanced Linked Mode có thể liên kết nhiều vCenter trong cùng miền quản trị, nhưng cần xác nhận nếu khách hàng dùng.
- Khi troubleshoot install/upgrade, cần lấy installation logs, deployment log files và support bundle.

## Evidence From Source

- Source có các mục: What is vCenter Server Appliance, vCenter Enhanced Linked Mode, system/storage/DNS requirements, prerequisites, GUI/CLI deployment, file-based backup and restore, image-based backup and restore, after deployment, troubleshooting logs.
- Source mô tả workflow cài đặt vSphere: install ESXi, deploy vCenter Server Appliance, connect to vCenter using vSphere Client.
- Source nêu vCenter appliance bao gồm vCenter Server, vSphere Client, authentication services, VMware Certificate Authority và các dịch vụ liên quan.

## Key Architecture Knowledge

### vCenter Server Appliance

vCenter Server Appliance là VM trung tâm quản trị ESXi/cluster/VM/datastore/network. Trong VDI, vCenter không nhất thiết nằm trong data path của user session, nhưng nằm trong control/operation path của pool, image, provisioning, power operation và host maintenance.

### DNS và time dependency

vCenter deployment và vận hành phụ thuộc DNS đúng, name resolution ổn định và time sync. Trong VDI, DNS/time issue có thể kéo theo lỗi authentication, certificate, API, Horizon/CVAD integration hoặc task failure.

### Backup/restore

File-based backup/restore là năng lực cần có cho vCenter Appliance. Với VDI, restore vCenter phải validate không chỉ đăng nhập vSphere Client mà còn các integration: Horizon/Citrix service account, inventory, tasks, host connectivity, datastore và image/pool/catalog operation.

### Enhanced Linked Mode

Nếu có nhiều vCenter, Enhanced Linked Mode ảnh hưởng phạm vi quản trị, certificate/SSO và recovery planning. Nếu khách hàng không dùng, không đưa vào tài liệu vận hành như giả định.

## Operational Knowledge

| Khu vực | Engineer cần kiểm tra | Evidence cần lưu |
|---|---|---|
| vCenter reachability | FQDN, DNS, HTTPS/vSphere Client, service health | URL/FQDN, timestamp, service status |
| Appliance resources | CPU, memory, disk/storage, backup health | Appliance health screenshot, datastore capacity |
| Backup | Schedule, last successful backup, backup location | Backup job status, restore test record |
| Certificates/SSO | Certificate validity, SSO domain, authentication | Certificate chain, login result |
| Integration | Horizon/CVAD connection, service account role | Integration status, vCenter task result |
| Troubleshooting logs | Installation/upgrade logs, support bundle | Bundle name/time, log excerpt summary |

## Troubleshooting Knowledge

| Triệu chứng | Nguyên nhân có thể | Lớp cần kiểm tra | Evidence | Hướng xử lý | Escalation |
|---|---|---|---|---|---|
| Horizon/CVAD không power/provision VM | vCenter API unavailable, service account, inventory/datastore issue | vCenter, RBAC, Datastore | vCenter task error, integration log | Kiểm tra vCenter service, role, datastore, object path | Escalate virtualization admin |
| Không truy cập được vSphere Client | vCenter service, DNS/cert, appliance resource | vCenter, DNS, Certificate | Browser error, DNS result, service health | Kiểm tra FQDN, certificate, appliance health | Escalate platform nếu vCenter service down |
| Restore vCenter chưa hoàn tất chức năng | Restore thiếu validation integration | Recovery, Integration | Restore record, Horizon/Citrix task test | Test host inventory, datastore, service account, VDI operation | Escalate DR owner nếu RTO/RPO không đạt |
| Backup vCenter fail | Backup target, credential, network, appliance issue | Backup, Network, Storage | Backup job error, appliance log | Kiểm tra target reachability và capacity | Escalate backup/storage owner |
| Deployment/upgrade fail | Thiếu prerequisite, DNS, storage, installer issue | Install/Upgrade | Deployment logs, support bundle | Thu thập log theo source, sửa prerequisite | Escalate VMware/platform nếu lỗi không rõ |

## Monitoring and Evidence

Theo dõi:

- vCenter service health.
- Appliance CPU/memory/disk.
- Backup success/failure.
- Certificate expiry.
- vCenter task failure trend.
- Host connectivity state.
- Integration error từ Horizon/CVAD nếu có.

Evidence:

- vCenter appliance health screenshot.
- Last backup status.
- vSphere Client task/event.
- Support bundle hoặc deployment log khi install/upgrade.
- Integration test result sau restore/change.

## Change, Patch and Rollback Notes

Change cần kiểm soát:

- Deploy/upgrade/patch vCenter Appliance.
- Certificate replacement.
- DNS/FQDN/IP change.
- Backup schedule/location change.
- SSO/Enhanced Linked Mode change.
- Service account permission change cho Horizon/CVAD.

Precheck:

- Confirm backup thành công trước change.
- Export/ghi nhận cấu hình quan trọng.
- Kiểm tra DNS, NTP/time, certificate.
- Thông báo các đội phụ thuộc Horizon/Citrix.

Rollback:

- Restore từ file-based backup hoặc phương án image-based được phê duyệt.
- Revert certificate/DNS/permission nếu change nhỏ.
- Không tự restore vCenter production nếu chưa có approval DR/change.

## Backup, Recovery, HA and DR Notes

- vCenter file-based backup phải có lịch, nơi lưu và restore test.
- Recovery vCenter cần validate: đăng nhập, inventory, host connected, datastore visible, task execution, Horizon/CVAD integration.
- Nếu có Enhanced Linked Mode, restore/certificate/SSO phức tạp hơn và cần runbook riêng.

## Security and RBAC Notes

- vCenter administrator quyền cao, chỉ platform admin được dùng.
- Service account cho VDI platform cần least privilege theo vendor requirement.
- Backup target và support bundle có thể chứa thông tin nhạy cảm; lưu trữ theo policy khách hàng.
- Không ghi secret hoặc private key vào wiki.

## Concepts to Create or Update

| Concept | Vì sao quan trọng | Source support |
|---|---|---|
| [[concepts/vcenter-server-appliance]] | VM quản trị vCenter | Source trực tiếp |
| [[concepts/vcenter-server]] | Control plane virtualization | Source trực tiếp |
| [[concepts/enhanced-linked-mode]] | Multi-vCenter/SSO nếu có | Source có mục riêng |
| [[concepts/backup-and-recovery]] | File-based restore vCenter | Source có chapter backup/restore |
| [[concepts/certificate-management]] | vCenter cert/SSO | Appliance components |
| [[concepts/dns-and-time-sync]] | Prerequisite quan trọng | DNS requirements |

## Related Topic Mapping

| Topic document | Cách source này hỗ trợ |
|---|---|
| [[topics/7_Hypervisor_and_HCI_Operations_Guide]] | vCenter role và operations dependency |
| [[topics/11_VDI_Provisioning_and_Allocation_Guide]] | vCenter API/inventory cho provisioning |
| [[topics/20_VDI_Change_Management_Guide]] | vCenter/cert/permission changes |
| [[topics/21_VDI_Patch_and_Upgrade_Guide]] | vCenter upgrade/precheck |
| [[topics/22_VDI_Backup_and_Recovery_Guide]] | File-based backup/restore vCenter |
| [[topics/23_VDI_High_Availability_and_Disaster_Recovery_Guide]] | vCenter recovery validation |
| [[topics/24_VDI_Access_Control_and_RBAC_Guide]] | vCenter admin/service account roles |
| [[topics/27_VDI_Glossary_and_Concept_Dictionary]] | vCenter, VCSA, ELM |

## Need Customer Confirmation

- vCenter version/build và deployment topology?
- vCenter backup method, schedule, location và restore test gần nhất?
- Có Enhanced Linked Mode không?
- Horizon/CVAD đang dùng service account nào và role gì trên vCenter?
- Certificate management process và expiry monitoring?
- DR/RTO/RPO cho vCenter?

## Related Sources

- [[sources/vcenter-server-installation-and-setup-chapter-runbook-ingest]]
- [[sources/vmware-vsphere-8-0]]
- [[sources/horizon-8-architecture]]
- [[sources/citrix-virtual-apps-and-desktops-7-2603]]
- [[sources/vdi-training-idea]]

## People

Không nêu cá nhân tác giả trong phần nguồn đã nạp.

## Open Questions

- Cần bổ sung runbook backup/restore thật của khách hàng để operationalize phần này.
- Cần xác nhận backup target có encryption/access control như thế nào.
