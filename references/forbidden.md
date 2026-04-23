# forbidden.md — apple-box-design 금칙

전역 + HTML 레이아웃 11대 + PPTX 변환 + 옵시디언 금칙 일괄. 타겟 다양(HTML·PDF·PPTX·.md) → 금칙 분할.

> 공통 금칙: `VAULT/_skills research/html-skill-refactor/spine.md §공통 금칙`
> 축4 PPTX 상세: `VAULT/_skills research/html-skill-refactor/axis4-pptx-pdf-conversion.md`

---

## 전역 (모든 타겟)

| # | 금지 | 이유 |
|---|---|---|
| G1 | `position: fixed` | PDF/PPTX 무시·옵시디언 붕괴 |
| G2 | viewport 단위 단독 (`vw`/`vh`) | PPTX 무의미·PDF 페이지 무관 |
| G3 | `<script>` | PPTX·PDF·옵시디언 전부 차단 |
| G4 | 컬러 일반 (블랙/화이트/그레이 외) | Apple 정체성 — Oxford Blue 액센트만 예외 |

## HTML 레이아웃 11대 (핵심 — 제출 전 전수 점검)

| # | 원인 | 증상 | 처방 |
|---|---|---|---|
| 1 | 암시적 그리드 트랙 (명명 선택자 span 리셋 누락) | 모바일 span 유지·횡스크롤 | base span 선언 선택자 전수 열거 후 @media 1024·640에서 강제 리셋 |
| 2 | CSS 특이도 역전 | @media 리셋 무시 | @media 선택자 특이도 ≥ base |
| 3 | flex 자식 `min-width:auto` | 카드가 부모 폭 초과 | `.flex-item { min-width: 0 }` |
| 4a | **한글 세로 1글자 낙하 (치명)** | `break-word`·`break-all` 한글 적용 | **`word-break: keep-all; overflow-wrap: break-word;`** (단독 break-* 금지) |
| 4b | 영문·URL·mono | 한글 처방 혼용 | 영문 컨테이너만 `overflow-wrap: anywhere` |
| 5 | `white-space: nowrap` + 긴 텍스트 | 단일 라인·횡스크롤 | 장식 외 금지. 필수 시 ellipsis 동반 |
| 6 | 이미지·테이블·iframe max-width 누락 | 모바일 폭 돌파 | `img,svg,video,iframe{max-width:100%;height:auto}` |
| 7 | 패딩+폰트 고정px 누적 | 360px서 콘텐츠 −값 | 모바일 패딩 20~24px·clamp |
| 8 | **`repeat(N, 1fr)` 단독 (치명)** | grid item 오버플로우 | **`repeat(N, minmax(0, 1fr))` 필수** + `.box{min-width:0;overflow:hidden}` |
| 9 | **inline `style="font-size:clamp(...)"` (치명)** | specificity 1000이 @media 무력화 | 인라인 0건. 클래스 경유 |
| 10 | `<br>` 강제 줄바꿈 (히어로) | 모바일 2+5자 낙하 | 자연 wrap + `word-break:keep-all` |
| 11 | clamp 하한 모바일 미역산 | 히어로가 본문 크기로 왜소 | 히어로 ≥40px·섹션 ≥26px (375px 실측) |

## HTML 색상 금칙

### inline `style="color:…"` 금지 (치명)

specificity 1000이 다크 역매핑(`.dark`·`.key`·`.hot`·`.now`·`.think.dark`·Oxford Blue)을 무조건 무력화.

```html
<!-- ❌ FAIL -->
<div class="case" style="color:#424245">타 산업 사례</div>

<!-- ✅ PASS -->
<div class="case">타 산업 사례</div>
<style>.case { color: var(--label-caption); }</style>
```

### 다크 배경 금지 색

`#424245` · `#6e6e73` · `#666` · `#888` 다크 배경 FAIL (대비 ≤3:1).
다크 허용 4색만: `#fff` · `#d1d1d6` · `#86868b` · `#3a3a3c`.

### `--muted` 단일 변수 금지

Tier 1/2/3 한 변수에 몰면 다크 역매핑이 위계 3단을 2단(또는 1단)으로 붕괴. **3 변수 독립 분리 필수.**

## HTML 반응형 금지

| 금지 | 대체 |
|---|---|
| viewport 메타 누락 | `<meta name="viewport" content="width=device-width, initial-scale=1">` 필수 |
| 히어로 고정 80px | clamp 최소 48px로 축소 |
| 고정열 `grid-template-columns: 1fr 1fr 1fr 1fr` | `repeat(auto-fit, minmax(280px, 1fr))` |
| body·html `overflow-x: hidden` | 원인 은폐. 실제 수정 필요 |
| 데스크탑 패딩 모바일 전파 | 모바일 20~32px로 축소 |
| 터치 타겟 <44px | 44×44 강제 |

## PPTX 변환 금칙 (python-pptx·Aspose 등)

| 금지 | 이유 | 대체 |
|---|---|---|
| CSS 그라디언트 복잡 | PPTX 변환 불안정 | 단색 또는 2-stop만 |
| backdrop-filter·glassmorphism | PPTX 무지원 | 불투명 색 |
| flex 중첩 3단+ | 변환서 레이아웃 손실 | 2단 이내 또는 table 레이아웃 |
| clamp 폰트 | PPTX는 고정 pt | px=pt 1:1 환산 |
| CSS 애니메이션 | 정적 캡처만 남음 | 제거·정적 상태로 |
| 한글 세로 작성 | 변환서 깨짐 | 가로만 |

## 옵시디언 금칙 (.md 출력 시)

`→ html-div-style/references/forbidden.md §옵시디언 14금칙` 동일 적용.

핵심: ❶ div 내부 빈줄 · ❷ 마크다운 문법 · ❸ 다크 color 개별 명시 · ❺ div 전후 빈줄 · ❻ 인라인 style만 · ❽ font-family 금지 · ⓫ 연속 카드 `<br>` 스페이서.

## 콘텐츠 금지

| 금지 | 이유 |
|---|---|
| "~하는 것이 중요하다" | Apple 톤 이탈 → "~다." 단언형 |
| 섹션당 5줄+ | 여백 철학 위반 → 4줄 이내 |
| 번호 목록 5개+ | 시각 밀도 과잉 → 최대 4개 또는 플로우(→) |
| 배경·서론 | 결론만 |

## 자동 QC 게이트

```bash
bash mnt/.claude/skills/design-skill/scripts/qc-mobile.sh output.html
grep -n 'style="[^"]*color:' *.html            # = 0
grep -n 'style="[^"]*font-size:[^"]*clamp' *.html  # = 0
grep -E 'repeat\([0-9]+, *1fr\)' *.html         # = 0
```

상세 체크리스트: `→ qc.md`.
