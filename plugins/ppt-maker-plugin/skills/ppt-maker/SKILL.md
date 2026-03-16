---
name: ppt-maker
description: "순수 HTML/CSS/JS로 고품질 웹 프레젠테이션(PPT)을 자동 생성. PPT, 프레젠테이션, 슬라이드 제작 요청 시 자동 발동."
---

# Web PPT Maker Skill

## 발동 조건
사용자가 다음 키워드를 사용할 때 이 스킬 자동 발동:
- "PPT 만들어줘", "프레젠테이션 생성", "슬라이드 제작"
- "발표자료 만들어줘", "slides", "presentation"

## 핵심 원칙
1. **단일 HTML 파일**: 외부 CDN, 라이브러리 의존성 없이 순수 HTML/CSS/JS로 동작
2. **점진적 생성**: 먼저 3장 시안 → 사용자 확인 → 전체 생성 (한번에 40장 금지)
3. **고품질 디자인**: Neumorphism, 그레디언트, CSS 애니메이션 적극 활용

## 생성 규칙

### 1. HTML 구조
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{프레젠테이션 제목}</title>
  <style>/* 내부 CSS */</style>
</head>
<body>
  <div class="presentation">
    <div class="slide active" id="slide-1"><!-- 슬라이드 내용 --></div>
    <div class="slide" id="slide-2"><!-- 슬라이드 내용 --></div>
    <!-- ... -->
  </div>
  <div class="controls">
    <button class="prev-btn">◀</button>
    <span class="slide-counter">1 / N</span>
    <button class="next-btn">▶</button>
  </div>
  <script>/* 내부 JavaScript */</script>
</body>
</html>
```

### 2. CSS 필수 스타일

#### 2.1 레이아웃 시스템
```css
* { margin: 0; padding: 0; box-sizing: border-box; }

body {
  font-family: 'Segoe UI', 'Apple SD Gothic Neo', sans-serif;
  overflow: hidden;
  height: 100vh;
  width: 100vw;
}

.presentation {
  position: relative;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

.slide {
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 60px 80px;
  opacity: 0;
  transform: translateX(100%);
  transition: all 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  pointer-events: none;
}

.slide.active {
  opacity: 1;
  transform: translateX(0);
  pointer-events: all;
}

.slide.prev {
  opacity: 0;
  transform: translateX(-100%);
}
```

#### 2.2 컬러 테마 시스템
사용자가 요청한 테마에 따라 CSS 변수를 변경:

```css
/* 다크 골드 테마 (기본) */
:root {
  --bg-primary: #0a0a0f;
  --bg-secondary: #12121a;
  --accent: #d4a853;
  --accent-glow: rgba(212, 168, 83, 0.3);
  --text-primary: #f0f0f0;
  --text-secondary: #a0a0a0;
  --card-bg: rgba(255, 255, 255, 0.05);
  --border: rgba(255, 255, 255, 0.1);
}

/* 다크 시안 테마 */
.theme-cyan {
  --accent: #00d4aa;
  --accent-glow: rgba(0, 212, 170, 0.3);
}

/* 다크 바이올렛 테마 */
.theme-violet {
  --accent: #8b5cf6;
  --accent-glow: rgba(139, 92, 246, 0.3);
}

/* 라이트 테마 */
.theme-light {
  --bg-primary: #ffffff;
  --bg-secondary: #f8f9fa;
  --text-primary: #1a1a2e;
  --text-secondary: #6c757d;
  --card-bg: rgba(0, 0, 0, 0.03);
  --border: rgba(0, 0, 0, 0.1);
}
```

#### 2.3 타이포그래피
```css
.slide-title {
  font-size: clamp(2rem, 4vw, 3.5rem);
  font-weight: 800;
  color: var(--text-primary);
  margin-bottom: 20px;
  line-height: 1.2;
}

.slide-subtitle {
  font-size: clamp(1rem, 2vw, 1.5rem);
  color: var(--accent);
  font-weight: 600;
  margin-bottom: 30px;
  text-transform: uppercase;
  letter-spacing: 3px;
}

.slide-content {
  font-size: clamp(0.9rem, 1.5vw, 1.2rem);
  color: var(--text-secondary);
  line-height: 1.8;
  max-width: 800px;
}
```

#### 2.4 애니메이션
```css
/* 요소 등장 애니메이션 */
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes fadeInLeft {
  from { opacity: 0; transform: translateX(-30px); }
  to { opacity: 1; transform: translateX(0); }
}

@keyframes scaleIn {
  from { opacity: 0; transform: scale(0.9); }
  to { opacity: 1; transform: scale(1); }
}

@keyframes glowPulse {
  0%, 100% { box-shadow: 0 0 20px var(--accent-glow); }
  50% { box-shadow: 0 0 40px var(--accent-glow); }
}

.slide.active .slide-title { animation: fadeInUp 0.6s 0.2s both; }
.slide.active .slide-subtitle { animation: fadeInUp 0.6s 0.4s both; }
.slide.active .slide-content { animation: fadeInUp 0.6s 0.6s both; }
```

### 3. JavaScript 필수 로직

```javascript
class Presentation {
  constructor() {
    this.slides = document.querySelectorAll('.slide');
    this.currentSlide = 0;
    this.totalSlides = this.slides.length;
    this.isTransitioning = false;
    this.init();
  }

  init() {
    // 키보드 이벤트
    document.addEventListener('keydown', (e) => {
      if (this.isTransitioning) return;
      if (e.key === 'ArrowRight' || e.key === 'ArrowDown' || e.key === ' ') {
        e.preventDefault();
        this.next();
      }
      if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') {
        e.preventDefault();
        this.prev();
      }
      if (e.key === 'f' || e.key === 'F') {
        this.toggleFullscreen();
      }
    });

    // 버튼 클릭
    document.querySelector('.prev-btn')?.addEventListener('click', () => this.prev());
    document.querySelector('.next-btn')?.addEventListener('click', () => this.next());

    // 터치/스와이프
    let startX = 0;
    document.addEventListener('touchstart', (e) => startX = e.touches[0].clientX);
    document.addEventListener('touchend', (e) => {
      const diffX = startX - e.changedTouches[0].clientX;
      if (Math.abs(diffX) > 50) diffX > 0 ? this.next() : this.prev();
    });

    // 카운터 업데이트
    this.updateCounter();
  }

  goTo(index) {
    if (index < 0 || index >= this.totalSlides || this.isTransitioning) return;
    this.isTransitioning = true;

    const current = this.slides[this.currentSlide];
    const target = this.slides[index];

    if (index > this.currentSlide) {
      current.classList.remove('active');
      current.classList.add('prev');
      target.classList.remove('prev');
      target.classList.add('active');
    } else {
      current.classList.remove('active');
      target.classList.remove('prev');
      target.classList.add('active');
    }

    this.currentSlide = index;
    this.updateCounter();

    setTimeout(() => {
      this.isTransitioning = false;
      // Reset non-active slides
      this.slides.forEach((slide, i) => {
        if (i !== this.currentSlide) {
          slide.classList.remove('active', 'prev');
        }
      });
    }, 600);
  }

  next() { this.goTo(this.currentSlide + 1); }
  prev() { this.goTo(this.currentSlide - 1); }

  updateCounter() {
    const counter = document.querySelector('.slide-counter');
    if (counter) counter.textContent = `${this.currentSlide + 1} / ${this.totalSlides}`;
  }

  toggleFullscreen() {
    if (!document.fullscreenElement) {
      document.documentElement.requestFullscreen();
    } else {
      document.exitFullscreen();
    }
  }
}

document.addEventListener('DOMContentLoaded', () => new Presentation());
```

### 4. 슬라이드 유형별 레이아웃

#### 타이틀 슬라이드 (첫 페이지)
- 중앙 정렬, 큰 제목 + 부제목 + 발표자 이름
- 배경: 그래디언트 또는 기하학적 패턴

#### 콘텐츠 슬라이드
- 왼쪽: 제목 + 본문 | 오른쪽: 이미지/차트/아이콘
- 또는 중앙 정렬 + 불릿 포인트 리스트

#### 데이터/비교 슬라이드
- CSS Grid 기반 카드형 레이아웃
- 2~4열 그리드, 각 카드에 아이콘 + 수치 + 설명

#### 마무리 슬라이드
- 중앙 정렬, "감사합니다" + 연락처
- 액센트 컬러 glow 효과

### 5. 사용자 지시 처리 규칙

| 사용자 요청 | 처리 방법 |
|---|---|
| "골드 테마" | `:root`에 골드 컬러 변수 적용 |
| "시안 테마" | `.theme-cyan` 클래스 적용 |
| "바이올렛 테마" | `.theme-violet` 클래스 적용 |
| "라이트 테마" | `.theme-light` 클래스 적용 |
| "N장으로 만들어줘" | 정확히 N개 슬라이드 생성 |
| "전체화면" | F키 전체화면 토글 기능 기본 포함 |
| "애니메이션 없이" | transition/animation 제거 |

### 6. 생성 결과물
- 파일명: `{주제}_presentation.html`
- 단일 HTML 파일 (인라인 CSS + JS)
- 브라우저에서 바로 열어서 사용 가능
- 키보드(←→), 버튼 클릭, 터치 스와이프 모두 지원

## 참조
- `scripts/template.html`: 기본 템플릿 파일
- `examples/sample.html`: 10페이지 골드 테마 샘플
