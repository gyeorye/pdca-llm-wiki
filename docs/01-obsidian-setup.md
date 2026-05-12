# 01. Obsidian 설치 + Vault 생성

## 1. Obsidian 설치

- 다운로드: https://obsidian.md/download
- 지원 OS: macOS / Windows / Linux / iOS / Android
- 설치 후 실행

## 2. Vault 생성

Obsidian 시작 화면 → **"Create new vault"** 클릭.

| 항목 | 권장값 | 이유 |
|------|--------|------|
| Vault name | 자유 (예: `MyVault`) | |
| Location | iCloud Drive 하위 (Mac) | 멀티 디바이스 sync 가능. 또는 Obsidian Sync 유료 사용. |

**Mac에서 iCloud sync**:
- Location: `~/Library/Mobile Documents/iCloud~md~obsidian/Documents/MyVault`
- 파인더에서는 "iCloud Drive > Obsidian > MyVault"로 보임

> ⚠️ Git으로 sync할 거면 iCloud 안 쓰는 게 낫다. Conflict 자주 남.

## 3. 5개 Plugin 설치

이 vault 시스템은 5개의 Obsidian plugin을 사용한다.

| Plugin | 용도 | 설치 위치 |
|--------|------|-----------|
| **Tasks** | 일/할일 체크박스 + 쿼리 | Community plugin |
| **Periodic Notes** | Daily/Weekly/Monthly 노트 자동 생성 | Community plugin |
| **Templater** | 동적 template (날짜 자동 삽입 등) | Community plugin |
| **Excalidraw** | 다이어그램 (PKM 구조 시각화 등) | Community plugin |
| **Obsidian Web Clipper** | 웹 페이지를 vault에 저장 | **브라우저 확장** (별도) |

### Community plugin 설치 단계

1. **Settings (⚙️) → Community plugins → Turn on community plugins** (처음 한 번만)
2. **Browse** 클릭
3. 각 plugin 검색 후 **Install** → **Enable**

설치할 plugin ID (Browse에서 검색):
- `Tasks` (저자: Schemar)
- `Periodic Notes` (저자: liamcain)
- `Templater` (저자: SilentVoid13)
- `Excalidraw` (저자: zsviczian)

### Obsidian Web Clipper (브라우저 확장)

- Chrome/Firefox/Safari 모두 지원
- 설치: https://obsidian.md/clipper
- 브라우저 확장 스토어에서 "Obsidian Web Clipper" 검색해도 됨

## 4. 확인

설치 후 Obsidian 좌측 사이드바에 plugin 아이콘이 보여야 함.

다음: `docs/02-plugin-config.md`에서 각 plugin 설정.
