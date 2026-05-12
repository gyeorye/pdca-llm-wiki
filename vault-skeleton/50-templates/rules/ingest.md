---
tags: [rule, ingest]
domain: meta
updated: 2026-05-12
---

# Ingest Rule

Trigger: "ingest this" or 새 file specified in `10-raw/`.

## Ingest 제외 경로

- `00-inbox/placeholder/**` — 미완성 working draft. 완성되면 `10-raw/`로 이동 후 ingest.

## 기본 절차

1. Source 읽고 핵심 내용 식별
2. `20-wiki/`에 요약 페이지 생성 (또는 기존에 병합)
3. 관련 wiki 페이지 찾아 cross-reference 갱신
4. `20-wiki/index.md`에 entry 추가/갱신
5. `20-wiki/log.md`에 기록:
   ```
   ## [YYYY-MM-DD] ingest | <제목>
   - 생성: path/to/new.md
   - 업데이트: path/to/existing.md
   ```

## Wiki page 작성 시
→ `50-templates/rules/wiki-conventions.md` 참조 (frontmatter / 도메인 분할 / content rules)

## Special cases (소스 경로별 추가 rule)

Source path 매칭 시 해당 rule file을 Read 후 추가 절차 적용.

예시 (사용자가 필요 시 `ingest-cases/` 하위에 rule 파일 추가):
- `10-raw/books/**` → `50-templates/rules/ingest-cases/books.md` (책 ingest 패턴)
- `10-raw/personal-journal/**` → 개인 영역 처리 rule

`ingest-cases/` 폴더가 없거나 매칭 case가 없으면 "기본 절차"만 적용.

## index.md format

```markdown
# Wiki Index
Updated: YYYY-MM-DD

## Work — Concepts
- [[some-concept]] — 한 줄 요약 (N sources)

## Personal — Career
- [[some-page]] — 한 줄 요약 (N sources)
```

## log.md format

```markdown
# Wiki Log

## [YYYY-MM-DD] ingest | <제목>
- 생성: <new files>
- 업데이트: <updated files>

## [YYYY-MM-DD] query | <질문 요약>
- 답변을 path/to/page.md에 통합
```
