# Claude Code Config

## 파일

- `settings.json.template` — Claude Code 전역 설정 샘플. `~/.claude/settings.json`에 병합.

## 적용 방법

이미 `~/.claude/settings.json`이 있다면 **병합** (덮어쓰지 말 것):

```bash
# 백업
cp ~/.claude/settings.json ~/.claude/settings.json.bak

# 수동으로 enabledPlugins / extraKnownMarketplaces 항목만 추가
```

처음이라면 그대로 복사 가능:

```bash
cp settings.json.template ~/.claude/settings.json
# 그 후 본인에 맞게 수정
```

## qmd plugin (선택)

`qmd`는 vault 안 markdown을 인덱싱해 LLM이 검색할 수 있게 하는 MCP server.

설치 후 활성화:
```json
"enabledPlugins": {
  "qmd@qmd": true
}
```

GitHub: https://github.com/tobi/qmd

## CLAUDE.md

이건 settings.json이 아니라 **vault 루트에 두는 파일**. `vault-skeleton/CLAUDE.md.template`을 vault 루트에 `CLAUDE.md`로 복사. (`docs/03-folder-structure.md` 참조)
