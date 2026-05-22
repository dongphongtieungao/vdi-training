---
id: concept-true-sso
title: "True SSO"
type: concept
created: 2026-05-22
updated: 2026-05-22
key_sources:
  - sources/horizon-8-architecture
related_concepts:
  - omnissa-horizon
  - identity-and-access-management
confidence: unverified
---

## Definition

True SSO là cơ chế Horizon cho phép người dùng vào desktop mà không phải nhập lại mật khẩu Windows sau khi đã xác thực ở lớp truy cập.

## Variants

- Tích hợp với Omnissa Access hoặc nguồn xác thực bên ngoài.
- Phụ thuộc vào certificate và cấu hình identity phù hợp.

## Key sources

- [[sources/horizon-8-architecture]]

## Related concepts

- [[concepts/identity-and-access-management]]
- [[concepts/certificate-management]]

## Mentioned in

Chưa có trang tổng hợp.

## Notes

Lỗi True SSO thường nằm ở certificate, enrollment, domain trust hoặc cấu hình identity provider.

