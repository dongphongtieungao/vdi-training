---
id: concept-virtual-networking
title: "Virtual networking"
type: concept
created: 2026-05-22
updated: 2026-05-22
key_sources:
  - sources/vmware-vsphere-8-0
  - sources/xenserver-8-4
related_concepts:
  - firewall-ports
  - vdi-connection-flow
confidence: unverified
---

## Definition

Virtual networking là lớp mạng ảo trong hypervisor, nối VM tới VLAN, port group, virtual switch, uplink vật lý và các chính sách mạng.

## Variants

- Standard hoặc distributed switch trong vSphere.
- Network, bond và interface trong XenServer.

## Key sources

- [[sources/vmware-vsphere-8-0]]
- [[sources/xenserver-8-4]]

## Related concepts

- [[concepts/firewall-ports]]
- [[concepts/load-balancing]]
- [[concepts/vdi-connection-flow]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

Lỗi mạng ảo có thể biểu hiện giống lỗi VDI, nên cần tách kiểm tra từ VM ra gateway và broker.

## Source References

- [[sources/vmware-vsphere-8-0-part-06-host-profiles-networking]] - vSwitch, vDS, port group, uplink, VMkernel và network rollback.
