# OmniAgent - Multi-Agent E-commerce Intelligence System

<p align="center">
  <img src="./ai-frontend/src/assets/ai-orb.gif" alt="OmniAgent Logo" width="120" height="120" style="border-radius: 50%;">
</p>

<p align="center">
  <strong>AI-powered multi-agent orchestration for intelligent e-commerce business operations</strong>
  <br/>
  Built with <a href="https://github.com/langchain-ai/langgraphjs">LangGraph.js</a> and <a href="https://ollama.ai">Ollama</a>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License"></a>
  <a href="./CONTRIBUTING.md"><img src="https://img.shields.io/badge/Contributions-Welcome-brightgreen" alt="Contributions"></a>
  <a href="https://nodejs.org/"><img src="https://img.shields.io/badge/Node.js-20+-green" alt="Node"></a>
</p>

---

## 🎯 Overview

OmniAgent is a **local-first, privacy-focused AI system** that transforms how small business owners manage e-commerce operations. Instead of reactive dashboards, OmniAgent **proactively hunts for business problems** and presents intelligent, actionable solutions through a familiar chat interface.

### Why OmniAgent?

- **🏠 Fully Local**: Runs entirely on your machine using Ollama—no cloud APIs, no data leaving your servers
- **🤖 Multi-Agent Collaboration**: 5 specialized agents that debate decisions and reach consensus
- **📊 Proactive Intelligence**: Continuous monitoring with automatic alerts
- **⚡ Action-Oriented**: Doesn't just report problems—proposes solutions with financial impact analysis
- **🔐 Privacy First**: Sensitive business data (revenue, inventory, customers) stays protected locally
- **📱 Modern UX**: Web dashboard + Telegram notifications for on-the-go management

### Real-World Example

> **8:00 AM**: Warden Agent detects Product A selling 3x faster than usual (viral social post)
>
> **8:02 AM**: Finance Agent calculates budget impact of restocking 500 units
>
> **8:03 AM**: You get a Telegram notification: _"Trending opportunity! Restock 500 units (₹25,000)? [Approve] [Edit] [Reject]"_
>
> **8:04 AM**: You tap Approve while having coffee
>
> **8:05 AM**: Executive Agent updates inventory and notifies warehouse

---

## ✨ Key Features

### 🕵️ Intelligent Monitoring

- **Inventory Tracking**: Automatic alerts for low stock, overstock, or slow movers
- **Sales Analytics**: Detect trends, anomalies, and demand spikes
- **Customer Insights**: Monitor cart abandonment, return rates, sentiment
- **Financial Health**: Track cash flow, budget constraints, profitability

### 🤖 Multi-Agent System

| Agent         | Specialty              | Capabilities                                             |
| ------------- | ---------------------- | -------------------------------------------------------- |
| **Warden**    | Monitoring & Detection | Inventory surveillance, trend analysis, alert triggers   |
| **Finance**   | Budget & Approvals     | Financial analysis, budget enforcement, ROI calculations |
| **Architect** | Data Analysis          | SQL query generation, schema analysis, custom reports    |
| **Support**   | Customer Care          | Draft responses, email automation, sentiment analysis    |
| **Executive** | Coordination           | Consensus building, action execution, notifications      |

### 💬 Multi-Interface Access

- **Web Dashboard**: Deep-dive analysis with full thought traces
- **Telegram Bot**: Mobile-first alerts and quick approvals
- **REST API**: Program custom workflows and integrations

### 🔄 Human-in-the-Loop Workflow

Agents propose → You decide → System executes (with proper safeguards)

---

## 🚀 Quick Start

### Prerequisites

- **Node.js 20.x** - [Download](https://nodejs.org/)
- **Ollama** - [Download](https://ollama.ai/) (for local AI)
- **npm** or **yarn** for package management

### 1️⃣ Clone & Install

```bash
git clone https://github.com/AMV0027/omni-agent
cd omni-agent

npm install
```

### 2️⃣ Configure Ollama

```bash
# Download and start Ollama
# Then in terminal, pull the recommended model
ollama pull qwen3:0.6b

# Optional: For better function calling
ollama pull functiongemma:latest
```

### 3️⃣ Setup Environment

```bash
# Copy and configure environment variables
cp .env.example .env

# Edit .env with your settings (API keys are optional)
nano .env  # or use your preferred editor
```

### 4️⃣ Initialize Database

```bash
# Install, migrate, and seed the database
npm run db:setup
```

### 5️⃣ Start Development

```bash
# Start main API server
npm run dev

# In separate terminals (optional):
npm run dev:ai-frontend     # Web chat dashboard
npm run dev:ecom-frontend   # E-commerce store

# Or start all at once
npm run dev:all
```

The API will be available at **http://localhost:8000**

---

## 📡 API Reference

### Health Check

```bash
GET /api/health
```

### Chat with Agents

```bash
POST /api/chat/message
Content-Type: application/json

{
  "message": "Check inventory levels",
  "sessionId": "optional-session-id"
}
```

### More Endpoints

See [API Specification](./documentation/05-api-specification.md) for complete documentation.

---

## 📚 Documentation

- **[System Overview](./documentation/01-system-overview.md)** - Architecture and design
- **[Technical Design](./documentation/03-technical-design.md)** - Deep dive into implementation
- **[Agent Architecture](./documentation/06-agent-architecture.md)** - How agents work together
- **[API Specification](./documentation/05-api-specification.md)** - REST endpoints and webhooks
- **[Data Model](./documentation/04-data-model.md)** - Database schema overview
- **[Implementation Guide](./documentation/00-implementation-guide.md)** - Setup and deployment

---

## 🗂️ Project Structure

```
omniagent/
├── src/
│   ├── agents/              # Agent definitions & orchestration
│   │   ├── graph.ts         # LangGraph workflow
│   │   ├── nodes.ts         # Agent implementations
│   │   ├── state.ts         # Shared state definition
│   │   ├── prompts.ts       # System prompts
│   │   └── tools.ts         # Available tools
│   ├── routes/              # API endpoints
│   ├── services/            # Business logic
│   ├── config/              # Configuration & setup
│   ├── types/               # TypeScript definitions
│   └── server.ts            # Express server
├── prisma/                  # Database schema & migrations
├── ai-frontend/             # React dashboard
├── ecom-frontend/           # E-commerce store
├── documentation/           # Technical documentation
└── .env.example             # Configuration template
```

---

## 🛠️ Development

### Available Commands

```bash
# Development
npm run dev              # Start API with auto-reload
npm run build            # Compile TypeScript
npm run start            # Run compiled version

# Database
npm run prisma:generate  # Regenerate Prisma client
npm run prisma:migrate   # Apply database migrations
npm run prisma:studio    # Open Prisma GUI
npm run db:setup         # Complete setup (migrations + seed)

# Frontend
npm run dev:ai-frontend  # Start AI dashboard
npm run dev:ecom-frontend # Start store frontend
npm run dev:all          # All services together
```

### Project Scripts

All scripts are configured in [package.json](./package.json)

---

## 🔧 Configuration

### AI Providers

**Ollama (Recommended - Default)**

- Runs completely locally
- No API keys needed
- Privacy-first approach
- Limited to your machine's capabilities

**OpenRouter (Optional)**

- Paid API service
- Access to premium models
- Requires `OPENROUTER_API_KEY`

### Optional Features

Enable features by adding API keys to `.env`:

| Feature         | Provider | Setup                                                             |
| --------------- | -------- | ----------------------------------------------------------------- |
| Telegram Alerts | Telegram | [BotFather](https://t.me/botfather)                               |
| Email Support   | Gmail    | [App Password](https://support.google.com/accounts/answer/185833) |
| Product Images  | Pexels   | [API Key](https://www.pexels.com/api/)                            |
| Web Search      | Tavily   | [API Key](https://tavily.com)                                     |

---

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

### Quick Start for Contributors

```bash
# 1. Fork the repository
# 2. Create a feature branch
git checkout -b feature/your-feature

# 3. Make changes and test
npm run build
npm run dev

# 4. Commit with clear messages
git commit -m "feat: add your feature"

# 5. Push and create a Pull Request
```

---

## 📋 Roadmap

- [ ] **v1.1** - Enhanced agent personality system
- [ ] **v1.2** - Shopify/WooCommerce marketplace connectors
- [ ] **v1.3** - Advanced scheduling and automation rules
- [ ] **v2.0** - Multi-language support and regional models

---

## 🔒 Security & Privacy

- **Local Processing**: All AI inference happens locally with Ollama
- **No Tracking**: No telemetry or usage tracking
- **Data Ownership**: All business data remains in your control
- **Open Source**: Fully auditable codebase

**Security Recommendations:**

- Use strong database credentials
- Keep API keys confidential
- Run in isolated network for production
- Regular backups of SQLite database

See [SECURITY.md](./SECURITY.md) for detailed security guidelines.

---

## 📄 License

OmniAgent is licensed under the **MIT License** - see [LICENSE](./LICENSE) for details.

---

## ❓ Support & Questions

- 📖 Check the [documentation](./documentation/) first
- 🐛 [Report bugs](https://github.com/AMV0027/omni-agent/issues/new?template=bug_report.md)
- ✨ [Request features](https://github.com/AMV0027/omni-agent/issues/new?template=feature_request.md)
- 💬 [Ask questions](https://github.com/AMV0027/omni-agent/issues/new?template=question.md)

---

## 🙏 Acknowledgments

- [LangChain](https://github.com/langchain-ai/langchainjs) - AI orchestration framework
- [LangGraph](https://github.com/langchain-ai/langgraphjs) - Agent graph coordination
- [Ollama](https://ollama.ai/) - Local LLM runtime
- [Prisma](https://www.prisma.io/) - Database ORM

---

<p align="center">
  <strong>Made with ❤️ for solo entrepreneurs and small business owners</strong>
  <br/>
  <a href="./CONTRIBUTING.md">Contribute</a> • 
  <a href="./documentation/">Docs</a> • 
  <a href="https://github.com/AMV0027/omni-agent/issues">Issues</a>
</p>

# Start production server

npm start

# Open Prisma Studio (database GUI)

npm run prisma:studio

````

## 📚 Documentation

See the [`documentation/`](./documentation/) folder for comprehensive technical docs:

- `00-implementation-guide.md` - Quick start guide
- `01-system-overview.md` - System architecture
- `02-feature-driven-doc.md` - Feature specifications
- `03-technical-design.md` - Technical design
- `04-data-model.md` - Database schema
- `05-api-specification.md` - API documentation
- `06-agent-architecture.md` - Agent system details

## 🧪 Testing the System

### 1. Start Ollama
```bash
ollama serve
````

### 2. Test with cURL

```bash
curl -X POST http://localhost:8000/api/chat/message \
  -H "Content-Type: application/json" \
  -d '{"message": "What is the status of inventory?"}'
```

### 3. Expected Response

```json
{
  "success": true,
  "data": {
    "response": "[Warden] Analyzing inventory...\n[Finance] Budget analysis...",
    "decision": {
      "status": "approved",
      "votes": [...]
    }
  }
}
```

## 🔧 Configuration

Edit `.env` file:

```env
# Database
DATABASE_URL="file:./dev.db"

# Ollama
OLLAMA_BASE_URL="http://localhost:11434"
OLLAMA_MODEL="phi4-mini:latest"

# Server
PORT=8000
NODE_ENV=development
```

## 📝 License

ISC

---

Built with ❤️ using LangGraph.js, Ollama, and TypeScript
