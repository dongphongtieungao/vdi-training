---
id: concept-datastore
title: "Datastore"
type: concept
created: 2026-05-22
updated: 2026-05-22
key_sources:
  - sources/vmware-vsphere-8-0
related_concepts:
  - vmware-vsphere
  - storage-permissions
confidence: unverified
---

## Definition

Datastore là nơi vSphere lưu tệp máy ảo như disk, cấu hình, snapshot và log.

## Variants

- VMFS hoặc NFS datastore.
- vSAN datastore nếu môi trường dùng vSAN.

## Key sources

- [[sources/vmware-vsphere-8-0]]

## Related concepts

- [[concepts/virtual-machine]]
- [[concepts/snapshot]]
- [[concepts/storage-permissions]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

Datastore đầy hoặc latency cao là nguyên nhân phổ biến của lỗi và chậm trong VDI.

## Source References

- [[sources/vmware-vsphere-8-0-part-07-storage]] - datastore capacity, latency, storage policy, multipathing và snapshot growth.
- [[sources/vmware-vsphere-8-0-part-05-vcenter-host-vm-admin]] - VM placement, task failure và datastore dependency.
