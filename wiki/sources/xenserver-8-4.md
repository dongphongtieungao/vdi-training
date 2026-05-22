---
id: source-xenserver-8-4
title: XenServer 8.4
type: source
created: 2026-05-22
updated: 2026-05-22
authors:
  - Citrix Systems
year: 2026
importance: 5
urls: []
raw_paths:
  - raw/sources/xenserver-8.4.txt
provenance: replayable
confidence: unverified
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

Tài liệu XenServer 8.4 bao phủ kiến trúc, yêu cầu hệ thống, giới hạn cấu hình, hỗ trợ hệ điều hành khách, licensing, cài đặt, nâng cấp, cập nhật host, high availability, storage, networking và vận hành pool. Trong bối cảnh Citrix VDI, đây là nguồn nền để hiểu lớp hypervisor khi Citrix Virtual Apps and Desktops chạy trên XenServer thay vì VMware ESXi.

## Key Claims

- XenServer tổ chức tài nguyên theo host, pool, VM, storage repository và network, với XenCenter hoặc công cụ dòng lệnh là các kênh quản trị phổ biến.
- VDI trên XenServer cần đặc biệt chú ý tới pool design, HA, storage multipathing, network bonding, cập nhật host và tương thích guest OS.
- Licensing và kênh cập nhật ảnh hưởng đến khả năng dùng tính năng doanh nghiệp và lịch vận hành bảo trì.
- Khi xử lý sự cố, cần phân biệt lỗi ở lớp hypervisor, storage, network, VM guest và lớp Citrix phía trên.

## Concepts

- [[concepts/xenserver]]
- [[concepts/hypervisor-pool]]
- [[concepts/storage-repository]]
- [[concepts/high-availability]]
- [[concepts/virtual-networking]]
- [[concepts/guest-operating-system-support]]
- [[concepts/citrix-virtual-apps-and-desktops]]
- [[concepts/lifecycle-management]]

## People

Không nêu cá nhân tác giả trong phần nguồn đã nạp.

## Open Questions

- Cần tạo runbook riêng cho pool master, HA failover, storage repository lỗi, VM không start và update host.
- Cần xác định khách hàng dùng XenServer hay VMware ESXi cho từng cụm Citrix.

