---
name: apple-design-style
description: |
  Apple Keynote 감성 미니멀 디자인 시스템. 블랙/화이트 기반 극단적 weight 대비. HTML·PDF·PPTX·옵시디언 산출물 생성. 모바일 반응형 기본 포함(모바일 우선, clamp 폰트, 3단계 브레이크포인트). '애플 디자인 스타일' 명시 요청시에만 발동.
  P1: 애플디자인스타일, 애플스타일, 키노트스타일, 미니멀디자인, 블랙화이트, 벤토, bento, 반응형애플, 모바일애플.
  P2: 적용해줘, 만들어줘, apply, create.
  P3: Apple design, Keynote style, minimal design system, responsive, mobile-first.
  P5: .html로, .pdf로, .pptx로, .md로.
  NOT: 일반HTML디자인(→html-div-style), UI설계(→ui-action-designer).
"@uses":
  - references/mode-html-scroll.md
  - references/mode-html-bento.md
  - references/mode-pdf.md
  - references/mode-pptx.md
  - references/mode-obsidian.md
---

<!-- Trigger Conditions (moved from description for token compression)
P1: 애플디자인스타일, 애플스타일, 키노트스타일, 미니멀디자인, 블랙화이트, 벤토, bento.
P4: "애플 디자인 스타일" 명시 요청시에만 발동. 자동발동 없음.
P5: .html로, .pdf로, .pptx로, .md로.
NOT: 일반 옵시디언 문서(→마크다운 기본), mermaid(→직접수행)
-->

# Apple Design Style

Apple Keynote 감성의 미니멀 디자인 언어. 블랙/화이트 + 5단계 폰트 스케일 + 극단적 weight 대비가 핵심. 콘텐츠 구조(BP, 보고서, 매뉴얼 등)는 자유 — 이 디자인 언어를 입히는 것이 목적.

---

## 라우팅

| 출력 모드 | 로드 대상 |
|-----------|-----------|
| HTML 풀페이지 스크롤 | → `references/mode-html-scroll.md` |
| HTML 벤토 그리드 | → `references/mode-html-bento.md` |
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
| 사이즈 | 5단계: XL(80px) → L(48px) → M(28px) → S(18px) → XS(12px). HTML은 모바일 우선 clamp 반응형 적용 (→ §반응형 원칙) |
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
| XS | 매우작게 | 12 | 라벨, 메타정보, 섹션헤더 | 400-600 |

모드별 매핑: 스크롤HTML·벤토HTML 모두 clamp로 반응형 적용(모바일 우선), PDF는 pt(=px) 직접 적용, 옵시디언 .md는 기본 폰트 사용.

**HTML clamp 기본값** (모바일 → 데스크탑):
- XL: `clamp(48px, 8vw, 80px)` · L: `clamp(32px, 5vw, 48px)` · M: `clamp(20px, 2.5vw, 28px)` · S: `clamp(15px, 1.6vw, 18px)` · XS: `clamp(11px, 1vw, 12px)`

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

## 색상 팔레트

| 역할 | 스크롤HTML | 벤토HTML | PDF | Obsidian(.md) |
|------|-----------|---------|-----|---|
| 배경 | `#000` | `#f5f5f7` | `(0,0,0)` | 투명(마크다운 기본) |
| 박스(화이트) | — | — | — | `#fff` + border `#e0e0e0` |
| 박스(그레이) | — | — | — | `#f5f5f7` + border `#e0e0e0` |
| 박스(다크) | — | — | — | `#2d2d2d` + text `#fff` |
| 제목 | `#fff` | `#1d1d1f` | `(1,1,1)` | `#1d1d1f` (박스 바깥) |
| 본문 | `#ccc` | `#1d1d1f` | `(0.5,0.5,0.5)` | `#1d1d1f` (박스 내) |
| 강조 | `#fff` wght600 | `#1d1d1f` wght700 | `(1,1,1)` Bold | `#fff` (다크박스) / `#1d1d1f` (밝은박스) |
| 보조 | `#888` | `#86868b` | `(0.28,0.28,0.28)` | `#86868b` |
| 플로우 | `#666` | `#86868b` | `(0.28,0.28,0.28)` | `#666` |
| 구분 | `#1a1a1a` | `#e5e5ea` | — | `#e0e0e0` (박스 테두리) |

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

- [ ] 폰트 스케일 5단계(XL/L/M/S/XS) 준수
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

---

## Gotchas

- **div 속성값 불일치:** 외곽 div와 내부 div의 border-radius/padding 값을 임의로 변경하는 실수. 반드시 디자인 시스템 값(외곽 12px/32px 40px, 내부 8px/12px)을 고정 사용. "비슷하게"가 아니라 정확히 일치해야 함.
- **옵시디언 div 렌더링:** .md 출력 시 html-div-style의 obsidian-rules(빈줄 금지, HTML 태그만, 색상 명시 등)를 동일하게 적용. 해당 규칙의 상세는 html-div-style 스킬을 참조.
- **모바일에서 XL 80px 강행:** 히어로 폰트를 고정 80px로 두면 모바일에서 가로 넘침·줄바꿈 대참사. clamp 최소값 48px로 축소 필수.
- **벤토 그리드 고정열:** `grid-template-columns: 1fr 1fr 1fr 1fr` 같은 고정 4열은 모바일에서 깨짐. `repeat(auto-fit, minmax(280px, 1fr))` 또는 미디어쿼리 필수.
- **명시적 span 리셋 누락 (벤토 최빈 함정):** `.col-3,.col-4{grid-column:span N}` 유틸만 리셋하고 `.hero{span 2}`·`.section-head{span 4}`·`.closing{span 4}`·`.elev{span 3}`·`.think{span 2}` 같은 **명명 컴포넌트의 span 선언**을 @media에서 리셋 안 하면, 자식 카드가 **암시적 그리드 트랙**을 생성해 모바일에서도 4열 유지. 시각 발현: "카드가 화면 밖으로 밀려 잘림". 규칙: base에 `grid-column:span` 값을 준 **모든 선택자**를 1024px(≤span 2)·640px(span 1)에서 전수 리셋. 실제 사례: KISAS_PLANNING_V2.html 2026-04-18 발견.
- **viewport 메타 누락:** HTML 출력 시 `<meta name="viewport" content="width=device-width, initial-scale=1">` 없으면 모바일에서 데스크탑 뷰로 축소렌더링 → 글자 좁쌀. 필수 삽입.
- **과도한 패딩 모바일 전파:** 데스크탑 80~120px 패딩을 모바일에서 그대로 쓰면 콘텐츠 영역이 휴대폰 화면의 20%만 남음. 미디어쿼리로 20~32px로 축소.
