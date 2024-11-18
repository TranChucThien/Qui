
# Hướng Dẫn Xây Dựng và Triển Khai Docker

## 1. Xây Dựng Hình Ảnh Docker

Để xây dựng các hình ảnh Docker cho từng phần của ứng dụng, sử dụng các lệnh sau trong terminal hoặc CMD tại thư mục root của dự án:

```bash
# Xây dựng hình ảnh cho phần quản trị (admin)
docker build -t admin ./admin/

# Xây dựng hình ảnh cho phần người dùng (user)
docker build -t user ./user/

# Xây dựng hình ảnh cho backend
docker build -t be ./backend/
```

### Giải Thích:

- **docker build**: Lệnh này được sử dụng để xây dựng một hình ảnh Docker từ một Dockerfile và các nguồn mã trong thư mục hiện tại.
  
- **-t**: Tùy chọn này gán một tên (tag) cho hình ảnh Docker được xây dựng. Điều này giúp bạn dễ dàng quản lý và tham chiếu đến hình ảnh sau này.
  
- **./admin/**, **./user/**, **./backend/**: Đây là các đường dẫn tới các thư mục chứa Dockerfile và mã nguồn tương ứng cho từng phần của ứng dụng.

---

## 2. Quản Lý Containers với Docker Compose

Docker Compose là một công cụ mạnh mẽ giúp bạn định nghĩa và quản lý các containers Docker cho ứng dụng đa dịch vụ. Sau khi cấu hình xong tệp `docker-compose.yml`, bạn có thể sử dụng các lệnh sau để quản lý các containers.

### 2.1. Build và Chạy Tất Cả Services

```bash
docker-compose up --build
```

#### Giải Thích:

- **docker-compose up**: Lệnh này khởi động tất cả các dịch vụ (services) được định nghĩa trong tệp `docker-compose.yml`. Nếu các hình ảnh Docker chưa được xây dựng, lệnh này sẽ tự động xây dựng chúng trước khi khởi động.
  
- **--build**: Tùy chọn này buộc Docker Compose phải xây dựng lại các hình ảnh Docker ngay cả khi chúng đã tồn tại. Điều này hữu ích khi bạn đã thay đổi Dockerfile hoặc mã nguồn và muốn cập nhật hình ảnh mới.

#### Khi Nào Sử Dụng:
- Khi bạn lần đầu thiết lập dự án hoặc sau khi đã thay đổi Dockerfile hoặc mã nguồn mà bạn muốn cập nhật các hình ảnh Docker.

---

### 2.2. Chạy Containers Không Build Lại

```bash
docker-compose up -d
```

#### Giải Thích:

- **docker-compose up**: Tương tự như trên, lệnh này khởi động các dịch vụ được định nghĩa trong `docker-compose.yml`.
  
- **-d**: Tùy chọn này chạy các containers trong chế độ **detached** (chạy ngầm). Điều này có nghĩa là các dịch vụ sẽ chạy ở nền mà không chiếm dụng terminal của bạn.

#### Khi Nào Sử Dụng:
- Khi bạn đã xây dựng xong các hình ảnh Docker và chỉ cần khởi động lại các dịch vụ mà không cần xây dựng lại hình ảnh.

---

### 2.3. Dừng và Xóa Tất Cả Services

```bash
docker-compose down
```

#### Giải Thích:

- **docker-compose down**: Lệnh này dừng tất cả các containers đang chạy và xóa chúng cùng với các mạng (networks) và volumes được tạo bởi `docker-compose up`. Điều này giúp giải phóng tài nguyên hệ thống và đảm bảo rằng lần khởi động tiếp theo sẽ bắt đầu từ trạng thái sạch sẽ.

#### Khi Nào Sử Dụng:
- Khi bạn muốn tạm dừng toàn bộ ứng dụng và giải phóng tài nguyên hệ thống.
- Khi bạn cần xóa các tài nguyên đã tạo bởi Docker Compose để thực hiện các thay đổi cấu hình hoặc cập nhật ứng dụng.

---

## 3. Các Lệnh Docker Compose Khác (Tùy Chọn)

Dưới đây là một số lệnh Docker Compose hữu ích khác mà bạn có thể sử dụng để quản lý ứng dụng Docker của mình:

### 3.1. Xem Trạng Thái Các Services

```bash
docker-compose ps
```

- **Mô tả**: Hiển thị trạng thái hiện tại của tất cả các dịch vụ được định nghĩa trong `docker-compose.yml`.

### 3.2. Xem Logs Của Các Services

```bash
docker-compose logs -f
```

- **Mô tả**: Hiển thị logs của tất cả các dịch vụ. Tùy chọn `-f` giúp theo dõi logs theo thời gian thực.

### 3.3. Dừng Tạm Thời Các Services

```bash
docker-compose stop
```

- **Mô tả**: Dừng tạm thời các containers mà không xóa chúng. Bạn có thể khởi động lại chúng bằng lệnh `docker-compose start`.

### 3.4. Khởi Động Lại Các Services

```bash
docker-compose restart
```

- **Mô tả**: Dừng và sau đó khởi động lại tất cả các dịch vụ. Điều này hữu ích khi bạn đã thay đổi cấu hình và cần áp dụng các thay đổi mới.

---

## 4. Một Số Lưu Ý Khi Sử Dụng Docker và Docker Compose

- **Dockerfile**: Đảm bảo rằng mỗi dịch vụ có một Dockerfile chính xác để xây dựng hình ảnh Docker. Kiểm tra kỹ các lệnh trong Dockerfile để tránh lỗi khi xây dựng hình ảnh.
  
- **docker-compose.yml**: Đảm bảo rằng tệp cấu hình này được định nghĩa chính xác với tất cả các dịch vụ, mạng, và volumes cần thiết. Sử dụng YAML Validator để kiểm tra cú pháp.
  
- **Quản Lý Tài Nguyên**: Đảm bảo rằng hệ thống của bạn có đủ tài nguyên (CPU, RAM, ổ cứng) để chạy tất cả các containers mà bạn đã định nghĩa.
  
- **Bảo Mật**: Luôn cập nhật các hình ảnh Docker lên phiên bản mới nhất để đảm bảo rằng bạn không bị lỗ hổng bảo mật. Sử dụng các hình ảnh chính thức từ Docker Hub khi có thể.

---

## Kết Luận

Docker và Docker Compose là những công cụ mạnh mẽ giúp bạn xây dựng, triển khai và quản lý các ứng dụng đa dịch vụ một cách hiệu quả. Bằng cách hiểu rõ các lệnh cơ bản và cách sử dụng chúng, bạn có thể tối ưu hóa quy trình phát triển và triển khai ứng dụng của mình.


