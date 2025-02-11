## Create-CA-Server-And-Configuration-Web-Server
<h4>1. Create Certificate Authorities (CA) Server</h4>
<h4>Bước 1: Cấu hình IP</h4>
<p>Đặt IP tĩnh cho CA Server:</p>
<ul>
  <li>IP: 192.168.12.254</li>
  <li>Subnet Mask: 255.255.255.0</li>
  <li>Default Gateway: 192.168.12.1</li>
</ul>
<h4>Bước 2: Nâng cấp lên Domain Controller</h4>
<ul>
  <li>Mở Server Manager -> Add roles and features.</li>
  <li>Chọn Active Directory Domain Services (AD DS) và DNS Server -> Nhấn Next đến khi hoàn tất > Install.</li>
  <li>Sau khi cài đặt xong, chọn Promote this server to a domain controller.</li>
  <li>Chọn Add a new forest, nhập tên domain: XYZ.COM </li>
  <li>Nhập Password cho Directory Services Restore Mode (DSRM).</li>
  <li>Nhấn Next nhiều lần -> Install
</ul>
<h4>2. Configuration Web Server</h4>
