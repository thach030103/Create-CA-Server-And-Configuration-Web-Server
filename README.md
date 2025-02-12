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
<h4>Bước 4: Ký chứng chỉ với CA Server</h4>
<ul>
  <li>Truy cập CA Server qua URL: http://192.168.12.254/certsrv.</li>
  <li>Chọn Request a certificate -> advanced certificate request.</li>
  <li>Chọn Submit a certificate request by using a base-64-encoded CMC or PKCS #10 file...</li>
  <li>Mở file ca.txt, copy nội dung và dán vào Base-64-encoded certificate request -> Submit.</li>
  <li>Chuyển sang CA Server, vào Pending Requests, nhấn chuột phải vào yêu cầu -> All Tasks -> Issue.</li>
  <li>Trở lại Web Server, truy cập CA Server qua URL: http://192.168.12.254/certsrv.</li>
  <li>Chọn View the status of a pending certificate request -> Saved-Request Certificate … -> Download 2 chứng chi đã cấp</li>
</ul>
<h4>Bước 5: Import chứng chỉ trên Web Server</h4>
<ul>
  <li>Mở Run -> gõ mmc -> Enter.</li>
  <li>Vào File -> Add/Remove Snap-in .. -> Chọn Certificates -> My user account -> Finish</li>
  <li>Chuột phải vào Trusted Root Certificate Authorities -> Import.</li>
  <li>Import file chứng chỉ đã tải về từ CA Server.</li>
</ul>
<h4>Bước 6: Hoàn tất cấu hình chứng chỉ trên IIS</h4>
<ul>
  <li>Mở lại IIS Manager, nhấn Complete Certificate Request.
  <li>Chọn file .cer, đặt Friendly name là CNTT-VN.
  <li>Chuột phải vào Default Web Site -> Edit Bindings.
  <li>Thêm binding:
    <ul>
      <li>Type: https</li>
      <li>Port: 443</li>
      <li>Host Name: www.cntt.vn</li>
      <li>SSL Certificate: CNTT-VN  </li>
    </ul>
  <li>Nhấn OK và đóng cửa sổ.</li>
</ul>
<h4>Bước 7: Bật SSL cho Website</h4>
<ul>
  <li>Chọn Default Web Site -> SSL Settings.</li>
  <li>Tick chọn Require SSL -> Nhấn Apply.</li>
</ul>
<h4>3. Kiểm tra kết quả</h4>
<ul>
  <li>Truy cập website: https://www.cntt.vn.</li>
  <li>Nếu có cảnh báo, nhấn Continue to this website (not recommended).</li>
  <li>Nhấn vào Certificate error để xem thông tin chứng chỉ.</li>
</ul>
