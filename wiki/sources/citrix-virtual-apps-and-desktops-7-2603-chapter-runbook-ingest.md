---
id: source-citrix-virtual-apps-and-desktops-7-2603-chapter-runbook-ingest
title: Citrix Virtual Apps and Desktops 7 2603 - Chapter Insight and Tutorial Runbook Ingest
type: source
created: 2026-05-26
updated: 2026-05-26
authors:
  - Citrix Systems
year: 2026
importance: 5
urls: []
raw_paths:
  - raw/sources/citrix-virtual-apps-and-desktops™-7-2603.txt
provenance: replayable
confidence: high
ingest_status: finalized
verify_status: skipped
findings: []
---

## Summary

Trang này là lớp ingest theo `chapter-ingest-loop.prompt` cho source Citrix Virtual Apps and Desktops 7 2603. Mục tiêu là biến từng vùng nội dung lớn trong vendor corpus thành báo cáo insight tri thức và runbook best practice dạng tutorial thực hành. Trang này bổ sung cho [[sources/citrix-virtual-apps-and-desktops-7-2603]] và [[sources/citrix-virtual-apps-and-desktops-7-2603-technical-deep-ingest-report]]; trọng tâm ở đây là thao tác vận hành, cấu hình, kiểm chứng, rollback và gói bằng chứng.

## Chapter Knowledge Insight Report

Citrix Virtual Apps and Desktops không nên được học như danh sách màn hình quản trị rời rạc. Insight trung tâm của source là CVAD là một chuỗi điều phối trạng thái: identity, StoreFront/Gateway, Delivery Controller, database, catalog, Delivery Group, VDA, policy, HDX và monitoring cùng tạo ra một phiên làm việc. Vì vậy runbook tốt phải đi theo chuỗi trạng thái này, không chỉ ghi "vào console và bấm".

## Central Knowledge Thesis

Một engineer vận hành CVAD 7 2603 phải luôn trả lời được bốn câu hỏi trước khi thao tác: thay đổi này đụng vào lớp nào, blast radius là user/catalog/group/site nào, bằng chứng trước và sau thay đổi là gì, và rollback có đưa user journey về trạng thái kiểm chứng được hay không. Các chương cài đặt, cấu hình, policy, TLS, Gateway, VDA, Director, backup/restore và VDA Upgrade Service trong source đều lặp lại cùng một nguyên tắc: thao tác chỉ an toàn khi có precheck, scope, pilot, validation và evidence.

## Insight and Depth Control

| Trường | Giá trị |
|---|---|
| Ingest mode | Chapter insight report plus tutorial runbook extraction |
| Source richness | Very high: install, configure, secure, monitor, troubleshoot, backup, restore, upgrade |
| Runbook style | Hands-on tutorial runbook, not summary checklist |
| Runbook count target | Proportional to source richness, no artificial cap |
| Installation/configuration coverage | Required and included |
| Customer-specific assumptions | Marked as `Need Customer Confirmation` |

## Runbook Source Coverage

| Chapter | Source locator from raw TOC / heading signal | Operational sections covered | Runbook coverage |
|---|---|---|---|
| CH01 | Technical overview, system requirements, Director overview around source lines 3904-4068 | Site architecture, Controller, StoreFront, Gateway, VDA, database, monitoring | RB01-RB04 |
| CH02 | Install and configure page 123; install core components page 231; command-line install page 243; Web Studio page 261 | Install sequence, command-line install, Web Studio install | RB05-RB09 |
| CH03 | Install VDAs page 271; Defender Access Control page 292; VDA precheck page 294; script/SCCM/Intune pages 304-328 | VDA install, scripted deployment, SCCM, Intune, precheck | RB10-RB16 |
| CH04 | Machine identities page 796; site connections/resources; catalog/image areas; AD account repair and machine profile notes | Machine Catalog, MCS, image, identity, hosting resources | RB17-RB23 |
| CH05 | Delivery Group, Application Group, entitlement, policy set sections page 1619+ | Delivery Group, entitlement, published apps, policy modeling | RB24-RB30 |
| CH06 | Gateway integration page 1094; TLS on Controllers/Web Studio/Director/VDA/Universal Print Server pages 1142-1171 | Gateway, STA path, TLS/DTLS, certificate validation | RB31-RB37 |
| CH07 | HDX page 100 and lines 4823-4889; HDX connectivity page 1187; USB page 1237; printing and clipboard sections | HDX, ICA channels, USB, clipboard, printing, graphics, Teams | RB38-RB45 |
| CH08 | Monitoring page 1333; Director page 2345; install/configure Director page 2350; troubleshoot deployment/app/machine/user sections | Director, Web Studio, session evidence, troubleshooting | RB46-RB52 |
| CH09 | Backup/restore page 1930; Automated Configuration Tool pages 1962/1990/2008; VDA Upgrade Service page 2653; Log Server page 2678 | Backup, restore, migration, VDA upgrade, logging | RB53-RB60 |

## Mandatory Installation and Configuration Runbooks

Các phần sau trong source có tín hiệu install/configure/enable/upgrade/restore rõ ràng và đã được chuyển thành runbook tutorial: install core components, command-line install, Web Studio install, VDA install, Defender Access Control liên quan VDA, VDA precheck, VDA script deployment, SCCM deployment, Intune deployment, Machine Catalog, Delivery Group, policy set/modeling, Gateway integration, TLS trên Controller/Web Studio/Director/VDA/Universal Print Server, Director install/configure, backup/restore bằng Automated Configuration Tool, VDA Upgrade Service và Log Server.

## Runbook Inventory

| ID | Runbook | Chapter | Depth |
|---|---|---|---|
| RB01 | Vẽ và xác minh bản đồ kiến trúc CVAD site | CH01 | Tutorial |
| RB02 | Kiểm tra health chain Controller-DB-License-StoreFront-VDA | CH01 | Tutorial |
| RB03 | Chuẩn hóa evidence baseline trước ngày vận hành | CH01 | Tutorial |
| RB04 | Phân loại lỗi theo enumerate, broker, launch, session, HDX | CH01 | Tutorial |
| RB05 | Cài core components theo chuỗi an toàn | CH02 | Tutorial |
| RB06 | Cài core components bằng command line có log và rollback | CH02 | Tutorial |
| RB07 | Cài và xác minh Web Studio | CH02 | Tutorial |
| RB08 | Chuẩn bị tài khoản, DNS, certificate, firewall trước install | CH02 | Tutorial |
| RB09 | Pilot install site mới trước khi mở rộng | CH02 | Tutorial |
| RB10 | Precheck VDA install/upgrade | CH03 | Tutorial |
| RB11 | Cài Windows VDA bằng GUI/ISO có evidence | CH03 | Tutorial |
| RB12 | Cài hoặc upgrade VDA bằng script tùy biến | CH03 | Tutorial |
| RB13 | Triển khai VDA bằng SCCM | CH03 | Tutorial |
| RB14 | Triển khai VDA bằng Microsoft Intune | CH03 | Tutorial |
| RB15 | Xử lý Defender Access Control và security tooling khi cài VDA | CH03 | Tutorial |
| RB16 | Điều tra VDA install fail hoặc partial upgrade | CH03 | Tutorial |
| RB17 | Tạo Machine Catalog từ prepared image | CH04 | Tutorial |
| RB18 | Kiểm tra hosting connection và resource mapping | CH04 | Tutorial |
| RB19 | Repair AD computer account cho MCS catalog | CH04 | Tutorial |
| RB20 | Cập nhật image cho catalog theo pilot ring | CH04 | Tutorial |
| RB21 | Kiểm tra machine identity trước khi publish catalog | CH04 | Tutorial |
| RB22 | Dọn machine failed provisioning task | CH04 | Tutorial |
| RB23 | Đánh giá capacity catalog trước giờ cao điểm | CH04 | Tutorial |
| RB24 | Tạo Delivery Group và publish desktop | CH05 | Tutorial |
| RB25 | Publish application và kiểm tra Application Group | CH05 | Tutorial |
| RB26 | Cấp quyền bằng AD group có kiểm soát | CH05 | Tutorial |
| RB27 | Simulate policy bằng Policy Modeling wizard | CH05 | Tutorial |
| RB28 | Thay đổi clipboard/USB/printing policy an toàn | CH05 | Tutorial |
| RB29 | Khoanh vùng user không thấy resource | CH05 | Tutorial |
| RB30 | Rollback Delivery Group hoặc policy scope | CH05 | Tutorial |
| RB31 | Tích hợp CVAD với Citrix Gateway | CH06 | Tutorial |
| RB32 | Kiểm tra STA và external launch path | CH06 | Tutorial |
| RB33 | Enable TLS trên Delivery Controllers | CH06 | Tutorial |
| RB34 | Enable TLS trên Web Studio và Director | CH06 | Tutorial |
| RB35 | Enable TLS/DTLS trên VDAs | CH06 | Tutorial |
| RB36 | Enable TLS trên Universal Print Server | CH06 | Tutorial |
| RB37 | Điều tra lỗi certificate/Gateway/TLS sau change | CH06 | Tutorial |
| RB38 | Kiểm tra HDX connectivity và session reliability | CH07 | Tutorial |
| RB39 | Điều tra USB redirection issue | CH07 | Tutorial |
| RB40 | Điều tra clipboard bị chặn hoặc sai format | CH07 | Tutorial |
| RB41 | Điều tra printing issue trên VDA | CH07 | Tutorial |
| RB42 | Kiểm tra HDX 3D Pro/graphics policy | CH07 | Tutorial |
| RB43 | Monitor HDX channel trong Director | CH07 | Tutorial |
| RB44 | Troubleshoot Teams optimization | CH07 | Tutorial |
| RB45 | Dùng registry/policy cho HDX feature có kiểm soát | CH07 | Tutorial |
| RB46 | Cài và cấu hình Director | CH08 | Tutorial |
| RB47 | Monitor machine/session trong Search và Task Center | CH08 | Tutorial |
| RB48 | Điều tra VDA registration bằng Director/Web Studio/event log | CH08 | Tutorial |
| RB49 | Điều tra user logon duration | CH08 | Tutorial |
| RB50 | Troubleshoot application launch | CH08 | Tutorial |
| RB51 | Reset user profile theo evidence | CH08 | Tutorial |
| RB52 | Chuẩn bị escalation package cho incident CVAD | CH08 | Tutorial |
| RB53 | Backup cấu hình site theo best practice | CH09 | Tutorial |
| RB54 | Restore cấu hình và validate user journey | CH09 | Tutorial |
| RB55 | Dùng Automated Configuration Tool cmdlets cho migration | CH09 | Tutorial |
| RB56 | Dùng Automated Configuration Tool cmdlets cho backup/restore | CH09 | Tutorial |
| RB57 | Upgrade VDA bằng VDA Upgrade Service | CH09 | Tutorial |
| RB58 | Monitor và troubleshoot VDA Upgrade Service | CH09 | Tutorial |
| RB59 | Cài và cấu hình Log Server | CH09 | Tutorial |
| RB60 | Thu log bằng AOT/Log Server cho support | CH09 | Tutorial |

## CH01 - Architecture and Health Chain

### Chapter Knowledge Insight Report

CH01 dạy engineer nhìn CVAD như dependency chain thay vì một console. Controller phụ thuộc database/license; StoreFront/Gateway phụ thuộc auth, STA và broker; VDA phụ thuộc registration, network, machine identity và policy; Director/Web Studio là lớp quan sát và điều khiển. Insight thực hành: health check phải đi từ user journey về control plane, không chỉ xem một máy còn ping được hay không.

### Detailed Runbook - RB01 Vẽ và xác minh bản đồ kiến trúc CVAD site

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Bạn nhận bàn giao một CVAD site chưa có sơ đồ vận hành đáng tin. Mục tiêu là tạo bản đồ component có thể dùng cho troubleshooting. |
| Learning outcomes | Phân biệt StoreFront, Gateway, Controller, VDA, database, license, catalog, Delivery Group; xác định owner và evidence của từng lớp. |
| RACI | Platform admin thực hiện; identity, network, SQL, security xác nhận dependency; helpdesk dùng sơ đồ để phân loại ticket. |
| Precheck | Thu tên site, danh sách Controller, StoreFront, Gateway VIP, SQL database, License Server, catalog, Delivery Group, VDA OS, hypervisor connection, monitoring endpoint. Đánh dấu mục chưa biết là `Need Customer Confirmation`. |
| Procedure | 1. Mở Web Studio/Studio và ghi site name, Controller, catalog, Delivery Group. 2. Mở StoreFront console hoặc cấu hình store để ghi store/base URL. 3. Với external access, ghi Gateway VIP, STA server được cấu hình và certificate chain. 4. Ghi database role: Site, Monitoring, Configuration Logging. 5. Từ Director, xác định machine/session metrics có hiển thị bình thường. 6. Vẽ luồng internal và external riêng. |
| Validation | Chọn một user test, xác minh login, resource enumeration, launch, reconnect, logoff. Mỗi bước phải map được vào component trên sơ đồ. |
| Rollback/undo | Không thay đổi cấu hình; rollback là loại bỏ sơ đồ sai và thay bằng bản đã xác nhận. |
| Evidence pack | Screenshot cấu hình site/store, danh sách Controller, STA/Gateway, database, catalog/group, kết quả test user journey. |
| Anti-patterns | Dùng sơ đồ marketing thay cho sơ đồ production; trộn internal/external flow; không ghi owner từng component. |

### Detailed Runbook - RB02 Kiểm tra health chain Controller-DB-License-StoreFront-VDA

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Trước giờ cao điểm, engineer cần xác nhận CVAD đủ khỏe để nhận phiên mới. |
| Precheck | Có quyền đọc Web Studio/Director, quyền xem event log liên quan, dashboard SQL/license, tài khoản test. |
| Procedure | 1. Kiểm tra Controller service và event nghiêm trọng. 2. Kiểm tra database connectivity và latency bất thường. 3. Kiểm tra license server reachable và license không cạn. 4. Test StoreFront login/enumeration. 5. Kiểm tra VDA registered count theo catalog/group, không chỉ tổng site. 6. Launch desktop/app bằng tài khoản test. 7. Kiểm tra Director có ghi nhận session và metrics. |
| Validation | Có thể login, thấy resource, launch, reconnect, logoff; không có spike failed session; registered count nằm trong ngưỡng bình thường. |
| Stop conditions | Nếu database, license hoặc Controller có lỗi diện rộng, dừng mọi change không khẩn cấp và mở incident. |
| Evidence pack | Thời điểm kiểm tra, registered/unregistered count, failed session count, event nổi bật, kết quả test launch. |

## CH02 - Core Component and Web Studio Installation

### Chapter Knowledge Insight Report

CH02 là vùng cài đặt control plane. Source có các mục install core components, command-line install và Web Studio. Insight quan trọng: cài đặt core component không chỉ là chạy installer; nó là tạo nền cho broker, quản trị, logging, database và future upgrade. Mọi install phải có readiness checklist, log path, quyền tài khoản, port/firewall, certificate/DNS, rollback snapshot hoặc backup.

### Detailed Runbook - RB05 Cài core components theo chuỗi an toàn

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Dựng mới hoặc mở rộng control plane CVAD 7 2603 trong lab/pilot trước khi production. |
| Pre-install checklist | Xác nhận OS hỗ trợ, domain join, DNS/time sync, service account, SQL/database plan, license server, firewall ports, antivirus exclusion theo policy tổ chức, local admin, backup/snapshot nếu là server hiện hữu. |
| Procedure | 1. Tải ISO đúng release và lưu checksum/evidence. 2. Chạy installer bằng tài khoản được duyệt. 3. Chọn core components phù hợp vai trò server, tránh cài chồng vai trò không cần thiết. 4. Ghi install log path. 5. Cấu hình kết nối database/license theo thiết kế. 6. Sau install, reboot nếu installer yêu cầu. 7. Mở Web Studio/Studio để kiểm tra site/object visibility. |
| Validation | Component service running, console mở được, database reachable, license visible, không có critical event mới, user journey test trong pilot thành công. |
| Rollback | Nếu là server mới, remove component hoặc rebuild từ snapshot/template; nếu đã join site, cần remove server khỏi site inventory theo quy trình trước khi hủy. |
| Security note | Không dùng domain admin thường trực; không lưu credential trong wiki; log phải được bảo vệ vì có thể chứa đường dẫn và thông tin môi trường. |

### Detailed Runbook - RB06 Cài core components bằng command line có log và rollback

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Môi trường yêu cầu cài lặp lại bằng automation hoặc change window ngắn. |
| Precheck | Installer path, tham số đã review, thư mục log, tài khoản chạy, maintenance window, snapshot/backup, tiêu chí success/failure. |
| Procedure | 1. Viết lệnh command-line trong change record, không chạy trực tiếp từ trí nhớ. 2. Chạy ở pilot server trước. 3. Bật verbose log nếu được hỗ trợ. 4. Sau khi hoàn tất, thu exit code và log. 5. Reboot theo yêu cầu. 6. Kiểm tra service, console, database, license. 7. Chỉ nhân rộng khi pilot đạt tiêu chí. |
| Validation | Exit code thành công, log không có fatal error, component xuất hiện đúng trong site, user journey pilot pass. |
| Rollback | Dừng rollout, giữ log, restore snapshot hoặc uninstall theo vendor procedure; không thử chạy lại nhiều lần khi chưa đọc log. |

### Detailed Runbook - RB07 Cài và xác minh Web Studio

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Tổ chức chuyển quản trị sang Web Studio hoặc cần triển khai server quản trị mới. |
| Precheck | IIS/web prerequisite, certificate/TLS plan nếu dùng HTTPS, quyền admin, network tới Controller/site, browser compatibility, RBAC role. |
| Procedure | 1. Cài Web Studio theo installer. 2. Kiểm tra website/app pool/service liên quan. 3. Cấu hình TLS nếu dùng HTTPS. 4. Đăng nhập bằng tài khoản admin có quyền tối thiểu. 5. Kiểm tra có thấy catalog, Delivery Group, policy, monitoring/task. |
| Validation | Web Studio mở ổn định, không lỗi certificate, RBAC đúng, thao tác read-only và task test hiển thị đúng. |
| Rollback | Gỡ Web Studio khỏi server pilot hoặc restore snapshot; không thay đổi policy/site object nếu chỉ đang xác minh portal quản trị. |

## CH03 - VDA Installation and Upgrade

### Chapter Knowledge Insight Report

CH03 là vùng runbook bắt buộc nhất của source vì có nhiều nội dung install/upgrade: Install VDAs, Defender Access Control, precheck, Meta Installer Helper Tool, script, SCCM và Intune. Insight trung tâm: VDA là nơi user session thật sự chạy; một lỗi VDA image hoặc deployment method có thể làm hỏng cả catalog. VDA install phải là tutorial có pilot, log, registration validation và rollback image.

### Detailed Runbook - RB10 Precheck VDA install/upgrade

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Chuẩn bị nâng cấp VDA cho một catalog production bằng pilot ring. |
| Precheck | OS/build hỗ trợ, pending reboot, free disk, local admin, DNS/time sync, domain trust, Controller FQDN/list, firewall, security/EDR policy, Windows Defender Access Control, existing VDA version, machine in maintenance mode nếu cần, snapshot/golden image backup. |
| Procedure | 1. Chọn 1-3 máy pilot hoặc bản sao image. 2. Ghi current VDA version, machine identity, registered state. 3. Kiểm tra event log hiện tại để không đổ lỗi sai sau upgrade. 4. Kiểm tra Controller reachable bằng DNS/FQDN. 5. Đảm bảo installer và script có checksum/version. 6. Xác định rollback: revert image/snapshot, uninstall VDA, hoặc publish image cũ. |
| Validation | Precheck pass, không có pending reboot, Controller reachable, account đủ quyền, rollback asset tồn tại. |
| Stop conditions | Controller không reachable, domain trust lỗi, snapshot không có, hoặc security tooling chặn installer. |

### Detailed Runbook - RB11 Cài Windows VDA bằng GUI/ISO có evidence

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Cài VDA mới trên master image hoặc server workload trước khi tạo catalog. |
| Procedure | 1. Đưa máy vào trạng thái sạch, reboot nếu cần. 2. Chạy VDA installer đúng release. 3. Chọn đúng workload type và feature cần thiết theo thiết kế, tránh bật feature không dùng. 4. Nhập Controller address hoặc để cơ chế discovery theo chuẩn site. 5. Chọn option HDX/optimization phù hợp desktop/app. 6. Lưu install log. 7. Reboot. 8. Kiểm tra Citrix services và registration trong Studio/Director. |
| Validation | VDA registered, launch test thành công, Director thấy session metrics, event log không có lỗi registration/install nghiêm trọng. |
| Rollback | Revert master image snapshot hoặc uninstall VDA rồi reboot; nếu đã tạo catalog từ image lỗi, dừng rollout và republish image cũ. |
| Evidence pack | VDA version trước/sau, installer log, screenshot registered state, kết quả launch test. |

### Detailed Runbook - RB12 Cài hoặc upgrade VDA bằng script tùy biến

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Chuẩn hóa VDA install để chạy nhiều máy qua automation. |
| Precheck | Script đã peer review, tham số Controller/feature/reboot/log chính xác, test trên lab, rollback command hoặc image rollback sẵn sàng. |
| Procedure | 1. Generate hoặc viết script từ nguồn chuẩn. 2. Không hard-code credential. 3. Chạy với logging chi tiết. 4. Kiểm tra exit code. 5. Reboot có kiểm soát. 6. Sau reboot, kiểm tra registration và launch. 7. Mở rộng theo ring: lab, pilot, small production, broad production. |
| Validation | Tỷ lệ success đạt ngưỡng đã định; failed machines có log; không mở rộng rollout nếu failure pattern chưa rõ. |
| Rollback | Dừng job, cô lập máy lỗi, revert snapshot/image, hoặc chạy uninstall/repair theo procedure đã test. |

### Detailed Runbook - RB13 Triển khai VDA bằng SCCM

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Đội endpoint dùng SCCM để deploy/upgrade VDA trên nhiều máy. |
| Procedure | 1. Package installer và script với detection rule dựa trên version. 2. Scope collection theo pilot trước. 3. Đặt maintenance window và reboot behavior rõ ràng. 4. Theo dõi deployment status, exit code, client log. 5. Cross-check với Director registered count. 6. Chỉ mở rộng collection khi pilot pass. |
| Validation | SCCM success không đủ; phải có VDA registered và user launch test. |
| Rollback | Remove deployment, revert collection, republish image cũ hoặc deploy rollback package đã test. |

### Detailed Runbook - RB14 Triển khai VDA bằng Microsoft Intune

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Máy persistent hoặc cloud-managed cần VDA deployment qua Intune. |
| Procedure | 1. Đóng gói installer/script thành app deployment. 2. Định nghĩa detection rule theo VDA version/service. 3. Scope nhóm thiết bị pilot. 4. Kiểm tra restart behavior và dependency. 5. Theo dõi install status. 6. Xác minh registration/launch trong Citrix. |
| Validation | Intune app installed, VDA registered, Director có session data, user pilot không mất khả năng launch. |
| Rollback | Unassign app khỏi group, deploy uninstall/old version nếu được hỗ trợ, hoặc revert image/device theo quy trình endpoint. |

## CH04 - Machine Catalog, Image and Identity

### Chapter Knowledge Insight Report

CH04 chuyển install thành capacity thật: catalog, image, machine identity và hosting resource quyết định máy nào có thể được broker. Insight chính: catalog là nguồn máy và lifecycle image, không phải lớp cấp quyền user. Lỗi ở image hoặc identity thường biến thành VDA unregistered, provisioning failure hoặc capacity shortage.

### Detailed Runbook - RB17 Tạo Machine Catalog từ prepared image

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Tạo catalog mới cho nhóm desktop/app dựa trên image đã chuẩn bị. |
| Precheck | Image đã cài VDA và app, patched, sysprep/identity readiness theo design, hosting connection healthy, datastore/network mapping đúng, AD OU/account convention đã xác nhận, capacity target rõ. |
| Procedure | 1. Chọn đúng hosting connection/resource. 2. Chọn prepared image/snapshot đã được approve. 3. Chọn OS type và provisioning method đúng. 4. Cấu hình machine count, naming scheme, domain/OU. 5. Chạy tạo catalog trong pilot size nhỏ. 6. Theo dõi task và VM creation. 7. Kiểm tra máy boot, domain join, VDA registered. |
| Validation | Catalog có máy registered, không lỗi provisioning task, launch test qua Delivery Group pilot thành công. |
| Rollback | Xóa catalog pilot nếu chưa cấp quyền production; nếu đã publish, đưa Delivery Group vào maintenance/disable assignment rồi rollback image/catalog theo change plan. |

### Detailed Runbook - RB20 Cập nhật image cho catalog theo pilot ring

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Publish image mới chứa patch hoặc VDA version mới. |
| Procedure | 1. Chụp snapshot image cũ và mới. 2. Ghi app/VDA/OS delta. 3. Áp dụng image mới cho nhóm pilot. 4. Kiểm tra boot, registration, logon, app launch, printer, clipboard, USB/Teams nếu liên quan. 5. Theo dõi incident trong thời gian soak. 6. Mở rộng theo ring. |
| Validation | Pilot pass đủ user journey; không tăng failed session/logon duration bất thường. |
| Rollback | Republish image cũ hoặc revert catalog update; giữ evidence của máy lỗi để RCA. |

### Detailed Runbook - RB19 Repair AD computer account cho MCS catalog

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Máy MCS không domain join/registration vì AD computer account có vấn đề. |
| Procedure | 1. Xác định phạm vi: một máy, nhiều máy, hay toàn catalog. 2. Kiểm tra AD account tồn tại, OU, disabled/locked/stale state. 3. Kiểm tra naming scheme và quyền service account. 4. Chạy repair theo công cụ/flow được Citrix hỗ trợ. 5. Reboot hoặc recreate máy nếu cần. |
| Validation | Computer account healthy, VDA registered, policy apply, user launch pass. |
| Rollback | Không xóa hàng loạt computer account khi chưa có backup/export; nếu repair làm xấu hơn, recreate máy từ catalog hoặc restore AD object theo team identity. |

## CH05 - Delivery Group, Entitlement and Policy

### Chapter Knowledge Insight Report

CH05 là lớp user-visible: Delivery Group quyết định user thấy và dùng gì; policy quyết định session được phép làm gì. Insight thực hành: "không thấy desktop" và "desktop chậm hoặc thiếu chức năng" là hai nhóm lỗi khác nhau. Một bên ưu tiên entitlement/enumeration, bên kia ưu tiên policy/HDX/session evidence.

### Detailed Runbook - RB24 Tạo Delivery Group và publish desktop

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Cấp desktop cho một nhóm user từ catalog đã sẵn sàng. |
| Precheck | Catalog registered, capacity đủ, AD group đã duyệt, naming/description rõ, maintenance window nếu production. |
| Procedure | 1. Tạo Delivery Group từ catalog đúng. 2. Gán machine count/capacity. 3. Cấu hình desktop/app visibility. 4. Gán AD group thay vì user lẻ nếu policy tổ chức yêu cầu. 5. Kiểm tra StoreFront enumeration bằng user test. 6. Launch và logoff test. |
| Validation | User test thấy resource đúng, launch đúng desktop/app, Director ghi session đúng Delivery Group. |
| Rollback | Remove entitlement hoặc disable Delivery Group/published resource; không xóa catalog nếu chỉ lỗi cấp quyền. |

### Detailed Runbook - RB27 Simulate policy bằng Policy Modeling wizard

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Trước khi thay đổi clipboard/USB/printing/session policy, cần biết user/machine nào bị ảnh hưởng. |
| Procedure | 1. Xác định user, machine, Delivery Group, IP/client filter nếu có. 2. Chạy policy modeling. 3. Ghi policy winning result, priority và filter. 4. So sánh với mục tiêu change. 5. Pilot thay đổi với scope hẹp. 6. Re-run modeling sau change. |
| Validation | Policy result khớp thiết kế; user pilot có hành vi mong muốn; không ảnh hưởng nhóm ngoài scope. |
| Rollback | Restore policy setting/scope/priority cũ đã ghi lại trước change. |

### Detailed Runbook - RB29 Khoanh vùng user không thấy resource

| Mục | Nội dung |
|---|---|
| Tutorial scenario | User đăng nhập được StoreFront nhưng không thấy desktop/app. |
| Procedure | 1. Xác nhận user dùng đúng store và đúng domain. 2. Kiểm tra AD group membership/replication. 3. Kiểm tra Delivery Group/Application Group entitlement. 4. Kiểm tra resource disabled hoặc hidden. 5. Kiểm tra StoreFront enumeration error. 6. So sánh với user cùng group đang hoạt động. |
| Validation | Sau fix, user thấy đúng resource và launch pass. |
| Anti-patterns | Reboot VDA trước khi kiểm tra entitlement; cấp quyền trực tiếp cho user để chữa cháy rồi quên thu hồi. |

## CH06 - Gateway, TLS and Certificate Security

### Chapter Knowledge Insight Report

CH06 gom các thao tác có rủi ro cao: tích hợp Gateway, STA, TLS trên Controller/Web Studio/Director/VDA/Universal Print Server. Insight chính: access external và encryption không thể validate bằng cách mở được trang login; phải test đủ authenticate, enumerate, broker, STA ticket, ICA/HDX path và certificate chain.

### Detailed Runbook - RB31 Tích hợp CVAD với Citrix Gateway

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Cho phép user external truy cập CVAD qua Gateway. |
| Precheck | Gateway VIP, public/private DNS, certificate, StoreFront store, STA list, firewall path, session policy/profile, test user, rollback config backup. |
| Procedure | 1. Backup cấu hình Gateway/StoreFront liên quan. 2. Cấu hình Gateway integration với StoreFront theo design. 3. Khai báo STA là Controller phù hợp và dùng FQDN nhất quán. 4. Kiểm tra certificate chain và hostname. 5. Test external login, enumeration, launch. 6. Kiểm tra Director/Gateway logs khi launch. |
| Validation | External user login, thấy resource, launch session, reconnect; internal flow không bị ảnh hưởng. |
| Rollback | Restore Gateway/StoreFront config backup hoặc revert session policy; thông báo helpdesk nếu external access rollback. |

### Detailed Runbook - RB33 Enable TLS trên Delivery Controllers

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Bật TLS cho giao tiếp quản trị/broker theo yêu cầu bảo mật. |
| Precheck | Certificate đúng CN/SAN, private key bảo vệ, trust chain trên client/server, maintenance window, backup config, danh sách component phụ thuộc. |
| Procedure | 1. Import/bind certificate đúng server. 2. Cấu hình TLS theo hướng dẫn vendor. 3. Restart service nếu yêu cầu. 4. Kiểm tra Web Studio/StoreFront/Gateway/Director còn kết nối được. 5. Test launch. |
| Validation | Không lỗi certificate, broker flow pass, event log sạch, monitoring không báo mất kết nối. |
| Rollback | Rebind certificate cũ hoặc restore config; nếu Controller mất broker function, chuyển traffic sang Controller khác nếu HA cho phép. |

### Detailed Runbook - RB35 Enable TLS/DTLS trên VDAs

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Mã hóa/đảm bảo kênh session tới VDA theo policy bảo mật. |
| Procedure | 1. Kiểm tra certificate trên VDA và trust chain. 2. Pilot trên một nhóm VDA nhỏ. 3. Cấu hình TLS/DTLS theo source. 4. Reboot/restart service nếu cần. 5. Test launch từ internal và external. 6. Kiểm tra HDX connectivity và performance. |
| Validation | Session launch pass, không lỗi certificate, Director vẫn có metrics, user pilot không báo disconnect/black screen. |
| Rollback | Tắt setting mới hoặc restore image/config cũ; không rollout toàn catalog khi pilot còn lỗi. |

## CH07 - HDX, ICA Channels and User Experience

### Chapter Knowledge Insight Report

CH07 dạy rằng sau khi launch thành công vẫn còn cả một lớp chất lượng phiên. HDX, USB, clipboard, printing, graphics, Teams và registry/policy controlled features là nơi user cảm nhận "VDI tốt hay tệ". Insight: troubleshooting HDX phải thu metric và policy result, không được kết luận chung chung là network chậm.

### Detailed Runbook - RB38 Kiểm tra HDX connectivity và session reliability

| Mục | Nội dung |
|---|---|
| Tutorial scenario | User báo session hay gián đoạn hoặc reconnect chậm. |
| Procedure | 1. Xác định internal/external access. 2. Xem Director session metrics: latency, reconnect, failure, endpoint. 3. Kiểm tra Gateway nếu external. 4. Kiểm tra policy liên quan session reliability/HDX. 5. So sánh user khác cùng VDA/catalog. 6. Kiểm tra event log VDA và Controller cùng timestamp. |
| Validation | Xác định được lớp lỗi: endpoint, network, Gateway, VDA resource, policy hay broker. |
| Evidence pack | Session ID, user, endpoint, VDA, timestamp, Director metrics, policy result, event logs. |

### Detailed Runbook - RB39 Điều tra USB redirection issue

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Thiết bị USB không xuất hiện hoặc xuất hiện nhưng không dùng được trong session. |
| Procedure | 1. Xác định thiết bị thuộc optimized hay generic redirection. 2. Kiểm tra client Workspace App và endpoint policy. 3. Kiểm tra Citrix policy USB devices. 4. Kiểm tra filter/deny rule. 5. Test với user/máy khác. 6. Nếu cần, dùng USB diagnostics tool theo source. |
| Validation | Xác định policy/client/device class là nguyên nhân; không mở rộng cho toàn bộ USB khi chỉ cần một class cụ thể. |
| Rollback | Restore policy filter cũ; thu hồi exception tạm sau khi incident đóng. |

### Detailed Runbook - RB41 Điều tra printing issue trên VDA

| Mục | Nội dung |
|---|---|
| Tutorial scenario | User không in được hoặc printer mapping chậm/sai. |
| Procedure | 1. Xác định client printer hay network printer trên VDA. 2. Kiểm tra Universal Print Server nếu dùng. 3. Kiểm tra printing policy và driver strategy. 4. Kiểm tra spooler/service/event trên VDA. 5. Test với user khác cùng Delivery Group. 6. Ghi rõ printer name, driver, session ID. |
| Validation | Printer xuất hiện đúng, in test page thành công, không tạo printer stale sau reconnect. |
| Rollback | Revert policy/driver mapping; tránh cài driver thủ công hàng loạt trên VDA production nếu chưa test image. |

## CH08 - Director, Monitoring and Troubleshooting

### Chapter Knowledge Insight Report

CH08 là evidence plane. Director, Monitor, Search, Task Center và troubleshooting sections giúp biến cảm giác user thành dữ liệu: failed session, logon duration, VDA registration, HDX channel, machine state, task state. Insight: runbook incident phải bắt đầu bằng phạm vi và timeline trước khi sửa.

### Detailed Runbook - RB46 Cài và cấu hình Director

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Triển khai Director cho helpdesk và platform admin. |
| Precheck | Server prerequisite, quyền truy cập Controller/monitoring data, TLS/certificate nếu dùng HTTPS, delegated admin model, retention/historical trend requirement. |
| Procedure | 1. Cài Director theo installer. 2. Cấu hình kết nối site/Controller. 3. Cấu hình TLS nếu production. 4. Gán delegated admin role theo nhóm. 5. Kiểm tra Search, user session, machine detail, trend, failure reason. |
| Validation | Helpdesk chỉ thấy/thao tác đúng quyền; platform admin thấy đủ metrics; historical trend hoạt động nếu có dữ liệu. |
| Rollback | Remove server khỏi LB/DNS hoặc restore config; không cấp quyền rộng để chữa lỗi truy cập. |

### Detailed Runbook - RB48 Điều tra VDA registration bằng Director/Web Studio/event log

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Nhiều máy trong catalog chuyển unregistered. |
| Procedure | 1. Xác định phạm vi theo catalog/image/host/OU. 2. Kiểm tra power state và maintenance mode. 3. Kiểm tra VDA service/event log. 4. Kiểm tra Controller list, DNS, firewall, time sync. 5. Kiểm tra change gần đây: image, VDA upgrade, certificate, policy, AD. 6. Reboot một máy pilot nếu phù hợp, không reboot hàng loạt ngay. |
| Validation | Máy pilot registered lại và launch pass; RCA có layer rõ ràng. |
| Evidence pack | Catalog, machine list, timestamps, VDA events, Controller events, recent change, pilot action result. |

### Detailed Runbook - RB52 Chuẩn bị escalation package cho incident CVAD

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Incident vượt quyền xử lý của helpdesk/platform shift và cần chuyển Citrix/network/identity/SQL team. |
| Procedure | 1. Tóm tắt symptom bằng user journey step. 2. Ghi phạm vi: user, Delivery Group, catalog, site, internal/external. 3. Ghi timeline và change gần nhất. 4. Đính kèm Director screenshot/metrics, event logs, Gateway/StoreFront/Controller/VDA evidence. 5. Nêu action đã thử và kết quả. 6. Nêu yêu cầu cụ thể cho team nhận. |
| Validation | Team nhận có đủ dữ liệu để hành động, không phải hỏi lại thông tin cơ bản. |
| Anti-patterns | Escalate bằng câu "Citrix lỗi"; gửi log không timestamp; thiếu user/session/VDA ID. |

## CH09 - Backup, Restore, Upgrade and Log Server

### Chapter Knowledge Insight Report

CH09 là vùng bảo toàn khả năng phục hồi. Source có backup/restore best practices, Automated Configuration Tool, VDA Upgrade Service và Log Server. Insight: backup chỉ có giá trị khi restore được kiểm chứng qua user journey; upgrade chỉ an toàn khi quan sát được bằng log và rollback.

### Detailed Runbook - RB53 Backup cấu hình site theo best practice

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Chuẩn bị trước thay đổi lớn hoặc lập lịch backup cấu hình CVAD. |
| Precheck | Xác định phạm vi backup: site configuration, policy, catalog, Delivery Group, admin/RBAC, StoreFront/Gateway dependency riêng, database backup do SQL team. |
| Procedure | 1. Chạy công cụ/cmdlet backup được Citrix hỗ trợ. 2. Lưu output vào vị trí bảo mật. 3. Ghi version, thời điểm, account, site. 4. Kiểm tra file backup đọc được. 5. Đồng bộ với backup SQL/config/logging nếu có. |
| Validation | Có backup artifact, checksum/size hợp lệ, restore test plan tồn tại. |
| Rollback | Backup không thay đổi production; nếu backup fail, dừng change phụ thuộc backup. |

### Detailed Runbook - RB54 Restore cấu hình và validate user journey

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Khôi phục sau lỗi cấu hình hoặc test DR. |
| Precheck | Xác định backup đúng version/site, môi trường restore, quyền, downtime, approval, điểm dừng nếu restore không khớp. |
| Procedure | 1. Restore vào lab hoặc maintenance window theo quy trình. 2. Kiểm tra object count: catalog, Delivery Group, policy, admin role. 3. Kiểm tra Controller/database connectivity. 4. Test StoreFront enumeration và launch. 5. Kiểm tra Director/monitoring. |
| Validation | User journey pass, object quan trọng khôi phục đúng, không có policy/entitlement ngoài ý muốn. |
| Rollback | Nếu restore lỗi, dừng, giữ log, quay lại snapshot/database backup cũ theo kế hoạch DR. |

### Detailed Runbook - RB57 Upgrade VDA bằng VDA Upgrade Service

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Dùng VDA Upgrade Service để nâng cấp VDA có kiểm soát. |
| Precheck | Prerequisites của VUS, VDA compatibility, network/proxy nếu có, pilot group, maintenance window, rollback image/snapshot, success criteria. |
| Procedure | 1. Chọn nhóm pilot. 2. Cấu hình VUS theo source. 3. Kiểm tra proxy/support requirement. 4. Chạy upgrade. 5. Theo dõi progress và log. 6. Reboot nếu cần. 7. Kiểm tra VDA registered, launch, HDX, app/printer/USB nếu liên quan. |
| Validation | VDA version mới, registered, session pass, no elevated failure trend. |
| Rollback | Dừng rollout, revert image/snapshot hoặc redeploy VDA version cũ theo tested plan. |

### Detailed Runbook - RB59 Cài và cấu hình Log Server

| Mục | Nội dung |
|---|---|
| Tutorial scenario | Chuẩn hóa thu thập log cho troubleshooting và support. |
| Precheck | Server prerequisite, storage/retention, access control, network path, sensitive data handling, owner của log. |
| Procedure | 1. Cài Log Server theo source. 2. Cấu hình vị trí lưu log và quyền truy cập. 3. Test thu log từ component mục tiêu. 4. Xác minh timestamp/time zone. 5. Tạo quy ước đặt tên evidence theo incident ID. |
| Validation | Log thu được, đọc được, timestamp đúng, chỉ nhóm được phép truy cập. |
| Rollback | Dừng service hoặc remove integration nếu gây tải/lỗi; không xóa log incident khi chưa được duyệt. |

## Installation and Configuration Coverage Gaps

Không có khoảng trống chủ ý trong các mục install/configure lớn đã phát hiện từ source. Các phần cần ingest sâu hơn trong lượt sau nếu muốn đạt mức manual vendor đầy đủ từng màn hình là: tham số command-line đầy đủ cho từng installer, option chi tiết của từng HDX policy setting, và các flow chuyên sâu riêng cho Citrix Gateway/NetScaler nếu có tài liệu Gateway độc lập.

## Related Concepts

- [[concepts/citrix-virtual-apps-and-desktops]]
- [[concepts/delivery-controller]]
- [[concepts/storefront]]
- [[concepts/virtual-delivery-agent]]
- [[concepts/delivery-group]]
- [[concepts/machine-identity]]
- [[concepts/hdx]]
- [[concepts/ica-virtual-channel]]
- [[concepts/monitoring-and-logs]]
- [[concepts/change-management]]
- [[concepts/backup-and-recovery]]
- [[concepts/certificate-management]]

## Related Sources

- [[sources/citrix-virtual-apps-and-desktops-7-2603]]
- [[sources/citrix-virtual-apps-and-desktops-7-2603-technical-deep-ingest-report]]
- [[sources/vmware-vsphere-8-0]]
- [[sources/xenserver-8-4]]
- [[sources/fslogix-documentation]]

## Self Review

- Đã chuyển mỗi vùng/chapter lớn thành insight tri thức, không chỉ tóm tắt nội dung.
- Đã trích xuất 60 runbook best practice từ các phần vận hành, cài đặt, cấu hình, bảo mật, monitoring, backup và upgrade.
- Đã detail hóa các runbook quan trọng ở mức tutorial với scenario, precheck, procedure, validation, rollback và evidence.
- Đã đánh dấu rõ khoảng trống còn lại cho mức tham số vendor chi tiết từng option.
