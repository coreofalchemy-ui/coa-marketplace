# 🏪 COA Marketplace — Claude Code 플러그인 마켓플레이스

COA Team의 Claude Code 플러그인 마켓플레이스입니다.

## 📦 설치된 플러그인

| 플러그인 | 버전 | 설명 |
|---------|------|------|
| **ppt-maker-plugin** | 1.0.0 | 순수 HTML/CSS/JS로 고품질 웹 PPT 자동 생성 |

## 🚀 사용법

### 1. 마켓플레이스 추가
```bash
# Claude Code에서 실행
/plugin marketplace add coreofalchemy-ui/coa-marketplace
```

### 2. 플러그인 설치
```bash
/plugin install ppt-maker-plugin@coa-marketplace
```

### 3. 사용
```bash
/ppt-maker-plugin:ppt-maker 발표 자료 만들어줘
```

## 🔄 자동 업데이트
마켓플레이스 UI에서 "Enable Auto Update" 를 켜면,
Claude Code 실행 시 자동으로 최신 버전을 동기화합니다.

## 📁 구조
```
coa-marketplace/
├── .claude-plugin/
│   └── marketplace.json
├── plugins/
│   └── ppt-maker-plugin/
│       ├── .claude-plugin/plugin.json
│       ├── skills/ppt-maker/SKILL.md
│       └── README.md
└── README.md
```

---
Made with ❤️ by COA Team
