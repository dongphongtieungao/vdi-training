---
id: concept-connection-server
title: "Connection Server"
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

Connection Server là thành phần môi giới kết nối trong Horizon, xử lý xác thực, entitlement, chọn tài nguyên và điều phối phiên tới desktop hoặc application.

## Variants

- Nhiều Connection Server sau load balancer trong một pod.
- Connection Server kết hợp với Unified Access Gateway cho truy cập bên ngoài.

## Key sources

- [[sources/horizon-8-architecture]]
- [[sources/understand-and-troubleshoot-horizon-connections]]

## Related concepts

- [[concepts/omnissa-horizon]]
- [[concepts/unified-access-gateway]]
- [[concepts/load-balancing]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

Connection Server là nơi kiểm tra entitlement, trạng thái pool và đường đi phiên khi người dùng không vào được desktop.

