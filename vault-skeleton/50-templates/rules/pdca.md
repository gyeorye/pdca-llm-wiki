---
tags: [rule, pdca, lint]
domain: meta
updated: 2026-05-12
---

# PDCA + Lint Rule

## Weekly PDCA

Trigger: "write weekly PDCA"

1. `00-inbox/daily/`에서 이번 주 daily notes 읽기
2. `40-actions/` todo 상태 확인
3. `30-pdca/cycles/`에 weekly 회고 draft 생성 (Periodic Notes가 빈 template 만들어둠 — LLM은 채우기만)
4. **Light lint**: 이번 주 변경·신규 wiki page에서 모순·누락 link 점검

## Monthly PDCA

Trigger: "write monthly PDCA"

1. 4 주차 weekly 종합
2. **Full lint** (아래)
3. (선택) `20-wiki/work/` concepts/projects/decisions 컴파일 페이지 갱신
4. `about-you.md` "Current situation" + "Ongoing activities" 갱신 제안
5. (선택) `focus-principles-YYYY.md` "Monthly log" append

## Lint (자체 trigger: "wiki lint")

- 모순 내용 감지
- Orphan page 나열 (inbound link 0)
- 90일+ 미갱신 page flag
- 자주 언급되는데 자체 page 없는 개념 감지
- 누락 cross-reference 제안

## 장기 액션 관리

PDCA에서 자주 등장하는데 closure가 안 되는 장기 액션은 별도로 모아라:
- `30-pdca/active-experiments.md`로 이동 또는
- `30-pdca/someday-maybe.md`에 보관

Weekly/monthly PDCA마다 검토.
