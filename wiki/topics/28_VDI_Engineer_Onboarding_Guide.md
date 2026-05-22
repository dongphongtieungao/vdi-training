# VDI Engineer Onboarding Guide

## 0. Document Control

| Trường | Giá trị |
|---|---|
| Thứ tự | 28 |
| Tên tài liệu | VDI Engineer Onboarding Guide |
| Tên file | 28_VDI_Engineer_Onboarding_Guide.md |
| Mục đích tài liệu | Cung cấp lộ trình học và thực hành cho engineer mới, từ kiến thức nền tảng đến đọc kiến trúc, thao tác quản trị, xử lý incident và tham gia vận hành khách hàng. |
| Nguồn điều khiển | [[sources/vdi-training-idea]], [[sources/vdi-documentation-list-context]] |
| Trạng thái | Tài liệu onboarding đào tạo; access thực tế, lab, mentor, SLA, tool, checklist sign-off và quyền thao tác là Need Customer Confirmation |

### Source Grounding

| Nội dung | Nguồn sử dụng | Mức độ tin cậy | Ghi chú |
|---|---|---|---|
| Bối cảnh khách hàng có hai hệ thống VDI, quy mô 1500-2000+ VDI, cần đào tạo engineer theo lớp vận hành | [[sources/vdi-training-idea]] | High | Nguồn điều khiển chính cho lộ trình onboarding. |
| Tên tài liệu, tên file và mục đích tài liệu | [[sources/vdi-documentation-list-context]] | High | Source of truth cho scope file 28. |
| Kiến thức Horizon, UAG, Connection Server, Horizon Agent, connection flow | [[sources/horizon-8-architecture]], [[sources/understand-and-troubleshoot-horizon-connections]], [[concepts/omnissa-horizon]], [[concepts/connection-server]], [[concepts/unified-access-gateway]] | High | Dùng cho track Horizon. |
| Kiến thức Citrix CVAD, Delivery Controller, StoreFront, Gateway, VDA, Delivery Group | [[sources/citrix-virtual-apps-and-desktops-7-2603]], [[concepts/citrix-virtual-apps-and-desktops]], [[concepts/delivery-controller]], [[concepts/storefront]], [[concepts/virtual-delivery-agent]], [[concepts/delivery-group]] | High | Dùng cho track Citrix. |
| Kiến thức hypervisor, storage, profile, monitoring, incident, change, support | [[sources/fslogix-documentation]], [[sources/vmware-vsphere-8-0]], [[sources/vcenter-server-installation-and-setup]], [[sources/xenserver-8-4]], [[concepts/vcenter-server]], [[concepts/xenserver]], [[concepts/datastore]], [[concepts/profile-container]], [[concepts/monitoring-and-logs]], [[concepts/incident-management]], [[concepts/change-management]] | High | Dùng cho track vận hành thực tế. |

## 1. Mục tiêu onboarding

Tài liệu này là lộ trình học và thực hành cho system engineer mới tiếp cận hệ thống VDI của khách hàng. Mục tiêu không phải biến engineer thành chuyên gia Citrix/Horizon trong vài ngày. Mục tiêu thực tế hơn: engineer hiểu bức tranh tổng thể, đọc được sơ đồ, biết đặt câu hỏi đúng, biết kiểm tra theo lớp, biết thu thập evidence, biết giới hạn quyền của mình và biết escalation đúng đội.

Sau onboarding, engineer cần:

- Hiểu khách hàng có hai nền tảng VDI: Omnissa Horizon trên HCI và Citrix CVAD trên XenServer hoặc VMware ESXi.
- Giải thích được luồng user từ endpoint tới gateway, broker, desktop/app session và backend.
- Phân biệt được các khái niệm: broker, gateway, VDA, Horizon Agent, pool, catalog, delivery group, entitlement, profile, datastore, image, session.
- Biết đọc dashboard cơ bản: session, failed session, registered/unregistered, broker/gateway health, host/storage/network metric.
- Biết xử lý ticket support ở mức L1/L2 theo evidence, không thao tác cảm tính.
- Biết khi nào một việc là service request, incident, change hoặc escalation.
- Biết chuẩn bị tham gia vận hành khách hàng mà không bịa version, topology, SLA hoặc owner khi chưa xác nhận.

## 2. Đối tượng sử dụng

Tài liệu phù hợp cho:

- Engineer mới vào đội VDI.
- System engineer đã biết Windows/VMware nhưng chưa quen Horizon hoặc Citrix.
- Helpdesk nâng cấp vai trò lên L2 VDI support.
- Engineer network/storage/identity cần hiểu VDI dependency để phối hợp incident.
- Technical lead dùng làm checklist mentor cho thành viên mới.

Kiến thức đầu vào tối thiểu:

- Biết cơ bản về Windows user, domain account, VM, IP/DNS, ticket và monitoring.
- Không bắt buộc đã có kinh nghiệm Citrix CVAD hoặc Omnissa Horizon.
- Nếu chưa biết virtualization, đọc kỹ phần foundation, hypervisor và storage trước khi xử lý ticket.

## 3. Nguyên tắc học VDI cho engineer mới

1. **Học theo lớp, không học theo nút bấm.** Console thay đổi theo version, nhưng lớp user access, gateway, broker, agent, identity, hypervisor, storage và network luôn cần hiểu.
2. **Đọc symptom như một tín hiệu, không phải root cause.** "Không vào được VDI" có thể là account, gateway, entitlement, agent, profile hoặc storage.
3. **Luôn hỏi recent change.** Image, policy, certificate, patch, host maintenance hoặc entitlement change thường liên quan incident.
4. **Không thao tác production khi chưa rõ quyền và SOP.** Engineer mới nên quan sát, kiểm tra read-only và validate cùng mentor trước.
5. **Evidence là ngôn ngữ chung.** Ticket tốt có timestamp, user, resource, screenshot/log, scope, checks done và request escalation rõ.
6. **Unknown là câu trả lời hợp lệ.** Nếu chưa có version, topology, owner, SLA, profile solution hoặc monitoring tool, ghi Need Customer Confirmation.

## 4. Lộ trình đọc tài liệu

### Phase 1: Foundation và landscape

| Thứ tự | Tài liệu | Mục tiêu học |
|---|---|---|
| 1 | [[topics/1_VDI_Foundation_Overview]] | Hiểu VDI là gì, desktop ảo, published app, session và các lớp hạ tầng. |
| 2 | [[topics/2_Customer_VDI_Landscape_Overview]] | Hiểu khách hàng có hai hệ thống VDI, quy mô và phạm vi vận hành. |
| 27 | [[topics/27_VDI_Glossary_and_Concept_Dictionary]] | Nắm thuật ngữ cốt lõi trước khi đọc sâu. |

Kết quả cần đạt: engineer có thể giải thích bằng lời của mình "user mở VDI đi qua những lớp nào" và "Horizon khác Citrix ở các thành phần chính nào".

### Phase 2: Architecture và access flow

| Thứ tự | Tài liệu | Mục tiêu học |
|---|---|---|
| 3 | [[topics/3_Omnissa_Horizon_Architecture_Overview]] | Hiểu Connection Server, UAG, Horizon Agent, desktop pool, entitlement. |
| 4 | [[topics/4_Citrix_CVAD_Architecture_Overview]] | Hiểu Delivery Controller, StoreFront, Gateway, VDA, Catalog, Delivery Group. |
| 5 | [[topics/5_VDI_Access_Flow_Design]] | Đọc được luồng internal và external access. |

Kết quả cần đạt: engineer vẽ được sơ đồ đơn giản cho internal user và external user trên cả hai nền tảng.

### Phase 3: Dependency nền tảng

| Thứ tự | Tài liệu | Mục tiêu học |
|---|---|---|
| 6 | [[topics/6_Identity_and_Domain_Integration_Guide]] | Hiểu AD, DC, DNS, GPO, group, computer account. |
| 7 | [[topics/7_Hypervisor_and_HCI_Operations_Guide]] | Hiểu ESXi, vCenter, XenServer, HCI, host, VM lifecycle. |
| 8 | [[topics/8_Storage_Operations_for_VDI]] | Hiểu datastore, profile storage, image storage, latency, IOPS. |
| 9 | [[topics/9_Network_Operations_for_VDI]] | Hiểu VLAN, firewall, LB, DNS, certificate, latency, packet loss. |

Kết quả cần đạt: engineer biết lỗi VDI không phải lúc nào cũng nằm trong VDI console; identity, storage, network và hypervisor có thể là root cause.

### Phase 4: Day-to-day operations

| Thứ tự | Tài liệu | Mục tiêu học |
|---|---|---|
| 10 | [[topics/10_VDI_Security_and_Policy_Management_Guide]] | Hiểu policy và security controls ảnh hưởng user experience. |
| 11 | [[topics/11_VDI_Provisioning_and_Allocation_Guide]] | Hiểu tạo mới, cấp quyền, mở rộng, thu hồi VDI. |
| 12 | [[topics/12_Master_Image_Management_Guide]] | Hiểu lifecycle và rủi ro master image. |
| 13 | [[topics/13_Citrix_Machine_Catalog_and_Delivery_Group_Guide]] | Hiểu vận hành Catalog/DG trong Citrix. |
| 14 | [[topics/14_Omnissa_Desktop_Pool_and_Entitlement_Guide]] | Hiểu vận hành pool/entitlement trong Horizon. |
| 15 | [[topics/15_VDI_Monitoring_and_Alerting_Guide]] | Biết đọc metric và triage alert. |
| 16 | [[topics/16_Daily_Operations_Checklist]] | Biết checklist đầu ca/cuối ca. |

Kết quả cần đạt: engineer có thể thực hiện health check read-only, đọc state cơ bản và ghi evidence.

### Phase 5: Incident, troubleshooting và support

| Thứ tự | Tài liệu | Mục tiêu học |
|---|---|---|
| 17 | [[topics/17_VDI_Incident_Classification_Guide]] | Biết phân loại impact/priority theo phạm vi. |
| 18 | [[topics/18_VDI_Troubleshooting_Playbook]] | Biết playbook xử lý symptom phổ biến. |
| 25 | [[topics/25_VDI_Support_and_Escalation_Guide]] | Biết hỗ trợ user, thu thập evidence và escalation. |
| 26 | [[topics/26_VDI_Operational_Knowledge_Base]] | Biết dùng KB pattern trong ca trực. |

Kết quả cần đạt: engineer xử lý được ticket giả lập từ intake tới escalation package.

### Phase 6: Change, patch, recovery và governance

| Thứ tự | Tài liệu | Mục tiêu học |
|---|---|---|
| 19 | [[topics/19_VDI_Performance_and_Capacity_Guide]] | Hiểu capacity và bottleneck. |
| 20 | [[topics/20_VDI_Change_Management_Guide]] | Hiểu precheck, impact, rollback, evidence. |
| 21 | [[topics/21_VDI_Patch_and_Upgrade_Guide]] | Hiểu patch/upgrade theo compatibility, pilot, batch. |
| 22 | [[topics/22_VDI_Backup_and_Recovery_Guide]] | Hiểu đối tượng backup và validation restore. |
| 23 | [[topics/23_VDI_High_Availability_and_Disaster_Recovery_Guide]] | Hiểu HA/DR, failover, failback, DR drill. |
| 24 | [[topics/24_VDI_Access_Control_and_RBAC_Guide]] | Hiểu least privilege và role vận hành. |

Kết quả cần đạt: engineer biết việc nào cần change, việc nào cần approval, việc nào không được tự làm.

## 5. Onboarding timeline đề xuất

Timeline dưới đây là khung đào tạo. Thời lượng thật phụ thuộc kinh nghiệm engineer và mức độ access/lab khách hàng cung cấp.

| Giai đoạn | Thời lượng gợi ý | Mục tiêu | Output |
|---|---:|---|---|
| Day 1-2 | 2 ngày | Foundation, landscape, glossary | Engineer giải thích được bức tranh tổng thể |
| Day 3-5 | 3 ngày | Horizon/Citrix architecture và access flow | Engineer vẽ được 2 luồng internal/external |
| Week 2 | 5 ngày | Identity, hypervisor, storage, network, monitoring | Engineer đọc được dashboard và dependency |
| Week 3 | 5 ngày | Provisioning, image, pool/catalog, daily operation | Engineer làm được checklist read-only và ticket giả lập |
| Week 4 | 5 ngày | Incident, troubleshooting, support/escalation | Engineer xử lý scenario dưới giám sát mentor |
| Week 5-6 | 1-2 tuần | Change, patch, backup, HA/DR, RBAC | Engineer tham gia shadow change/incident thực tế |
| Sign-off | Sau đánh giá | Sẵn sàng trực có giám sát hoặc nhận task L2 | Mentor sign-off theo checklist |

Nếu engineer đã có kinh nghiệm VDI, có thể rút ngắn Phase 1-3 nhưng không nên bỏ qua phần customer landscape và Need Customer Confirmation.

## 6. Kỹ năng cần đạt theo cấp độ

### Level 0: Quan sát có định hướng

Engineer có thể:

- Đọc tài liệu foundation và glossary.
- Nêu được các thành phần Horizon/Citrix chính.
- Theo dõi mentor xử lý ticket và ghi lại flow.
- Không thao tác production ngoài quyền read-only.

Chưa nên:

- Reset session, reboot VDI, thay entitlement hoặc chỉnh policy.
- Escalate ticket khi chưa được review.

### Level 1: Read-only triage

Engineer có thể:

- Nhận ticket và hỏi thông tin tối thiểu.
- Xác định lỗi ở bước login, enumeration, launch, session, profile hay app.
- Xem dashboard/session/machine state theo quyền.
- Thu thập evidence và đề xuất lớp escalation.
- Chạy checklist daily operation read-only.

Chưa nên:

- Thực hiện thay đổi cấu hình.
- Xử lý incident diện rộng một mình.

### Level 2: Guided operation

Engineer có thể:

- Reset/logoff session hoặc restart VDI theo SOP và có user confirmation.
- Kiểm tra entitlement/group mapping và đề xuất action.
- Tham gia xử lý incident dưới giám sát.
- Viết escalation package tốt.
- Cập nhật KB sau khi mentor review.

Chưa nên:

- Publish image, patch broker/gateway, thay policy diện rộng, restore profile hoặc thao tác destructive.

### Level 3: Supervised change participation

Engineer có thể:

- Chuẩn bị precheck cho image/policy/entitlement/patch change.
- Ghi evidence trong maintenance window.
- Thực hiện postcheck login/launch/registration/monitoring.
- Phân tích rollback condition.
- Tham gia DR drill hoặc restore validation.

Chưa nên:

- Tự lead change rủi ro cao nếu chưa được sign-off.

### Level 4: Independent operations with escalation discipline

Engineer có thể:

- Trực vận hành theo ca.
- Lead triage incident mức vừa.
- Phối hợp network/storage/IAM/hypervisor/security owner.
- Thực hiện change đã được phê duyệt trong phạm vi role.
- Hướng dẫn engineer mới hơn theo checklist.

Điều kiện: hiểu rõ customer-specific SOP, topology, owner, SLA, escalation path và quyền RBAC.

## 7. Bài tập tư duy bắt buộc

### Exercise 1: Vẽ luồng truy cập

Vẽ hai luồng:

- User nội bộ vào Horizon hoặc Citrix.
- User bên ngoài vào Horizon hoặc Citrix.

Phải đánh dấu các lớp: endpoint, gateway, broker/portal, agent/VDA, identity, hypervisor, storage, network, monitoring.

### Exercise 2: Phân loại 10 ticket mẫu

Phân loại các ticket sau theo lớp lỗi và evidence cần lấy:

| Ticket mẫu | Lớp nghi ngờ | Evidence cần lấy |
|---|---|---|
| User login fail | Identity/Gateway/Broker | Account, timestamp, error, auth log |
| User không thấy desktop | Entitlement/Broker | Group, resource mapping, pool/DG state |
| Launch timeout external-only | Gateway/Network/Protocol | Internal/external comparison, gateway/LB |
| VDA unregistered | Agent/Identity/Network/Image | Machine list, event log, DNS, recent image |
| Black screen sau image update | Image/Agent/Profile/Display | Image version, session log, affected scope |
| Login chậm đầu giờ | Profile/Storage/DC/GPO | Login phase, storage/DC metrics |
| Printer không map | Policy/Endpoint/Driver | Policy result, client, printer info |
| Nhiều VDI powered off | Hypervisor/Power policy | VM/host state, recent change |
| Datastore latency alert | Storage/Capacity | Latency trend, affected VDI |
| User mất profile | Profile/Storage/Restore | Profile log, path, backup point |

### Exercise 3: Viết escalation package

Chọn một ticket launch fail và viết handoff gồm:

- Ticket ID giả định.
- User/resource/timestamp.
- Access path.
- Symptom.
- Checks done.
- Evidence.
- Suspected layer.
- Request to receiving team.

### Exercise 4: Đọc change plan

Cho một change "publish image mới cho 300 VDI", hãy chỉ ra:

- Precheck còn thiếu.
- Impact assessment.
- Pilot plan.
- Stop condition.
- Rollback point.
- Postcheck.
- Evidence cần lưu.

### Exercise 5: Đánh giá readiness của bản thân

Engineer tự trả lời:

- Tôi có thể giải thích broker/gateway/agent khác nhau chưa?
- Tôi có biết ticket nào phải escalation network/storage/IAM chưa?
- Tôi có biết evidence cần lấy trước khi reset/reboot chưa?
- Tôi có biết khi nào không được thao tác production chưa?

## 8. Checklist sẵn sàng trước khi tham gia vận hành

### 8.1 Kiến thức nền

- [ ] Hiểu VDI là gì và khác published app thế nào.
- [ ] Hiểu hai hệ thống khách hàng: Horizon on HCI và Citrix CVAD on XenServer/ESXi.
- [ ] Biết thuật ngữ broker, gateway, VDA, Horizon Agent, pool, catalog, DG, entitlement, profile, datastore, image.
- [ ] Biết luồng internal và external user.

### 8.2 Kỹ năng kiểm tra

- [ ] Biết đọc session state và failed session.
- [ ] Biết kiểm tra registered/unregistered.
- [ ] Biết kiểm tra user/resource entitlement ở mức read-only.
- [ ] Biết xem host/datastore/network/profile metric cơ bản.
- [ ] Biết thu thập screenshot/log/metric an toàn.

### 8.3 Quy trình

- [ ] Biết phân biệt service request, incident, change, problem/KB.
- [ ] Biết priority/impact theo phạm vi affected user/resource.
- [ ] Biết escalation path hoặc biết ghi Unknown để hỏi.
- [ ] Biết change nào cần approval.
- [ ] Biết không ghi secret/password/token vào ticket.

### 8.4 Thực hành

- [ ] Đã shadow ít nhất một ca daily health check.
- [ ] Đã shadow ít nhất một ticket user issue.
- [ ] Đã viết ít nhất một escalation package giả lập.
- [ ] Đã đọc một change plan và chỉ ra rollback/postcheck.
- [ ] Đã giải thích lại một KB entry cho mentor.

## 9. Mentor sign-off checklist

Mentor có thể dùng bảng này để đánh giá readiness.

| Năng lực | Tiêu chí đạt | Kết quả |
|---|---|---|
| Foundation | Giải thích được VDI service theo lớp | Pending/Pass |
| Horizon basics | Nêu được vai trò Client, UAG, Connection Server, Agent, Pool, Entitlement | Pending/Pass |
| Citrix basics | Nêu được vai trò Workspace/StoreFront/Gateway/Controller/VDA/Catalog/DG | Pending/Pass |
| Access flow | Vẽ được internal/external flow và điểm lỗi | Pending/Pass |
| Identity | Biết kiểm tra account/group/DNS/GPO ở mức phù hợp | Pending/Pass |
| Infra dependency | Biết host/datastore/network/profile ảnh hưởng VDI thế nào | Pending/Pass |
| Monitoring | Đọc được các metric session/registration/failed/session/storage cơ bản | Pending/Pass |
| Support | Viết được ticket intake và escalation package | Pending/Pass |
| Incident | Phân loại được impact và urgency | Pending/Pass |
| Change | Nhận diện được precheck/rollback/postcheck | Pending/Pass |
| Security | Biết RBAC, least privilege và không yêu cầu secret | Pending/Pass |
| Judgment | Biết khi nào dừng và escalation | Pending/Pass |

## 10. Common mistakes của engineer mới

| Sai lầm | Vì sao nguy hiểm | Cách sửa |
|---|---|---|
| Thấy user lỗi là reboot VDI | Mất evidence và có thể làm mất work chưa lưu | Khoanh vùng login/enumeration/launch/session trước |
| Nhầm gateway với broker | Escalate sai đội, kiểm tra sai lớp | Vẽ lại access flow |
| Chỉ xem VM powered on | VM bật nhưng Agent/VDA có thể unregistered | Kiểm tra registration và launch |
| Quên hỏi internal/external | Bỏ qua gateway/network path | Luôn hỏi access path |
| Không hỏi recent change | Bỏ qua nguyên nhân sau image/policy/patch | Check change calendar/ticket |
| Lưu log có dữ liệu nhạy cảm | Rủi ro security/audit | Chỉ lưu excerpt an toàn |
| Đóng ticket khi task completed | User chưa validate, lỗi quay lại | Cần user/monitoring confirmation |
| Escalate bằng câu "nhờ kiểm tra" | Đội nhận thiếu dữ liệu | Gửi evidence package |
| Học từng console riêng lẻ | Không hiểu dependency | Học theo lớp kiến trúc |

## 11. Scenario Based Learning

### Scenario 1: Engineer mới nhận ticket "không vào được VDI"

**Bối cảnh:** User báo "em không vào được VDI" qua ticket, không có screenshot.

**Yêu cầu:** Viết 8 câu hỏi hoặc thông tin cần bổ sung.

**Gợi ý đáp án:** Username, timestamp, internal/external, client/browser, lỗi ở login hay launch, resource name, screenshot/error text, user khác có bị không, recent password/group change.

**Điểm học:** Không xử lý khi symptom còn mơ hồ.

### Scenario 2: Mentor hỏi "Citrix launch fail thì kiểm tra gì?"

**Yêu cầu:** Trả lời theo lớp.

**Gợi ý đáp án:** StoreFront/resource visible, Delivery Controller failed session, Delivery Group/machine availability, VDA registration, VM power, Gateway/ICA path nếu external, profile/app nếu session mở rồi lỗi.

**Điểm học:** Không nhảy thẳng vào VDA hoặc reboot VM.

### Scenario 3: Sau image update nhiều Horizon desktop Agent unreachable

**Yêu cầu:** Xác định đây là incident hay change rollback candidate.

**Gợi ý đáp án:** Nếu nhiều desktop cùng pool sau image update bị Agent unreachable, dừng rollout, thu thập image version/registration/event log, cân nhắc rollback theo change plan và escalation image/platform owner.

**Điểm học:** Recent change rất quan trọng.

### Scenario 4: Daily health check thấy datastore latency tăng

**Yêu cầu:** Engineer mới nên làm gì?

**Gợi ý đáp án:** Kiểm tra affected datastore/pool, session/login impact, alert trend, recent provisioning/reboot storm, lưu screenshot metric và escalation storage/hypervisor nếu vượt baseline hoặc có user impact.

**Điểm học:** Alert hạ tầng có thể là sự cố VDI sớm.

## 12. Knowledge Check

**Câu 1. Vì sao onboarding VDI phải học theo lớp?**  
Vì user symptom có thể đến từ nhiều lớp phụ thuộc: gateway, broker, agent, identity, hypervisor, storage, network, profile.

**Câu 2. Engineer mới nên thao tác production ở mức nào trước khi sign-off?**  
Chủ yếu read-only, health check, evidence collection và ticket triage dưới giám sát.

**Câu 3. Ba tài liệu đầu tiên nên đọc là gì?**  
Foundation, Customer Landscape và Glossary để có bức tranh tổng thể và thuật ngữ.

**Câu 4. Khi user login được nhưng không thấy desktop, nên đọc tài liệu nào?**  
Provisioning/Allocation, Citrix Catalog/DG hoặc Horizon Pool/Entitlement tùy nền tảng.

**Câu 5. Khi nào cần escalation thay vì tự xử lý?**  
Khi vượt quyền/SOP, impact rộng, có rủi ro dữ liệu/security, cần change, hoặc lỗi thuộc owner khác.

**Câu 6. Evidence tối thiểu của một ticket VDI là gì?**  
User, timestamp, access path, resource, symptom, screenshot/error, scope, checks done và recent change.

**Câu 7. Vì sao không nên học bằng cách nhớ nút trong console?**  
Console thay đổi theo version; hiểu lớp và dependency giúp xử lý đúng dù UI khác.

**Câu 8. Engineer sẵn sàng trực độc lập khi nào?**  
Khi hiểu customer topology/SOP/owner/SLA, có RBAC phù hợp, xử lý được triage và biết escalation đúng.

## 13. Need Customer Confirmation

Các thông tin cần khách hàng hoặc service owner xác nhận để onboarding thành chương trình thật:

- Version cụ thể của Horizon, CVAD, vCenter/ESXi, XenServer, Gateway/UAG, VDA/Horizon Agent.
- Topology thật: site, pod, broker, gateway, StoreFront, load balancer, pool/catalog/DG.
- Access flow thật cho internal và external user.
- Console/dashboard nào engineer mới được xem.
- RBAC cho trainee, helpdesk, system engineer, platform admin.
- Lab hoặc sandbox có không, hay chỉ shadow production.
- Ticket tool, queue, SLA, priority matrix.
- Escalation path và owner từng lớp.
- Change calendar và maintenance window.
- Profile solution, storage design, monitoring tool.
- Checklist mentor sign-off chính thức.
- Danh sách known issues và KB nội bộ hiện tại.
- Quy trình cấp quyền tạm và thu hồi quyền khi onboarding kết thúc.

## 14. Related Wiki Links

### Source summaries

- [[sources/vdi-training-idea]]
- [[sources/vdi-documentation-list-context]]
- [[sources/horizon-8-architecture]]
- [[sources/understand-and-troubleshoot-horizon-connections]]
- [[sources/citrix-virtual-apps-and-desktops-7-2603]]
- [[sources/fslogix-documentation]]
- [[sources/vmware-vsphere-8-0]]
- [[sources/vcenter-server-installation-and-setup]]
- [[sources/xenserver-8-4]]

### Core concept links

- [[concepts/vdi-training-program]]
- [[concepts/vdi-operational-readiness]]
- [[concepts/vdi-documentation-architecture]]
- [[concepts/vdi-connection-flow]]
- [[concepts/omnissa-horizon]]
- [[concepts/citrix-virtual-apps-and-desktops]]
- [[concepts/identity-and-access-management]]
- [[concepts/monitoring-and-logs]]
- [[concepts/incident-management]]
- [[concepts/change-management]]

### Full topic path

- [[topics/1_VDI_Foundation_Overview]]
- [[topics/2_Customer_VDI_Landscape_Overview]]
- [[topics/3_Omnissa_Horizon_Architecture_Overview]]
- [[topics/4_Citrix_CVAD_Architecture_Overview]]
- [[topics/5_VDI_Access_Flow_Design]]
- [[topics/6_Identity_and_Domain_Integration_Guide]]
- [[topics/7_Hypervisor_and_HCI_Operations_Guide]]
- [[topics/8_Storage_Operations_for_VDI]]
- [[topics/9_Network_Operations_for_VDI]]
- [[topics/10_VDI_Security_and_Policy_Management_Guide]]
- [[topics/11_VDI_Provisioning_and_Allocation_Guide]]
- [[topics/12_Master_Image_Management_Guide]]
- [[topics/13_Citrix_Machine_Catalog_and_Delivery_Group_Guide]]
- [[topics/14_Omnissa_Desktop_Pool_and_Entitlement_Guide]]
- [[topics/15_VDI_Monitoring_and_Alerting_Guide]]
- [[topics/16_Daily_Operations_Checklist]]
- [[topics/17_VDI_Incident_Classification_Guide]]
- [[topics/18_VDI_Troubleshooting_Playbook]]
- [[topics/19_VDI_Performance_and_Capacity_Guide]]
- [[topics/20_VDI_Change_Management_Guide]]
- [[topics/21_VDI_Patch_and_Upgrade_Guide]]
- [[topics/22_VDI_Backup_and_Recovery_Guide]]
- [[topics/23_VDI_High_Availability_and_Disaster_Recovery_Guide]]
- [[topics/24_VDI_Access_Control_and_RBAC_Guide]]
- [[topics/25_VDI_Support_and_Escalation_Guide]]
- [[topics/26_VDI_Operational_Knowledge_Base]]
- [[topics/27_VDI_Glossary_and_Concept_Dictionary]]

## 15. Summary for Learners

Onboarding VDI không kết thúc khi đọc xong tài liệu. Nó kết thúc khi engineer có thể nhìn một symptom, đặt câu hỏi đúng, kiểm tra theo lớp, lưu evidence, biết giới hạn quyền của mình và escalation đúng owner.

Thứ tự học khuyến nghị:

1. Foundation, landscape, glossary.
2. Horizon, Citrix, access flow.
3. Identity, hypervisor, storage, network.
4. Provisioning, image, pool/catalog, monitoring, daily operation.
5. Incident, troubleshooting, support, KB.
6. Performance, change, patch, backup, HA/DR, RBAC.
7. Shadow thực tế, scenario, mentor sign-off.

Điều cần nhớ nhất: engineer VDI giỏi không phải người nhớ mọi nút bấm. Đó là người hiểu hệ thống theo lớp, không bịa điều chưa biết, không thao tác vượt quyền, và luôn để lại evidence đủ rõ cho người tiếp theo.

## 16. Self Review

- [x] Đúng tên tài liệu trong list_context.txt.
- [x] Đúng tên file trong cột Name File.
- [x] Đúng mục đích: lộ trình học và thực hành cho engineer mới từ nền tảng đến vận hành khách hàng.
- [x] Bám bối cảnh training_idea.md: Horizon on HCI, Citrix CVAD trên XenServer/ESXi, quy mô 1500-2000+ VDI.
- [x] Không bịa version, topology, access, SLA, owner hoặc lab của khách hàng.
- [x] Có phân biệt Need Customer Confirmation.
- [x] Có reading path, timeline, skill levels, exercises, readiness checklist và mentor sign-off.
- [x] Có scenario, knowledge check và common mistakes.
- [x] Có liên kết tới toàn bộ topic trong bộ tài liệu.
- [x] Phù hợp cho system engineer mới chuẩn bị tham gia vận hành thực tế.
