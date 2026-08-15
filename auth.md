# Auth.md — Authentication & Access

This document describes how AI agents authenticate to and pay for this site's API.

## Summary

This site and its API use the **x402 payment protocol** for authentication and access control — no API keys, no accounts, no OAuth bearer tokens.

## How it works

1. Call the API (`POST /v1/sentiment`).
2. The server responds with `HTTP 402 Payment Required` and a challenge in the `X-Paywall` / `WWW-Authenticate` headers, pointing at the payment manifest at `/.well-known/x402`.
3. Your wallet signs the challenge and pays **0.005 USDC** (per call) on **Base** (`eip155:8453`) or **Solana**.
4. The API returns the sentiment result.

## Registration / provisioning

No account registration is required. Access is provisioned per-request via the x402 payment flow:

- **Provisioning endpoint:** the x402 challenge itself (see `/.well-known/x402`)
- **Method:** HTTP 402 challenge-response micropayment (`urn:x402:payment`)
- **Credential:** the signed payment receipt returned by the wallet; present it as the `Authorization` header on the follow-up request

## Supported methods

| Method | Description |
|---|---|
| `x402` | HTTP 402 Payment Required, 0.005 USDC per call, Base + Solana |

## Payment details

- **Protocol:** [x402](https://x402.org) (HTTP 402 micropayments)
- **Price:** 0.005 USDC per sentiment call
- **Networks:** Base (`eip155:8453`), Solana
- **Pay-to (Base):** `0x583FfEE3f6E0E8cAB3531fBd5C4e291784D3b6cD`
- **Pay-to (Solana):** `7bu8aB2w94N8TRysqbBdKXNoPqSr9UopaZXJGVSRbLgk`

## MCP server

The same sentiment engine is exposed as an MCP server:

- **Endpoint:** `https://api.6766587364.lol` (MCP over Streamable HTTP)
- **Tools:** `analyze_sentiment`, `analyze_sentiment_batch`
- **Cost:** 0.005 USDC per tool call, paid via x402

## Related discovery documents

- `/.well-known/oauth-authorization-server` — authorization server metadata (x402 flavor)
- `/.well-known/oauth-protected-resource` — protected resource metadata
- `/.well-known/x402` — payment manifest
- `/capabilities.json` — service description
- `/llms.txt` — LLM-facing documentation

## Public resources (no payment required)

- `GET /` — homepage
- `GET /llms.txt` — LLM documentation
- `GET /robots.txt` — crawl rules
