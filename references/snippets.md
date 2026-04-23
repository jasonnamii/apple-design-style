# snippets.md — apple-box-design 스니펫 라이브러리

이 스킬 **유일한 고유물**. 벤토 그리드·극단 weight·다크 역매핑·Think 패턴.

> 모드별 풀스펙: `mode-html-scroll.md` · `mode-html-bento.md` · `mode-pdf.md` · `mode-pptx.md` · `mode-obsidian.md`
> 레이아웃 상세: `layout-safety.md`

---

## 모드 인덱스

| 출력 모드 | 로드 |
|---|---|
| HTML 풀페이지 스크롤 | `mode-html-scroll.md` |
| HTML 벤토 그리드 | `mode-html-bento.md` |
| HTML 디버그 | `layout-safety.md` |
| PDF (reportlab) | `mode-pdf.md` |
| PPTX (python-pptx) | `mode-pptx.md` |
| 옵시디언 .md | `mode-obsidian.md` |

**필요한 mode만 로드.**

---

## 색상 시스템 (CSS 변수 + 다크 자동 역매핑)

```css
:root {
  --label-info:    #1d1d1f;
  --label-caption: #424245;
  --label-deco:    #86868b;
  --accent-dark:   #002147;
}

/* 다크 컨테이너 진입 시 3 변수 전부 역매핑 */
.dark, .key, .hot, .now, .region.hot, .think.dark,
[style*="background:#002147"], [style*="background:#000"],
[style*="background:#1d1d1f"], [style*="background:#2d2d2d"] {
  --label-info:    #fff;
  --label-caption: #d1d1d6;  /* #424245·#6e6e73 다크 금지 */
  --label-deco:    #86868b;
  color: var(--label-info);
}

.dark .caption, .dark .case         { color: var(--label-caption); }
.dark .deco, .dark .date, .dark .tag{ color: var(--label-deco); }
```

**다크 컨테이너 식별자:** `.dark`·`.key`·`.hot`·`.now`·`.elev`·`.region.hot`·`.think.dark`·`[class*="dark"]`·Oxford Blue 배경.

**다크 허용 4색:** `#fff`·`#d1d1d6`·`#86868b`·`#3a3a3c`.

---

## 히어로 블록 (XL 타이틀)

```html
<section class="hero">
  <h1 class="title-xl">Think Output.</h1>
  <p class="subtitle-m">결과가 말한다.</p>
</section>

<style>
.title-xl {
  font-size: clamp(48px, 8vw, 80px);  /* 하한 ≥40px */
  font-weight: 950;
  letter-spacing: -0.02em;
  color: var(--label-info);
  word-break: keep-all;
  overflow-wrap: break-word;
}
.subtitle-m {
  font-size: clamp(20px, 2.5vw, 28px);
  font-weight: 300;
  color: var(--label-caption);
}
</style>
```

## 벤토 그리드 (반응형 안전)

```html
<section class="bento">
  <article class="box key">...</article>  <!-- 다크 강조 -->
  <article class="box">...</article>
  <article class="box">...</article>
  <article class="box">...</article>
</section>

<style>
.bento {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));  /* auto-fit */
  gap: 24px;
}
.box {
  min-width: 0;          /* grid item 오버플로우 방지 */
  overflow: hidden;
  padding: clamp(20px, 4vw, 80px);
  border-radius: 12px;
  background: #fff;
}
.box.key {
  background: var(--accent-dark);  /* Oxford Blue */
  color: #fff;
}

/* 명시적 span 리셋 (@media에서 전수) */
@media (max-width: 1024px) {
  .hero, .section-head, .closing, .elev, .think { grid-column: span 2; }
}
@media (max-width: 640px) {
  .hero, .section-head, .closing, .elev, .think { grid-column: span 1; }
}
</style>
```

**명시적 repeat(N) 사용 시:** `repeat(N, minmax(0, 1fr))` 필수 (단독 `1fr` 금지).

## "Think [Word]." 패턴

```
Think [핵심단어].
→ 서술 1줄 (gray, light)
→ 강조 1줄 (white/black, bold)
→ 플로우 (mono, dim)
→ 결론 1줄
```

```html
<div class="think dark">
  <h2 class="think-word">Think Output.</h2>
  <p class="caption">과정은 기록된다.</p>
  <p class="accent">결과가 말한다.</p>
  <p class="flow">계획 → 실행 → 검증 → 증거</p>
  <p class="conclude">그래서 만든다.</p>
</div>
```

## 연속 카드 (옵시디언 .md 출력 시)

```html
<div style="padding:24px;border-radius:12px;background:#f5f5f7;">
<p style="color:#1d1d1f;font-size:22px;font-weight:700;">카드 A</p>
<p style="color:#424245;">본문</p>
</div>

<br>

<div style="padding:24px;border-radius:12px;background:#f5f5f7;">
<p style="color:#1d1d1f;font-size:22px;font-weight:700;">카드 B</p>
</div>
```

→ html-div-style/references/forbidden.md §옵시디언 14금칙 준수.

## 다크 박스 (Oxford Blue)

```html
<div style="padding:32px;border-radius:16px;background:#002147;">
<p style="color:#fff;font-size:28px;font-weight:700;">강조 제목</p>
<p style="color:#d1d1d6;font-size:18px;">캡션 (Tier 2 다크 역매핑)</p>
<p style="color:#86868b;font-size:13px;">메타 (Tier 3)</p>
</div>
```

---

## 모드별 스펙 요약

| 모드 | 배경 | 기본 텍스트 | 포인트 |
|---|---|---|---|
| HTML 스크롤 | `#000` | `#fff` | 섹션 풀스크린·극단 여백 |
| HTML 벤토 | `#f5f5f7` | `#1d1d1f` | 그리드·auto-fit·다크 박스 강조 |
| PDF | `(0,0,0)` | `(1,1,1)` | 고정 pt·Pretendard 임베딩 |
| PPTX | 흰/검 교차 | 역매핑 | 정적 캡처·flex 2단 이내 |
| Obsidian .md | 기본 | `#1d1d1f` | 14금칙·div 래퍼 |

풀스펙: 각 `mode-*.md` 참조.

## UX 원리 준수

| 원리 | 반영 |
|---|---|
| N4 CONSISTENCY | 5단 스케일·3색 Tier 고정 |
| N6 RECOGNITION | Pretendard·Oxford Blue 액센트 |
| N8 MINIMAL | 3색·여백 > 콘텐츠·극단 weight |

허브: `→ 공통 참조는 별도 ux 허브 미포함 (이 스킬은 Apple 브랜드 시스템 독립)`.
