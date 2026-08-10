# Authentication

This site and its API use the **x402 payment protocol** for authentication and access control.

## How it works

1. Call the API (`POST /v1/sentiment`).
2. The server responds with `HTTP 402 Payment Required` and a challenge in the `X-Paywall` / `WWW-Authenticate` headers, pointing at the payment manifest at `/.well-known/x402`.
3. Your wallet signs the challenge and pays **0.005 USDC** (per call) on **Base** (`eip155:8453`) or **Solana**.
4. The API returns the sentiment result. No API keys, no accounts, no subscriptions.

## Payment details

- **Protocol:** [x402](https://x402.org) (HTTP 402 micropayments)
- **Price:** 0.005 USDC per sentiment call
- **Networks:** Base (`eip155:8453`), Solana
- **Pay-to (Base):** `0x583FfEE3f6E0E8cAB3531fBd5C4e291784D3b6cD`
- **Pay-to (Solana):** `7bu8aB2w94N8TRysqbBdKXNoPqSr9UopaZXJGVSRbLgk`

## MCP server

The same sentiment engine is exposed as an MCP server:

- **Endpoint:** `https://abstain-eliminate-unison.ngrok-free.dev` (MCP over Streamable HTTP)
- **Tools:** `analyze_sentiment`, `analyze_sentiment_batch`
- **Cost:** 0.005 USDC per tool call, paid via x402

## Public resources (no payment required)

- `GET /` — homepage
- `GET /robots.txt` — crawling rules
- `GET /sitemap.xml` — sitemap
- `GET /llms.txt` — LLM-friendly site summary
- `GET /capabilities.json` — agent capabilities manifest
- `GET /.well-known/x402` — x402 payment manifest (public)
- `GET /.well-known/api-catalog` — API catalog
- `GET /.well-known/agent-card.json` — A2A agent card
- `GET /.well-known/mcp/server-card.json` — MCP server card

## Contact

- Email: dorianmike369@gmail.com
- Slack: x402 workspace (#general)
