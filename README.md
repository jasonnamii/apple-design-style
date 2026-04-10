# apple-design-style

**Apple Keynote-inspired minimalism: extreme contrast, precise typography, versatile output formats.**

## Prerequisites

- **Obsidian Vault** — required for `mode-obsidian` output (box styling, font/color constraints)
- **Claude Cowork or Claude Code** environment
- For HTML/PDF/PPTX output, Obsidian is not required

## Goal

apple-design-style provides a design system rooted in black/white contrast, extreme font weight variation, generous whitespace, and strategic typography. It outputs to HTML, PDF, PPTX, or Obsidian markdown from a single specification.

## When & How to Use

Deploy exclusively when explicitly requested. Ideally paired with deliverable-engine for content structure before visual application. Use for high-stakes presentations, investor decks, executive summaries, or documentation that needs to impress through clarity and minimalism.

## Use Cases

| Scenario | Prompt | What Happens |
|---|---|---|
| Investor pitch deck | `"Design Series A deck with apple design style. PPTX."` | Black/white base→5-scale weight contrast→minimal color accent→production-ready .pptx |
| Executive summary | `"Reformat strategy doc with apple design style. PDF."` | Typographic hierarchy→negative space→single-color accent→print-ready PDF |
| Obsidian documentation | `"Apply apple design style to documentation."` | Typography hierarchy in markdown→minimal callouts→whitespace→elegant vault |

## Key Features

- Black/white foundation with one accent color maximum
- 5-scale font weight hierarchy for extreme visual contrast
- Generous whitespace emphasizing what matters
- Multi-format: Obsidian + HTML + PDF + PPTX from single design spec
- Explicit activation only — never auto-triggers

## Works With

- **[deliverable-engine](https://github.com/jasonnamii/deliverable-engine)** — structures content; apple-design-style applies visual design
- **[html-div-style](https://github.com/jasonnamii/html-div-style)** — alternative design system with more style variety

## Installation

```bash
git clone https://github.com/jasonnamii/apple-design-style.git ~/.claude/skills/apple-design-style
```

## Update

```bash
cd ~/.claude/skills/apple-design-style && git pull
```

Skills placed in `~/.claude/skills/` are automatically available in Claude Code and Cowork sessions.

## Part of Cowork Skills

This is one of 25+ custom skills. See the full catalog: [github.com/jasonnamii/cowork-skills](https://github.com/jasonnamii/cowork-skills)

## License

MIT License — feel free to use, modify, and share.
