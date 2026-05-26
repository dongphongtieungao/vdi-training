---
id: source-understand-and-troubleshoot-horizon-connections
title: Understand and Troubleshoot Horizon Connections
type: source
created: 2026-05-22
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

Tài liệu này là nguồn quan trọng nhất cho luồng kết nối và troubleshooting Horizon. Nó giải thích primary protocol, secondary protocol, internal connection, external connection qua [[concepts/unified-access-gateway]], load balancer affinity, firewall, Blast/PCoIP/RDP port path, Connection Server, Horizon Agent và các lỗi phổ biến khi protocol traffic bị route sai.

Đây là source trực tiếp cho topic access flow, network operations và troubleshooting playbook. Nó không mô tả firewall rule/topology thật của khách hàng nên mọi port/path phải được xác nhận theo môi trường thực tế.

## Source Metadata

| Trường | Giá trị |
|---|---|
| Source file | `raw/sources/understand_and_troubleshoot_horizon_connections_noindex.txt` |
| Source type | Vendor troubleshooting guide |
| Platform | Omnissa Horizon 8 / Horizon Cloud connection concepts |
| Version covered | Horizon 8 theo nội dung source |
| Primary training use | Internal/external connection flow, Blast/PCoIP/RDP troubleshooting, UAG/LB/firewall evidence |
| Confidence | High for connection model; Unknown for customer network design |

## Key Claims

- Một kết nối Horizon thành công có hai giai đoạn: primary XML-API over HTTPS cho authentication/authorization/session management, sau đó secondary protocol cho display/session traffic.
- Internal connection thường đi Client -> Connection Server cho broker, rồi Client -> Horizon Agent cho secondary protocol.
- External connection thường đi Client -> Unified Access Gateway -> Connection Server cho primary protocol, rồi Client -> UAG -> Horizon Agent cho secondary protocol.
- Với external access, secondary protocol phải được route tới cùng UAG đã xử lý primary XML-API; nếu load balancer route sai, protocol session không được authorize và sẽ fail.
- Double-hop gateway không được hỗ trợ: nếu UAG đã làm gateway thì không nên bật Blast/PCoIP Secure Gateway trên Connection Server theo kiểu gây double-hop protocol traffic.

## Evidence From Source

- Source nêu Horizon Agent cho phép Connection Server quản lý machine và Horizon Client tạo protocol session tới machine.
- Source nêu Connection Server xác thực user qua Active Directory và điều hướng request tới resource.
- Source nêu UAG có thể đặt trong DMZ/internal network và làm proxy host cho kết nối tới internal resources.
- Source mô tả primary XML-API over HTTPS và secondary protocol.
- Source mô tả internal flow: Client login Connection Server, Connection Server lookup entitlement, Client connect tới Horizon Agent.
- Source mô tả external flow: Client login Connection Server qua UAG, then protocol session qua Blast Secure Gateway trên cùng UAG.
- Source cảnh báo load balancer affinity và misrouting secondary protocol là lỗi phổ biến.

## Key Architecture Knowledge

### Primary protocol

Primary protocol là bước xác thực, phân quyền và quản lý phiên. Nó thường dùng HTTPS/XML-API tới Connection Server hoặc qua UAG. Nếu primary protocol lỗi, user thường không đăng nhập được, không enumerate được pool hoặc nhận lỗi portal/broker.

### Secondary protocol

Secondary protocol là lưu lượng display/session như Blast Extreme, PCoIP hoặc RDP. Nếu secondary protocol lỗi, user có thể đăng nhập và thấy desktop nhưng launch fail, black screen, disconnect hoặc protocol timeout.

### Internal connection

Luồng điển hình:

1. Horizon Client kết nối Connection Server.
2. Connection Server xác thực user qua Active Directory và lookup entitlement.
3. Client kết nối trực tiếp Horizon Agent cho protocol session, trừ khi gateway/tunnel được bật trên Connection Server.

### External connection

Luồng điển hình:

1. Horizon Client kết nối UAG.
2. UAG chuyển primary request tới Connection Server.
3. Connection Server xác thực/entitlement.
4. Client mở secondary protocol tới cùng UAG.
5. UAG proxy protocol tới Horizon Agent.

### Load balancing và affinity

Với external flow, LB phải giữ được liên kết giữa primary và secondary protocol. Nếu secondary session bị đưa sang UAG khác, UAG đó không có authenticated session context và connection bị drop.

## Operational Knowledge

| Khu vực | Engineer cần kiểm tra | Evidence cần lưu |
|---|---|---|
| Primary protocol | DNS, certificate, HTTPS path, Connection Server auth, AD reachability | Client error, Connection Server log, certificate chain |
| Secondary protocol | Blast/PCoIP/RDP path, firewall, UAG edge service, Agent reachability | UAG log, Agent log, firewall/LB evidence |
| UAG affinity | LB persistence/source IP affinity, VIP mapping, N+1 VIP nếu có | LB config screenshot/export, UAG session mapping |
| External URL | Blast external URL, gateway settings | Horizon admin/UAG settings screenshot |
| Firewall | Required path giữa Client-UAG, UAG-Connection Server, UAG-Agent, Client-Agent internal | Firewall rule evidence, packet/log timestamp |
| Agent | Horizon Agent service, VM power state, protocol service | Agent event/log, desktop state |

## Troubleshooting Knowledge

| Triệu chứng | Nguyên nhân có thể | Lớp cần kiểm tra | Evidence | Hướng xử lý | Escalation |
|---|---|---|---|---|---|
| Login fail trước khi thấy pool | Primary HTTPS/XML-API lỗi, cert/AD/DNS/Connection Server | Client, Broker, Identity, Network | Client error, cert chain, Connection Server event | Kiểm tra URL, DNS, cert, Connection Server auth, AD | Escalate identity/network nếu lỗi nhiều user |
| Thấy desktop nhưng launch fail | Secondary protocol bị block hoặc route sai | Protocol, Firewall, UAG, Agent | UAG log, Agent log, firewall deny, client protocol error | Tách primary OK/secondary fail; kiểm tra Blast/PCoIP/RDP path | Escalate network nếu port/path bị chặn |
| External-only launch fail | UAG/LB affinity sai, external URL sai, firewall DMZ | Gateway, LB, Network | LB persistence, UAG session, Blast external URL | Đảm bảo secondary tới cùng UAG với primary | Escalate LB/network nếu cần sửa persistence |
| Internal OK, external disconnect | UAG edge service, certificate, LB, DMZ route | Gateway, Network | UAG health/log, cert, route test | Kiểm tra UAG, LB, firewall, external URL | Escalate security/network nếu path DMZ sai |
| Black screen | Protocol session thiết lập một phần, Agent/graphics/network issue | Agent, Protocol, Network, Hypervisor | Agent log, client log, host metrics | Kiểm tra secondary protocol, Agent service, VM resource | Escalate platform/network theo evidence |
| Fail sau thay đổi LB/Gateway | Persistence, VIP, certificate, external URL, double-hop | Gateway, LB, Change | Change record, before/after config | Rollback config nếu nhiều user fail | Escalate change owner nếu không có rollback rõ |

## Monitoring and Evidence

Theo dõi:

- Failed login vs failed launch để tách primary/secondary.
- External vs internal error rate.
- UAG edge service health và connection failures.
- Connection Server authentication/session errors.
- Horizon Agent unreachable count.
- Protocol disconnect trend, black screen report.
- LB persistence/session distribution.
- Certificate expiry và DNS resolution.

Evidence tối thiểu:

- User path: internal hay external.
- Thời điểm lỗi, pool, desktop, protocol đang dùng.
- Client error/screenshot.
- Connection Server log cho primary.
- UAG log cho external/secondary.
- Horizon Agent log và VM state.
- Firewall/LB evidence nếu nghi network.

## Change, Patch and Rollback Notes

Change nhạy cảm:

- UAG configuration, external URL, certificate, edge service.
- Load balancer VIP/persistence/affinity.
- Firewall rule giữa Client/UAG/Connection Server/Agent.
- Connection Server gateway/tunnel settings.
- Protocol policy như Blast/PCoIP/RDP preference.

Precheck:

- Test internal và external path trước change.
- Ghi lại URL, certificate, LB persistence, UAG mapping.
- Xác định rollback config.
- Thực hiện pilot với user test trước khi mở rộng.

Rollback:

- Revert LB persistence/VIP.
- Revert UAG config/external URL/certificate binding.
- Revert firewall rule.
- Revert Connection Server gateway setting nếu gây double-hop hoặc protocol fail.

## Backup, Recovery, HA and DR Notes

- UAG HA phụ thuộc LB và affinity; chỉ có nhiều UAG chưa đủ nếu LB route sai secondary protocol.
- Connection Server HA cần đi cùng DNS/LB, certificate và AD/DNS availability.
- DR/cutover phải kiểm thử cả primary và secondary protocol từ internal/external user.

## Security and RBAC Notes

- Gateway/firewall/certificate change cần approval từ security/network.
- Engineer cần quyền read log/config để troubleshooting nhưng quyền thay đổi UAG/LB/firewall nên giới hạn.
- Không lưu private key, password hoặc token trong evidence.

## Concepts to Create or Update

| Concept | Vì sao quan trọng | Source support |
|---|---|---|
| [[concepts/vdi-connection-flow]] | Mô hình primary/secondary | Source trực tiếp |
| [[concepts/primary-and-secondary-protocols]] | Tách lỗi login vs launch | Source trực tiếp |
| [[concepts/unified-access-gateway]] | External proxy/gateway | External flow |
| [[concepts/connection-server]] | Broker/auth/entitlement | Primary protocol |
| [[concepts/blast-extreme]] | Secondary protocol chính | Protocol troubleshooting |
| [[concepts/load-balancing]] | UAG affinity | Misrouting issue |
| [[concepts/firewall-ports]] | Network path | Internal/external port diagrams |
| [[concepts/display-protocol]] | Blast/PCoIP/RDP | Protocol session |

## Related Topic Mapping

| Topic document | Cách source này hỗ trợ |
|---|---|
| [[topics/3_Omnissa_Horizon_Architecture_Overview]] | Luồng Connection Server/UAG/Agent |
| [[topics/5_VDI_Access_Flow_Design]] | Source chính cho internal/external flow |
| [[topics/9_Network_Operations_for_VDI]] | Firewall, LB, DNS, protocol path |
| [[topics/14_Omnissa_Desktop_Pool_and_Entitlement_Guide]] | Entitlement lookup trong primary protocol |
| [[topics/18_VDI_Troubleshooting_Playbook]] | Login fail vs launch fail vs external-only fail |
| [[topics/20_VDI_Change_Management_Guide]] | UAG/LB/firewall/protocol change |
| [[topics/23_VDI_High_Availability_and_Disaster_Recovery_Guide]] | UAG/LB affinity và failover validation |
| [[topics/25_VDI_Support_and_Escalation_Guide]] | Evidence phân tuyến network/gateway/broker/agent |
| [[topics/27_VDI_Glossary_and_Concept_Dictionary]] | Primary protocol, secondary protocol, UAG, Blast |

## Need Customer Confirmation

- Internal flow của khách hàng đi trực tiếp Connection Server hay qua gateway nội bộ?
- External flow dùng bao nhiêu UAG, LB mode nào, persistence/affinity ra sao?
- Blast external URL và certificate design hiện tại?
- Firewall rule thực tế giữa Client/UAG/Connection Server/Agent?
- Protocol được phép: Blast, PCoIP, RDP hay giới hạn theo policy?
- Tool/log location để lấy UAG/Connection Server/Agent logs?

## Related Sources

- [[sources/understand-and-troubleshoot-horizon-connections-chapter-runbook-ingest]]
- [[sources/horizon-8-architecture]]
- [[sources/vdi-training-idea]]
- [[sources/vdi-documentation-list-context]]

## People

Không nêu cá nhân tác giả trong phần nguồn đã nạp.

## Open Questions

- Cần sơ đồ network thật để biến kiến thức này thành checklist production.
- Cần xác nhận load balancer vendor/config để tạo hướng dẫn kiểm tra cụ thể.
