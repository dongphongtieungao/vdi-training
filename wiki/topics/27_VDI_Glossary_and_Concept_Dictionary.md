# VDI Glossary and Concept Dictionary

## 0. Document Control

| Trường | Giá trị |
|---|---|
| Thứ tự | 27 |
| Tên tài liệu | VDI Glossary and Concept Dictionary |
| Tên file | 27_VDI_Glossary_and_Concept_Dictionary.md |
| Mục đích tài liệu | Giải thích thuật ngữ quan trọng như broker, VDA, Horizon Agent, pool, catalog, delivery group, entitlement, profile, gateway, datastore, session và image. |
| Nguồn điều khiển | [[sources/vdi-training-idea]], [[sources/vdi-documentation-list-context]] |
| Trạng thái | Tài liệu đào tạo thuật ngữ; tên gọi nội bộ, product version, console label và cách khách hàng đặt tên object là Need Customer Confirmation |

### Source Grounding

| Nội dung | Nguồn sử dụng | Mức độ tin cậy | Ghi chú |
|---|---|---|---|
| Bối cảnh hai hệ thống VDI, quy mô 1500-2000+ VDI và yêu cầu đào tạo engineer mới | [[sources/vdi-training-idea]] | High | Dùng làm bối cảnh diễn giải thuật ngữ. |
| Tên tài liệu, tên file và mục đích tài liệu | [[sources/vdi-documentation-list-context]] | High | Source of truth cho scope file 27. |
| Thuật ngữ Horizon: Connection Server, UAG, Horizon Agent, pool, entitlement, protocol | [[sources/horizon-8-architecture]], [[sources/understand-and-troubleshoot-horizon-connections]], [[concepts/omnissa-horizon]], [[concepts/connection-server]], [[concepts/unified-access-gateway]], [[concepts/display-protocol]] | High | Dùng cho nhóm thuật ngữ Horizon. |
| Thuật ngữ Citrix: Delivery Controller, StoreFront, VDA, Machine Catalog, Delivery Group, HDX/ICA | [[sources/citrix-virtual-apps-and-desktops-7-2603]], [[concepts/citrix-virtual-apps-and-desktops]], [[concepts/delivery-controller]], [[concepts/storefront]], [[concepts/virtual-delivery-agent]], [[concepts/delivery-group]], [[concepts/hdx]], [[concepts/ica-virtual-channel]] | High | Dùng cho nhóm thuật ngữ Citrix. |
| Thuật ngữ hạ tầng: vCenter, ESXi, XenServer, datastore, storage repository, VM, snapshot, virtual networking | [[sources/vmware-vsphere-8-0]], [[sources/vcenter-server-installation-and-setup]], [[sources/xenserver-8-4]], [[concepts/vcenter-server]], [[concepts/esxi]], [[concepts/xenserver]], [[concepts/datastore]], [[concepts/storage-repository]], [[concepts/virtual-machine]], [[concepts/snapshot]], [[concepts/virtual-networking]] | High | Dùng cho nhóm hạ tầng. |
| Thuật ngữ profile, identity, monitoring, change, incident, backup, HA | [[sources/fslogix-documentation]], [[concepts/profile-container]], [[concepts/fslogix]], [[concepts/cloud-cache]], [[concepts/identity-and-access-management]], [[concepts/monitoring-and-logs]], [[concepts/change-management]], [[concepts/incident-management]], [[concepts/backup-and-recovery]], [[concepts/high-availability]] | Medium | Dùng cho nhóm vận hành. |

## 1. Cách dùng glossary này

Glossary này không chỉ là bảng dịch thuật ngữ. Mục tiêu là giúp system engineer mới đọc tài liệu VDI và hiểu ngay:

- Thuật ngữ đó nghĩa là gì.
- Nó nằm ở lớp nào trong kiến trúc VDI.
- Nó liên quan thế nào tới Omnissa Horizon hoặc Citrix CVAD.
- Khi nó lỗi, user thường thấy triệu chứng gì.
- Engineer nên kiểm tra gì đầu tiên.
- Nên đọc tài liệu nào tiếp.

Với môi trường thật của khách hàng, tên object có thể khác: pool name, catalog name, Delivery Group, AD group, datastore, gateway VIP, monitoring dashboard. Những tên thật đó chưa có trong nguồn và phải ghi Need Customer Confirmation.

## 2. Bản đồ thuật ngữ theo lớp

| Lớp | Thuật ngữ thường gặp | Tài liệu nên đọc |
|---|---|---|
| User Access | Client, endpoint, session, display protocol, HDX, Blast/primary-secondary protocol | [[topics/5_VDI_Access_Flow_Design]] |
| Gateway | Citrix Gateway, Unified Access Gateway, load balancer, certificate, firewall | [[topics/9_Network_Operations_for_VDI]] |
| Broker/Control Plane | Broker, Delivery Controller, Connection Server, StoreFront, Site Database | [[topics/3_Omnissa_Horizon_Architecture_Overview]], [[topics/4_Citrix_CVAD_Architecture_Overview]] |
| Desktop/App Session | VDA, Horizon Agent, desktop, published app, session, app backend | [[topics/18_VDI_Troubleshooting_Playbook]] |
| Identity | AD, Domain Controller, DNS, GPO, entitlement, AD group, machine identity | [[topics/6_Identity_and_Domain_Integration_Guide]] |
| Provisioning | Pool, Machine Catalog, Delivery Group, image, snapshot, persistent/non-persistent | [[topics/11_VDI_Provisioning_and_Allocation_Guide]], [[topics/12_Master_Image_Management_Guide]] |
| Hypervisor/HCI | VM, ESXi, vCenter, XenServer, host, cluster, HCI, datastore, storage repository | [[topics/7_Hypervisor_and_HCI_Operations_Guide]] |
| Storage/Profile | Profile, FSLogix, profile container, Cloud Cache, datastore, latency, IOPS | [[topics/8_Storage_Operations_for_VDI]] |
| Operations | Monitoring, alert, incident, change, backup, HA/DR, RBAC, support | [[topics/15_VDI_Monitoring_and_Alerting_Guide]], [[topics/17_VDI_Incident_Classification_Guide]] |

## 3. Core VDI Terms

### VDI

VDI, Virtual Desktop Infrastructure, là mô hình cung cấp desktop hoặc application từ hạ tầng trung tâm cho user. User không làm việc trực tiếp trên một PC vật lý cố định, mà truy cập vào desktop/session chạy trên datacenter hoặc private cloud.

Trong môi trường khách hàng, VDI gồm hai nền tảng: Omnissa Horizon trên HCI và Citrix CVAD trên XenServer hoặc VMware ESXi. Với quy mô 1500-2000+ VDI, engineer phải nhìn VDI như một dịch vụ nhiều lớp, không phải một tập VM rời rạc.

**Khi lỗi thường thấy:** login fail, không thấy desktop, launch fail, session disconnect, profile issue, chậm.  
**Cần nhớ:** user symptom có thể đến từ broker, gateway, identity, storage, network hoặc hypervisor.

### Virtual Desktop

Virtual desktop là desktop Windows/Linux chạy như VM hoặc session được broker cấp cho user. Nó có thể persistent hoặc non-persistent.

**Persistent desktop:** user có desktop gắn lâu dài, thay đổi có thể được giữ lại.  
**Non-persistent desktop:** desktop có thể được refresh/recreate từ image, dữ liệu user thường nằm ở profile/container hoặc storage riêng.

**Khi lỗi thường thấy:** VM powered off, Agent/VDA unregistered, user được gán sai desktop, profile mất sau reset.  
**Cần kiểm tra:** power state, assignment, registration, profile policy, image version.

### Published Application

Published application là ứng dụng được xuất bản cho user dùng từ xa mà không nhất thiết cấp full desktop. User thấy ứng dụng trên portal/client và mở app trong session từ hạ tầng VDI.

Trong Citrix, published app thường liên quan Delivery Group/Application Group và VDA. Trong Horizon, application pool có thể cung cấp ứng dụng cho user.

**Khi lỗi thường thấy:** app không hiện, app launch fail, app mở nhưng backend lỗi.  
**Cần kiểm tra:** entitlement, Delivery Group/Application Group hoặc application pool, VDA/Agent, app backend, profile.

### Session

Session là phiên làm việc của user với desktop hoặc application. Session có thể active, disconnected, reconnecting hoặc failed.

Session không giống VM. Một VM có thể chạy nhưng user session fail. Một user có thể có disconnected session gây lock profile hoặc app issue.

**Khi lỗi thường thấy:** disconnect, frozen session, black screen, không reconnect được.  
**Cần kiểm tra:** session state, client path, gateway, protocol, profile, host resource.

### Broker

Broker là thành phần điều phối user tới resource phù hợp. Broker xác thực hoặc phối hợp xác thực, kiểm tra entitlement, chọn desktop/app và điều phối launch.

Trong Citrix, broker logic nằm ở Delivery Controller. Trong Horizon, broker chính là Connection Server. StoreFront là portal Citrix, còn Gateway/UAG là access edge chứ không phải broker chính.

**Khi lỗi thường thấy:** không thấy resource, launch fail diện rộng, failed session tăng.  
**Cần kiểm tra:** broker service, database/connectivity nếu có, entitlement, machine registration, recent change.

## 4. Citrix CVAD Terms

### Citrix CVAD

Citrix Virtual Apps and Desktops, CVAD, là nền tảng cung cấp virtual desktop và published application. Các thành phần quan trọng gồm Delivery Controller, StoreFront, Citrix Gateway, VDA, Machine Catalog, Delivery Group, Site Database và License Server nếu có.

**Cần nhớ:** CVAD không chỉ là VDA. Lỗi user có thể nằm ở StoreFront, Gateway, Delivery Controller, Site Database, VDA, policy, profile, hypervisor hoặc AD.

### Delivery Controller

Delivery Controller là control plane/broker của Citrix Site. Nó điều phối access, resource selection, VDA registration và session brokering.

**Khi lỗi thường thấy:** VDA không registered, user không thấy app/desktop, launch fail, Studio/Director báo lỗi.  
**Cần kiểm tra:** Controller service, Site Database connectivity, VDA registration, Delivery Group, license/status nếu có cảnh báo.

### StoreFront

StoreFront là portal nơi user đăng nhập và thấy desktop/application được cấp. StoreFront làm việc với Delivery Controller để enumerate resource.

**Khi lỗi thường thấy:** user login portal lỗi, không thấy resource, external integration với Gateway lỗi.  
**Cần kiểm tra:** Store health, authentication method, Gateway integration, certificate, resource enumeration.

### Citrix Gateway

Citrix Gateway là lớp truy cập từ ngoài mạng hoặc access edge cho Citrix. Nó thường đứng trước StoreFront/VDI path và liên quan TLS, certificate, firewall, load balancer và ICA/HDX traffic.

**Khi lỗi thường thấy:** external user không login/launch được, TLS warning, disconnect.  
**Cần kiểm tra:** gateway health, certificate chain, LB member, STA/StoreFront integration, firewall path.

### VDA

VDA, Virtual Delivery Agent, là agent cài trên desktop hoặc server cung cấp session cho user trong Citrix. VDA phải đăng ký với Delivery Controller để sẵn sàng nhận session.

**Khi lỗi thường thấy:** VDA unregistered, launch fail, black screen, session disconnect.  
**Cần kiểm tra:** VDA service, registration, DNS, domain join, Controller list, firewall, image/VDA version.

### Machine Catalog

Machine Catalog là nhóm machine trong Citrix được quản lý theo cùng loại workload, OS, provisioning method hoặc image. Delivery Group sử dụng machine từ catalog để cấp cho user.

**Khi lỗi thường thấy:** không có machine available, provisioning task fail, catalog dùng image sai.  
**Cần kiểm tra:** catalog type, machine count, provisioning status, image version, hypervisor connection.

### Delivery Group

Delivery Group xác định machine nào được cung cấp cho user/group nào và desktop/app nào user có thể dùng. Đây là nơi entitlement vận hành trong Citrix thường được nhìn thấy rõ.

**Khi lỗi thường thấy:** user không thấy resource, resource hiện sai nhóm, launch fail do thiếu available VDA.  
**Cần kiểm tra:** user/group assignment, machine availability, access policy, application assignment.

### Application Group

Application Group là cách gom ứng dụng published trong Citrix để quản lý access, visibility và phân tách workload/policy chi tiết hơn.

**Khi lỗi thường thấy:** app không hiện, app hiện sai nhóm, app launch vào sai workload.  
**Cần kiểm tra:** linked Delivery Group, user/group assignment, application properties, policy.

### Site Database

Site Database là database lưu cấu hình và trạng thái quan trọng của Citrix Site. Delivery Controller phụ thuộc vào database cho nhiều hoạt động quản trị và broker.

**Khi lỗi thường thấy:** Studio lỗi, Controller service degraded, config không đọc/ghi được.  
**Cần kiểm tra:** DB connectivity, SQL health, backup/HA, recent DB change.

### HDX và ICA

HDX là tập công nghệ trải nghiệm người dùng của Citrix. ICA là protocol/luồng kết nối session truyền display, input và virtual channels. Engineer không cần nhớ mọi chi tiết protocol lúc đầu, nhưng cần biết launch/session issue có thể khác với login issue.

**Khi lỗi thường thấy:** lag, disconnect, printer/clipboard/USB issue, display issue.  
**Cần kiểm tra:** session policy, network latency/loss, gateway, client version, virtual channel.

## 5. Omnissa Horizon Terms

### Omnissa Horizon

Omnissa Horizon, trước đây là VMware Horizon, là nền tảng VDI/application virtualization. Trong bối cảnh khách hàng, Horizon chạy trên HCI và phục vụ quy mô 1500-2000+ VDI.

**Cần nhớ:** Horizon gồm Client, UAG nếu external, Connection Server, desktop/application pool, entitlement, Horizon Agent, vCenter/HCI, storage và network.

### Horizon Client

Horizon Client là phần mềm hoặc client path để user đăng nhập và mở desktop/app. Một số môi trường cũng có access qua browser nếu cấu hình.

**Khi lỗi thường thấy:** client version cũ, certificate warning, launch protocol lỗi.  
**Cần kiểm tra:** client version, internal/external path, error screenshot, DNS/certificate.

### Connection Server

Connection Server là broker/control plane của Horizon. Nó xử lý authentication flow, entitlement, desktop pool và session brokering.

**Khi lỗi thường thấy:** user không thấy pool, launch fail, broker service issue, external integration với UAG lỗi.  
**Cần kiểm tra:** service health, entitlement, pool status, UAG integration, vCenter connectivity nếu liên quan.

### Unified Access Gateway

Unified Access Gateway, UAG, là gateway/edge component cho truy cập an toàn từ ngoài mạng vào Horizon. UAG giúp tránh expose trực tiếp Connection Server và desktop nội bộ.

**Khi lỗi thường thấy:** external user không login/launch được, certificate/TLS issue, tunnel/protocol timeout.  
**Cần kiểm tra:** UAG health, certificate, network path, backend Connection Server, firewall/LB.

### Horizon Agent

Horizon Agent là agent cài trên desktop/RDSH/physical host để Horizon có thể quản lý và cung cấp session.

**Khi lỗi thường thấy:** Agent unreachable, desktop unavailable, launch fail, black screen.  
**Cần kiểm tra:** Agent service, registration, DNS/domain, firewall, image/Agent version.

### Desktop Pool

Desktop Pool là nhóm desktop Horizon được cấp cho user. Pool có thể là dedicated, floating, persistent, non-persistent hoặc theo thiết kế cụ thể.

**Khi lỗi thường thấy:** pool không có available machine, user không thấy pool, desktop không registered.  
**Cần kiểm tra:** pool enabled, entitlement, machine state, image/snapshot, vCenter/HCI capacity.

### Application Pool

Application Pool trong Horizon cung cấp published application hoặc application resource cho user.

**Khi lỗi thường thấy:** app không hiện, launch fail, app backend lỗi.  
**Cần kiểm tra:** entitlement, application pool status, hosting desktop/RDSH, Agent state, backend dependency.

## 6. Access and Identity Terms

### Gateway

Gateway là lớp entry point, thường dùng cho user từ ngoài mạng hoặc để proxy session traffic. Trong Citrix là Citrix Gateway; trong Horizon là UAG.

**Khi lỗi thường thấy:** external-only issue, TLS warning, timeout, disconnect.  
**Cần nhớ:** gateway lỗi có thể làm user login/launch fail dù broker và desktop bên trong vẫn khỏe.

### Load Balancer

Load Balancer phân phối traffic tới nhiều gateway, broker hoặc portal node. Nó dùng VIP, health probe và member pool.

**Khi lỗi thường thấy:** một node down nhưng user vẫn bị đưa vào node lỗi, external/internal access không ổn định.  
**Cần kiểm tra:** VIP, member state, health probe, certificate binding, recent network change.

### Certificate

Certificate xác nhận danh tính dịch vụ và bảo vệ TLS. Nó thường liên quan portal, gateway, broker, load balancer và client trust.

**Khi lỗi thường thấy:** browser/client warning, login fail, gateway integration fail.  
**Cần kiểm tra:** expiry, CN/SAN, chain, binding target, trust.

### Active Directory

Active Directory là nền tảng identity cho user, group, computer account và policy trong môi trường Windows enterprise.

**Khi lỗi thường thấy:** login fail, user không thấy resource do group sai, VDA/Agent registration lỗi do domain/computer account.  
**Cần kiểm tra:** account state, group membership, OU/GPO, computer account, DC health.

### Domain Controller

Domain Controller cung cấp authentication, directory và domain services cho AD.

**Khi lỗi thường thấy:** nhiều user login fail, GPO chậm, domain join issue, time/auth errors.  
**Cần kiểm tra:** DC availability, DNS, replication, time sync, site/subnet mapping.

### DNS

DNS chuyển tên thành địa chỉ. Trong VDI, DNS lỗi có thể phá authentication, broker lookup, gateway access, Agent/VDA registration và profile/backend access.

**Khi lỗi thường thấy:** client không tới portal, Agent/VDA không đăng ký, profile/app path không resolve.  
**Cần kiểm tra:** forward lookup, reverse lookup nếu cần, split DNS, DNS server used.

### Group Policy

Group Policy, GPO, áp cấu hình Windows/user/computer theo AD. Nó có thể ảnh hưởng login, printer, drive mapping, security, scripts và user experience.

**Khi lỗi thường thấy:** login chậm, printer/drive mapping lỗi, policy không đúng nhóm.  
**Cần kiểm tra:** GPO processing, OU, security filtering, loopback processing nếu có.

### Entitlement

Entitlement là quyền user/group được truy cập resource VDI. Trong Horizon, entitlement gắn với pool. Trong Citrix, access thường gắn với Delivery Group/Application Group và AD group.

**Khi lỗi thường thấy:** user không thấy desktop/app hoặc thấy resource không nên thấy.  
**Cần kiểm tra:** AD group, assignment, effective access, recent entitlement change.

### Machine Identity

Machine identity là danh tính máy VDI trong domain hoặc hệ thống quản trị, gồm hostname, computer account, domain trust và đôi khi machine ID trong platform.

**Khi lỗi thường thấy:** Agent/VDA unregistered, GPO không apply, duplicate computer account.  
**Cần kiểm tra:** computer account, DNS, domain trust, naming convention.

## 7. Image, Provisioning and Allocation Terms

### Master Image hoặc Golden Image

Master image/golden image là image chuẩn dùng để tạo hoặc cập nhật nhiều VDI. Nó chứa OS, application, security tool, VDA/Horizon Agent và cấu hình cơ bản.

**Khi lỗi thường thấy:** sau publish image, nhiều VDI unregistered, app lỗi, black screen, login chậm.  
**Cần nhớ:** image change luôn cần pilot, rollback và postcheck.

### Snapshot

Snapshot là mốc trạng thái của VM/image tại một thời điểm. Nó thường dùng trước change hoặc làm mốc image deployment.

**Khi lỗi thường thấy:** snapshot tồn đọng làm datastore tăng, chọn nhầm snapshot khi publish image.  
**Cần nhớ:** snapshot không phải backup dài hạn.

### Provisioning

Provisioning là quá trình tạo hoặc chuẩn bị desktop/application resource: tạo VM, mở rộng pool/catalog, dùng image, gán vào delivery group/pool.

**Khi lỗi thường thấy:** machine tạo thất bại, không join domain, không registered, thiếu available machine.  
**Cần kiểm tra:** image, hypervisor task, datastore, naming, AD computer account, broker registration.

### Allocation

Allocation là cấp phát resource cho user hoặc group. Nó khác provisioning: resource có thể tồn tại nhưng chưa được cấp cho user.

**Khi lỗi thường thấy:** user không thấy desktop/app dù machine đang healthy.  
**Cần kiểm tra:** AD group, entitlement, assignment, approval.

### Persistent Desktop

Persistent desktop là desktop gắn với user và giữ trạng thái lâu dài hơn. Nó thường có rủi ro dữ liệu cao hơn khi thu hồi hoặc rebuild.

**Khi lỗi thường thấy:** mất dữ liệu nếu reclaim sai, profile/disk cần retention.  
**Cần kiểm tra:** assignment, backup/retention, user data policy.

### Non-persistent Desktop

Non-persistent desktop thường được refresh/recreate từ image, dữ liệu user nên nằm ở profile/container hoặc storage riêng.

**Khi lỗi thường thấy:** user mất setting nếu profile solution lỗi, image lỗi ảnh hưởng nhiều máy.  
**Cần kiểm tra:** profile path, image version, pool/catalog state.

## 8. Hypervisor and Storage Terms

### Virtual Machine

Virtual Machine, VM, là máy ảo chạy desktop, server hoặc thành phần hạ tầng. VDI desktop thường là VM hoặc session host tùy mô hình.

**Khi lỗi thường thấy:** powered off, stuck, snapshot issue, resource contention.  
**Cần kiểm tra:** power state, host, datastore, tools, task/event.

### VMware ESXi

ESXi là hypervisor chạy VM trong hệ sinh thái VMware. Với Horizon on HCI hoặc CVAD trên VMware, ESXi là lớp chạy desktop/server VM.

**Khi lỗi thường thấy:** host contention, VM restart, datastore path issue.  
**Cần kiểm tra:** host health, CPU/memory, datastore, network, VM events.

### vCenter

vCenter quản lý ESXi host, cluster, VM, datastore, network và task. Horizon/Citrix có thể tích hợp với vCenter để provision/quản lý VM.

**Khi lỗi thường thấy:** không power/clone được VM, hypervisor connection fail, inventory mismatch.  
**Cần kiểm tra:** vCenter service, permissions, cluster/host/datastore visibility, task log.

### XenServer

XenServer là hypervisor có thể dùng cho Citrix CVAD. Nó quản lý host pool, VM, storage repository và networking.

**Khi lỗi thường thấy:** VM provisioning fail, host/pool issue, storage repository unavailable.  
**Cần kiểm tra:** pool health, host, SR, VM state, network.

### HCI

HCI, Hyperconverged Infrastructure, là mô hình tích hợp compute, storage và networking trong cùng platform/cluster. Horizon system của khách hàng được mô tả chạy trên HCI.

**Khi lỗi thường thấy:** host/storage cùng ảnh hưởng VDI, datastore latency, cluster capacity.  
**Cần kiểm tra:** cluster health, node health, storage latency, capacity, resync/rebuild nếu có.

### Datastore

Datastore là nơi lưu VM disk, template, snapshot hoặc image trong VMware. Datastore capacity và latency ảnh hưởng trực tiếp VDI.

**Khi lỗi thường thấy:** datastore full, VM slow, provisioning fail, snapshot growth.  
**Cần kiểm tra:** free capacity, latency, IOPS, snapshot, affected VM/pool.

### Storage Repository

Storage Repository là khái niệm storage chứa VM/disk trong XenServer.

**Khi lỗi thường thấy:** VM không boot, provisioning fail, storage unavailable.  
**Cần kiểm tra:** SR state, capacity, path, host connectivity.

### IOPS, Latency, Throughput

IOPS là số thao tác I/O mỗi giây. Latency là độ trễ I/O. Throughput là băng thông dữ liệu. Trong VDI, latency thường ảnh hưởng user experience rõ rệt, đặc biệt khi login/boot storm.

**Khi lỗi thường thấy:** login chậm, desktop freeze, provisioning task chậm.  
**Cần kiểm tra:** trend theo timestamp, không chỉ một điểm đo.

## 9. Profile and User Experience Terms

### Profile

Profile chứa cấu hình và dữ liệu trạng thái của user: desktop settings, app settings, registry/user state và một phần dữ liệu tùy thiết kế.

**Khi lỗi thường thấy:** temporary profile, mất setting, login chậm, app reset.  
**Cần kiểm tra:** profile path, permission, lock file, profile solution, storage latency.

### FSLogix

FSLogix là giải pháp profile/container phổ biến trong môi trường Windows VDI, thường dùng profile container hoặc ODFC container.

**Khi lỗi thường thấy:** container không attach, profile locked, Cloud Cache issue, login chậm.  
**Cần kiểm tra:** container path, permission, lock, storage health, logs.

### Profile Container

Profile Container là file/container chứa profile user và được attach khi user login.

**Khi lỗi thường thấy:** attach fail, temporary profile, profile corrupt, storage latency.  
**Cần kiểm tra:** file path, permission, size, lock, storage metrics.

### Cloud Cache

Cloud Cache là cơ chế FSLogix hỗ trợ nhiều location cho container nhằm tăng khả năng chịu lỗi hoặc phân tán dữ liệu tùy thiết kế.

**Khi lỗi thường thấy:** sync conflict, location unavailable, login delay.  
**Cần kiểm tra:** location health, logs, replication/sync status.

### Boot Storm và Logon Storm

Boot storm là khi nhiều VDI boot cùng lúc. Logon storm là khi nhiều user login cùng lúc. Cả hai tạo tải lên storage, broker, domain controller, profile storage và network.

**Khi lỗi thường thấy:** đầu giờ sáng chậm, datastore latency, DC/GPO chậm, broker load cao.  
**Cần kiểm tra:** timeline, concurrent sessions, power schedule, storage/DC metrics.

## 10. Operations Terms

### Monitoring

Monitoring là quan sát trạng thái service, session, broker, gateway, VDI, host, storage, network và identity.

**Khi lỗi thường thấy:** không có alert trước incident, dashboard thiếu lớp.  
**Cần nhớ:** monitoring phải theo baseline/trend, không chỉ xem trạng thái xanh/đỏ.

### Alert

Alert là cảnh báo khi metric hoặc sự kiện vượt ngưỡng. Alert tốt phải có owner, severity, action và evidence.

**Khi lỗi thường thấy:** alert noise, alert không có owner, alert thiếu runbook.  
**Cần kiểm tra:** threshold, affected component, trend, duplicate alert.

### Incident

Incident là sự cố làm gián đoạn hoặc suy giảm dịch vụ. Trong VDI, incident cần phân loại theo impact: một user, một VDI, một pool/catalog, gateway, site, storage, network hoặc toàn platform.

**Cần nhớ:** incident classification quyết định priority và escalation.

### Change

Change là thay đổi có kiểm soát như image update, policy change, entitlement change, certificate change, broker patching, host maintenance hoặc storage expansion.

**Cần nhớ:** recent change là một trong những câu hỏi đầu tiên khi xử lý sự cố.

### Backup and Recovery

Backup/recovery bảo vệ khả năng phục hồi cấu hình, database, image, profile, gateway config, vCenter config và tài liệu vận hành.

**Cần nhớ:** backup job success chưa đủ; phải có restore validation.

### High Availability và Disaster Recovery

HA giúp chịu lỗi cục bộ. DR giúp phục hồi khi lỗi phạm vi lớn hơn. Trong VDI, HA/DR phải xét end-to-end: gateway, broker, database, identity, profile, storage, hypervisor và application backend.

### RBAC

RBAC, Role Based Access Control, là phân quyền theo vai trò. Trong VDI, cần phân biệt RBAC quản trị với entitlement user.

**Cần nhớ:** least privilege giảm rủi ro thao tác nhầm và tăng khả năng audit.

### Escalation

Escalation là chuyển ticket/sự cố tới nhóm có ownership hoặc quyền xử lý đúng lớp lỗi. Escalation tốt phải kèm evidence.

**Cần nhớ:** escalation không phải "đẩy việc đi"; nó là handoff có trách nhiệm.

## 11. Thuật ngữ dễ nhầm

| Dễ nhầm | Phân biệt nhanh |
|---|---|
| Broker vs Gateway | Broker chọn resource/session; gateway là entry/proxy access, nhất là external. |
| Entitlement vs RBAC | Entitlement cho user dùng desktop/app; RBAC cho engineer/admin vận hành hệ thống. |
| Machine Catalog vs Delivery Group | Catalog là nhóm machine; Delivery Group gán machine/app cho user/group. |
| Desktop Pool vs Delivery Group | Horizon dùng pool; Citrix dùng Delivery Group cho access/workload. |
| VDA vs Horizon Agent | VDA là agent Citrix; Horizon Agent là agent Horizon. |
| VM powered on vs desktop available | VM bật chưa đủ; Agent/VDA phải registered và resource phải available. |
| Snapshot vs Backup | Snapshot là mốc ngắn hạn; backup có retention/recovery purpose. |
| HA vs DR | HA chịu lỗi cục bộ; DR phục hồi khi sự cố lớn hơn. |
| Login fail vs Launch fail | Login fail xảy ra trước resource/session; launch fail xảy ra sau khi user thấy resource. |
| Profile issue vs Desktop issue | Desktop có thể healthy nhưng profile lỗi làm user experience hỏng. |

## 12. Knowledge Check

**Câu 1. Broker trong Citrix và Horizon tương ứng với thành phần nào?**  
Citrix: Delivery Controller. Horizon: Connection Server.

**Câu 2. VDA khác Horizon Agent thế nào?**  
VDA là agent của Citrix CVAD. Horizon Agent là agent của Omnissa Horizon. Cả hai giúp desktop/session nhận quản lý và kết nối từ broker.

**Câu 3. User login portal được nhưng không thấy desktop, nên nghĩ tới thuật ngữ nào?**  
Entitlement, AD group, Delivery Group/Desktop Pool, resource availability.

**Câu 4. Datastore full có thể gây lỗi gì?**  
Provisioning fail, VM slow, snapshot growth issue, boot/login chậm hoặc VM không hoạt động ổn định.

**Câu 5. Vì sao profile không đồng nghĩa với desktop?**  
Desktop là workload/session; profile là trạng thái/dữ liệu user. Desktop có thể chạy nhưng profile vẫn lỗi.

**Câu 6. Gateway lỗi thường biểu hiện thế nào?**  
External user không login/launch được, TLS warning, timeout, disconnect hoặc chỉ external path lỗi.

**Câu 7. Snapshot có nên xem là backup dài hạn không?**  
Không. Snapshot dùng ngắn hạn và có thể ảnh hưởng datastore nếu để lâu.

**Câu 8. RBAC khác entitlement như thế nào?**  
RBAC kiểm soát quyền quản trị của engineer/admin. Entitlement kiểm soát user được truy cập desktop/app nào.

## 13. Need Customer Confirmation

Các thông tin cần hỏi khách hàng:

- Tên gọi nội bộ cho Horizon system và Citrix system là gì?
- Các pool, catalog, Delivery Group, Application Group chính đang được đặt tên theo chuẩn nào?
- Khách hàng dùng persistent, non-persistent, dedicated hay pooled desktop cho từng nhóm user?
- Profile solution thực tế là FSLogix, Citrix Profile Management, roaming profile hay giải pháp khác?
- Gateway thật là Citrix Gateway, UAG, load balancer nào, có tên VIP nào?
- Monitoring dashboard nào hiển thị session, registration, failed session, storage latency và profile?
- Thuật ngữ nào trong đội khách hàng đang dùng khác vendor term?
- Có glossary nội bộ hoặc naming convention document không?
- Có thuật ngữ tiếng Việt/tiếng Anh bắt buộc dùng trong tài liệu khách hàng không?

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

### Concepts

- [[concepts/vdi-connection-flow]]
- [[concepts/omnissa-horizon]]
- [[concepts/connection-server]]
- [[concepts/unified-access-gateway]]
- [[concepts/citrix-virtual-apps-and-desktops]]
- [[concepts/delivery-controller]]
- [[concepts/storefront]]
- [[concepts/virtual-delivery-agent]]
- [[concepts/delivery-group]]
- [[concepts/hdx]]
- [[concepts/ica-virtual-channel]]
- [[concepts/display-protocol]]
- [[concepts/identity-and-access-management]]
- [[concepts/machine-identity]]
- [[concepts/vcenter-server]]
- [[concepts/esxi]]
- [[concepts/xenserver]]
- [[concepts/datastore]]
- [[concepts/storage-repository]]
- [[concepts/virtual-machine]]
- [[concepts/snapshot]]
- [[concepts/profile-container]]
- [[concepts/fslogix]]
- [[concepts/cloud-cache]]
- [[concepts/monitoring-and-logs]]
- [[concepts/change-management]]
- [[concepts/incident-management]]
- [[concepts/backup-and-recovery]]
- [[concepts/high-availability]]

### Topic documents

- [[topics/1_VDI_Foundation_Overview]]
- [[topics/3_Omnissa_Horizon_Architecture_Overview]]
- [[topics/4_Citrix_CVAD_Architecture_Overview]]
- [[topics/5_VDI_Access_Flow_Design]]
- [[topics/6_Identity_and_Domain_Integration_Guide]]
- [[topics/7_Hypervisor_and_HCI_Operations_Guide]]
- [[topics/8_Storage_Operations_for_VDI]]
- [[topics/11_VDI_Provisioning_and_Allocation_Guide]]
- [[topics/12_Master_Image_Management_Guide]]
- [[topics/13_Citrix_Machine_Catalog_and_Delivery_Group_Guide]]
- [[topics/14_Omnissa_Desktop_Pool_and_Entitlement_Guide]]
- [[topics/18_VDI_Troubleshooting_Playbook]]
- [[topics/26_VDI_Operational_Knowledge_Base]]

## 15. Summary for Learners

Khi gặp thuật ngữ mới trong VDI, engineer nên hỏi:

1. Thuật ngữ này thuộc lớp nào: user, gateway, broker, desktop, identity, hypervisor, storage, network hay operation?
2. Nó thuộc Horizon, Citrix hay dùng chung?
3. Nó ảnh hưởng user experience ở bước nào: login, enumerate, launch, session, profile hay app?
4. Khi nó lỗi, symptom thường là gì?
5. Cần kiểm tra console/dashboard/log nào?
6. Tài liệu nào trong bộ wiki giải thích sâu hơn?

Điều cần nhớ nhất: hiểu thuật ngữ không phải để nói cho đúng tên sản phẩm, mà để khoanh vùng lỗi nhanh hơn. Một từ như "broker", "gateway", "profile" hay "datastore" đại diện cho cả một lớp dependency trong vận hành VDI.

## 16. Self Review

- [x] Đúng tên tài liệu trong list_context.txt.
- [x] Đúng tên file trong cột Name File.
- [x] Đúng mục đích: giải thích broker, VDA, Horizon Agent, pool, catalog, delivery group, entitlement, profile, gateway, datastore, session và image.
- [x] Bám bối cảnh training_idea.md: Horizon on HCI, Citrix CVAD trên XenServer/ESXi, quy mô 1500-2000+ VDI.
- [x] Không bịa tên object, version, naming convention hoặc thuật ngữ nội bộ khách hàng.
- [x] Có phân biệt Need Customer Confirmation.
- [x] Có giải thích theo hướng đào tạo vận hành, không chỉ dịch thuật ngữ.
- [x] Có chỉ ra lỗi liên quan và điểm cần kiểm tra.
- [x] Có knowledge check, thuật ngữ dễ nhầm và related links.
- [x] Phù hợp cho system engineer mới tiếp cận VDI.
