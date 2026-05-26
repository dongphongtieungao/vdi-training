---
id: source-understand-and-troubleshoot-horizon-connections-chapter-runbook-ingest
title: Understand and Troubleshoot Horizon Connections - Chapter Insight and Tutorial Runbook Ingest
type: source
created: 2026-05-26
updated: 2026-05-26
authors:
  - Omnissa
year: 2026
importance: 5
urls: []
raw_paths:
  - raw/sources/understand_and_troubleshoot_horizon_connections_noindex.txt
provenance: replayable
confidence: high
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

Trang này ingest source Understand and Troubleshoot Horizon Connections. Trọng tâm là biến mô hình primary XML-API protocol, secondary protocols, internal/external connections, UAG, load balancer affinity, Blast External URL, certificate, DNS, firewall/ports và logs thành runbook triage thực hành.

## Source Inventory

| Trường | Giá trị |
|---|---|
| Raw file | `raw/sources/understand_and_troubleshoot_horizon_connections_noindex.txt` |
| File size | 54,680 bytes |
| Source type | Troubleshooting guide |
| Product/platform | Omnissa Horizon 8 / Horizon Cloud connection flow |
| Version | Horizon 8-focused |
| Ingest mode | Chapter/major-section insight loop with tutorial runbooks |

## Chapter Knowledge Insight Report

Source này tạo insight cốt lõi cho incident response: Horizon connection không phải một kết nối duy nhất. Nó có phase primary XML-API qua HTTPS cho authentication/authorization/session management, rồi phase secondary protocol cho Blast/PCoIP/RDP. Vì vậy câu hỏi đầu tiên trong mọi incident phải là: user fail ở authentication, resource launch hay secondary protocol path?

## Central Knowledge Thesis

**Thesis:** Troubleshooting Horizon hiệu quả bắt đầu bằng tách primary protocol khỏi secondary protocol. Nếu user chưa authenticate/enumerate, kiểm tra client-to-UAG/Connection Server, identity, DNS, certificate và load balancer XML-API. Nếu user authenticate được nhưng launch/protocol fail, kiểm tra UAG affinity, Blast External URL, firewall ports, WebSockets, UAG-to-Agent path, Agent-to-Connection Server state và gateway/tunnel configuration. Khi không tách phase, engineer sẽ sửa nhầm lớp và kéo dài MTTR.

## Insight and Depth Control

| Trường | Giá trị |
|---|---|
| Required insight sections completed | Yes |
| Required technical sections completed | Yes |
| Chapter report thesis present | Yes |
| Runbook best practices extracted | Yes |
| Runbooks are actionable | Yes |
| Source-backed vs inference separated | Yes |
| Depth Exception | Source contains troubleshooting procedures rather than install workflow; runbooks focus on triage/config validation |

## Table of Contents Extracted

| Chapter | Title | Source locator | Priority |
|---|---|---|---|
| CH01 | Understanding Horizon connections | Lines 124-178 | High |
| CH02 | Primary and secondary protocols | Lines 180-236 | High |
| CH03 | Internal connection network ports | Lines 237-276 | High |
| CH04 | External connections through UAG | Lines 280-336 | High |
| CH05 | External network ports | Lines 336-368 | High |
| CH06 | UAG and Connection Server architecture | Lines 378-388 | High |
| CH07 | Troubleshooting sequence | Lines 399-456 | High |
| CH08 | Horizon Client to UAG troubleshooting | Lines 466-567 | High |
| CH09 | Third-party auth, UAG to CS, DNS and Agent path | Lines 608+ and TOC lines 82-100 | High |
| CH10 | Horizon Web Client connections | TOC lines 100-104 | Medium |

## Runbook Best Practices Extracted

### Runbook Source Coverage

| Source subsection / heading | Operational content found | Runbook mapping | Coverage status | Nếu chưa tạo runbook, lý do |
|---|---|---|---|---|
| Horizon components | Client, Agent, Connection Server, UAG | HZ-CONN-RB01 | Covered | N/A |
| Primary/secondary protocols | XML-API vs Blast/PCoIP/RDP | HZ-CONN-RB02-RB04 | Covered | N/A |
| Internal connection ports | Direct client-to-CS and client-to-Agent paths | HZ-CONN-RB05-RB06 | Covered | N/A |
| External UAG path | Client-to-UAG-to-CS and protocol via same UAG | HZ-CONN-RB07-RB10 | Covered | N/A |
| LB affinity and misrouting | Secondary protocol must hit same UAG | HZ-CONN-RB11-RB13 | Covered | N/A |
| Blast External URL | URL/port/certificate validation | HZ-CONN-RB14-RB16 | Covered | N/A |
| Certificates and curl/browser tests | TLS evidence | HZ-CONN-RB17-RB18 | Covered | N/A |
| Test-NetConnection/tcpdump | Network evidence | HZ-CONN-RB19-RB20 | Covered | N/A |
| UAG to auth source / DNS | Third-party auth and name resolution | HZ-CONN-RB21-RB23 | Covered | N/A |
| UAG to Connection Server / Agent | Target URL, routing, Agent path | HZ-CONN-RB24-RB27 | Covered | N/A |
| Horizon Web Client | HTML Access/Blast Secure Gateway | HZ-CONN-RB28-RB29 | Covered | N/A |

### Mandatory Installation and Configuration Runbooks

| Source procedure / config heading | Procedure type | Runbook required? | Runbook ID | Nếu không tạo, lý do |
|---|---|---|---|---|
| Configure UAG external connection path | Configure / Validate | Yes | HZ-CONN-RB07 | N/A |
| Configure load balancer affinity | Configure | Yes | HZ-CONN-RB11 | N/A |
| Configure Blast External URL | Configure | Yes | HZ-CONN-RB14 | N/A |
| Configure certificate consistency | Configure / Security | Yes | HZ-CONN-RB17 | N/A |
| Configure firewall ports | Configure / Network | Yes | HZ-CONN-RB05, RB08 | N/A |
| Configure third-party auth path | Configure / Identity | Yes | HZ-CONN-RB21 | N/A |
| Validate WebSockets / tcpdump / Test-NetConnection | Troubleshoot / Evidence | Yes | HZ-CONN-RB19, RB20 | N/A |

### Runbook Inventory

| Runbook ID | Family | Tên runbook | Dùng khi nào | Owner | Risk | Source locator |
|---|---|---|---|---|---|---|
| HZ-CONN-RB01 | Foundation | Vẽ Horizon connection map | Onboarding/incident | System Engineer | Low | Components |
| HZ-CONN-RB02 | Triage | Tách authentication fail khỏi protocol fail | Incident | Helpdesk/System Engineer | Medium | Lines 180-189 |
| HZ-CONN-RB03 | Triage | Triage internal direct connection | Incident | System Engineer | Medium | Lines 196-235 |
| HZ-CONN-RB04 | Triage | Triage tunneled-through-Connection-Server design | Incident/design | Architect | High | Lines 204-215 |
| HZ-CONN-RB05 | Network | Validate internal Blast/PCoIP/RDP ports | Pre-change/incident | Network + VDI | Medium | Lines 237-276 |
| HZ-CONN-RB06 | Network | Validate UDP bidirectional/stateful firewall | Incident | Network | Medium | Lines 248, 346 |
| HZ-CONN-RB07 | UAG | Validate external UAG connection path | Incident | VDI + Network | High | Lines 280-308 |
| HZ-CONN-RB08 | Network | Validate external Blast/PCoIP/RDP ports | Incident | Network + VDI | High | Lines 336-368 |
| HZ-CONN-RB09 | UAG | Prevent double-hop gateway misconfiguration | Design/review | VDI Architect | High | Lines 286-288 |
| HZ-CONN-RB10 | UAG | Validate same-UAG primary/secondary path | Incident | VDI + LB | High | Lines 313-320 |
| HZ-CONN-RB11 | LB | Configure LB affinity for UAG | Build/change | Network | High | Lines 322-333 |
| HZ-CONN-RB12 | LB | Triage secondary protocol misrouting | Incident | Network + VDI | High | Lines 490-507 |
| HZ-CONN-RB13 | LB | Validate WebSockets through LB | Incident | Network | Medium | Lines 512-515 |
| HZ-CONN-RB14 | Blast | Validate Blast External URL | Incident/change | VDI Admin | High | Lines 518-527 |
| HZ-CONN-RB15 | Blast | Choose Blast TCP 443 vs 8443 exposure | Design | Architect + Security | Medium | Lines 482-485 |
| HZ-CONN-RB16 | Blast | Analyze bsg.log timeout | Incident | VDI Admin | Medium | Lines 471-497 |
| HZ-CONN-RB17 | Certificate | Validate UAG/LB TLS certificate | Incident/change | Security + VDI | High | Lines 531-554 |
| HZ-CONN-RB18 | Certificate | Collect curl/browser certificate evidence | Incident | System Engineer | Low | Lines 545-554 |
| HZ-CONN-RB19 | Network | Run Test-NetConnection evidence from Windows client | Incident | Helpdesk/Network | Low | Lines 558-567 |
| HZ-CONN-RB20 | Network | Capture tcpdump on UAG for protocol ports | Incident | VDI Admin | Medium | Lines 592-598 |
| HZ-CONN-RB21 | Identity | Validate UAG to RADIUS/RSA/third-party auth | Incident | Identity + VDI | High | Lines 608-638 |
| HZ-CONN-RB22 | DNS | Triage UAG DNS/name resolution issue | Incident | Network + VDI | Medium | TOC 86 |
| HZ-CONN-RB23 | CS | Validate UAG to Connection Server URL | Incident | VDI Admin | High | TOC 82 |
| HZ-CONN-RB24 | Agent | Validate UAG to Horizon Agent path | Incident | VDI + Network | High | TOC 88 |
| HZ-CONN-RB25 | Agent | Triage Agent-to-Connection Server state | Incident | VDI Admin | Medium | Lines 421-422 |
| HZ-CONN-RB26 | Config | Triage Connection Server misconfiguration | Incident | VDI Admin | High | TOC 96 |
| HZ-CONN-RB27 | Escalation | Build Horizon connection escalation package | Escalation | System Engineer | Low | Whole source |
| HZ-CONN-RB28 | Web Client | Validate Horizon Web Client path | Incident | VDI Admin | Medium | TOC 100-104 |
| HZ-CONN-RB29 | Training | Lab: identify broken phase from symptom | Training | Trainer | Low | Whole source |

### HZ-CONN-RB02 - Tách authentication fail khỏi protocol fail

#### Procedure

1. Hỏi user có login được Horizon Client/Web Client không. Nếu không login được, đây là primary XML-API/authentication path.
2. Nếu login được, hỏi user có thấy resource/desktop/app không. Nếu không thấy, kiểm tra entitlement/Connection Server, không nhảy sang UAG protocol ngay.
3. Nếu thấy resource nhưng launch timeout/black screen/disconnect, chuyển sang secondary protocol path: Blast/PCoIP/RDP.
4. Xác định user internal hay external. External thêm UAG/LB/certificate/Blast External URL vào scope.
5. Ghi phase vào ticket: `primary-auth`, `enumeration`, `secondary-protocol`, hoặc `session-quality`.

#### Validation

Ticket có phase rõ, component scope rõ và evidence phù hợp. Đây là bước giảm MTTR quan trọng nhất.

### HZ-CONN-RB11 - Configure LB affinity for UAG

#### Procedure

1. Xác nhận primary XML-API và secondary protocol có đi qua cùng load balancer hay dùng N+1 VIP/direct protocol VIP.
2. Nếu cả primary và secondary qua LB, cấu hình source IP affinity hoặc cơ chế tương đương để toàn bộ session đi tới cùng UAG.
3. Timeout/persistence phải bao phủ duration session mặc định/thiết kế; source nêu default maximum 10 hours cho session affinity context.
4. Test external login và launch nhiều lần từ cùng client; xác nhận UAG nhận primary và secondary cùng appliance.
5. Nếu Blast fail, đọc `bsg.log` trên UAG để xem secondary session không tới đúng UAG hay bị timeout.

#### Rollback

Revert LB config về bản đã lưu hoặc route pilot user tới dedicated UAG VIP. Không đổi đồng thời certificate, URL và affinity trong cùng incident nếu chưa có change control.

### HZ-CONN-RB14 - Validate Blast External URL

#### Procedure

1. Mở cấu hình UAG và ghi `blastExternalUrl`.
2. Kiểm tra URL/port đó có reachable từ client external. Source nêu valid ports thường là 8443 hoặc 443 tùy cấu hình.
3. Kiểm tra certificate name/SAN khớp hostname public/LB/UAG.
4. Test Blast launch; nếu fail, kiểm tra `bsg.log` và network path port tương ứng.
5. Nếu LB TLS offload/re-encryption, đảm bảo certificate nhất quán giữa LB và UAG theo source.

#### Evidence

blastExternalUrl value, DNS resolution, Test-NetConnection/curl/browser certificate screenshot, bsg.log timestamp, client error.

### HZ-CONN-RB20 - Capture tcpdump on UAG for protocol ports

#### Procedure

1. Xác định protocol/port cần quan sát: 443, 8443, UDP 8443, 4172 tùy Blast/PCoIP.
2. Chạy capture ngắn trong window tái hiện lỗi. Không capture quá lâu hoặc chứa dữ liệu ngoài phạm vi.
3. Đồng thời yêu cầu user tái hiện launch.
4. Kiểm tra có packet tới UAG không, có reply không, và có đi tiếp tới Agent/Connection Server theo phase không.
5. Lưu capture/log theo incident ID và hạn chế quyền truy cập.

#### Stop conditions

Dừng capture nếu chứa traffic nhạy cảm ngoài phạm vi hoặc chưa được phê duyệt trong production.

## Knowledge Atoms

| Atom | Insight vận hành |
|---|---|
| Primary protocol | HTTPS XML-API cho auth/authorization/session management |
| Secondary protocol | Blast/PCoIP/RDP cho protocol session |
| Same UAG | External secondary protocol phải đến cùng UAG đã authenticate |
| Blast External URL | Client dùng URL/port này để đi vào Blast qua UAG |
| WebSockets | Blast phụ thuộc WebSockets; LB có thể block |
| bsg.log | Evidence quan trọng khi Blast qua UAG timeout/drop |

## Related Concepts

- [[concepts/vdi-connection-flow]]
- [[concepts/primary-and-secondary-protocols]]
- [[concepts/unified-access-gateway]]
- [[concepts/connection-server]]
- [[concepts/firewall-ports]]
- [[concepts/load-balancing]]
- [[concepts/certificate-management]]

## Related Sources

- [[sources/understand-and-troubleshoot-horizon-connections]]
- [[sources/horizon-8-architecture]]

## Self Review

- Đã chuyển troubleshooting guide thành runbook theo phase primary/secondary.
- Đã phủ UAG, LB affinity, Blast External URL, certificate, port, tcpdump/Test-NetConnection và escalation package.
