🔧 Bước 1: Cài Docker & Docker Compose
sudo apt update && sudo apt upgrade -y
sudo apt install docker.io docker-compose -y
sudo systemctl enable docker

Bước 2: Tạo thư mục cho n8n và file cấu hình
mkdir -p ~/n8n && cd ~/n8n
nano docker-compose.yml
