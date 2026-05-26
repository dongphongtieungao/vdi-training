---
id: source-fslogix-documentation-chapter-runbook-ingest
title: FSLogix Documentation - Chapter Insight and Tutorial Runbook Ingest
type: source
created: 2026-05-26
updated: 2026-05-26
authors:
  - Microsoft
year: 2026
importance: 5
urls: []
raw_paths:
  - raw/sources/fslogix.txt
provenance: replayable
confidence: high
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

Trang này là lớp ingest theo `chapter-ingest-loop.prompt` cho source FSLogix. Mục tiêu là chuyển tài liệu vendor thành báo cáo insight tri thức và runbook thực hành cho profile operations trong VDI: cài đặt FSLogix, cấu hình Profile Container, ODFC Container, Cloud Cache, redirections.xml, storage permissions, registry/GPO, antivirus exclusions, VHD compaction, HA/DR và troubleshooting. Trang này bổ sung cho [[sources/fslogix-documentation]].

## Source Inventory

| Trường | Giá trị |
|---|---|
| Raw file | `raw/sources/fslogix.txt` |
| File size | 605,552 bytes |
| Source type | Vendor documentation / profile management guide |
| Product/platform | Microsoft FSLogix |
| Version | Source filename does not specify exact version; source includes modern FSLogix/Cloud Cache/Teams content |
| Ingest mode | Chapter/major-section insight loop with tutorial runbooks |
| Primary VDI use | Profile, Office cache, storage, logon performance, HA/DR, incident troubleshooting |

## Chapter Knowledge Insight Report

FSLogix là lớp giữ trạng thái người dùng trong VDI, nên không thể được vận hành như một agent phụ. Khi Profile Container hoặc ODFC attach chậm, mount fail, storage latency cao, Cloud Cache provider unhealthy, redirections.xml sai, hoặc antivirus lock file VHD/VHDX, triệu chứng phía người dùng có thể là logon chậm, temporary profile, black screen, Outlook/Teams/OneDrive lỗi hoặc sign-out treo. Báo cáo này chuyển nội dung source thành mô hình vận hành: container attach state, storage path/permission, registry/GPO configuration, application cache behavior, Cloud Cache sync path, evidence/log path và recovery guardrail.

## Central Knowledge Thesis

**Thesis:** Trong môi trường VDI, FSLogix không chỉ là công cụ roaming profile mà là dependency trực tiếp của logon, application state, storage availability và user data recovery. Mọi thay đổi vào FSLogix agent, Profile Container, ODFC, Cloud Cache, redirections.xml, storage permissions hoặc antivirus exclusions đều có thể ảnh hưởng dữ liệu người dùng và trải nghiệm phiên. Vì vậy engineer phải vận hành FSLogix bằng precheck, pilot user, log/evidence, rollback cấu hình, và validation bằng user sign-in/sign-out thật thay vì chỉ kiểm tra rằng GPO đã apply.

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
| Depth Exception | Exact registry values and command syntax remain vendor-reference where not visible in extracted source; mark Need Customer Confirmation for production paths |

## Table of Contents Extracted

| Chapter | Title | Source locator | Priority |
|---|---|---|---|
| CH01 | Overview, use cases and terminology | TOC/intro lines 130-196; glossary lines 672-747 | High |
| CH02 | Install FSLogix and product support | TOC line 60; FAQ/support lines 755-807; support lines 1474+ | High |
| CH03 | Group Policy templates, registry and configuration methods | TOC line 62; registry/GPO lines 1180-1194 and 2124-2144 | High |
| CH04 | Profile Container architecture and storage design | Profile container lines 1721-1789; storage lines 1968-2064 | High |
| CH05 | ODFC Container, Office/Teams/OneDrive/Outlook | TOC line 36; ODFC lines 1835-1906; Teams/OneDrive lines 833-910 | High |
| CH06 | Cloud Cache and HA/DR | TOC lines 38, 66-74; Cloud Cache FAQ lines 1110-1142 | High |
| CH07 | redirections.xml | TOC line 42; redirections FAQ lines 987-1068 | High |
| CH08 | VHD/VHDX sizing and disk compaction | FAQ lines 807-820; compaction lines 1068-1106 | High |
| CH09 | Storage permissions, network and antivirus/security exclusions | storage/network lines 1528-1558; exclusions lines 1570-1683 | High |
| CH10 | Troubleshooting, logs, PowerShell and escalation | support/troubleshooting lines 472-474, 807+, 1474+ | High |

## Chapter Map

| Chapter ID | Title | Main keywords | Related VDI topics | Status | Notes |
|---|---|---|---|---|---|
| CH01 | FSLogix operating model | container, VHDX, profile, ODFC, Cloud Cache | Foundation, profile | Extracted | RB01-RB04 |
| CH02 | Install and supportability | install package, support, version | Image, lifecycle | Extracted | RB05-RB09 |
| CH03 | Configuration delivery | GPO, registry, PowerShell, templates | Policy, change | Extracted | RB10-RB14 |
| CH04 | Profile Container and storage | VHDLocations, SMB, profile attach, storage | Storage, logon | Extracted | RB15-RB21 |
| CH05 | ODFC and Microsoft 365 app data | ODFC, Outlook, Teams, OneDrive | App profile | Extracted | RB22-RB28 |
| CH06 | Cloud Cache and HA/DR | CCDLocations, provider, sync, BCDR | HA/DR | Extracted | RB29-RB36 |
| CH07 | redirections.xml | exclusions, local redirect, profile size | Performance, policy | Extracted | RB37-RB42 |
| CH08 | VHD sizing and compaction | 30% free space, logoff, compaction | Capacity, performance | Extracted | RB43-RB48 |
| CH09 | Storage/network/security exclusions | permissions, AV, SMB, latency | Security, storage | Extracted | RB49-RB56 |
| CH10 | Troubleshooting and escalation | logs, frxsvc, events, provider health | Incident, support | Extracted | RB57-RB66 |

## Runbook Best Practices Extracted

### Runbook Source Coverage

| Source subsection / heading | Operational content found | Runbook mapping | Coverage status | Nếu chưa tạo runbook, lý do |
|---|---|---|---|---|
| FSLogix overview / terminology | Container, VHD(x), Profile, ODFC, Cloud Cache, storage | RB01-RB04 | Covered | N/A |
| Install FSLogix | Install package and post-install configuration | RB05-RB07 | Covered | N/A |
| FSLogix product support | Latest supported version, support request evidence | RB08-RB09, RB65 | Covered | N/A |
| Use Group Policy templates | Policy delivery and scale | RB10-RB12 | Covered | N/A |
| Registry configuration | Per-machine registry settings, manual/PowerShell/GPO | RB13-RB14 | Covered | N/A |
| Configure Profile Container | Profile attach, VHDLocations, profile data | RB15-RB18 | Covered | N/A |
| Storage providers and SMB | Share design, capacity, latency | RB19-RB21, RB49-RB52 | Covered | N/A |
| Configure ODFC containers | Office-only container use cases | RB22-RB24 | Covered | N/A |
| OneDrive/Teams/Outlook behavior | App-specific cache and VDI app state | RB25-RB28 | Covered | N/A |
| Configure Cloud Cache containers | CCDLocations, providers, local cache, sync | RB29-RB34 | Covered | N/A |
| High availability and disaster recovery | HA, BCDR, standard containers vs Cloud Cache | RB35-RB36, RB53-RB55 | Covered | N/A |
| Create and implement redirections.xml | Exclusions, local redirects, sign-out behavior | RB37-RB42 | Covered | N/A |
| VHD disk compaction | Compaction threshold, logoff behavior, Cloud Cache effect | RB43-RB46 | Covered | N/A |
| Free space planning | 30% free space, 2 GB/500 MB warnings | RB47-RB48 | Covered | N/A |
| Antivirus/security exclusions | frxsvc/frxccds, VHD/VHDX, SMB files, mount points, registry | RB49-RB56 | Covered | N/A |
| Troubleshooting/support/logs | Event/text logs, PowerShell module, escalation evidence | RB57-RB66 | Covered | N/A |

### Mandatory Installation and Configuration Runbooks

| Source procedure / config heading | Procedure type | Runbook required? | Runbook ID | Nếu không tạo, lý do |
|---|---|---|---|---|
| Install FSLogix | Install | Yes | RB05 | N/A |
| Update FSLogix in image | Upgrade / lifecycle | Yes | RB06 | N/A |
| Use Group Policy templates | Configure | Yes | RB10 | N/A |
| Configure registry settings | Configure | Yes | RB13 | N/A |
| Configure Profile Container | Configure | Yes | RB15-RB18 | N/A |
| Configure ODFC Container | Configure | Yes | RB22-RB24 | N/A |
| Configure Cloud Cache | Configure / HA | Yes | RB29-RB34 | N/A |
| Create and implement redirections.xml | Configure / Optimize | Yes | RB37-RB42 | N/A |
| Configure storage permissions | Configure / Security | Yes | RB49-RB52 | N/A |
| Configure antivirus/security exclusions | Configure / Security | Yes | RB53-RB56 | N/A |
| VHD disk compaction | Configure / Validate | Yes | RB43-RB46 | N/A |
| Troubleshooting/support | Remediate / Escalate | Yes | RB57-RB66 | N/A |

### Runbook Inventory

| Runbook ID | Runbook family | Tên runbook | Dùng khi nào | Đối tượng thực hiện | Mức rủi ro | Source locator |
|---|---|---|---|---|---|---|
| RB01 | Foundation | Vẽ operating model FSLogix cho VDI | Onboarding | System Engineer | Low | Overview/terminology |
| RB02 | Foundation | Chọn Profile Container vs ODFC vs kết hợp | Design | VDI Architect | Medium | ODFC/Profile guidance |
| RB03 | Foundation | Map symptom logon/app sang FSLogix layer | Incident | Helpdesk/System Engineer | Medium | FAQ/troubleshooting |
| RB04 | Evidence | Chuẩn hóa evidence baseline FSLogix | Daily/incident | System Engineer | Low | Logs/support |
| RB05 | Install | Cài FSLogix agent trong golden image | Build/image | System Engineer | High | Install FSLogix |
| RB06 | Upgrade | Cập nhật FSLogix agent theo pilot ring | Patch/change | System Engineer | High | Product support |
| RB07 | Install | Post-install validation FSLogix service/logs | Post-install | System Engineer | Medium | Install/config |
| RB08 | Support | Xác minh version supportability | Pre-change/incident | System Engineer | Low | Product support |
| RB09 | Support | Chuẩn bị support package trước case Microsoft | Escalation | Platform Admin | Low | Support |
| RB10 | Policy | Deploy FSLogix ADMX/GPO templates | Configure | System Engineer | Medium | Use GPO templates |
| RB11 | Policy | Scope GPO theo pilot user/machine | Pre-change | System Engineer | Medium | GPO configuration |
| RB12 | Policy | Rollback GPO/registry change | Recovery | System Engineer | High | Registry/GPO |
| RB13 | Registry | Configure FSLogix registry settings | Configure | System Engineer | Medium | Registry settings |
| RB14 | Registry | Audit resultant FSLogix configuration | Daily/incident | System Engineer | Low | Registry/GPO |
| RB15 | Profile | Configure Profile Container | Configure | System Engineer | High | Profile container |
| RB16 | Profile | Validate profile attach/mount at logon | Post-change | System Engineer | Medium | Profile attach |
| RB17 | Profile | Troubleshoot temporary profile/container fail | Incident | System Engineer | High | FAQ/troubleshooting |
| RB18 | Profile | Recover from stale lock or failed detach | Incident | Platform Admin | High | Container detach |
| RB19 | Storage | Design VHDLocations and SMB storage path | Design | Storage + VDI | High | Storage providers |
| RB20 | Storage | Validate profile share permissions | Configure | Storage + VDI | High | Storage permissions |
| RB21 | Storage | Monitor profile storage capacity/latency | Daily | System Engineer | Medium | Storage/FAQ |
| RB22 | ODFC | Configure ODFC Container | Configure | System Engineer | Medium | ODFC containers |
| RB23 | ODFC | Decide whether ODFC should coexist with Profile Container | Design | VDI Architect | Medium | ODFC guidance |
| RB24 | ODFC | Troubleshoot ODFC mount/create failure | Incident | System Engineer | Medium | ODFC release notes |
| RB25 | Apps | Validate Outlook data roaming | Post-change | App/VDI Engineer | Medium | ODFC/Outlook |
| RB26 | Apps | Validate Teams data roaming and launch | Post-change | App/VDI Engineer | Medium | Teams/ODFC |
| RB27 | Apps | Validate OneDrive with FSLogix | Post-change | App/VDI Engineer | Medium | OneDrive FAQ |
| RB28 | Apps | Reset application cache safely | Incident | App/VDI Engineer | High | ODFC/app data |
| RB29 | Cloud Cache | Configure Cloud Cache providers | Configure/HA | VDI Architect | High | Cloud Cache |
| RB30 | Cloud Cache | Validate provider health and failover behavior | HA test | Platform Admin | High | Cloud Cache |
| RB31 | Cloud Cache | Troubleshoot unhealthy provider | Incident | Platform Admin | High | Cloud Cache PowerShell |
| RB32 | Cloud Cache | Investigate long sign-out with Cloud Cache | Incident | System Engineer | Medium | Cloud Cache FAQ |
| RB33 | Cloud Cache | Configure limited local cache | Configure | Platform Admin | Medium | CcdMaxCacheSizeInMBs |
| RB34 | Cloud Cache | Rollback Cloud Cache to standard VHDLocations | Recovery | VDI Architect | High | Cloud Cache/HA |
| RB35 | HA/DR | Decide standard HA storage vs Cloud Cache | Design | Architect/Storage | High | HA/DR FAQ |
| RB36 | HA/DR | Restore user profile container and validate | Recovery | Platform Admin | High | BCDR |
| RB37 | Redirection | Create redirections.xml | Configure | System Engineer | Medium | redirections.xml |
| RB38 | Redirection | Deploy redirections.xml through controlled source | Configure | System Engineer | Medium | RedirXMLSourceFolder |
| RB39 | Redirection | Validate redirections events in logs | Post-change | System Engineer | Low | redirections FAQ |
| RB40 | Redirection | Troubleshoot profile growth after exclusions | Incident | System Engineer | Medium | redirections FAQ |
| RB41 | Redirection | Rollback redirections.xml safely | Recovery | System Engineer | Medium | redirections.xml |
| RB42 | Redirection | Review redirections for Teams/OneDrive risk | Design | App/VDI Engineer | Medium | Teams/OneDrive |
| RB43 | VHD | Plan VHD/VHDX size and free space | Design | Storage + VDI | High | FAQ free space |
| RB44 | VHD | Validate VHD disk compaction | Post-change | System Engineer | Medium | VHD compaction |
| RB45 | VHD | Troubleshoot compaction not running | Incident | System Engineer | Medium | Compaction FAQ |
| RB46 | VHD | Investigate reconnect blocked by disk in use | Incident | System Engineer | High | Compaction/sign-out |
| RB47 | Capacity | Monitor 2GB/500MB free space warnings | Daily | System Engineer | Medium | FAQ warnings |
| RB48 | Capacity | Respond to container full/low-space event | Incident | System Engineer | High | FAQ capacity |
| RB49 | Security | Configure FSLogix AV exclusions | Configure | Security + VDI | High | AV exclusions |
| RB50 | Security | Validate AV exclusions after policy deployment | Post-change | Security + VDI | Medium | AV exclusions |
| RB51 | Storage | Troubleshoot permission denied on container path | Incident | Storage + VDI | High | Storage permissions |
| RB52 | Storage | Audit storage ACL without reading user data | Audit | Security/Storage | Medium | Storage permissions |
| RB53 | Security | Protect FSLogix registry/policy keys | Configure | Security + VDI | Medium | AV/DLP exclusions |
| RB54 | Security | Handle profile data access approval | Incident | Security + VDI | High | Security interpretation |
| RB55 | Network | Validate network latency to profile storage | Daily/incident | Network + VDI | Medium | Network config |
| RB56 | Network | Troubleshoot storage path outage | Incident | Network/Storage | High | Storage/network |
| RB57 | Troubleshooting | Triage slow logon | Incident | Helpdesk/System Engineer | High | FAQ logon time |
| RB58 | Troubleshooting | Triage temporary profile | Incident | System Engineer | High | FAQ/troubleshooting |
| RB59 | Troubleshooting | Triage logoff hang | Incident | System Engineer | Medium | Cloud Cache/compaction |
| RB60 | Troubleshooting | Triage Outlook/Teams/OneDrive issue | Incident | App/VDI Engineer | Medium | ODFC/Apps |
| RB61 | Logs | Collect FSLogix text/event logs | Incident | System Engineer | Low | Logs/support |
| RB62 | Logs | Correlate FSLogix logs with CVAD/Horizon logon | Incident | System Engineer | Medium | General interpretation |
| RB63 | Service | Troubleshoot frxsvc/frxccds service issue | Incident | System Engineer | High | frxsvc/frxccds |
| RB64 | PowerShell | Use FSLogix PowerShell for Cloud Cache investigation | Incident | Platform Admin | Medium | PowerShell module |
| RB65 | Escalation | Build Microsoft support escalation package | Escalation | Platform Admin | Low | Product support |
| RB66 | Training | Lab: map profile symptom to storage/config/app layer | Training | Trainer | Low | Whole source |

## CH01 - Operating Model and Container Choice

### Chapter Knowledge Insight Report

CH01 làm rõ FSLogix là mô hình container hóa user state. Profile Container lưu toàn bộ profile; ODFC tập trung dữ liệu Office/Microsoft 365; Cloud Cache là cơ chế provider/cache chứ không phải loại container riêng. Insight vận hành: khi user báo lỗi, engineer phải hỏi "container nào, path nào, state nào, app data nào" trước khi sửa.

### RB01 - Vẽ operating model FSLogix cho VDI

#### 0. Tutorial scenario

Bạn nhận bàn giao môi trường VDI có logon chậm và chưa rõ profile solution. Mục tiêu là tạo bản đồ FSLogix để helpdesk và platform team biết profile nằm ở đâu, gắn lúc nào và evidence lấy ở đâu.

#### Procedure

1. Xác nhận có dùng FSLogix không. Nếu chưa rõ, ghi `Need Customer Confirmation`.
2. Xác định container type: Profile Container, ODFC, cả hai, hoặc Cloud Cache cho một trong hai.
3. Ghi storage path: `VHDLocations` hoặc `CCDLocations`, nhưng không ghi secret hoặc path nhạy cảm nếu policy cấm.
4. Ghi delivery method cấu hình: GPO, registry, image script, MDM hoặc tool khác.
5. Ghi log/evidence path: FSLogix text logs, event logs, storage metrics, CVAD/VDI logon metrics.
6. Vẽ flow: user sign-in -> FSLogix config read -> storage access -> VHD/VHDX attach -> profile/app data available -> sign-out/detach/compaction/sync.

#### Validation

Chọn một user test và xác minh flow bằng sign-in/sign-out thật. Evidence phải cho thấy container attach, profile path đúng, app state roaming và logoff không lỗi.

#### Anti-patterns

Không coi "GPO applied" là bằng chứng đủ. Không đọc nội dung profile user khi không có approval.

### RB02 - Chọn Profile Container vs ODFC vs kết hợp

#### Procedure

1. Nếu chưa có profile solution khác, ưu tiên đánh giá Profile Container vì source mô tả nó chứa profile toàn phần.
2. Nếu đã có roaming profile khác và chỉ cần Office/Microsoft 365 cache, đánh giá ODFC Container.
3. Nếu muốn dùng cả Profile và ODFC, ghi rõ lý do vì source lưu ý dưới đa số tình huống không dùng đồng thời trừ khi có thiết kế cụ thể.
4. Đánh giá backup/restore: Profile chứa dữ liệu người dùng quan trọng hơn; ODFC nhiều dữ liệu có thể tái tạo từ remote service nhưng vẫn ảnh hưởng user experience.
5. Pilot với user thật: Outlook, Teams, OneDrive, sign-in, sign-out, profile persistence.

#### Validation

Thiết kế được chấp nhận khi user state cần giữ đã roam đúng, không double-cache dữ liệu không cần thiết, storage capacity dự báo được, và rollback về thiết kế cũ có thể thực hiện.

## CH02 - Install, Upgrade and Supportability

### Chapter Knowledge Insight Report

Install FSLogix là thay đổi image có blast radius lớn. Source nhấn mạnh package install, latest supported version và supportability. Với VDI, agent lỗi trong golden image có thể ảnh hưởng toàn pool/catalog sau rollout, nên cài đặt phải theo pilot ring và validate logon/app behavior.

### RB05 - Cài FSLogix agent trong golden image

#### Pre-install checklist

| Hạng mục | Yêu cầu |
|---|---|
| Image scope | Catalog/pool nào sẽ nhận image |
| FSLogix package | Version từ nguồn được duyệt |
| Profile design | Profile/ODFC/Cloud Cache decision đã có |
| Storage | Path, permission, capacity đã validate |
| Rollback | Snapshot/image version cũ |
| Pilot | User/machine pilot rõ ràng |

#### Procedure

1. Cài FSLogix agent vào golden image hoặc test VM theo package vendor.
2. Reboot nếu installer yêu cầu.
3. Kiểm tra FSLogix services như `frxsvc`; nếu dùng Cloud Cache, kiểm tra component liên quan `frxccds`.
4. Áp dụng cấu hình pilot bằng GPO/registry, không bật production rộng ngay.
5. Sign in bằng pilot user, kiểm tra container tạo/mount, profile path, log FSLogix.
6. Sign out, kiểm tra detach/compaction/sync nếu bật.
7. Seal/publish image theo quy trình VDI khi pilot pass.

#### Validation

FSLogix logs không có lỗi mount nghiêm trọng, user profile persistence pass, Outlook/Teams/OneDrive test theo thiết kế, logoff không treo.

#### Rollback

Revert golden image snapshot hoặc publish image cũ. Không xóa container pilot trừ khi có approval và backup nếu chứa dữ liệu cần giữ.

### RB06 - Cập nhật FSLogix agent theo pilot ring

#### Procedure

1. Xác định version hiện tại và version mới; source nêu Microsoft chỉ hỗ trợ latest version, nhưng production vẫn cần pilot.
2. Đọc release notes liên quan ODFC, Teams, redirections, Cloud Cache, compaction và sign-in/sign-out.
3. Cập nhật image pilot.
4. Test sign-in/sign-out, profile attach, ODFC app behavior, Cloud Cache provider nếu có.
5. Soak với nhóm nhỏ trước khi rollout rộng.
6. Theo dõi temporary profile, logon duration, logoff duration, app launch issue.

#### Stop conditions

Dừng rollout nếu có profile không detach, logon hang, ODFC mount failure, Teams/Outlook launch issue hoặc compaction/logoff regression.

## CH03 - Group Policy, Registry and Configuration Delivery

### Chapter Knowledge Insight Report

FSLogix đọc cấu hình per-machine qua registry/GPO. Insight thực hành: lỗi profile thường không nằm trong user data mà nằm ở cấu hình bị apply sai scope, sai path, sai precedence hoặc thay đổi không kiểm soát. GPO/registry là control plane của FSLogix.

### RB10 - Deploy FSLogix ADMX/GPO templates

#### Procedure

1. Import ADMX/ADML phù hợp vào Central Store hoặc policy management path được tổ chức duyệt.
2. Tạo GPO riêng cho FSLogix pilot, không trộn với policy rộng khó rollback.
3. Scope theo OU/security filtering để chỉ áp dụng cho VDI machines/user pilot.
4. Cấu hình container enablement, path và setting tối thiểu cần thiết.
5. Trên VDI pilot, chạy kiểm tra resultant policy/registry.
6. Sign in pilot user và đọc FSLogix log để xác nhận config được đọc.

#### Validation

Registry/policy trên máy pilot khớp thiết kế, logs ghi nhận cấu hình, container attach pass. Nếu GPO applied nhưng log không đọc đúng setting, chưa đạt.

### RB12 - Rollback GPO/registry change

#### Procedure

1. Trước change, export/screenshot GPO setting và registry state.
2. Nếu change gây lỗi, xác định setting nào mới được áp dụng và scope user/machine.
3. Disable GPO link hoặc revert setting cụ thể cho pilot trước.
4. Force refresh hoặc reboot/sign-out theo mức cần thiết.
5. Test lại sign-in/sign-out.

#### Guardrail

Không xóa user container để rollback cấu hình. Cấu hình sai phải rollback cấu hình trước, dữ liệu user là lớp khác.

## CH04 - Profile Container and Storage Path

### Chapter Knowledge Insight Report

Profile Container là điểm giao giữa Windows profile và storage. Source nêu container là VHD/VHDX chứa dữ liệu profile và có thể nằm trên SMB/cloud provider tùy cấu hình. Insight: logon thành công nghĩa là FSLogix đọc config, truy cập storage, attach disk, expose profile và detach sạch lúc sign-out.

### RB15 - Configure Profile Container

#### Pre-config checklist

| Hạng mục | Yêu cầu |
|---|---|
| Storage path | Need Customer Confirmation |
| Permissions | User create/read/write, admin/support theo least privilege |
| Capacity | Có dự báo growth và 30% free space planning |
| GPO/registry | Scope pilot |
| Backup | RPO/RTO cho profile data |

#### Procedure

1. Cấu hình Profile Container enablement và `VHDLocations` theo policy/registry được duyệt.
2. Đảm bảo storage path accessible từ VDI machine, không chỉ từ admin workstation.
3. Sign in user pilot lần đầu để tạo container.
4. Kiểm tra folder/container theo user/SID naming convention của môi trường.
5. Mở ứng dụng, thay đổi setting nhỏ, sign out.
6. Sign in lại vào máy khác/pool khác nếu cần để xác minh persistence.

#### Validation

Container tạo/mount đúng, profile setting tồn tại sau login lại, logs không có mount/permission error, sign-out detach sạch.

#### Rollback

Disable Profile Container GPO/registry cho pilot hoặc revert path/config. Không xóa container production nếu chưa có backup và approval.

### RB17 - Troubleshoot temporary profile/container fail

#### Procedure

1. Thu user, machine, timestamp, VDI pool/catalog và profile path.
2. Kiểm tra FSLogix event/text logs tại timestamp sign-in.
3. Kiểm tra storage path reachable từ VDI machine.
4. Kiểm tra share/NTFS permissions cho user và machine context nếu cần.
5. Kiểm tra VHD/VHDX lock hoặc container đang in-use do failed detach.
6. Kiểm tra free space trên share và container.
7. Nếu container corruption nghi ngờ, copy/backup trước khi repair/reset theo approval.

#### Evidence

FSLogix logs, event IDs/messages, path test result, permission export, container filename, lock file state, storage metrics.

## CH05 - ODFC, Outlook, Teams and OneDrive

### Chapter Knowledge Insight Report

ODFC Container không phải "Profile Container thứ hai" mặc định; nó tập trung Office/Microsoft 365 data khi đã có profile solution khác hoặc có nhu cầu tách cache. Source có nhiều nội dung về Outlook for Windows, Teams, OneDrive và ODFC. Insight: app issue trong VDI có thể là ODFC/cache issue chứ không phải toàn bộ profile fail.

### RB22 - Configure ODFC Container

#### Procedure

1. Xác định lý do dùng ODFC: Office data roaming khi profile solution khác đang tồn tại, hoặc thiết kế tách container có chủ đích.
2. Cấu hình ODFC enablement và storage path/Cloud Cache path theo scope pilot.
3. Đảm bảo profile solution khác loại trừ ODFC data nếu source yêu cầu tránh conflict.
4. Sign in pilot, mở Outlook/Teams/OneDrive theo test case.
5. Kiểm tra ODFC log/container creation.
6. Sign out/sign in lại để kiểm tra app state.

#### Validation

ODFC container tạo/mount đúng, app cache/state hoạt động, không duplicate/conflict với Profile Container hoặc profile solution khác.

### RB26 - Validate Teams data roaming and launch

#### Procedure

1. Xác định Teams classic hay new Teams và OS/server version.
2. Kiểm tra FSLogix version hỗ trợ Teams behavior theo release/source.
3. Sign in pilot user, launch Teams, kiểm tra app registration và user settings.
4. Sign out/sign in lại, kiểm tra Teams launch không lỗi.
5. Đọc ODFC/Profile logs nếu Teams data được redirect/roam.

#### Stop conditions

Dừng rollout nếu Teams crash/fails to start, on-demand registration fail hoặc profile creation không roam Teams data đúng.

## CH06 - Cloud Cache and HA/DR

### Chapter Knowledge Insight Report

Cloud Cache tăng khả năng dùng nhiều provider nhưng cũng tăng state machine: local cache, async provider update, unhealthy provider, merge/upload at sign-out. Source nêu không bắt buộc dùng Cloud Cache để đạt HA nếu storage provider chuẩn đã HA. Insight: Cloud Cache là thiết kế HA/DR có chi phí logoff và troubleshooting riêng.

### RB29 - Configure Cloud Cache providers

#### Pre-config checklist

| Hạng mục | Yêu cầu |
|---|---|
| Provider list | Need Customer Confirmation |
| Latency | Network path tới từng provider |
| Capacity | Local cache và remote provider capacity |
| Failure test | Một provider unavailable scenario |
| Rollback | Có path về standard VHDLocations hoặc previous CCDLocations |

#### Procedure

1. Xác định dùng Cloud Cache cho Profile, ODFC hoặc cả hai.
2. Cấu hình `CCDLocations` theo provider đã duyệt.
3. Kiểm tra mỗi provider accessible từ VDI machines.
4. Sign in pilot user, kiểm tra container attach.
5. Tạo thay đổi nhỏ trong profile/app, sign out, quan sát sync/merge.
6. Test một provider unhealthy trong lab/pilot nếu được phép, xác minh behavior và logs.

#### Validation

Provider health ổn, sign-in pass, sign-out không kéo dài quá ngưỡng chấp nhận, dữ liệu persist sau provider recovery.

### RB32 - Investigate long sign-out with Cloud Cache

#### Procedure

1. Xác nhận user dùng Cloud Cache hay standard container.
2. Thu logoff duration từ VDI/CVAD và FSLogix logs.
3. Kiểm tra Cloud Cache provider latency/health.
4. Kiểm tra compaction có bật không vì source nêu compaction với Cloud Cache kéo dữ liệu xuống local rồi upload lại provider.
5. Kiểm tra `ProfileType`/`VHDAccessMode` nếu dùng differencing/base disk modes; source cảnh báo một số mode làm sign-out xấu hơn trong bối cảnh này.
6. Pilot mitigation: review topology/latency, disable VHDCompactDisk nếu được phê duyệt, hoặc điều chỉnh Cloud Cache design.

#### Evidence

Provider list, unhealthy provider log, sign-out timestamp, compaction log, storage/network latency, user impact count.

## CH07 - redirections.xml

### Chapter Knowledge Insight Report

redirections.xml giúp giảm dữ liệu không cần thiết trong container nhưng có thể gây lỗi app hoặc không giảm container hiện hữu như kỳ vọng. Source nêu Microsoft không cung cấp recommended values chung; điều này rất quan trọng: redirections.xml là thiết kế theo môi trường, không phải copy/paste template.

### RB37 - Create redirections.xml

#### Procedure

1. Xác định mục tiêu: giảm container growth, loại cache không cần roam, hoặc xử lý app-specific path.
2. Không bắt đầu bằng template không rõ nguồn. Liệt kê từng path cần exclude/include và owner ứng dụng.
3. Kiểm tra ảnh hưởng với Outlook/Teams/OneDrive trước khi loại trừ cache.
4. Deploy cho pilot qua source folder/GPO được kiểm soát.
5. Sign in pilot, kiểm tra log có xử lý redirections.xml.
6. Test app behavior và profile persistence.

#### Validation

FSLogix log ghi nhận redirections processing, app vẫn chạy đúng, container growth giảm trong quan sát sau pilot.

### RB41 - Rollback redirections.xml safely

#### Procedure

1. Lưu version redirections.xml hiện tại.
2. Nếu app lỗi sau deploy, revert file hoặc unset source folder theo change plan.
3. Sign out/sign in để FSLogix xử lý thay đổi.
4. Kiểm tra source behavior: nếu RedirXMLSourceFolder removed/not configured, redirections.xml trong profile container được xử lý ở sign-out theo source.
5. Validate app và profile.

#### Guardrail

Không tự xóa dữ liệu trong container để "hoàn tác" redirection nếu chưa hiểu dữ liệu đã bị exclude, local redirect hay deletion-based behavior.

## CH08 - VHD/VHDX Sizing, Free Space and Compaction

### Chapter Knowledge Insight Report

Container là disk-in-file, nên capacity và compaction là vận hành storage thực sự. Source nêu cần plan ít nhất 30% free space và theo dõi warning dưới 2 GB/500 MB. Compaction xảy ra ở sign-out và có tương tác phức tạp với Cloud Cache.

### RB43 - Plan VHD/VHDX size and free space

#### Procedure

1. Xác định số user, loại container, app cache, Teams/OneDrive/Outlook, profile retention.
2. Tính capacity storage bao gồm container maximum, expected growth, snapshot/backup overhead và 30% free space planning từ source.
3. Thiết lập alert cho free space thấp, đặc biệt 2 GB và 500 MB warning.
4. Pilot với user đại diện heavy/normal/light.
5. Theo dõi container growth trong ít nhất một chu kỳ làm việc.

#### Validation

Storage không gần đầy trong logon storm, container growth nằm trong dự báo, alert hoạt động trước khi user bị ảnh hưởng.

### RB45 - Troubleshoot compaction not running

#### Procedure

1. Kiểm tra profile hoặc ODFC log files để tìm error/warning như source hướng dẫn.
2. Xác định compaction setting và threshold.
3. Kiểm tra user sign-out có hoàn tất không, có disconnected session/reconnect trong lúc compaction không.
4. Nếu dùng Cloud Cache, đánh giá thời gian download/evaluate/upload provider.
5. Không ép compaction hàng loạt trong giờ cao điểm.

#### Validation

Compaction chạy hoặc có lý do rõ vì sao không chạy; logoff duration không vượt ngưỡng chấp nhận.

## CH09 - Storage Permissions, Network and Security Exclusions

### Chapter Knowledge Insight Report

Source nhấn mạnh storage, network và antivirus/security exclusions là nền của FSLogix reliability. Insight: nhiều lỗi profile không phải lỗi FSLogix code mà là file share ACL, SMB latency, AV lock VHD/VHDX, DLP quét registry/mount point hoặc network path không ổn định.

### RB49 - Configure FSLogix AV exclusions

#### Procedure

1. Review exclusions từ source theo nhóm: executables (`frxsvc.exe`, `frxccds.exe`), log/config directories, per-user cache/temp VHD/VHDX, SMB share VHD/VHDX/lock/meta files, FSLogix registry keys và mount points.
2. Chuyển danh sách thành policy của security tooling đang dùng. Vendor AV/DLP có cú pháp riêng, ghi `Need Customer Confirmation`.
3. Deploy cho pilot VDI machines.
4. Validate bằng sign-in/sign-out, Cloud Cache sync nếu có, và kiểm tra security tool không quarantine/lock FSLogix files.
5. Theo dõi logon duration và mount errors trước/sau.

#### Security note

Exclusion không có nghĩa bỏ kiểm soát bảo mật toàn bộ share. Cần least privilege, monitoring và approval security.

### RB51 - Troubleshoot permission denied on container path

#### Procedure

1. Xác định user SID/container path và lỗi trong FSLogix log.
2. Kiểm tra share permission và NTFS permission. Không chỉ kiểm tra bằng admin account.
3. Test access từ VDI machine context/user context nếu policy cho phép.
4. Kiểm tra user có quyền create/write/modify container mới hoặc attach existing container.
5. Kiểm tra inheritance/owner nếu container đã tồn tại.
6. Sửa permission theo thiết kế, test pilot, ghi evidence.

#### Stop conditions

Không cấp Everyone Full Control để xử lý nhanh. Không đọc/copy dữ liệu profile user nếu chưa có approval.

## CH10 - Troubleshooting, Logs and Escalation

### Chapter Knowledge Insight Report

Troubleshooting FSLogix phải bắt đầu từ timestamp sign-in/sign-out và container state. Source nhắc log/event, product support, Cloud Cache PowerShell module và nhiều FAQ về logon time, compaction, redirections, OneDrive. Insight: evidence tốt phải nối user symptom với FSLogix log, storage metric, policy config và app behavior.

### RB57 - Triage slow logon

#### Procedure

1. Thu user, machine, VDI pool/catalog, timestamp, logon duration breakdown nếu có.
2. Kiểm tra FSLogix logs quanh sign-in: config read, storage path, attach/mount timing, error/warning.
3. Kiểm tra storage latency/capacity tại cùng thời điểm.
4. Kiểm tra Cloud Cache provider nếu dùng.
5. Kiểm tra container size và free space.
6. So sánh với user cùng storage path và user ở path khác để khoanh vùng.
7. Nếu storage/network bình thường, kiểm tra app/profile growth/redirections/AV lock.

#### Evidence

`fslogix-slow-logon-<user>-<date>`: FSLogix logs, event logs, storage metrics, policy config, container size, affected user count, change timeline.

### RB58 - Triage temporary profile

#### Procedure

1. Xác nhận Windows đang dùng temporary profile hay FSLogix attach fail.
2. Thu FSLogix log và event log.
3. Kiểm tra container path/permission/lock/free space.
4. Kiểm tra failed detach từ phiên trước hoặc disk in use.
5. Không xóa local/temp profile hoặc remote container ngay; backup/evidence trước.
6. Nếu cần reset/rebuild profile, yêu cầu approval vì tác động dữ liệu user.

#### Validation

User sign-in lại với profile đúng, data/settings còn theo kỳ vọng, logs không còn attach failure.

### RB65 - Build Microsoft support escalation package

#### Procedure

1. Ghi FSLogix version, OS build, VDI platform, profile/ODFC/Cloud Cache design.
2. Ghi exact symptom: slow logon, temporary profile, ODFC mount fail, sign-out hang, Teams issue.
3. Thu FSLogix logs, event logs, registry/GPO export, storage provider info, container path pattern đã che thông tin nhạy cảm.
4. Ghi timeline và change gần nhất: agent update, GPO, redirections.xml, AV policy, storage migration.
5. Ghi impact: số user, pool/catalog, workaround đã thử.
6. Nêu câu hỏi cho Microsoft: known issue, config validation, recovery path hay RCA.

#### Anti-patterns

Escalate với log thiếu timestamp; không nêu Cloud Cache/ODFC/Profile type; gửi path nhạy cảm không được che; thiếu storage metric.

## Knowledge Atoms

| Atom | Insight vận hành |
|---|---|
| Profile Container | Chứa profile state trong VHD/VHDX; attach/mount quyết định logon success |
| ODFC Container | Tập trung Microsoft 365 app data; không mặc định cần đi cùng Profile Container |
| Cloud Cache | Provider/cache layer cho HA/DR nhưng làm troubleshooting và sign-out phức tạp hơn |
| redirections.xml | Tối ưu dung lượng nhưng không có template universal; phải pilot theo app |
| VHD compaction | Diễn ra ở sign-out và có thể kéo dài khi dùng Cloud Cache |
| Storage permissions | Lỗi ACL/path là nguyên nhân phổ biến của attach fail/temporary profile |
| AV exclusions | AV/DLP lock VHD/VHDX hoặc registry/mount point có thể gây logon delay/fail |
| Logs | FSLogix text/event logs là bằng chứng chính, phải correlate timestamp với VDI platform |

## Training Conversion

| Training asset | Nội dung tạo được từ trang này |
|---|---|
| Concept explanation | Profile Container, ODFC, Cloud Cache, VHD/VHDX, redirections.xml |
| Scenario lab | Temporary profile do ACL, slow logon do storage latency, sign-out hang do Cloud Cache |
| Checklist | Pre-install, pre-GPO change, storage permission validation, AV exclusion validation |
| Troubleshooting table | Symptom-to-layer mapping: profile, storage, network, app, Cloud Cache |
| Knowledge check | Khi nào dùng ODFC, Cloud Cache có bắt buộc cho HA không, snapshot/backup profile khác gì |
| Operating model | Pilot ring, evidence pack, escalation package, rollback rules |

## Need Customer Confirmation

- Khách hàng có dùng FSLogix không? Nếu có, Profile Container, ODFC, Cloud Cache hay kết hợp?
- `VHDLocations`/`CCDLocations`, storage backend, HA/replication và backup design là gì?
- FSLogix version và image update process hiện tại?
- GPO/registry source of truth ở đâu?
- AV/DLP/security tooling nào đang áp dụng và exclusions đã được duyệt chưa?
- Monitoring có thu FSLogix logs, logon duration, storage latency, Cloud Cache provider health không?
- Quy trình reset/rebuild/copy profile container cần approval từ ai?

## Related Concepts

- [[concepts/fslogix]]
- [[concepts/profile-container]]
- [[concepts/odfc-container]]
- [[concepts/cloud-cache]]
- [[concepts/user-profile-management]]
- [[concepts/storage-permissions]]
- [[concepts/monitoring-and-logs]]
- [[concepts/backup-and-recovery]]
- [[concepts/change-management]]

## Related Sources

- [[sources/fslogix-documentation]]
- [[sources/citrix-virtual-apps-and-desktops-7-2603]]
- [[sources/citrix-virtual-apps-and-desktops-7-2603-chapter-runbook-ingest]]
- [[sources/vmware-vsphere-8-0]]
- [[sources/xenserver-8-4]]

## Self Review

- Đã lập Source Inventory, TOC extraction và Chapter Map.
- Đã chuyển 10 vùng nội dung lớn thành insight tri thức gắn với VDI operations.
- Đã trích xuất 66 runbook inventory, phủ install/config/Profile/ODFC/Cloud Cache/redirections/VHD/storage/security/troubleshooting.
- Đã viết chi tiết các runbook trọng yếu ở mức tutorial với scenario, precheck, procedure, validation, rollback/stop condition và evidence.
- Đã đánh dấu thông tin production cần xác nhận là `Need Customer Confirmation`.
