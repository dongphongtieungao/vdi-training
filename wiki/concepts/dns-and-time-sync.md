---
id: concept-dns-and-time-sync
title: "DNS and time sync"
type: concept
created: 2026-05-22
updated: 2026-05-22
key_sources:
  - sources/vcenter-server-installation-and-setup
related_concepts:
  - certificate-management
  - identity-and-access-management
confidence: unverified
---

## Definition

DNS and time sync là nhóm điều kiện nền gồm phân giải tên đúng và đồng bộ thời gian chính xác giữa các thành phần hạ tầng.

## Variants

- DNS forward và reverse cho appliance hoặc server.
- NTP cho vCenter, ESXi, domain controller, broker và gateway.

## Key sources

- [[sources/vcenter-server-installation-and-setup]]

## Related concepts

- [[concepts/certificate-management]]
- [[concepts/identity-and-access-management]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

Sai DNS hoặc lệch thời gian có thể làm lỗi certificate, Kerberos, SSO và tích hợp dịch vụ.

