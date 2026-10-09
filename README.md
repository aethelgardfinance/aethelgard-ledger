# Aethelgard Ledger

**A double-entry, multi-entity, tamper-evident ledger for AI agents.**

Aethelgard Ledger is a local [Model Context Protocol](https://modelcontextprotocol.io) server. It gives your agent real accounting tools backed by an engine that enforces accounting rules. The agent can't talk its way past them. It is the same engine that runs the [Aethelgard](https://aethelgard.finance) desktop ledger.

> **Evaluation build, for business use only.** Licensed under the [Aethelgard Ledger Evaluation Licence](LICENSE.txt). The ledger file is **not encrypted**, and output must not be relied on without independent verification.

## What it does

- **Balanced journals or nothing.** Every posting must balance. If debits don't equal credits, the engine rejects the posting and returns the reason, so the agent can't book it.
- **Multi-entity.** Companies, trusts and individuals across 9 jurisdictions, with subsidiaries that consolidate into a parent.
- **Tamper-evident.** Every posting is linked into a per-entity SHA-256 hash-chain, so an entry edited outside the engine fails the integrity check. The chain is unkeyed. For independent assurance, record the latest chain hash (returned by `verify_integrity`) somewhere outside the ledger and compare it later.
- **Local.** The ledger lives in a file on your machine and is never sent to us.

### Tools

| Tool | What it does |
|---|---|
| `create_entity` | Create a company, trust or individual, optionally as a subsidiary of a parent |
| `create_account` | Add an account (ASSET, LIABILITY, EQUITY, REVENUE, EXPENSE) |
| `post_transaction` | Post a double-entry journal; unbalanced journals are rejected |
| `list_entities` | List entities |
| `list_accounts` | List an entity's chart of accounts |
| `list_transactions` | List postings with every journal line, filtered by date |
| `trial_balance` | Trial balance for one entity |
| `consolidate` | Consolidated trial balance for a parent and its subsidiaries |
| `verify_integrity` | Verify the hash-chain and return the latest chain hash |

## Download

Get the latest build from [Releases](https://github.com/aethelgardfinance/aethelgard-ledger/releases).

| Platform | File | Signing |
|---|---|---|
| Windows (x86_64) | `aethelgard-mcp-<version>-windows-x86_64.zip` | Signed by Aethelgard Finance Ltd |
| macOS (Intel + Apple Silicon) | `aethelgard-mcp-<version>-macos-universal.zip` | Developer ID signed and notarized by Apple |
| Linux (x86_64, static) | `aethelgard-mcp-<version>-linux-x86_64.tar.gz` | Verify with `SHA256SUMS` |

## Quick start

1. Unzip it and put `aethelgard-mcp` somewhere permanent. Check it runs: `aethelgard-mcp --version`.
2. Add it to your MCP client as a local (stdio) server.

   **Claude Code**
   ```bash
   claude mcp add aethelgard-ledger -- /full/path/to/aethelgard-mcp
   ```

   **Claude Desktop, Cursor and other clients**
   ```json
   {
     "mcpServers": {
       "aethelgard-ledger": { "command": "/full/path/to/aethelgard-mcp" }
     }
   }
   ```
   On Windows, use the path to `aethelgard-mcp.exe` with doubled backslashes, e.g. `"C:\\Tools\\aethelgard-mcp.exe"`.

3. Ask your agent to keep some books. For example:
   *"Create PropCo Ltd (GBP, GB, UkLtd) with a bank and a rental income account, then post October's £1,500 rent."*

### Where the ledger is kept

| Platform | Default location |
|---|---|
| Windows | `%APPDATA%\Aethelgard Ledger` |
| macOS | `~/Library/Application Support/Aethelgard Ledger` |
| Linux | `~/.local/share/aethelgard-ledger` |

To keep it somewhere else, use `--vault <DIR>` or set `AETHELGARD_LEDGER_VAULT`. Use `--ephemeral` for a throwaway ledger that is deleted when the server stops. Run `aethelgard-mcp --help` for every option.

## Your data

The server runs on your machine and does not send your ledger to us. There is no telemetry. **Your MCP client and the AI model you connect see whatever the tools return**, such as balances and transactions, under that provider's terms. Choose them accordingly.

## Licence

[Aethelgard Ledger Evaluation Licence](LICENSE.txt), which covers free evaluation and internal pilots for business use. Open-source components are listed with their licences in `THIRD-PARTY-NOTICES.txt` inside each download. Production or commercial use needs a separate licence.

This repository contains documentation and releases only. The software is closed source.

## Contact

Feedback, bugs and commercial licensing: **contact@aethelgard.finance**. Bug reports are welcome as [issues](https://github.com/aethelgardfinance/aethelgard-ledger/issues).

© 2026 Aethelgard Finance Ltd, registered in England and Wales (Company No. 17173295).
