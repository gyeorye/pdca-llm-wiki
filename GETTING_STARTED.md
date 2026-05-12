# Getting Started — Full Setup Guide

> 6 guides, ~1 hour total. Currently Korean-first; English translation in progress.
> 6개 가이드, 약 1시간 소요. 한국어 우선 작성, 영문 번역 진행 중.

## 사전 요구사항 / Prerequisites

| Item | Purpose | Cost |
|------|---------|------|
| **Obsidian** | Vault 본체 / Vault | Free |
| **Claude Code (CLI)** | LLM agent | API usage |
| **iCloud / Obsidian Sync** (선택 / optional) | Multi-device sync | iCloud free / Sync $5/mo |
| **Obsidian Web Clipper** (브라우저 확장 / browser extension) | Web clipping | Free |

## 셋업 순서 / Setup order

| 단계 / Step | 가이드 / Guide | 무엇을 한다 / What you do |
|------------|---------------|---------------------------|
| 1 | [`docs/01-obsidian-setup.md`](./docs/01-obsidian-setup.md) | Install Obsidian, create vault, install 5 plugins |
| 2 | [`docs/02-plugin-config.md`](./docs/02-plugin-config.md) | Configure Tasks / Periodic Notes / Templater / Excalidraw / Web Clipper |
| 3 | [`docs/03-folder-structure.md`](./docs/03-folder-structure.md) | Copy `vault-skeleton/` into vault; learn folder semantics |
| 4 | [`docs/04-claude-code-setup.md`](./docs/04-claude-code-setup.md) | Install Claude Code, copy `CLAUDE.md`, optional MCP setup |
| 5 | [`docs/05-daily-workflow.md`](./docs/05-daily-workflow.md) | Learn daily / weekly / monthly usage scenarios |
| 6 | [`docs/06-customization.md`](./docs/06-customization.md) | Fill `about-you.md` with your context |

## Repository layout

```
pdca-llm-wiki/
├── README.md                    # English marketing intro
├── README.ko.md                 # Korean marketing intro
├── GETTING_STARTED.md           # This file
├── LICENSE                      # MIT
├── docs/                        # 6 setup guides (Korean)
├── examples/                    # Reference walkthroughs (identity methodology, qmd setup)
├── vault-skeleton/              # Drop into your Obsidian vault
│   ├── CLAUDE.md.template       # Generic agent brief
│   ├── 00-inbox/                # Daily notes, drafts
│   ├── 10-raw/                  # Source material (read-only)
│   ├── 20-wiki/                 # LLM-compiled knowledge
│   ├── 30-pdca/                 # Retrospectives
│   ├── 40-actions/              # Todos
│   └── 50-templates/            # Templater templates + LLM rule files
│       └── rules/               # ingest.md, wiki-conventions.md, todo-rules.md, pdca.md
├── obsidian-config/             # Plugin config files (reference)
└── claude-code-config/          # Claude Code settings template
```

## What's a "trigger"?

A natural-language phrase that makes the agent read a specific rule file and follow it. Examples:

| Trigger | Rule file the agent reads | What happens |
|---------|---------------------------|--------------|
| `"ingest this"` | `50-templates/rules/ingest.md` | Source → wiki summary + index update |
| `"weekly PDCA"` | `50-templates/rules/pdca.md` | Daily notes → weekly retro draft |
| `"monthly PDCA"` | `50-templates/rules/pdca.md` | 4 weeklies → monthly retro + full lint |
| `"wiki lint"` | `50-templates/rules/pdca.md` (lint section) | Contradictions, orphans, stale pages |
| (no trigger — implicit) | `50-templates/rules/wiki-conventions.md` | Whenever agent writes to `20-wiki/` |
| (no trigger — implicit) | `50-templates/rules/todo-rules.md` | Whenever agent creates a todo |

You can edit any rule file. The next trigger picks up your change.

## After the basic setup

Read [`examples/`](./examples/) when you want to see how the scaffolding fills out in practice:

- [`examples/identity-discovery-methodology.md`](./examples/identity-discovery-methodology.md) — 6-step process for arriving at your own `about-you.md`
- [`examples/qmd-search-integration.md`](./examples/qmd-search-integration.md) — local semantic search via MCP (recommended once the vault crosses ~100 notes)

## Next

Start with [`docs/01-obsidian-setup.md`](./docs/01-obsidian-setup.md).
