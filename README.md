# About to docker
<br>

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Container](https://img.shields.io/badge/Container-Technology-0db7ed?style=for-the-badge&logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![DockerHub](https://img.shields.io/badge/Docker_Hub-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Compose](https://img.shields.io/badge/Docker-Compose-FF9900?style=for-the-badge&logo=docker&logoColor=white)

> 💡 **Docker = Apni app ko ek box me pack karo — phir kisi bhi computer pe same kaam karega. "Works on my machine" problem khatam!**

</div>

---

## 📌 Table of Contents

| # | Topic |
|---|-------|
| 01 | [🤔 Docker Kya Hai?](#-docker-kya-hai) |
| 02 | [🏗️ Docker Architecture](#️-docker-architecture) |
| 03 | [📦 Images vs Containers](#-images-vs-containers) |
| 04 | [⚙️ Installation](#️-installation) |
| 05 | [🔧 Docker Basic Commands](#-docker-basic-commands) |
| 06 | [📝 Dockerfile](#-dockerfile) |
| 07 | [🌐 Docker Networking](#-docker-networking) |
| 08 | [💾 Docker Volumes](#-docker-volumes) |
| 09 | [🐙 Docker Compose](#-docker-compose) |
| 10 | [📤 Docker Hub](#-docker-hub) |
| 11 | [💡 Pro Tips & Tricks](#-pro-tips--tricks) |
| 12 | [❌ Common Errors & Fixes](#-common-errors--fixes) |
| 13 | [📋 Cheat Sheet](#-cheat-sheet) |

---

## 🤔 Docker Kya Hai?

```
╔══════════════════════════════════════════════════════════════╗
║                DOCKER SIMPLE SAMAJHO                        ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║   📦 REAL LIFE:              🐳 DOCKER:                      ║
║                                                              ║
║   Shipping Container         Docker Container                ║
║   Kuch bhi andar pack karo   App + Dependencies pack karo   ║
║   Kisi bhi ship pe rakho     Kisi bhi server pe chalao      ║
║   Same result everywhere!    Same result everywhere! ✅      ║
║                                                              ║
║   ══════════════════════════════════════════════════════    ║
║                                                              ║
║   😤 PROBLEM (Before Docker):                                ║
║   "Mere computer pe kaam karta hai                           ║
║    par server pe nahi!" 😤                                   ║
║                                                              ║
║   😊 SOLUTION (After Docker):                                ║
║   App + Libraries + Config = Container                       ║
║   Har jagah same environment! ✅                             ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
```

**Docker Kyun Use Karte Hain?**

| 🎯 Feature | 💬 Detail |
|-----------|-----------|
| 🚀 **Portability** | Laptop se server pe same run karega |
| ⚡ **Speed** | VM se 10x fast start hota hai |
| 📦 **Isolation** | Har app apna environment |
| 🔄 **Consistency** | Dev = Staging = Production |
| 💰 **Cost** | Ek server pe bahut saare containers |
| 🛠️ **DevOps** | CI/CD me easy deploy |

---

## 🏗️ Docker Architecture

```
╔══════════════════════════════════════════════════════════════════╗
║                  DOCKER ARCHITECTURE                            ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║   👤 USER (tum)                                                  ║
║       │  docker run / build / pull                               ║
║       ▼                                                          ║
║   ┌──────────────────────────────────────────────────────────┐  ║
║   │              🐳 DOCKER CLIENT (CLI)                      │  ║
║   │              docker command type karte hain              │  ║
║   └──────────────────────────┬───────────────────────────────┘  ║
║                              │  REST API                        ║
║   ┌──────────────────────────▼───────────────────────────────┐  ║
║   │              🔧 DOCKER DAEMON (dockerd)                  │  ║
║   │              Background me chalta hai                    │  ║
║   │              Images, Containers manage karta hai         │  ║
║   └──────┬───────────────────────────────┬────────────────────┘  ║
║          │                               │                       ║
║   ┌──────▼──────┐                ┌───────▼──────┐               ║
║   │  📦 IMAGE   │                │ 🏃 CONTAINER │               ║
║   │  Template   │                │  Running     │               ║
║   │  (Read Only)│                │  Instance    │               ║
║   └─────────────┘                └──────────────┘               ║
║          │                                                       ║
║   ┌──────▼──────────────────────────────────────────────────┐   ║
║   │              🌐 DOCKER REGISTRY                         │   ║
║   │              Docker Hub (Public)                        │   ║
║   │              ECR / ACR (Private)                        │   ║
║   └─────────────────────────────────────────────────────────┘   ║
╚══════════════════════════════════════════════════════════════════╝
```

---

## 📦 Images vs Containers

```
╔══════════════════════════════════════════════════════════════════╗
║                IMAGE vs CONTAINER                               ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║   📦 IMAGE                       🏃 CONTAINER                   ║
║   ┌──────────────────────┐       ┌──────────────────────┐       ║
║   │  Blueprint / Template│       │   Running Instance   │       ║
║   │  Read-Only           │  ──►  │   Read-Write         │       ║
║   │  Like: .exe file     │       │   Like: Running app  │       ║
║   │                      │       │                      │       ║
║   │  ubuntu:22.04        │       │  container_id: abc   │       ║
║   │  nginx:latest        │       │  Status: Running     │       ║
║   │  node:18             │       │  Port: 80:80         │       ║
║   └──────────────────────┘       └──────────────────────┘       ║
║                                                                  ║
║   LAYERS CONCEPT:                                                ║
║   ┌────────────────────────────────────────────────────────┐    ║
║   │  Layer 4: Your App Code          ← tumhara code        │    ║
║   │  Layer 3: npm install            ← dependencies        │    ║
║   │  Layer 2: node:18 base           ← base image          │    ║
║   │  Layer 1: Ubuntu OS              ← OS layer            │    ║
║   └────────────────────────────────────────────────────────┘    ║
║   ✅ Layers cache hote hain — fast rebuild!                      ║
╚══════════════════════════════════════════════════════════════════╝
```

---

## ⚙️ Installation

### 🐧 Linux (Ubuntu)

```bash
# ── METHOD 1: Official Script (Recommended) ──────────
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Sudo ke bina Docker use karo
sudo usermod -aG docker $USER
newgrp docker

# ── METHOD 2: Step by Step ───────────────────────────
sudo apt update
sudo apt install -y ca-certificates curl gnupg

# Docker GPG key
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
    sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Repository add karo
echo "deb [arch=$(dpkg --print-architecture) \
    signed-by=/etc/apt/keyrings/docker.gpg] \
    https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list

# Install
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io \
    docker-buildx-plugin docker-compose-plugin

# ✅ Version check karo
docker --version
docker compose version
```

### 🍎 macOS & 🪟 Windows

```
🍎 macOS:
  1. docs.docker.com/desktop/mac pe jao
  2. Docker Desktop download karo
  3. .dmg install karo
  4. docker --version ✅

🪟 Windows:
  1. docs.docker.com/desktop/windows pe jao
  2. Docker Desktop download karo
  3. .exe install karo (WSL2 enable karo)
  4. docker --version ✅
```

---

## 🔧 Docker Basic Commands

```bash
# ════════════════════════════════════════════
# 🖼️  IMAGE COMMANDS
# ════════════════════════════════════════════

# Image pull karo (Docker Hub se)
docker pull ubuntu:22.04
docker pull nginx:latest
docker pull node:18-alpine

# Images list dekho
docker images
docker image ls

# Image delete karo
docker rmi nginx:latest
docker image rm ubuntu:22.04

# Dangling images clean karo
docker image prune

# Image details dekho
docker inspect nginx:latest


# ════════════════════════════════════════════
# 🏃 CONTAINER COMMANDS
# ════════════════════════════════════════════

# Container run karo
docker run nginx                           # Basic run
docker run -d nginx                        # Background (detached)
docker run -d -p 80:80 nginx              # Port mapping
docker run -d -p 80:80 --name webserver nginx  # Custom naam

# Running containers dekho
docker ps                                  # Running only
docker ps -a                               # Saare containers

# Container start / stop / restart
docker start container_id
docker stop container_id
docker restart container_id

# Container delete karo
docker rm container_id
docker rm -f container_id                  # Force delete (running bhi)

# Saare stopped containers delete karo
docker container prune

# Container ke andar jao (bash)
docker exec -it container_id bash
docker exec -it webserver sh               # Alpine ke liye

# Container logs dekho
docker logs container_id
docker logs -f container_id               # Live logs (follow)
docker logs --tail 50 container_id        # Last 50 lines

# Container ki info dekho
docker inspect container_id

# Container stats (CPU, Memory)
docker stats
docker stats container_id
```

---

## 📝 Dockerfile

```
╔══════════════════════════════════════════════════════════════╗
║              DOCKERFILE ANATOMY                             ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║   FROM    → Base image choose karo                          ║
║   WORKDIR → Working directory set karo                      ║
║   COPY    → Files container me copy karo                    ║
║   RUN     → Commands chalao (build time)                    ║
║   ENV     → Environment variables set karo                  ║
║   EXPOSE  → Port define karo                                ║
║   CMD     → Container start hone pe kya chalega            ║
║   ENTRYPOINT → Container ka main process                    ║
╚══════════════════════════════════════════════════════════════╝
```

### 🟢 Node.js App Dockerfile

```dockerfile
# Base image
FROM node:18-alpine

# Working directory
WORKDIR /app

# Dependencies pehle copy karo (cache ke liye)
COPY package*.json ./

# Dependencies install karo
RUN npm install --production

# Baaki code copy karo
COPY . .

# Port expose karo
EXPOSE 3000

# Environment variable
ENV NODE_ENV=production

# App start karo
CMD ["node", "server.js"]
```

### 🐍 Python App Dockerfile

```dockerfile
FROM python:3.11-slim

WORKDIR /app

# Requirements copy & install
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

ENV FLASK_ENV=production

CMD ["python", "app.py"]
```

### 🌐 Nginx Static Website Dockerfile

```dockerfile
# Build stage
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Production stage
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

```bash
# 🔨 Image build karo
docker build -t myapp:latest .
docker build -t myapp:v1.0 .
docker build -t myapp:latest -f Dockerfile.prod .

# 🔨 Build with no cache
docker build --no-cache -t myapp:latest .

# 🏃 Container run karo
docker run -d -p 3000:3000 --name my-node-app myapp:latest

# ✅ Test karo
curl http://localhost:3000
```

---

## 🌐 Docker Networking

```
╔══════════════════════════════════════════════════════════════════╗
║                DOCKER NETWORK TYPES                             ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║  🔵 BRIDGE (Default)                                             ║
║  ┌──────────────────────────────────────────────────────────┐   ║
║  │  Containers ek dusre se baat kar sakte hain              │   ║
║  │  docker0 bridge se connect hote hain                     │   ║
║  │  Use: Single host pe multiple containers                 │   ║
║  └──────────────────────────────────────────────────────────┘   ║
║                                                                  ║
║  🟢 HOST                                                         ║
║  ┌──────────────────────────────────────────────────────────┐   ║
║  │  Container host ka network directly use karta hai        │   ║
║  │  Port mapping ki zarurat nahi                            │   ║
║  │  Use: High performance networking                        │   ║
║  └──────────────────────────────────────────────────────────┘   ║
║                                                                  ║
║  🔴 NONE                                                         ║
║  ┌──────────────────────────────────────────────────────────┐   ║
║  │  No network — completely isolated                        │   ║
║  │  Use: Security-sensitive containers                      │   ║
║  └──────────────────────────────────────────────────────────┘   ║
║                                                                  ║
║  🟡 CUSTOM BRIDGE (Recommended)                                  ║
║  ┌──────────────────────────────────────────────────────────┐   ║
║  │  Apna network banao — naam se containers connect karo    │   ║
║  │  Use: Microservices, Docker Compose                      │   ║
║  └──────────────────────────────────────────────────────────┘   ║
╚══════════════════════════════════════════════════════════════════╝
```

```bash
# 🌐 Custom Network banao
docker network create myapp-network

# Networks list karo
docker network ls

# Container ko network se connect karke run karo
docker run -d \
    --name webapp \
    --network myapp-network \
    -p 3000:3000 \
    myapp:latest

docker run -d \
    --name database \
    --network myapp-network \
    -e MYSQL_ROOT_PASSWORD=secret \
    mysql:8.0

# Ab webapp container "database" naam se db access kar sakta hai!
# mysql -h database -u root -p

# Network inspect karo
docker network inspect myapp-network

# Network delete karo
docker network rm myapp-network
```

---

## 💾 Docker Volumes

```
╔══════════════════════════════════════════════════════════════╗
║              DOCKER VOLUMES KYA HAIN?                       ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║   PROBLEM:                                                   ║
║   Container delete karo → Sab data lost! ❌                 ║
║                                                              ║
║   SOLUTION — VOLUMES:                                        ║
║   ┌──────────────────────────────────────────────────────┐  ║
║   │  🖥️  HOST MACHINE         🐳 CONTAINER               │  ║
║   │                                                      │  ║
║   │  /home/data/db  ◄────────► /var/lib/mysql            │  ║
║   │  (Safe rehta)              (Container ka path)       │  ║
║   │                                                      │  ║
║   │  Container delete karo → Data host pe safe! ✅       │  ║
║   └──────────────────────────────────────────────────────┘  ║
║                                                              ║
║   VOLUME TYPES:                                              ║
║   📁 Named Volume    → docker manage karta hai              ║
║   📂 Bind Mount      → Tumhara local folder mount karo      ║
║   💾 tmpfs Mount     → RAM me temporary (fast)              ║
╚══════════════════════════════════════════════════════════════╝
```

```bash
# 💾 Named Volume banao
docker volume create mydata

# Volumes list karo
docker volume ls

# Volume ke saath container run karo
docker run -d \
    --name mysql-db \
    -v mydata:/var/lib/mysql \
    -e MYSQL_ROOT_PASSWORD=secret \
    mysql:8.0

# Bind Mount (local folder → container)
docker run -d \
    --name webapp \
    -v $(pwd)/website:/usr/share/nginx/html \
    -p 80:80 \
    nginx:latest

# Development ke liye (live code reload)
docker run -d \
    --name dev-app \
    -v $(pwd):/app \
    -w /app \
    -p 3000:3000 \
    node:18-alpine \
    node server.js

# Volume inspect karo
docker volume inspect mydata

# Volume delete karo
docker volume rm mydata

# Unused volumes clean karo
docker volume prune
```

---

## 🐙 Docker Compose

```
╔══════════════════════════════════════════════════════════════╗
║              DOCKER COMPOSE KYA HAI?                        ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║   Multiple containers ek saath manage karo!                  ║
║                                                              ║
║   BINA COMPOSE:                                              ║
║   docker run -d --name db ...  (manually)                   ║
║   docker run -d --name app ... (manually)                   ║
║   docker run -d --name nginx ...(manually)                  ║
║   😩 Tedious!                                                ║
║                                                              ║
║   COMPOSE KE SAATH:                                          ║
║   docker compose up -d   ← Sab ek command me! ✅            ║
╚══════════════════════════════════════════════════════════════╝
```

### 📝 docker-compose.yml — Full Stack App

```yaml
version: '3.8'

services:

  # 🌐 Frontend (Nginx)
  frontend:
    image: nginx:alpine
    container_name: frontend
    ports:
      - "80:80"
    volumes:
      - ./frontend:/usr/share/nginx/html
    depends_on:
      - backend
    networks:
      - app-network

  # 🔧 Backend (Node.js)
  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile
    container_name: backend
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DB_HOST=database
      - DB_USER=root
      - DB_PASS=secret123
      - DB_NAME=myapp
    depends_on:
      - database
    networks:
      - app-network
    restart: unless-stopped

  # 🗄️  Database (MySQL)
  database:
    image: mysql:8.0
    container_name: database
    environment:
      MYSQL_ROOT_PASSWORD: secret123
      MYSQL_DATABASE: myapp
      MYSQL_USER: appuser
      MYSQL_PASSWORD: apppass
    volumes:
      - db-data:/var/lib/mysql
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql
    ports:
      - "3306:3306"
    networks:
      - app-network
    restart: unless-stopped

  # 🔴 Cache (Redis)
  cache:
    image: redis:7-alpine
    container_name: cache
    ports:
      - "6379:6379"
    volumes:
      - redis-data:/data
    networks:
      - app-network

networks:
  app-network:
    driver: bridge

volumes:
  db-data:
  redis-data:
```

```bash
# 🐙 Docker Compose Commands

# Saare containers start karo (background)
docker compose up -d

# Logs dekho
docker compose logs
docker compose logs -f backend

# Status dekho
docker compose ps

# Containers stop karo
docker compose stop

# Containers stop + delete karo
docker compose down

# Volumes ke saath delete karo
docker compose down -v

# Rebuild karke start karo
docker compose up -d --build

# Specific service restart
docker compose restart backend

# Specific service ke andar jao
docker compose exec backend bash
```

---

## 📤 Docker Hub

```bash
# 📤 Docker Hub pe push karo

# Step 1: Login karo
docker login
# Username: tumhara-dockerhub-username
# Password: xxxxxxxx

# Step 2: Image tag karo
docker tag myapp:latest username/myapp:latest
docker tag myapp:latest username/myapp:v1.0

# Step 3: Push karo
docker push username/myapp:latest
docker push username/myapp:v1.0

# Step 4: Kahi se bhi pull karo!
docker pull username/myapp:latest


# 🔒 Private Registry (AWS ECR)
# ECR login
aws ecr get-login-password --region ap-south-1 | \
    docker login --username AWS --password-stdin \
    ACCOUNT.dkr.ecr.ap-south-1.amazonaws.com

# ECR me push
docker tag myapp:latest \
    ACCOUNT.dkr.ecr.ap-south-1.amazonaws.com/myapp:latest
docker push \
    ACCOUNT.dkr.ecr.ap-south-1.amazonaws.com/myapp:latest
```

---

## 💡 Pro Tips & Tricks

```bash
# ════════════════════════════════════════════
# 💡 TIP 1: .dockerignore FILE BANAO
# ════════════════════════════════════════════
cat > .dockerignore << 'EOF'
node_modules
.git
.env
*.log
dist
coverage
.DS_Store
EOF
# Build fast hogi, image chhoti hogi! ✅


# ════════════════════════════════════════════
# 💡 TIP 2: ALPINE IMAGES USE KARO
# ════════════════════════════════════════════
# node:18       → 1.1 GB  ❌ Bada
# node:18-slim  → 280 MB  ✅ Better
# node:18-alpine→  70 MB  ✅✅ Best!


# ════════════════════════════════════════════
# 💡 TIP 3: MULTI-STAGE BUILD
# ════════════════════════════════════════════
# Build stage alag, production stage alag
# Final image me sirf zaruri cheez!
# See: Nginx Static Website Dockerfile above ☝️


# ════════════════════════════════════════════
# 💡 TIP 4: HEALTH CHECK ADD KARO
# ════════════════════════════════════════════
# Dockerfile me:
# HEALTHCHECK --interval=30s --timeout=3s \
#   CMD curl -f http://localhost:3000/ || exit 1


# ════════════════════════════════════════════
# 💡 TIP 5: SYSTEM CLEANUP KARO
# ════════════════════════════════════════════
# Sab unused resources delete karo
docker system prune -a

# Size dekho
docker system df

# Specific cleanup
docker image prune      # Unused images
docker container prune  # Stopped containers
docker volume prune     # Unused volumes
docker network prune    # Unused networks
```

---

## ❌ Common Errors & Fixes

```
╔══════════════════════════════════════════════════════════════════╗
║               COMMON DOCKER ERRORS & SOLUTIONS                  ║
╠══════════════════════════════════════════════════════════════════╣
║  ❌ Error                        ║  ✅ Fix                       ║
╠══════════════════════════════════╬═══════════════════════════════╣
║  Permission denied               ║  sudo usermod -aG docker $USER║
║  (docker socket)                 ║  newgrp docker                ║
╠══════════════════════════════════╬═══════════════════════════════╣
║  Port already in use             ║  docker ps se purana container║
║                                  ║  stop karo ya alag port use   ║
╠══════════════════════════════════╬═══════════════════════════════╣
║  Image not found                 ║  docker pull karo pehle       ║
╠══════════════════════════════════╬═══════════════════════════════╣
║  Container exits immediately     ║  docker logs se error dekho   ║
╠══════════════════════════════════╬═══════════════════════════════╣
║  No space left on device         ║  docker system prune -a       ║
╠══════════════════════════════════╬═══════════════════════════════╣
║  Cannot connect to Docker daemon ║  sudo systemctl start docker  ║
╠══════════════════════════════════╬═══════════════════════════════╣
║  Build fails — cache issue       ║  docker build --no-cache      ║
╠══════════════════════════════════╬═══════════════════════════════╣
║  Compose network error           ║  docker compose down && up    ║
╠══════════════════════════════════╬═══════════════════════════════╣
║  Volume permission denied        ║  Container me user check karo ║
╚══════════════════════════════════╩═══════════════════════════════╝
```

---

## 📋 Cheat Sheet

```
╔════════════════════════════════════════════════════════════════════╗
║                    DOCKER QUICK CHEAT SHEET                      ║
╠═══════════════════════════╦════════════════════════════════════════╣
║  🖼️  IMAGES                ║                                       ║
║  Pull                      ║  docker pull image:tag                ║
║  List                      ║  docker images                        ║
║  Build                     ║  docker build -t name:tag .           ║
║  Delete                    ║  docker rmi image:tag                 ║
║  Prune                     ║  docker image prune                   ║
╠═══════════════════════════╬════════════════════════════════════════╣
║  🏃 CONTAINERS             ║                                       ║
║  Run (detached)            ║  docker run -d -p 80:80 nginx         ║
║  List running              ║  docker ps                            ║
║  List all                  ║  docker ps -a                         ║
║  Stop                      ║  docker stop container_id             ║
║  Remove                    ║  docker rm container_id               ║
║  Logs                      ║  docker logs -f container_id          ║
║  Bash access               ║  docker exec -it container bash       ║
║  Stats                     ║  docker stats                         ║
╠═══════════════════════════╬════════════════════════════════════════╣
║  💾 VOLUMES                ║                                       ║
║  Create                    ║  docker volume create mydata          ║
║  List                      ║  docker volume ls                     ║
║  Mount                     ║  docker run -v mydata:/path           ║
║  Delete                    ║  docker volume rm mydata              ║
╠═══════════════════════════╬════════════════════════════════════════╣
║  🌐 NETWORKS               ║                                       ║
║  Create                    ║  docker network create mynet          ║
║  List                      ║  docker network ls                    ║
║  Connect                   ║  docker run --network mynet           ║
╠═══════════════════════════╬════════════════════════════════════════╣
║  🐙 COMPOSE                ║                                       ║
║  Start                     ║  docker compose up -d                 ║
║  Stop                      ║  docker compose down                  ║
║  Logs                      ║  docker compose logs -f               ║
║  Status                    ║  docker compose ps                    ║
║  Rebuild                   ║  docker compose up -d --build         ║
╠═══════════════════════════╬════════════════════════════════════════╣
║  🧹 CLEANUP                ║                                       ║
║  All unused                ║  docker system prune -a               ║
║  Disk usage                ║  docker system df                     ║
╚═══════════════════════════╩════════════════════════════════════════╝
```

---

## 📚 Resources

| 📖 Resource | 🔗 Link |
|-------------|---------|
| 🐳 Docker Docs | [docs.docker.com](https://docs.docker.com) |
| 🌐 Docker Hub | [hub.docker.com](https://hub.docker.com) |
| 📝 Dockerfile Reference | [docs.docker.com/reference/dockerfile](https://docs.docker.com/reference/dockerfile/) |
| 🐙 Compose Reference | [docs.docker.com/compose](https://docs.docker.com/compose/) |
| 🎓 Docker Tutorial | [docker.com/get-started](https://www.docker.com/get-started/) |
