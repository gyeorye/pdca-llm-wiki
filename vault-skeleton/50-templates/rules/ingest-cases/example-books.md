---
tags: [rule, ingest, ingest-case]
domain: meta
updated: 2026-05-12
---

# Ingest Case: Books (example)

> Trigger: `10-raw/books/**` 경로에서 ingest 요청 시 추가 적용.
> 사용하지 않으면 이 파일 삭제해도 OK.

## 추가 절차

1. 기본 ingest 절차 (parent rule `ingest.md`) 먼저 적용
2. 책 ingest 시 추가:
   - 핵심 개념 → `20-wiki/meta/concepts/<concept-slug>.md`로 분리 (이미 있으면 source 추가)
   - "이 책 때문에 할 것" 액션아이템 → 오늘 daily note에 todo로 등록
   - `about-you.md`의 "Long-Term Plan" / "Ongoing Activities"와 연결되는 부분 있으면 cross-reference 제안 (자동 갱신 X, 사용자 승인 후)

## 책 raw note frontmatter

`50-templates/book-raw-template.md` 참조. 다음 필드 활용:
- `title`, `author`, `started`, `finished`
- `status: reading | finished | dropped`

## 완독 판단

`status: finished` + `finished` 날짜 있을 때만 "ingest 완료" 처리.
