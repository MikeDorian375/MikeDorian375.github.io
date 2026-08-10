# Echo Sentiment API

Pay-per-call sentiment analysis and market intelligence, built on [x402](https://x402.org).
Dual-chain: Base + Solana. USDC. No API keys, no subscriptions — the payment is the authentication.

## Try it live

- Free tier: `GET https://abstain-eliminate-unison.ngrok-free.dev/v1/sample`
- Paid endpoints return `HTTP 402` with an x402 payment-required header
- OpenAPI: `https://abstain-eliminate-unison.ngrok-free.dev/openapi.json`

## Pricing

- **0.005 USDC** per sentiment call (Base `eip155:8453` or Solana)
- Paid via the x402 payment protocol — pay 0.005 USDC, receive a receipt, present it as `Authorization` header
- Pay-to (Base): `0x583FfEE3f6E0E8cAB3531fBd5C4e291784D3b6cD`
- Pay-to (Solana): `7bu8aB2w94N8TRysqbBdKXNoPqSr9UopaZXJGVSRbLgk`

## API endpoints

| Method | Path | Description |
|---|---|---|
| POST | `/v1/sentiment` | Analyze sentiment of a single text (polarity + confidence) |
| POST | `/v1/sentiment-report` | Batch sentiment analysis (0.005 USDC per item) |

## MCP server

The same sentiment engine is exposed as an MCP server over Streamable HTTP:

- Endpoint: `https://abstain-eliminate-unison.ngrok-free.dev`
- Tools: `analyze_sentiment`, `analyze_sentiment_batch`
- Cost: 0.005 USDC per tool call via x402

## Agent resources

- [llms.txt](llms.txt) — LLM-facing documentation
- [robots.txt](robots.txt) — crawl rules
- [sitemap.xml](sitemap.xml)
- [auth.md](auth.md) — agent authentication & payment
- `/.well-known/api-catalog` — API catalog (RFC 9727)
- `/.well-known/agent-card.json` — A2A agent card
- `/.well-known/mcp/server-card.json` — MCP server card

## Repos

- [echo-sentiment-mcp](https://github.com/MikeDorian375/echo-sentiment-mcp) — MCP server
- [x402-paywall-starter](https://github.com/MikeDorian375/x402-paywall-starter) — seller-side starter template
