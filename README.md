## Trước khi che:
[ERROR] 2026-10-01 23:12:04
SyncFarmerJob failed for farmer_id=1023
  name=Trần Văn Hùng
  email=tranvanhung.htx@gmail.com
  phone=0987654321
  client_ip=113.160.22.15
DB: mysql://admin:Nongsan@2026@db.local/htx
API_KEY=sk-live-9aF3kLm2QpX7
TypeError: Cannot read properties of
  undefined (reading 'harvestDate')
  at syncFarmer (farmer.job.js:42)
## Sau khi che:
[ERROR] 2026-10-01 23:12:04
SyncFarmerJob failed for farmer_id=1023
  name=User A 
  email=user@test.com
  phone=0000000000
  client_ip=x.x.x.x
DB: mysql://<DB_USERNAME>:<DB_PASSWORD>@<DB_HOST>/<DB_NAME>
API_KEY=<API_KEY>
TypeError: Cannot read properties of
  undefined (reading 'harvestDate')
  at syncFarmer (farmer.job.js:42)
## Lý do:
name	User A	Bảo vệ họ tên, thông tin nhận dạng cá nhân.
email	user@test.com	Bảo vệ địa chỉ email cá nhân.
phone	0000000000	Bảo vệ số điện thoại cá nhân.
client_ip	x.x.x.x	Hạn chế tiết lộ thông tin mạng có thể hỗ trợ xác định thiết bị hoặc vị trí gần đúng.
DB username	<DB_USERNAME>	Che tên tài khoản truy cập cơ sở dữ liệu.
DB password	<DB_PASSWORD>	Ngăn lộ mật khẩu và truy cập trái phép vào cơ sở dữ liệu.
DB host	<DB_HOST>	Che thông tin máy chủ cơ sở dữ liệu và hạ tầng nội bộ.
DB name	<DB_NAME>	Hạn chế tiết lộ tên cơ sở dữ liệu và cấu trúc hệ thống.
API_KEY	<API_KEY>	Bảo vệ khóa xác thực API, tránh bị lợi dụng để truy cập dịch vụ.