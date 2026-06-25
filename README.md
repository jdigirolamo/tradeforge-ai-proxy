# TradeForge AI Proxy

A serverless AI proxy layer built on **Cloudflare Workers** with **D1** (SQLite at the edge). Routes, logs, and manages AI model API calls for the TradeForge platform — a CRM and automation suite built for Alberta's trades industry.

## What It Does

- Proxies requests to AI model APIs (Claude, OpenAI) through a secure Cloudflare Worker
- - Logs all AI interactions to a persistent D1 (SQLite) database at the edge
  - - Provides a lightweight API layer between the TradeForge frontend and external AI providers
    - - Enables rate limiting, request logging, and API key management without exposing credentials to the client
     
      - ## Tech Stack
     
      - | Layer | Technology |
      - |---|---|
      - | Edge Runtime | Cloudflare Workers |
      - | Database | Cloudflare D1 (SQLite) |
      - | Language | TypeScript |
      - | Config | Wrangler (wrangler.json) |
      - | ORM / Query | Prepared Statements via D1 binding |
     
      - ## Project Structure
     
      - ```
        tradeforge-ai-proxy/
        ├── src/
        │   ├── index.ts          # Worker entry point — handles all incoming requests
        │   └── renderHtml.ts     # HTML response renderer for debug/status views
        ├── migrations/           # D1 database schema migrations
        ├── wrangler.json         # Cloudflare Worker + D1 binding config
        ├── tsconfig.json         # TypeScript config
        └── package.json
        ```

        ## Setup

        ### Prerequisites
        - Node.js 18+
        - - Cloudflare account with Workers enabled
          - - Wrangler CLI: `npm install -g wrangler`
           
            - ### Local Development
           
            - ```bash
              npm install
              npx wrangler dev
              ```

              ### D1 Database Setup

              ```bash
              # Create the D1 database
              npx wrangler d1 create tradeforge-proxy-db

              # Update database_id in wrangler.json with the output ID

              # Run migrations
              npx wrangler d1 migrations apply --remote tradeforge-proxy-db
              ```

              ### Deploy

              ```bash
              npx wrangler deploy
              ```

              ## Environment Variables

              Set these as Cloudflare Worker secrets:

              ```bash
              npx wrangler secret put OPENAI_API_KEY
              npx wrangler secret put ANTHROPIC_API_KEY
              ```

              ## Part of the TradeForge Platform

              This Worker is one component of the **TradeForge** system — a full-stack AI-powered CRM built for HVAC, plumbing, electrical, and general contracting businesses in Calgary and Alberta.

              Related systems:
              - **TradeForge CRM** — lead tracking, SMS follow-up, job pipeline
              - - **AI Receptionist** — missed call → SMS automation via n8n + Claude API
                - - **Cloudflare Pages frontend** — React/TypeScript dashboard
                 
                  - ## License
                 
                  - MIT
                  - 
