<div align="center">
  <h1> TradeAxis</h1>
  <p><em>The Next-Generation Institutional-Grade Trading & AI Analysis Ecosystem</em></p>

  <p>
    <a href="https://nextjs.org/"><img src="https://img.shields.io/badge/Next.js-14-black?style=for-the-badge&logo=next.js" alt="Next.js" /></a>
    <a href="https://www.typescriptlang.org/"><img src="https://img.shields.io/badge/TypeScript-5.0-blue?style=for-the-badge&logo=typescript" alt="TypeScript" /></a>
    <a href="https://tailwindcss.com/"><img src="https://img.shields.io/badge/Tailwind_CSS-3.0-38B2AC?style=for-the-badge&logo=tailwind-css" alt="Tailwind CSS" /></a>
    <a href="https://www.postgresql.org/"><img src="https://img.shields.io/badge/PostgreSQL-15-336791?style=for-the-badge&logo=postgresql" alt="PostgreSQL" /></a>
    <a href="https://openai.com/"><img src="https://img.shields.io/badge/OpenAI-GPT--4-412991?style=for-the-badge&logo=openai" alt="OpenAI" /></a>
  </p>
</div>

---

## 📋 Table of Contents
- [📋 Table of Contents](#-table-of-contents)
- [📖 Overview](#-overview)
- [🎯 Vision](#-vision)
- [✨ Features](#-features)
- [💻 Tech Stack](#-tech-stack)
- [🏗️ Architecture](#️-architecture)
- [🔀 Flow](#-flow)
- [📂 Project Structure](#-project-structure)
- [🚀 Setup](#-setup)
  - [Prerequisites](#prerequisites)
  - [Installation Steps](#installation-steps)
- [📘 Usage Guide](#-usage-guide)
- [🔗 API Reference (Internal)](#-api-reference-internal)
- [🛠️ Troubleshooting](#️-troubleshooting)
- [🔐 Environment Variables](#-environment-variables)
- [☁️ Deployment](#️-deployment)
- [⚡ Performance](#-performance)

## Code Availability

This repository is a **sanitized showcase version** of a production SaaS system.

Core business logic, sensitive components, and full implementation details are intentionally excluded to protect intellectual property and maintain system security.

The goal of this repository is to demonstrate:
- System architecture  
- Code structure  
- Engineering practices  

📩 **Full codebase access can be provided upon request for  technical evaluation.**

Contact: **amar01pawar80@gmail.com**

## 📖 Overview
TradeAxis  is a comprehensive, professional-grade trading platform engineered for both novice investors and experienced traders. By unifying real-time market data, advanced AI-powered analysis (TradeAxis), paper trading capabilities, and sophisticated technical charting, TradeAxis provides a complete ecosystem for modern investment analysis and strategy backtesting.

## 🎯 Vision
**Short-term Vision:** Democratize institutional-level trading tools and AI-driven market insights for retail investors by providing an intuitive, fast, and unified interface.  
**Long-term Vision:** Evolve into the definitive all-in-one ecosystem for automated trading, multi-asset portfolio management, advanced ML-based predictive modeling, and continuous strategy backtesting.

## ✨ Features
- **Real-Time Market Dashboard**: Live portfolio tracking, market gainers/losers, sector performance, and market session indicators.
- **TradeAxis AI Assistant**: Advanced conversational AI powered by GPT-4 for natural language stock screening, technical analysis, and personalized trading recommendations.
- **Advanced Stock Screener**: Multi-criteria and natural language filtering with real-time results and saved queries.
- **Paper Trading & Portfolio Manager**: Risk-free simulated trading environment with detailed performance analytics, trade history, and PnL tracking.
- **Professional Charting**: Interactive WebGL-based charts (Lightweight Charts/Recharts) featuring multiple timeframes, technical indicators, and drawing tools.
- **Market Intelligence**: AI-curated financial news aggregation, sentiment analysis, earnings calendars, and unusual volume alerts.
- **Machine Learning Predictions**: Python-based ML microservices leveraging QLib for quantitative investment datasets and predictive backtesting.
- **Watchlists & Price Alerts**: Real-time monitoring, multi-watchlist management, and customizable price threshold notifications.

## 💻 Tech Stack
| Category | Technologies |
|---|---|
| **Frontend** | Next.js 14 (App Router), React, TypeScript, Tailwind CSS, shadcn/ui, Framer Motion, Zustand |
| **Backend** | Node.js 18+, Next.js API Routes (Serverless), Prisma ORM |
| **Database** | PostgreSQL 15+ |
| **AI & ML** | OpenAI GPT-4, Python 3.8+, QLib, Custom ML Scripts |
| **Data Providers** | Polygon.io, Yahoo Finance, News API |
| **Authentication**| NextAuth.js (OAuth + Credentials), JWT |
| **Charts/UI** | Lightweight Charts, Recharts, Lucide React, Tremor |

## 🏗️ Architecture

```mermaid
graph TD
    Client[Web Browser / Client]
    Client --> |HTTP/REST & WebSockets| Frontend[Next.js 14 Frontend]
    
    subgraph TradeAxis Platform
        Frontend --> |API Routes| Backend[Next.js Serverless API]
        Backend --> |ORM| Prisma[Prisma ORM]
        Prisma --> |SQL| DB[(PostgreSQL Database)]
        Backend --> |State/Session| Auth[NextAuth.js]
    end
    
    subgraph External Services
        Backend --> |Market Data| Polygon[Polygon.io API]
        Backend --> |Fallback Data| YFinance[Yahoo Finance API]
        Backend --> |AI Analysis| OpenAI[OpenAI GPT-4]
    end
    
    subgraph ML & Python Engine
        Backend --> |Spawn/Exec| PythonScripts[Python ML Scripts]
        PythonScripts --> |Quantitative Data| QLib[Microsoft QLib]
        PythonScripts --> |Predictions| DB
    end
```

## 🔀 Flow
**User Journey & Data Flow**
```mermaid
sequenceDiagram
    participant User
    participant UI as Next.js UI
    participant API as Next.js API
    participant AI as TradeAxis (OpenAI)
    participant Market as Polygon.io
    participant DB as PostgreSQL

    User->>UI: Ask "Analyze AAPL for swing trade"
    UI->>API: POST /api/ai/chat
    API->>Market: Fetch AAPL Real-time Data & Technicals
    Market-->>API: Return Stock Data
    API->>AI: Send Prompt + Context + Market Data
    AI-->>API: Stream Analysis & Strategy Recommendation
    API-->>UI: Stream Response to User
    User->>UI: Click "Buy 100 AAPL (Paper Trade)"
    UI->>API: POST /api/paper-trading/orders
    API->>DB: Verify Funds & Execute Trade
    DB-->>API: Confirm Transaction
    API-->>UI: Update Portfolio & Balance
```

## 📂 Project Structure
```text
TradeAxis.com-main/
├── src/                                    # Main Next.js application
│   ├── app/                               # Next.js 14 App Router
│   │   ├── (authenticated)/              # Protected routes
│   │   │   └── dashboard/
│   │   │       └── page.tsx
│   │   ├── about/                         # About page
│   │   ├── api/                           # API routes
│   │   │   ├── ai/                        # AI endpoints
│   │   │   │   ├── chat/
│   │   │   │   │   └── route.ts
│   │   │   │   └── stream/
│   │   │   │       └── route.ts
│   │   │   ├── auth/                      # Authentication endpoints
│   │   │   │   └── forgot-password/
│   │   │   │       └── route.ts
│   │   │   └── chat/                      # Chat endpoints
│   │   │       └── expert/
│   │   │           └── route.ts
│   │   ├── chart/                         # Chart pages
│   │   │   └── [symbol]/
│   │   │       └── page.tsx
│   │   ├── compliance/                    # Compliance pages
│   │   ├── cookies/                       # Cookie policy
│   │   ├── disclaimer/                    # Disclaimer page
│   │   ├── help/                          # Help page
│   │   ├── how-it-works/                  # How it works page
│   │   ├── login/                         # Login page
│   │   ├── notifications/                 # Notifications page
│   │   ├── privacy/                       # Privacy policy
│   │   ├── privacy-policy/                # Privacy policy page
│   │   ├── profile/                       # User profile
│   │   ├── register/                      # Registration page
│   │   ├── regulatory/                    # Regulatory information
│   │   ├── security/                      # Security page
│   │   ├── security-info/                 # Security information
│   │   ├── settings/                      # Settings page
│   │   ├── status/                        # Status page
│   │   ├── terms/                         # Terms page
│   │   ├── terms-of-service/              # Terms of service
│   │   ├── icon.svg
│   │   ├── layout.tsx
│   │   └── page.tsx                       # Main landing page
│   ├── components/                        # React components
│   │   ├── contact/
│   │   │   └── ContactForm.tsx
│   │   ├── landing/
│   │   │   └── ComparisonTable.tsx
│   │   ├── layout/                        # Layout components
│   │   │   ├── Footer.tsx
│   │   │   ├── header.tsx
│   │   │   └── sidebar.tsx
│   │   └── market/                        # Market components
│   │       ├── ai-expert-chat.tsx
│   │       └── stock-detail-modal.tsx
│   └── lib/                               # Utility libraries
│       ├── services/
│       │   └── openai.ts
│       ├── auth-storage.ts
│       ├── db.ts
│       ├── email-service.ts
│       ├── email-verification-service.ts
│       ├── enhanced-memory-system.ts
│       ├── enhanced-reasoning-engine.ts
│       ├── guardrails-system.ts
│       ├── memory-system.ts
│       ├── real-time-data-system.ts
│       └── universal-knowledge-tools.ts
├── scripts/                                # Python ML and utility scripts
│   ├── advanced_ml_engine.py
│   ├── ai_predictions_engine.py
│   ├── backtest_validation.py
│   ├── backtest_validation_cli.py
│   ├── backtest_validation_framework.py
│   ├── backtest_validator.py
│   ├── cleanup-verification-codes.js
│   ├── comprehensive_us_stock_downloader.py
│   ├── custom_qlib.py
│   ├── debug_backtest.py
│   ├── enhanced_ai_predictions_engine.py
│   ├── enhanced_backtesting.py
│   ├── enhanced_backtesting_cli.py
│   ├── enhanced_backtesting_engine.py
│   ├── enhanced_backtesting_part2.py
│   ├── enhanced_qlib_data_manager.py
│   ├── ensemble_ai_predictor.py
│   ├── install-python-deps.js
│   ├── install-python-deps.sh
│   ├── ml_prediction_engine.py
│   ├── polygon_backtesting_cli.py
│   ├── polygon_backtesting_engine.py
│   ├── polygon_data_provider.py
│   ├── portfolio_optimization_engine.py
│   ├── qlib_advanced_predictor.py
│   ├── qlib_backtesting.py
│   ├── qlib_config.py
│   ├── qlib_data_manager.py
│   ├── qlib_data_reader.py
│   ├── qlib_dataset_downloader.py
│   ├── real_time_optimizer.py
│   ├── reinforcement_learning_engine.py
│   ├── security-validation.js
│   ├── send-test-email.cjs
│   ├── send-test-email.ts
│   ├── stock_screener.py
│   ├── test-market-status.js
│   ├── yfinance_api.py
│   ├── yfinance_quote.py
│   └── yfinance_search.py
├── prisma/                                 # Database schema and migrations
│   ├── migrations/
│   │   ├── 20241201000000_add_security_tables/
│   │   │   └── migration.sql
│   │   ├── 20241201000001_add_email_verification/
│   │   │   └── migration.sql
│   │   ├── 20250903034650_init/
│   │   │   └── migration.sql
│   │   └── migration_lock.toml
│   ├── dev.db
│   └── schema.prisma
├── tests/                                  # Test files
│   └── enhanced-web-search.test.ts
├── documentation/                          # Comprehensive documentation
│   ├── 01_SITE_OVERVIEW_AND_FEATURES.txt
│   ├── 02_TECHNICAL_ARCHITECTURE_AND_INFRASTRUCTURE.txt
│   ├── 03_CORE_FEATURES_AND_FUNCTIONALITY.txt
│   ├── 04_AI_AND_MACHINE_LEARNING_SYSTEMS.txt
│   ├── 05_USER_GUIDE_AND_HOW_THINGS_WORK.txt
│   ├── 06_API_REFERENCE_DOCUMENTATION.txt
│   ├── 07_DEVELOPER_SETUP_GUIDE.txt
│   ├── 08_ENVIRONMENT_VARIABLES_AND_CONFIGURATION.txt
│   └── 09_SECURITY_AND_BEST_PRACTICES.txt
├── Screener/                              # Standalone screener application
│   ├── api/
│   │   ├── routes/
│   │   │   └── auth.ts
│   │   ├── app.ts
│   │   ├── index.ts
│   │   └── server.ts
│   └── src/
│       ├── assets/
│       │   └── react.svg
│       ├── components/
│       │   ├── Empty.tsx
│       │   ├── FilterControls.tsx
│       │   └── ResultsTable.tsx
│       ├── hooks/
│       │   └── useTheme.ts
│       ├── lib/
│       │   └── utils.ts
│       ├── pages/
│       │   ├── Home.tsx
│       │   └── StockScreener.tsx
│       ├── services/
│       │   └── polygonApi.ts
│       ├── test/
│       │   └── stockScreener.test.ts
│       ├── types/
│       │   └── stock.ts
│       ├── App.tsx
│       ├── index.css
│       ├── main.tsx
│       └── vite-env.d.ts
├── market page working/                   # Market page development
│   ├── client/
│   │   └── src/
│   │       ├── components/
│   │       │   ├── ui/                    # 30+ UI components
│   │       │   ├── Header.tsx
│   │       │   ├── MarketOverview.tsx
│   │       │   ├── SearchBar.tsx
│   │       │   ├── StockCard.tsx
│   │       │   ├── StockList.tsx
│   │       │   ├── ai-expert-chat.tsx
│   │       │   ├── chart-placeholder.tsx
│   │       │   ├── error-boundary.tsx
│   │       │   ├── market-overview.tsx
│   │       │   ├── stock-ai-analysis.tsx
│   │       │   ├── stock-card.tsx
│   │       │   ├── stock-chart.tsx
│   │       │   ├── stock-detail-modal.tsx
│   │       │   ├── stock-news.tsx
│   │       │   └── stock-search.tsx
│   │       ├── hooks/
│   │       │   ├── use-mobile.tsx
│   │       │   └── use-toast.ts
│   │       ├── lib/
│   │       │   ├── api.ts
│   │       │   ├── queryClient.ts
│   │       │   └── utils.ts
│   │       ├── pages/
│   │       │   ├── not-found.tsx
│   │       │   └── stocks.tsx
│   │       ├── types/
│   │       │   └── stock.ts
│   │       ├── App.tsx
│   │       └── index.css
│   ├── server/
│   │   ├── services/
│   │   │   ├── openai.ts
│   │   │   ├── polygonApi.ts
│   │   │   ├── stockDataService.ts
│   │   │   ├── yahooFinance.ts
│   │   │   └── yahooFinanceApi.ts
│   │   ├── index.ts
│   │   ├── routes.ts
│   │   ├── storage.ts
│   │   └── vite.ts
│   └── shared/
│       └── schema.ts
├── marketpage/                             # Market page application
│   └── src/
│       ├── components/
│       │   ├── Empty.tsx
│       │   ├── LoadMoreButton.tsx
│       │   ├── SearchBox.tsx
│       │   ├── StockCard.tsx
│       │   ├── StockDashboard.tsx
│       │   ├── StockList.tsx
│       │   └── StockModal.tsx
│       ├── hooks/
│       │   └── useTheme.ts
│       ├── lib/
│       │   └── utils.ts
│       ├── pages/
│       │   └── Home.tsx
│       ├── services/
│       │   └── stockService.ts
│       ├── types/
│       │   └── stock.ts
│       ├── App.tsx
│       ├── index.css
│       ├── main.tsx
│       └── vite-env.d.ts
├── polygon_backtest_results/              # Backtesting results
│   ├── polygon_mean_reversion_*/          # Multiple mean reversion results
│   └── polygon_momentum_*/                  # Multiple momentum results
├── backtest_validation_results/             # Validation results
│   └── validation_report_*.json           # Multiple validation reports
├── backup/                                # Backup files
│   └── screener-old/
├── pages_legacy/                          # Legacy pages
│   ├── 404.tsx
│   ├── _app.js
│   └── _document.js
└── [configuration files and compliance documents]
```

## 🚀 Setup

### Prerequisites
- Node.js 18.0.0+ and npm 8.0.0+
- PostgreSQL 15+ (Local or Cloud)
- Python 3.8+ (Optional, for ML features)
- Polygon.io API Key & OpenAI API Key

### Installation Steps
1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd TradeAxis.com-main
   ```
2. **Install dependencies**
   ```bash
   npm install
   # For Python ML dependencies
   npm run install-python-deps
   ```
3. **Configure Environment Variables**
   ```bash
   cp ENV_TEMPLATE.txt .env.local
   # Fill in the required variables (Database URL, API Keys, NextAuth secret)
   ```
4. **Database Setup**
   ```bash
   npx prisma generate
   npx prisma db push
   # Or run migrations: npx prisma migrate deploy
   ```
5. **Start Development Server**
   ```bash
   npm run dev
   ```
   *Platform will be available at `http://localhost:3000`*

## 📘 Usage Guide
- **Dashboard**: Upon login, view your portfolio overview, daily top movers, and quick market status.
- **TradeAxis**: Navigate to the TradeAxis section to ask natural language questions like "What are the technical indicators saying about TSLA today?" or "Screen for tech stocks with P/E under 20 and high volume."
- **Paper Trading**: Go to Portfolio Manager to allocate virtual funds, search for stocks, and execute simulated Buy/Sell orders to test strategies.
- **Charting**: Open any stock detail page to interact with advanced Lightweight Charts, draw trendlines, and toggle technical indicators.

## 🔗 API Reference (Internal)
The platform exposes several internal REST endpoints under `/api`:
- `/api/market/*`: Real-time market status, top movers, and indices.
- `/api/stocks/[symbol]/*`: Granular stock data, quotes, and historical charts.
- `/api/ai/*`: Endpoints powering TradeAxis, streaming chat, and file analysis.
- `/api/paper-trading/*`: Order execution, account stats, and position management.
- `/api/portfolio/*`: Portfolio analytics, trades, and sector data.

## 🛠️ Troubleshooting
- **Prisma Connection Issues**: Ensure `DATABASE_URL` is correctly formatted in `.env.local` and your PostgreSQL instance is running.
- **Missing Market Data**: Check your `POLYGON_API_KEY` limit. The platform falls back to Yahoo Finance, but Polygon is highly recommended for real-time accuracy.
- **Python Script Errors**: Ensure `python3` is in your PATH and `pip install -r requirements-ml.txt` has been executed successfully.
- **NextAuth Login Fails**: Verify `NEXTAUTH_URL` and `NEXTAUTH_SECRET` are set correctly.

## 🔐 Environment Variables
Key variables required in `.env.local`:
```env
# Database
DATABASE_URL="postgresql://user:pass@localhost:5432/tradeaxis"

# Authentication
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="your-32-char-secret"
GOOGLE_CLIENT_ID="your-google-client-id"
GOOGLE_CLIENT_SECRET="your-google-client-secret"

# APIs
POLYGON_API_KEY="your-polygon-api-key"
OPENAI_API_KEY="your-openai-api-key"
```

## ☁️ Deployment
The application is optimized for deployment on **Render.com** or **Vercel**.
1. Set the Node.js version to 18.x in the hosting environment.
2. Add all environment variables to the project settings.
3. Build command: `npm run build`
4. Start command: `npm run start`
*(Ensure database migrations run during the build step or via CI/CD pipelines).*

## ⚡ Performance
- **Server-Side Rendering (SSR) & Static Site Generation (SSG)**: Utilized via Next.js App Router to deliver rapid initial page loads.
- **Caching**: Extensive use of React Query and Next.js data cache for market data to minimize API calls and prevent rate limiting.
- **Edge Runtime**: Applicable API routes use edge functions for ultra-low latency.
- **Component Lazy Loading**: Heavy charting libraries and ML visualization tools are dynamically imported.


