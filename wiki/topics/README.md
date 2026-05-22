# VDI Training Documentation Index

## 1. Purpose

Đây là bộ tài liệu đào tạo tri thức VDI cho system engineer chuẩn bị tiếp cận hệ thống VDI quy mô lớn của khách hàng.

## 2. Source Corpus

- training_idea.md: [[sources/vdi-training-idea]]
- list_context.txt: [[sources/vdi-documentation-list-context]]
- raw/sources đã được ingest thành wiki/sources.
- raw/notes: chưa phát hiện nội dung bổ sung trong lượt này.
- wiki/sources và wiki/concepts được dùng để ground từng tài liệu.

## 3. Documentation List

| Thứ tự | Tên tài liệu | Tên file | Mục đích tài liệu | Trạng thái | Source coverage |
|---|---|---|---|---|---|
| 1 | VDI Foundation Overview | 1_VDI_Foundation_Overview.md | Cung cấp kiến thức nền tảng về VDI, khái niệm desktop ảo, published application, session, user access và các lớp hạ tầng liên quan. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 2 | Customer VDI Landscape Overview | 2_Customer_VDI_Landscape_Overview.md | Mô tả tổng quan hai hệ thống VDI của khách hàng, quy mô 1500 đến hơn 2000 VDI, nền tảng sử dụng và phạm vi vận hành cần nắm. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 3 | Omnissa Horizon Architecture Overview | 3_Omnissa_Horizon_Architecture_Overview.md | Giải thích kiến trúc Omnissa Horizon trên HCI, vai trò của Connection Server, Unified Access Gateway, Horizon Agent, desktop pool, entitlement, vCenter, storage và network. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 4 | Citrix CVAD Architecture Overview | 4_Citrix_CVAD_Architecture_Overview.md | Giải thích kiến trúc Citrix Virtual Apps and Desktops, vai trò của Delivery Controller, StoreFront, Citrix Gateway, VDA, Site Database, License Server, Machine Catalog và Delivery Group. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 5 | VDI Access Flow Design | 5_VDI_Access_Flow_Design.md | Mô tả luồng kết nối của người dùng nội bộ và người dùng bên ngoài vào hệ thống VDI, từ client đến gateway, broker, agent, desktop và application backend. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 6 | Identity and Domain Integration Guide | 6_Identity_and_Domain_Integration_Guide.md | Cung cấp kiến thức về Domain Controller, Active Directory, DNS, Group Policy, user group, computer account và khả năng tích hợp Hybrid Microsoft Entra ID. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 7 | Hypervisor and HCI Operations Guide | 7_Hypervisor_and_HCI_Operations_Guide.md | Giúp engineer hiểu lớp hạ tầng chạy VDI, gồm VMware ESXi, vCenter, XenServer nếu có, HCI cluster, host, datastore, resource pool, snapshot và VM lifecycle. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 8 | Storage Operations for VDI | 8_Storage_Operations_for_VDI.md | Giải thích vai trò của storage trong VDI, gồm datastore, profile storage, image storage, capacity, latency, IOPS, snapshot growth, boot storm và logon storm. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 9 | Network Operations for VDI | 9_Network_Operations_for_VDI.md | Mô tả các thành phần mạng cần vận hành như VLAN, routing, firewall, load balancer, DNS, certificate, gateway, latency, packet loss và bandwidth. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 10 | VDI Security and Policy Management Guide | 10_VDI_Security_and_Policy_Management_Guide.md | Hướng dẫn quản trị policy liên quan đến clipboard, USB, printer, drive mapping, session timeout, MFA, conditional access, RBAC và audit log. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 11 | VDI Provisioning and Allocation Guide | 11_VDI_Provisioning_and_Allocation_Guide.md | Mô tả quy trình tạo mới, cấp phát, mở rộng, thu hồi VDI, gán quyền user, gán AD group và kiểm tra trạng thái desktop sau cấp phát. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 12 | Master Image Management Guide | 12_Master_Image_Management_Guide.md | Hướng dẫn quản trị master image, cập nhật OS, application, agent, security tool, snapshot, publish image, kiểm thử image và rollback khi phát sinh lỗi. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 13 | Citrix Machine Catalog and Delivery Group Guide | 13_Citrix_Machine_Catalog_and_Delivery_Group_Guide.md | Giải thích cách quản trị Machine Catalog, Delivery Group, Application Group, entitlement, VDA registration và các tình huống vận hành thường gặp trong CVAD. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 14 | Omnissa Desktop Pool and Entitlement Guide | 14_Omnissa_Desktop_Pool_and_Entitlement_Guide.md | Giải thích cách quản trị desktop pool, application pool, entitlement, Horizon Agent registration, pool availability và các tình huống vận hành thường gặp trong Horizon. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 15 | VDI Monitoring and Alerting Guide | 15_VDI_Monitoring_and_Alerting_Guide.md | Xác định các chỉ số cần giám sát cho broker, gateway, VDI, session, host, storage, network, identity, license và profile service. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 16 | Daily Operations Checklist | 16_Daily_Operations_Checklist.md | Cung cấp checklist kiểm tra hàng ngày cho engineer, gồm health check, alert review, session status, VDI registration, host resource, datastore capacity và incident pending. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 17 | VDI Incident Classification Guide | 17_VDI_Incident_Classification_Guide.md | Hướng dẫn phân loại incident theo phạm vi ảnh hưởng như một user, một VDI, một pool, một catalog, một site, một gateway, một host cluster hoặc toàn bộ nền tảng. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 18 | VDI Troubleshooting Playbook | 18_VDI_Troubleshooting_Playbook.md | Cung cấp playbook xử lý lỗi phổ biến như login fail, không thấy desktop, launch fail, VDA unregistered, Horizon Agent unreachable, login chậm, black screen, disconnect và profile issue. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 19 | VDI Performance and Capacity Guide | 19_VDI_Performance_and_Capacity_Guide.md | Giúp engineer đánh giá hiệu năng và năng lực hệ thống qua CPU, memory, storage latency, IOPS, concurrent session, login duration, boot storm, logon storm và capacity trend. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 20 | VDI Change Management Guide | 20_VDI_Change_Management_Guide.md | Chuẩn hóa cách thực hiện thay đổi như image update, policy change, entitlement change, certificate change, broker patching, host maintenance và storage expansion. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 21 | VDI Patch and Upgrade Guide | 21_VDI_Patch_and_Upgrade_Guide.md | Mô tả nguyên tắc cập nhật Delivery Controller, StoreFront, Citrix Gateway, VDA, Connection Server, UAG, Horizon Agent, hypervisor tools và Windows patch. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 22 | VDI Backup and Recovery Guide | 22_VDI_Backup_and_Recovery_Guide.md | Xác định đối tượng cần backup và recovery như configuration, site database, master image, profile data, vCenter configuration, gateway configuration và tài liệu vận hành. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 23 | VDI High Availability and Disaster Recovery Guide | 23_VDI_High_Availability_and_Disaster_Recovery_Guide.md | Mô tả nguyên tắc HA và DR cho broker, gateway, database, storage, hypervisor, identity, profile service và các tình huống failover cần kiểm thử. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 24 | VDI Access Control and RBAC Guide | 24_VDI_Access_Control_and_RBAC_Guide.md | Chuẩn hóa quyền truy cập cho system engineer, helpdesk, platform admin, security admin và customer operator theo nguyên tắc phân quyền tối thiểu. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 25 | VDI Support and Escalation Guide | 25_VDI_Support_and_Escalation_Guide.md | Quy định cách hỗ trợ người dùng, thu thập evidence, xác định nhóm phụ trách, escalation theo lớp lỗi và thông tin cần cung cấp khi chuyển tuyến xử lý. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 26 | VDI Operational Knowledge Base | 26_VDI_Operational_Knowledge_Base.md | Tập hợp kiến thức ngắn gọn theo dạng lỗi thường gặp, kinh nghiệm xử lý, lệnh kiểm tra, màn hình quản trị và lưu ý khi vận hành thực tế. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 27 | VDI Glossary and Concept Dictionary | 27_VDI_Glossary_and_Concept_Dictionary.md | Giải thích thuật ngữ quan trọng như broker, VDA, Horizon Agent, pool, catalog, delivery group, entitlement, profile, gateway, datastore, session và image. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |
| 28 | VDI Engineer Onboarding Guide | 28_VDI_Engineer_Onboarding_Guide.md | Cung cấp lộ trình học và thực hành cho engineer mới, từ kiến thức nền tảng đến đọc kiến trúc, thao tác quản trị, xử lý incident và tham gia vận hành khách hàng. | Updated full training document | training_idea.md; list_context.txt; Document Research Pack; wiki/sources; wiki/concepts |

## 4. Recommended Learning Path

1. Foundation
2. Customer Landscape
3. Architecture
4. Access Flow
5. Identity
6. Hypervisor and HCI
7. Storage
8. Network
9. Security and Policy
10. Provisioning
11. Image Management
12. Monitoring
13. Daily Operation
14. Incident
15. Troubleshooting
16. Performance and Capacity
17. Change
18. Patch and Upgrade
19. Backup
20. HA and DR
21. RBAC
22. Support
23. Knowledge Base
24. Glossary
25. Onboarding

## 5. Concept Index

- [[concepts/vdi-connection-flow]]
- [[concepts/omnissa-horizon]]
- [[concepts/connection-server]]
- [[concepts/unified-access-gateway]]
- [[concepts/citrix-virtual-apps-and-desktops]]
- [[concepts/delivery-controller]]
- [[concepts/storefront]]
- [[concepts/virtual-delivery-agent]]
- [[concepts/delivery-group]]
- [[concepts/vmware-vsphere]]
- [[concepts/esxi]]
- [[concepts/vcenter-server]]
- [[concepts/xenserver]]
- [[concepts/datastore]]
- [[concepts/storage-repository]]
- [[concepts/profile-container]]
- [[concepts/cloud-cache]]
- [[concepts/identity-and-access-management]]
- [[concepts/firewall-ports]]
- [[concepts/load-balancing]]
- [[concepts/monitoring-and-logs]]
- [[concepts/incident-management]]
- [[concepts/change-management]]
- [[concepts/backup-and-recovery]]
- [[concepts/high-availability]]

## 6. Source Index

- [[sources/vdi-training-idea]] - training_idea.md
- [[sources/vdi-documentation-list-context]] - list_context.txt
- [[sources/horizon-8-architecture]] - Horizon 8 architecture
- [[sources/understand-and-troubleshoot-horizon-connections]] - Understand and Troubleshoot Horizon Connections
- [[sources/citrix-virtual-apps-and-desktops-7-2603]] - Citrix Virtual Apps and Desktops 7 2603
- [[sources/fslogix-documentation]] - FSLogix documentation
- [[sources/vmware-vsphere-8-0]] - VMware vSphere 8.0
- [[sources/vcenter-server-installation-and-setup]] - vCenter Server Installation and Setup
- [[sources/xenserver-8-4]] - XenServer 8.4

## 7. Need Customer Confirmation Summary

- Version thực tế của Horizon, CVAD, vCenter/ESXi, XenServer, gateway, Agent/VDA.
- Topology thật và access flow thật.
- HA/DR design, RPO/RTO và DR drill evidence.
- Monitoring tool, dashboard, alert threshold và ticket integration.
- Storage, network, profile solution, change process, SLA, escalation path và ownership.

## 8. Maintenance Guide

1. Chạy /lumi-ingest cho source mới.
2. Dùng /lumi-ask để khai thác tri thức mới.
3. Cập nhật concept liên quan trong wiki/concepts.
4. Cập nhật topic liên quan trong wiki/topics.
5. Chạy /lumi-check.
6. Chạy /lumi-verify nếu cần.
