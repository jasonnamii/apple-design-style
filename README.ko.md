# Apple 디자인 스타일

> 🇺🇸 [English README](./README.md)

**Apple Keynote 감성 미니멀 디자인: 극단적 대비, 정밀한 타이포그래피, 다양한 산출 포맷.**

## 사전 요구사항

- **Obsidian Vault** — `mode-obsidian` 산출 시 필요 (박스 스타일, 폰트/색상 제약)
- **Claude Cowork 또는 Claude Code** 환경
- HTML/PDF/PPTX 산출의 경우 Obsidian 불필요

## 목적

Apple 디자인 스타일은 흑백 대비, 극단적 폰트 가중치 변화, 넉넉한 여백, 전략적 타이포그래피를 기반으로 한 디자인 시스템입니다. 단일 설계 명세에서 HTML, PDF, PPTX, Obsidian 마크다운으로 산출합니다.

## 사용 시점 및 방법

명시적 요청이 있을 때만 배포하세요. 가급적 콘텐츠 구조화를 위해 deliverable-engine과 함께 사용하면 좋습니다. 고위험 프레젠테이션, 투자자 피치, 경영진 요약, 명확함과 미니멀함으로 인상을 남겨야 하는 문서에 사용하세요.

## 사용 예시

| 상황 | 프롬프트 | 결과 |
|---|---|---|
| 투자자 피치 덱 | `"apple-design-style로 Series A 덱 설계. PPTX."` | 흑백 베이스→5단계 weight 대비→최소 색상 악센트→프로덕션급 .pptx |
| 경영 요약서 | `"apple-design-style로 전략 문서 재구성. PDF."` | 타이포그래피 계층→음의 공간→단색 악센트→프린트 준비 완료된 PDF |
| Obsidian 문서 | `"apple-design-style 적용."` | 마크다운 타이포그래피 계층→최소 콜아웃→여백→우아한 Vault |

## 핵심 기능

- 흑백 기초에 최대 1가지 악센트 색상
- 극단적 시각 대비를 위한 5단계 폰트 가중치 계층
- 중요한 것을 강조하는 넉넉한 여백
- 단일 설계 명세에서 Obsidian + HTML + PDF + PPTX 다중 포맷 산출
- 명시적 활성화만—자동 작동 금지

## 연관 스킬

- **[deliverable-engine](https://github.com/jasonnamii/deliverable-engine)** — 콘텐츠 구조화; apple-design-style은 시각적 설계 적용
- **[html-div-style](https://github.com/jasonnamii/html-div-style)** — 더 다양한 스타일의 대체 디자인 시스템

## 설치

```bash
git clone https://github.com/jasonnamii/apple-design-style.git ~/.claude/skills/apple-design-style
```

## 업데이트

```bash
cd ~/.claude/skills/apple-design-style && git pull
```

`~/.claude/skills/`에 배치된 스킬은 Claude Code 및 Cowork 세션에서 자동으로 사용할 수 있습니다.

## Cowork 스킬 생태계

25개 이상의 커스텀 스킬 중 하나입니다. 전체 카탈로그: [github.com/jasonnamii/cowork-skills](https://github.com/jasonnamii/cowork-skills)

## 라이선스

MIT 라이선스 — 자유롭게 사용, 수정, 공유하세요.