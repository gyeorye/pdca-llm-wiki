# 03. 폴더 구조 + 의미

## 1. Skeleton 복사

`vault-skeleton/` 안의 모든 폴더와 파일을 본인 vault 루트에 복사한다.

```bash
# 예: vault가 ~/Obsidian/MyVault 라면
cp -R vault-skeleton/* ~/Obsidian/MyVault/
cp vault-skeleton/CLAUDE.md.template ~/Obsidian/MyVault/CLAUDE.md
```

> `CLAUDE.md.template` 파일명에서 `.template` 제거 → `CLAUDE.md`로 저장. 내용은 다음 단계(04)에서 채운다.

## 2. 폴더 의미 (필수 이해)

이 vault는 **5개 최상위 폴더**로만 구성된다. 각각의 역할이 명확히 분리돼야 LLM이 헷갈리지 않음.

```
MyVault/
├── 00-inbox/         # 매일 들어오는 것 (daily, draft)
├── 10-raw/           # 원본 (read-only, immutable)
├── 20-wiki/          # LLM이 컴파일한 정제 지식
├── 30-pdca/          # 회고 (P-D-C-A 사이클)
├── 40-actions/       # 할 일 (todo 모음)
├── 50-templates/     # Templater template + LLM rule 파일
└── CLAUDE.md         # LLM agent brief
```

### `00-inbox/` — 매일 들어오는 것

| 하위 | 용도 |
|------|------|
| `daily/` | Periodic Notes가 자동 생성. `YYYY-MM/YYYY-MM-DD.md`. |
| `placeholder/` | 미완성 working draft. 완성되면 `10-raw/`로 이동. |

규칙:
- LLM은 daily에서 todo·메모 패턴 추출 가능
- placeholder는 **ingest 제외** (미완성이므로)

### `10-raw/` — 원본 (immutable)

**LLM이 절대 수정하지 않는다** (frontmatter 추가는 예외).

| 하위 (제안) | 용도 |
|-------------|------|
| `articles/` | 직접 작성한 articles/memos |
| `web-clips/` | Obsidian Web Clipper 저장 (회의록 포함) |
| `tech-notes/` | 업무 단편 학습 노트 |
| `books/` | 책 raw note + 인용 + 메모 |

용도에 맞게 하위 폴더 추가 가능 (예: `interviews/`, `personal-journal/`).

### `20-wiki/` — LLM이 컴파일한 정제 지식

**LLM이 작성·유지**. `10-raw/`를 ingest해 여기로 들어옴.

| 하위 | 용도 |
|------|------|
| `index.md` | 모든 wiki 페이지 목록 (도메인별) |
| `log.md` | LLM 작업 로그 (ingest/query 기록) |
| `work/concepts/` | 업무 관련 개념 (Team Topologies, Kafka 등) |
| `work/projects/` | 프로젝트별 정리 |
| `work/people-teams/` | 조직 구조, stakeholder |
| `work/decisions/` | ADR (Architecture Decision Records) |
| `personal/` | 개인 영역 (육아, 건강, 재정, 커리어) |
| `meta/` | 나에 대한 정리 (`about-you.md`, patterns, anti-patterns) |

규칙은 `50-templates/rules/wiki-conventions.md` 참조.

### `30-pdca/` — 회고

| 하위 | 용도 |
|------|------|
| `cycles/` | Weekly + Monthly PDCA (Periodic Notes가 생성) |
| `retrospectives/` | 분기/연간 큰 회고 |
| `active-experiments.md` | 진행 중인 실험 추적 |
| `someday-maybe.md` | 언젠가 할 일 |

### `40-actions/` — 할 일

| 하위 | 용도 |
|------|------|
| `work-todo.md` | 업무 todo 대시보드 (Tasks 쿼리) |
| `personal-todo.md` | 개인 todo 대시보드 |
| `waiting-for.md` | 남에게 위임한 항목 |

### `50-templates/` — Template + LLM rule

| 항목 | 역할 |
|------|------|
| `daily-note.md` | Periodic Notes daily template |
| `weekly-pdca.md` / `monthly-pdca.md` | 회고 template |
| `source-ingest.md` | 새 source 등록 시 |
| `decision-record.md` | ADR template |
| `meeting-note.md` | 회의록 template |
| `book-raw-template.md` | 책 raw note template (Templater 동적) |
| `rules/` | **LLM이 trigger 시 읽는 규칙 파일** |

`rules/` 안의 파일:
- `ingest.md` — "ingest this" trigger
- `wiki-conventions.md` — 20-wiki/ 작성 규칙
- `todo-rules.md` — todo 생성 규칙
- `pdca.md` — 회고 + lint 규칙
- `ingest-cases/` — 소스 경로별 추가 규칙

## 3. 핵심 원칙

| 원칙 | 의미 |
|------|------|
| **소스 분리** | `10-raw/` 원본 ↔ `20-wiki/` 정제. 원본 절대 수정 X. |
| **Trigger 기반** | LLM이 자연어 trigger ("ingest this") 보고 rule 파일 읽어 동작. |
| **Single source of truth** | `20-wiki/meta/about-you.md`가 나에 대한 단일 진입점. |
| **모순 명시** | 두 source가 충돌하면 `> ⚠️ Contradiction: A says X but B says Y` 표시. |
| **Cross-reference** | `[[wikilink]]`로 page 간 연결. Orphan 페이지는 lint로 검출. |

## 4. 폴더 만들기 후 확인

```bash
ls MyVault/
# 00-inbox  10-raw  20-wiki  30-pdca  40-actions  50-templates  CLAUDE.md
```

다음: `docs/04-claude-code-setup.md`
