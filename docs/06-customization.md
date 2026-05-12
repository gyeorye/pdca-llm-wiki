# 06. 나의 컨텍스트 채우기

`about-you.md`는 **Claude의 single entry point**. 여기에 본인 정보를 채우면 LLM이 모든 답변에서 본인 맥락을 자동 반영한다.

## 1. 파일 위치

```
MyVault/20-wiki/meta/about-you.md
```

`vault-skeleton/20-wiki/meta/about-you.md.template`을 복사한 뒤 `.template` 제거하고 채워라.

## 2. 작성 순서 (단계적)

처음부터 다 채울 필요 없음. 최소부터 시작해 점진적으로 풍부하게.

### Stage 1: 최소 시작 (5분)

다음만 채워도 사용 가능:

```markdown
## 📍 Current Situation

### Job
- 직무, 회사, 부서, 미션

### Life Phase
- 현재 인생 단계의 큰 사건 (이직 준비, 결혼, 출산 등)

## 🎯 How to Interact with You

### Communication style
- 선호하는 응답 스타일 (간결 vs 상세, 한국어/영어 비중 등)

### What to avoid
- LLM이 하지 않았으면 하는 것
```

### Stage 2: 정체성 추가 (꾸준히)

본인을 정의하는 핵심 트레이트가 보이기 시작하면:

```markdown
## 🏛️ Identity Layers

### Layer 1 — What: [본인 정체성 한 문장]
### Layer 2 — How: [어떻게 일하는 사람]
### Layer 3 — Why: [무엇을 위해 일하는 사람]
### Layer 4 — Embodied: [그 정체성의 실증 증거]

## 🧭 Core Traits

(여러 source에서 반복해 나오는 본인 특성. 처음엔 3-5개로 시작 → 시간이 지나며 확장)

1. **트레이트 이름** — 설명. 외부 검증 데이터 있으면 함께.
```

### Stage 3: Focus Principles

긴 시간 관통하는 본인의 핵심 원칙 (1-3개):

```markdown
## ⭐ Focus Principles

### Principle 1: [원칙 1]
### Principle 2: [원칙 2]
### Principle 3: [원칙 3]

**Adoption criterion**: 새 활동이 이 중 하나에 기여하는가?
```

### Stage 4: Shadow Areas

본인의 약점·블라인드 스팟. 정직한 자기인식.

```markdown
## 🌑 Shadow Areas

### Shadow 1: [패턴 이름]
- 설명, 외부 피드백 source, 학습 영역
```

### Stage 5: 검증 데이터

객관 데이터 (피드백, 평가, 성과)로 보강:

```markdown
## 🎤 Public Activities & Validated Impact

### Large audience (one-time)
### Mid-scale coaching (ongoing)
### Small-scale direct management
### External recommendations
```

## 3. 갱신 사이클

LLM이 자동으로 제안:

| 시점 | 갱신 항목 |
|------|----------|
| Monthly PDCA | "Current Situation" / "Ongoing Activities" 갱신 제안 |
| 새 트레이트 감지 | "사용자 확인 후 추가" — 본인 승인 필수 |
| 외부 검증 데이터 (피드백/평가) | 관련 트레이트에 citation 추가 |

## 4. Manually Managed (LLM 수정 금지) 명시

`about-you.md` 하단에 다음 명시:

```markdown
## 📝 Update Principles

- 다음은 manually managed (LLM 자동 수정 금지):
  - 트레이트 목록 + 정의
  - Focus principles
  - Shadow areas (새 추가는 사용자 확인 필수)
- Auto-update OK (제안만):
  - Current situation
  - Ongoing activities
```

## 5. Deep references 만들기 (선택)

`about-you.md`가 너무 길어지면 detail document로 분리:

| 파일 | 내용 |
|------|------|
| `20-wiki/meta/identity-thesis.md` | 정체성 장기 누적 (Phase log, open questions) |
| `20-wiki/meta/focus-principles-YYYY.md` | 그 해의 focus principles (monthly review) |
| `20-wiki/meta/patterns.md` | 반복되는 본인 패턴·인사이트 |
| `20-wiki/meta/anti-patterns.md` | 실패한·비효율 접근 |

`CLAUDE.md`의 "Deep references" 섹션에 등록하면 LLM이 deep 질문 시 함께 참고.

## 6. 예시 진행도

### Month 1 (시작)
- `about-you.md`: Current Situation + Communication style만 채움 (Stage 1)
- daily note 작성하며 LLM과 대화 시작
- 매주 weekly PDCA

### Month 3
- 반복되는 패턴 발견 → Stage 2 트레이트 3-5개 추가
- 첫 monthly PDCA → patterns.md 첫 항목

### Month 6
- 트레이트 10개 이상 + Focus principles 정해짐 (Stage 3)
- Shadow areas 1-2개 명시 (Stage 4)

### Month 12
- 정체성 layer 4개 정착
- 외부 피드백 데이터로 트레이트 검증 (Stage 5)
- thesis.md로 detail 분리

## 7. 주의사항

| 함정 | 대응 |
|------|------|
| LLM이 트레이트를 너무 자주 제안 | "Manually managed" 명시 + 사용자 승인 절차 |
| 트레이트가 너무 많아짐 (>30) | 통합·정리 — 비슷한 건 한 항목으로 |
| 한 번 적고 안 보게 됨 | Monthly PDCA에서 강제로 검토 |
| Wiki에 너무 노골적 사생활 | 민감 정보는 `10-raw/personal-journal/`에 두고 `20-wiki/`에는 추상화된 패턴만 |

---

## 끝

이제 vault 시스템 구축 + LLM 연동 + 개인화까지 완료. `docs/05-daily-workflow.md` 시나리오대로 사용하면서 본인 패턴에 맞게 진화시켜 가면 됨.

문제 생기면 트러블슈팅:
- `04-claude-code-setup.md` 8번 표
- `02-plugin-config.md` 각 plugin "확인" 섹션
