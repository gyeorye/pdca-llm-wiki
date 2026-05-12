# pdca-llm-wiki

> **스스로 정리하는 두 번째 뇌.**
> Obsidian vault + Claude Code agent가 raw 노트를 ingest하고, wiki를 컴파일하고, weekly/monthly 회고를 대신 써준다. PKM을 유지하는 게 아니라 PKM을 쓰는 데 시간을 쓸 수 있도록.
>
> [Andrej Karpathy의 *LLM Wiki* 패턴](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)의 instantiation. PDCA 사이클 + trigger 기반 rule 아키텍처 추가.

[English README](./README.md) · [전체 셋업 가이드](./GETTING_STARTED.md) · [License](./LICENSE)

---

## 이게 뭔가?

1시간 안에 동작하는 **LLM이 유지·관리하는 PKM 시스템**을 만들어주는 starter kit:

- **Obsidian** vault (모든 노트는 로컬에 plain markdown으로)
- **Claude Code** agent가 읽고·정리하고·연결하고·검토
- **5개 Obsidian plugin** (Tasks, Periodic Notes, Templater, Excalidraw, Web Clipper) 사전 셋업
- **폴더 컨벤션 + rule 파일** 기반으로 agent가 일관되게 동작

결과: 편한 곳(web clip, 회의록, 책 인용)에 raw 노트 자유롭게 작성. Agent가 2차 패스로 요약·cross-link·모순 감지·주간 회고 draft를 진행. 모든 규칙은 markdown 파일로 노출돼있어 본인이 읽고 고칠 수 있음.

## 왜 만들었나?

대부분의 PKM은 바빠지면 무너진다. 태깅 멈춤. 노트 누적. 두 번째 뇌가 잡동사니 서랍이 됨.

이 kit의 가설: **작성 패스와 정리 패스를 분리**하고, 정리 패스를 LLM agent에게 위임한다.

| | 보통의 PKM | 이 kit |
|---|---|---|
| **소스 노트** | 요약과 섞임 | Read-only, agent가 절대 수정 X |
| **Wiki / 요약** | 수동 유지, 빠르게 쇠퇴 | LLM이 유지, 소스에서 컴파일 |
| **회고** | "더 자주 적어야지" | Weekly/monthly agent가 draft, 본인은 검토 |
| **나에 대한 컨텍스트** | 머릿속에만 | 한 파일에 single source, agent가 매번 먼저 읽음 |
| **Trigger** | 클릭 8번 | `"ingest this"`, `"weekly PDCA"`, `"wiki lint"` |

마법 아님. 폴더 구조 + 4개 rule 파일로 인코딩된 규율. Agent가 따르는 모든 규칙은 `50-templates/rules/`에 plain markdown으로 노출.

## 무엇이 들어있나

- **5-폴더 vault 구조** (`10-raw/`, `20-wiki/`, `00-inbox/`, `30-pdca/`, `40-actions/`, `50-templates/`) — 각 폴더 의미 명확히 분리
- **`CLAUDE.md`** — vault에서 Claude Code 시작할 때 항상 로드되는 agent brief
- **4개 rule 파일** — ingest / wiki 작성 / todo 생성 / 회고 절차
- **Templater template** — daily / weekly / monthly / 회의록 / ADR / 책 raw note
- **`about-you.md` template** — agent가 가장 먼저 읽는 "나"에 대한 single source. 5단계 작성 scaffold 포함
- **Plugin 설정 JSON** — `.obsidian/`에 그대로 복사 가능
- **Claude Code `settings.json` template** — 선택적 MCP server 통합
- **`examples/`** — reference walkthrough. 27 trait + 6 shadow identity portrait 도달 과정, [`qmd`](https://github.com/tobi/qmd) local 검색 셋업

## Quick start (5분)

```bash
# 1. Clone or download
git clone https://github.com/gyeorye/pdca-llm-wiki.git

# 2. Vault skeleton을 새 Obsidian vault에 복사
cp -R pdca-llm-wiki/vault-skeleton/* ~/Obsidian/MyVault/
cp pdca-llm-wiki/vault-skeleton/CLAUDE.md.template ~/Obsidian/MyVault/CLAUDE.md

# 3. Obsidian에서 vault 열고, 5개 community plugin 설치
#    (Tasks, Periodic Notes, Templater, Excalidraw, Web Clipper)

# 4. Vault에서 Claude Code 실행
cd ~/Obsidian/MyVault && claude
```

최소 셋업. Plugin 설정·MCP·커스터마이제이션은 [GETTING_STARTED.md](./GETTING_STARTED.md) 참조 (6개 짧은 가이드, 합쳐서 1시간).

## 하루 사용 예시

```
사용자:  "ingest this" (web-clip 기사에서)
Agent:  소스 읽고 → 20-wiki/work/concepts/에 요약 draft
        → index.md에 항목 추가 → log.md에 기록
        → 관련 3개 페이지 cross-reference

사용자:  "weekly PDCA"
Agent:  이번 주 daily 노트 읽고 → Do/Check/Act draft
        → 이번 주 변경된 wiki 페이지의 모순·누락 link flag

사용자:  "Kafka consumer group에 대해 내가 정리해둔 거 있나?"
Agent:  20-wiki/index.md 확인 → 관련 페이지 읽고 →
        cross-reference와 함께 답변 → 확장 제안
```

Trigger는 자연어. Agent가 `CLAUDE.md`와 `rules/*.md` 파일을 읽어 동작 결정. Rule 수정하면 다음 trigger부터 반영.

## Tech stack

| Component | Role | Cost |
|---|---|---|
| [Obsidian](https://obsidian.md) | Markdown vault | Free |
| [Claude Code](https://claude.com/claude-code) | LLM agent (CLI) | API 사용량 |
| [Tasks](https://github.com/obsidian-tasks-group/obsidian-tasks) | Todo 시스템 | Free |
| [Periodic Notes](https://github.com/liamcain/obsidian-periodic-notes) | Daily/weekly/monthly 자동 생성 | Free |
| [Templater](https://github.com/SilentVoid13/Templater) | 동적 template | Free |
| [Excalidraw](https://github.com/zsviczian/obsidian-excalidraw-plugin) | 다이어그램 | Free |
| [Obsidian Web Clipper](https://obsidian.md/clipper) | 웹 페이지 클리핑 (브라우저 확장) | Free |
| [qmd](https://github.com/tobi/qmd) (선택) | 큰 vault용 로컬 검색 MCP | Free |

## 누구에게 맞나

- 이미 많이 쓰는데 노트가 퇴적물처럼 쌓이는 사람
- Notion / Roam / Logseq 써봤는데 유지보수 부담에 튕긴 사람
- 터미널이 익숙하고, agent가 따르는 모든 규칙이 markdown으로 노출되는 투명성을 원하는 사람
- 데이터는 로컬에 markdown으로, 본인 소유로 두고 싶은 사람

GUI 통한 turnkey 설치가 필요하면 이 kit은 아님. 본인이 형태를 빚어가고 싶으면 맞을 수 있음.

## Examples (참고용, 따라할 template 아님)

[`examples/`](./examples/) 폴더 2개 case-study:

- **[`identity-discovery-methodology.md`](./examples/identity-discovery-methodology.md)** — Gary가 27 trait + 6 shadow `about-you.md`에 도달한 과정. ~12회 Claude Code 세션, 6-step 절차 (brain dump → layer 분류 → 외부 검증 → shadow pass → focus 3 추출 → 업데이트 규율). 절차는 재현 가능, 27이라는 숫자는 본인은 다를 것.
- **[`qmd-search-integration.md`](./examples/qmd-search-integration.md)** — [`qmd`](https://github.com/tobi/qmd) (Karpathy gist가 권장하는 local 검색 MCP) 실용 셋업: 설치, collection 분리, 일상 사용 패턴.

기본 셋업 완료 후 읽기 권장. 몇 주 누적된 후 결과물 모습이 어떤지 미리 보는 용도.

## 커스터마이제이션

기본 가정:
- **한국어 default + 기술 용어 영어 병기** (CLAUDE.md에서 변경 가능)
- **PDCA 사이클** 기반 회고 (GTD / Bullet Journal 등으로 교체 가능 — `50-templates/rules/pdca.md` 수정)
- **Work / Personal / Meta** wiki domain 분할 (`50-templates/rules/wiki-conventions.md` 수정)

모든 가정은 agent가 읽는 markdown rule 파일로 인코딩돼 있음. 바꾸려면 rule 파일을 수정.

## Roadmap / 현재 한계

- **셋업 가이드 한국어 우선** — 영문 번역 진행 중
- **GUI 인스톨러 없음** — 폴더 복사 + 파일 편집 수동. 의도된 단순함이지만 거친 부분 있음
- **Agent loop은 trigger 단위** — 백그라운드 데몬 없음. 본인이 trigger해야 동작
- **Web Clipper template** — kit metadata 필드용 클리퍼 템플릿 아직 미포함

## License

[MIT](./LICENSE) — fork·수정·재배포·상용화 자유. 출처 표기 환영 (필수 아님).

## Lineage

이 kit은 [Andrej Karpathy의 *LLM Wiki* gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)의 instantiation. LLM을 markdown 지식 베이스의 **maintainer**(단순 reader가 아니라)로 쓰는 패턴.

Karpathy의 gist는 의도적으로 패턴 수준에서 멈춤: 3-layer (raw / wiki / schema), 3-operation (ingest / query / lint), 그리고 명시적 권유 — _"share it with your LLM agent and work together to instantiate a version that fits your needs."_

이 repo는 그 instantiation 중 하나. Karpathy에서 온 것은 명시 attribution, 나머지는 그 위에 쌓은 opinionated 구현.

**Karpathy gist가 제공하는 것** (패턴):
- Raw / wiki / schema 3-layer 아키텍처
- Ingest / Query / Lint operation
- `index.md` + `log.md` 네비게이션 파일
- Stateless RAG 대비 우위 논거
- [`qmd`](https://github.com/tobi/qmd) — local 검색 MCP 권장

**이 kit이 추가하는 것** (구현):
- **6-폴더 명시 구조** + 각 의미 (`00-inbox`, `10-raw`, `20-wiki`, `30-pdca`, `40-actions`, `50-templates`)
- **PDCA 사이클 통합** — weekly/monthly 회고를 first-class workflow로 (단순 periodic lint 아님)
- **`about-you.md` single entry point** — 사용자 정체성을 agent가 매 세션 먼저 읽는 first-class source로
- **4개 rule 파일 trigger 아키텍처** (`ingest.md`, `wiki-conventions.md`, `todo-rules.md`, `pdca.md`) — Karpathy의 단일 `CLAUDE.md` schema를 modular split으로 확장
- **Opinionated 5-plugin Obsidian stack** — Tasks, Periodic Notes, Templater, Excalidraw, Web Clipper — 설정 파일 포함
- **Templater template 7종** (daily / weekly / monthly / ADR / meeting / book-raw / source-ingest)
- **Todo 시스템 컨벤션** (`#personal` tag, dashboard query, work/personal 분리)
- **Domain split** (work / personal / meta) + 하위 도메인 컨벤션

## 배경

[Gary (이겨레)](https://www.linkedin.com/in/gyeorye) 제작 — 한국 IT 회사 TPM. 본인의 두 번째 뇌가 썩어가는 게 지겨워서 만듦. 원본 vault는 reading curriculum, 업무 노트, 회고를 수개월간 컴파일 중. 이 kit은 동일 구조에서 Gary 개인 컨텍스트를 제거한 버전.

뭔가 만들어 보면 issue나 멘션 환영.

---

## Contribute / 피드백

- **버그·누락 발견**: issue 등록
- **Rule·template 개선**: PR 환영 (특히 다른 언어로 번역)
- **확장 빌드**: 알려주면 README에 link
