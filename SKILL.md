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
  - references/tokens.md
  - references/snippets.md
  - references/forbidden.md
  - references/qc.md
---

<!-- Trigger Conditions
P1: 애플디자인스타일, 애플스타일, 키노트스타일, 미니멀디자인, 블랙화이트, 벤토, bento.
P4: "애플 디자인 스타일" 명시 요청 시에만 발동. 자동발동 없음.
P5: .html로, .pdf로, .pptx로, .md로.
NOT: 일반 옵시디언 문서(→마크다운 기본), mermaid(→직접수행).
-->

# Apple Box Design (애플 스킬)

Apple Keynote 감성의 미니멀 박스 디자인 언어. 블랙/화이트 + 5단계 폰트 스케일 + **극단 weight 대비**(950 + 300) + 벤토 그리드 + **색상 3단 역매핑**이 핵심. 콘텐츠 구조(BP·보고서·매뉴얼 등) 자유 — 이 디자인 언어를 입히는 것이 목적.

**호출명:** 애플스킬·애플디자인·애플박스·애플박스디자인·애플디자인스타일·애플스타일·애플벤토·반응형애플·모바일애플·키노트스타일·미니멀디자인·블랙화이트·벤토/bento.

---

## 4블록 참조 구조

| 블록 | 파일 | 역할 |
|---|---|---|
| 토큰 | `references/tokens.md` | 5단 타이포·3단 색·액센트·브레이크포인트·모드별 매핑 |
| 스니펫 | `references/snippets.md` | 히어로·벤토·Think 패턴·다크 역매핑 · (→ mode-*.md 모드별 풀스펙) |
| 금칙 | `references/forbidden.md` | 전역·HTML 레이아웃 11대·PPTX 변환·옵시디언 금칙 |
| QC | `references/qc.md` | 6계층 스코어카드·모드별 전수 체크·자동 QC 게이트 |

공통 스파인: `VAULT/_skills research/html-skill-refactor/spine.md`.

---

## 라우팅

### 출력 모드 선택

| 출력 모드 | 로드 |
|---|---|
| HTML 풀페이지 스크롤 | `mode-html-scroll.md` |
| HTML 벤토 그리드 | `mode-html-bento.md` |
| HTML 레이아웃 디버그 | `layout-safety.md` (HTML 출력 시 필수 대조) |
| PDF (reportlab) | `mode-pdf.md` |
| PPTX (python-pptx) | `mode-pptx.md` |
| 옵시디언 .md | `mode-obsidian.md` |

**필요한 모드만 로드.** HTML 스크롤 작업 시 PPTX 로드 불필요.

### 로드 최소화

| 상황 | 로드 순서 |
|---|---|
| 스타일 적용 | snippets.md → 해당 mode-*.md |
| 검증까지 | + forbidden.md → qc.md |
| 신규 값 정의 | + tokens.md (금지 토큰 확인) |
| HTML 레이아웃 디버그 | + layout-safety.md |

---

## 디자인 원칙

| 원칙 | 규칙 |
|---|---|
| 색상 | 블랙(`#000·#1d1d1f`) + 화이트(`#fff·#f5f5f7`). 컬러 금지 — Oxford Blue 액센트 예외 |
| 타이포 | Pretendard 전 모드 통일. Black 950(제목) + Light 300(본문) 극단 대비 |
| 여백 | 과감한 여백. 빈 공간 = 디자인 요소 |
| 사이즈 | 5단(XL 80·L 48·M 28·S 18·XS 13). HTML은 clamp 반응형. XS 13px 하한 |
| 강조 | bold(600-700)로만. 밑줄·색상·기울임 금지 |
| 구두점 | 제목 끝 마침표(.) 권장 ("Think Output." 패턴) |
| 반응형 | HTML mobile-first. 3 브레이크포인트(≤640·641-1024·≥1025). 터치 ≥44px |

**타이포 스케일 상세·clamp 기본값:** `→ tokens.md §타이포`.

---

## 색상 시스템 (3단 Tier + 다크 역매핑)

| Tier | 라이트 | 다크 | weight | 용도 |
|---|---|---|---|---|
| 1 정보성 | `#1d1d1f` | `#fff` | 500-700 | 라벨·카드 제목 |
| 2 캡션 | `#424245` | `#d1d1d6` | 400-500 | 캡션·사례·설명 |
| 3 장식 | `#86868b` | `#86868b` | 400-500 | 일련번호·날짜·tag |

**CSS 변수 3분리 필수**(`--label-info·-caption·-deco`). 단일 `--muted` 변수 = FAIL (위계 붕괴).

**다크 컨테이너 자동 역매핑 + 금지 색:** `→ snippets.md §색상 시스템` · `→ forbidden.md §HTML 색상`.

### 액센트 (등록)

| 이름 | HEX | 용도 |
|---|---|---|
| Oxford Blue | `#002147` | 다크 박스 배경·CTA·강조 테두리 |

1문서 1액센트. 면적 ≤20%. 상세: `→ tokens.md §액센트 팔레트`.

---

## 레이어링 (1층·2층)

html-div-style과 동일 2층 구조. 이 스킬 = 2층(디자인 레이어).

| 층 | 담당 | 적용 범위 |
|---|---|---|
| 1층 | design-skill 이쁘니 (md 네이티브) | **.md 출력 시만** |
| 2층 | **이 스킬** | 전 모드 |

**규칙:** .md 출력 시만 1층 먼저 확인. HTML/PDF/PPTX는 해당 없음. 형 명시 요청 시 1층 스킵 허용.

---

## 워크플로우

```
0. [.md 출력시] 1층 확인 (md 네이티브 존재 여부)
1. 콘텐츠 수신 → 원본 구조 파악
2. 압축 (결론 위주·단언형·섹션 4줄 이내)
3. Think 패턴 여부 판단
4. 산출물 모드 선택 → 해당 mode-*.md 로드
5. 토큰·스니펫 참조 → 히어로 + 본문 + 클로징 구성
6. [HTML] 레이아웃 11대 전수 + 5폭 실측 + 자동 QC
7. 6계층 스코어카드 합격 확인
```

---

## 핵심 제약 (HTML 최빈 치명 6)

| 원인 | 금칙 |
|---|---|
| `repeat(N, 1fr)` 단독 | forbidden §HTML 레이아웃 11대 #8 → `minmax(0, 1fr)` |
| inline `style="font-size:clamp(...)"` | #9 → 클래스 경유 |
| inline `style="color:..."` | §HTML 색상 → 변수·클래스 경유 |
| 다크 배경 `#424245` | §HTML 색상 → Tier 2 자동 역매핑 `#d1d1d6` |
| 히어로 clamp 하한 375px 미역산 | #11 → 히어로 ≥40px·섹션 ≥26px |
| 한글 `break-word`·`break-all` 단독 | #4a → `keep-all; overflow-wrap: break-word` |

전수: `→ forbidden.md §HTML 레이아웃 11대`.

---

## 콘텐츠 압축 규칙

| Before | After |
|---|---|
| 긴 설명 문단 | 2줄 서술 + 1줄 강조 |
| 번호 목록 5개+ | 플로우 화살표 1줄 또는 최대 4개 |
| "~하는 것이 중요하다" | "~다." 단언형 |
| 배경·서론 | 삭제·결론만 |

"Think [Word]." 패턴 예시: `→ snippets.md §Think 패턴`.

---


## §INV NO_WORK_LABEL (산출물·대화 본질 보호)

| 항목 | 정의 |
|------|------|
| RULE | 산출물·대화 = 인간 언어. 작업 라벨 ZERO. (1만 페이지 1단어 = FAIL) |
| 판정 | "이 단어, 이 대화 밖 사람이 사전 없이 읽을 수 있나?" NO → 작업 라벨 → 금지 |
| ALLOW | 업계 전문용어(CSS·HTML·SVG·CSS변수·flexbox·grid) · 고유명사(Apple·Keynote) |
| CONVERT | 라벨 발견 → 실명·평문 풀어쓰기. 예) "벤토·다크컨테이너·역매핑·C8/C9" → 결과만 노출(코드명 ✗) |
| SELF_CHECK | HTML·PDF·PPTX 출력 직전에서 자체 스캔. 1개라도 발견 = 차단·재작성. paper-engine cascade 경유 시 INV 13 자동 적용 |

---

## Gotchas

- **div 속성값 임의 변경:** 외곽 radius 12/32/40, 내부 8/12 고정. "비슷하게" ✗ — 정확히 일치.
- **옵시디언 div 렌더링:** .md 출력 시 html-div-style `forbidden.md §옵시디언 14금칙` 동일 적용.
- **모바일 XL 80px 강행:** 히어로 고정 80px = 가로 넘침. clamp 최소 48px.
- **벤토 고정열 (`1fr 1fr 1fr 1fr`):** 모바일 붕괴. `repeat(auto-fit, minmax(280px, 1fr))` 또는 미디어쿼리.
- **명시적 span 리셋 누락 (벤토 최빈):** `.hero·.section-head·.closing·.elev·.think` 등 모든 명명 선택자를 @media 1024·640에서 전수 리셋.
- **viewport 메타 누락:** 모바일 좁쌀 렌더. `<meta name="viewport" content="width=device-width, initial-scale=1">` 필수.
- **과도한 패딩 모바일 전파:** 데스크탑 80~120 → 모바일 20~32.
- **XS 12px + muted + weight 300 3중 약화:** 읽기 불가. XS 13 하한 + weight 500+ + Tier 2 `#424245`.
- **진블루 위 `#424245`·`#6e6e73`:** 대비 2.4:1 FAIL. Tier 2 자동 역매핑 `#d1d1d6`.
- **inline `style="color:…"`:** specificity 1000이 다크 역매핑 무력화. 변수·클래스 경유만.
- **`--muted` 단일 변수:** 위계 3단 붕괴. 3 변수 독립 분리.
- **`repeat(N, 1fr)` 단독:** grid item 오버플로우. `minmax(0, 1fr)` + `min-width:0; overflow:hidden`.
- **인라인 `font-size:clamp(...)`:** @media 무력화. 클래스 경유.
- **히어로 `<br>` 강제 개행:** 모바일 2+5자 낙하. 자연 wrap + `keep-all`.
- **clamp 하한 모바일 미역산:** `clamp(26px, 5.5vw, 84px)`는 375px서 20.6px. 히어로 ≥40·섹션 ≥26.
- **데스크탑 먼저 설계 관성:** PC 완벽 → 모바일 늦게 확인 = 수정 3-5회. mobile-first 375px서 선설계.
- **PPTX 변환 시 복잡 그라디언트·backdrop-filter·애니메이션:** 변환 깨짐. 단색·2-stop만, flex 2단 이내, 정적 캡처 기준.
