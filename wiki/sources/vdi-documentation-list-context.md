---
id: source-vdi-documentation-list-context
title: VDI documentation list context
type: source
created: 2026-05-22
updated: 2026-05-22
authors:
  - User
year: 2026
importance: 5
urls: []
raw_paths:
  - raw/sources/list_context.txt
provenance: replayable
confidence: unverified
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

Nguồn này liệt kê 28 tài liệu chính thức cần xây dựng cho bộ tài liệu vận hành VDI, gồm thứ tự, tên tài liệu, tên file đầu ra và mục đích của từng tài liệu. Danh mục bao phủ từ nền tảng VDI, bức tranh khách hàng, kiến trúc Horizon/Citrix, access flow, identity, hypervisor, storage, network, policy, provisioning, image, monitoring, incident, troubleshooting, capacity, change, patch, backup, HA/DR, RBAC, escalation, knowledge base, glossary đến onboarding.

## Key Claims

- Danh mục hiện tại đã bao phủ hầu hết các lớp vận hành VDI chính: kiến trúc, hạ tầng, truy cập, identity, storage, network, policy, monitoring, incident, change và onboarding.
- Cột Name File cung cấp tên file chuẩn cho từng tài liệu, ví dụ 1_VDI_Foundation_Overview.md đến 28_VDI_Engineer_Onboarding_Guide.md; đây nên được xem là quy ước đặt tên khi tạo artifact đầu ra.
- Các tài liệu theo sản phẩm như Citrix Machine Catalog and Delivery Group Guide và Omnissa Desktop Pool and Entitlement Guide giúp chuyển từ kiến thức chung sang thao tác nền tảng cụ thể.
- Các tài liệu vận hành ngang như Monitoring, Incident Classification, Troubleshooting, Performance, Change, Patch, Backup, HA/DR, RBAC và Escalation là cần thiết để biến kiến thức thành năng lực vận hành.
- Danh mục còn nên bổ sung một số tài liệu đầu vào/chuẩn hóa như sơ đồ kiến trúc thật, ma trận thành phần, inventory, acceptance criteria và mẫu SOP để giảm rủi ro khi triển khai viết chi tiết.

## Concepts

- [[concepts/vdi-documentation-architecture]]
- [[concepts/vdi-training-program]]
- [[concepts/vdi-operational-readiness]]
- [[concepts/daily-operations]]
- [[concepts/incident-management]]
- [[concepts/change-management]]
- [[concepts/capacity-management]]
- [[concepts/backup-and-recovery]]
- [[concepts/high-availability]]
- [[concepts/identity-and-access-management]]

## People

Không nêu cá nhân cụ thể.

## Open Questions

- Có nên gom một số tài liệu nhỏ thành nhóm để tránh quá nhiều đầu mục độc lập?
- Có cần thêm tài liệu theo persona, ví dụ Helpdesk, L1/L2 System Engineer, Platform Admin và Security/Network/Storage phối hợp?
- Khi tạo tài liệu thật, các file đầu ra có bắt buộc lưu đúng theo cột Name File trong cùng một thư mục hay cần chia theo nhóm/chapter?
