---
id: concept-storage-repository
title: "Storage repository"
type: concept
created: 2026-05-22
updated: 2026-05-22
key_sources:
  - sources/xenserver-8-4
related_concepts:
  - xenserver
  - storage-permissions
confidence: unverified
---

## Definition

Storage repository là vùng lưu trữ trong XenServer dùng để chứa virtual disk, ISO hoặc dữ liệu liên quan tới VM.

## Variants

- Local storage.
- Shared storage như NFS, iSCSI hoặc GFS2 tùy thiết kế.

## Key sources

- [[sources/xenserver-8-4]]

## Related concepts

- [[concepts/xenserver]]
- [[concepts/storage-permissions]]
- [[concepts/high-availability]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

Storage repository lỗi thường kéo theo VM không start, migration lỗi hoặc HA không hoạt động đúng.

