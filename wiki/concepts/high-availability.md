---
id: concept-high-availability
title: "High availability"
type: concept
created: 2026-05-22
updated: 2026-05-22
key_sources:
  - sources/fslogix-documentation
  - sources/xenserver-8-4
related_concepts:
  - load-balancing
  - cloud-cache
confidence: unverified
---

## Definition

High availability là thiết kế giúp dịch vụ tiếp tục hoạt động khi một thành phần hỏng, thường bằng cách có nhiều node, nhiều đường network, nhiều vị trí lưu trữ hoặc cơ chế failover.

## Variants

- HA cho gateway, Connection Server hoặc Controller.
- HA cho hypervisor pool hoặc cluster.
- HA cho storage/profile container.

## Key sources

- [[sources/fslogix-documentation]]
- [[sources/xenserver-8-4]]

## Related concepts

- [[concepts/load-balancing]]
- [[concepts/cloud-cache]]
- [[concepts/hypervisor-pool]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

HA không thay thế monitoring; cần kiểm tra cả trạng thái failover và năng lực khi mất một node.

## Source References

- [[sources/vmware-vsphere-8-0-part-08-security-resource-availability]] - vSphere HA, admission control, DRS và failover capacity.
- [[sources/vmware-vsphere-8-0-part-02-esxi-install-upgrade]] - host maintenance and HA validation.
