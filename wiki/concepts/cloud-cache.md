---
id: concept-cloud-cache
title: "Cloud Cache"
type: concept
created: 2026-05-22
updated: 2026-05-22
key_sources:
  - sources/fslogix-documentation
related_concepts:
  - fslogix
  - high-availability
confidence: unverified
---

## Definition

Cloud Cache là cơ chế FSLogix cho phép dùng nhiều vị trí lưu container để tăng khả năng sẵn sàng, đồng thời duy trì cache cục bộ và đồng bộ dữ liệu giữa các provider.

## Variants

- Nhiều file share trong cùng datacenter.
- Kết hợp file share tại nhiều site hoặc cloud storage được hỗ trợ.

## Key sources

- [[sources/fslogix-documentation]]

## Related concepts

- [[concepts/fslogix]]
- [[concepts/high-availability]]
- [[concepts/storage-permissions]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

Cloud Cache tăng khả năng chịu lỗi nhưng cũng tăng độ phức tạp khi điều tra lock, provider offline và đồng bộ.

