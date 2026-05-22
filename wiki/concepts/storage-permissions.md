---
id: concept-storage-permissions
title: "Storage permissions"
type: concept
created: 2026-05-22
updated: 2026-05-22
key_sources:
  - sources/fslogix-documentation
related_concepts:
  - profile-container
  - datastore
confidence: unverified
---

## Definition

Storage permissions là quyền truy cập ở lớp file share, filesystem hoặc datastore, quyết định dịch vụ và người dùng có thể tạo, đọc, ghi và khóa dữ liệu đúng cách hay không.

## Variants

- NTFS và share permission cho FSLogix.
- Quyền datastore hoặc storage repository cho hypervisor.

## Key sources

- [[sources/fslogix-documentation]]

## Related concepts

- [[concepts/profile-container]]
- [[concepts/datastore]]
- [[concepts/storage-repository]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

Sai quyền storage có thể biểu hiện thành lỗi đăng nhập, container không tạo được, VM không start hoặc snapshot lỗi.

