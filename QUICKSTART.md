# Quick Reference Guide

Fast lookup for common OmniAgent tasks.

## 🚀 Getting Started (2 minutes)

```bash
# Clone and setup
git clone https://github.com/AMV0027/omni-agent
cd omni-agent
npm install

# Configure
cp .env.example .env     # Edit with your settings

# Start
npm run db:setup         # Setup database
npm run dev              # Run dev server
```

**Open in browser**: http://localhost:8000

## 📝 Development Commands

```bash
# Start services
npm run dev              # Main API
npm run dev:ai-frontend  # Dashboard
npm run dev:ecom-frontend # Store frontend
npm run dev:all          # All together

# Build & run
npm run build            # Compile TypeScript
npm run start            # Run compiled version

# Database
npm run db:setup         # Complete setup
npm run prisma:migrate   # Apply migrations
npm run prisma:studio    # Open Prisma GUI
npm run prisma:seed      # Seed data

# Check for issues
npm run build            # Will show TypeScript errors
```

## 🏗️ Project Structure

```
src/agents/              # 5 specialized agents (Warden, Finance, Architect, Support, Executive)
src/routes/              # API endpoints (chat, orders, products, returns, support)
src/services/            # Business logic (agent execution, memory, enrichment)
src/config/              # LLM & database configuration
prisma/                  # Database schema & migrations
ai-frontend/             # React dashboard
ecom-frontend/           # E-commerce store
documentation/           # Technical docs
```

## 🤖 The 5 Agents

| Agent         | Role              | Triggers                     |
| ------------- | ----------------- | ---------------------------- |
| **Warden**    | Monitor & detect  | Inventory, sales, trends     |
| **Finance**   | Approve budgets   | Financial analysis, ROI      |
| **Architect** | Data analysis     | Custom queries, reports      |
| **Support**   | Draft responses   | Customer issues, reviews     |
| **Executive** | Execute decisions | Final approval, coordination |

## 🔌 Key APIs

```bash
# Health check
curl http://localhost:8000/api/health

# Chat with agents
curl -X POST http://localhost:8000/api/chat/message \
  -H "Content-Type: application/json" \
  -d '{"message": "Check inventory"}'

# List endpoints
curl http://localhost:8000/api/

# See documentation/05-api-specification.md for all endpoints
```

## ⚙️ Configuration

### Environment Variables

```env
# AI Provider (recommended: ollama for privacy)
AI_PROVIDER=ollama
OLLAMA_BASE_URL=http://localhost:11434
OLLAMA_MODEL=qwen3:0.6b

# Or use cloud API
AI_PROVIDER=openrouter
OPENROUTER_API_KEY=sk-or-v1-xxx

# Optional features
TELEGRAM_BOT_TOKEN=xxx           # For notifications
TAVILY_API_KEY=xxx               # For web search
GMAIL_EMAIL=xxx                  # For email
PEXELS_API_KEY=xxx               # For images
```

See `.env.example` for full list.

## 🧪 Testing

```bash
# Run development
npm run dev
# Check server is responding
curl http://localhost:8000/api/health

# Test agent interaction
curl -X POST http://localhost:8000/api/chat/message \
  -H "Content-Type: application/json" \
  -d '{"message": "Check inventory"}'
```

## 📦 Adding Dependencies

```bash
# Add a package
npm install package-name

# Add dev dependency
npm install --save-dev package-name

# Update all
npm update

# Check security issues
npm audit
npm audit fix
```

## 🐛 Debugging

### View Logs

```bash
# Terminal logs (when running npm run dev)
# Will show errors and console.log output

# Database
npm run prisma:studio   # Interactive database GUI
```

### Common Issues

**Port 8000 already in use**

```bash
lsof -i :8000          # Find what's using port
kill -9 <PID>          # Kill it
```

**Database locked**

```bash
rm *.db-shm *.db-wal   # Remove WAL files
npm run prisma:migrate # Reapply migrations
```

**Ollama won't connect**

```bash
curl http://localhost:11434/api/tags  # Check if running
ollama serve                          # Start Ollama
```

## 📚 Documentation Map

| Document                               | Purpose             | Read When               |
| -------------------------------------- | ------------------- | ----------------------- |
| README.md                              | Overview            | Getting started         |
| CONTRIBUTING.md                        | How to contribute   | Planning a PR           |
| SECURITY.md                            | Security guidelines | Before production       |
| DEPLOYMENT.md                          | Production setup    | Deploying               |
| documentation/01-system-overview.md    | System design       | Understand architecture |
| documentation/06-agent-architecture.md | Agent details       | Debug agent issues      |
| documentation/05-api-specification.md  | API reference       | Using the API           |
| CHANGELOG.md                           | Version history     | Tracking changes        |

## 🔐 Security Reminders

⚠️ **CRITICAL**:

- Never commit `.env` file
- Never put API keys in code
- Never log sensitive data
- Use `.env.example` as template only

## 🚢 Deployment Quick Steps

```bash
# 1. Build
npm run build

# 2. Setup environment
cp .env.example .env
# Edit .env with production values

# 3. Setup database
npm run db:setup

# 4. Start with process manager
pm2 start dist/server.js

# Or use Docker
docker-compose up -d
```

See [DEPLOYMENT.md](./DEPLOYMENT.md) for full guide.

## 💡 Tips & Tricks

### Auto-reload during development

```bash
npm run dev  # Uses nodemon, auto-restarts on changes
```

### Run multiple services at once

```bash
npm run dev:all  # Runs API + both frontends concurrently
```

### Check TypeScript compilation

```bash
npm run build  # Will show type errors before running
```

### Update Prisma when schema changes

```bash
npm run prisma:migrate  # Create migration for schema changes
```

### View database visually

```bash
npm run prisma:studio  # Opens browser-based Prisma GUI
```

## 🔗 Useful Links

- **GitHub**: https://github.com/AMV0027/omni-agent
- **LangGraph.js**: https://github.com/langchain-ai/langgraphjs
- **Ollama**: https://ollama.ai
- **Prisma**: https://www.prisma.io
- **Express.js**: https://expressjs.com

## 📞 Support

- 📖 [Documentation](./documentation/)
- 🐛 [Report bugs](https://github.com/AMV0027/omni-agent/issues/new?template=bug_report.md)
- ✨ [Request features](https://github.com/AMV0027/omni-agent/issues/new?template=feature_request.md)
- 💬 [Ask questions](https://github.com/AMV0027/omni-agent/issues/new?template=question.md)

---

**Need more help?** Check [CONTRIBUTING.md](./CONTRIBUTING.md) or the [DOCUMENTATION_INDEX.md](./DOCUMENTATION_INDEX.md)
