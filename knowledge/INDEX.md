# WasakaAI — Knowledge Index

> **Read this file first on every session.**
> This is the bootstrap — contains pointers to all persistent knowledge.
> When new information is discovered, write it to the corresponding file and update this index.

---

## Who

- [[Alan de Jesus Martinez]] — Primary user. Web dev, content creator, brand owner.
- [[Wasaka Be]] — Personal brand. YouTube, Instagram, website on Vercel.
- [[New Nuwamei]] — Company brand. LinkedIn + Facebook.

## What

- [[Arch Linux]] — Current system. KDE Plasma 6 + Wayland, 756+ packages.
- [[Arch Packages]] — Recommended packages by category.
- [[MS912x USB Display]] — Third monitor via MacroSilicon 345f:9132 USB-HDMI adapter. Driver at `~/build/ms912x/`.
- [[ECC]] — Agent harness OS (262 skills, 25 subagents, 35 commands). Integrated into OpenCode. Repo: `~/build/ecc/`.
- [[OpenCode]] — AI-assisted editor. WasakaAI runs here.
- [[WasakaAI]] — This identity. British composure, senior engineering rigor, ECC-powered.
- [[Preferences]] — How Alan likes things. Language, tone, tools, naming conventions.

## How (Processes)

- **On session start**: Read this file. Load context. No need to ask again.
- **On new information**: Write to the appropriate file. Update this index if a new entity is created.
- **On decisions**: Log in `sessions/` with date. Cross-reference with `decisions/` if it's a lasting choice.
- **On learnings**: Write to `learnings/` category. Tag with relevant entities.

## Decisions

- [[ADR-001: Token Optimization]] — Condensed system prompts, knowledge graph for context. 47% token savings.
- [[ADR-002: Senior Engineering Protocol]] — SOLID, strict typing, testing pyramid, value creation bar. No toy code.
- [[ADR-003: MS912x Driver Selection]] — Use yxmicha/ms912x for MacroSilicon 345f:9132 USB display. Over official vendor driver (laggy) and rhgndf/ms912x (wrong protocol).
- [[ADR-004: WasakaAI Identity]] — JARVIS rebranded to WasakaAI. Branded, personal AI assistant. ECC v2.0.0 integrated as capability layer. Knowledge graph preserved and migrated.

## Directory Map

```
~/WasakaAI/
├── INDEX.md                    ← You are here
├── .opencode/
│   ├── agent/
│   │   └── wasakaai.md         ← WasakaAI agent definition
│   ├── commands/               ← 35 slash commands
│   ├── prompts/agents/         ← 25 subagent prompt templates
│   ├── plugins/                ← ecc-hooks, tools integration
│   ├── tools/                  ← 8 custom tools
│   └── instructions/           ← ECC coding standards
├── knowledge/
│   ├── profile/                ← People, identities
│   │   └── alan.md
│   ├── projects/               ← Brands, products, repos
│   │   ├── wasaka-be.md
│   │   └── new-nuwamei.md
│   ├── stack/                  ← Technologies, tools, configs
│   │   ├── arch-linux.md
│   │   ├── arch-packages.md
│   │   ├── docker.md
│   │   ├── ecc.md
│   │   ├── gimp.md
│   │   ├── jarvis.md
│   │   ├── kdenlive.md
│   │   ├── kde-plasma-6.md
│   │   ├── krita.md
│   │   ├── ms912x-usb-display.md
│   │   ├── nextjs.md
│   │   ├── nodejs.md
│   │   ├── obs-studio.md
│   │   ├── opencode.md
│   │   ├── open-design.md
│   │   ├── python.md
│   │   ├── rust.md
│   │   └── vercel.md
│   ├── preferences/            ← How Alan likes things
│   │   └── preferences.md
│   ├── decisions/              ← Architectural & design decisions (ADRs)
│   │   ├── 001-token-optimization.md
│   │   ├── 002-senior-engineering-protocol.md
│   │   ├── 003-ms912x-driver-selection.md
│   │   └── 004-wasakaai-identity.md
│   ├── learnings/              ← Things discovered over time
│   │   └── wasaka-be-website-tech.md
│   └── sessions/               ← Session logs (what happened when)
│       ├── 2026-06-04.md
│       └── 2026-06-11.md
└── skills/                     ← 262 ECC skills (on-demand)
```

## Session Protocol

1. **Start**: Read `INDEX.md` → load context → proceed
2. **During**: If new facts emerge, write to appropriate file immediately
3. **End**: Update `sessions/` log with what happened, decisions made, action items

## Wikilink Convention

All `[[links]]` use Title Case and map to filenames:
- `[[Wasaka Be]]` → `projects/wasaka-be.md`
- `[[Arch Linux]]` → `stack/arch-linux.md`
- `[[Alan de Jesus Martinez]]` → `profile/alan.md`

This ensures Obsidian compatibility and human readability.

---

*Last updated: 2026-06-11*