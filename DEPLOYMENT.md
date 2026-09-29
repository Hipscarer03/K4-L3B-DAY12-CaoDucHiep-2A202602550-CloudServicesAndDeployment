# Thông Tin Deploy — Checkpoint 5

> Điền file này sau khi deploy xong. `pytest tests/test_cp5.py` đọc file này
> để tìm địa chỉ service của bạn và gọi thử.
>
> **Chỉ ghi TÊN biến môi trường, tuyệt đối không dán giá trị API key vào đây.**
> Repo này công khai — dán khóa vào là mất khóa.

## Thông Tin Học Viên

| Mục | Nội dung |
|-----|----------|
| Họ và tên | Cao Đức Hiệp |
| Mã học viên | 2A202602550 |
| Repo | https://github.com/Hipscarer03/K4-L3B-DAY12-CaoDucHiep-2A202602550-CloudServicesAndDeployment |

## Service

| Mục | Nội dung |
|-----|----------|
| Public URL | https://day12-agent-m6qx.onrender.com |
| Platform | Render |
| Ngày deploy | 2026-09-29 |

## Biến Môi Trường Đã Set Trên Cloud

Ghi tên biến và **nguồn giá trị**, không ghi giá trị:

| Biến | Đã set | Ghi chú |
|------|--------|---------|
| `PORT` | ✅ | platform tự gán |
| `AGENT_API_KEY` | ✅ | đặt trong dashboard, không nằm trong repo |
| `REDIS_URL` | ✅ | Render Key Value (day12-redis) |
| `RATE_LIMIT_PER_MINUTE` | ✅ | 10 |
| `MONTHLY_BUDGET_USD` | ✅ | 10.0 |
| `LOG_LEVEL` | ✅ | INFO |

## Lệnh Kiểm Tra

Thay `<URL>` bằng Public URL ở trên:

```bash
# 1. Liveness — mong đợi 200 {"status":"ok"}
curl -i https://day12-agent-m6qx.onrender.com/health

# 2. Readiness — mong đợi 200 {"status":"ready"} (đã nối được Redis)
curl -i https://day12-agent-m6qx.onrender.com/ready

# 3. Không có API key — mong đợi 401
curl -i -X POST https://day12-agent-m6qx.onrender.com/ask \
  -H "Content-Type: application/json" \
  -d '{"question":"Hello"}'
```

## Kết Quả Chạy Thật

Dán output của các lệnh trên vào đây:

```
$ curl -i https://day12-agent-m6qx.onrender.com/health
HTTP/2 200
content-type: application/json
{"status":"ok","service":"day12-agent","version":"1.0.0"}

$ curl -i https://day12-agent-m6qx.onrender.com/ready
HTTP/2 200
content-type: application/json
{"status":"ready","redis":true}

$ curl -i -X POST https://day12-agent-m6qx.onrender.com/ask -H "Content-Type: application/json" -d '{"question":"Hello"}'
HTTP/2 401
content-type: application/json
{"detail":"invalid or missing API key"}
```

## Ảnh Chụp Màn Hình

Đặt ảnh trong thư mục `screenshots/`:

- `screenshots/dashboard.png` — trang quản lý service trên platform
- `screenshots/health.png` — kết quả gọi `/health` từ trình duyệt hoặc curl