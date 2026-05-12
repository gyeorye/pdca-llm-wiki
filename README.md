# pdca-llm-wiki

> **A second-brain that maintains itself.**
> Drop-in Obsidian vault + Claude Code agent that ingests your raw notes, compiles a self-organized wiki, and runs your weekly/monthly retrospectives — so you can stop maintaining your PKM and start using it.
>
> An instantiation of [Andrej Karpathy's *LLM Wiki* pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f), with a PDCA cycle and a trigger-based rule architecture.

[한국어 README](./README.ko.md) · [Full Setup Guide](./GETTING_STARTED.md) · [License](./LICENSE)

---

## What is this?

A starter kit that gives you a fully working **LLM-maintained Personal Knowledge Management system** in under an hour:

- **Obsidian** as the vault (your notes stay local, in plain markdown)
- **Claude Code** as the agent that reads, organizes, links, and reviews
- **5 Obsidian plugins** (Tasks, Periodic Notes, Templater, Excalidraw, Web Clipper) wired up
- **A folder convention + rule files** that the agent uses to keep everything coherent

The result: you write raw notes wherever it's convenient (web clips, meeting notes, book quotes). The agent does the second pass — summarizing, cross-linking, finding contradictions, drafting weekly retros — based on rules you can read and edit.

## Why does this exist?

Most PKM systems break when life gets busy. You stop tagging. Notes pile up. The "second brain" turns into a junk drawer.

The bet here is simple: **separate the writing pass from the organizing pass**, and let an LLM agent do the second one.

| | Most PKM systems | This kit |
|---|---|---|
| **Source notes** | Mixed with summaries | Read-only, never mutated by the agent |
| **Wiki / summaries** | Manually maintained, decays fast | LLM-maintained, compiled from sources |
| **Retrospectives** | "I should journal more" | Weekly/monthly drafted by the agent, you review |
| **About-me context** | Lives in your head | One file the agent reads first, every time |
| **Triggers** | Click 8 things | `"ingest this"`, `"weekly PDCA"`, `"wiki lint"` |

It's not magic. It's discipline encoded as a folder structure and four rule files. You can read every rule the agent follows — they're plain markdown in `50-templates/rules/`.

## What you get

- **5-folder vault** (`10-raw/`, `20-wiki/`, `00-inbox/`, `30-pdca/`, `40-actions/`, `50-templates/`) with explicit semantics
- **`CLAUDE.md`** — the agent brief that loads on every Claude Code session in the vault
- **4 rule files** the agent follows for ingestion, wiki writing, todo creation, and retrospectives
- **Ready-made Templater templates** for daily / weekly / monthly notes, meeting notes, ADRs, book raw notes
- **`about-you.md` template** — a 5-stage scaffold for the single document that defines who you are to the agent
- **Plugin configs** you can drop into `.obsidian/`
- **Claude Code `settings.json` template** with optional MCP server integration
- **`examples/`** — reference walkthroughs: how one user arrived at a 27-trait identity portrait, and how to wire local semantic search via [`qmd`](https://github.com/tobi/qmd)

## Quick start (5 minutes)

```bash
# 1. Clone or download
git clone https://github.com/gyeorye/pdca-llm-wiki.git

# 2. Copy the vault skeleton into a new Obsidian vault
cp -R pdca-llm-wiki/vault-skeleton/* ~/Obsidian/MyVault/
cp pdca-llm-wiki/vault-skeleton/CLAUDE.md.template ~/Obsidian/MyVault/CLAUDE.md

# 3. Open the vault in Obsidian, install the 5 community plugins
#    (Tasks, Periodic Notes, Templater, Excalidraw, Web Clipper)

# 4. Run Claude Code from the vault
cd ~/Obsidian/MyVault && claude
```

That's the minimum. For full plugin configuration, MCP setup, and customization, follow [GETTING_STARTED.md](./GETTING_STARTED.md) (6 short guides, ~1 hour total).

## A day in the life

```
You:    "ingest this" (in a web-clipped article)
Agent:  Reads source → drafts a summary in 20-wiki/work/concepts/
        → adds entry to index.md → logs in log.md
        → cross-references three related pages

You:    "weekly PDCA"
Agent:  Reads this week's daily notes → drafts the Do/Check/Act sections
        → flags contradictions in any wiki pages you touched this week

You:    "what do I know about Kafka consumer groups?"
Agent:  Checks 20-wiki/index.md → reads the relevant page →
        answers with cross-references → offers to expand it
```

Triggers are plain English. The agent reads `CLAUDE.md` and the `rules/*.md` files to figure out what to do. You can edit those rules; the next trigger picks up the change.

## Tech stack

| Component | Role | Cost |
|---|---|---|
| [Obsidian](https://obsidian.md) | Markdown vault | Free |
| [Claude Code](https://claude.com/claude-code) | LLM agent (CLI) | API usage |
| [Tasks](https://github.com/obsidian-tasks-group/obsidian-tasks) | Todo system | Free |
| [Periodic Notes](https://github.com/liamcain/obsidian-periodic-notes) | Auto-generated daily/weekly/monthly notes | Free |
| [Templater](https://github.com/SilentVoid13/Templater) | Dynamic templates | Free |
| [Excalidraw](https://github.com/zsviczian/obsidian-excalidraw-plugin) | Diagrams | Free |
| [Obsidian Web Clipper](https://obsidian.md/clipper) | Browser extension for clipping pages | Free |
| [qmd](https://github.com/tobi/qmd) (optional) | Local search MCP server for big vaults | Free |

## Who is this for?

- You already write a lot but your notes feel like sediment
- You've tried Notion / Roam / Logseq and bounced off the maintenance overhead
- You're comfortable in a terminal and want the agent to be transparent (every rule is a markdown file you can read)
- You want your data local, in markdown, owned by you

If you want a turnkey GUI with no setup, this isn't it. If you want a system you can shape, it might be.

## Examples (reference, not prescription)

Two case-study docs in [`examples/`](./examples/):

- **[`identity-discovery-methodology.md`](./examples/identity-discovery-methodology.md)** — How Gary arrived at a 27-trait + 6-shadow `about-you.md` through ~12 iterative Claude Code sessions. The 6-step process (brain dump → layer scaffolding → external validation → shadow pass → focus distillation → update discipline) reproduces; the specific numbers don't.
- **[`qmd-search-integration.md`](./examples/qmd-search-integration.md)** — Practical setup for [`qmd`](https://github.com/tobi/qmd) (the local search MCP recommended by Karpathy's gist): install, collection scoping, daily-use patterns.

Read these once you've completed the basic setup. They show what the kit looks like after weeks of compounding, so you know what you're heading toward.

## Customization

The kit gives you scaffolding. The opinions are:

- **Korean by default** with English technical terms (Gary's preference — change in `CLAUDE.md` if you want English-only)
- **PDCA cycle** for retrospectives (swap to GTD / Bullet Journal / your own — edit `50-templates/rules/pdca.md`)
- **Work / Personal / Meta** as the top-level wiki domains (edit `50-templates/rules/wiki-conventions.md`)

Every assumption is encoded as a markdown rule file the agent reads. To change an assumption, edit the rule.

## Roadmap / Known limits

- **Setup guides are currently Korean-first**. English translation in progress.
- **No GUI installer** — you copy folders and edit files by hand. By design, but rough edges.
- **Agent loop is per-trigger** — there's no background daemon. The agent acts when you ask.
- **Web Clipper templates** for the kit's metadata fields not yet bundled.

## License

[MIT](./LICENSE) — fork it, ship it, sell it. Attribution welcome but not required.

## Lineage

This kit is an instantiation of [Andrej Karpathy's *LLM Wiki* gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — a pattern for using an LLM as the maintainer (not just the reader) of a markdown knowledge base.

Karpathy's gist deliberately stops at the pattern level: 3 layers (raw / wiki / schema), 3 operations (ingest / query / lint), and an explicit invitation to _"share it with your LLM agent and work together to instantiate a version that fits your needs."_

This repo is one such instantiation. The pieces that come from Karpathy are credited as such; everything else is opinionated implementation built on top.

**What Karpathy's gist provides** (the pattern):
- Raw / wiki / schema 3-layer architecture
- Ingest / Query / Lint operations
- `index.md` + `log.md` navigation files
- The argument for why this beats stateless RAG
- [`qmd`](https://github.com/tobi/qmd) as the recommended local search MCP

**What this kit adds** (the instantiation):
- A concrete **6-folder structure** with explicit semantics (`00-inbox`, `10-raw`, `20-wiki`, `30-pdca`, `40-actions`, `50-templates`)
- **PDCA cycle integration** — weekly/monthly retrospectives as a first-class workflow, not just periodic lint
- **`about-you.md` single entry point** — user identity as a first-class source the agent reads first, every session
- **4 rule files driving a trigger-based architecture** (`ingest.md`, `wiki-conventions.md`, `todo-rules.md`, `pdca.md`) — replacing Karpathy's single `CLAUDE.md` schema with a modular split that scales
- **Opinionated 5-plugin Obsidian stack** — Tasks, Periodic Notes, Templater, Excalidraw, Web Clipper — with config files included
- **7 Templater templates** (daily / weekly / monthly / ADR / meeting / book-raw / source-ingest)
- **Todo system convention** (`#personal` tag, dashboard queries, work/personal split)
- **Domain split** (work / personal / meta) with subdomain conventions

## Background

Built by [Gary (Gyeorye Lee)](https://www.linkedin.com/in/gyeorye) — a TPM at a Korean tech company who got tired of his second brain rotting. The original vault has been compiling Gary's reading curriculum, work notes, and retrospectives for months. This kit is the genericized version: same structure, none of Gary's content.

If you build something with it, an issue or a tag would make Gary's day.

---

## Contribute / feedback

- **Found a bug or missing piece?** Open an issue.
- **Improved a rule or template?** PRs welcome — especially translation to other languages.
- **Built something cool on top?** Tell us — we'll link it from the README.
