---
id: concept-unified-access-gateway
title: "Unified Access Gateway"
type: concept
created: 2026-05-22
updated: 2026-05-22
key_sources:
  - sources/horizon-8-architecture
  - sources/understand-and-troubleshoot-horizon-connections
related_concepts:
  - omnissa-horizon
  - vdi-connection-flow
confidence: unverified
---

## Definition

Unified Access Gateway là appliance gateway của Horizon đặt ở vùng truy cập an toàn để phục vụ người dùng bên ngoài, chuyển tiếp xác thực và giao thức phiên tới thành phần Horizon bên trong.

## Variants

- Single DMZ.
- Double DMZ.
- Nhiều appliance sau load balancer.

## Key sources

- [[sources/horizon-8-architecture]]
- [[sources/understand-and-troubleshoot-horizon-connections]]

## Related concepts

- [[concepts/connection-server]]
- [[concepts/load-balancing]]
- [[concepts/firewall-ports]]
- [[concepts/certificate-management]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

Sai cấu hình URL ngoài, certificate hoặc firewall quanh UAG thường làm phiên bên ngoài lỗi dù nội bộ vẫn chạy.

