# 04. Claude Code 설치 + 연동

## 1. Claude Code 설치

```bash
# macOS / Linux
curl -fsSL https://claude.ai/install.sh | bash

# 또는 npm
npm install -g @anthropic-ai/claude-code
```

상세: https://docs.claude.com/claude-code

설치 확인:
```bash
claude --version
```

## 2. Anthropic API key 설정

```bash
claude login
```

→ 브라우저에서 Anthropic 계정 로그인.

## 3. CLAUDE.md 배치

이미 `docs/03-folder-structure.md`에서 `CLAUDE.md.template` → `CLAUDE.md`로 복사했음.

위치 확인:
```
MyVault/
└── CLAUDE.md     # vault 루트에 위치
```

이 파일은 **Claude Code가 vault에서 시작할 때 항상 읽는 agent brief**. 이 starter kit에서 가장 중요한 파일.

내용은 이미 일반화돼 있음. 다음만 본인에 맞게 수정:

| 수정 항목 | 위치 |
|-----------|------|
| `about-gary.md` 같은 이름 → `about-you.md` | "Context entry" 섹션 |
| Active projects 예시 → 본인 진행 프로젝트 | "Active projects" 섹션 |
| Manually managed 목록 → 본인이 직접 관리하고 싶은 항목 | "Manually managed" 섹션 |

> 일단 그대로 두고 사용하면서 점진적으로 본인 vault에 맞게 조정해도 OK.

## 4. Vault에서 Claude Code 실행

```bash
cd ~/Obsidian/MyVault  # 본인 vault 경로
claude
```

→ Claude Code가 시작되며 `CLAUDE.md`를 자동 로드. 첫 메시지로 "안녕"이라고 보내 확인.

## 5. (선택) MCP server: qmd

`qmd`는 vault 안 markdown을 검색용 인덱스로 만드는 MCP server. 큰 vault에서 "X 관련 노트 찾아줘" 같은 쿼리에 유용.

설치:
- GitHub: https://github.com/tobi/qmd
- Claude Code에서 `/plugin install qmd` 또는 직접 MCP config 추가

```json
// ~/.claude/settings.json 의 mcpServers 또는 plugin marketplace
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

샘플 전체 설정은 `claude-code-config/settings.json.template` 참조.

> 처음엔 qmd 없이 사용해도 OK. 노트 100개 넘어가면 도입 고려.

## 6. 동작 확인 — 첫 trigger

vault 안에서 Claude Code 실행 후 자연어로 trigger:

### Test 1: 일반 질문
```
나에 대해 알려줘
```

→ Claude가 `CLAUDE.md` 읽고 `20-wiki/meta/about-you.md` 찾아서 답할 것. (`about-you.md`가 아직 비어있다면 "파일이 비어있어요" 같은 응답)

### Test 2: Ingest
`10-raw/articles/test.md` 만들고 아무 내용 채운 뒤:
```
10-raw/articles/test.md 파일 ingest해줘
```

→ Claude가 `50-templates/rules/ingest.md` 읽고, 절차대로 `20-wiki/`에 요약 생성 + `index.md`·`log.md` 업데이트.

### Test 3: Todo 생성
```
"내일 운동하기" 개인 todo로 추가해줘
```

→ `50-templates/rules/todo-rules.md` 읽고 `#personal` tag + `📅` due date 형식으로 daily/personal-todo에 등록.

## 7. 자주 쓰는 trigger 모음

| Trigger 문구 | LLM 동작 |
|--------------|---------|
| "X 파일 ingest해줘" | `rules/ingest.md` 절차 적용, `20-wiki/`에 정리 |
| "weekly PDCA 써줘" | 이번 주 daily 종합 → `30-pdca/cycles/` draft 생성 |
| "monthly PDCA 써줘" | 4주 weekly 종합 + full lint |
| "wiki lint" | 모순/orphan/오래된 page 점검 |
| "X에 대해 알고 있는 거?" | `index.md`로 관련 페이지 찾아 답변 |
| "이번 주 todo 정리" | daily에서 todo 추출 → `40-actions/`로 |

## 8. 트러블슈팅

| 증상 | 원인·해결 |
|------|----------|
| Claude가 CLAUDE.md를 모름 | vault 루트에서 `claude` 실행했는지 확인 |
| Ingest 후 20-wiki에 안 보임 | `index.md` 직접 확인. 등록 누락이면 "index 업데이트해줘" |
| Daily note 자동 생성 안 됨 | Periodic Notes 설정 확인 (02 단계) |
| 한국어/영어 섞임 | CLAUDE.md "Korean default" 줄 확인 |

다음: `docs/05-daily-workflow.md`
