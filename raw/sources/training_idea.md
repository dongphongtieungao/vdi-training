# Mô tả thông tin hệ thống VDI phục vụ xây dựng tài liệu nghiên cứu cho System Engineer

## 1. Mục tiêu của tài liệu

Tài liệu cần giúp engineer hiểu nhanh hai nền tảng VDI khách hàng đang vận hành:

1. Omnissa Horizon, trước đây là VMware Horizon, chạy trên hạ tầng HCI.

2. Citrix Virtual Apps and Desktops, viết tắt là CVAD, có thể chạy trên XenServer hoặc VMware ESXi.

3. Mỗi hệ thống có quy mô lớn, khoảng 1500 đến hơn 2000 máy VDI, nên engineer không thể chỉ nhìn theo từng máy ảo riêng lẻ. Cần nhìn như một nền tảng dịch vụ gồm identity, broker, image, hypervisor, storage, network, policy, monitoring và quy trình vận hành.

4. Đối tượng đọc có thể đã hoặc chưa có nền tảng về ảo hóa, Citrix, Omnissa, network, storage. Vì vậy tài liệu phải bắt đầu từ mô hình tổng quan, sau đó đi vào các tác vụ vận hành thường gặp.

5. Tài liệu không nên chỉ là manual theo sản phẩm. Nó cần là tài liệu chuẩn bị vận hành thực tế, giúp engineer biết cần nhìn thành phần nào, kiểm tra ở đâu, lỗi thường nằm ở lớp nào và khi nào cần escalation.

## 2. Cách nhìn tổng thể về hệ thống VDI

VDI là mô hình cung cấp desktop hoặc ứng dụng từ hạ tầng trung tâm cho người dùng. Người dùng không làm việc trực tiếp trên máy cá nhân vật lý, mà truy cập vào desktop hoặc application session được đặt trong datacenter hoặc cloud private. Với quy mô từ 1500 đến hơn 2000 VDI, hệ thống cần được vận hành như một platform có nhiều lớp phụ thuộc lẫn nhau.

Các lớp cần mô tả trong tài liệu gồm:

1. Lớp người dùng truy cập: laptop, thin client, browser, Citrix Workspace App hoặc Horizon Client.

2. Lớp truy cập ngoài: Citrix Gateway hoặc Omnissa Unified Access Gateway nếu người dùng truy cập từ ngoài mạng nội bộ.

3. Lớp portal và broker: StoreFront, Delivery Controller đối với Citrix; Connection Server đối với Omnissa Horizon.

4. Lớp desktop hoặc application session: VDI machine, VDA trong Citrix, Horizon Agent trong Horizon.

5. Lớp identity: Domain Controller, Active Directory, có thể có Microsoft Entra ID hoặc Hybrid Entra ID. Microsoft Entra ID là tên mới của Azure Active Directory theo tài liệu Microsoft. ([azure.microsoft.com][1])

6. Lớp virtualization: HCI, VMware ESXi, vCenter, XenServer tùy nền tảng.

7. Lớp storage: datastore, volume, image storage, profile storage, snapshot, backup.

8. Lớp network: VLAN, routing, firewall, load balancer, DNS, certificate, NAT, latency, bandwidth.

9. Lớp governance và operation: policy, entitlement, monitoring, alert, incident, change, capacity, patching, image lifecycle.

## 3. Mô hình Omnissa Horizon on HCI

### 3.1 Vai trò của Omnissa Horizon

Omnissa Horizon 8 là nền tảng VDI và ứng dụng ảo hóa, cho phép tổ chức cung cấp desktop hoặc application cho người dùng trên nhiều loại thiết bị, đồng thời vẫn quản trị tập trung hiệu năng, policy và hạ tầng. ([Omnissa][2])

Các thành phần chính cần mô tả trong tài liệu gồm:

1. Horizon Client: phần mềm hoặc giao diện người dùng dùng để đăng nhập và mở desktop hoặc application.

2. Unified Access Gateway, viết tắt là UAG: gateway bảo mật cho truy cập từ bên ngoài. UAG nằm ở vùng biên mạng, chuyển tiếp authentication request đến Connection Server và proxy traffic đến Horizon Agent, giúp tránh expose trực tiếp hệ thống nội bộ. ([Omnissa][3])

3. Horizon Connection Server: thành phần broker kết nối. Nó xác thực người dùng qua Active Directory, kiểm tra quyền được cấp và điều hướng người dùng đến desktop hoặc application phù hợp. Connection Server điều phối quá trình thiết lập session nhưng không nhất thiết nằm trong luồng protocol sau khi session đã được thiết lập. ([Omnissa][3])

4. Horizon Agent: agent cài trên desktop, RDSH server hoặc physical system để Horizon có thể quản lý và cung cấp session cho người dùng. ([Omnissa][3])

5. Active Directory: cung cấp identity, authentication và policy enforcement cho Horizon. ([Omnissa][3])

6. vCenter, ESXi, HCI: lớp hạ tầng chịu trách nhiệm tạo, chạy, snapshot, quản lý host, datastore và VM.

7. Storage và network: nền tảng đảm bảo VDI boot, login, profile, application và session hoạt động ổn định khi có nhiều người dùng đồng thời.

### 3.2 Luồng truy cập Omnissa Horizon từ ngoài mạng nội bộ

Người dùng ngoài công ty
→ Horizon Client hoặc browser
→ Unified Access Gateway
→ Horizon Connection Server
→ Desktop pool hoặc application pool
→ VDI có Horizon Agent
→ Application, file share, database hoặc hệ thống nội bộ theo quyền được cấp

Tài liệu cần giải thích rõ rằng UAG là lớp bảo vệ biên, còn Connection Server là lớp broker và entitlement. Engineer khi xử lý lỗi phải phân biệt lỗi trước khi vào gateway, lỗi authentication, lỗi entitlement, lỗi broker, lỗi agent và lỗi desktop runtime.

### 3.3 Luồng truy cập Omnissa Horizon từ mạng nội bộ

Người dùng nội bộ
→ Horizon Client hoặc browser
→ Horizon Connection Server hoặc load balancer trước Connection Server
→ Desktop pool hoặc application pool
→ VDI có Horizon Agent
→ Application và tài nguyên nội bộ

Tùy thiết kế của khách hàng, người dùng nội bộ có thể đi trực tiếp vào Connection Server hoặc vẫn đi qua gateway nội bộ. Đây là điểm cần xác nhận khi viết tài liệu thực tế.

### 3.4 Các điểm engineer cần biết khi vận hành Horizon

1. Desktop pool: nhóm desktop được cấp cho người dùng.

2. Entitlement: quyền của user hoặc group được truy cập pool nào.

3. Golden image hoặc master image: image chuẩn dùng để tạo hoặc refresh VDI.

4. Snapshot: mốc image được dùng để deploy hoặc cập nhật pool.

5. Horizon Agent: thành phần bắt buộc để desktop đăng ký và nhận session.

6. Connection Server health: trạng thái broker, authentication, certificate, replication nếu có nhiều server.

7. vCenter và HCI health: host, cluster, datastore, resource pool, snapshot, template, VM power state.

8. Storage performance: latency, capacity, boot storm, logon storm, profile access.

9. Network path: DNS, firewall, routing, certificate, load balancer, UAG, protocol display.

## 4. Mô hình Citrix Virtual Apps and Desktops

### 4.1 Vai trò của CVAD

Citrix Virtual Apps and Desktops là nền tảng ảo hóa application và desktop, cho phép IT quản lý virtual machine, application, licensing, security và cung cấp truy cập từ nhiều loại thiết bị. Kiến trúc thống nhất của CVAD là FlexCast Management Architecture, viết tắt là FMA. ([docs.citrix.com][4])

Các thành phần chính cần mô tả trong tài liệu gồm:

1. Citrix Workspace App: client trên thiết bị người dùng.

2. StoreFront: portal để người dùng đăng nhập và chọn application hoặc desktop.

3. Citrix Gateway hoặc NetScaler Gateway: gateway bảo mật cho người dùng truy cập từ ngoài firewall, thường đặt tại DMZ và dùng TLS. ([docs.citrix.com][4])

4. Delivery Controller: thành phần quản trị trung tâm của một Citrix Site. Nó phân phối application và desktop, xác thực và quản lý user access, broker connection, optimize connection và load balance connection. ([docs.citrix.com][4])

5. Site Database: Microsoft SQL Server database dùng để lưu configuration và session information của Citrix Site. ([docs.citrix.com][4])

6. Virtual Delivery Agent, viết tắt là VDA: agent cài trên máy vật lý hoặc máy ảo cung cấp desktop hoặc application cho người dùng. VDA đăng ký với Delivery Controller và quản lý kết nối giữa user device và machine. ([docs.citrix.com][4])

7. Citrix Studio: console quản trị để cấu hình site, tạo workload, gán application hoặc desktop cho user và quản lý license. ([docs.citrix.com][4])

8. Citrix Director: công cụ web cho helpdesk và IT support để monitor, troubleshoot và hỗ trợ end user. Director hiển thị real time session data và historical site data. ([docs.citrix.com][4])

9. License Server: quản lý license cho Citrix product và session. ([docs.citrix.com][4])

10. Hypervisor: lớp chạy VM, trong trường hợp của khách hàng có thể là XenServer hoặc VMware ESXi. Citrix có tài liệu riêng cho XenServer và VMware virtualization environments. ([docs.citrix.com][5])

### 4.2 Luồng truy cập CVAD từ ngoài mạng nội bộ

Người dùng ngoài công ty
→ Citrix Workspace App hoặc browser
→ Citrix Gateway
→ StoreFront
→ Delivery Controller
→ VDA phù hợp
→ Session desktop hoặc application

Trong CVAD, người dùng không truy cập trực tiếp Delivery Controller. VDA đóng vai trò trung gian giữa user session và Controller. Khi người dùng đăng nhập qua StoreFront, thông tin xác thực đi tới Broker Service trên Controller, Controller xác định resource người dùng được phép dùng, sau đó chọn VDA phù hợp. Sau khi session được thiết lập, ICA file có thể được dùng để tạo kết nối giữa client và VDA, qua đó traffic session không đi theo cùng cách như traffic quản trị. ([docs.citrix.com][4])

### 4.3 Luồng truy cập CVAD từ mạng nội bộ

Người dùng nội bộ
→ Citrix Workspace App hoặc StoreFront website
→ StoreFront
→ Delivery Controller
→ VDA
→ Desktop hoặc published application

Nếu khách hàng thiết kế gateway cho cả user nội bộ, luồng truy cập sẽ khác. Vì vậy tài liệu thực tế cần có sơ đồ riêng cho internal access và external access.

### 4.4 Các khái niệm engineer cần nắm với CVAD

1. Site: đơn vị triển khai logic trong Citrix.

2. Delivery Controller: broker và control plane của Site.

3. Site Database, Monitoring Database, Configuration Logging Database: các database nền tảng cho cấu hình, giám sát và audit.

4. Machine Catalog: nhóm máy vật lý hoặc máy ảo được quản lý như một đơn vị. Các máy trong cùng catalog thường có cùng OS, cùng VDA và cùng application hoặc desktop role. ([docs.citrix.com][4])

5. Master image: image chuẩn dùng để tạo VM trong catalog. Citrix có thể dùng MCS hoặc Citrix Provisioning, trước đây là PVS, tùy thiết kế. ([docs.citrix.com][4])

6. Delivery Group: xác định user nào được truy cập application hoặc desktop nào trên machine nào. Delivery Group chứa machine từ Machine Catalog và Active Directory user hoặc group. ([docs.citrix.com][4])

7. Application Group: nhóm application để quản trị và phân vùng quyền hoặc workload chi tiết hơn. ([docs.citrix.com][4])

8. VDA Registration: trạng thái VDA đăng ký được với Delivery Controller hay không.

9. Citrix Policy: policy điều khiển session, clipboard, USB, printer, profile, display, bandwidth, session reliability.

10. Profile Management: có thể dùng Citrix Profile Management, FSLogix hoặc giải pháp khác. Cần xác nhận thực tế với khách.

## 5. Các mảng kiến thức tài liệu cần bao quát

### 5.1 Identity và authentication

Tài liệu cần giải thích Domain Controller, Active Directory, DNS, Group Policy, user group, service account, computer account, Kerberos, LDAP, certificate và time sync. Với môi trường có Hybrid Microsoft Entra ID, cần bổ sung khái niệm sync identity giữa on premises AD và Microsoft Entra ID, nhưng không đưa giả định chi tiết nếu khách chưa cung cấp topology.

Engineer cần hiểu lỗi VDI đôi khi không nằm ở Citrix hoặc Horizon mà nằm ở identity, ví dụ user không đăng nhập được, group chưa được cấp quyền, DNS sai, clock skew, domain trust lỗi hoặc policy áp sai OU.

### 5.2 Hypervisor và HCI

Tài liệu cần mô tả lớp hypervisor là nơi chạy VM desktop, VM server và các thành phần quản trị. Với Horizon on HCI, engineer cần nhìn vào cluster, host, datastore, resource pool, snapshot, vCenter, VM tools, host health và storage latency. Với CVAD, engineer cần biết hệ thống có thể chạy trên XenServer hoặc VMware ESXi, nhưng thao tác thực tế sẽ phụ thuộc hypervisor khách hàng đang dùng.

### 5.3 Storage

Storage là lớp ảnh hưởng trực tiếp đến boot storm, logon storm, profile loading, application launch và user experience. Tài liệu cần giải thích datastore, thin provisioning, snapshot growth, profile storage, image repository, backup, replication nếu có, capacity alert và latency.

Không nên chỉ ghi “kiểm tra storage”. Cần ghi rõ engineer phải kiểm tra capacity, latency, IOPS, snapshot tồn đọng, datastore full, path lỗi, storage controller lỗi và profile share có truy cập được hay không.

### 5.4 Network

Tài liệu cần mô tả network theo các luồng:

1. User đến gateway hoặc portal.

2. Gateway đến broker.

3. Broker đến VDA hoặc Horizon Agent.

4. VDI đến Domain Controller, DNS, file server, application server, database, internet proxy.

5. Monitoring system đến host, VM, service và agent.

Các lỗi network thường xuất hiện dưới dạng login chậm, session rớt, màn hình đen, không resolve DNS, không đăng ký agent, không truy cập profile hoặc application nội bộ.

### 5.5 Policy và security

Tài liệu cần bao quát policy ở nhiều lớp:

1. Active Directory Group Policy.

2. Citrix Policy hoặc Horizon policy.

3. USB, clipboard, printer, drive redirection.

4. Session timeout, reconnect, idle session.

5. MFA, conditional access nếu có tích hợp Entra ID hoặc identity provider khác.

6. Role based access cho engineer, helpdesk, operator.

7. Audit log cho thao tác thay đổi.

## 6. Quản trị vòng đời VDI

### 6.1 Tạo lập VDI

Tài liệu cần mô tả quy trình chung:

1. Xác định nhóm người dùng hoặc business unit cần VDI.

2. Xác định loại desktop: persistent, non persistent, single session, multi session, application only.

3. Xác định image chuẩn.

4. Xác định policy và entitlement.

5. Xác định resource placement trên cluster hoặc host.

6. Tạo hoặc mở rộng pool, catalog, delivery group.

7. Kiểm tra VDI đăng ký thành công với broker.

8. Kiểm tra user có thể đăng nhập và mở application.

### 6.2 Quản trị master image

Master image là điểm cực kỳ quan trọng vì một thay đổi sai có thể ảnh hưởng hàng trăm hoặc hàng nghìn VDI. Tài liệu cần có quy trình chuẩn:

1. Clone hoặc snapshot image hiện tại trước khi thay đổi.

2. Cập nhật OS patch, application, security agent, VDA hoặc Horizon Agent theo kế hoạch.

3. Kiểm tra domain join hoặc image preparation theo chuẩn của nền tảng.

4. Kiểm tra application chính.

5. Kiểm tra login bằng user test.

6. Publish image vào pool hoặc catalog thử nghiệm trước.

7. Theo dõi lỗi sau triển khai.

8. Có rollback point rõ ràng.

### 6.3 Phân quyền và cấp phát VDI

Tài liệu cần phân biệt rõ:

1. Quyền quản trị nền tảng: ai được thao tác trên Citrix Studio, Director, Horizon Console, vCenter, XenCenter hoặc tool quản trị khác.

2. Quyền người dùng: user hoặc AD group nào được truy cập desktop pool, delivery group hoặc application group.

3. Quyền hỗ trợ: helpdesk có thể shadow session, reset session, logoff user, reboot VDI hay chỉ xem trạng thái.

4. Quyền thay đổi image: chỉ nhóm quản trị được cập nhật image, snapshot, publish catalog hoặc pool.

### 6.4 Thu hồi VDI

Tài liệu cần có quy trình thu hồi:

1. Xác định user, group, desktop hoặc application cần thu hồi.

2. Kiểm tra session đang hoạt động.

3. Thông báo nếu cần.

4. Remove entitlement hoặc remove user khỏi delivery group.

5. Xử lý dữ liệu người dùng theo chính sách khách hàng.

6. Reclaim VM nếu là persistent desktop.

7. Cập nhật inventory và audit log.

## 7. Các lỗi thường gặp trong môi trường VDI quy mô lớn

### 7.1 User không đăng nhập được

Triệu chứng: login fail, credential rejected, MFA fail, không thấy desktop hoặc application.

Hướng kiểm tra:

1. Kiểm tra user có bị lock, disabled hoặc expired không.

2. Kiểm tra group membership trong Active Directory.

3. Kiểm tra entitlement trong Horizon hoặc Delivery Group trong Citrix.

4. Kiểm tra DNS và Domain Controller.

5. Kiểm tra certificate trên StoreFront, Gateway, UAG hoặc Connection Server.

6. Kiểm tra time sync giữa client, broker, domain controller và VDI.

7. Kiểm tra log trên broker, gateway và identity provider nếu có.

### 7.2 Không có desktop hoặc application để launch

Triệu chứng: user đăng nhập portal được nhưng không thấy resource, hoặc thấy resource nhưng launch fail.

Hướng kiểm tra:

1. Kiểm tra entitlement hoặc AD group mapping.

2. Kiểm tra pool, catalog, delivery group có enabled không.

3. Kiểm tra số lượng machine available.

4. Kiểm tra VM power state.

5. Kiểm tra VDA hoặc Horizon Agent registration.

6. Kiểm tra hypervisor connection từ broker đến vCenter hoặc XenServer.

7. Kiểm tra license nếu nền tảng báo liên quan license.

### 7.3 VDA hoặc Horizon Agent không đăng ký

Triệu chứng: machine hiển thị unregistered, unavailable hoặc agent unreachable.

Hướng kiểm tra:

1. Kiểm tra service VDA hoặc Horizon Agent trên VM.

2. Kiểm tra DNS forward và reverse lookup.

3. Kiểm tra firewall giữa VDI và broker.

4. Kiểm tra danh sách Controller hoặc Connection Server cấu hình trong agent.

5. Kiểm tra domain join và computer account.

6. Kiểm tra time sync.

7. Kiểm tra phiên bản agent có phù hợp với nền tảng hiện tại không.

### 7.4 Login chậm

Triệu chứng: user mất nhiều thời gian ở bước preparing desktop, applying policy, loading profile hoặc launching application.

Hướng kiểm tra:

1. Kiểm tra Group Policy processing time.

2. Kiểm tra profile solution và file share chứa profile.

3. Kiểm tra storage latency.

4. Kiểm tra Domain Controller latency.

5. Kiểm tra logon script.

6. Kiểm tra antivirus scan lúc login.

7. Kiểm tra application startup.

8. Kiểm tra số lượng user login đồng thời có tạo logon storm hay không.

### 7.5 Session rớt hoặc màn hình đen

Triệu chứng: user vào được nhưng session disconnect, freeze, black screen hoặc display lag.

Hướng kiểm tra:

1. Kiểm tra network latency, packet loss, jitter.

2. Kiểm tra gateway hoặc UAG.

3. Kiểm tra display protocol và policy liên quan graphics.

4. Kiểm tra driver, VM tools, VDA hoặc Horizon Agent version.

5. Kiểm tra CPU, RAM, GPU nếu có.

6. Kiểm tra profile hoặc shell startup.

7. Kiểm tra client version.

### 7.6 Boot storm hoặc logon storm

Triệu chứng: nhiều VDI boot hoặc login cùng lúc làm host, storage hoặc broker quá tải.

Hướng kiểm tra:

1. Kiểm tra lịch power management.

2. Kiểm tra datastore latency.

3. Kiểm tra host CPU và memory contention.

4. Kiểm tra số lượng session đồng thời.

5. Kiểm tra Connection Server hoặc Delivery Controller load.

6. Kiểm tra profile storage và file server.

7. Kiểm tra có image update hoặc reboot schedule trùng giờ cao điểm không.

### 7.7 Image update gây lỗi hàng loạt

Triệu chứng: sau khi publish image mới, nhiều VDI không boot, không đăng ký, application lỗi hoặc user login fail.

Hướng kiểm tra:

1. Xác định image version hoặc snapshot vừa publish.

2. So sánh với image version trước đó.

3. Kiểm tra agent version, VM tools, Windows patch, application patch.

4. Kiểm tra image đã được seal hoặc prepare đúng quy trình chưa.

5. Rollback về image trước nếu ảnh hưởng rộng và có rollback point.

6. Ghi nhận change record và RCA.

### 7.8 Profile lỗi hoặc mất dữ liệu cá nhân

Triệu chứng: user vào temporary profile, mất setting, desktop icon mất, application profile reset.

Hướng kiểm tra:

1. Kiểm tra profile path hoặc profile container.

2. Kiểm tra quyền truy cập file share.

3. Kiểm tra lock file hoặc session cũ chưa release.

4. Kiểm tra dung lượng profile storage.

5. Kiểm tra policy profile management.

6. Kiểm tra antivirus hoặc backup có lock file không.

### 7.9 Lỗi printer, USB, clipboard, drive redirection

Triệu chứng: user không in được, không copy paste được, không nhận USB hoặc không map drive.

Hướng kiểm tra:

1. Kiểm tra Citrix Policy hoặc Horizon policy.

2. Kiểm tra Group Policy.

3. Kiểm tra client capability.

4. Kiểm tra driver printer.

5. Kiểm tra rule theo user group, network location hoặc device type.

6. Kiểm tra security exception nếu cần, nhưng không tự mở policy rộng nếu chưa được phê duyệt.

## 8. Nội dung vận hành cần đưa vào tài liệu

### 8.1 Monitoring

Tài liệu cần hướng dẫn engineer theo dõi tối thiểu các nhóm chỉ số sau:

1. Broker health: Connection Server, Delivery Controller, StoreFront, Gateway, UAG.

2. Session health: số session active, disconnected, failed, reconnect.

3. VDI health: registered, unregistered, powered off, maintenance mode, agent unreachable.

4. Hypervisor health: host CPU, memory, datastore, VM power, snapshot.

5. Storage health: capacity, latency, throughput, profile share.

6. Network health: DNS, gateway, firewall, latency, packet loss.

7. Identity health: Domain Controller, authentication error, account lock, group policy.

8. License health: Citrix License Server hoặc license status của nền tảng liên quan.

### 8.2 Incident handling

Tài liệu cần đưa ra cách phân loại incident theo lớp:

1. User issue: chỉ một user bị ảnh hưởng.

2. VDI issue: một hoặc một nhóm desktop bị ảnh hưởng.

3. Pool hoặc catalog issue: một nhóm người dùng bị ảnh hưởng.

4. Broker issue: nhiều pool hoặc nhiều delivery group bị ảnh hưởng.

5. Gateway hoặc network issue: user ngoài mạng hoặc một site bị ảnh hưởng.

6. Hypervisor hoặc storage issue: ảnh hưởng diện rộng, có thể tác động hàng trăm hoặc hàng nghìn VDI.

### 8.3 Change operation

Các thao tác thay đổi cần có checklist riêng:

1. Cập nhật master image.

2. Publish image mới.

3. Tăng hoặc giảm số lượng VDI.

4. Thay đổi policy.

5. Thay đổi entitlement.

6. Patch Delivery Controller, Connection Server, StoreFront, UAG, Gateway, VDA hoặc Horizon Agent.

7. Bảo trì host hoặc datastore.

8. Thay đổi certificate.

9. Thay đổi firewall hoặc load balancer.

Mỗi change cần có precheck, impact assessment, rollback plan, validation sau thay đổi và evidence lưu lại.

### 8.4 Hỗ trợ kỹ thuật

Tài liệu cần mô tả các tình huống helpdesk và engineer thường gặp:

1. Reset session.

2. Logoff user.

3. Restart VDI.

4. Shadow hoặc remote assistance nếu chính sách cho phép.

5. Kiểm tra user đang vào VDI nào.

6. Kiểm tra lỗi launch application.

7. Kiểm tra profile và printer.

8. Phân biệt lỗi user endpoint với lỗi backend VDI.

## 9. Đề cương tài liệu nghiên cứu đề xuất

### Chương 1: Tổng quan VDI

Mục tiêu: giúp engineer hiểu VDI là gì, vì sao doanh nghiệp dùng VDI, khác biệt giữa physical PC, remote desktop, published app và full virtual desktop.

Nội dung chính:

1. Khái niệm VDI.

2. Mô hình user access.

3. Các lớp kiến trúc VDI.

4. Rủi ro vận hành ở quy mô lớn.

5. Cách đọc sơ đồ VDI.

### Chương 2: Tổng quan hệ thống khách hàng

Mục tiêu: mô tả bối cảnh có hai nền tảng VDI khác nhau.

Nội dung chính:

1. Hệ thống Omnissa Horizon on HCI.

2. Hệ thống Citrix CVAD.

3. Quy mô mỗi hệ thống.

4. Các thành phần chung: Domain Controller, Entra ID nếu có, vCenter, storage, network, monitoring, policy.

5. Các thông tin chưa có cần xác nhận với khách.

### Chương 3: Kiến trúc Omnissa Horizon

Mục tiêu: giúp engineer hiểu vai trò từng thành phần Horizon.

Nội dung chính:

1. Horizon Client.

2. Unified Access Gateway.

3. Connection Server.

4. Horizon Agent.

5. Desktop Pool.

6. Entitlement.

7. vCenter, ESXi, HCI.

8. Storage và network path.

9. Internal access flow và external access flow.

### Chương 4: Kiến trúc Citrix CVAD

Mục tiêu: giúp engineer hiểu Citrix Site và cách Citrix broker session.

Nội dung chính:

1. Citrix Workspace App.

2. StoreFront.

3. Citrix Gateway hoặc NetScaler.

4. Delivery Controller.

5. Site Database và Monitoring Database.

6. VDA.

7. Citrix Studio.

8. Citrix Director.

9. License Server.

10. Machine Catalog, Delivery Group, Application Group.

11. XenServer hoặc VMware ESXi.

### Chương 5: Identity, Domain và Hybrid Entra ID

Mục tiêu: giải thích phần xác thực và phân quyền.

Nội dung chính:

1. Active Directory.

2. Domain Controller.

3. DNS.

4. Group Policy.

5. AD group và entitlement.

6. Hybrid Microsoft Entra ID nếu có.

7. MFA hoặc conditional access nếu có.

8. Lỗi thường gặp liên quan identity.

### Chương 6: Hypervisor, HCI và Storage

Mục tiêu: giúp engineer hiểu nền tảng bên dưới VDI.

Nội dung chính:

1. ESXi, vCenter, cluster, host, datastore.

2. XenServer nếu khách dùng cho CVAD.

3. HCI là gì trong ngữ cảnh VDI.

4. Snapshot và template.

5. Storage latency và capacity.

6. Boot storm và logon storm.

7. Profile storage.

### Chương 7: Network và luồng kết nối

Mục tiêu: giúp engineer biết đọc lỗi theo đường đi của traffic.

Nội dung chính:

1. Internal user flow.

2. External user flow.

3. Gateway, load balancer, firewall.

4. DNS và certificate.

5. Protocol session.

6. Network troubleshooting checklist.

### Chương 8: VDI provisioning và image management

Mục tiêu: giúp engineer hiểu cách tạo và cập nhật VDI an toàn.

Nội dung chính:

1. Master image.

2. Snapshot.

3. Machine Catalog hoặc Desktop Pool.

4. Delivery Group hoặc Entitlement.

5. Persistent và non persistent desktop.

6. Image update flow.

7. Rollback flow.

8. Validation sau publish image.

### Chương 9: Policy và user experience

Mục tiêu: giúp engineer hiểu policy ảnh hưởng trực tiếp đến trải nghiệm user.

Nội dung chính:

1. Clipboard policy.

2. USB redirection.

3. Printer mapping.

4. Drive mapping.

5. Display và graphics.

6. Session timeout và reconnect.

7. Profile policy.

8. Security boundary.

### Chương 10: Monitoring và daily operation

Mục tiêu: cung cấp checklist vận hành hàng ngày.

Nội dung chính:

1. Kiểm tra broker service.

2. Kiểm tra gateway.

3. Kiểm tra VDI registration.

4. Kiểm tra active session và failed session.

5. Kiểm tra host và datastore.

6. Kiểm tra alert.

7. Kiểm tra incident tồn đọng.

8. Ghi nhận abnormal trend.

### Chương 11: Troubleshooting guide

Mục tiêu: đưa ra playbook xử lý lỗi.

Nội dung chính:

1. Login fail.

2. Không thấy resource.

3. Launch fail.

4. VDI unregistered.

5. Login chậm.

6. Session disconnect.

7. Black screen.

8. Profile issue.

9. Printer issue.

10. Storage hoặc hypervisor issue.

### Chương 12: Change và escalation

Mục tiêu: giúp engineer biết thao tác nào cần kiểm soát thay đổi.

Nội dung chính:

1. Image update.

2. Policy change.

3. Entitlement change.

4. Broker patching.

5. Gateway certificate renewal.

6. Host maintenance.

7. Storage expansion.

8. Rollback expectation.

9. Escalation matrix.

10. Evidence cần thu thập trước khi escalation.

## 10. Các thông tin cần hỏi thêm khách hàng để tài liệu chính xác hơn

1. Phiên bản cụ thể của Omnissa Horizon và Citrix CVAD đang sử dụng là gì?

2. Mỗi hệ thống đang có bao nhiêu site, pod, pool, catalog, delivery group và user group chính?

3. CVAD hiện chạy trên XenServer, VMware ESXi hay cả hai?

4. Horizon on HCI đang dùng HCI platform nào, ví dụ VMware vSAN, Nutanix hoặc nền tảng khác?

5. Người dùng truy cập từ ngoài mạng đi qua gateway nào, có load balancer không?

6. Người dùng nội bộ có đi qua gateway không hay truy cập trực tiếp StoreFront hoặc Connection Server?

7. Hệ thống đang dùng profile solution nào, ví dụ Citrix Profile Management, FSLogix, roaming profile hoặc giải pháp khác?

8. Monitoring hiện tại dùng công cụ nào và có alert rule cho host, storage, session, broker, gateway chưa?

9. Quy trình change hiện tại đối với image update, policy change và certificate change như thế nào?

10. SLA hoặc mức độ ưu tiên incident cho VDI là gì, đặc biệt với lỗi ảnh hưởng nhiều user cùng lúc?

## 11. Nhận định về độ rõ của yêu cầu

Yêu cầu hiện tại đủ rõ để xây dựng khung tài liệu nghiên cứu và tài liệu đào tạo nền tảng cho engineer. Tuy nhiên chưa đủ để viết runbook vận hành chi tiết cho từng môi trường thật, vì còn thiếu version, topology, network path, monitoring tool, profile solution, storage design, HA design, access flow và quy trình change thực tế.

Nên triển khai tài liệu theo hai lớp:

1. Lớp 1: tài liệu nền tảng chung về Horizon, CVAD và vận hành VDI quy mô lớn.

2. Lớp 2: tài liệu vận hành riêng cho hệ thống khách hàng, bổ sung sơ đồ thật, tên thành phần thật, dashboard thật, checklist thật, escalation path thật và SOP theo từng loại incident.

[1]: https://azure.microsoft.com/en-us/services/active-directory/?utm_source=chatgpt.com "Microsoft Entra ID (formerly Azure Active Directory) | Microsoft Security"
[2]: https://www.omnissa.com/horizon-8/?utm_source=chatgpt.com "Omnissa Horizon | Flexible, secure VDI & apps with Horizon 8"
[3]: https://www.omnissa.com/horizon-8/ "Omnissa Horizon 8 | Virtual desktops for modern IT"
[4]: https://docs.citrix.com/en-us/citrix-virtual-apps-desktops/2411/technical-overview "Technical overview | Citrix Virtual Apps and Desktops™ 7 2411"
[5]: https://docs.citrix.com/en-us/citrix-virtual-apps-desktops/2411/system-requirements "System requirements | Citrix Virtual Apps and Desktops 7 2411"
