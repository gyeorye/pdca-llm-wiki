# 05. 일상 사용 시나리오

이 vault 시스템이 실제로 어떻게 돌아가는지 시나리오 단위로 정리.

## 🌅 매일 아침

1. Obsidian 열기
2. Cmd-P → "Periodic: Open today's daily note" (또는 단축키 설정)
3. Templater가 자동으로 daily template 적용 → 빈 칸 채우면서 시작
4. 일 시작 전 오늘 할 일 입력 (`- [ ] ... 📅 today`)

## 📚 새 콘텐츠 들어왔을 때

### Case 1: 블로그/기사 읽었을 때
1. Obsidian Web Clipper로 클립 → `10-raw/web-clips/`에 저장
2. Claude Code: `10-raw/web-clips/X.md 파일 ingest해줘`
3. LLM이 `20-wiki/`에 요약 페이지 만들고 `index.md` 업데이트

### Case 2: 책을 다 읽었을 때
1. 읽으며 `10-raw/books/책이름.md`에 인용·메모 작성 (Templater "book-raw-template" 사용)
2. 완독 후 Claude Code: `10-raw/books/책이름.md 책 ingest해줘`
3. LLM이 `20-wiki/meta/concepts/`에 개념 페이지 생성 + 관련 wiki 페이지 cross-reference 업데이트

### Case 3: 회의가 끝났을 때
1. Templater "meeting-note" template으로 `10-raw/web-clips/회의-제목.md` 생성 (또는 회의록 페이지를 Web Clipper로 저장)
2. Claude Code: `오늘 회의 ingest. action item들은 daily에 todo로 추가해줘`
3. LLM이 회의 요약 → `20-wiki/work/projects/`에 정리 + 액션 → 오늘 daily에 등록

## 🌙 매일 저녁 (선택)

1. Daily note 마무리 — "오늘 배운 것 (1줄)" 채우기
2. 미완료 todo는 LLM에게: `오늘 미완 todo 내일로 옮겨줘`

## 📅 매주 일요일/월요일

1. Cmd-P → "Periodic: Open this week's weekly note"
2. Claude Code: `weekly PDCA 써줘`
3. LLM이 이번 주 daily 7개 종합 → Do/Check/Act 자동 채움
4. 본인이 검토하며 추가/수정
5. **Light lint**: 이번 주 변경된 wiki page에서 모순·누락 link 점검

## 📊 매월 1주차

1. Cmd-P → "Periodic: Open this month's monthly note"
2. Claude Code: `monthly PDCA 써줘`
3. LLM이 4주 weekly 종합 + **full lint** + `about-you.md` "Current situation" 갱신 제안
4. 본인이 검토·승인 → wiki 갱신

## ❓ 자주 하는 질문 시나리오

### "X에 대해 내가 정리한 거 있나?"
```
DB 인덱스 관련 wiki 페이지 있어?
```
→ LLM이 `20-wiki/index.md` 보고 관련 페이지 찾아 답변. 없으면 "관련 raw 노트는 X에 있어요" 식.

### "내가 어떤 사람인지 다시 알려줘"
```
나에 대해 아는 거 요약해줘
```
→ LLM이 `20-wiki/meta/about-you.md` 읽고 정리.

### "이번 달 패턴이 뭐였지?"
```
이번 달 패턴 분석해줘
```
→ Monthly PDCA + daily notes 종합 → `20-wiki/meta/patterns.md`에 새 항목 제안.

## 🛠️ 유지보수 시나리오

### Wiki lint (자체 trigger)
```
wiki lint 해줘
```
→ 모순 / orphan page (inbound link 0) / 90일+ 미갱신 page / 자주 언급되는데 페이지 없는 개념 / 누락 cross-ref 점검.

월 1회 정도 권장.

### 새 폴더/도메인 추가
예: 개인 도메인에 `pet/` 추가.
1. `20-wiki/personal/pet/` 폴더 생성
2. `50-templates/rules/wiki-conventions.md`의 "Domain 분할" 섹션에 한 줄 추가
3. 첫 ingest 때 LLM이 자동으로 cross-reference 시작

### Rule 파일 수정
- `50-templates/rules/*.md` 직접 편집 → 다음 trigger부터 자동 반영
- "처음 사용 시 X 규칙 추가" 식으로 LLM에게 요청해도 OK (수정안 제안 → 본인 승인 → 저장)

## 💡 권장 패턴

| 상황 | 권장 동작 |
|------|----------|
| 메모가 길어진다 | `10-raw/`로 분리, daily에는 링크만 |
| Wiki page가 길어진다 | 도메인 분할 (해당 폴더로 옮기고 cross-ref) |
| Todo가 daily에서 사라진다 | Tasks plugin 쿼리 대시보드 만들어 `40-actions/`에 |
| LLM이 같은 실수 반복 | 해당 rule 파일에 한 줄 추가 |

다음: `docs/06-customization.md` — 나만의 컨텍스트 채우기
