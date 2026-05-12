---
tags: [rule, todo]
domain: meta
updated: 2026-05-12
---

# Todo Rules

## Vault-wide 규칙

- **Default (no tag) = work** — 별도 tag 없음
- **Personal todo = `#personal` tag 필수**
- Format: `- [ ] content 📅 YYYY-MM-DD` (Tasks plugin)

## LLM이 todo 생성 시

- Work context (work/, projects/, meeting notes) → no tag
- Personal context (personal/, health/, family 등) → `#personal`
- 모호하면 user에게 물어라

## Wiki 페이지 내부 todo

`20-wiki/` + `30-pdca/` 내부 standard todo는 dashboard query 자동 제외.

노출하려면 **memo 형식** 사용 (standard todo 대신).
보정 항목 등 dashboard 노출이 필요한 todo는 daily note에 별도 등록.

## Web-clip 출처 액션아이템

Web-clip(`10-raw/web-clips/`)에서 추출한 액션아이템은 daily note에 등록 시 **원본 URL 함께 적기** (출처 추적·재방문 용이).

예: `- [ ] X 작업 (출처: https://...) 📅 2026-05-15`
