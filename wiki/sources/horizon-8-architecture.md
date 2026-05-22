---
id: source-horizon-8-architecture
title: Horizon 8 architecture
type: source
created: 2026-05-22
updated: 2026-05-22
authors:
  - Omnissa
year: 2026
importance: 5
urls:
  - "https://techzone.omnissa.com/resource/horizon-8-architecture"
raw_paths:
  - raw/sources/horizon_8_architecture_noindex.txt
provenance: replayable
confidence: unverified
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

Tài liệu này trình bày kiến trúc Omnissa Horizon 8, gồm Connection Server, pod, block, hypervisor manager, Unified Access Gateway, Cloud Pod Architecture, mạng, giao thức hiển thị, xác thực và True SSO. Đây là nguồn nền tảng để System Engineer hiểu bức tranh tổng thể trước khi đi vào cấp phát desktop, vận hành pool, thiết kế truy cập ngoài và xử lý sự cố kết nối.

## Key Claims

- Horizon 8 được tổ chức quanh Connection Server, các pod/block, tài nguyên hypervisor và lớp truy cập an toàn qua Unified Access Gateway.
- Khả năng mở rộng và sẵn sàng cao phụ thuộc vào cách chia pod, block, load balancing Connection Server và load balancing Unified Access Gateway.
- Luồng truy cập nội bộ và bên ngoài có khác biệt quan trọng về đường đi mạng, giao thức hiển thị, cổng firewall và điểm đặt thành phần bảo mật.
- Horizon Cloud và Cloud Pod Architecture mở rộng phạm vi quản trị nhưng cần hiểu rõ phân quyền, entitlement và vị trí của gateway.

## Concepts

- [[concepts/omnissa-horizon]]
- [[concepts/connection-server]]
- [[concepts/unified-access-gateway]]
- [[concepts/pod-and-block]]
- [[concepts/cloud-pod-architecture]]
- [[concepts/display-protocol]]
- [[concepts/vdi-connection-flow]]
- [[concepts/true-sso]]
- [[concepts/load-balancing]]

## People

Không nêu cá nhân tác giả trong phần nguồn đã nạp.

## Open Questions

- Cần bổ sung chi tiết về Instant Clone, master image, desktop pool và entitlement từ các nguồn Horizon vận hành khác.
- Cần xác định môi trường khách hàng có dùng Horizon Cloud, True SSO, Omnissa Access hay chỉ triển khai on-premises.

