# Swiss Whale Intelligence MCP

> Methodology-transparent on-chain forensics for Bitcoin and Ethereum, exposed via the [Model Context Protocol](https://modelcontextprotocol.io/) (MCP). Real-time whale alerts, per-address MVRV, Meiklejohn-canonical clusters, mining-pool attribution, OFAC SDN sanctions tagging. **30 tools**, anonymous OAuth 2.1 Free tier.

🌐 **Live server**: https://mcp.btcwhalealerts.com/mcp
📘 **Documentation + landing page**: https://btcwhalealerts.com/mcp/
📜 **Methodology whitepaper** (CC-BY-4.0, SHA256-pinned): https://btcwhalealerts.com/whitepaper/v1.md
✅ **Status**: Production. [Listed in the official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=swiss-whale) as `io.github.alpineflow-io/swiss-whale-intelligence`.

[![smithery badge](https://smithery.ai/badge/avk359/swiss-whale-intelligence)](https://smithery.ai/servers/avk359/swiss-whale-intelligence)
[![MCP Registry](https://img.shields.io/badge/MCP_Registry-active-brightgreen)](https://registry.modelcontextprotocol.io/v0/servers?search=swiss-whale)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains the **public metadata** for the Swiss Whale Intelligence MCP server: documentation, install instructions, tool inventory, and methodology references. The server itself is hosted at `mcp.btcwhalealerts.com` — no clone, no install, no Docker required to use it.

---

## What it does

Connect any [MCP client](https://modelcontextprotocol.io/clients) (Claude Desktop, Claude Code, Cursor, ChatGPT plugins, custom agents) to a 4.7-million-transaction on-chain dataset for Bitcoin and Ethereum.

**The server answers questions like**:

- *"Show me Bitcoin whale transactions over 1,000 BTC in the last 6 hours."*
- *"What's the MVRV state of address `bc1q...`? Is it in profit or loss?"*
- *"List the addresses that share a Meiklejohn cluster with this one."*
- *"Which mining pool extracted the most blocks last week?"*
- *"Compare BTC's risk-adjusted return vs SPY and Gold over the last quarter."*
- *"Which dormant wallets just woke up after being inactive for 5+ years?"*
- *"Is this address on the OFAC SDN list?"*

Returns are first-party data only — no vendor labels, no AI-generated summaries presented as facts.

---

## Install

### Direct (recommended)

In Claude Code:

```bash
claude mcp add btc-whale-intelligence https://mcp.btcwhalealerts.com/mcp
```

In Claude Desktop, add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "btc-whale-intelligence": {
      "url": "https://mcp.btcwhalealerts.com/mcp"
    }
  }
}
```

In Cursor (Settings → MCP → Add Server):
```
URL: https://mcp.btcwhalealerts.com/mcp
```

OAuth 2.1 with anonymous Free tier — your client is auto-granted Free-tier access on first connect, no signup, no API key to copy-paste. Upgrade flow is in-product if you want paid-tier access.

### Via Smithery Gateway (alternative)

If your MCP client has trouble with OAuth discovery or you want Smithery's built-in observability:

```bash
claude mcp add btc-whale-intelligence https://swiss-whale-intelligence.run.tools
```

Smithery's gateway proxies the connection and handles OAuth on behalf of the client. Slightly more latency, but smoother for some setups.

---

## Tools (30)

24 free + 6 paid. Free-tier covers the everyday "what just happened on-chain?" questions.

### Bitcoin (21 tools)

| Tool | Free? | Description |
|---|---|---|
| `whale_my_status` | ✅ | Show authenticated user's tier and capabilities |
| `whale_recent` | ✅ | Recent BTC whale transactions (filterable by min_btc, flow_type, hours) |
| `whale_top_holders` | ✅ | Top BTC holders by current balance |
| `whale_top_coins` | ✅ | Top crypto coins by market cap with current prices |
| `whale_lookup` | ✅ | Lookup BTC address details (balance, history, cluster) |
| `whale_lookup_any` | 💎 | Universal address lookup (any chain) — Pro tier |
| `whale_tx_detail` | ✅ | Detailed BTC transaction analysis with cluster + flow context |
| `whale_address_cluster` | ✅ | Get Meiklejohn cluster for a BTC address |
| `whale_address_mvrv` | ✅ | MVRV per BTC address (profit/loss state) |
| `whale_cohort_breakdown` | ✅ | BTC whale activity by holder-size cohort |
| `whale_exchange_flows` | ✅ | Exchange inflows/outflows over a time window |
| `whale_frequency_context` | ✅ | How rare is this whale activity vs historical baseline |
| `whale_btc_price` | ✅ | Current BTC price + 24h change |
| `whale_btc_indicators` | ✅ | BTC indicators (Pi Cycle Top, Stock-to-Flow, dominance) |
| `whale_fear_greed` | ✅ | Crypto Fear & Greed Index (alternative.me) |
| `whale_dominance` | ✅ | BTC + ETH market dominance |
| `whale_dormant_wakeups` | ✅ | Recently-awakened dormant whale addresses |
| `whale_hodl_wave` | ✅ | UTXO age distribution (HODL waves) |
| `whale_sopr` | ✅ | Spent Output Profit Ratio for whale cohort |
| `whale_miner_balances` | ✅ | Mining pool balance snapshots |
| `whale_entity_search` | ✅ | Search known entities (exchanges, OFAC, mining pools) |

### Ethereum (5 tools)

| Tool | Free? | Description |
|---|---|---|
| `whale_eth_recent` | ✅ | Recent ETH whale transactions |
| `whale_eth_cohort_breakdown` | ✅ | ETH whale activity by holder-size cohort |
| `whale_eth_address_cluster` | ✅ | Get hybrid L1+L3 cluster for an ETH address |
| `whale_eth_cluster_members` | ✅ | List all members of an ETH cluster |
| `whale_eth_mvrv` | ✅ | MVRV per ETH address (3-tier doctrine) |

### Benchmarks + Pro tools (4)

| Tool | Free? | Description |
|---|---|---|
| `whale_benchmark_compare` | ✅ | Compare BTC strategies vs SPY / Gold (Alpha/Beta/Sharpe/MaxDD) |
| `whale_benchmark_prices` | ✅ | Historical benchmark prices (BTC/SPY/Gold) |
| `whale_address_history` | 💎 | Full address transaction history — Pro tier |
| `whale_export_csv` | 💎 | CSV export with backfill — Pro tier |

---

## Why this exists

Most on-chain data services either (a) charge enterprise prices for everything ($799+/mo Glassnode Professional) or (b) sell convenient summaries without showing how they were computed. We do neither.

**Three concrete differentiators**:

1. **Methodology-transparent**. Every metric the server returns is reproducible from documented heuristics. The published whitepaper (CC-BY-4.0, SHA256-pinned) covers cluster computation (Meiklejohn 2013 + ETH hybrid L1+L3), MVRV (UTXO-age × historical price), and mining-pool attribution (coinbase-tag matching, 99.6% YTD coverage). Limitations — CoinJoin, PayJoin, pre-2014 data — are explicit, not hidden.

2. **First-party data only**. No vendor labels we couldn't ourselves verify. The label sources are public and citable (OFAC SDN, Etherscan public labels, MyEtherWallet darklist, Scamsniffer). A separate `entity_label_imports` audit table tracks every label-source run.

3. **Free tier means free**. Anonymous OAuth 2.1, 24 of 30 tools accessible without signup. The 6 paid tools are historical-export and full-address-history — the things that would cost us bandwidth at scale.

---

## Verification

Three external audit reports, all green:

| Report | Phases | Result |
|---|---|---|
| Production audit | 30 tools tested anonymously | 24 PASS / 1 latency-WARN / 5 INFO / **0 FAIL** |
| Deep audit | A (doc-vs-reality) + B (chains) + C (inner-consistency) | 47 PASS / **0 FAIL** |
| External cross-check | D (vs mempool.space + Etherscan + CoinGecko + alternative.me) + E (internal source freshness) | 23 PASS / **0 FAIL** |

Reports available on request — happy to share with reviewers, partners, or anyone evaluating the server's reliability.

---

## Pricing

| Tier | Price | Access |
|---|---|---|
| Free | 0 | Anonymous OAuth, 24 tools, 10 API calls/day |
| Trial 30d | 0 | Login required, full access for 30 days, no auto-renewal |
| Intelligence | 49 CHF/mo | Realtime dashboard, custom tickers, 100 lookups/day, 10K API/day, personal license |
| Pro | 149 CHF/mo | REST API 100k/mo, 60/min, 3 seats, business license, full address-history, MCP/Claude-native |
| Academic | 0 | Verified `.edu` / `.ac.*` / `.uni-*` domains, 12-month renewal, citation required |
| Enterprise | Custom | Unlimited seats, white-label possible — [contact form](https://btcwhalealerts.com/) |

Excludes 8.1% Swiss VAT for CH residents.

---

## License

This repository (README and any docs/examples) is published under the [MIT License](LICENSE). Anyone is free to fork, adapt, or redistribute the documentation.

The MCP server source code is **not** in this repository — it runs as a hosted service operated by [Catering & Event Services GmbH](https://btcwhalealerts.com/imprint/) from Switzerland. The methodology whitepaper at https://btcwhalealerts.com/whitepaper/v1.md is published under CC-BY-4.0 and is freely citable in academic work.

---

## Links

- **Live MCP server**: https://mcp.btcwhalealerts.com/mcp
- **Landing + onboarding**: https://btcwhalealerts.com/mcp/
- **OAuth discovery**: https://mcp.btcwhalealerts.com/.well-known/oauth-authorization-server
- **OpenAPI spec**: https://api.btcwhalealerts.com/openapi.json
- **Methodology whitepaper**: https://btcwhalealerts.com/whitepaper/v1.md
- **Public ledger** (transparency): https://btcwhalealerts.com/ledger/
- **Status page**: https://mcp.btcwhalealerts.com/.well-known/oauth-authorization-server
- **Imprint + privacy**: https://btcwhalealerts.com/imprint/

---

## About alpineflow-io

[alpineflow-io](https://github.com/alpineflow-io) is the engineering identity behind Swiss Whale Intelligence and related on-chain tooling. Built and operated independently from Switzerland.
