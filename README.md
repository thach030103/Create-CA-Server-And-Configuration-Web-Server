## Create-CA-Server-And-Configuration-Web-Server
<h4>1. Create Certificate Authorities (CA) Server trên PC1</h4>
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
<h4>Bước 3: Cài đặt và cấu hình Active Directory Certificate Services (AD CS)</h4>
<ul>
  <li>Mở Server Manager -> Add roles and features.</li>
  <li>Chọn Active Directory Certificate Services -> Next.</li>
  <li>Chọn Certification Authority và Certification Authority Web Enrollment -> Next.</li>
  <li>Nhấn Next nhiều lần -> Install
  <li>Sau khi cài đặt xong, nhấn Configure Active Directory Certificate Services on the...</li>
  <li>Chọn Root CA -> Next.</li>
  <li>Chọn Create a new private key -> Next.</li>
  <li>Chọn SHA256 làm thuật toán mã hóa ->Next.</li>
  <li>Nhấn Next nhiều lần -> Nhấn Configure để hoàn tất.</li>
</ul>
<h4>Bước 4: Cấu hình DNS cho máy CA Server</h4>
<ul>
  <li>Mở DNS Manager > Nhấn chuột phải vào Forward Lookup Zones > Chọn New Zone.</li>
  <li>Chọn Primary Zone > Nhập tên zone là cntt.vn.</li>
  <li>Hoàn tất cấu hình và kiểm tra DNS.</li>
</ul>
<h4>2. Configuration Web Server trên PC2</h4>
<h4>Bước 1: Cấu hình IP</h4>
<p>Đặt IP tĩnh cho Web Server:</p>
<ul>
  <li>IP: 192.168.12.200</li>
  <li>Subnet Mask: 255.255.255.0</li>
  <li>Default Gateway: 192.168.12.1</li>
</ul>
<h4>Bước 2: Cài đặt dịch vụ Web Server (IIS)</h4>
<ul>
  <li>Mở Server Manager -> Add roles and features.</li>
  <li>Chọn Web Server (IIS) -> Next nhiều lần -> Install.</li>
</ul>
<h4>Bước 3: Tạo Certificate Request trên IIS</h4>
<ul>
<li>Mở IIS Manager, chọn Server Certificates.</li>
<li>Nhấn Create Certificate Request và điền thông tin:</li>
<ul>
<li>Common Name:CNTT-VN</li>
<li>Organization: CNTTVN</li>
<li>Organization unit: Thu Duc</li>
<li>City/locality: HCM</li>
<li>State/province: HCM</li>
<li>Country/region: VN</li>
</ul>
<li>Lưu file CSR (Certificate Signing Request) thành ca.txt.</li>
</ul>
