---
id: source-vcenter-server-installation-and-setup
title: vCenter Server Installation and Setup
type: source
created: 2026-05-22
updated: 2026-05-22
authors:
  - VMware by Broadcom
year: 2023
importance: 4
urls:
  - "https://docs.vmware.com/"
raw_paths:
  - raw/sources/vsphere-vcenter-802-installation-guide.txt
provenance: replayable
confidence: unverified
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

Tài liệu này hướng dẫn cài đặt và thiết lập vCenter Server Appliance cho vSphere 8.0 Update 2, gồm thành phần dịch vụ, domain, Enhanced Linked Mode, yêu cầu hệ thống, DNS, NTP, cổng mạng, triển khai GUI/CLI và cấu hình sau cài đặt. Với VDI, vCenter là điểm điều khiển quan trọng để Horizon hoặc Citrix quản lý máy ảo, template, snapshot, cluster và quyền truy cập hạ tầng.

## Key Claims

- vCenter Server Appliance là thành phần quản trị trung tâm của môi trường vSphere và cần chuẩn bị kỹ DNS, thời gian hệ thống, tài nguyên phần cứng, storage và network.
- Enhanced Linked Mode và vSphere domain ảnh hưởng đến cách nhiều vCenter được quản trị chung và cách phân tách phạm vi vận hành.
- Quy trình triển khai gồm chuẩn bị, cài appliance, cấu hình ban đầu và xác nhận dịch vụ sau cài đặt.
- Các yêu cầu về port, đồng bộ thời gian và quyền truy cập là điểm kiểm tra quan trọng trước khi tích hợp với nền tảng VDI.

## Concepts

- [[concepts/vcenter-server]]
- [[concepts/vcenter-server-appliance]]
- [[concepts/enhanced-linked-mode]]
- [[concepts/dns-and-time-sync]]
- [[concepts/firewall-ports]]
- [[concepts/vmware-vsphere]]
- [[concepts/identity-and-access-management]]

## People

Không nêu cá nhân tác giả trong phần nguồn đã nạp.

## Open Questions

- Cần bổ sung cấu hình quyền tối thiểu cho tài khoản tích hợp Horizon hoặc Citrix vào vCenter.
- Cần kiểm tra mô hình khách hàng có một vCenter, nhiều vCenter hay Enhanced Linked Mode.

