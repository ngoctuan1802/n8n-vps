🔧 Bước 1: Cài Docker & Docker Compose
sudo apt update && sudo apt upgrade -y
sudo apt install docker.io docker-compose -y
sudo systemctl enable docker

Bước 2: Tạo thư mục cho n8n và file cấu hình
mkdir -p ~/n8n && cd ~/n8n
nano docker-compose.yml

## Cài Nginx & Certbot

apt install nginx certbot python3-certbot-nginx -y


Tạo cấu hình Nginx cho n8n
vim /etc/nginx/sites-available/n8n

server {
    listen 80;
    server_name n8n.techconnect.io.vn;

    location / {
        proxy_pass http://localhost:5678;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

Kích hoạt config
ln -s /etc/nginx/sites-available/n8n /etc/nginx/sites-enabled/
nginx -t && systemctl reload nginx

Cấp SSL miễn phí bằng Let's Encrypt
certbot --nginx -d n8n.techconnect.io.vn
