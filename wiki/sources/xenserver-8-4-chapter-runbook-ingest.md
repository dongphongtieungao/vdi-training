---
id: source-xenserver-8-4-chapter-runbook-ingest
title: XenServer 8.4 - Chapter Insight and Tutorial Runbook Ingest
type: source
created: 2026-05-26
updated: 2026-05-26
authors:
  - XenServer
year: 2026
importance: 5
urls: []
raw_paths:
  - raw/sources/xenserver-8.4.txt
provenance: replayable
confidence: high
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

Trang này là lớp ingest theo `chapter-ingest-loop.prompt` cho source XenServer 8.4. Mục tiêu là chuyển các chương lớn của vendor guide thành báo cáo insight tri thức và runbook thực hành cho system engineer vận hành hypervisor backend của VDI/CVAD. Trang này bổ sung cho [[sources/xenserver-8-4]]; trọng tâm ở đây là install, update, pool, networking, storage repository, VM lifecycle, HA/DR, backup, snapshot, RBAC, monitoring và troubleshooting.

## Source Inventory

| Trường | Giá trị |
|---|---|
| Raw file | `raw/sources/xenserver-8.4.txt` |
| File size | 2,394,858 bytes |
| Source type | Vendor platform documentation / administration guide |
| Product/platform | XenServer |
| Version | 8.4 |
| Ingest mode | Chapter/major-section insight loop with tutorial runbooks |
| Primary VDI use | Hypervisor/HCI, storage, network, lifecycle, backup/DR, troubleshooting, RBAC |

## Chapter Knowledge Insight Report

XenServer 8.4 phải được đọc như operational substrate của VDI, không chỉ như hypervisor có màn hình quản trị. Với CVAD, lỗi ở pool, host, SR, network, VM Tools, update level hoặc HA có thể biểu hiện thành VDA unregistered, desktop không power on, session disconnect, image update fail hoặc catalog provisioning fail. Báo cáo này chuyển các heading của source thành mô hình vận hành: control plane của pool, data path của storage/network, lifecycle của update/VM Tools, recovery path của HA/DR và evidence path của troubleshooting.

## Central Knowledge Thesis

**Thesis:** Trong môi trường VDI, XenServer không nên được hiểu là nơi "chạy VM" đơn giản, mà là lớp hạ tầng quyết định machine availability, storage integrity, network reachability và recovery behavior của desktop/application workloads. Khi update, storage, networking, pool membership hoặc HA thay đổi, tác động có thể lan lên Citrix Machine Catalog, Delivery Group và user session. Vì vậy engineer cần kiểm tra pool/host/SR/network/VM state, thu evidence trước/sau change, và validate bằng user journey CVAD thay vì chỉ nhìn task XenCenter báo thành công.

## Insight and Depth Control

| Trường | Giá trị |
|---|---|
| Depth target | Complete required insight and technical extraction sections |
| Character target | No fixed minimum |
| Required insight sections completed | Yes |
| Required technical sections completed | Yes |
| Chapter report thesis present | Yes |
| Insight report reads independently | Yes |
| Runbook best practices extracted | Yes |
| Runbooks are actionable | Yes |
| Source-backed vs inference separated | Yes |
| Depth Exception | None for major operational sections; detailed command syntax remains vendor-reference / Need Customer Confirmation |

## Table of Contents Extracted

| Chapter | Title | Source locator | Priority |
|---|---|---|---|
| CH01 | Release model, licensing, XenCenter and updates | TOC lines 17-67; headings around source lines 338-505 | High |
| CH02 | Install and other installation scenarios | TOC page 230 and 239 | High |
| CH03 | Resource pools, GFS2 clustered pools and clustered pool troubleshooting | TOC pages 377-385 | High |
| CH04 | RBAC roles and permissions, RBAC CLI | TOC pages 402-416 | Medium |
| CH05 | Manage networking and troubleshoot networking | TOC pages 440-462 | High |
| CH06 | Create storage repository and SR families | TOC page 473; NFS/SMB/GFS2/XFS related signals | High |
| CH07 | XenServer VM Tools, VM lifecycle, import/export, migration, placement | TOC pages 616-674 | High |
| CH08 | High availability | TOC page 707 | High |
| CH09 | Disaster recovery, backup, host/VM restore, snapshots, third-party backup | TOC pages 720-743 | High |
| CH10 | Alerts, health checks and advanced troubleshooting | TOC page 1011 plus alert/health check signals | High |

## Chapter Map

| Chapter ID | Title | Main keywords | Related VDI topics | Status | Notes |
|---|---|---|---|---|---|
| CH01 | Release/update/licensing operations | frequent updates, XenCenter, xe CLI, LAS, update channel | Patch, change, lifecycle | Extracted | Runbooks RB01-RB06 |
| CH02 | Install and baseline readiness | install, hardware, XenCenter, certificate verification | Hypervisor foundation | Extracted | Runbooks RB07-RB10 |
| CH03 | Pool and clustered pool operations | resource pool, coordinator, GFS2, clustering | HA, capacity, VDI placement | Extracted | Runbooks RB11-RB16 |
| CH04 | RBAC | roles, CLI, least privilege | Security/RBAC | Extracted | Runbooks RB17-RB20 |
| CH05 | Networking | PIF, VIF, bond, VLAN, management network | Network operations | Extracted | Runbooks RB21-RB28 |
| CH06 | Storage repository | SR, NFS, SMB, GFS2, XFS, capacity, CBT | Storage, backup | Extracted | Runbooks RB29-RB36 |
| CH07 | VM lifecycle and VM Tools | Windows/Linux tools, import/export, migration, placement | Provisioning, image | Extracted | Runbooks RB37-RB45 |
| CH08 | High availability | HA, failover, heartbeat, capacity | HA/DR | Extracted | Runbooks RB46-RB50 |
| CH09 | DR, backup, restore and snapshots | backup, restore, snapshots, third-party backup | Recovery | Extracted | Runbooks RB51-RB58 |
| CH10 | Alerts and troubleshooting | XenCenter alerts, health check, logs, advanced troubleshooting | Incident, support | Extracted | Runbooks RB59-RB66 |

## Runbook Best Practices Extracted

### Runbook Source Coverage

| Source subsection / heading | Operational content found | Runbook mapping | Coverage status | Nếu chưa tạo runbook, lý do |
|---|---|---|---|---|
| Early Access / Normal channel updates | Update stream and risk selection | RB01 | Covered | N/A |
| Apply updates by using XenCenter | GUI update operation | RB02 | Covered | N/A |
| Apply updates by using the xe CLI | CLI update operation | RB03 | Covered | N/A |
| XenCenter version requirement | Admin console compatibility | RB04 | Covered | N/A |
| License Activation Service / licensing | Activation model and grace risk | RB05 | Covered | N/A |
| Install / other installation scenarios | Host install and baseline readiness | RB07-RB10 | Covered | N/A |
| Resource pools | Pool membership, coordinator, host consistency | RB11-RB13 | Covered | N/A |
| GFS2 clustered pools | Clustered storage/pool behavior | RB14-RB16 | Covered | N/A |
| RBAC roles and permissions / CLI | Role assignment and least privilege | RB17-RB20 | Covered | N/A |
| Manage networking / troubleshoot networking | PIF, VIF, bond, VLAN, management network | RB21-RB28 | Covered | N/A |
| Create storage repository / NFS / SMB / GFS2 / XFS | SR creation, storage backend, capacity | RB29-RB36 | Covered | N/A |
| XenServer VM Tools for Windows/Linux | Drivers, management agent, update | RB37-RB39 | Covered | N/A |
| Import/export VMs / migration from VMware | Import, export, vDisk migration | RB40-RB42 | Covered | N/A |
| VM placement / anti-affinity | Placement groups and host spread | RB43-RB45 | Covered | N/A |
| High availability | HA enablement, failover validation | RB46-RB50 | Covered | N/A |
| Disaster recovery and backup | DR planning and restore validation | RB51-RB53 | Covered | N/A |
| Back up and restore hosts and VMs | Host/VM backup and restore | RB54-RB55 | Covered | N/A |
| VM snapshots | Snapshot use, rollback, storage risk | RB56-RB57 | Covered | N/A |
| Third-party backup solutions / CBT | Backup tool integration | RB58 | Covered | N/A |
| Alerts / health check / advanced troubleshooting | Evidence, logs, escalation | RB59-RB66 | Covered | N/A |

### Mandatory Installation and Configuration Runbooks

| Source procedure / config heading | Procedure type | Runbook required? | Runbook ID | Nếu không tạo, lý do |
|---|---|---|---|---|
| Install | Install | Yes | RB07 | N/A |
| Other installation scenarios | Install / Prepare | Yes | RB08 | N/A |
| Certificate verification after upgrade/fresh install | Configure / Security | Yes | RB09 | N/A |
| Apply updates by using XenCenter | Upgrade / Patch | Yes | RB02 | N/A |
| Apply updates by using xe CLI | Upgrade / Patch | Yes | RB03 | N/A |
| Configure update channel / remote pool synchronization | Configure | Yes | RB01, RB06 | N/A |
| Register/use License Activation Service | Configure / License | Yes | RB05 | N/A |
| Create/join/manage resource pool | Configure | Yes | RB11-RB13 | N/A |
| GFS2 clustered pools | Configure / Troubleshoot | Yes | RB14-RB16 | N/A |
| RBAC roles and permissions | Configure / Security | Yes | RB17-RB20 | N/A |
| Manage networking | Configure / Network | Yes | RB21-RB26 | N/A |
| Create storage repository | Configure / Storage | Yes | RB29-RB33 | N/A |
| Install/update XenServer VM Tools | Install / Upgrade | Yes | RB37-RB39 | N/A |
| Import/export VMs | Migrate / Backup | Yes | RB40-RB42 | N/A |
| VM placement | Configure / Availability | Yes | RB43-RB45 | N/A |
| High availability | Enable / Configure / Validate | Yes | RB46-RB50 | N/A |
| Disaster recovery and backup | Backup / Restore | Yes | RB51-RB58 | N/A |
| Advanced troubleshooting | Evidence / Escalation | Yes | RB59-RB66 | N/A |

### Runbook Inventory

| Runbook ID | Runbook family | Tên runbook | Dùng khi nào | Đối tượng thực hiện | Mức rủi ro | Source locator |
|---|---|---|---|---|---|---|
| RB01 | Lifecycle | Chọn update channel và lập kế hoạch frequent updates | Pre-change | Platform Admin | Medium | Early/Normal channel, frequent updates |
| RB02 | Lifecycle | Apply updates bằng XenCenter | Patch window | Platform Admin | High | Apply updates by using XenCenter |
| RB03 | Lifecycle | Apply updates bằng xe CLI | Patch window / automation | Platform Admin | High | Apply updates by using xe CLI |
| RB04 | Lifecycle | Xác minh XenCenter compatibility | Pre-change / daily readiness | System Engineer | Low | XenCenter |
| RB05 | Licensing | Kiểm tra License Activation Service và licensing state | Pre-change / incident | Platform Admin | Medium | Licensing / LAS |
| RB06 | Lifecycle | Đồng bộ update level giữa pools/hosts | Pre-change | Platform Admin | High | Remote pool update synchronization |
| RB07 | Install | Cài XenServer host baseline | Build / rebuild | Platform Admin | High | Install |
| RB08 | Install | Chuẩn bị installation scenario khác chuẩn | Build / recovery | Platform Admin | High | Other installation scenarios |
| RB09 | Security | Enable và validate certificate verification | Post-install / post-upgrade | Security + Platform | Medium | Certificate verification |
| RB10 | Readiness | Baseline host trước khi đưa vào VDI pool | Pre-production | Platform Admin | Medium | Install / XenCenter |
| RB11 | Pool | Tạo hoặc join resource pool | Build / expansion | Platform Admin | High | Resource pools |
| RB12 | Pool | Daily pool health check cho VDI workloads | Daily | System Engineer | Low | Resource pools |
| RB13 | Pool | Evacuate hoặc remove host khỏi pool có kiểm soát | Change / incident | Platform Admin | High | Resource pools |
| RB14 | Storage/Pool | Chuẩn bị GFS2 clustered pool | Build / storage design | Platform Admin | High | GFS2 clustered pools |
| RB15 | Troubleshooting | Troubleshoot clustered pool issue | Incident | Platform Admin | High | Troubleshoot clustered pools |
| RB16 | Capacity | Kiểm tra pool capacity trước maintenance | Pre-change | System Engineer | Medium | Resource pools / HA |
| RB17 | RBAC | Thiết kế role matrix cho XenServer | Security design | Security + Platform | Medium | RBAC roles |
| RB18 | RBAC | Gán role bằng XenCenter | Access request | Platform Admin | Medium | RBAC roles |
| RB19 | RBAC | Gán/kiểm tra RBAC bằng CLI | Access request / audit | Platform Admin | Medium | Use RBAC with CLI |
| RB20 | RBAC | Audit quyền trước change lớn | Pre-change | Security + Platform | Medium | RBAC roles |
| RB21 | Network | Baseline host networking | Build / daily | System Engineer | Medium | Manage networking |
| RB22 | Network | Cấu hình bond/VLAN cho VDI network | Build / change | Network + Platform | High | Manage networking |
| RB23 | Network | Troubleshoot VDA mất kết nối do XenServer network | Incident | System Engineer | High | Troubleshoot networking |
| RB24 | Network | Kiểm tra management network trước pool/update | Pre-change | Platform Admin | High | Manage networking |
| RB25 | Network | Validate VM network sau migration/import | Post-change | System Engineer | Medium | Networking / import |
| RB26 | Network | Rollback network change an toàn | Recovery | Network + Platform | High | Troubleshoot networking |
| RB27 | Network | Điều tra VLAN/DHCP/network boot issue | Incident | Network + Platform | Medium | Update notes / network boot |
| RB28 | Network | Evidence package cho network escalation | Escalation | System Engineer | Low | Troubleshoot networking |
| RB29 | Storage | Tạo Storage Repository mới | Build / expansion | Storage + Platform | High | Create storage repository |
| RB30 | Storage | Cấu hình NFS SR cho VDI | Build / change | Storage + Platform | High | NFS SRs |
| RB31 | Storage | Cấu hình SMB SR cho VDI | Build / change | Storage + Platform | High | SMB SR |
| RB32 | Storage | Cấu hình GFS2/XFS SR và CBT-aware backup | Build / backup design | Storage + Platform | High | GFS2/XFS / CBT |
| RB33 | Storage | Kiểm tra SR capacity/health trước image operation | Pre-change | System Engineer | Medium | SR / snapshots |
| RB34 | Storage | Troubleshoot SR unavailable/full/slow | Incident | Storage + Platform | High | SR troubleshooting |
| RB35 | Storage | Cleanup snapshot/VDI chain có kiểm soát | Maintenance | Platform Admin | High | Snapshot / SR fixes |
| RB36 | Storage | Evidence package cho storage escalation | Escalation | System Engineer | Low | SR / advanced troubleshooting |
| RB37 | VM Tools | Cài XenServer VM Tools for Windows | Build / image | System Engineer | Medium | VM Tools for Windows |
| RB38 | VM Tools | Cập nhật VM Tools và drivers | Patch / image | System Engineer | Medium | VM Tools updates |
| RB39 | VM Tools | Troubleshoot missing/broken VM Tools | Incident | System Engineer | Medium | VM Tools |
| RB40 | Migration | Import VHDX/AVHDX/VMDK vào XenServer | Migration | Platform Admin | High | Import VMs |
| RB41 | Migration | Export VM để backup/move | Backup / migration | Platform Admin | Medium | Export VMs |
| RB42 | Migration | Migrate workload từ VMware/PVS disk sang XenServer | Migration | Platform Admin | High | Import wizard / VHDX |
| RB43 | Placement | Cấu hình anti-affinity placement group | Availability design | Platform Admin | Medium | VM placement |
| RB44 | Placement | Kiểm tra placement trước host maintenance | Pre-change | System Engineer | Medium | VM placement |
| RB45 | Placement | Troubleshoot VM placement/power-on failure | Incident | Platform Admin | High | VM placement / pool capacity |
| RB46 | HA | Enable HA cho pool | Build / change | Platform Admin | High | High availability |
| RB47 | HA | Validate HA capacity và failover readiness | Pre-change / quarterly | Platform Admin | High | High availability |
| RB48 | HA | Disable/adjust HA trước maintenance | Maintenance | Platform Admin | High | High availability |
| RB49 | HA | Điều tra HA failover không đạt | Incident | Platform Admin | High | High availability |
| RB50 | HA | HA evidence package cho DR review | Escalation / audit | Platform Admin | Low | High availability |
| RB51 | DR | Thiết kế DR runbook cho XenServer-backed VDI | DR planning | DR Owner | High | Disaster recovery |
| RB52 | Backup | Backup host/pool metadata | Scheduled / pre-change | Platform Admin | Medium | Back up hosts |
| RB53 | Backup | Backup VM workload hoặc image VM | Scheduled / pre-change | Backup + Platform | Medium | Back up VMs |
| RB54 | Restore | Restore host hoặc VM và validate CVAD | Recovery | Platform Admin | High | Restore hosts and VMs |
| RB55 | Restore | Diễn tập restore theo user journey | DR test | DR Owner | High | DR and backup |
| RB56 | Snapshot | Tạo snapshot VM/image an toàn | Pre-change | System Engineer | Medium | VM snapshots |
| RB57 | Snapshot | Rollback snapshot sau change lỗi | Recovery | Platform Admin | High | VM snapshots |
| RB58 | Backup | Tích hợp third-party backup / CBT | Backup design | Backup + Platform | High | Third-party backup solutions |
| RB59 | Monitoring | Daily alerts review trong XenCenter | Daily | System Engineer | Low | Alerts |
| RB60 | Monitoring | Health Check service evidence | Daily / incident | System Engineer | Low | Health Check logs |
| RB61 | Troubleshooting | Triage incident VDI nghi do XenServer | Incident | System Engineer | High | Troubleshooting |
| RB62 | Troubleshooting | Thu server status report | Escalation | Platform Admin | Low | Advanced troubleshooting |
| RB63 | Troubleshooting | Điều tra task stuck/fail trong XenCenter | Incident | Platform Admin | Medium | Advanced troubleshooting |
| RB64 | Troubleshooting | Điều tra performance graph/RRDD bất thường | Incident | Platform Admin | Medium | Updates / monitoring fixes |
| RB65 | Support | Chuẩn bị vendor escalation package | Escalation | Platform Admin | Low | Advanced troubleshooting |
| RB66 | Training | Diễn tập map lỗi CVAD sang XenServer layer | Training | Trainer + Engineer | Low | General from source |

## CH01 - Release Model, XenCenter, Licensing and Updates

### Chapter Knowledge Insight Report

CH01 làm rõ rằng XenServer 8.4 là một nền tảng có frequent update model, không phải bản cài xong rồi bỏ yên. XenCenter version, update channel, license activation và update level của pool trở thành một phần của vận hành hằng ngày. Với VDI, update sai thời điểm hoặc pool không đồng nhất có thể gây lỗi VM power, migration, storage behavior, network behavior hoặc CVAD catalog operation.

### RB01 - Chọn update channel và lập kế hoạch frequent updates

#### 0. Tutorial scenario

Bạn đang chuẩn bị đưa một pool XenServer 8.4 vào vận hành cho CVAD. Source nêu XenServer 8.4 nhận frequent updates qua Early Access hoặc Normal channel. Mục tiêu không phải là chọn kênh mới nhất, mà là chọn kênh phù hợp với rủi ro của workload VDI.

#### 1. Bạn sẽ làm được gì sau runbook này

Bạn biết cách đặt update channel thành quyết định vận hành: ai phê duyệt, pool nào nhận trước, evidence nào lưu, và khi nào dừng rollout.

#### 2. Prerequisites

| Hạng mục | Yêu cầu |
|---|---|
| Pool inventory | Danh sách pool/host, workload CVAD liên quan, mapping catalog nếu có |
| Business risk | Production, pilot, lab, DR hoặc test pool |
| Maintenance policy | Need Customer Confirmation |
| Tool | XenCenter latest supported version hoặc `xe` CLI |

#### 3. Procedure

1. Phân loại pool theo vai trò: lab, pilot, production, DR. Việc này quan trọng vì Early Access phù hợp thử nghiệm tính năng, còn production thường cần kênh ổn định hơn.
2. Mở XenCenter và kiểm tra Notifications > Updates để xem update có sẵn. Lưu screenshot hoặc export thông tin update làm evidence.
3. Xác định update có security fix, storage/network fix, licensing change hay VM behavior change. Nếu update chạm storage/network, coi rủi ro là cao với VDI.
4. Chọn pilot pool hoặc một nhóm host ít rủi ro để nhận update trước. Không áp dụng trực tiếp lên toàn bộ production pool nếu chưa có soak.
5. Ghi change record: update channel, pool, host, version trước/sau, owner, rollback/mitigation, postcheck.

#### 4. Validation

Sau khi chọn kế hoạch, phải có pilot ring, maintenance window, tiêu chí success/failure và danh sách user journey sẽ test: VM power on, live migration, VDA registration, CVAD launch.

#### 5. Stop / rollback guardrails

Dừng rollout nếu update có known issue liên quan SR/network/VM import/export, hoặc nếu không có người sở hữu rollback. Rollback update phụ thuộc vendor procedure; nếu không có rollback đơn giản, mitigation là cô lập host/pool hoặc restore từ backup/snapshot theo thiết kế.

#### 6. Source grounding

Source nêu frequent updates, Early Access/Normal channel, XenCenter Notifications > Updates và khả năng apply bằng XenCenter hoặc xe CLI. Việc dùng ring/pilot là `General engineering interpretation` cho môi trường VDI.

### RB02 - Apply updates bằng XenCenter

#### 0. Tutorial scenario

Bạn cần patch pool XenServer chạy desktop VDI. Người dùng chỉ quan tâm sau patch còn launch được desktop hay không; vì vậy update thành công trong XenCenter chưa phải điều kiện đủ.

#### 1. Pre-change checklist

| Kiểm tra | Cách quan sát | Dừng nếu |
|---|---|---|
| Pool health | XenCenter pool/host status | Host degraded hoặc pool inconsistent |
| Active sessions | CVAD Director hoặc công cụ khách hàng | Session critical chưa có kế hoạch drain |
| SR capacity/health | XenCenter SR view | SR full/unavailable |
| VM migration ability | Test/confirmed live migration path | Không migrate được VM cần evacuate |
| Backup/evidence | Screenshot version/pool/update | Không có baseline |

#### 2. Step-by-step procedure

1. Mở XenCenter bằng version được source yêu cầu là latest supported XenCenter cho XenServer 8.4.
2. Chọn pool, vào Notifications > Updates. Ghi tên update, mô tả, host áp dụng, trạng thái trước.
3. Chạy update theo wizard. Khi wizard yêu cầu evacuate/reboot host, xác nhận VM migration hoặc maintenance plan trước khi tiếp tục.
4. Theo dõi task trong XenCenter. Nếu task fail, không retry mù; mở detail, lưu error text, xác định host/SR/network liên quan.
5. Sau update, kiểm tra từng host trong pool có cùng update level mong muốn. Kiểm tra alert mới.
6. Postcheck với VDI: chọn VM/VDA pilot, power operation, VDA registration, CVAD launch, reconnect/logoff.

#### 3. Branching decisions

| Kết quả | Hành động tiếp theo |
|---|---|
| Update pass, VDI pass | Ghi version sau, đóng change sau soak |
| Update pass, VDI fail | Khoanh vùng host/SR/network/VM Tools; không mở rộng rollout |
| Update fail một host | Giữ host khỏi production workload nếu cần, thu log, escalate platform/vendor |
| Pool inconsistent | Dừng change, không update host khác cho tới khi trạng thái rõ |

#### 4. Evidence pack

Tên evidence nên gồm `xenserver-update-<pool>-<date>`: screenshot update view, task result, host version before/after, alert list, CVAD launch validation, affected VM list nếu có lỗi.

### RB03 - Apply updates bằng xe CLI

#### 0. Tutorial scenario

Môi trường yêu cầu automation hoặc remote session không dùng XenCenter. Source cho phép apply updates bằng `xe` CLI, nhưng CLI càng cần guardrail vì dễ chạy sai scope.

#### Procedure

1. Xác định pool/host UUID rõ ràng trước khi chạy lệnh. Không dùng tên host mơ hồ nếu có nhiều pool.
2. Ghi lại lệnh dự kiến trong change record và peer review. Tham số cụ thể phụ thuộc source/vendor command reference; không bịa syntax trong wiki nếu chưa mở reference lệnh.
3. Chạy lệnh read-only để liệt kê update/host state trước. Lưu output.
4. Apply update cho scope đã duyệt. Theo dõi task UUID và trạng thái.
5. Nếu CLI trả lỗi, lưu đầy đủ output, task UUID, host UUID; không chạy lại nhiều biến thể khi chưa hiểu lỗi.
6. Postcheck giống RB02: pool state, host update level, alert, VM operation, VDA registration, user launch.

#### Validation and rollback

Validation giống XenCenter path. Rollback/mitigation phụ thuộc update type; cần vendor procedure hoặc restore/evacuate/maintenance mode plan đã phê duyệt.

## CH02 - Install and Baseline Readiness

### Chapter Knowledge Insight Report

CH02 biến install thành nền móng vận hành. Host XenServer mới chỉ sẵn sàng cho VDI khi đã có XenCenter compatible, management network ổn định, license/activation rõ, certificate verification đúng, storage/network mapping đủ, và baseline evidence trước khi join pool.

### RB07 - Cài XenServer host baseline

#### 0. Tutorial scenario

Bạn build hoặc rebuild một host XenServer 8.4 để đưa vào pool chạy CVAD workloads. Runbook này không thay thế hướng dẫn installer từng màn hình của vendor; nó biến install thành checklist vận hành có validation.

#### Pre-install checklist

| Hạng mục | Trạng thái cần có |
|---|---|
| Hardware compatibility | Need Customer Confirmation theo HCL/thiết kế |
| Network | Management NIC, VLAN, IP/DNS/NTP/gateway đã duyệt |
| Storage | SR backend/path/permission sẵn sàng |
| License | LAS/licensing path đã xác định |
| Console | XenCenter latest supported version |
| Security | Certificate verification plan, credential handling, admin access |
| Rollback | Rebuild plan hoặc remove host khỏi pool nếu join fail |

#### Procedure

1. Cài XenServer 8.4 từ media được duyệt. Ghi version/build và ngày media.
2. Cấu hình management network theo thiết kế. Kiểm tra DNS, gateway, NTP/time sync vì các lỗi này làm hỏng pool join, certificate và quản trị.
3. Kết nối bằng XenCenter compatible. Không dùng XenCenter cũ vì source nêu XenServer 8.4 yêu cầu latest XenCenter dạng `YYYY.x.x`.
4. Cấu hình license/activation theo mô hình hiện hành.
5. Cấu hình certificate verification nếu là fresh install hoặc sau upgrade theo source behavior.
6. Không join production pool cho tới khi baseline health không có alert nghiêm trọng.

#### Validation

Host hiển thị healthy trong XenCenter, quản trị được, management network ổn định, license hợp lệ, certificate không báo lỗi, có thể thấy storage/network dự kiến.

#### Post-install test

Nếu là lab/pilot, tạo hoặc chạy một VM test, kiểm tra power operation, network reachability và storage write. Với VDI production, test thêm VDA registration sau khi host chạy workload pilot.

### RB09 - Enable và validate certificate verification

#### Tutorial scenario

Source nêu certificate verification được bật mặc định trên fresh install XenServer 8.4 trở lên, nhưng upgrade từ phiên bản cũ không tự bật và XenCenter sẽ nhắc enable. Đây là điểm dễ tạo khác biệt giữa pool mới và pool nâng cấp.

#### Procedure

1. Kiểm tra trạng thái certificate verification khi XenCenter kết nối pool/host.
2. Nếu XenCenter cảnh báo, ghi lại pool/host và trạng thái hiện tại.
3. Trước khi enable, xác minh DNS/FQDN và certificate chain trong môi trường. Nếu naming/trust sai, enable có thể làm admin connection hoặc peer trust gặp lỗi.
4. Enable trong maintenance window hoặc theo change nhỏ đã duyệt.
5. Reconnect XenCenter và kiểm tra host/pool không còn cảnh báo.
6. Test management operation read-only, sau đó task nhỏ ít rủi ro nếu cần.

#### Validation

XenCenter kết nối không lỗi certificate, pool/host quản trị được, không có alert mới. Nếu external authentication liên quan AD bị lỗi sau upgrade, xử lý theo evidence và escalation identity/security.

## CH03 - Resource Pools and Clustered Pools

### Chapter Knowledge Insight Report

Pool là blast-radius boundary quan trọng. Một host lỗi có thể chỉ ảnh hưởng vài VM; một pool metadata/storage/cluster issue có thể ảnh hưởng toàn bộ workload VDI. GFS2 clustered pool thêm khả năng shared block/thin provisioning nhưng cũng tăng dependency vào cluster network, fencing và SR consistency.

### RB11 - Tạo hoặc join resource pool

#### Tutorial scenario

Bạn thêm host mới để mở rộng capacity VDI. Sai khác update level, network, storage hoặc license có thể làm pool không ổn định.

#### Procedure

1. Kiểm tra host mới theo RB07/RB10 trước khi join.
2. So sánh update level, XenServer version, license, management network, storage access với pool hiện hữu.
3. Kiểm tra pool coordinator/supporter status và pool health.
4. Join host vào pool bằng XenCenter hoặc CLI theo change đã duyệt.
5. Sau join, kiểm tra host xuất hiện đúng, không alert, thấy SR/network cần thiết.
6. Chỉ đưa VDI workload lên host sau khi test VM/pilot pass.

#### Validation

Pool healthy, host không degraded, VM có thể chạy/migrate, SR/network mapping đúng, CVAD workload pilot register/launch được.

#### Rollback

Nếu join fail hoặc host gây alert, remove khỏi pool theo procedure vendor, giữ log/task evidence, không ép workload production lên host mới.

### RB15 - Troubleshoot clustered pool issue

#### Tutorial scenario

Pool dùng GFS2 clustered storage có lỗi fencing, host communication hoặc SR behavior. Với VDI, biểu hiện có thể là VM power/migration fail hoặc VDA mất đồng loạt theo host/SR.

#### Procedure

1. Xác định phạm vi: một host, nhiều host, một SR, toàn pool.
2. Kiểm tra cluster network/management VLAN và host reachability. Source update notes có nhiều điểm liên quan GFS2 cluster network/non-management VLAN, vì vậy không bỏ qua VLAN.
3. Kiểm tra SR health, GFS2/XFS status và alert.
4. Kiểm tra task fail gần nhất: VM start, migrate, VDI copy, snapshot, backup.
5. Cô lập host bị lỗi nếu có nguy cơ làm lan lỗi, theo HA/maintenance plan.
6. Thu server status report và escalation package nếu không có nguyên nhân rõ.

#### Validation

Cluster/pool healthy trở lại, VM operation pass, không có VDI registration/session issue mới.

## CH04 - RBAC and Least Privilege

### Chapter Knowledge Insight Report

RBAC trong XenServer là guardrail chống lỗi thao tác. Với VDI, một tài khoản có quyền quá rộng có thể đổi network/SR/HA/update và ảnh hưởng hàng trăm desktop. Source có RBAC roles/permissions và CLI usage, nên runbook phải biến quyền thành matrix vận hành.

### RB17 - Thiết kế role matrix cho XenServer

#### Procedure

1. Liệt kê nhóm người dùng: helpdesk, system engineer, platform admin, security auditor, vendor support.
2. Map thao tác cần làm: xem VM, power operation, migrate, snapshot, SR/network change, update, HA, RBAC.
3. Gán least privilege: helpdesk chỉ thao tác được phần được duyệt; platform admin mới đổi pool/SR/network/HA/update.
4. Đánh dấu thao tác cần dual approval: network, SR, HA, update, delete VM, rollback snapshot production.
5. Lưu matrix vào tài liệu vận hành nội bộ; không lưu credential.

#### Validation

Test bằng account mẫu: đúng quyền cần có, bị chặn ở thao tác ngoài phạm vi. Evidence là screenshot/CLI output role assignment và test result.

### RB20 - Audit quyền trước change lớn

#### Procedure

1. Trước change high-risk, liệt kê account có quyền trên pool.
2. Kiểm tra change executor có đúng role, không dùng shared admin account nếu policy cấm.
3. Kiểm tra vendor/temporary access có expiry.
4. Sau change, thu hồi quyền tạm và lưu evidence.

#### Stop conditions

Dừng change nếu chỉ có thể thực hiện bằng credential không rõ owner hoặc quyền quá rộng chưa được phê duyệt.

## CH05 - Networking

### Chapter Knowledge Insight Report

Network trong XenServer là nơi hypervisor failure biến thành CVAD symptom. PIF/VIF/bond/VLAN/management network không chỉ phục vụ host; nó quyết định VM reachability, VDA registration, session stability, migration và storage traffic nếu dùng network storage.

### RB21 - Baseline host networking

#### Procedure

1. Ghi management IP, DNS, gateway, VLAN, physical NIC, bond, MTU và network purpose.
2. Kiểm tra link state/error counter nếu tool cho phép.
3. Kiểm tra VM network mapping cho VDI VLAN.
4. Test connectivity từ VM/VDA pilot tới Controller, DNS, StoreFront/Gateway path phù hợp.
5. Lưu sơ đồ host NIC-to-switch-to-VLAN ở mức không chứa secret.

#### Validation

Host quản trị ổn định, VM có IP đúng VLAN, VDA registered, session launch pass. Nếu chỉ host ping được nhưng VDA không register, chưa đủ validation.

### RB22 - Cấu hình bond/VLAN cho VDI network

#### Pre-config checklist

| Hạng mục | Yêu cầu |
|---|---|
| Network design | Need Customer Confirmation |
| Switch config | VLAN/trunk/LACP/MTU nhất quán |
| Maintenance window | Có, vì ảnh hưởng connectivity |
| Rollback | Cấu hình cũ, out-of-band access hoặc onsite access nếu mất management |

#### Procedure

1. Xác nhận VLAN và bond mode với network team.
2. Ghi cấu hình hiện tại trước khi đổi.
3. Thực hiện thay đổi trên host/pool theo phạm vi nhỏ.
4. Kiểm tra management không mất, storage network nếu có vẫn reachable.
5. Test VM trên VLAN VDI, VDA registration và CVAD launch.

#### Stop conditions

Dừng nếu mất management network, SR network flapping, hoặc VM pilot không có connectivity. Không tiếp tục host khác khi host đầu tiên chưa pass.

### RB23 - Troubleshoot VDA mất kết nối do XenServer network

#### Procedure

1. Map affected VDA theo host, network, VLAN và Delivery Group/Catalog.
2. Nếu các VDA lỗi cùng host hoặc VLAN, ưu tiên XenServer host network thay vì CVAD entitlement.
3. Kiểm tra XenCenter network alerts, PIF/bond state, VM VIF connected state.
4. Kiểm tra từ OS VM: IP, gateway, DNS, Controller reachability.
5. Nếu external session drop, phân biệt VDA-to-Controller path và user-to-VDA/Gateway path.
6. Thu evidence và escalate network/platform nếu phát hiện switch/VLAN/bond issue.

#### Evidence

Affected VM list, host, network/VLAN, timestamp, PIF/VIF state, user symptom, CVAD registration state.

## CH06 - Storage Repository

### Chapter Knowledge Insight Report

SR là lớp dữ liệu của XenServer. Với VDI, SR full, unavailable hoặc chậm có thể làm VM boot fail, snapshot fail, image update fail, backup kéo dài hoặc session logon chậm. Source có create SR, NFS, SMB, GFS2/XFS và CBT, nên runbook phải coi storage là dependency của cả performance và recovery.

### RB29 - Tạo Storage Repository mới

#### Pre-config checklist

| Hạng mục | Yêu cầu |
|---|---|
| Backend | NFS/SMB/block/GFS2/XFS theo thiết kế |
| Access | Host/pool có quyền và network path |
| Capacity | Đủ cho VM disks, snapshots, backup overhead |
| Performance | Need Customer Confirmation về IOPS/latency |
| Backup | CBT/third-party support nếu cần |

#### Procedure

1. Xác định workload: desktop persistent, non-persistent, image, ISO, backup target hay test.
2. Tạo SR bằng XenCenter hoặc CLI theo vendor procedure.
3. Gán tên rõ nghĩa gồm pool/site/purpose, tránh tên chung chung.
4. Kiểm tra tất cả host trong pool thấy SR nếu là shared SR.
5. Tạo VM/test disk nhỏ để xác minh read/write.
6. Kiểm tra alert/capacity sau khi attach.

#### Validation

SR healthy, shared visibility đúng, VM test thao tác disk pass, không có alert backend. Với VDI, kiểm tra thêm catalog/image operation nếu SR dùng cho CVAD.

#### Rollback

Detach/remove SR mới nếu chưa có production data. Nếu đã chứa VM, không xóa trước khi backup/migrate data và có approval.

### RB33 - Kiểm tra SR capacity/health trước image operation

#### Procedure

1. Trước snapshot/clone/catalog update, kiểm tra SR free capacity và alert.
2. Ước lượng tăng trưởng snapshot/clone theo số máy và image size. Nếu không có số liệu, ghi `Need Customer Confirmation`.
3. Kiểm tra backup window đang chạy hay không để tránh IO contention.
4. Kiểm tra task tồn đọng trên SR.
5. Chỉ bắt đầu image operation khi capacity và IO window đạt điều kiện.

#### Validation

Image operation hoàn tất, không làm SR full, VM boot/register pass, không có latency/alert bất thường.

### RB34 - Troubleshoot SR unavailable/full/slow

#### Procedure

1. Xác định SR nào ảnh hưởng và VM nào nằm trên SR đó.
2. Kiểm tra SR status trong XenCenter, capacity, backend path, network storage connectivity.
3. Nếu SR full, dừng snapshot/clone/backup mới và xác định safe cleanup.
4. Nếu SR unavailable, kiểm tra storage backend và network path; không reboot host hàng loạt khi chưa rõ backend.
5. Map VM lỗi sang CVAD catalog/delivery group để thông báo phạm vi user.
6. Thu SR evidence và escalate storage/platform.

#### Stop conditions

Không xóa VDI/snapshot chain nếu chưa hiểu dependency. Không force detach SR có VM production đang dùng trừ khi DR/incident commander phê duyệt.

## CH07 - VM Tools, Import/Export, Migration and Placement

### Chapter Knowledge Insight Report

CH07 nối hypervisor với guest OS. VM Tools giúp XenServer quản lý và quan sát VM; import/export và placement quyết định workload đi đâu; anti-affinity giúp giảm rủi ro dồn VM lên cùng host. Với CVAD, guest tools lỗi có thể làm power/migration/monitoring sai; placement xấu có thể làm một host failure ảnh hưởng quá nhiều VDA.

### RB37 - Cài XenServer VM Tools for Windows

#### Procedure

1. Trên image/VM pilot, kiểm tra VM Tools hiện có hay chưa và version.
2. Cài XenServer VM Tools for Windows theo source/vendor installer.
3. Xác định policy auto-update drivers/management agent nếu conversion/import workflow có lựa chọn này.
4. Reboot nếu yêu cầu.
5. Kiểm tra trong XenCenter VM Tools status và trong Windows event/device state.
6. Test power operation, graceful shutdown/reboot, network/storage driver behavior, VDA registration.

#### Validation

Tools status healthy, driver không lỗi, VM management operation chính xác, CVAD launch pass.

### RB40 - Import VHDX/AVHDX/VMDK vào XenServer

#### Tutorial scenario

Source nêu import wizard hỗ trợ VHDX/AVHDX và disk image import tốt hơn, có thể giúp Citrix customer migrate vDisk từ VMware sang XenServer. Đây là migration có rủi ro cao vì liên quan driver, VM Tools, disk format và network mapping.

#### Procedure

1. Xác định source disk format, OS, boot mode, network requirement và licensing.
2. Export/copy disk từ source theo quy trình an toàn.
3. Dùng XenCenter Import wizard để import vào pool hoặc host được duyệt.
4. Trong wizard, chọn SR, network, VM resources và VM Tools configuration phù hợp.
5. Boot VM trong isolated/pilot network nếu cần để tránh conflict.
6. Cài/cập nhật VM Tools sau import.
7. Nếu VM là VDA/image, kiểm tra domain identity, VDA registration, app/service, CVAD launch.

#### Validation

VM boot được, network đúng, tools healthy, không có duplicate identity, VDA/user journey pass nếu là workload CVAD.

### RB43 - Cấu hình anti-affinity placement group

#### Procedure

1. Xác định nhóm VM không nên chạy cùng host: Delivery Controller, infrastructure VM, hoặc nhóm VDA quan trọng nếu thiết kế yêu cầu.
2. Tạo placement/anti-affinity group theo source feature.
3. Gán VM vào group với quy tắc phù hợp.
4. Kiểm tra placement sau power cycle/migration.
5. Validate host failure scenario bằng simulation hoặc review capacity, không nhất thiết test failure production.

#### Validation

VM trải đều theo rule, host maintenance không phá capacity, VDI service không dồn rủi ro vào một host.

## CH08 - High Availability

### Chapter Knowledge Insight Report

HA không phải nút bật magic. HA cần shared state, heartbeat, pool capacity, network/storage ổn định và workload được thiết kế để failover. Với VDI, HA pass phải được đo bằng VM restart/migration và CVAD session recovery, không chỉ bằng trạng thái "HA enabled".

### RB46 - Enable HA cho pool

#### Pre-config checklist

| Kiểm tra | Yêu cầu |
|---|---|
| Pool health | Không degraded |
| Shared storage / heartbeat | Theo thiết kế HA |
| Capacity | Đủ host/resource để chịu failure |
| Workload priority | VM nào cần restart trước |
| Maintenance process | Cách disable/adjust HA khi bảo trì |

#### Procedure

1. Xác nhận pool, SR, network và host capacity đạt điều kiện.
2. Xác định restart priority cho VM quan trọng.
3. Enable HA theo XenCenter/vendor procedure.
4. Kiểm tra cảnh báo HA và protected VM list.
5. Ghi cấu hình HA và owner.

#### Validation

HA enabled không báo lỗi, capacity plan cho N-1/N+1 rõ, VM priority đúng, DR/operations team biết cách xử lý khi host failure.

### RB47 - Validate HA capacity và failover readiness

#### Procedure

1. Kiểm tra host count, usable capacity, reserved capacity và VM load.
2. Xác định host failure nào làm thiếu capacity.
3. Kiểm tra SR/network dependency của protected VMs.
4. Chạy tabletop hoặc lab failover test nếu production không cho phép.
5. Với VDI, validate sau failover: VM boot, VDA registered, user launch/reconnect.

#### Evidence

HA config, capacity screenshot, protected VM list, test result, CVAD validation.

## CH09 - Disaster Recovery, Backup, Restore and Snapshots

### Chapter Knowledge Insight Report

CH09 nhấn mạnh rằng snapshot, backup và DR không giống nhau. Snapshot hỗ trợ rollback nhanh nhưng tiêu thụ SR và không thay thế backup. Backup/restore host/VM bảo vệ dữ liệu/cấu hình nhưng chỉ có giá trị khi restore được chứng minh bằng workload validation. Với VDI, restore thành công nghĩa là CVAD nhìn thấy máy, VDA registered và user launch được.

### RB51 - Thiết kế DR runbook cho XenServer-backed VDI

#### Procedure

1. Xác định scope: pool, host, SR, VM image, VDA persistent VM, infrastructure VM.
2. Xác định RTO/RPO với owner kinh doanh. Nếu chưa có, ghi `Need Customer Confirmation`.
3. Map dependency: CVAD Controller/StoreFront/Gateway/SQL, XenServer pool, SR, network, identity.
4. Xác định restore order: hạ tầng quản trị, storage/network, hypervisor pool, VM infrastructure, VDA workloads.
5. Viết validation bằng user journey: login, enumerate, launch, reconnect, profile/app.

#### Validation

DR runbook có owner, dependency, restore order, evidence template và test schedule. Không gọi là DR-ready nếu chưa có restore test.

### RB56 - Tạo snapshot VM/image an toàn

#### Procedure

1. Xác định snapshot dùng cho pre-change rollback, image versioning hay short-term protection.
2. Kiểm tra SR free capacity và active backup job.
3. Với VM production, xác nhận application consistency requirement. Nếu không rõ, ghi `Need Customer Confirmation`.
4. Tạo snapshot, đặt tên gồm VM/purpose/date/change ID.
5. Ghi snapshot vào change record.
6. Sau change, quyết định retain/delete snapshot theo retention policy.

#### Stop conditions

Dừng nếu SR gần đầy, backup đang gây IO cao, hoặc không rõ snapshot có nhất quán với workload hay không.

### RB57 - Rollback snapshot sau change lỗi

#### Procedure

1. Xác nhận symptom thật sự do change cần rollback, không phải lỗi ngoài phạm vi.
2. Thông báo impact: rollback sẽ mất trạng thái sau snapshot nếu VM/data thay đổi.
3. Power state và application state phải theo procedure vendor/application.
4. Rollback snapshot hoặc revert image theo phê duyệt.
5. Boot VM, kiểm tra OS, network, VM Tools, VDA registration, CVAD launch.
6. Lưu evidence và RCA.

#### Anti-pattern

Không rollback snapshot production để "thử xem" khi chưa hiểu dữ liệu phát sinh sau snapshot.

## CH10 - Alerts, Monitoring and Advanced Troubleshooting

### Chapter Knowledge Insight Report

CH10 là evidence discipline. XenCenter alerts, Health Check logs, server status report và advanced troubleshooting giúp engineer không xử lý incident bằng cảm tính. Với VDI, evidence phải nối được từ user symptom sang VM, host, SR, network và pool task.

### RB59 - Daily alerts review trong XenCenter

#### Procedure

1. Mở XenCenter và lọc alerts theo severity/time.
2. Nhóm alert theo pool/host/SR/network/VM/license/update.
3. Map alert high severity sang workload CVAD liên quan nếu có.
4. Ghi action: acknowledge, investigate, open incident, or monitor.
5. Không clear alert chỉ để "dashboard sạch" nếu chưa có action/evidence.

#### Validation

Daily review có danh sách alert xử lý, owner, trạng thái và impact VDI nếu có.

### RB61 - Triage incident VDI nghi do XenServer

#### Tutorial scenario

Helpdesk báo nhiều user không launch được desktop. Trước khi kết luận Citrix lỗi, engineer cần chứng minh có hoặc không có dấu hiệu từ XenServer.

#### Procedure

1. Thu danh sách affected users/VMs/Delivery Group/Catalog từ CVAD.
2. Map VMs sang XenServer host, SR, network.
3. Kiểm tra pattern: cùng host, cùng SR, cùng VLAN, cùng pool hay rải rác.
4. Kiểm tra XenCenter alerts/tasks cùng timestamp.
5. Kiểm tra VM power state, tools state, network state, SR health.
6. Nếu pattern tập trung ở XenServer layer, mở incident platform/storage/network kèm evidence.
7. Nếu XenServer sạch, trả evidence cho CVAD team để đi tiếp broker/policy/StoreFront.

#### Evidence pack

`incident-<id>-xenserver-triage`: affected VM list, host/SR/network mapping, alert screenshot, task errors, timestamp correlation, CVAD symptom, conclusion.

### RB65 - Chuẩn bị vendor escalation package

#### Procedure

1. Tóm tắt issue bằng state machine: action nào fail, object nào, từ khi nào.
2. Ghi pool/host/SR/VM UUID hoặc tên, version/update level, XenCenter version.
3. Đính kèm server status report hoặc log bundle theo yêu cầu support.
4. Đính kèm task error, alerts, timeline, change gần nhất.
5. Ghi impact VDI: số VM, Delivery Group/Catalog, user affected, workaround đã thử.
6. Nêu câu hỏi cụ thể cho vendor: cần RCA, hotfix, recovery path hay confirmation known issue.

#### Anti-patterns

Escalate chỉ với câu "VM không chạy"; thiếu UUID/timestamp; không nói update level; không liên kết impact tới workload.

## Knowledge Atoms

| Atom | Insight vận hành |
|---|---|
| Frequent updates | XenServer 8.4 thay đổi theo update stream, nên version/update level là evidence bắt buộc khi troubleshooting |
| XenCenter compatibility | Admin console cũ có thể không phù hợp XenServer 8.4 |
| Pool | Là blast-radius boundary cho VDI workload |
| SR | Là dependency vừa của performance vừa của rollback/backup |
| Network | Hypervisor network lỗi có thể biểu hiện như VDA registration/session issue |
| VM Tools | Guest management state ảnh hưởng power operation, driver và observability |
| HA | Cần capacity và validation, không chỉ trạng thái enabled |
| Snapshot | Là rollback ngắn hạn có rủi ro SR/data consistency, không thay backup |
| RBAC | Là guardrail change, không chỉ compliance |
| Evidence | Cần map CVAD symptom sang pool/host/SR/network/VM trước escalation |

## Training Conversion

| Training asset | Nội dung tạo được từ trang này |
|---|---|
| Concept explanation | XenServer pool, SR, VM Tools, HA, snapshot, RBAC, update stream |
| Scenario lab | VDA unregistered do host network, SR full trước image update, pool update fail |
| Checklist | Pre-update, pre-SR change, pre-HA enablement, daily alert review |
| Troubleshooting table | CVAD symptom to XenServer layer mapping |
| Knowledge check | Phân biệt snapshot/backup/HA; pool vs host blast radius; SR vs VM disk |
| Operating model | Change ring, evidence pack, escalation routing |

## Need Customer Confirmation

- Production CVAD có dùng XenServer 8.4 không, hay XenServer chỉ là nguồn đào tạo thay thế?
- Pool count, host count, SR backend, network/VLAN/bond design, HA state là gì?
- LAS/licensing model đã chuyển đổi chưa?
- Update channel và patch cadence hiện tại?
- Backup tool, CBT usage, RPO/RTO và restore test gần nhất?
- RBAC role matrix hiện tại và quyền helpdesk/platform/vendor?
- Mapping giữa CVAD Machine Catalog/Delivery Group với XenServer pool/host/SR?

## Related Concepts

- [[concepts/xenserver]]
- [[concepts/hypervisor-pool]]
- [[concepts/storage-repository]]
- [[concepts/virtual-networking]]
- [[concepts/snapshot]]
- [[concepts/high-availability]]
- [[concepts/backup-and-recovery]]
- [[concepts/lifecycle-management]]
- [[concepts/identity-and-access-management]]
- [[concepts/monitoring-and-logs]]

## Related Sources

- [[sources/xenserver-8-4]]
- [[sources/citrix-virtual-apps-and-desktops-7-2603]]
- [[sources/citrix-virtual-apps-and-desktops-7-2603-chapter-runbook-ingest]]
- [[sources/vmware-vsphere-8-0]]

## Self Review

- Đã lập Source Inventory, TOC extraction và Chapter Map.
- Đã chuyển 10 vùng/chapter lớn thành insight tri thức gắn với VDI operations.
- Đã trích xuất 66 runbook inventory, gồm install/config/update/network/storage/HA/DR/backup/troubleshooting/RBAC.
- Đã viết chi tiết các runbook trọng yếu ở mức tutorial với scenario, precheck, procedure, validation, rollback/stop condition và evidence.
- Đã đánh dấu các dữ liệu production cần xác nhận là `Need Customer Confirmation`.
