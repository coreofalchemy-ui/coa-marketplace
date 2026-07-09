# HANDOFF — 다음 에이전트 시작점
> 마지막 업데이트: 2026-07-09 (Codex — 기록 보강 작전)

## 이 프로젝트는 무엇 (2-3줄)
COA Team의 Claude Code 플러그인 마켓플레이스 레포다.
현재 등록 플러그인은 `ppt-maker-plugin` 1개이며, 순수 HTML/CSS/JavaScript 웹 프레젠테이션을 생성하는 스킬과 템플릿을 제공한다.
일반 앱 소스나 서버가 아니라 마켓플레이스 JSON, 플러그인 manifest, 스킬 문서, HTML 템플릿으로 구성된다.

## 어디까지 했음 (최근 60일 실측 — 커밋·코드 근거)
- `062240b` WHERE.md 위치 맵을 추가해 마켓플레이스 구조, 핵심 파일, 실행/빌드 부재, 주의사항을 정리했다.
- README는 `/plugin marketplace add coreofalchemy-ui/coa-marketplace`, `/plugin install ppt-maker-plugin@coa-marketplace` 설치 흐름을 적는다.
- `.claude-plugin/marketplace.json`은 `ppt-maker-plugin` source를 `./plugins/ppt-maker-plugin`로 지정한다.
- `plugins/ppt-maker-plugin/.claude-plugin/plugin.json`은 버전 1.0.0, MIT, ppt/presentation/slides/web/html 키워드를 적는다.
- `plugins/ppt-maker-plugin/skills/ppt-maker/SKILL.md`는 3장 시안 후 확인, 단일 HTML 파일, 테마와 키보드 네비게이션 규칙을 적는다.

## 현재 상태 (돌아가는 것 / 멈춘 것 / 미확인)
- 돌아가는 것: 마켓플레이스와 플러그인 파일 구조는 존재하고, 작업 전 git status는 깨끗했다.
- 멈춘 것: package.json, src, 빌드 스크립트, 서버 실행 흐름은 없다.
- 미확인: 이번 작업은 Claude Code 실제 `/plugin install`과 스킬 실행 결과를 검증하지 않았다.

## 다음 액션 (로드맵 — 우선순위 3-5개, 근거 포함)
1. 플러그인 변경 전 `marketplace.json`, plugin.json, SKILL.md를 함께 읽는다. WHERE.md가 세 파일을 핵심 진입점으로 적는다.
2. 설치 검증이 필요하면 Claude Code에서 마켓플레이스 추가와 플러그인 설치를 직접 확인한다. README의 사용법이 근거다.
3. PPT 생성 품질 수정은 `plugins/ppt-maker-plugin/skills/ppt-maker/SKILL.md`와 `scripts/template.html`만 범위로 잡는다.
4. 버전 변경이 생기면 plugin.json과 marketplace.json의 버전을 같이 맞춘다.
5. 새 플러그인을 추가할 때는 `plugins/<plugin>/` 아래 manifest, skills, README 구조를 기존 플러그인과 맞춘다.

## 지뢰 · 주의 (건드리면 깨지는 것, 실측/기록 근거만)
- `package.json`, `src`, `.env`가 없으므로 실행 앱처럼 다루면 안 된다. WHERE.md가 확인 결과를 적는다.
- `skills/` 폴더는 플러그인 루트 아래에 있다. WHERE.md가 `.claude-plugin/` 안으로 옮기지 말라고 적는다.
- `template.html`과 sample은 단일 HTML 구조다. 외부 라이브러리 의존을 추가하기 전 현재 설계를 먼저 확인한다.
- 소스 수정 없이 위치 문서만 다룰 때는 기존 플러그인 파일을 건드리지 않는다.
- 마켓플레이스 source 경로 `./plugins/ppt-maker-plugin`을 바꾸면 설치 경로가 깨질 수 있다.
