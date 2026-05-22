# VDI Operational Knowledge Base

## 0. Document Control

| Trường | Giá trị |
|---|---|
| Thứ tự | 26 |
| Tên tài liệu | VDI Operational Knowledge Base |
| Tên file | 26_VDI_Operational_Knowledge_Base.md |
| Mục đích tài liệu | Tập hợp kiến thức ngắn gọn theo dạng lỗi thường gặp, kinh nghiệm xử lý, lệnh kiểm tra, màn hình quản trị và lưu ý khi vận hành thực tế. |
| Nguồn điều khiển | [[sources/vdi-training-idea]], [[sources/vdi-documentation-list-context]] |
| Trạng thái | Tài liệu đào tạo vận hành; console name, command set, log path, dashboard, KB workflow và owner thực tế là Need Customer Confirmation |

### Source Grounding

| Nội dung | Nguồn sử dụng | Mức độ tin cậy | Ghi chú |
|---|---|---|---|
| Bối cảnh hai hệ thống VDI, quy mô 1500-2000+ VDI và yêu cầu vận hành thực tế | [[sources/vdi-training-idea]] | High | Dùng làm nền cho KB vận hành. |
| Tên tài liệu, tên file và mục đích tài liệu | [[sources/vdi-documentation-list-context]] | High | Source of truth cho scope file 26. |
| Pattern Horizon: Connection Server, UAG, Horizon Agent, pool, entitlement, connection troubleshooting | [[sources/horizon-8-architecture]], [[sources/understand-and-troubleshoot-horizon-connections]], [[concepts/omnissa-horizon]], [[concepts/connection-server]], [[concepts/unified-access-gateway]] | High | Dùng cho thẻ KB Horizon. |
| Pattern Citrix CVAD: Delivery Controller, StoreFront, Gateway, VDA, Delivery Group | [[sources/citrix-virtual-apps-and-desktops-7-2603]], [[concepts/citrix-virtual-apps-and-desktops]], [[concepts/delivery-controller]], [[concepts/storefront]], [[concepts/virtual-delivery-agent]], [[concepts/delivery-group]] | High | Dùng cho thẻ KB Citrix. |
| Pattern profile, storage, hypervisor, monitoring, incident, change và support | [[sources/fslogix-documentation]], [[sources/vmware-vsphere-8-0]], [[sources/xenserver-8-4]], [[concepts/profile-container]], [[concepts/user-profile-management]], [[concepts/datastore]], [[concepts/vcenter-server]], [[concepts/xenserver]], [[concepts/monitoring-and-logs]], [[concepts/incident-management]], [[concepts/change-management]] | High | Dùng cho checklist, evidence và escalation pattern. |

## 1. Mục tiêu đào tạo

Operational Knowledge Base là nơi biến kinh nghiệm vận hành thành tri thức dùng lại. Khác với troubleshooting playbook, KB không cố mô tả mọi bước xử lý dài. KB cung cấp thẻ tri thức ngắn, rõ, có pattern nhận diện, câu hỏi chẩn đoán, màn hình cần xem, lệnh hoặc kiểm tra an toàn, evidence cần lưu và điều kiện escalation.

Sau khi đọc tài liệu này, engineer cần:

- Biết dùng KB để xử lý nhanh các lỗi VDI lặp lại mà không xử lý theo cảm tính.
- Biết cấu trúc một KB entry tốt cho Horizon, Citrix, identity, profile, storage, network, hypervisor và policy.
- Biết các pattern lỗi thường gặp: login fail, no resource, launch fail, Agent/VDA unregistered, black screen, disconnect, login chậm, profile issue, printer/USB/clipboard, storage latency.
- Biết khi nào một lỗi đã có KB nhưng vẫn cần escalation hoặc incident.
- Biết cập nhật KB sau incident/change để tri thức không nằm trong đầu một cá nhân.

Tài liệu này không thay thế SOP chi tiết hoặc troubleshooting playbook. Với lỗi phức tạp, dùng KB để định hướng ban đầu, sau đó đọc [[topics/18_VDI_Troubleshooting_Playbook]] và escalation theo [[topics/25_VDI_Support_and_Escalation_Guide]].

## 2. KB vận hành nên chứa gì

Một KB entry tốt nên trả lời nhanh 8 câu hỏi:

| Câu hỏi | Ý nghĩa |
|---|---|
| Symptom là gì? | User hoặc monitoring thấy gì. |
| Pattern nhận diện là gì? | Một user, nhiều user, external-only, cùng pool/catalog, sau change. |
| Lớp nghi ngờ đầu tiên là gì? | Identity, broker, gateway, agent, profile, storage, network, hypervisor, policy, application. |
| Kiểm tra ở đâu? | Console, dashboard, log, ticket, monitoring. |
| Lệnh/kiểm tra an toàn nào dùng được? | Chỉ lệnh read-only hoặc kiểm tra không phá hủy; command thật cần xác nhận theo môi trường. |
| Evidence cần lưu là gì? | Timestamp, screenshot, log excerpt, metric, user/resource. |
| Workaround hoặc hướng xử lý an toàn là gì? | Chỉ trong phạm vi SOP và quyền. |
| Khi nào escalation? | Impact rộng, dữ liệu, security, vượt quyền, không rõ root cause. |

KB không nên chứa password, token, private key, thông tin bí mật, dữ liệu user nhạy cảm hoặc hướng dẫn thao tác phá hủy thiếu approval.

## 3. Mẫu chuẩn cho một KB entry

```markdown
## KB-[ID] - [Tên lỗi ngắn]

### Symptom
- User/monitoring thấy gì?

### Pattern nhận diện
- Một user hay nhiều user?
- Internal hay external?
- Pool/catalog/DG nào?
- Có recent change không?

### Lớp cần kiểm tra
- Lớp 1:
- Lớp 2:
- Lớp 3:

### Kiểm tra nhanh
- Console/dashboard cần xem:
- Log/event cần xem:
- Kiểm tra/lệnh read-only nếu được phép:

### Evidence cần lưu
- Timestamp:
- User/resource:
- Screenshot/log/metric:

### Hướng xử lý an toàn
- Action trong SOP:
- Workaround nếu có:

### Escalation
- Chuyển đội nào:
- Gửi kèm gì:

### Related docs
- Link topic/concept/source:
```

Mỗi KB entry nên có owner và ngày review trong hệ thống thật. Nếu chưa có owner, ghi Need Customer Confirmation.

## 4. Bản đồ pattern lỗi theo lớp

| Pattern | Dấu hiệu nhanh | Lớp nghi ngờ | Màn hình cần xem | Evidence chính |
|---|---|---|---|---|
| Login fail | Không vào portal hoặc authentication fail | Identity, Gateway, Broker | AD/IAM, StoreFront/Horizon/UAG/Gateway, monitoring auth | User, timestamp, error, auth log |
| No resource | Login được nhưng không thấy desktop/app | Entitlement, AD group, Broker | Horizon entitlement, Citrix DG/App Group, AD group | Group mapping, resource state |
| Launch fail | Thấy resource nhưng mở không được | Broker, Agent/VDA, VM, protocol | Failed session, registration, VM power, gateway | Failed session, agent state |
| Unregistered | Desktop unavailable, VDA/Agent không nhận broker | Agent, DNS, domain, firewall, image | Citrix/Horizon machine state, event log, DNS | Machine list, event sample |
| Black screen | Session mở nhưng màn hình đen | Agent, display, profile, OS, security tool | Session log, profile log, image/version, display policy | Screenshot, session ID |
| Disconnect | Session rớt/reconnect liên tục | Network, Gateway, protocol, endpoint | Network metrics, gateway log, client version | Latency/loss, path |
| Login chậm | Preparing/loading profile/GPO lâu | Profile, GPO, storage, DC, logon script | Login duration, profile share, GPO, storage | Phase timing, metrics |
| Profile issue | Temporary profile, mất setting | Profile storage, permission, lock | Profile log, file share/container state | User sample, path, permission |
| Printer/USB/Clipboard | Redirect không hoạt động | Policy, client, driver, security | Citrix/Horizon policy, GPO, client capability | Effective policy, user group |
| Storage latency | Nhiều VDI chậm, boot/logon storm | Storage, datastore, host | Datastore latency, IOPS, capacity | Metric trend, affected pool |

## 5. KB entry: Login fail

### Symptom

User không đăng nhập được portal, bị authentication failed, account locked, MFA fail nếu có, hoặc nhận lỗi certificate/trust trước khi thấy resource.

### Pattern nhận diện

- Một user: kiểm tra account, password state, group, endpoint, MFA.
- Nhiều user cùng site: kiểm tra DC/DNS, gateway/portal, certificate, recent change.
- External-only: kiểm tra gateway, DNS public/internal split, certificate, firewall/LB.

### Kiểm tra nhanh

- Account có locked/disabled/expired không.
- User có thuộc đúng domain/UPN không.
- DC/DNS/time sync có alert không.
- Portal/gateway/broker service có healthy không.
- Certificate có cảnh báo client không.

### Kiểm tra/lệnh an toàn

- Kiểm tra DNS bằng `nslookup <portal-or-broker-name>` trên endpoint hoặc jump host được phép.
- Kiểm tra thời gian hệ thống bằng công cụ OS hoặc dashboard chuẩn.
- Kiểm tra trạng thái account và group trong console IAM/AD theo quyền được cấp.

Lệnh cụ thể cho AD, Horizon, Citrix hoặc gateway phải theo SOP khách hàng; không ghi credential vào ticket.

### Evidence cần lưu

Timestamp, username, access path, screenshot lỗi, portal/gateway/broker log excerpt nếu có, account state, recent change.

### Escalation

- IAM nếu account, group, DC, MFA, GPO hoặc time sync bất thường.
- Network/Gateway nếu external-only hoặc certificate/DNS/LB nghi vấn.
- VDI platform nếu broker/portal authentication service lỗi.

## 6. KB entry: Login được nhưng không thấy desktop/app

### Symptom

User vào portal được nhưng danh sách desktop/app trống hoặc thiếu resource mong muốn.

### Pattern nhận diện

- User mới onboard: nghi AD group/entitlement chưa đúng.
- Một nhóm user: nghi mapping AD group với pool/DG/app group.
- Sau change entitlement/policy: nghi thay đổi quyền.
- Resource vẫn visible với user khác: nghi user/group cụ thể.

### Kiểm tra nhanh

- User có trong đúng AD group không.
- AD group có được map vào Horizon pool hoặc Citrix Delivery Group/Application Group không.
- Pool/catalog/DG/application group có enabled không.
- Có available machines không.
- Có license/resource capacity alert không.

### Evidence cần lưu

User, expected resource, group membership, entitlement/DG mapping, screenshot portal, resource state, ticket approval.

### Hướng xử lý an toàn

Không tự thêm user vào group rộng hơn để "fix nhanh". Chỉ sửa quyền theo request/approval và ghi evidence before/after.

### Escalation

- IAM nếu group membership hoặc replication có vấn đề.
- VDI platform nếu mapping đúng nhưng broker không enumerate resource.

## 7. KB entry: Launch fail

### Symptom

User thấy desktop/app nhưng khi bấm mở thì timeout, lỗi launch, không tạo session hoặc mở rồi đóng ngay.

### Pattern nhận diện

- External-only: nghi gateway/protocol path.
- Cùng pool/catalog: nghi Agent/VDA, image, resource availability.
- Sau patch/image: nghi agent/image/security tool.
- Một user: kiểm tra assignment, profile, endpoint.

### Kiểm tra nhanh

- Failed session trong broker/monitoring.
- VDA/Horizon Agent registered không.
- VM powered on và không maintenance mode.
- Pool/catalog/DG có available machines không.
- Gateway/LB/protocol path có alert không.

### Evidence cần lưu

Failed session ID hoặc screenshot, resource name, machine name nếu có, registration state, VM state, internal/external comparison, recent change.

### Escalation

- VDI platform nếu broker/agent/resource selection lỗi.
- Network/Gateway nếu external-only hoặc protocol timeout.
- Hypervisor nếu VM power/host issue.

## 8. KB entry: VDA/Horizon Agent unregistered

### Symptom

Desktop hiển thị unavailable, unregistered, agent unreachable hoặc không nhận session.

### Pattern nhận diện

- Một máy: service/VM/domain/DNS cục bộ.
- Nhiều máy cùng image: image/agent version/security tool.
- Nhiều máy cùng host/datastore: hypervisor/storage/network.
- Sau patch/change: quay lại change timeline.

### Kiểm tra nhanh

- VM powered on không.
- Agent/VDA service có running không nếu có quyền xem.
- DNS forward/reverse và domain join có bất thường không.
- Firewall path tới broker có thay đổi không.
- Broker list/controller list cấu hình đúng không.
- Time sync có lệch không.

### Evidence cần lưu

Machine list, affected pool/catalog, registration dashboard, event log sample, image/version, recent change, DNS/domain evidence.

### Hướng xử lý an toàn

Không reboot hàng loạt khi chưa hiểu pattern. Nếu nhiều máy cùng batch/image unregistered, dừng rollout và escalation image/platform.

## 9. KB entry: Black screen

### Symptom

User launch thành công nhưng màn hình đen, desktop không load shell, hoặc app không render.

### Pattern nhận diện

- Sau image/agent/Windows patch: nghi agent, display driver, shell, security tool.
- Một user: nghi profile, policy, endpoint.
- Nhiều user cùng pool/catalog: nghi image/policy/agent.
- External-only: nghi protocol/gateway/network.

### Kiểm tra nhanh

- Session thực sự active hay disconnected.
- Event log trên desktop nếu có quyền.
- Profile có load đúng không.
- Display protocol/policy có thay đổi không.
- CPU/memory của VM có bất thường không.
- Security/AV có chặn shell/app không.

### Evidence cần lưu

Screenshot, user/session, machine name, image version, policy before/after nếu có, profile log, event sample.

### Escalation

VDI platform/image owner nếu nhiều user cùng image; profile/storage nếu liên quan profile; security nếu security tool/policy nghi vấn.

## 10. KB entry: Login chậm

### Symptom

User mất nhiều thời gian ở preparing desktop, applying policy, loading profile hoặc launching application.

### Pattern nhận diện

- Đầu giờ sáng: logon storm, storage/profile/DC bottleneck.
- Một user: profile lớn/corrupt, GPO/user-specific script.
- Nhiều user cùng site: DC/DNS/storage/network.
- Sau policy/image change: GPO, logon script, AV/security scan.

### Kiểm tra nhanh

- Login duration theo phase nếu tool có.
- GPO processing time.
- Profile load time và profile log.
- Storage latency/IOPS/capacity.
- DC latency/auth errors.
- Host CPU/memory contention.

### Evidence cần lưu

Sample users, timestamp, login phase, GPO/profile/storage/DC/host metrics, recent change, affected scope.

### Escalation

Storage/profile owner nếu profile/storage evidence rõ; IAM nếu GPO/DC; hypervisor nếu host contention; VDI platform nếu broker/session metrics bất thường.

## 11. KB entry: Profile issue

### Symptom

Temporary profile, mất desktop icon, app setting reset, profile container không attach hoặc user báo mất dữ liệu cá nhân.

### Pattern nhận diện

- Một user: profile corrupt/permission/lock.
- Nhiều user: profile share/storage/path/permission.
- Sau DR/failover: profile path/replication/Cloud Cache nếu có.
- Sau security/AV change: file lock hoặc scan.

### Kiểm tra nhanh

- Profile solution thật là gì: FSLogix, Citrix Profile Management, roaming profile hay khác.
- Profile path/container có truy cập được không.
- Permission/ownership có đúng không.
- Có lock file/session cũ không.
- Storage capacity/latency có bất thường không.

### Evidence cần lưu

User, profile path hoặc container metadata an toàn, error log, permission evidence, storage metric, restore/backup point nếu cần.

### Lưu ý

Không restore đè profile khi chưa hiểu thời điểm lỗi và policy retention. Profile có thể chứa dữ liệu nhạy cảm.

## 12. KB entry: Printer, USB, clipboard, drive mapping

### Symptom

User không in được, không copy/paste được, USB không redirect hoặc drive không map vào session.

### Pattern nhận diện

- Một user/endpoint: client capability, driver, endpoint policy.
- Một group: Citrix/Horizon policy, GPO, AD group scope.
- Sau security change: policy chặn có chủ đích hoặc scope sai.

### Kiểm tra nhanh

- User thuộc group policy nào.
- Policy Citrix/Horizon/GPO effective là gì.
- Client hỗ trợ tính năng không.
- Printer/USB/drive có bị chặn theo network location hoặc device type không.
- Có exception được approval không.

### Evidence cần lưu

User/group, policy result, client version, device/printer name nếu được phép, screenshot lỗi, change ID nếu có.

### Escalation

Security/platform nếu policy scope sai hoặc cần exception; endpoint/helpdesk nếu driver/client; application owner nếu app-specific printing.

## 13. KB entry: Storage latency hoặc datastore issue

### Symptom

Nhiều VDI chậm, boot storm/logon storm, machine provisioning fail, datastore warning hoặc profile load chậm.

### Pattern nhận diện

- Cùng datastore/storage repository: nghi storage path/capacity/latency.
- Đầu giờ hoặc sau reboot batch: boot/logon storm.
- Sau snapshot/image/change: snapshot growth hoặc write burst.

### Kiểm tra nhanh

- Datastore capacity và free space.
- Latency, IOPS, throughput theo trend.
- Snapshot tồn đọng.
- Host/datastore path alert.
- Profile share/storage có alert không.
- Affected pool/catalog nằm trên datastore nào.

### Evidence cần lưu

Dashboard storage, affected VDI/pool, timestamp, latency/capacity trend, provisioning task error, host/datastore relation.

### Escalation

Storage owner nếu latency/capacity/path evidence rõ; hypervisor owner nếu datastore visibility/host path; VDI platform nếu provisioning task cần retry sau khi storage ổn.

## 14. KB entry: Network hoặc gateway issue

### Symptom

External user timeout, disconnect, session lag, DNS fail, certificate warning hoặc chỉ một site/network bị ảnh hưởng.

### Pattern nhận diện

- External-only: gateway/LB/firewall/certificate/DNS.
- Internal và external đều lỗi: broker/identity/backend hoặc shared network.
- Một site: routing/firewall/DNS/local WAN.
- Session rớt nhưng login được: protocol path/latency/packet loss.

### Kiểm tra nhanh

- Internal vs external comparison.
- DNS resolution.
- Certificate warning/expiry/chain.
- LB member/gateway health.
- Latency/packet loss nếu tool có.
- Firewall/routing recent change.

### Evidence cần lưu

Source location, destination URL/VIP, timestamp, DNS result, client error, gateway/LB status, internal/external test.

### Escalation

Network/gateway owner với source/destination, timing, comparison và error cụ thể. Không chỉ ghi "network chậm".

## 15. Màn hình quản trị nên biết

| Nền tảng/lớp | Màn hình/dashboard cần biết | Dùng để xem gì |
|---|---|---|
| Citrix Director | User session, machine, failed logon, trends | Support, failed session, user experience |
| Citrix Studio | Machine Catalog, Delivery Group, policy, machine state | Cấu hình và resource availability |
| Citrix Gateway/ADC | VIP, session, certificate, STA/StoreFront integration | External access |
| Horizon Console | Desktop pool, session, entitlement, machine/agent state | Horizon operations |
| Unified Access Gateway admin/monitoring | Edge service, tunnel, certificate, backend target | External Horizon access |
| vCenter | VM, host, cluster, datastore, task/event | Hypervisor/HCI operations |
| XenServer/XenCenter nếu có | Host pool, VM, storage repository, network | CVAD hypervisor operations |
| AD/IAM | User, group, computer account, GPO | Identity, entitlement, registration |
| Storage monitoring | Capacity, latency, IOPS, path, snapshot | Performance/profile/provisioning |
| Network/LB monitoring | VIP/member/probe, DNS, firewall, latency | Access/session path |
| Ticket/ITSM | Incident/change timeline, owner, SLA | Process and evidence |

Tên console, URL, quyền truy cập và dashboard thật là Need Customer Confirmation.

## 16. Kiểm tra/lệnh an toàn cần biết

Các ví dụ dưới đây là nhóm kiểm tra read-only phổ biến. Lệnh thật, endpoint chạy lệnh và quyền sử dụng phải theo SOP khách hàng.

| Mục tiêu | Kiểm tra an toàn | Lưu ý |
|---|---|---|
| DNS | Resolve tên portal, gateway, broker, DC | Dùng `nslookup` hoặc công cụ tương đương; lưu kết quả, không sửa DNS. |
| Network reachability | Kiểm tra path tới URL/VIP/service | Dùng công cụ kiểm tra kết nối được phê duyệt; không scan rộng. |
| Time sync | So sánh thời gian endpoint, VDI, broker, DC | Lệch thời gian có thể gây auth/registration lỗi. |
| User/group | Xem trạng thái account và group membership | Không đổi group nếu chưa có approval. |
| VM state | Xem power state, host, datastore | Không reboot/delete nếu chưa có SOP và user confirmation. |
| Agent/VDA | Xem service/state/version nếu có quyền | Không reinstall/upgrade ngoài change. |
| Profile path | Xem path, permission, capacity, lock state | Không restore/delete profile khi chưa có approval. |
| Logs | Thu thập log excerpt theo timestamp | Không gửi secret hoặc dữ liệu user nhạy cảm. |

KB nên ghi "kiểm tra gì" trước khi ghi "chạy lệnh gì". Môi trường thật có thể giới hạn quyền hoặc dùng tool riêng.

## 17. Quy trình cập nhật KB sau incident/change

KB sống bằng vòng lặp học từ thực tế.

1. Xác định incident/change có tạo tri thức lặp lại không.
2. Ghi symptom ngắn gọn bằng ngôn ngữ user/monitoring.
3. Ghi pattern nhận diện: scope, nền tảng, lớp lỗi, recent change.
4. Ghi evidence có giá trị nhất.
5. Ghi kiểm tra nào giúp khoanh vùng nhanh nhất.
6. Ghi workaround hoặc fix đã dùng, kèm điều kiện áp dụng.
7. Ghi khi nào không được dùng workaround.
8. Ghi escalation owner và thông tin cần gửi.
9. Link tới topic/runbook liên quan.
10. Review để loại bỏ thông tin nhạy cảm.

KB entry không cần dài, nhưng phải đủ để engineer khác tái sử dụng mà không hỏi lại người đã xử lý.

## 18. Checklist sử dụng KB trong ca trực

- [ ] Tìm theo symptom trước, không tìm theo sản phẩm trước.
- [ ] So sánh pattern trong KB với scope thực tế.
- [ ] Kiểm tra recent change.
- [ ] Thu thập evidence trước action.
- [ ] Chỉ áp dụng workaround nếu điều kiện khớp.
- [ ] Không áp dụng fix rủi ro cao ngoài SOP.
- [ ] Escalate nếu impact rộng, security/data risk, hoặc không khớp pattern.
- [ ] Sau khi xử lý, cập nhật KB nếu có tri thức mới.

## 19. Scenario Based Learning

### Scenario 1: Ticket "VDI chậm" được chuyển nhiều vòng

**Bối cảnh:** Ticket chỉ ghi "VDI chậm", không có timestamp, user, pool, access path hay metric.

**Câu hỏi cho học viên:** KB entry nào giúp cải thiện? Cần bổ sung trường gì?

**Gợi ý phân tích:** Dùng pattern login chậm/performance: cần timestamp, scope, login phase, profile/storage/host metrics, recent change.

**Hướng xử lý đề xuất:** Chuẩn hóa intake template và tạo KB "VDI chậm - thông tin tối thiểu cần hỏi".

**Evidence cần lưu:** Ticket mẫu trước/sau, checklist intake, metric cần thu thập.

### Scenario 2: Lỗi black screen lặp lại sau image update

**Bối cảnh:** Sau hai lần image update, cùng một nhóm user báo black screen.

**Câu hỏi cho học viên:** KB entry cần chứa pattern gì?

**Gợi ý phân tích:** Ghi image version, affected pool/catalog, agent version, display protocol, security tool, profile signal và rollback condition.

**Hướng xử lý đề xuất:** Tạo KB black screen sau image update, link tới image management và troubleshooting playbook.

**Evidence cần lưu:** Image version, change ID, screenshot, event log sample, affected machine list.

### Scenario 3: Helpdesk reset session quá sớm làm mất evidence

**Bối cảnh:** User launch fail, helpdesk reset session ngay. Lỗi biến mất tạm thời nhưng quay lại, không còn failed session ban đầu.

**Câu hỏi cho học viên:** KB cần cảnh báo gì?

**Gợi ý phân tích:** KB action phải có precheck: lưu failed session, screenshot, timestamp, machine/session ID trước reset.

**Hướng xử lý đề xuất:** Cập nhật KB support action "reset/logoff session" với evidence-before-action.

**Evidence cần lưu:** SOP update, ticket example, required evidence list.

## 20. Knowledge Check

**Câu 1. KB khác troubleshooting playbook như thế nào?**  
KB là tri thức ngắn, dùng lại theo pattern và evidence. Playbook là quy trình xử lý sâu hơn theo lớp lỗi.

**Câu 2. Một KB entry tốt cần có những phần nào?**  
Symptom, pattern, lớp cần kiểm tra, kiểm tra nhanh, evidence, hướng xử lý an toàn, escalation và liên kết tài liệu.

**Câu 3. Vì sao KB không nên chứa credential?**  
Vì credential là thông tin nhạy cảm, không cần cho đào tạo và tạo rủi ro bảo mật/audit.

**Câu 4. Khi thấy lỗi lặp lại sau change, KB cần ghi gì?**  
Change ID/type, thời điểm, affected scope, evidence, workaround/rollback condition và link tới change/troubleshooting docs.

**Câu 5. Tại sao nên tìm KB theo symptom trước?**  
Vì user thường báo theo triệu chứng, còn root cause có thể nằm ở nhiều lớp khác nhau.

**Câu 6. Khi nào không áp dụng workaround trong KB?**  
Khi pattern không khớp, impact rộng, có rủi ro dữ liệu/security, cần change/approval hoặc chưa có evidence.

**Câu 7. Evidence quan trọng nhất cho lỗi no resource là gì?**  
User/group, expected resource, entitlement/DG mapping, resource state và screenshot portal.

**Câu 8. KB cần review khi nào?**  
Sau incident lớn, sau change/upgrade, khi topology/tool thay đổi, khi workaround không còn đúng hoặc theo chu kỳ customer quy định.

## 21. Common Misconceptions

- "KB càng dài càng tốt." Sai. KB tốt phải ngắn, đúng pattern, đủ evidence và dễ dùng.
- "Có KB là không cần escalation." Sai. KB giúp khoanh vùng; escalation vẫn cần khi vượt quyền, impact rộng hoặc rủi ro cao.
- "KB có thể copy từ vendor doc là đủ." Sai. Vendor doc cần được chuyển thành tri thức vận hành theo môi trường khách hàng.
- "Lệnh kiểm tra là phần quan trọng nhất." Không hẳn. Câu hỏi đúng và evidence đúng quan trọng hơn chạy lệnh nhiều.
- "Workaround đã từng dùng thì luôn dùng lại được." Sai. Phải kiểm tra pattern và điều kiện áp dụng.

## 22. Need Customer Confirmation

Các thông tin cần hỏi khách hàng:

- KB hiện tại lưu ở đâu: wiki, ITSM, SharePoint, Confluence hay tool khác?
- Ai là owner review KB?
- Format KB chuẩn của khách hàng là gì?
- Console/dashboard chính thức support được phép dùng là gì?
- Log path và log collection tool chính thức cho Horizon, Citrix, Gateway, VDA/Agent, profile là gì?
- Lệnh kiểm tra nào được phép dùng trên endpoint, VDI, broker, server và jump host?
- Có danh sách known issues hiện tại không?
- Có KB cho các lỗi lặp lại theo pool/catalog/site không?
- Quy định loại bỏ dữ liệu nhạy cảm khỏi screenshot/log như thế nào?
- Ai phê duyệt workaround rủi ro như reset hàng loạt, policy exception, rollback image?
- Ticket taxonomy/symptom categories chính thức là gì?
- Quy trình biến incident RCA thành KB entry là gì?
- Chu kỳ review và archive KB lỗi thời là gì?

## 23. Related Wiki Links

### Source summaries

- [[sources/vdi-training-idea]]
- [[sources/vdi-documentation-list-context]]
- [[sources/horizon-8-architecture]]
- [[sources/understand-and-troubleshoot-horizon-connections]]
- [[sources/citrix-virtual-apps-and-desktops-7-2603]]
- [[sources/fslogix-documentation]]
- [[sources/vmware-vsphere-8-0]]
- [[sources/xenserver-8-4]]

### Concepts

- [[concepts/vdi-connection-flow]]
- [[concepts/incident-management]]
- [[concepts/monitoring-and-logs]]
- [[concepts/change-management]]
- [[concepts/omnissa-horizon]]
- [[concepts/connection-server]]
- [[concepts/unified-access-gateway]]
- [[concepts/citrix-virtual-apps-and-desktops]]
- [[concepts/delivery-controller]]
- [[concepts/storefront]]
- [[concepts/virtual-delivery-agent]]
- [[concepts/delivery-group]]
- [[concepts/identity-and-access-management]]
- [[concepts/profile-container]]
- [[concepts/user-profile-management]]
- [[concepts/datastore]]
- [[concepts/vcenter-server]]
- [[concepts/xenserver]]
- [[concepts/virtual-networking]]
- [[concepts/display-protocol]]

### Topic documents

- [[topics/5_VDI_Access_Flow_Design]]
- [[topics/6_Identity_and_Domain_Integration_Guide]]
- [[topics/8_Storage_Operations_for_VDI]]
- [[topics/9_Network_Operations_for_VDI]]
- [[topics/15_VDI_Monitoring_and_Alerting_Guide]]
- [[topics/16_Daily_Operations_Checklist]]
- [[topics/17_VDI_Incident_Classification_Guide]]
- [[topics/18_VDI_Troubleshooting_Playbook]]
- [[topics/20_VDI_Change_Management_Guide]]
- [[topics/25_VDI_Support_and_Escalation_Guide]]
- [[topics/27_VDI_Glossary_and_Concept_Dictionary]]

## 24. Summary for Learners

Khi dùng hoặc viết KB vận hành VDI, hãy nhớ:

1. Bắt đầu từ symptom và pattern.
2. Không kết luận root cause nếu chưa có evidence.
3. Ghi rõ màn hình cần xem, kiểm tra an toàn và evidence cần lưu.
4. Workaround phải có điều kiện áp dụng và điều kiện không áp dụng.
5. Escalation phải nêu đúng lớp lỗi và gói thông tin cần chuyển.
6. KB phải được cập nhật sau incident/change, không để tri thức nằm trong trí nhớ cá nhân.

Điều quan trọng nhất: KB vận hành tốt là bộ nhớ thực tế của đội VDI. Nó giúp engineer mới học nhanh hơn, engineer trực ca xử lý nhất quán hơn, và incident lặp lại được giảm dần thay vì cứ quay lại như lần đầu.

## 25. Self Review

- [x] Đúng tên tài liệu trong list_context.txt.
- [x] Đúng tên file trong cột Name File.
- [x] Đúng mục đích: lỗi thường gặp, kinh nghiệm xử lý, lệnh/kiểm tra, màn hình quản trị và lưu ý vận hành thực tế.
- [x] Bám bối cảnh training_idea.md: Horizon on HCI, Citrix CVAD trên XenServer/ESXi, quy mô 1500-2000+ VDI.
- [x] Không bịa console URL, command set, log path, dashboard hoặc KB workflow của khách hàng.
- [x] Có phân biệt Need Customer Confirmation.
- [x] Có mẫu KB entry, pattern lỗi, symptom cards, evidence và escalation.
- [x] Có kiểm tra/lệnh an toàn ở mức định hướng, không chứa thao tác phá hủy.
- [x] Có scenario, knowledge check, misconception và related links.
- [x] Phù hợp cho system engineer và helpdesk dùng trong vận hành thực tế.
