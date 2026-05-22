---
id: concept-load-balancing
title: "Load balancing"
type: concept
created: 2026-05-22
updated: 2026-05-22
key_sources:
  - sources/horizon-8-architecture
  - sources/understand-and-troubleshoot-horizon-connections
related_concepts:
  - high-availability
  - vdi-connection-flow
confidence: unverified
---

## Definition

Load balancing là cơ chế phân phối kết nối tới nhiều node dịch vụ để tăng khả năng chịu tải và sẵn sàng, đồng thời cần giữ đúng affinity hoặc phiên khi ứng dụng yêu cầu.

## Variants

- Load balancing Connection Server.
- Load balancing Unified Access Gateway.
- Load balancing cho StoreFront hoặc gateway Citrix.

## Key sources

- [[sources/horizon-8-architecture]]
- [[sources/understand-and-troubleshoot-horizon-connections]]

## Related concepts

- [[concepts/high-availability]]
- [[concepts/vdi-connection-flow]]
- [[concepts/firewall-ports]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

Sai affinity hoặc WebSocket handling có thể tạo lỗi khó lặp lại trong phiên VDI.

