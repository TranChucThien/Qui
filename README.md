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

## 2. Quản Lý Containers với Docker Compose

Sau khi cấu hình xong tệp `docker-compose.yml`, bạn có thể sử dụng các lệnh sau để quản lý các containers.

### 2.1. Build và Chạy Tất Cả Services

```bash
docker-compose up --build
```
### 2.2. Chạy Containers Không Build Lại

```bash
docker-compose up -d
```
### 2.3. Dừng và Xóa Tất Cả Services

```bash
docker-compose down
```
