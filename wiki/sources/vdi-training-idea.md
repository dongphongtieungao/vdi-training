---
id: source-vdi-training-idea
title: "VDI training idea"
type: source
created: 2026-05-22
updated: 2026-05-22
authors:
  - User
year: 2026
importance: 5
urls: []
raw_paths:
  - raw/sources/training_idea.md
provenance: replayable
confidence: unverified
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

Nguồn này mô tả ý tưởng xây dựng bộ tài liệu đào tạo và nghiên cứu vận hành VDI cho System Engineer, tập trung vào hai nền tảng lớn: Omnissa Horizon trên HCI và Citrix Virtual Apps and Desktops trên XenServer hoặc VMware ESXi. Ý tưởng chính là không viết manual theo sản phẩm, mà xây dựng tài liệu giúp engineer hiểu kiến trúc, đọc luồng kết nối, nhận diện lớp lỗi, thực hiện tác vụ vận hành và biết khi nào cần escalation.

## Key Claims

- Bộ tài liệu nên phục vụ vận hành thực tế, không chỉ mô tả tính năng sản phẩm.
- Engineer cần nhìn hệ thống VDI quy mô 1500 đến hơn 2000 máy như một nền tảng dịch vụ nhiều lớp: identity, broker, image, hypervisor, storage, network, policy, monitoring và quy trình vận hành.
- Horizon và Citrix cần có phần riêng về kiến trúc, nhưng các lớp dùng chung như identity, storage, network, monitoring, change và troubleshooting nên được chuẩn hóa để tránh trùng lặp.
- Runbook chi tiết cần dữ liệu thật từ khách hàng như phiên bản, topology, access flow, monitoring tool, profile solution, HA design và quy trình change.

## Concepts

- [[concepts/vdi-training-program]]
- [[concepts/vdi-documentation-architecture]]
- [[concepts/vdi-operational-readiness]]
- [[concepts/vdi-connection-flow]]
- [[concepts/omnissa-horizon]]
- [[concepts/citrix-virtual-apps-and-desktops]]
- [[concepts/identity-and-access-management]]
- [[concepts/monitoring-and-logs]]
- [[concepts/lifecycle-management]]

## People

Không nêu cá nhân cụ thể.

## Open Questions

- Cần xác nhận topology thực tế của khách hàng trước khi viết các SOP chi tiết.
- Cần quyết định bộ tài liệu sẽ ưu tiên onboarding engineer mới, vận hành hằng ngày, xử lý sự cố, hay tất cả theo lộ trình nhiều lớp.

