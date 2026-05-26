---
id: source-horizon-8-architecture-chapter-runbook-ingest
title: Horizon 8 Architecture - Chapter Insight and Tutorial Runbook Ingest
type: source
created: 2026-05-26
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

Trang này ingest source Horizon 8 Architecture theo chuẩn `chapter-ingest-loop.prompt`. Trọng tâm không phải là vẽ lại kiến trúc, mà là biến các phần Connection Server, load balancing, pod/block, Cloud Pod Architecture, Unified Access Gateway, DMZ, Horizon Cloud, True SSO và vCenter/Nutanix considerations thành insight vận hành và runbook thiết kế/kiểm chứng.

## Source Inventory

| Trường | Giá trị |
|---|---|
| Raw file | `raw/sources/horizon_8_architecture_noindex.txt` |
| File size | 124,762 bytes |
| Source type | Reference architecture / design guide |
| Product/platform | Omnissa Horizon 8 |
| Version | Horizon 8 |
| Ingest mode | Chapter/major-section insight loop with tutorial runbooks |

## Chapter Knowledge Insight Report

Horizon 8 Architecture dạy engineer nhìn Horizon như một chuỗi brokered access có hai lớp: control plane cho authentication/entitlement/broker và protocol data path cho Blast/PCoIP/RDP. Insight quan trọng của source là không được scale Horizon bằng cách thêm máy tùy hứng; phải dùng pod/block, Connection Server n+1, load balancer persistence, UAG edge design, CPA federation và hypervisor manager boundary để giới hạn blast radius.

## Central Knowledge Thesis

**Thesis:** Trong môi trường VDI quy mô lớn, Horizon 8 phải được thiết kế theo boundary lặp lại: Connection Server chịu session brokering, resource block chịu compute capacity, UAG chịu external edge, CPA chịu federation giữa pod, còn vCenter/hypervisor manager là delimiter của resource block. Khi một boundary bị kéo căng hoặc đặt sai, lỗi sẽ biểu hiện thành authentication fail, resource không launch, session mất đường protocol, hoặc outage lan rộng. Vì vậy mọi thiết kế/kiểm chứng phải map user journey sang đúng boundary và có evidence capacity/HA rõ ràng.

## Insight and Depth Control

| Trường | Giá trị |
|---|---|
| Required insight sections completed | Yes |
| Required technical sections completed | Yes |
| Chapter report thesis present | Yes |
| Runbook best practices extracted | Yes |
| Runbooks are actionable | Yes |
| Source-backed vs inference separated | Yes |
| Depth Exception | Source là architecture guide, không phải step-by-step installer; runbooks là design validation và operational verification derived from source |

## Table of Contents Extracted

| Chapter | Title | Source locator | Priority |
|---|---|---|---|
| CH01 | Core Horizon components and connection flow | Lines 253-327 | High |
| CH02 | Connection Server scalability and load balancing | Lines 368-431 | High |
| CH03 | Pod and block design | Lines 441-550 | High |
| CH04 | Cloud Pod Architecture | Lines 552-586 | High |
| CH05 | Unified Access Gateway, DMZ and external access | Lines 597-658 | High |
| CH06 | Horizon Cloud / Edge Gateway | TOC lines 70-74 | Medium |
| CH07 | True SSO and Enrollment Server | TOC lines 82-94 | High |
| CH08 | vSphere/vCenter and Nutanix considerations | TOC lines 142-182 | High |
| CH09 | Multi-site and unsupported stretched pod considerations | TOC lines 132-134 | High |

## Runbook Best Practices Extracted

### Runbook Source Coverage

| Source subsection / heading | Operational content found | Runbook mapping | Coverage status | Nếu chưa tạo runbook, lý do |
|---|---|---|---|---|
| Horizon core components | Client, Connection Server, Agent, UAG, Console, events DB | HZ-ARCH-RB01-RB03 | Covered | N/A |
| Connection Server scale | 4,000 sessions/server, 2,000 when tunneled, 7 servers/pod, 20,000 sessions/pod | HZ-ARCH-RB04-RB06 | Covered | N/A |
| Load balancing Connection Servers | Persistence, health monitoring, central namespace | HZ-ARCH-RB07-RB09 | Covered | N/A |
| Pod and block | Repeatable resource blocks, hypervisor manager boundary, management cluster | HZ-ARCH-RB10-RB14 | Covered | N/A |
| Cloud Pod Architecture | Global entitlements, multiple pod federation, not stretched pod | HZ-ARCH-RB15-RB17 | Covered | N/A |
| UAG architecture | External access, 1:1 or N:1 target, avoid inline LB where possible | HZ-ARCH-RB18-RB22 | Covered | N/A |
| Single/double DMZ | DMZ placement and reverse proxy pattern | HZ-ARCH-RB23-RB24 | Covered | N/A |
| True SSO | Enrollment Server, SSO after non-password auth | HZ-ARCH-RB25-RB27 | Covered | N/A |
| vCenter/resource block | vCenter as hypervisor manager delimiter | HZ-ARCH-RB28-RB30 | Covered | N/A |

### Mandatory Installation and Configuration Runbooks

| Source procedure / config heading | Procedure type | Runbook required? | Runbook ID | Nếu không tạo, lý do |
|---|---|---|---|---|
| Deploy multiple Connection Servers per pod | Design / Configure | Yes | HZ-ARCH-RB04, RB06 | N/A |
| Load balance Connection Servers | Configure | Yes | HZ-ARCH-RB07 | N/A |
| Design pod and block | Design / Scale | Yes | HZ-ARCH-RB10 | N/A |
| Configure CPA/global entitlement plan | Configure / Federation | Yes | HZ-ARCH-RB15 | N/A |
| Deploy UAG external access architecture | Configure / Integrate | Yes | HZ-ARCH-RB18 | N/A |
| Plan DMZ model | Configure / Security | Yes | HZ-ARCH-RB23 | N/A |
| Plan True SSO/Enrollment Server | Configure / Identity | Yes | HZ-ARCH-RB25 | N/A |
| Map Horizon to vCenter/resource block | Configure / Capacity | Yes | HZ-ARCH-RB28 | N/A |

### Runbook Inventory

| Runbook ID | Family | Tên runbook | Dùng khi nào | Owner | Risk | Source locator |
|---|---|---|---|---|---|---|
| HZ-ARCH-RB01 | Architecture | Vẽ Horizon user journey internal/external | Onboarding/design | Architect | Low | Core components |
| HZ-ARCH-RB02 | Architecture | Phân biệt broker path và protocol path | Incident/design | System Engineer | Low | Lines 253-262 |
| HZ-ARCH-RB03 | Monitoring | Thiết kế events database per pod | Build | Platform Admin | Medium | Lines 325-327 |
| HZ-ARCH-RB04 | Scale | Sizing Connection Server theo session target | Design | Architect | High | Lines 375-381 |
| HZ-ARCH-RB05 | Scale | Đánh giá rủi ro tunneling qua Connection Server | Design/review | Architect | High | Lines 377-379 |
| HZ-ARCH-RB06 | HA | Kiểm chứng n+1 Connection Server | Pre-production | Platform Admin | High | Lines 388-396 |
| HZ-ARCH-RB07 | Load Balancing | Cấu hình LB persistence cho Connection Servers | Build/change | Network + VDI | High | Lines 400-428 |
| HZ-ARCH-RB08 | Load Balancing | Kiểm thử health monitor và timeout LB | Pre-change | Network + VDI | Medium | Lines 427-428 |
| HZ-ARCH-RB09 | Incident | Triage lỗi authentication qua LB | Incident | System Engineer | Medium | Load balancing |
| HZ-ARCH-RB10 | Scale | Thiết kế pod/block repeatable | Design | Architect | High | Lines 441-512 |
| HZ-ARCH-RB11 | Capacity | Xác định resource block boundary theo hypervisor manager | Design | Architect | High | Lines 469-483 |
| HZ-ARCH-RB12 | HA | Tách management cluster khỏi desktop/RDSH workload | Design | Architect | Medium | Lines 523-539 |
| HZ-ARCH-RB13 | Change | Thêm resource block vào pod | Expansion | Platform Admin | High | Scaling with pod/block |
| HZ-ARCH-RB14 | Incident | Khoanh vùng outage theo pod/block/vCenter | Incident | System Engineer | High | Pod/block |
| HZ-ARCH-RB15 | CPA | Thiết kế CPA và global entitlements | Multi-site | Architect | High | Lines 552-572 |
| HZ-ARCH-RB16 | CPA | Validate disconnected session reconnect across pods | Test | Platform Admin | Medium | Lines 570-572 |
| HZ-ARCH-RB17 | CPA | Tránh stretched pod unsupported design | Architecture review | Architect | High | Lines 567-568; TOC 132 |
| HZ-ARCH-RB18 | UAG | Thiết kế UAG external access | Build | Architect | High | Lines 597-620 |
| HZ-ARCH-RB19 | UAG | Map UAG to Connection Server target | Build/change | Platform Admin | High | Lines 617-624 |
| HZ-ARCH-RB20 | UAG/LB | Quyết định có đặt LB giữa UAG và CS không | Design review | Architect | Medium | Lines 610-631 |
| HZ-ARCH-RB21 | UAG | Validate UAG HA/scaling | Pre-production | Platform Admin | High | TOC 54-58 |
| HZ-ARCH-RB22 | Incident | Triage external-only Horizon issue theo UAG boundary | Incident | System Engineer | High | External access |
| HZ-ARCH-RB23 | Security | Chọn single DMZ vs double DMZ | Security design | Security + Architect | High | Lines 642-658 |
| HZ-ARCH-RB24 | Security | Validate authenticated-only traffic through DMZ | Security test | Security + VDI | Medium | Lines 649-650 |
| HZ-ARCH-RB25 | Identity | Thiết kế True SSO component chain | Design | Identity + VDI | High | TOC 82-94 |
| HZ-ARCH-RB26 | HA | Load balance Enrollment Servers | Build | Identity + Network | Medium | TOC 86 |
| HZ-ARCH-RB27 | Incident | Triage True SSO launch/auth issue | Incident | Identity + VDI | High | True SSO |
| HZ-ARCH-RB28 | vSphere | Map pod/block sang vCenter design | Design | Architect | High | TOC 142-152 |
| HZ-ARCH-RB29 | vSphere | Validate vCenter availability for Horizon operations | Pre-change | Platform Admin | Medium | vCenter considerations |
| HZ-ARCH-RB30 | Evidence | Architecture review evidence pack | Review/audit | Architect | Low | Whole source |

### HZ-ARCH-RB04 - Sizing Connection Server theo session target

#### Tutorial scenario

Bạn cần thiết kế Horizon pod cho vài nghìn user đồng thời. Source nêu một Connection Server hỗ trợ tối đa 4,000 sessions, giảm còn 2,000 nếu tunneling qua Connection Server bằng Blast Secure Gateway/PCoIP Secure Gateway/HTTPS Secure Tunnel.

#### Procedure

1. Xác định concurrent session target, peak, growth và số site/pod. Nếu chưa có dữ liệu, ghi `Need Customer Confirmation`.
2. Xác định Connection Server có nằm trên data path hay chỉ broker/auth. Nếu tunnel qua Connection Server, dùng ngưỡng thấp hơn và coi rủi ro cao.
3. Tính số Connection Server cần cho tải và thêm n+1. Source reference architecture dùng 3 Connection Servers cho target 8,000 users vì hai server xử lý tải và một server redundancy.
4. Kiểm tra giới hạn pod: tối đa 7 Connection Servers và 20,000 active sessions per pod theo source.
5. Nếu vượt ngưỡng pod, chuyển sang multi-pod/CPA thay vì ép một pod.

#### Validation

Thiết kế pass khi Connection Server count, load balancing, n+1 và pod boundary được ghi rõ. Evidence gồm sizing sheet, assumption, tunneling decision và failure scenario.

### HZ-ARCH-RB07 - Cấu hình LB persistence cho Connection Servers

#### Procedure

1. Xác định VIP/FQDN nội bộ cho Connection Servers.
2. Cấu hình health monitor theo KB/vendor guidance; source yêu cầu persistence/sticky connection để giữ dữ liệu tới đúng Connection Server.
3. Validate timeout/persistence values với Horizon session behavior.
4. Test login/enumeration qua VIP, rồi tắt một Connection Server pilot để kiểm tra failover.
5. Thu evidence: LB pool members, monitor state, persistence setting, Horizon login result.

#### Rollback

Nếu VIP gây login fail, route pilot users về Connection Server FQDN trực tiếp theo kế hoạch khẩn cấp hoặc revert LB config đã lưu.

### HZ-ARCH-RB10 - Thiết kế pod/block repeatable

#### Procedure

1. Chia capacity thành resource blocks, mỗi block gắn với resource cluster/hypervisor manager boundary.
2. Không thiết kế tới published maximum nếu failure domain quá lớn; source cảnh báo không nên tự động dùng maximum làm design target.
3. Tách Horizon management components khỏi desktop/RDSH resource cluster nếu scale đủ lớn.
4. Ghi mapping: pod -> Connection Servers -> blocks -> vCenter/cluster -> desktop pools.
5. Validate failure domain: mất một block ảnh hưởng pool/user nào, còn pod hoạt động không.

#### Evidence

Architecture diagram, pod/block matrix, vCenter mapping, capacity assumption, HA/DR notes.

### HZ-ARCH-RB18 - Thiết kế UAG external access

#### Procedure

1. Xác định external access path: internet/client -> UAG -> Connection Server -> Horizon Agent.
2. Deploy ít nhất hai UAG nếu yêu cầu HA, và target tới Connection Servers khác nhau nếu dùng 1:1 pattern.
3. Tránh đặt LB inline giữa UAG và Connection Server trừ khi có lý do; source nêu architecture preferred giúp UAG phát hiện Connection Server target down dễ hơn.
4. Chọn single DMZ hoặc double DMZ theo security policy. Source nêu double DMZ không bắt buộc, nhưng có thể dùng nếu tổ chức yêu cầu.
5. Validate external login, entitlement, Blast/PCoIP protocol path, reconnect và log.

#### Stop conditions

Dừng rollout nếu external protocol connect fail dù authentication pass, hoặc UAG không detect target Connection Server failure như thiết kế.

## Knowledge Atoms

| Atom | Insight vận hành |
|---|---|
| Broker path vs protocol path | Authentication/authorization qua Connection Server khác với session protocol tới Agent |
| Connection Server tunneling | Làm session phụ thuộc Connection Server và giảm sizing threshold |
| Pod/block | Boundary lặp lại để scale và giới hạn blast radius |
| CPA | Federation giữa pod, không phải stretched pod |
| UAG | Edge gateway cho external protocol/auth path, cần HA và target mapping rõ |
| True SSO | Identity bridge cần Enrollment Server và certificate/identity chain |

## Related Concepts

- [[concepts/omnissa-horizon]]
- [[concepts/connection-server]]
- [[concepts/unified-access-gateway]]
- [[concepts/pod-and-block]]
- [[concepts/cloud-pod-architecture]]
- [[concepts/true-sso]]
- [[concepts/load-balancing]]
- [[concepts/vdi-connection-flow]]

## Related Sources

- [[sources/horizon-8-architecture]]
- [[sources/understand-and-troubleshoot-horizon-connections]]
- [[sources/vcenter-server-installation-and-setup]]

## Self Review

- Đã chuyển architecture source thành insight report và runbook design/validation.
- Đã phủ core components, Connection Server scale, LB, pod/block, CPA, UAG/DMZ, True SSO và vCenter boundary.
- Đã đánh dấu các assumption production là `Need Customer Confirmation`.
