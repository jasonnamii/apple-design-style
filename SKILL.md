---
name: apple-box-design
description: |
  Apple Keynote 감성 박스·벤토 디자인. 블랙/화이트 극단 weight + 색상 3단(정보·캡션·장식) + 다크컨테이너 자동 역매핑. HTML·PDF·PPTX·옵시디언.
  P1: 애플스킬, 애플디자인, 애플박스, 애플박스디자인, 애플디자인스타일, 애플스타일, 키노트스타일, 미니멀디자인, 블랙화이트, 벤토, bento, 반응형애플, 모바일애플, 애플벤토.
  P2: 적용해줘, 만들어줘, apply, create.
  P3: apple skill, apple design, apple box, Apple Keynote, bento grid, dark container remap.
  P5: .html로, .pdf로, .pptx로, .md로.
  NOT: 일반HTML(→html-div-style), UI설계(→ui-action-designer).
"@uses":
  - references/mode-html-scroll.md
  - references/mode-html-bento.md
  - references/mode-pdf.md
  - references/mode-pptx.md
  - references/mode-obsidian.md
  - references/layout-safety.md
---

<!-- Trigger Conditions (moved from description for token compression)
P1: 애플디자인스타일, 애플스타일, 키노트스타일, 미니멀디자인, 블랙화이트, 벤토, bento.
P4: "애플 디자인 스타일" 명시 요청시에만 발동. 자동발동 없음.
P5: .html로, .pdf로, .pptx로, .md로.
NOT: 일반 옵시디언 문서(→마크다운 기본), mermaid(→직접수행)
-->

# Apple Box Design (애플 박스 디자인 / 애플 스킬)

Apple Keynote 감성의 미니멀 박스 디자인 언어. 블랙/화이트 + 5단계 폰트 스케일 + 극단적 weight 대비 + 벤토 그리드 박스 + 색상 3단 역매핑이 핵심. 콘텐츠 구조(BP, 보고서, 매뉴얼 등)는 자유 — 이 디자인 언어를 입히는 것이 목적.

**호출명:** 애플스킬 · 애플디자인 · 애플박스 · 애플박스디자인 · 애플디자인스타일 · 애플스타일 · 애플벤토 · 반응형애플 · 모바일애플 · 키노트스타일 · 미니멀디자인 · 블랙화이트 · 벤토 / bento. 하나라도 걸리면 발동.

---

## 라우팅

| 출력 모드 | 로드 대상 |
|-----------|-----------|
| HTML 풀페이지 스크롤 | → `references/mode-html-scroll.md` |
| HTML 벤토 그리드 | → `references/mode-html-bento.md` |
| HTML 레이아웃 붕괴 디버그·상세 | → `references/layout-safety.md` (HTML 출력 시 필수 대조) |
| PDF (reportlab) | → `references/mode-pdf.md` |
| PPTX (python-pptx) | → `references/mode-pptx.md` |
| 옵시디언 .md | → `references/mode-obsidian.md` |

**필요한 mode만 로드한다.** HTML 스크롤 작업 시 PPTX spoke를 로드할 필요 없다.

---

## 디자인 원칙

| 원칙 | 규칙 |
|------|------|
| 색상 | 블랙(`#000`, `#1d1d1f`) + 화이트(`#fff`, `#f5f5f7`). 컬러 금지 |
| 타이포 | Pretendard(전 모드 통일, 한글+영문). Black 950(제목) + Light 300(본문) 극단적 대비. HTML CDN: `https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable.min.css` |
| 여백 | 과감한 여백. 빈 공간 = 디자인 요소 |
| 사이즈 | 5단계: XL(80px) → L(48px) → M(28px) → S(18px) → XS(13px, 최소 가독성 하한). HTML은 모바일 우선 clamp 반응형 적용 (→ §반응형 원칙). XS 12px 이하 금지 |
| 강조 | bold(600-700)로만. 밑줄·색상·기울임 금지 |
| 구두점 | 제목 끝에 마침표(.) 권장. "Think Output." 패턴 사용시 필수 |
| 반응형 | HTML 출력시 모바일 우선. 3단계 브레이크포인트(≤640·641-1024·≥1025). 터치 타겟 ≥44px. 벤토 그리드는 모바일에서 1열로 붕괴 (→ §반응형 원칙) |

---

## 폰트 스케일 (5단계)

| 토큰 | 이름 | px | 용도 | weight |
|------|------|-----|------|--------|
| XL | 매우크게 | 80 | Think 타이틀, 히어로 | 950 (Black) |
| L | 크게 | 48 | 섹션 제목, 강조 문구 | 700-950 |
| M | 보통 | 28 | 본문, 설명 텍스트 | 300-400 |
| S | 작게 | 18 | 보조 설명, 캡션 | 300 |
| XS | 매우작게 | 13 | 라벨, 메타정보, 섹션헤더, 캡션 | 500-700 |

모드별 매핑: 스크롤HTML·벤토HTML 모두 clamp로 반응형 적용(모바일 우선), PDF는 pt(=px) 직접 적용, 옵시디언 .md는 기본 폰트 사용.

**HTML clamp 기본값** (모바일 → 데스크탑):
- XL: `clamp(48px, 8vw, 80px)` · L: `clamp(32px, 5vw, 48px)` · M: `clamp(20px, 2.5vw, 28px)` · S: `clamp(16px, 1.6vw, 18px)` · XS: `clamp(13px, 1vw, 14px)`

**가독성 하한 (필수):** XS는 모바일에서도 13px 밑으로 내려가지 않는다. S 본문은 16px 하한. 12px·11px 이하 고정값 금지(화면 DPI·사용자 뷰포트 확대 고려).

---

## 반응형 원칙 (HTML 전용)

Apple 스타일의 극단적 weight·여백은 모바일에서 깨지기 쉽다. **모바일 우선**으로 설계하고 데스크탑으로 확장한다.

### 브레이크포인트 3단계

| 단계 | 범위 | 기준 |
|------|------|------|
| 모바일 | ≤ 640px | 기본값. 1열 레이아웃, 패딩 축소 |
| 태블릿 | 641 ~ 1024px | 2열 허용, 여백 중간 |
| 데스크탑 | ≥ 1025px | 풀 위계, 벤토 3~4열, XL 폰트 |

### 모바일 필수 규칙

| 규칙 | 값 |
|------|-----|
| 터치 타겟 최소 | 44×44px (CTA·링크·버튼 전부) |
| 뷰포트 메타 | `<meta name="viewport" content="width=device-width, initial-scale=1">` 필수 |
| 패딩 축소 | 데스크탑 80~120px → 모바일 20~32px |
| 벤토 그리드 붕괴 | 데스크탑 3~4열 → 태블릿 2열 → 모바일 1열 |
| 폰트 clamp | 고정 px 금지. 위 XL~XS clamp 기본값 또는 변형 사용 |
| 히어로 XL | 모바일 80px 강행 금지. clamp 최소값 48px로 축소 |
| 횡스크롤 | 절대 발생 금지. 긴 테이블·이미지는 `overflow-x: auto` 또는 분할 |

### 모드별 반응형 상세

- **HTML 스크롤**: `mode-html-scroll.md` 참조. clamp + flexbox/grid min-content
- **HTML 벤토**: `mode-html-bento.md` 참조. `grid-template-columns: repeat(auto-fit, minmax(280px, 1fr))` 기본
- **PDF/PPTX/Obsidian**: 해당 없음 (고정 포맷)

---

## 레이아웃 붕괴 7대 원인 (HTML 전용 · 필수 체크)

벤토·그리드 설계 후 **제출 전 반드시 7대 전수 점검**. 하나라도 걸리면 모바일/태블릿에서 붕괴.

| # | 원인 | 증상 | 진단 | 처방 |
|---|------|------|------|------|
| 1 | **암시적 그리드 트랙** | base `.hero{grid-column:span 2}` + @media에서 리셋 누락 | 모바일에서 span 2 유지 → 횡스크롤 | base span 선언된 **모든 명명 선택자** 전수 열거 후 @media 1024·640에서 `span 2`·`span 1` 강제 |
| 2 | **CSS 특이도 역전** | @media 선언보다 뒤에 오는 일반 선택자가 더 구체 | 리셋 무시됨 | @media 내 선택자 특이도 ≥ base 선택자. 필요 시 `!important`(최후수단) 또는 선택자 체인 일치 |
| 3 | **flex 자식 `min-width:auto` 기본값** | flex 아이템이 콘텐츠보다 작게 수축 거부 | 카드가 부모 폭 초과 | `.flex-item { min-width: 0; }` 선언 필수 |
| 4a | **한글 세로 1글자 낙하 (치명)** | `word-break:break-word`·`break-all`을 한글에 적용 | "배우고, 결과물..." 세로 1자씩 떨어짐 | **한글 필수: `word-break: keep-all; overflow-wrap: break-word;`** (break-all·anywhere·break-word 단독 금지) |
| 4b | **긴 영문·URL·mono 텍스트** | 한글 처방과 혼용 | 영문 긴 단어 트랙 밀어냄 | 영문 전용 컨테이너에만 `overflow-wrap: anywhere`. 한글·혼용은 4a 규칙 우선 |
| 5 | **`white-space: nowrap` + 긴 텍스트** | `.mono`·태그·뱃지에 nowrap 박힘 | 단일 라인 강제 → 횡스크롤 | 장식용 외 nowrap 금지. 꼭 필요 시 `overflow: hidden; text-overflow: ellipsis; max-width:100%` 동반 |
| 6 | **이미지·테이블·iframe max-width 누락** | 원본 사이즈 고정 | 모바일에서 부모 폭 돌파 | `img,svg,video,iframe{max-width:100%; height:auto}` / `table{table-layout:fixed; width:100%}` |
| 7 | **패딩+폰트 고정px 누적** | card padding 44px + 폰트 28px + gap 24px | 360px 뷰포트에서 콘텐츠 영역 −값 | 모바일 패딩 20~24px로 축소, 폰트 clamp 강제 |

### 제출 전 5 체크포인트 (실측)

```
360px · 390px · 480px · 640px · 768px · 1024px
```

각 폭에서 `document.scrollWidth === window.innerWidth` 확인. 하나라도 `>` → 원인 7개 중 해당 항목 역추적.

### base span 선언 전수 열거 방법

```css
/* base에 span이 박힌 모든 선택자 grep */
grep -E "grid-column:\s*span" style.css
/* 결과의 모든 선택자를 @media에 복사 → span 값만 강제 치환 */
```

---

## 콘텐츠 적용

이 스킬은 **디자인 언어**. 콘텐츠 구조는 원본을 따른다.

### 적용 가능 콘텐츠 예시

사업계획서, 조직운영 매뉴얼, 보고서, 제안서, 온보딩 가이드, 제품소개 등 — 구조 무관.

### 콘텐츠 압축 규칙 (공통)

| Before | After |
|--------|-------|
| 긴 설명 문단 | 2줄 이내 서술 + 1줄 강조 |
| 번호 목록 5개+ | 플로우 화살표 1줄 또는 최대 4개 |
| "~하는 것이 중요하다" | "~다." 단언형 |
| 배경 설명 | 삭제. 결론만 |

### "Think [Word]." 패턴 (선택)

콘텐츠를 단어 하나로 압축한 섹션으로 분리할 때 사용. 사용자가 요청하거나 콘텐츠가 독립 섹션 나열형일 때 적합.

```
Think [핵심단어].
→ 서술 1줄 (gray, light)
→ 강조 1줄 (white/black, bold)
→ 플로우 (mono, dim)
→ 결론 1줄
```

---

## 색상 시스템 (3단 + 다크 역매핑 + inline 금지)

작은 글자의 "흐림"은 색상 혼용이 원인. **역할별 3단 고정 + CSS 변수 3분리 + 다크 컨테이너 자동 역매핑** 3중 방어.

### 1) 역할 3단 (필수 판정)

| 단계 | 라이트 HEX | 다크 HEX | weight | 용도 | 금지 용도 |
|------|-----------|---------|--------|------|----------|
| **Tier 1 정보성** | `#1d1d1f` | `#fff` | 500-700 | 정보성 라벨(섹션 라벨·표 행 라벨·카드 제목·항목명) | 장식·일련번호 |
| **Tier 2 캡션** | `#424245` | `#d1d1d6` | 400-500 | 캡션·사례·설명문·"타 산업 유사사례" 등 본문급 보조 | 본문 대체·다크배경 원색 사용 |
| **Tier 3 장식** | `#86868b` | `#86868b` | 400-500 | 일련번호(①②③④/01·02)·날짜·tag·장식 점 "·" | 정보성 라벨 |

**판정 기준:** "이 글자를 못 읽으면 정보 손실이 있는가?" Yes → Tier 1/2 / No → Tier 3.

**WCAG AA 본문 4.5:1:** `#424245` on `#f5f5f7` = 9.7:1 ✅ / `#86868b` on `#f5f5f7` = 3.5:1 ❌ (장식 한정).

### 2) CSS 변수 3분리 (필수 — `--muted` 단일 변수 FAIL)

```css
:root {
  /* 라이트 배경 기본값 */
  --label-info:    #1d1d1f;  /* Tier 1 */
  --label-caption: #424245;  /* Tier 2 */
  --label-deco:    #86868b;  /* Tier 3 */
  /* 액센트 (선택) */
  --accent-dark:   #002147;  /* Oxford Blue */
}
```

**왜 3분리:** `--muted` 하나에 1·2·3단을 몰아넣으면 다크 컨테이너 역매핑이 한 변수에 걸려 깨진다. 예: 다크 배경에서 `--muted:#fff`로 덮으면 장식까지 흰색이 되어 위계 붕괴. **변수별 독립 역매핑 필수.**

### 3) 다크 컨테이너 자동 역매핑 (치명 방어 — `#424245` on dark = FAIL)

**다크 컨테이너 식별자:** `.dark` · `.key` · `.hot` · `.now` · `.elev` · `.region.hot` · `.think.dark` · `[class*="dark"]` · Oxford Blue 배경(`#002147`) 클래스.

```css
/* 다크 컨테이너 진입 시 3 변수 전부 역매핑 */
.dark, .key, .hot, .now, .region.hot, .think.dark,
[style*="background:#002147"], [style*="background:#000"],
[style*="background:#1d1d1f"], [style*="background:#2d2d2d"] {
  --label-info:    #fff;     /* Tier 1 역매핑 */
  --label-caption: #d1d1d6;  /* Tier 2 역매핑 — #424245·#6e6e73 다크배경 금지 */
  --label-deco:    #86868b;  /* Tier 3 유지 (대비 충분) */
  color: var(--label-info);
}

/* 자식 요소는 variable 경유만 */
.dark .caption, .dark .case,        { color: var(--label-caption); }
.dark .deco, .dark .date, .dark .tag{ color: var(--label-deco); }
```

**다크 배경 허용 4색만:** `#fff` · `#d1d1d6` · `#86868b` · `#3a3a3c`. **`#424245`·`#6e6e73`·`#666`·`#888` 다크배경 전부 FAIL** (대비 ≤3:1).

**WCAG AA 다크 검증:** `#424245` on `#002147` = 2.4:1 ❌ / `#d1d1d6` on `#002147` = 11.8:1 ✅.

### 4) inline `style="color:..."` 금지 (치명)

**규칙:** 색상은 **변수·클래스 경유만**. inline `style="color:#xxx"` 선언 = FAIL.

**왜:** inline style은 CSS specificity 1000으로 다크 컨테이너 역매핑(0,0,1,0~0,0,2,0)을 **무조건 무효화**. 실제 KISAS_PLANNING_V2.html에서 `<div class="xs" style="color:#424245">`가 `.think.dark` 내부에서 진블루 위에 그대로 출력되어 가독성 붕괴.

```html
<!-- ❌ FAIL: inline이 역매핑 무력화 -->
<div class="case" style="color:#424245">타 산업 유사사례</div>

<!-- ✅ PASS: 클래스 + 변수 경유 -->
<div class="case">타 산업 유사사례</div>
<style>.case { color: var(--label-caption); }</style>
```

**예외:** 디자인 시스템 외 1회성 데모·프린트 전용 CSS만 허용. 프로덕션 문서 = 금지.

### 5) 출력 모드별 매핑 (PDF·PPTX·Obsidian)

| 역할 | 스크롤HTML | 벤토HTML | PDF (reportlab) | Obsidian(.md) |
|------|-----------|---------|-----|---|
| 배경 | `#000` | `#f5f5f7` | `(0,0,0)` | 마크다운 기본 |
| 박스 테두리 | — | `#e5e5ea` | — | `#e0e0e0` |
| Tier 1 정보성 | `#fff` | `#1d1d1f` | `(0.11,0.11,0.12)` | `#1d1d1f` |
| Tier 2 캡션 | `#d1d1d6` | `#424245` | `(0.26,0.26,0.27)` | `#424245` |
| Tier 3 장식 | `#86868b` | `#86868b` | `(0.52,0.52,0.54)` | `#86868b` |
| 강조 | `#fff` wght600 | `#1d1d1f` wght700 | `(1,1,1)` Bold | wght700 |
| 다크박스 배경 | — | `#1d1d1f`·`#002147` | — | `#2d2d2d`·`#002147` |
| 플로우(mono) | `#666` | `#6e6e73` | `(0.43,0.43,0.45)` | `#6e6e73` |

### 액센트 옵션 (형 명시 요청 시만)

기본 정체성은 블랙/화이트/그레이 극단 대비. 액센트 컬러는 형이 명시 요청할 때만 사용한다.

| 이름 | HEX | 용도 | 톤 |
|------|-----|------|-----|
| Oxford Blue | `#002147` | 박스 배경(다크 variant), CTA, 강조 테두리, 제목 배경 | 권위·신뢰·학술 |

**사용 규칙:**
- 1문서 1액센트만 (2종 이상 혼용 금지)
- 액센트 위 텍스트는 `#fff` (wght 600+) 또는 `#e0e0e0` (wght 300)
- 액센트 면적은 전체의 ≤ 20%. 주조는 블랙/화이트 유지
- 박스(다크) 역할을 Oxford Blue로 교체 가능: `#2d2d2d` → `#002147`

---

## 레이어링 원칙 (UP §H 준수)

html-div-style과 동일한 2층 구조. 이 스킬 = 2층(디자인 레이어). .md 출력 시 1층(md 네이티브) 선행 필수. HTML/PDF/PPTX는 해당 없음. 형 명시 요청 시 1층 없이 허용.

---

## 워크플로우

```
0. [.md 출력시] 1층 확인: md 네이티브(콜아웃 등) 존재 여부 확인. 없으면 → 형에게 "1층 md 네이티브를 먼저 깔까요?" 확인 (형 명시 요청 시 스킵. HTML/PDF/PPTX 출력 시 해당 없음)
1. 콘텐츠 수신 → 원본 구조 파악
2. 압축 규칙 적용 (결론 위주, 단언형)
3. Think패턴 적용 여부 판단 (사용자 요청 또는 나열형일 때)
4. 산출물 모드 선택 → 해당 mode spoke 로드
5. 해당 모드의 폰트 스케일 + 색상 팔레트 + 사양표 참조
6. 히어로 + 본문 + 클로징 구성
7. 서브에이전트 위임 시 렌더링 규칙 포함
```

---

## 검증 역할 분리

스타일 생성만 담당. 렌더링 검증은 UP §C.QC 파이프라인이 수행 (html-div-style과 동일 원칙).

---

## 체크리스트 (공통)

- [ ] 폰트 스케일 5단계(XL/L/M/S/XS) 준수, XS 13px 하한
- [ ] 색상 3단 분리: 정보성=`#1d1d1f` · 캡션=`#424245` · 장식=`#86868b`
- [ ] CSS 변수 3분리 (`--label-info` · `--label-caption` · `--label-deco`), `--muted` 단일 변수 없음
- [ ] 다크 컨테이너(`.dark`·`.key`·`.hot`·`.now`·`.region.hot`·`.think.dark`·Oxford Blue) 내부 자동 역매핑 CSS 존재
- [ ] 다크 배경 텍스트는 4색만 (`#fff`·`#d1d1d6`·`#86868b`·`#3a3a3c`). `#424245`·`#6e6e73` 다크배경 없음
- [ ] inline `style="color:#xxx"` 전수 0건 — 색상은 변수·클래스 경유만 (`grep -n 'style="[^"]*color:' *.html` = 0)
- [ ] 컬러 사용 없음 (블랙/화이트/그레이만)
- [ ] 제목 wght 950 (Black), 본문 wght 300 (Light) 대비
- [ ] 섹션당 텍스트 4줄 이내
- [ ] 히어로 + 클로징 존재
- [ ] 플로우 화살표(→) 사용
- [ ] 여백 충분 (빈 공간 > 콘텐츠 면적)
- [ ] [HTML] viewport 메타 태그 존재
- [ ] [HTML] 폰트 clamp 반응형 적용 (고정 px 금지)
- [ ] [HTML] 모바일(≤640px)에서 1열 붕괴·횡스크롤 없음
- [ ] [HTML] 터치 타겟 ≥44px
- [ ] [HTML] 레이아웃 7대 원인 전수 점검 (암시적트랙·특이도·min-width:auto·word-break·nowrap·max-width·패딩누적)
- [ ] [HTML] 5 폭(360·390·480·640·768·1024) 횡스크롤 실측 0
- [ ] [HTML] `img,svg,video,iframe{max-width:100%}` 선언
- [ ] [HTML] **한글 `word-break: keep-all; overflow-wrap: break-word`** (break-word·anywhere·break-all 단독 금지)
- [ ] [HTML] flex·grid 자식 `min-width: 0` (콘텐츠 수축 허용)
- [ ] [HTML] body·html `overflow-x: hidden` 금지 (원인 은폐. 실제 수정 필요)

---

## Gotchas

- **div 속성값 불일치:** 외곽 div와 내부 div의 border-radius/padding 값을 임의로 변경하는 실수. 반드시 디자인 시스템 값(외곽 12px/32px 40px, 내부 8px/12px)을 고정 사용. "비슷하게"가 아니라 정확히 일치해야 함.
- **옵시디언 div 렌더링:** .md 출력 시 html-div-style의 obsidian-rules(빈줄 금지, HTML 태그만, 색상 명시 등)를 동일하게 적용. 해당 규칙의 상세는 html-div-style 스킬을 참조.
- **모바일에서 XL 80px 강행:** 히어로 폰트를 고정 80px로 두면 모바일에서 가로 넘침·줄바꿈 대참사. clamp 최소값 48px로 축소 필수.
- **벤토 그리드 고정열:** `grid-template-columns: 1fr 1fr 1fr 1fr` 같은 고정 4열은 모바일에서 깨짐. `repeat(auto-fit, minmax(280px, 1fr))` 또는 미디어쿼리 필수.
- **명시적 span 리셋 누락 (벤토 최빈 함정):** `.col-3,.col-4{grid-column:span N}` 유틸만 리셋하고 `.hero{span 2}`·`.section-head{span 4}`·`.closing{span 4}`·`.elev{span 3}`·`.think{span 2}` 같은 **명명 컴포넌트의 span 선언**을 @media에서 리셋 안 하면, 자식 카드가 **암시적 그리드 트랙**을 생성해 모바일에서도 4열 유지. 시각 발현: "카드가 화면 밖으로 밀려 잘림". 규칙: base에 `grid-column:span` 값을 준 **모든 선택자**를 1024px(≤span 2)·640px(span 1)에서 전수 리셋. 실제 사례: KISAS_PLANNING_V2.html 2026-04-18 발견.
- **viewport 메타 누락:** HTML 출력 시 `<meta name="viewport" content="width=device-width, initial-scale=1">` 없으면 모바일에서 데스크탑 뷰로 축소렌더링 → 글자 좁쌀. 필수 삽입.
- **과도한 패딩 모바일 전파:** 데스크탑 80~120px 패딩을 모바일에서 그대로 쓰면 콘텐츠 영역이 휴대폰 화면의 20%만 남음. 미디어쿼리로 20~32px로 축소.
- **XS 12px + muted 색상 3중 약화:** `font-size:12px` + `font-weight:300~400` + `color:#86868b`를 캡션·설명·사례에 함께 쓰면 읽기 불가 수준으로 흐림. 실제 사례: KISAS_PLANNING_V2.html 2026-04-21 보고. 규칙: XS 13px 하한 · weight 500 이상 · 캡션은 `#424245`(Tier 2). 애플 원본은 이 3중 약화를 "장식 메타(날짜·번호)"에만 국한.
- **진블루 위 `#424245`·`#6e6e73` (치명):** Oxford Blue `#002147` 위에 Tier 2 라이트값 `#424245` 그대로 쓰면 대비 2.4:1 — WCAG AA FAIL. 증상: "진블루 박스 안에 뭐가 써있긴 한데 안 읽힘". 규칙: 다크 컨테이너(`.dark`·`.hot`·`.key`·`.now`·Oxford Blue) 내부는 **Tier 2 자동 역매핑 `#d1d1d6`**. 3 CSS 변수 분리 필수(하나로 묶으면 장식까지 흰색 되어 위계 붕괴).
- **inline `style="color:..."` 선언 (치명):** inline specificity 1000이 다크 컨테이너 역매핑(0,0,1,0~0,0,2,0)을 **무조건 무력화**. `<div class="xs" style="color:#424245">`를 `.think.dark` 자식으로 넣으면 역매핑 CSS 무시되고 진블루 위 진한회색 그대로 출력. 규칙: **inline style 색상 선언 0건**. 색상은 `var(--label-*)` 경유만. 실제 사례: KISAS_PLANNING_V2.html 2026-04-21 라인 488.
- **`--muted` 단일 변수 설계 (설계 실패):** Tier 1/2/3를 한 변수에 몰면 다크 역매핑이 한 변수에만 걸려 위계 3단이 2단(또는 1단)으로 붕괴. 예: `--muted:#fff`로 다크 역매핑 → 정보성·캡션·장식 전부 흰색 = 위계 사라짐. 규칙: `--label-info`·`--label-caption`·`--label-deco` 3개로 분리해 각각 독립 역매핑.
