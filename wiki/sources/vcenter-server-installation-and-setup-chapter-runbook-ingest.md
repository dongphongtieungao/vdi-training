---
id: source-vcenter-server-installation-and-setup-chapter-runbook-ingest
title: vCenter Server Installation and Setup - Chapter Insight and Tutorial Runbook Ingest
type: source
created: 2026-05-26
updated: 2026-05-26
authors:
  - VMware
year: 2026
importance: 5
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

Trang này ingest source vCenter Server Installation and Setup 8.0.2. Đây là nguồn có nhiều procedure cài đặt/cấu hình trực tiếp: requirements, DNS/NTP/ports, GUI deployment Stage 1/Stage 2, CLI deployment JSON, file-based backup/restore, image-based backup/restore, post-deploy login/plugin, domain repoint và log/support bundle troubleshooting.

## Source Inventory

| Trường | Giá trị |
|---|---|
| Raw file | `raw/sources/vsphere-vcenter-802-installation-guide.txt` |
| File size | 248,080 bytes |
| Source type | Vendor installation and setup guide |
| Product/platform | VMware vCenter Server 8.0 / vCenter Server Appliance |
| Version | 8.0.2 source filename |
| Ingest mode | Chapter/major-section insight loop with tutorial runbooks |

## Chapter Knowledge Insight Report

vCenter deployment là control-plane bootstrap của vSphere. Với VDI, vCenter lỗi hoặc deploy sai sizing/DNS/NTP/SSO sẽ ảnh hưởng host inventory, provisioning, image operations, monitoring và recovery. Source này phải được chuyển thành runbook triển khai có precheck, Stage 1/Stage 2 validation, CLI repeatability, backup/restore drill và troubleshooting evidence.

## Central Knowledge Thesis

**Thesis:** vCenter Server Appliance deployment không phải thao tác OVA đơn lẻ mà là quá trình tạo identity, database, service, certificate, SSO domain và management endpoint cho toàn bộ vSphere estate. Nếu DNS, NTP, sizing, ports, SSO domain, storage hoặc backup plan sai, lỗi có thể không lộ ngay ở Stage 1 nhưng sẽ xuất hiện khi thêm host, dùng Enhanced Linked Mode, chạy lifecycle operation hoặc restore. Vì vậy install runbook phải kiểm chứng cả deployment state và operational readiness sau login.

## Insight and Depth Control

| Trường | Giá trị |
|---|---|
| Required insight sections completed | Yes |
| Required technical sections completed | Yes |
| Chapter report thesis present | Yes |
| Runbook best practices extracted | Yes |
| Runbooks are actionable | Yes |
| Source-backed vs inference separated | Yes |
| Depth Exception | Exact JSON values/passwords/customer FQDN are customer-specific; marked Need Customer Confirmation |

## Table of Contents Extracted

| Chapter | Title | Source locator | Priority |
|---|---|---|---|
| CH01 | Introduction, workflow, components and VCSA | Lines 205-639 | High |
| CH02 | System requirements, ports, DNS and preparation | Lines 727-1003 plus TOC 56-82 | High |
| CH03 | GUI deployment Stage 1/Stage 2 | TOC lines 84-92 | High |
| CH04 | CLI deployment and JSON templates | TOC lines 94-106 | High |
| CH05 | File-based backup and restore | TOC lines 114-126 | High |
| CH06 | Image-based backup and restore | TOC lines 128-134 | High |
| CH07 | After deployment, login, plugin, repoint | TOC lines 138-157 | Medium |
| CH08 | Troubleshooting logs and support bundle | TOC lines 159-167 | High |

## Runbook Best Practices Extracted

### Runbook Source Coverage

| Source subsection / heading | Operational content found | Runbook mapping | Coverage status | Nếu chưa tạo runbook, lý do |
|---|---|---|---|---|
| How to Install and Set Up vSphere | ESXi -> vCenter -> inventory workflow | VC-RB01-RB02 | Covered | N/A |
| vCenter components/services | SSO, VMCA, PostgreSQL, vSphere Client, Auto Deploy, Dump Collector | VC-RB03-RB04 | Covered | N/A |
| VCSA requirements | hardware, storage, software, ports, DNS, time | VC-RB05-RB10 | Covered | N/A |
| Preparing deployment | installer system, download/mount, prerequisites | VC-RB11-RB12 | Covered | N/A |
| GUI deployment | required info, Stage 1 OVA, Stage 2 setup | VC-RB13-RB16 | Covered | N/A |
| CLI deployment | JSON templates, parameters, syntax, multiple appliances | VC-RB17-RB20 | Covered | N/A |
| File-based backup/restore | manual backup, restore Stage 1/Stage 2 | VC-RB21-RB24 | Covered | N/A |
| Image-based backup/restore | image restore | VC-RB25-RB26 | Covered | N/A |
| After deploy | login, Enhanced Authentication Plug-in, repoint | VC-RB27-RB30 | Covered | N/A |
| Troubleshooting | collect logs, deployment logs, support bundle | VC-RB31-RB34 | Covered | N/A |

### Mandatory Installation and Configuration Runbooks

| Source procedure / config heading | Procedure type | Runbook required? | Runbook ID | Nếu không tạo, lý do |
|---|---|---|---|---|
| Deploy VCSA by GUI | Install / Deploy | Yes | VC-RB13-RB16 | N/A |
| Deploy VCSA by CLI | Install / Deploy / Automation | Yes | VC-RB17-RB20 | N/A |
| Prepare DNS/NTP/ports | Prepare / Configure | Yes | VC-RB05-RB10 | N/A |
| Configure SSO domain and ELM decision | Configure / Identity | Yes | VC-RB03, RB18 | N/A |
| File-based backup | Backup | Yes | VC-RB21 | N/A |
| File-based restore | Restore | Yes | VC-RB22-RB24 | N/A |
| Image-based restore | Restore | Yes | VC-RB25-RB26 | N/A |
| Repoint vCenter domain | Reconfigure / Migrate | Yes | VC-RB29-RB30 | N/A |
| Collect logs/support bundle | Troubleshoot / Escalate | Yes | VC-RB31-RB34 | N/A |

### Runbook Inventory

| Runbook ID | Family | Tên runbook | Dùng khi nào | Owner | Risk | Source locator |
|---|---|---|---|---|---|---|
| VC-RB01 | Architecture | Map vSphere install workflow | Onboarding | System Engineer | Low | Lines 234-327 |
| VC-RB02 | Readiness | Verify ESXi readiness before VCSA | Pre-install | Platform Admin | Medium | Workflow |
| VC-RB03 | Identity | Decide SSO domain and Enhanced Linked Mode | Design | Architect | High | Lines 559-628 |
| VC-RB04 | Services | Validate vCenter services and embedded PSC model | Post-install | Platform Admin | Medium | Components/services |
| VC-RB05 | Sizing | Choose VCSA size/storage size | Design | Architect | High | Lines 535-537, 856-950 |
| VC-RB06 | DNS | Validate DNS forward/reverse for VCSA | Pre-install | Network + Platform | High | Lines 838-850 |
| VC-RB07 | Time | Validate NTP/time sync | Pre-install | Platform Admin | High | Lines 850+ |
| VC-RB08 | Network | Validate vCenter required ports/firewall | Pre-install | Network + Platform | High | Lines 972-1003 |
| VC-RB09 | Installer | Prepare installer workstation and ISO mount | Pre-install | Platform Admin | Low | TOC 72-80 |
| VC-RB10 | Prereq | Build deployment information worksheet | Pre-install | Platform Admin | Medium | Required info |
| VC-RB11 | Security | Protect deployment credentials and certificates | Pre-install | Security + Platform | High | Components/VMCA |
| VC-RB12 | Change | Pre-change checklist for new VCSA | Change | Platform Admin | Medium | Deployment |
| VC-RB13 | GUI | Stage 1 deploy OVA via GUI | Install | Platform Admin | High | TOC 88-92 |
| VC-RB14 | GUI | Stage 2 setup VCSA via GUI | Install | Platform Admin | High | TOC 90-92 |
| VC-RB15 | Validation | Post-GUI deployment validation | Post-install | Platform Admin | High | After deploy |
| VC-RB16 | Rollback | Rollback failed GUI deployment | Recovery | Platform Admin | High | Troubleshooting |
| VC-RB17 | CLI | Prepare JSON for CLI deployment | Automation | Platform Admin | High | TOC 96-100 |
| VC-RB18 | CLI | Review CLI parameters and secrets | Automation | Security + Platform | High | Deployment parameters |
| VC-RB19 | CLI | Deploy VCSA using CLI | Install/automation | Platform Admin | High | TOC 102-104 |
| VC-RB20 | CLI | Deploy multiple VCSA using CLI | Multi-site/ELM | Architect | High | TOC 106 |
| VC-RB21 | Backup | Manual file-based backup | Scheduled/pre-change | Platform Admin | Medium | TOC 120 |
| VC-RB22 | Restore | File-based restore Stage 1 appliance | Recovery | Platform Admin | High | TOC 122-126 |
| VC-RB23 | Restore | File-based restore Stage 2 data transfer | Recovery | Platform Admin | High | TOC 126 |
| VC-RB24 | DR | Validate restored vCenter for VDI/vSphere operations | DR test | Platform Admin | High | Backup/restore |
| VC-RB25 | Backup | Image-based backup strategy | Backup design | Backup + Platform | Medium | Chapter 4 |
| VC-RB26 | Restore | Restore image-based vCenter environment | Recovery | Platform Admin | High | TOC 132-134 |
| VC-RB27 | PostDeploy | Login to vCenter and verify inventory | Post-install | Platform Admin | Medium | TOC 140 |
| VC-RB28 | Plugin | Install Enhanced Authentication Plug-in | Configure | System Engineer | Low | TOC 142 |
| VC-RB29 | Repoint | Repoint vCenter to another SSO domain | Migration | Architect | High | TOC 144-157 |
| VC-RB30 | License | Validate repoint license considerations | Migration | Platform Admin | Medium | TOC 157 |
| VC-RB31 | Logs | Retrieve installation logs manually | Troubleshooting | Platform Admin | Low | TOC 161-163 |
| VC-RB32 | Logs | Collect deployment log files | Troubleshooting | Platform Admin | Low | TOC 165 |
| VC-RB33 | Support | Export support bundle | Escalation | Platform Admin | Low | TOC 167 |
| VC-RB34 | Incident | Triage failed VCSA deployment | Incident | Platform Admin | High | Chapter 6 |

### VC-RB06 - Validate DNS forward/reverse for VCSA

#### Tutorial scenario

Bạn chuẩn bị deploy VCSA mới cho môi trường VDI/vSphere. Source nhấn mạnh DNS và network client/deployment target phải dùng DNS phù hợp; lỗi DNS có thể làm SSO, certificate, ELM và host management lỗi sau deployment.

#### Procedure

1. Xác định FQDN chính thức của VCSA. Ghi `Need Customer Confirmation` nếu chưa có naming standard.
2. Tạo/kiểm tra forward DNS record và reverse PTR.
3. Từ installer workstation, ESXi host target và network quản trị, resolve FQDN/IP hai chiều.
4. Kiểm tra không trùng hostname/IP với appliance cũ.
5. Lưu output/screenshot DNS lookup vào change record.

#### Validation

FQDN resolve đúng từ mọi điểm liên quan, reverse lookup khớp, không có mismatch certificate naming. Dừng deploy nếu DNS chưa ổn.

### VC-RB13 - Stage 1 deploy OVA via GUI

#### Procedure

1. Mở installer từ ISO trên workstation hỗ trợ.
2. Chọn Deploy vCenter Server Appliance và nhập target ESXi/vCenter, datastore, network, appliance size/storage size theo worksheet.
3. Kiểm tra lại IP/FQDN/DNS/gateway/NTP trước khi bắt đầu. Stage 1 sai thường dẫn đến Stage 2 hoặc post-install lỗi.
4. Deploy OVA và theo dõi task.
5. Khi Stage 1 hoàn tất, kiểm tra VM appliance power state, console basic health và network reachability.

#### Rollback

Nếu Stage 1 fail, không reuse half-deployed VM. Thu log, xóa appliance artifact theo change approval, sửa nguyên nhân và deploy lại sạch.

### VC-RB14 - Stage 2 setup VCSA via GUI

#### Procedure

1. Chạy Stage 2 chỉ sau khi Stage 1 appliance reachable.
2. Cấu hình SSO domain, administrator password, time sync/NTP, CEIP nếu policy yêu cầu.
3. Nếu tham gia Enhanced Linked Mode, xác nhận replication partner/domain design trước khi nhập.
4. Theo dõi setup service; nếu fail, thu deployment log.
5. Sau Stage 2, login vSphere Client bằng SSO admin và kiểm tra services.

#### Validation

Login thành công, services healthy, certificate/SSO không lỗi, inventory có thể thêm host, backup plan đã lên lịch.

### VC-RB17 - Prepare JSON for CLI deployment

#### Procedure

1. Chọn JSON template phù hợp: embedded VCSA on ESXi/vCenter hoặc replication/ELM variant theo source.
2. Điền parameter từ deployment worksheet: target, VM name, datastore, network, IP/FQDN, DNS, NTP, SSO domain, size.
3. Không lưu password trong repo/wiki. Dùng secure handling theo policy.
4. Validate JSON syntax và peer review trước khi chạy.
5. Lưu bản sanitized JSON làm evidence, che secrets.

#### Validation

JSON parse được, parameter khớp design, secrets không lộ, rollback plan rõ.

### VC-RB21 - Manual file-based backup

#### Procedure

1. Mở vCenter Server Management Interface.
2. Xác định backup destination, protocol, credential, encryption/retention theo policy.
3. Chạy manual backup trước change lớn hoặc theo lịch.
4. Ghi backup timestamp, size, target và result.
5. Không coi backup đạt nếu chưa có restore test định kỳ.

#### Validation

Backup job success, artifact tồn tại, có checksum/size hợp lý, credential/target được bảo vệ.

### VC-RB22 - File-based restore Stage 1 appliance

#### Procedure

1. Xác định backup cần restore, version/build compatibility và outage window.
2. Chạy restore wizard Stage 1 để deploy appliance mới.
3. Dùng DNS/IP theo recovery plan; tránh conflict với appliance cũ còn online.
4. Kiểm tra appliance mới reachable sau Stage 1.

#### Stop conditions

Dừng nếu backup version không phù hợp, DNS conflict, storage target không đủ hoặc chưa có approval DR.

### VC-RB31 - Retrieve installation logs manually

#### Procedure

1. Xác định deployment fail ở Stage 1, Stage 2, CLI parse, network, SSO hay service setup.
2. Thu installer logs từ workstation và appliance/deployment logs theo source chapter troubleshooting.
3. Lưu log theo incident/change ID.
4. Không retry nhiều lần khi chưa đọc lỗi đầu tiên; retry có thể ghi đè hoặc làm nhiễu evidence.
5. Nếu escalation, kèm worksheet, JSON sanitized, DNS/NTP/port evidence và task screenshots.

## Knowledge Atoms

| Atom | Insight vận hành |
|---|---|
| Stage 1 vs Stage 2 | OVA deployment khác với setup identity/service/database |
| DNS/NTP | Dependency nền cho SSO, certificate và ELM |
| SSO domain | Identity boundary cần quyết định trước deploy |
| VCSA sizing | Phụ thuộc environment size và database/storage requirement |
| File-based backup | Native recovery path cần restore drill |
| CLI JSON | Repeatability mạnh nhưng cần secret handling và peer review |

## Related Concepts

- [[concepts/vcenter-server-appliance]]
- [[concepts/vcenter-server]]
- [[concepts/dns-and-time-sync]]
- [[concepts/enhanced-linked-mode]]
- [[concepts/backup-and-recovery]]
- [[concepts/certificate-management]]
- [[concepts/lifecycle-management]]

## Related Sources

- [[sources/vcenter-server-installation-and-setup]]
- [[sources/vmware-vsphere-8-0-part-03-vcenter-install-upgrade]]
- [[sources/vmware-vsphere-8-0]]

## Self Review

- Đã phủ đầy đủ workflow install/config/backup/restore/troubleshooting chính từ source.
- Runbook có precheck, procedure, validation, rollback/evidence cho GUI, CLI, DNS/NTP/ports, backup/restore và logs.
