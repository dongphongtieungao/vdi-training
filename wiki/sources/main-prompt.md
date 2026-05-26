---
id: source-main-prompt
title: Main Prompt for VDI Training Wiki
type: source
created: 2026-05-26
updated: 2026-05-26
authors:
  - User
year: 2026
importance: 4
urls: []
raw_paths:
  - raw/sources/main.prompt
provenance: replayable
confidence: high
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

`main.prompt` là nguồn hướng dẫn quy trình tạo tài liệu đào tạo VDI trong Lumina Wiki. Nó nhấn mạnh rằng mục tiêu không phải là tạo khung tài liệu mà là tạo nội dung đào tạo đầy đủ, có source grounding, Document Research Pack, concept extraction, scenario, knowledge check, checklist, gaps và self review. Source này củng cố pipeline: raw/sources -> ingest -> wiki/sources/concepts -> lumi-ask -> topics.

Source này không phải vendor technical source. Nó là operational instruction cho cách xây dựng wiki và cách tránh tình trạng tài liệu hời hợt.

## Source Metadata

| Trường | Giá trị |
|---|---|
| Source file | `raw/sources/main.prompt` |
| Source type | User-provided workflow prompt / documentation generation instruction |
| Platform | Lumina Wiki training workflow |
| Version covered | Not applicable |
| Primary training use | Prompt governance, source grounding, document quality requirements |
| Confidence | High for workflow intent |

## Key Claims

- Lumina Wiki phải được dùng theo pipeline: ingest raw sources trước, tạo concepts, dùng lumi-ask để tổng hợp tri thức, rồi mới viết topic.
- Mỗi topic phải có Document Research Pack riêng, không dùng một câu hỏi chung cho toàn bộ 28 tài liệu.
- Tài liệu đào tạo phải có learning objectives, architecture/operational model, component deep dive, tasks, troubleshooting, scenarios, exercises, knowledge check, misconceptions, field checklist, monitoring/evidence, change/risk/rollback, security/RBAC, gaps và links.
- Cần phân biệt nguồn: raw/sources/wiki/sources, training_idea, list_context, general knowledge và unknown/customer confirmation.
- Không được bịa thông tin khách hàng hoặc đưa thao tác rủi ro cao mà thiếu precheck/impact/rollback/postcheck.

## Evidence From Source

- Source mô tả rõ thư mục `raw/`, `wiki/sources`, `wiki/concepts`, `wiki/topics`, `wiki/index.md`.
- Source yêu cầu bắt buộc dùng `training_idea.md` và `list_context.txt`.
- Source liệt kê workflow Lumina: init, ingest, ask nền tảng, tạo concept, ask riêng từng tài liệu, tạo 28 topic, README/index, check, verify.
- Source đưa mẫu cấu trúc topic với 21 mục, gồm Source Grounding và Self Review.

## Key Architecture Knowledge

Source này định nghĩa architecture của knowledge workflow:

```text
raw/sources
  -> wiki/sources
  -> wiki/concepts
  -> lumi-ask / Document Research Pack
  -> wiki/topics
  -> README / wiki index
  -> check / verify
```

Điểm quan trọng: `lumi-ask` chỉ có thể trả lời tốt nếu `wiki/sources` và `wiki/concepts` đã ingest đủ sâu. Vì vậy ingest không thể dừng ở summary ngắn.

## Operational Knowledge

| Hoạt động | Quy tắc từ source | Evidence |
|---|---|---|
| Ingest | Phải khai thác raw/sources trước khi viết topic | Source page có architecture/troubleshooting/evidence/gaps |
| Tạo concept | Concept phải có definition, operational view, common issues, source references | `wiki/concepts` có link nguồn |
| Tạo topic | Mỗi topic dùng Research Pack riêng | Source Grounding trong topic |
| Kiểm soát scope | Bám list_context, không đổi tên file/tài liệu | Metadata topic |
| Kiểm chứng | Chạy check/verify sau khi tạo | Báo cáo check/verify |

## Troubleshooting Knowledge

| Triệu chứng trong wiki | Nguyên nhân có thể | Cách kiểm tra | Hướng xử lý |
|---|---|---|---|
| Topic hời hợt | Ingest source mỏng, không dùng Research Pack | Kiểm tra `wiki/sources` và Source Grounding | Deep ingest lại, tạo Research Pack theo topic |
| Lumi-ask trả lời thiếu | Source page không chứa operational/troubleshooting knowledge | Kiểm tra source page chỉ có summary/key claims | Bổ sung architecture, tasks, evidence, gaps |
| Nội dung bịa customer fact | Không đánh dấu Unknown | Tìm IP/version/topology/SLA không có nguồn | Chuyển sang Need Customer Confirmation |
| Topic trùng lặp | Không bám purpose trong list_context | So sánh với mục đích topic | Refactor theo scope |

## Monitoring and Evidence

Evidence chất lượng của workflow:

- `wiki/sources` đủ sâu, có topic mapping.
- `wiki/concepts` có key sources.
- `wiki/topics` có source grounding và không thiếu mục đào tạo.
- README/index có đủ 28 topic.
- Check/verify không có lỗi nghiêm trọng hoặc có danh sách review.

## Change, Patch and Rollback Notes

Nếu sửa prompt/workflow:

- Cần xác định impact tới cách tạo topic và source page.
- Cần không ghi đè raw.
- Rollback bằng cách quay lại prompt version trước hoặc dùng `create.prompt`/`ingest.prompt` đã lưu.

## Backup, Recovery, HA and DR Notes

Không áp dụng trực tiếp cho hạ tầng VDI, nhưng áp dụng cho tri thức wiki:

- raw/sources là bất biến.
- wiki/sources/concepts/topics là sản phẩm có thể kiểm tra lại bằng source.
- Nếu topic sai, rollback bằng source grounding và list_context/training_idea.

## Security and RBAC Notes

- Không yêu cầu secret, password, token, credential.
- Khi viết tài liệu, các thao tác rủi ro phải có approval, precheck, rollback.

## Concepts to Create or Update

| Concept | Vì sao quan trọng | Source support |
|---|---|---|
| [[concepts/vdi-training-program]] | Quy trình đào tạo hoàn chỉnh | Prompt workflow |
| [[concepts/vdi-operational-readiness]] | Đầu ra năng lực engineer | Quality requirements |
| [[concepts/vdi-documentation-architecture]] | Cấu trúc tài liệu và source grounding | Topic structure |
| [[concepts/monitoring-and-logs]] | Evidence và verification | Check/verify requirements |

## Related Topic Mapping

Source này hỗ trợ toàn bộ 28 topic vì nó quy định cách tạo tài liệu và cấu trúc đào tạo. Các topic chịu ảnh hưởng mạnh nhất:

- [[topics/1_VDI_Foundation_Overview]]
- [[topics/2_Customer_VDI_Landscape_Overview]]
- [[topics/18_VDI_Troubleshooting_Playbook]]
- [[topics/20_VDI_Change_Management_Guide]]
- [[topics/26_VDI_Operational_Knowledge_Base]]
- [[topics/28_VDI_Engineer_Onboarding_Guide]]

## Need Customer Confirmation

- Không có customer fact mới trong prompt. Gaps phải lấy từ `training_idea.md`, vendor sources và từng topic.

## Related Sources

- [[sources/vdi-training-idea]]
- [[sources/vdi-documentation-list-context]]

## People

Nguồn do người dùng cung cấp.

## Open Questions

- Có cần chạy lại toàn bộ topic generation bằng Research Pack sau khi source pages đã deep ingest không?
- Có cần cập nhật concept pages sâu tương đương source pages không?
