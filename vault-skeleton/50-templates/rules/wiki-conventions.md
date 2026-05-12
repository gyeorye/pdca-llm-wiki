---
tags: [rule, wiki, conventions]
domain: meta
updated: 2026-05-12
---

# Wiki Page Conventions

## Frontmatter (required)

```yaml
---
tags: [concept | project | person | decision | source-summary]
domain: [work | personal | meta]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: ["10-raw/path/to/source.md"]
confidence: high | medium | low
---
```

## Content rules

- `[[wikilink]]` cross-page links
- Contradiction marker: `> ⚠️ Contradiction: [A] says X but [B] says Y`
- Korean default 권장 (변경 가능), tech term English 병기 권장 (e.g. 인지 부하(Cognitive Load))
- 페이지 self-contained (다른 페이지 안 읽어도 핵심 파악)

## Domain 분할

### work/ (20-wiki/work/)
- `concepts/` — tech concepts (Team Topologies, SLI/SLO, Kafka, gRPC 등)
- `projects/` — per-project (프로젝트별 정리)
- `people-teams/` — team structure, stakeholders
- `decisions/` — ADR format (architecture decision records)

### personal/ (20-wiki/personal/)
- 하위 폴더는 본인 도메인에 맞게 추가 (예: `health/`, `finance/`, `career/`, `parenting/`, `hobby/`)
- 폴더 추가 시 이 문서에 한 줄 추가

### meta/ (20-wiki/meta/)
- `patterns.md` — 반복 패턴·인사이트
- `anti-patterns.md` — 실패·비효율 접근
- `about-you.md` — 사용자 정체성 single source of truth
- (선택) `concepts/` — 도메인 횡단 핵심 개념
- (선택) `identity-thesis.md` — 정체성 장기 누적
- (선택) `focus-principles-YYYY.md` — 그 해의 focus principles

## 10-raw/ 폴더 의미 (소스 식별용)

기본 제안:
- `articles/` — 직접 작성 articles/memos
- `web-clips/` — Obsidian Web Clipper 저장 (회의록 포함)
- `tech-notes/` — 업무 단편 tech 학습 노트
- `books/` — 책 raw note (인용 + 메모)

사용자가 본인 필요에 따라 추가 가능 (예: `interviews/`, `personal-journal/`, `career-records/`, `external/`).
