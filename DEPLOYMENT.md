# Deployment Guide

This guide covers deploying OmniAgent in production environments.

## ⚠️ Pre-Deployment Checklist

- [ ] All API keys configured in `.env` (or use placeholder if not needed)
- [ ] Database backups configured
- [ ] `.env` file is in `.gitignore` (never commit credentials)
- [ ] Ollama service is running and accessible
- [ ] Firewall rules configured for required ports
- [ ] SSL/TLS certificates ready (for HTTPS)
- [ ] Sufficient disk space for database growth
- [ ] Memory requirements met (minimum 2GB recommended)

## 🚀 Deployment Options

### Option 1: Direct Server Deployment

#### System Requirements

- **OS**: Linux (Ubuntu 22.04 LTS recommended), macOS, Windows Server
- **CPU**: 2+ cores
- **RAM**: 4GB minimum (8GB recommended)
- **Disk**: 10GB+ for application and models
- **Network**: Stable internet connection

#### Steps

```bash
# 1. SSH into your server
ssh user@your-server

# 2. Clone repository
git clone https://github.com/AMV0027/omni-agent
cd omni-agent

# 3. Install Node.js (if not present)
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# 4. Install and setup Ollama
curl https://ollama.ai/install.sh | sh

# 5. Pull required models in background
ollama pull qwen3:0.6b &
ollama pull functiongemma:latest &

# 6. Configure .env
cp .env.example .env
# Edit with production values
nano .env

# 7. Setup database
npm install
npm run db:setup

# 8. Build application
npm run build

# 9. Start with process manager (see below)
```

#### Process Manager Setup

**Using PM2 (Recommended)**

```bash
npm install -g pm2

# Start application
pm2 start dist/server.js --name "omniagent"

# Save startup configuration
pm2 startup
pm2 save

# Monitor
pm2 logs omniagent
pm2 status
```

**Using systemd**

Create `/etc/systemd/system/omniagent.service`:

```ini
[Unit]
Description=OmniAgent Multi-Agent System
After=network.target

[Service]
Type=simple
User=omniagent
WorkingDirectory=/home/omniagent/omni-agent
ExecStart=/usr/bin/node dist/server.js
Restart=on-failure
RestartSec=5

Environment="NODE_ENV=production"
EnvironmentFile=/home/omniagent/omni-agent/.env

[Install]
WantedBy=multi-user.target
```

Then:

```bash
sudo systemctl daemon-reload
sudo systemctl enable omniagent
sudo systemctl start omniagent
```

### Option 2: Docker Deployment

#### Prerequisites

- Docker installed and running

#### Dockerfile

Create `Dockerfile`:

```dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .
RUN npm run build
RUN npm run prisma:generate

ENV NODE_ENV=production
EXPOSE 8000

CMD ["node", "dist/server.js"]
```

#### Docker Compose

Create `docker-compose.yml`:

```yaml
version: "3.8"

services:
  ollama:
    image: ollama/ollama:latest
    ports:
      - "11434:11434"
    volumes:
      - ollama_data:/root/.ollama
    environment:
      - OLLAMA_HOST=0.0.0.0:11434

  omniagent:
    build: .
    ports:
      - "8000:8000"
    environment:
      - NODE_ENV=production
      - DATABASE_URL=file:./omniagent.db
      - OLLAMA_BASE_URL=http://ollama:11434
      - PORT=8000
    depends_on:
      - ollama
    volumes:
      - ./data:/app/data
    restart: unless-stopped

volumes:
  ollama_data:
```

Deploy:

```bash
docker-compose up -d
```

### Option 3: Cloud Platform Deployment

#### Railway.app

1. Create account at railway.app
2. Connect GitHub repository
3. Set environment variables
4. Deploy (Note: Ollama models may not fit on free tier)

#### Render

1. Create new Web Service on render.com
2. Connect repository
3. Set build command: `npm install && npm run build`
4. Set start command: `node dist/server.js`
5. Add environment variables
6. Deploy

**Note**: Cloud deployments without local Ollama will require OpenRouter API key.

---

## 🔒 Production Security

### HTTPS/SSL

Use Nginx as reverse proxy:

```nginx
server {
    listen 443 ssl http2;
    server_name yourdomain.com;

    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;

    location / {
        proxy_pass http://localhost:8000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

### Firewall Rules

```bash
# Allow SSH
sudo ufw allow 22

# Allow HTTP/HTTPS
sudo ufw allow 80
sudo ufw allow 443

# Allow internal Ollama (if separate server)
sudo ufw allow from 10.0.0.0/8 to any port 11434

# Enable firewall
sudo ufw enable
```

### Secrets Management

- Use environment variable files (**.env** should NOT be in git)
- For sensitive deployments, consider:
  - HashiCorp Vault
  - AWS Secrets Manager
  - Azure Key Vault
  - Kubernetes Secrets

### Database Security

```bash
# Backup database regularly
0 2 * * * /path/to/backup-script.sh

# Enable SQLite WAL mode (in code)
PRAGMA journal_mode=WAL;
```

---

## 📊 Monitoring & Logging

### Application Logs

With PM2:

```bash
pm2 logs omniagent
pm2 logs omniagent --err
```

### System Monitoring

```bash
# Monitor with PM2
pm2 monit

# System resources
htop
```

### Logging to File

Modify server.ts to add logging:

```typescript
import fs from "fs";

const logStream = fs.createWriteStream("logs/app.log", { flags: "a" });
app.use(express.json());
// Add logging middleware
```

---

## 🔄 Updates & Maintenance

### Updating OmniAgent

```bash
# Pull latest changes
git pull origin main

# Update dependencies
npm update

# Run migrations
npm run prisma:migrate

# Rebuild
npm run build

# Restart service
pm2 restart omniagent
# or
sudo systemctl restart omniagent
```

### Ollama Model Updates

```bash
# Pull new model versions
ollama pull qwen3:0.6b

# Models are downloaded to ~/.ollama/models
```

---

## 🆘 Troubleshooting

### Port Already in Use

```bash
# Find process using port 8000
lsof -i :8000

# Kill process
kill -9 <PID>
```

### Database Locked

```bash
# Remove WAL files if corrupted
rm dev.db-shm dev.db-wal

# Reset database
rm dev.db
npm run db:setup
```

### Ollama Connection Issues

```bash
# Check if Ollama is running
curl http://localhost:11434/api/tags

# Restart Ollama service
sudo systemctl restart ollama
# or
ollama serve
```

---

## 📈 Scaling Considerations

### Single Process

Limited to: ~100-200 concurrent requests

### Load Balancing

```nginx
upstream omniagent {
    server localhost:8000;
    server localhost:8001;
    server localhost:8002;
}

server {
    listen 80;
    location / {
        proxy_pass http://omniagent;
    }
}
```

### Distributed Setup

For high-traffic scenarios:

- Use shared database (PostgreSQL instead of SQLite)
- Add Redis for session caching
- Scale horizontally with multiple instances
- Use dedicated Ollama server(s)

---

## 📞 Support

For deployment issues:

- Check [GitHub Issues](https://github.com/AMV0027/omni-agent/issues)
- Review logs carefully
- Ensure all prerequisites are met
