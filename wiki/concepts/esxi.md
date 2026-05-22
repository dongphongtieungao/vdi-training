---
id: concept-esxi
title: "ESXi"
type: concept
created: 2026-05-22
updated: 2026-05-22
key_sources:
  - sources/vmware-vsphere-8-0
related_concepts:
  - vmware-vsphere
  - virtual-machine
confidence: unverified
---

## Definition

ESXi là hypervisor của VMware chạy trực tiếp trên host vật lý để cung cấp tài nguyên CPU, memory, network và storage cho máy ảo.

## Variants

- Host độc lập.
- Host nằm trong cluster được vCenter quản lý.

## Key sources

- [[sources/vmware-vsphere-8-0]]

## Related concepts

- [[concepts/vmware-vsphere]]
- [[concepts/vcenter-server]]
- [[concepts/virtual-machine]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

Khi VDI chậm hoặc VM lỗi, cần kiểm tra cả host ESXi, datastore và network.

