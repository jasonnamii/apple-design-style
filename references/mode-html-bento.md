# MODE 2: HTML 벤토 (한 페이지 그리드)

| 항목 | 값 |
|------|-----|
| 배경 | `#f5f5f7` |
| 폰트 | `Pretendard Variable` wght 300,400,600,700,950. CDN: jsdelivr pretendardvariable.min.css |
| 그리드 | `repeat(4, 1fr)`, gap `12px` |
| 카드 | `#fff`, `border-radius: 20px`, padding `28px 30px` |
| 다크카드제목 | L `48px` wght 950, 라벨 XS `12px` `#86868b` |
| 히어로 | `#000`, span 2col, XL `80px` wght 950 |
| 섹션헤더 | XS `12px`, uppercase, `letter-spacing: 2px`, `#86868b` |
| 본문 | S `18px`, `#1d1d1f`, `line-height: 1.65` |
| 체크리스트 | 넘버 `#86868b` 700 + 텍스트 `#1d1d1f` |
| 프로그레스바 | `7px` height, `#f0f0f0` bg, `#1d1d1f` fill |
| 태그 | `#f5f5f7` bg, `1.5px solid #e5e5ea` |
| 플로우 | 가로 배치, `#fafafa` bg, `1.5px solid #e8e8e8` |
| 배치원칙 | 다크제목 좌 + 설명카드 우 = 한 행 = 한 맥락 |

## 반응형 (벤토 전용)

벤토는 `repeat(4,1fr)` 고정 그리드 + `grid-column:span N` 유틸로 배치. 단순 `auto-fit`과 다르게 **각 컴포넌트마다 span 값이 박혀있어**, 미디어쿼리에서 **전수 리셋**하지 않으면 모바일에서 붕괴 실패. design-skill responsive R4a와 동기.

### 브레이크포인트별 span 리셋

| 폭 | 그리드 | span 리셋 대상 | 목표 span |
|-----|--------|------|-----|
| ≥ 1025px | `repeat(4,1fr)` | — | base 그대로 (`.hero:2`·`.section-head:4`·`.closing:4`·`.elev:3`·`.think:2`·`.col-3:3`·`.col-4:4`) |
| 641 ~ 1024px | `repeat(2,1fr)` | `.col-3, .col-4, .hero, .section-head, .think, .elev, .closing` | `span 2` |
| ≤ 640px | `1fr` (1열) | `.col-1, .col-2, .col-3, .col-4, .hero, .section-head, .think, .elev, .closing` | `span 1` |

### 미디어쿼리 템플릿

```css
@media (max-width: 1024px) {
  .grid { grid-template-columns: repeat(2, 1fr); gap: 10px; }
  .col-3, .col-4, .hero, .section-head, .think, .elev, .closing { grid-column: span 2; }
}
@media (max-width: 640px) {
  .grid { grid-template-columns: 1fr; gap: 10px; }
  .col-1, .col-2, .col-3, .col-4, .hero, .section-head, .think, .elev, .closing { grid-column: span 1; }
}
```

**왜:** base CSS에서 명명 컴포넌트에 `grid-column:span N`을 선언하면, @media에서 그 선언이 살아있는 한 자식이 **암시적 트랙**을 생성한다. 즉 `grid-template-columns:1fr`로 바꿔도 span 4 카드는 4개 암시적 트랙을 만들어 횡스크롤 또는 화면 밖 잘림 발생. 규칙: **base에 span을 준 모든 선택자 = @media 리셋 필수.**

### 검증

- 360·390·480·640·768·1024px 각 폭에서 `document.scrollWidth == window.innerWidth`
- 640px 이하에서 모든 카드가 1열 세로 스택

---

## 체크리스트

- [ ] 벤토: 다크제목 + 설명카드 같은 행 배치
- [ ] 4열 그리드 + 12px gap
- [ ] base의 모든 `grid-column:span N` 선언(명명 컴포넌트 포함)이 @media 1024px·640px에서 전수 리셋
- [ ] 360·390·480·640·768px 실측 횡스크롤 0
