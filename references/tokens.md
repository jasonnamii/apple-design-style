# tokens.md — apple-box-design 토큰

Apple Keynote 감성 블랙/화이트 + 극단 weight + 색상 3단. HTML·PDF·PPTX·옵시디언 공통 토큰.

> 공통 토큰: `VAULT/_skills research/html-skill-refactor/spine.md §공통 토큰`
> 축1 디테일: `VAULT/_skills research/html-skill-refactor/axis1-css-tokens.md`

---

## 타이포 (5단계 스케일 + 극단 weight)

| 토큰 | 이름 | px | weight | 용도 |
|---|---|---|---|---|
| XL | 매우크게 | 80 | 950 (Black) | Think 타이틀·히어로 |
| L | 크게 | 48 | 700-950 | 섹션 제목·강조 |
| M | 보통 | 28 | 300-400 | 본문·설명 |
| S | 작게 | 18 | 300 | 보조·캡션 |
| XS | 매우작게 | 13 (하한) | 500-700 | 라벨·메타 |

**극단 weight 원칙:** 950 (Black) + 300 (Light). 중간 weight(400~700) 장식 전용. 밑줄·색상·기울임 강조 금지.

**폰트:** Pretendard 전 모드 통일. HTML CDN:
`https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable.min.css`

### HTML clamp 기본값 (mobile-first)

| 토큰 | clamp |
|---|---|
| XL | `clamp(48px, 8vw, 80px)` |
| L | `clamp(32px, 5vw, 48px)` |
| M | `clamp(20px, 2.5vw, 28px)` |
| S | `clamp(16px, 1.6vw, 18px)` |
| XS | `clamp(13px, 1vw, 14px)` |

**하한 철칙:** 히어로 ≥40px·섹션 타이틀 ≥26px·S 본문 ≥16px·XS ≥13px. 12px 이하 고정값 금지.

## 간격·여백

| 용도 | 값 |
|---|---|
| 카드 padding 데스크탑 | 80~120 |
| 카드 padding 모바일 | 20~32 |
| 그리드 gap | 24 / 32 / 48 |
| 외곽 div radius | 12 / 32 / 40 |
| 내부 div radius | 8 / 12 |

**여백 = 디자인 요소.** 빈 공간 > 콘텐츠 면적이 기본.

## 색 — 역할 3단 (필수 판정)

| 단계 | 라이트 HEX | 다크 HEX | weight | 용도 |
|---|---|---|---|---|
| **Tier 1 정보성** | `#1d1d1f` | `#fff` | 500-700 | 섹션 라벨·카드 제목·항목명 |
| **Tier 2 캡션** | `#424245` | `#d1d1d6` | 400-500 | 캡션·사례·설명문 |
| **Tier 3 장식** | `#86868b` | `#86868b` | 400-500 | 일련번호·날짜·tag |

**판정 기준:** "이 글자를 못 읽으면 정보 손실 있는가?" Yes → Tier 1/2 / No → Tier 3.

**WCAG AA:** Tier 2 `#424245` on `#f5f5f7` = 9.7:1 ✅ / Tier 3 `#86868b` on `#f5f5f7` = 3.5:1 ❌(장식 한정).

### CSS 변수 3분리 (필수, `--muted` 단일 변수 금지)

```css
:root {
  --label-info:    #1d1d1f;
  --label-caption: #424245;
  --label-deco:    #86868b;
  --accent-dark:   #002147;  /* Oxford Blue */
}
```

상세: `→ snippets.md §색상 시스템` · 다크 역매핑 `→ forbidden.md §inline 색상`.

## 액센트 팔레트 (등록)

| 이름 | HEX | 용도 | 톤 |
|---|---|---|---|
| Oxford Blue | `#002147` | 박스 배경(다크), CTA, 강조 테두리, 제목 배경 | 권위·신뢰·학술 |

**규칙:** 1문서 1액센트. 액센트 면적 ≤20%. 액센트 위 텍스트 `#fff`(wght600+) 또는 `#e0e0e0`(wght300).

## 브레이크포인트 (HTML)

| 단계 | 범위 | 기준 |
|---|---|---|
| 모바일 | ≤640px | 1열·패딩 축소 |
| 태블릿 | 641~1024px | 2열·중간 여백 |
| 데스크탑 | ≥1025px | 3~4열 벤토·XL 폰트 |

터치 타겟 ≥44×44px.

## PDF·PPTX·Obsidian 토큰 매핑

| 역할 | 스크롤HTML | 벤토HTML | PDF (rgb 0-1) | Obsidian(.md) |
|---|---|---|---|---|
| 배경 | `#000` | `#f5f5f7` | `(0,0,0)` | 기본 |
| 박스 테두리 | — | `#e5e5ea` | — | `#e0e0e0` |
| Tier 1 | `#fff` | `#1d1d1f` | `(0.11,0.11,0.12)` | `#1d1d1f` |
| Tier 2 | `#d1d1d6` | `#424245` | `(0.26,0.26,0.27)` | `#424245` |
| Tier 3 | `#86868b` | `#86868b` | `(0.52,0.52,0.54)` | `#86868b` |
| 강조 | `#fff` wght600 | `#1d1d1f` wght700 | `(1,1,1)` Bold | wght700 |
| 다크박스 배경 | — | `#1d1d1f`·`#002147` | — | `#2d2d2d`·`#002147` |
| 플로우(mono) | `#666` | `#6e6e73` | `(0.43,0.43,0.45)` | `#6e6e73` |

## 금지 토큰

| 토큰 | 이유 |
|---|---|
| 컬러 일반 (블랙/화이트/그레이 외) | Apple 정체성 이탈 — Oxford Blue 액센트만 예외 |
| `font-family` Pretendard 외 | 통일성 |
| 고정 px 히어로 (80px 강행) | 모바일 붕괴 |
| `repeat(N, 1fr)` 단독 | grid item 오버플로우 |
| inline `style="color:…"` | 다크 역매핑 무력화 |
| `--muted` 단일 변수 | 3단 위계 붕괴 |

상세 금지 사유: `→ forbidden.md`.
