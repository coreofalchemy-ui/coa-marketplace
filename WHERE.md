# 🗺️ WHERE — coa-marketplace 위치 맵

> **"어디에 뭐가 있나" 1장. 헤매기 전에 이거부터 본다.**
> 마지막 갱신: 2026-05-21

---

## 0. 이 레포 한 줄

`coa-marketplace` (= COA Claude Code 플러그인 마켓플레이스 레포) 는 COA Team의 Claude Code 플러그인 마켓플레이스다.
현재 등록된 플러그인은 `ppt-maker-plugin` (= 웹 발표자료 생성 플러그인) 1개이며, `package.json`과 `src` (= 앱 소스 폴더) 없이 JSON/Markdown/HTML 파일로 구성된다.

---

## 1. 폴더 지도 — 루트에서 뭐가 어디

| 찾는 것 | 폴더 |
|---|---|
| 마켓플레이스 설정 | `.claude-plugin/` (= Claude Code 마켓플레이스 설정 폴더) |
| 플러그인 패키지 모음 | `plugins/` (= 플러그인 묶음 폴더) |
| PPT 생성 플러그인 | `plugins/ppt-maker-plugin/` (= 발표자료 생성 플러그인 패키지) |
| Claude Code 스킬 모음 | `plugins/ppt-maker-plugin/skills/` (= 스킬 규칙 보관 폴더) |
| PPT 생성 스킬 | `plugins/ppt-maker-plugin/skills/ppt-maker/` (= 발표자료 생성 규칙·템플릿·예시 폴더) |
| HTML 생성 템플릿 | `plugins/ppt-maker-plugin/skills/ppt-maker/scripts/` (= 생성 템플릿 보관 폴더) |
| HTML 샘플 | `plugins/ppt-maker-plugin/skills/ppt-maker/examples/` (= 샘플 파일 보관 폴더) |

> 건드리지 말 것: `.git/` (= Git 저장소 내부 기록 폴더). 소스 작업 없이 위치 문서만 만들 때는 기존 플러그인 파일을 수정하지 않는다.

---

## 2. 핵심 파일 — 진입점 (어디부터 읽나)

| 무엇 | 파일 |
|---|---|
| 레포 설명 / 설치법 | `README.md` |
| 마켓플레이스 카탈로그 | `.claude-plugin/marketplace.json` |
| 플러그인 메타데이터 | `plugins/ppt-maker-plugin/.claude-plugin/plugin.json` |
| 플러그인 설명 / 로컬 설치법 | `plugins/ppt-maker-plugin/README.md` |
| PPT 생성 스킬 규칙 | `plugins/ppt-maker-plugin/skills/ppt-maker/SKILL.md` |
| 기본 HTML 템플릿 | `plugins/ppt-maker-plugin/skills/ppt-maker/scripts/template.html` |
| 10페이지 골드 테마 샘플 | `plugins/ppt-maker-plugin/skills/ppt-maker/examples/sample.html` |

---

## 3. 작업 → 어디 (이 레포에서 자주 하는 작업)

| 하려는 작업 | 어디 건드림 |
|---|---|
| 마켓플레이스 등록 정보 수정 | `.claude-plugin/marketplace.json` |
| 플러그인 이름·설명·버전 수정 | `plugins/ppt-maker-plugin/.claude-plugin/plugin.json` |
| 설치 / 사용 안내 수정 | `README.md`, `plugins/ppt-maker-plugin/README.md` |
| PPT 생성 규칙 수정 | `plugins/ppt-maker-plugin/skills/ppt-maker/SKILL.md` |
| 생성되는 HTML 기본 구조 수정 | `plugins/ppt-maker-plugin/skills/ppt-maker/scripts/template.html` |
| 샘플 발표자료 확인 / 수정 | `plugins/ppt-maker-plugin/skills/ppt-maker/examples/sample.html` |

---

## 4. 실행 / 빌드

- 개발 서버: 없음 확인 (`package.json` 없음, `src` 없음)
- 빌드: 없음 확인 (`package.json` 없음)
- 마켓플레이스 추가: `/plugin marketplace add coreofalchemy-ui/coa-marketplace`
- 플러그인 설치: `/plugin install ppt-maker-plugin@coa-marketplace`
- 플러그인 사용: `/ppt-maker-plugin:ppt-maker 발표 자료 만들어줘`
- 배포: 별도 배포 설정 파일 없음. README 기준 Claude Code 마켓플레이스에서 자동 업데이트를 켜면 최신 버전을 동기화한다.

---

## 5. 지뢰 / 주의

- `package.json`, `.env`, `.env.local`, `src`는 확인 결과 없다. 실행 스크립트나 환경변수가 있다고 가정하지 않는다.
- `.claude-plugin/marketplace.json`의 `source`는 `./plugins/ppt-maker-plugin`로 지정되어 있다.
- `skills/` 폴더는 플러그인 루트 아래에 있다. `.claude-plugin/` 안으로 옮기지 않는다.
- `template.html`과 `sample.html`은 단일 HTML 파일 구조다. 외부 라이브러리 설치 흐름을 추가하기 전에 현재 순수 HTML/CSS/JavaScript 구조를 먼저 확인한다.
- 이 레포는 Claude Code 플러그인 마켓플레이스다. 소스 수정 없이 위치 문서만 다룰 때는 커밋하지 않는다.
