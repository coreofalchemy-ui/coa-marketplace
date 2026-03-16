# 🎨 PPT Maker Plugin for Claude Code

순수 HTML/CSS/JavaScript로 고품질 웹 프레젠테이션(PPT)을 자동 생성하는 Claude Code 플러그인입니다.

## ✨ 특징
- **단일 HTML 파일** — 외부 의존성 없이 브라우저에서 바로 실행
- **다크 테마** — Gold, Cyan, Violet, Light 테마 지원
- **키보드 네비게이션** — ← → 방향키, F 전체화면
- **터치 지원** — 모바일 스와이프 제스처
- **CSS 애니메이션** — 부드러운 슬라이드 전환 효과
- **프로그레스 바** — 상단 진행률 표시

## 📦 설치

### 마켓플레이스에서 설치
```bash
/plugin marketplace add <username>/coa-marketplace
/plugin install ppt-maker-plugin@coa-marketplace
```

### 로컬 설치
```bash
claude --plugin-dir ./ppt-maker-plugin
```

## 🚀 사용법

Claude Code에서:
```
/ppt-maker-plugin:ppt-maker 클로드 코드의 작동 원리 PPT 3장 만들어줘
```

### 테마 옵션
- "골드 테마로" → 다크 + 골드 액센트 (기본)
- "시안 테마로" → 다크 + 시안 액센트
- "바이올렛 테마로" → 다크 + 보라 액센트
- "라이트 테마로" → 화이트 배경

## 📁 구조
```
ppt-maker-plugin/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── ppt-maker/
│       ├── SKILL.md
│       ├── scripts/template.html
│       └── examples/sample.html
└── README.md
```

## 📄 라이선스
MIT License — COA Team
