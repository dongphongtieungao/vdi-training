---
id: concept-vmware-vsphere
title: "VMware vSphere"
type: concept
created: 2026-05-22
updated: 2026-05-22
key_sources:
  - sources/vmware-vsphere-8-0
  - sources/vcenter-server-installation-and-setup
related_concepts:
  - esxi
  - vcenter-server
confidence: unverified
---

## Definition

VMware vSphere là nền tảng ảo hóa gồm ESXi, vCenter Server và các dịch vụ quản trị VM, cluster, network, storage và lifecycle.

## Variants

- vSphere dùng vCenter quản trị tập trung.
- ESXi host đơn lẻ quản trị bằng VMware Host Client.

## Key sources

- [[sources/vmware-vsphere-8-0]]
- [[sources/vcenter-server-installation-and-setup]]

## Related concepts

- [[concepts/esxi]]
- [[concepts/vcenter-server]]
- [[concepts/virtual-machine]]
- [[concepts/datastore]]
- [[concepts/virtual-networking]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

Trong VDI, vSphere là lớp nền nơi desktop VM, template, snapshot và datastore thực sự tồn tại.

## Source References

- [[sources/vmware-vsphere-8-0]] - overview và coverage ledger cho full-source chunked ingest.
- [[sources/vmware-vsphere-8-0-part-01-release-and-lifecycle]] - release notes, known issues và patch lifecycle.
- [[sources/vmware-vsphere-8-0-part-02-esxi-install-upgrade]] - ESXi install, upgrade, syslog và support bundle.
- [[sources/vmware-vsphere-8-0-part-03-vcenter-install-upgrade]] - vCenter install, upgrade, backup/restore dependency.
- [[sources/vmware-vsphere-8-0-part-05-vcenter-host-vm-admin]] - vCenter tasks, VM administration, template/snapshot.
- [[sources/vmware-vsphere-8-0-part-07-storage]] - datastore, storage policy, latency và capacity.
- [[sources/vmware-vsphere-8-0-part-08-security-resource-availability]] - security, RBAC, resource management và HA.
- [[sources/vmware-vsphere-8-0-part-09-monitoring-host-client-aria]] - monitoring, alarms, events, performance và syslog.
