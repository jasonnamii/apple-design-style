# MODE 5: 옵시디언 .md (다크그레이 박스)

옵시디언 환경에서 Apple Design을 구현하기 위한 모드. 불릿리스트, 카드, 강조 섹션 등 다양한 콘텐츠를 HTML div 박스로 렌더링.

## 박스 타입 및 스타일

**① 화이트 박스** (기본 설명 카드)
```html
<div style="background: #fff; border: 1px solid #e0e0e0; border-radius: 16px; padding: 24px 28px;">
<p style="color: #1d1d1f;">설명 텍스트</p>
</div>
```

**② 그레이 박스** (보조 정보, 배경)
```html
<div style="background: #f5f5f7; border: 1px solid #e0e0e0; border-radius: 16px; padding: 24px 28px;">
<p style="color: #1d1d1f;">보조 텍스트</p>
</div>
```

**③ 다크 박스** (강조, 결론)
```html
<div style="background: #2d2d2d; border-radius: 16px; padding: 24px 28px;">
<p style="color: #fff;">강조 텍스트</p>
</div>
```

## 다중 컬럼 레이아웃

```html
<div style="display: flex; gap: 12px;">
<div style="background: #fff; border: 1px solid #e0e0e0; border-radius: 16px; padding: 24px 28px; flex: 1;">
<p style="color: #1d1d1f;">좌측</p>
</div>
<div style="background: #fff; border: 1px solid #e0e0e0; border-radius: 16px; padding: 24px 28px; flex: 1;">
<p style="color: #1d1d1f;">우측</p>
</div>
</div>
```

## 주요 특성

- **폰트**: 기본 Obsidian 폰트. font-size, font-weight, letter-spacing, line-height, text-transform 지정 금지.
- **색상**: 다크박스(`#2d2d2d`) 내부 텍스트는 모든 요소(`<p>`, `<strong>`, `<li>`, `<td>`, `<span>`)에 `style="color: #fff"` 개별 지정 필수.
- **테이블**: 다크박스 바깥에 배치하거나, 각 `<td>`에 불투명 `background-color` 명시.
- **리스트**: HTML `<ul><li>` 사용. 마크다운 `-` 금지.
- **강조**: HTML `<strong>` 사용. 마크다운 `**` 금지.
- **링크**: 위키링크 `[[#헤딩명]]` 사용. 앵커링크 `[text](#slug)` 금지.

---

## 옵시디언 렌더링 규칙 (7개 — 필수 준수)

### ❶ div 내부 빈줄 금지

`<div>`~`</div>` 사이 빈 줄(empty line) **0개**. Obsidian이 HTML 블록을 끊음.

```html
<!-- ❌ WRONG -->
<div style="background: #fff; border-radius: 16px; padding: 24px 28px;">

<p style="color: #1d1d1f;">텍스트</p>

</div>

<!-- ✅ CORRECT -->
<div style="background: #fff; border-radius: 16px; padding: 24px 28px;">
<p style="color: #1d1d1f;">텍스트</p>
</div>
```

### ❷ div 내부 마크다운 금지

`**`·`*`·`[[]]`·`- ` 사용 금지 → HTML 태그만(`<strong>`·`<em>`·`<a>`·`<ul><li>`). 콜아웃 내부는 마크다운 허용.

### ❸ 다크배경 개별색상 필수

어두운배경(`#2d2d2d`) div 내 모든 텍스트 태그(`<p>`·`<strong>`·`<li>`·`<td>`·`<span>`)에 `style="color: #fff"` 개별 지정. div의 color는 하위요소에 전파 안됨.

### ❹ 다크배경 div 내 테이블 금지

테마 행줄무늬가 override → 테이블은 div 바깥 또는 각 `<td>`에 불투명 `background-color` 명시.

### ❺ 콜아웃 뒤 빈줄 필수

`> ...` 마지막줄 뒤 빈줄 1개. 후속 블록이 콜아웃에 흡수됨 방지.

### ❻ 앵커링크 = 위키링크

`[text](#slug)` 금지 → `[[#헤딩명]]`. TOC도 동일.

### ❼ 콜아웃 내 테이블 배경

콜아웃 색상이 테이블에 침투 → 각 `<td>`에 불투명 `background-color` 명시.

---

## 서브에이전트 렌더링 전파

이 스킬이 서브에이전트(또는 다른 도구)에 위임할 때, 다음 렌더링 규칙들을 **반드시 프롬프트에 포함**해야 합니다.

### 서브에이전트 프롬프트 템플릿

```
[기존 작업 설명]

## 출력 형식: Obsidian .md (Apple Design MODE 5)

박스 타입:
- 화이트: background:#fff, border: 1px solid #e0e0e0
- 그레이: background:#f5f5f7, border: 1px solid #e0e0e0
- 다크: background:#2d2d2d, color:#fff (각 요소마다)

## Obsidian 렌더링 규칙 (적용 필수)

❶ div 내부 빈줄 금지: <div>~</div> 사이 빈 줄(empty line) 0개
❷ div 내부 마크다운 금지: **·*·[[]]·- 금지 → <strong>·<em>·<a>·<ul><li> 사용
❸ 다크배경(#2d2d2d) div 내 color 필수: 모든 텍스트 태그에 style="color:#fff" 개별 지정
❹ 다크배경 div 내 테이블 금지: 테이블은 div 바깥 또는 각 <td>에 background-color 명시
❺ 콜아웃 뒤 빈줄 필수: > ... 마지막줄 뒤 빈줄 1개
❻ 앵커링크 = 위키링크: [text](#slug) 금지 → [[#헤딩명]] 사용
❼ 콜아웃 내 테이블 배경: 각 <td>에 불투명 background-color 명시

검증: UP §C.QC 파이프라인이 수행. 서브에이전트는 규칙 준수에 집중, 자가검증 불필요.
저장: 볼트 경로에 직접 작성. 옵시 MCP write_note/patch_note 사용 금지.
```

## 체크리스트

- [ ] ❶~❼ 렌더링 규칙 준수하여 생성 ✓
- [ ] 위키링크(`[[#헤딩명]]`) 사용 ✓
- [ ] 다크박스 텍스트 color 개별 지정 ✓
- [ ] G1-G5 검증은 UP §C.QC 파이프라인에 위임 (이 스킬에서 Python 검증 실행 안 함)
