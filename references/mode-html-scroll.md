# MODE 1: HTML 스크롤 (풀페이지)

| 항목 | 값 |
|------|-----|
| 배경 | `#000` |
| 폰트 | `Pretendard Variable` wght 300,400,600,700,950. CDN: jsdelivr pretendardvariable.min.css |
| 섹션 | `min-height: 100vh`, flex-center |
| 제목 | XL `clamp(64px, 8vw, 80px)` wght 950, `letter-spacing: -3px` |
| 서브제목 | L `clamp(36px, 5vw, 48px)` wght 700 |
| 본문 | M `clamp(22px, 3vw, 28px)` wght 300, color `#ccc` |
| 보조 | S `18px` wght 300, color `#888` |
| 라벨 | XS `12px` wght 400, color `#666` |
| 강조 | 동일 사이즈 + wght 600, color `#fff` |
| 플로우 | S mono계열, color `#666`, span내 `#fff` |
| 구분선 | `border-top: 1px solid #1a1a1a` |
| 애니메이션 | `IntersectionObserver` fade-in, `translateY(30px)` |
| 히어로 | 96-140pt, 센터, 하위 서브텍스트 `#888` |
| 클로징 | Before/After 대비 + 최종 문장 950 Black |

## 체크리스트

- [ ] HTML: Pretendard Variable CDN import 확인 (jsdelivr)
- [ ] IntersectionObserver 애니메이션 동작 확인
- [ ] clamp 반응형 사이즈 적용
