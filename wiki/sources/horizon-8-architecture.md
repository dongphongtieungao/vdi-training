---
id: source-horizon-8-architecture
title: Horizon 8 Architecture
type: source
created: 2026-05-22
updated: 2026-05-26
authors:
  - Omnissa
year: 2026
importance: 5
urls: []
raw_paths:
  - raw/sources/horizon_8_architecture_noindex.txt
provenance: replayable
confidence: high
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

Tài liệu Horizon 8 Architecture là nguồn vendor cho kiến trúc [[concepts/omnissa-horizon]], gồm cách nhìn pod/block, Connection Server, Unified Access Gateway, Horizon Agent, desktop/application, vCenter/ESXi, identity, protocol, load balancing và các pattern triển khai. Đây là nguồn nền cho các topic về kiến trúc Horizon, access flow, pool/entitlement, hypervisor/HCI, network, HA/DR và onboarding engineer.

Source này cung cấp kiến thức kiến trúc chung. Nó không xác nhận topology thật của khách hàng, số lượng pod, số Connection Server, UAG, load balancer, HCI vendor, datastore, network path hoặc HA/DR design.

## Source Metadata

| Trường | Giá trị |
|---|---|
| Source file | `raw/sources/horizon_8_architecture_noindex.txt` |
| Source type | Vendor architecture guide |
| Platform | Omnissa Horizon 8 |
| Version covered | Horizon 8 theo tên source |
| Primary training use | Horizon architecture, component role, dependency model, design vocabulary |
| Confidence | High for vendor architecture; Unknown for customer topology |

## Key Claims

- Horizon nên được nhìn theo lớp: client/access, gateway, Connection Server, desktop/application session, identity, vCenter/hypervisor, storage, network và operation.
- Connection Server là broker/control plane: xác thực qua Active Directory, kiểm tra entitlement, điều phối resource và kết nối user với Horizon Agent.
- Unified Access Gateway là lớp reverse proxy/gateway cho external access, thường đặt tại DMZ hoặc vùng biên mạng.
- Horizon Agent là thành phần trong desktop/RDSH/physical machine, cho phép Horizon quản lý machine và thiết lập protocol session.
- vCenter/ESXi/HCI là lớp nền cho VM lifecycle, snapshot, template, pool, host, datastore và performance.

## Evidence From Source

- Source có nội dung kiến trúc về Horizon 8, các thành phần Connection Server, Unified Access Gateway, Horizon Agent, vCenter, desktop pool, entitlement, protocol và deployment pattern.
- Source liên hệ trực tiếp đến mô hình pod/block và dependency giữa Horizon control plane với hạ tầng virtualization.
- Kết hợp với source `understand_and_troubleshoot_horizon_connections` để có cả kiến trúc và luồng connection/troubleshooting.

## Key Architecture Knowledge

### User Access Layer

User dùng Horizon Client hoặc browser để đăng nhập và mở desktop/application. Lớp này chịu ảnh hưởng bởi client version, DNS, certificate trust, network reachability, MFA/identity policy nếu có và protocol configuration.

### Gateway Layer

Unified Access Gateway phục vụ external access. UAG nhận kết nối từ client bên ngoài, chuyển phần authentication/broker tới Connection Server và proxy protocol traffic tới Horizon Agent theo cấu hình gateway service.

Operational implication:

- Lỗi chỉ xảy ra từ ngoài mạng thường nằm ở UAG, load balancer, firewall, certificate, external URL hoặc routing DMZ.
- Không nên expose trực tiếp Connection Server ra Internet nếu không có thiết kế bảo mật được phê duyệt.

### Broker / Control Plane Layer

Connection Server xử lý authentication, entitlement, session management và chọn resource. Trong môi trường nhiều server, cần hiểu replication, load balancing, certificate, service health và dependency tới AD/DNS.

Operational implication:

- User login được nhưng không thấy pool: kiểm tra entitlement, AD group, pool state.
- User thấy pool nhưng launch fail: kiểm tra Horizon Agent, protocol path, desktop availability, vCenter/VM state.

### Desktop / Application Session Layer

Horizon Agent là nơi desktop/application session được thiết lập. Nếu Agent unreachable hoặc không registered, user không thể launch ổn định dù broker/gateway vẫn khỏe.

### Hypervisor / HCI Layer

Horizon phụ thuộc vCenter/ESXi/HCI để quản lý VM, snapshot, image, pool, power operation và inventory. Vấn đề host/datastore/snapshot có thể biểu hiện thành pool thiếu máy, desktop không power on, launch chậm hoặc unregistered.

## Operational Knowledge

| Khu vực | Engineer cần kiểm tra | Dấu hiệu bất thường |
|---|---|---|
| Connection Server | Service health, certificate, AD/DNS reachability, event log, replication nếu có | Login fail, entitlement lookup fail, broker không điều phối session |
| Unified Access Gateway | Appliance health, edge service, external URL, certificate, firewall, route tới Connection Server/Agent | External-only failure, protocol disconnect, certificate warning |
| Horizon Agent | Agent service, registration, VM power state, event log, protocol availability | Agent unreachable, desktop unavailable, black screen/launch fail |
| Desktop pool | Pool enabled, provisioning state, machine count, assignment, entitlement | User không thấy desktop, pool hết máy available |
| vCenter/HCI | vCenter connectivity, host state, datastore, snapshot, VM tools | Power operation fail, refresh/recompose/publish issue |
| Storage | Datastore capacity/latency, snapshot growth, image/profile storage | Login chậm, boot storm, VM stun, pool operation chậm |
| Network | DNS, firewall ports, load balancer, latency/loss | Launch fail, disconnect, protocol timeout |

## Troubleshooting Knowledge

| Triệu chứng | Nguyên nhân có thể | Lớp cần kiểm tra | Evidence | Hướng xử lý | Escalation |
|---|---|---|---|---|---|
| User không đăng nhập được | AD/DNS/certificate/Connection Server service | Identity, Broker, Network | Client error, Connection Server event, DNS test | Kiểm tra auth path, service, certificate, DC reachability | Escalate identity/network nếu nhiều user/site |
| User không thấy pool | Entitlement sai, AD group chưa cập nhật, pool disabled | Broker, Entitlement, AD | User group membership, pool entitlement screenshot | So sánh entitlement và AD group, kiểm tra pool availability | Escalate Horizon admin nếu entitlement đúng nhưng broker không enumerate |
| Launch fail | Agent unreachable, VM off, protocol path blocked, pool hết máy | Agent, Hypervisor, Network | Agent state, VM state, client error, event log | Kiểm tra VM power/Agent/service/protocol route | Escalate hypervisor/network nếu VM/path bất thường |
| External fail nhưng internal OK | UAG, external URL, LB, firewall, certificate | Gateway, Network | UAG logs, LB mapping, cert chain | Kiểm tra UAG health, URL, port, LB persistence | Escalate network/security nếu DMZ path lỗi |
| Pool operation chậm/lỗi | vCenter/HCI/datastore/snapshot issue | Hypervisor, Storage | vCenter task, datastore latency, snapshot tree | Tạm dừng rollout, kiểm tra cluster/datastore | Escalate virtualization/storage nếu ảnh hưởng rộng |

## Monitoring and Evidence

Chỉ số và evidence nên giữ trong source-to-topic retrieval:

- Connection Server service health, event/error log.
- UAG appliance health, edge service, certificate expiry, failed connections.
- Horizon Agent registered/unreachable count.
- Desktop pool available/assigned/in-use/unavailable.
- vCenter task failure, VM power operation, snapshot/publish status.
- Host CPU/memory, datastore capacity/latency, network latency/loss.
- Login duration, protocol session failures, disconnect trend.

Evidence khi xử lý:

- User, endpoint, internal/external path, pool, desktop name, timestamp.
- Error screenshot hoặc client log nếu có.
- Connection Server/UAG/Agent logs cùng timestamp.
- vCenter task/event nếu liên quan VM/pool.
- Network/firewall/LB evidence nếu lỗi theo path.

## Change, Patch and Rollback Notes

Các change liên quan Horizon architecture:

- Thêm/bớt Connection Server hoặc thay certificate.
- Thay UAG, external URL, load balancer, firewall path.
- Upgrade Horizon component hoặc Horizon Agent.
- Publish/update desktop pool image.
- Thay vCenter integration hoặc HCI/storage/network dependency.

Precheck:

- Xác định internal/external user impact.
- Kiểm tra health hiện tại của Connection Server, UAG, pools, vCenter.
- Có backup/config export/snapshot phù hợp.
- Có rollback route: certificate cũ, UAG config cũ, pool image cũ, load balancer config cũ.

## Backup, Recovery, HA and DR Notes

- HA của Horizon không chỉ là nhiều Connection Server. Cần UAG/LB, AD/DNS, vCenter, datastore, profile storage và network path cùng sẵn sàng.
- DR cần xác định pod/site behavior, pool availability, image/profile recovery, DNS cutover và user access path.
- Recovery validation phải chạy từ góc nhìn user: login, entitlement, launch, profile/app access, reconnect.

## Security and RBAC Notes

- Horizon admin quyền cao chỉ nên cấp cho platform admin; helpdesk nên có role giới hạn để xem session/machine và hỗ trợ user.
- UAG/certificate/firewall change cần approval bảo mật.
- Entitlement change phải theo AD group và audit được.
- Không lưu credential, private key hoặc cấu hình bí mật trong wiki.

## Concepts to Create or Update

| Concept | Vì sao quan trọng | Source support |
|---|---|---|
| [[concepts/omnissa-horizon]] | Nền tảng VDI Horizon | Horizon 8 architecture |
| [[concepts/connection-server]] | Broker/control plane | Architecture component |
| [[concepts/unified-access-gateway]] | External gateway/proxy | Gateway layer |
| [[concepts/pod-and-block]] | Cách tổ chức Horizon scale | Architecture vocabulary |
| [[concepts/cloud-pod-architecture]] | Multi-pod nếu có | Horizon architecture concept |
| [[concepts/vcenter-server]] | Integration với virtualization | vCenter dependency |
| [[concepts/esxi]] | Hypervisor chạy desktop VM | Infrastructure dependency |
| [[concepts/vdi-connection-flow]] | Login/launch path | Access model |
| [[concepts/high-availability]] | Multi-component HA | HA dependency |

## Related Topic Mapping

| Topic document | Cách source này hỗ trợ |
|---|---|
| [[topics/3_Omnissa_Horizon_Architecture_Overview]] | Source kiến trúc Horizon chính |
| [[topics/5_VDI_Access_Flow_Design]] | Component path: Client/UAG/Connection Server/Agent |
| [[topics/7_Hypervisor_and_HCI_Operations_Guide]] | vCenter/ESXi/HCI dependency |
| [[topics/9_Network_Operations_for_VDI]] | Gateway, LB, firewall, DNS, protocol path |
| [[topics/14_Omnissa_Desktop_Pool_and_Entitlement_Guide]] | Pool, entitlement, Agent |
| [[topics/18_VDI_Troubleshooting_Playbook]] | Phân lớp lỗi Horizon |
| [[topics/20_VDI_Change_Management_Guide]] | UAG, Connection Server, pool, certificate changes |
| [[topics/21_VDI_Patch_and_Upgrade_Guide]] | Upgrade Horizon components/Agent |
| [[topics/23_VDI_High_Availability_and_Disaster_Recovery_Guide]] | HA theo nhiều lớp |
| [[topics/27_VDI_Glossary_and_Concept_Dictionary]] | Thuật ngữ Horizon |

## Need Customer Confirmation

- Horizon version, edition và deployment model thực tế?
- Số lượng pod/block/Connection Server/UAG và vị trí đặt UAG?
- Internal users có đi qua UAG không hay trực tiếp Connection Server/LB?
- HCI platform/vendor, vCenter topology, datastore/storage design?
- HA/DR design: multi-site, Cloud Pod Architecture, DNS/LB failover?
- Monitoring tool và alert threshold cho Horizon?
- RBAC role cho helpdesk/system engineer/platform admin?

## Related Sources

- [[sources/horizon-8-architecture-chapter-runbook-ingest]]
- [[sources/understand-and-troubleshoot-horizon-connections]]
- [[sources/vmware-vsphere-8-0]]
- [[sources/vcenter-server-installation-and-setup]]
- [[sources/vdi-training-idea]]
- [[sources/vdi-documentation-list-context]]

## People

Không nêu cá nhân tác giả trong phần nguồn đã nạp.

## Open Questions

- Source architecture cần được kết hợp với sơ đồ khách hàng để tạo runbook thật.
- Cần ingest thêm tài liệu Horizon Console/Administration nếu cần chi tiết thao tác pool/image/entitlement.
