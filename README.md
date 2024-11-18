# Hướng dẫn Xây Dựng và Triển Khai Docker

## 1. Xây dựng Hình Ảnh Docker

Để xây dựng các hình ảnh Docker cho các phần của ứng dụng, sử dụng các lệnh sau trong terminal hoặc CMD tại thư mục chứa Dockerfile:

```bash
# Xây dựng hình ảnh cho phần quản trị (admin)
docker build -t admin ./admin/

# Xây dựng hình ảnh cho phần người dùng (user)
docker build -t user ./user/

# Xây dựng hình ảnh cho backend
docker build -t be ./backend/
```

## 2. Chạy Docker Compose

Sau khi đã xây dựng xong các hình ảnh, bạn có thể sử dụng Docker Compose để khởi động và quản lý các container. Bạn cần tạo một file `docker-compose.yml` để định nghĩa cách các container tương tác với nhau.

```bash
# Chạy docker-compose.yml
docker compose up -d
```

