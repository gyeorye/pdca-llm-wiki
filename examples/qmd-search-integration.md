# qmd Local Search — Setup and Daily Use

> How to wire [qmd](https://github.com/tobi/qmd) into your vault so Claude Code can search across hundreds of markdown files instantly — BM25 + vector + HyDE, all local.
>
> **Credit**: qmd is recommended by [Karpathy's original LLM Wiki gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) as the local search MCP. This doc covers the practical setup — install steps, collection scoping, and daily-use patterns.
>
> Optional. Skip until your vault crosses ~100 notes. Becomes essential past ~150.

---

## Why qmd

Claude Code reads files with `Read` and searches with `Grep`. Both are fine for small vaults. They break down when:

- You don't remember which file holds the answer
- The relevant text uses different vocabulary than your query ("performance" vs "p99 latency")
- You want to scope a search to a subset (e.g., only `20-wiki/work/`)

qmd indexes your markdown locally and exposes 3 search modes via MCP:

| Mode | What it does | When to use |
|---|---|---|
| `lex` | BM25 keyword search | Exact terms ("Kafka consumer group") |
| `vec` | Semantic vector search | Meaning-based ("how do I handle backpressure") |
| `hyde` | Hypothetical document | "What would the answer look like?" then search for that |

Run together for best recall.

---

## Install (5 minutes)

```bash
# Install qmd CLI
# See https://github.com/tobi/qmd for current install steps

# Index your vault
cd ~/Obsidian/MyVault
qmd index

# Verify
qmd status
```

Enable in Claude Code (`~/.claude/settings.json`):

```json
{
  "enabledPlugins": {
    "qmd@qmd": true
  },
  "extraKnownMarketplaces": {
    "qmd": {
      "source": {
        "source": "github",
        "repo": "tobi/qmd"
      }
    }
  }
}
```

Restart Claude Code. The agent now has `qmd__query`, `qmd__get`, `qmd__multi_get`, `qmd__status` tools.

---

## Collections (scope your searches)

Define collections in your qmd config. Gary uses two:

| Collection | What's in it | Use case |
|---|---|---|
| `vault` (~160 docs) | Everything — `00-inbox/`, `10-raw/`, `20-wiki/`, `30-pdca/`, `40-actions/` | Broad lookup |
| `20-wiki` (~40 docs) | Only the LLM-compiled wiki | Answers from canonical knowledge, not raw drafts |

Why two collections matter: the wiki is the **reviewed** version. Searching only `20-wiki/` filters out half-formed raw notes and avoids the agent quoting your inbox draft as if it were established knowledge.

---

## Triggers that use qmd

Once enabled, the agent picks it up automatically. Useful phrasings:

| You say | What the agent does |
|---|---|
| "What do I know about platform engineering?" | qmd query → reads top matches → synthesizes answer with citations |
| "Find every note where I mention Karpathy" | `lex` mode → exact term |
| "Have I written about emotional regulation in family contexts?" | `vec` mode → semantic match |
| "Show me what's in last week's daily notes" | `multi_get` with glob `00-inbox/daily/2026-05-*.md` |

The agent decides between `lex` / `vec` / `hyde` based on the question. You don't need to specify mode.

---

## Daily-use patterns

### Pattern 1 — Identity-aware Q&A

Combine qmd with `about-you.md`:

```
You: Phase 3 reading curriculum에서 내가 어떤 open question 남겼었지?

Agent: [reads about-you.md → knows Gary is in reading curriculum]
       [qmd query: "Phase 3 open questions" in collection=vault]
       → finds 10-raw/books/reading-curriculum-2026/_phase-guide.md
       → finds structure-designer-thesis.md (Phase 3 log)
       → answers with citations to both
```

Without qmd: agent needs you to point at files. With qmd: agent finds them.

### Pattern 2 — Contradiction detection

```
You: I just wrote "low-context is always better" in today's daily.
     Anywhere else in the wiki I contradicted this?

Agent: [qmd vec query: "low-context limitations" / "context dependency"]
       → finds 20-wiki/meta/about-gary.md Shadow 3 (Korean roundaboutness)
       → flags: "You also wrote that low-context is a conscious shadow
         in Korean workplace contexts."
```

This is what "wiki lint" trigger does at scale.

### Pattern 3 — Cross-domain pattern surfacing

```
You: 16-year baseball team management과 platform engineering 사이에
     공통 패턴이 뭐가 있을까?

Agent: [qmd hyde query: "long-term community stewardship platform pattern"]
       → finds notes from both domains
       → surfaces designer-owner separation (#26) as the shared pattern
```

Pattern Gary couldn't surface alone — qmd's semantic search finds the conceptual bridge.

---

## When NOT to use qmd

- Vault under 50 notes. `Grep` + `Read` is faster.
- You already know the exact file. Just `Read` it.
- Search for a current-conversation artifact. Use the conversation, not the index.

qmd costs nothing per query (it's local), but the index must be kept fresh:

```bash
# Re-index after a big ingest batch
qmd index --collection vault

# Or set up a watch process
qmd watch
```

If the index drifts, the agent will quote stale text. `qmd status` shows last-index time.

---

## Diagnostic example

```
You: qmd status
Agent: [calls qmd__status]
       → vault: 161 docs, last indexed 2026-05-12 09:14
       → 20-wiki: 38 docs, last indexed 2026-05-12 09:14
```

If "last indexed" is more than a day stale and you've been writing, re-index before trusting search results.

---

## Going further

- **Custom collections per project**: index a specific project folder as its own collection, scope searches to it during focused work
- **Combine with `wiki-conventions.md` rules**: agent uses qmd to find related pages before drafting a new wiki entry, satisfying the "cross-reference 3 related pages" rule automatically
- **`qmd` + `weekly PDCA` trigger**: agent searches the past week's daily notes via qmd, drafts the retro with citations

The kit doesn't depend on qmd. But once you have it, every other rule file gets sharper because the agent's context-retrieval improves.
