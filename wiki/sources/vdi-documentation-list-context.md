---
id: source-vdi-documentation-list-context
title: VDI Documentation List Context
type: source
created: 2026-05-22
updated: 2026-05-26
authors:
  - User
year: 2026
importance: 5
urls: []
raw_paths:
  - raw/sources/list_context.txt
provenance: replayable
confidence: high
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

`list_context.txt` là source of truth cho danh mục 28 tài liệu trong `wiki/topics`: thứ tự, tên tài liệu, tên file và mục đích tài liệu. Source này kiểm soát scope để mỗi topic không bị đổi tên, không viết lệch mục tiêu và không mở rộng sang chủ đề ngoài danh mục.

Khác với vendor source, tài liệu này không cung cấp tri thức kỹ thuật sâu. Giá trị chính của nó là điều phối: quyết định topic nào cần tạo, topic nào đọc trước, topic nào liên quan và mỗi source kỹ thuật nên map vào đâu.

## Source Metadata

| Trường | Giá trị |
|---|---|
| Source file | `raw/sources/list_context.txt` |
| Source type | User-provided documentation scope list |
| Platform | Whole VDI training corpus |
| Version covered | Not applicable |
| Primary training use | Topic scope control, filename control, purpose control |
| Confidence | High for document list and purpose |

## Key Claims

- Bộ tài liệu gồm đúng 28 topic, từ VDI Foundation Overview đến VDI Engineer Onboarding Guide.
- Mỗi dòng tương ứng một file Markdown trong `wiki/topics`.
- Mục đích tài liệu là ranh giới scope bắt buộc khi viết/refactor topic.
- Các nhóm chính bao gồm foundation, landscape, architecture, access flow, identity, hypervisor/HCI, storage, network, security/policy, provisioning, image, monitoring, operations, incident, troubleshooting, performance, change, patch/upgrade, backup, HA/DR, RBAC, support, knowledge base, glossary và onboarding.

## Evidence From Source

Source chứa các cột:

- Thứ tự.
- Tên tài liệu.
- Name File.
- Mục đích tài liệu.

Ví dụ scope quan trọng:

- Topic 1 cung cấp kiến thức nền tảng về VDI, desktop ảo, published application, session, user access và các lớp hạ tầng.
- Topic 4 giải thích kiến trúc CVAD với Delivery Controller, StoreFront, Citrix Gateway, VDA, Site Database, License Server, Machine Catalog và Delivery Group.
- Topic 18 cung cấp playbook lỗi phổ biến như login fail, không thấy desktop, launch fail, VDA unregistered, Horizon Agent unreachable, login chậm, black screen, disconnect và profile issue.
- Topic 28 cung cấp lộ trình học và thực hành cho engineer mới.

## Key Architecture Knowledge

Source này không mô tả architecture sản phẩm, nhưng định nghĩa architecture của bộ tài liệu:

1. Nền tảng và landscape: topics 1-2.
2. Kiến trúc platform: topics 3-5.
3. Dependency nền: topics 6-10.
4. Provisioning/image/platform-specific operations: topics 11-14.
5. Monitoring/daily/incident/troubleshooting/performance: topics 15-19.
6. Governance/change/patch/backup/HA/RBAC/support: topics 20-25.
7. Knowledge consolidation: topics 26-28.

## Operational Knowledge

Khi dùng source này để viết tài liệu:

- Luôn lấy đúng tên topic và filename.
- Luôn đặt mục đích topic theo câu trong source.
- Không nhồi toàn bộ kiến thức VDI vào mọi topic.
- Nếu source kỹ thuật hỗ trợ nhiều topic, map theo mục đích từng topic.
- Nếu tri thức chưa thuộc topic hiện tại, chỉ cross-link sang topic liên quan.

## Troubleshooting Knowledge

Với quy trình tạo tài liệu, các lỗi thường gặp:

| Triệu chứng | Nguyên nhân có thể | Cách kiểm tra | Hướng xử lý |
|---|---|---|---|
| Topic viết lệch scope | Không đối chiếu mục đích trong list_context | So sánh heading/nội dung với dòng topic | Refactor lại theo mục đích gốc |
| Tên file sai | Tự đổi filename | So sánh với cột Name File | Đổi về đúng filename |
| Nội dung trùng nhau giữa topic | Không phân biệt mục tiêu | Kiểm tra mục đích từng topic | Giữ phần liên quan, chuyển sâu sang topic đúng |
| Thiếu topic mapping | Source ingest không map topic | Kiểm tra Related Topic Mapping | Bổ sung mapping theo 28 topic |

## Monitoring and Evidence

Evidence để kiểm soát chất lượng bộ tài liệu:

- Danh sách 28 file tồn tại trong `wiki/topics`.
- README/index liệt kê đúng thứ tự.
- Mỗi topic có mục đích khớp `list_context.txt`.
- Mỗi source page có Related Topic Mapping.
- Không có topic ngoài danh mục nếu người dùng chưa yêu cầu.

## Change, Patch and Rollback Notes

Nếu sửa `list_context.txt` hoặc thay đổi danh mục:

- Đây là change scope lớn, ảnh hưởng toàn bộ wiki/topics.
- Cần ghi rõ topic thêm/bớt/đổi tên/đổi mục đích.
- Cần cập nhật README, wiki/index, topic cross-links và create.prompt.
- Rollback là quay lại danh mục trước và kiểm tra file orphan/missing.

## Backup, Recovery, HA and DR Notes

Không áp dụng trực tiếp cho hạ tầng VDI. Tuy nhiên, với wiki:

- `list_context.txt` là source điều khiển, nên cần được giữ nguyên trong `raw/sources`.
- Nếu mất hoặc sai, bộ topic có thể bị lệch scope.

## Security and RBAC Notes

Không chứa credential. Tuy nhiên, nó quy định topic RBAC và security/policy cần tồn tại trong bộ tài liệu.

## Concepts to Create or Update

| Concept | Vì sao quan trọng | Source support |
|---|---|---|
| [[concepts/vdi-training-program]] | Quản lý chương trình 28 topic | Source trực tiếp |
| [[concepts/vdi-documentation-architecture]] | Cấu trúc bộ tài liệu | Source trực tiếp |
| [[concepts/vdi-operational-readiness]] | Chuẩn đầu ra onboarding | Source trực tiếp |

## Related Topic Mapping

Source này map tới toàn bộ 28 topic vì nó định nghĩa tên, file và mục đích của từng topic:

- [[topics/1_VDI_Foundation_Overview]]
- [[topics/2_Customer_VDI_Landscape_Overview]]
- [[topics/3_Omnissa_Horizon_Architecture_Overview]]
- [[topics/4_Citrix_CVAD_Architecture_Overview]]
- [[topics/5_VDI_Access_Flow_Design]]
- [[topics/6_Identity_and_Domain_Integration_Guide]]
- [[topics/7_Hypervisor_and_HCI_Operations_Guide]]
- [[topics/8_Storage_Operations_for_VDI]]
- [[topics/9_Network_Operations_for_VDI]]
- [[topics/10_VDI_Security_and_Policy_Management_Guide]]
- [[topics/11_VDI_Provisioning_and_Allocation_Guide]]
- [[topics/12_Master_Image_Management_Guide]]
- [[topics/13_Citrix_Machine_Catalog_and_Delivery_Group_Guide]]
- [[topics/14_Omnissa_Desktop_Pool_and_Entitlement_Guide]]
- [[topics/15_VDI_Monitoring_and_Alerting_Guide]]
- [[topics/16_Daily_Operations_Checklist]]
- [[topics/17_VDI_Incident_Classification_Guide]]
- [[topics/18_VDI_Troubleshooting_Playbook]]
- [[topics/19_VDI_Performance_and_Capacity_Guide]]
- [[topics/20_VDI_Change_Management_Guide]]
- [[topics/21_VDI_Patch_and_Upgrade_Guide]]
- [[topics/22_VDI_Backup_and_Recovery_Guide]]
- [[topics/23_VDI_High_Availability_and_Disaster_Recovery_Guide]]
- [[topics/24_VDI_Access_Control_and_RBAC_Guide]]
- [[topics/25_VDI_Support_and_Escalation_Guide]]
- [[topics/26_VDI_Operational_Knowledge_Base]]
- [[topics/27_VDI_Glossary_and_Concept_Dictionary]]
- [[topics/28_VDI_Engineer_Onboarding_Guide]]

## Need Customer Confirmation

Không có câu hỏi kỹ thuật trực tiếp từ source này. Các câu hỏi khách hàng nằm trong từng topic/source kỹ thuật. Tuy nhiên cần xác nhận với project owner nếu danh mục 28 topic thay đổi trong tương lai.

## Related Sources

- [[sources/vdi-training-idea]]
- [[sources/main-prompt]]

## People

Nguồn do người dùng cung cấp.

## Open Questions

- Có cần thêm topic mới ngoài 28 tài liệu không? Theo source hiện tại: không, trừ khi người dùng yêu cầu chính thức.
