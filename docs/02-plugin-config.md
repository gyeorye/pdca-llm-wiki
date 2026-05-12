# 02. Plugin 설정 + 사용 시점

각 plugin의 설정값과 **언제 사용하는지** 정리.

## 공통

먼저 vault에 폴더가 있어야 plugin 설정에서 경로를 지정할 수 있다. **`docs/03-folder-structure.md`를 먼저 적용**하고 이 문서로 돌아와도 OK.

폴더 미리 알기:
- `00-inbox/daily/` — 일일 노트
- `30-pdca/cycles/` — 주/월간 회고
- `50-templates/` — 모든 template

---

## 1. Periodic Notes

**용도**: 매일/매주/매월 노트를 자동 폴더·이름·template으로 생성.

**언제 사용**:
- 아침에 "오늘 daily note 열기" 단축키 (Cmd-P → "Periodic: Open today's daily note")
- 매주 월요일 "Open this week's weekly note"
- 매월 1일 "Open this month's monthly note"

**설정** (Settings → Periodic Notes):

| 항목 | 값 |
|------|-----|
| Daily Notes — Enabled | ✅ |
| Daily — Format | `YYYY-MM/YYYY-MM-DD` |
| Daily — Folder | `00-inbox/daily` |
| Daily — Template | `50-templates/daily-note` |
| Weekly Notes — Enabled | ✅ |
| Weekly — Format | `YYYY-[W]WW` |
| Weekly — Folder | `30-pdca/cycles` |
| Weekly — Template | `50-templates/weekly-pdca` |
| Monthly Notes — Enabled | ✅ |
| Monthly — Format | `YYYY-MM` |
| Monthly — Folder | `30-pdca/cycles` |
| Monthly — Template | `50-templates/monthly-pdca` |

> ⚠️ Obsidian core plugin "Daily notes"는 **끔** (Periodic Notes와 충돌). Settings → Core plugins → Daily notes OFF.

`obsidian-config/plugins/periodic-notes/data.json`을 참고하면 그대로 복사 가능.

---

## 2. Templater

**용도**: Template 안에서 동적 값 (오늘 날짜, 사용자 입력 등)을 실행. Periodic Notes와 결합해 자동 채워진 daily note 생성.

**언제 사용**:
- Periodic Notes가 호출 → 매일 자동 (사용자가 직접 호출 X)
- 책 raw note 만들 때 "책 제목/저자/Phase 입력 후 자동 생성"
- 새 폴더에 파일 만들 때 폴더별 template 자동 적용

**설정** (Settings → Templater):

| 항목 | 값 |
|------|-----|
| Templates folder location | `50-templates` |
| Trigger Templater on new file creation | ✅ |
| Folder Templates — Enabled | ✅ |
| Folder Templates 항목 | `00-inbox/daily` → `50-templates/daily-note.md` |
| Folder Templates 항목 | `30-pdca/cycles` → `50-templates/weekly-pdca.md` |

> ⚠️ Obsidian core plugin "Templates"는 끔 (Templater가 상위 호환). Settings → Core plugins → Templates OFF.

---

## 3. Tasks

**용도**: `- [ ]` 체크박스에 due date·priority·tag 부여. 대시보드 쿼리로 모아보기.

**언제 사용**:
- Daily note에 `- [ ] 할 일 📅 2026-05-15` 형태로 작성
- 별도 대시보드 페이지에서 `tasks` 쿼리로 due/overdue 모아보기
- 회고 시 done/undone 상태 확인

**설정** (Settings → Tasks):

기본값 대부분 OK. 다음만 확인:
- **Set due date when toggling status**: 취향
- **Task format**: `Tasks Emoji Format` (기본)

**Vault rule** (`50-templates/rules/todo-rules.md` 참조):
- 일반 todo: `- [ ] 내용 📅 YYYY-MM-DD` (work 기본)
- 개인 todo: `- [ ] 내용 #personal 📅 YYYY-MM-DD`

**대시보드 쿼리 예시** (별도 페이지에 작성):

```tasks
not done
due before tomorrow
sort by due
```

---

## 4. Excalidraw

**용도**: Vault 안에서 다이어그램 작성 (PKM 구조도, 시스템 아키텍처, mind map).

**언제 사용**:
- Vault intake pipeline 시각화
- 시스템 아키텍처 도식화
- Mind map (회의/브레인스토밍)
- 책 읽으며 개념 관계도

**설정** (Settings → Excalidraw):

기본값 대부분 OK. 권장 변경:
- **Excalidraw folder**: `Excalidraw` (vault root)
- **New drawing filename prefix**: 빈 값 또는 `drawing-`
- **Theme**: 취향 (light/dark)

**파일 만들기**: Cmd-P → "Excalidraw: Create new drawing" 또는 우클릭 → New Excalidraw drawing.

> ⚠️ **z-order는 `index` 필드가 아니라 elements 배열 순서로 결정**. 배경 사각형은 배열 앞쪽에 있어야 텍스트를 안 가린다. LLM이 직접 .excalidraw 편집할 일 있으면 주의.

---

## 5. Obsidian Web Clipper (브라우저 확장)

**용도**: 웹 페이지(블로그, 기사, 회의 페이지)를 vault에 markdown으로 저장.

**언제 사용**:
- 좋은 블로그/기사 읽고 vault에 보관 → 나중에 LLM ingest
- 회의록 페이지(Confluence/Notion) 저장
- 코드 snippet 모음

**설정** (브라우저 확장 아이콘 클릭 → ⚙️ Settings):

| 항목 | 값 |
|------|-----|
| Vault | 본인 vault 선택 |
| Default folder | `10-raw/web-clips` |
| Filename | `{{title}}` 또는 `{{date}}-{{title}}` |

**Template 만들기** (옵션):
- Settings → Templates → New
- Fields: `tags: [raw, web-clip]`, `source: {{url}}`, `domain: {{domain}}`, `clipped: {{date}}`
- Body: `{{content}}` (Defuddle 처리됨)

> 💡 Web-clip에서 만든 액션아이템은 daily note에 등록할 때 원본 URL을 함께 적어둘 것 (출처 추적 위해).

---

## 6. 확인

설치·설정이 다 됐는지 테스트:

1. Cmd-P → "Periodic: Open today's daily note" → `00-inbox/daily/2026-XX/` 아래 오늘 날짜 노트 생성됨
2. Template 자동 적용 확인 (할 일 섹션 등이 미리 채워져 있어야 함)
3. `- [ ] 테스트 📅 2026-12-31` 입력 → Tasks plugin이 인식

다음: `docs/03-folder-structure.md`
