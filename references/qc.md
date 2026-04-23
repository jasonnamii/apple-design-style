# qc.md — apple-box-design 품질 체크리스트

6계층 스코어카드 + 모드별 전수 체크. 합격선 ≥80 AND Layer 1-4 ≥85%.

> 공통 QC: `VAULT/_skills research/html-skill-refactor/spine.md §공통 QC`
> 축5 상세: `VAULT/_skills research/html-skill-refactor/axis5-qc-checklist.md`

---

## 6계층 스코어카드

| Layer | 항목 | 배점 | 자동화 |
|---|---|---|---|
| 1 Syntax | HTML 유효성·PDF·PPTX 객체 | 8 | 100% |
| 2 A11y | 대비·터치타겟·시맨틱 | 20 | 70% |
| 3 Perf | 경량·clamp·리소스 | 20 | 100% |
| 4 Semantic | 태그 의미 정합 | 15 | 50% |
| 5 Design | Apple 스타일·3색 3단 | 25 | 30% |
| 6 Brand | Pretendard·극단 weight·여백 | 12 | 10% |

---

## 공통 체크

- [ ] 폰트 스케일 5단계(XL/L/M/S/XS) 준수·XS 13px 하한
- [ ] 색상 3단 분리: Tier1 `#1d1d1f` · Tier2 `#424245` · Tier3 `#86868b`
- [ ] CSS 변수 3분리(`--label-info·-caption·-deco`) · `--muted` 단일 없음
- [ ] 다크 컨테이너 내부 자동 역매핑 CSS 존재
- [ ] 다크 배경 텍스트 4색만(`#fff·#d1d1d6·#86868b·#3a3a3c`) · `#424245·#6e6e73` 없음
- [ ] 컬러 사용 없음 (블랙/화이트/그레이만) — Oxford Blue 액센트 예외
- [ ] 제목 wght 950 · 본문 wght 300 대비
- [ ] 섹션당 텍스트 4줄 이내
- [ ] 히어로 + 클로징 존재
- [ ] 플로우 화살표(→) 사용
- [ ] 여백 > 콘텐츠 면적

## HTML 전용 (Layer 2·3 가중)

### 반응형 필수

- [ ] viewport 메타 존재
- [ ] 폰트 clamp 반응형 (고정 px 금지)
- [ ] 모바일(≤640px) 1열 붕괴·횡스크롤 없음
- [ ] 터치 타겟 ≥44px
- [ ] 5폭 실측(360·390·480·640·768·1024) 횡스크롤 0
- [ ] `img,svg,video,iframe{max-width:100%}` 선언
- [ ] 한글 `word-break: keep-all; overflow-wrap: break-word`
- [ ] flex·grid 자식 `min-width: 0`
- [ ] 히어로 clamp 하한 ≥40px · 섹션 타이틀 ≥26px (375px 실측)
- [ ] body·html `overflow-x: hidden` 없음

### 레이아웃 11대 전수 (forbidden.md §HTML 레이아웃 11대)

- [ ] 1. 암시적 그리드 트랙 리셋됨
- [ ] 2. CSS 특이도 @media ≥ base
- [ ] 3. flex `min-width:0` 선언
- [ ] 4a. 한글 `keep-all`
- [ ] 4b. 영문만 `anywhere` 한정
- [ ] 5. `nowrap` 장식 외 없음
- [ ] 6. img/table/iframe max-width
- [ ] 7. 모바일 패딩 20~32px
- [ ] 8. `repeat(N, minmax(0, 1fr))` 사용
- [ ] 9. 인라인 `style="font-size:clamp(...)"` 0건
- [ ] 10. 히어로 `<br>` 강제 개행 0건
- [ ] 11. clamp 하한 375px 역산 완료

### 자동 QC 게이트

```bash
bash mnt/.claude/skills/design-skill/scripts/qc-mobile.sh output.html  # PASS
grep -n 'style="[^"]*color:' *.html                # = 0
grep -n 'style="[^"]*font-size:[^"]*clamp' *.html  # = 0
grep -E 'repeat\([0-9]+, *1fr\)' *.html            # = 0
```

## PDF 전용

- [ ] reportlab rgb 0-1 스케일 사용
- [ ] Tier 1·2·3 → `(0.11,0.11,0.12)·(0.26,0.26,0.27)·(0.52,0.52,0.54)` 매핑
- [ ] 극단 weight (Bold/Light) 폰트 임베딩

## PPTX 전용

- [ ] 복잡 그라디언트·backdrop-filter·애니메이션 없음
- [ ] flex 중첩 2단 이내
- [ ] 폰트 pt 고정값 (px=pt 1:1)
- [ ] 한글 가로 레이아웃만
- [ ] 정적 캡처로도 의미 보존되는 레이아웃

## Obsidian (.md) 전용

- [ ] 14금칙 전수 PASS (→ html-div-style/references/forbidden.md)
- [ ] 다크 컨테이너 텍스트 태그별 color 개별 명시
- [ ] 연속 카드 사이 `<br>` 스페이서
- [ ] `<details>` 내부 빈줄·마크다운 0

## 합격 판정

- Total ≥80 AND Layer 1~4 ≥85%
- HTML: 레이아웃 11대 전수 PASS + 5폭 실측 0
- PPTX: 변환 후 캡처 대조 (깨짐 0)
- .md: 14금칙 전수 PASS

## 불합격 처방

| 주 실패 | 포인터 |
|---|---|
| Layer 1/3 (HTML) | → forbidden §HTML 레이아웃 11대 · 자동 QC 게이트 |
| Layer 2 다크 대비 | → tokens §Tier 2 다크 `#d1d1d6` · forbidden §HTML 색상 |
| Layer 5 Design 3단 붕괴 | → tokens §CSS 변수 3분리 |
| Layer 6 Brand | → tokens §타이포 Pretendard·극단 weight |
| PPTX 변환 깨짐 | → forbidden §PPTX 변환 금칙 · mode-pptx.md |
