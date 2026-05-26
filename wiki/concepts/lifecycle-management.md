---
id: concept-lifecycle-management
title: "Lifecycle management"
type: concept
created: 2026-05-22
updated: 2026-05-22
key_sources:
  - sources/vmware-vsphere-8-0
  - sources/xenserver-8-4
related_concepts:
  - snapshot
  - high-availability
confidence: unverified
---

## Definition

Lifecycle management là quy trình cập nhật, vá lỗi, nâng cấp, kiểm tra tương thích và duy trì trạng thái hỗ trợ cho host, platform, VM image và thành phần VDI.

## Variants

- vSphere Lifecycle Manager.
- Update host XenServer.
- Vòng đời master image hoặc gold image.

## Key sources

- [[sources/vmware-vsphere-8-0]]
- [[sources/xenserver-8-4]]

## Related concepts

- [[concepts/snapshot]]
- [[concepts/high-availability]]
- [[concepts/monitoring-and-logs]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

Trong VDI, lifecycle cần lịch bảo trì rõ vì thay đổi hạ tầng có thể ảnh hưởng nhiều người dùng cùng lúc.

## Source References

- [[sources/vmware-vsphere-8-0-part-01-release-and-lifecycle]] - release notes, compatibility and patch known issues.
- [[sources/vmware-vsphere-8-0-part-02-esxi-install-upgrade]] - ESXi upgrade workflow.
- [[sources/vmware-vsphere-8-0-part-04-authentication-lifecycle]] - host and cluster lifecycle, remediation and desired state.
