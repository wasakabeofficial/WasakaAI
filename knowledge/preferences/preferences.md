---
type: entity
created: 2026-06-04
updated: 2026-06-04
---

# Preferences

## Communication

- **Language**: Prefers Spanish, understands English perfectly
- **Tone**: Direct, no flattery, no filler. Technical precision over verbosity
- **Context**: Values token efficiency — wants persistent knowledge, not repeated explanations

## Technology

- **OS Philosophy**: Bleeding-edge, maximum customization (Arch Linux + KDE)
- **Deployment**: Vercel for web projects
- **Containers**: Docker for local dev
- **Editors**: Vim for quick edits, OpenCode for AI-assisted work
- **Package Management**: Prefers pacman/AUR over Flatpak/Snap

## Workflow

- **Knowledge Management**: Building a local knowledge graph (Obsidian-compatible)
- **Content Creation**: YouTube + Instagram + Facebook (multi-platform)
- **Branding**: Manages two brands ([[Wasaka Be]], [[New Nuwamei]])

## Engineering Standards

- **Protocol**: [[ADR-002: Senior Engineering Protocol]] — SOLID, strict typing, testing, value creation bar
- **No toy code**: Every project must pass the value creation test before building
- **No `any`**: TypeScript strict always. `unknown` + narrow.
- **No magic numbers**: Constants with descriptive names
- **Testing pyramid**: 70% unit / 20% integration / 10% E2E
- **Clean Architecture**: domain → application → infrastructure → presentation
- **Push back**: If requirements are vague or scope is wrong, say so

## Dislikes

- Cloud lock-in
- Repeating context across sessions
- Verbose explanations when a line suffices
- Over-engineering simple problems
- Tutorial projects rebranded as portfolio pieces
- CRUD apps with no business logic
- TODO apps in trench coats
- Code without error handling

## Naming Conventions

- Files: kebab-case (e.g., `wasaka-be.md`)
- Folders: lowercase, singular concept
- Links: `[[Title Case]]` for Obsidian compatibility
- Variables: descriptive, no abbreviations (`userRepository` not `ur`)
- Functions: verb + noun (`validateUserCredentials()` not `check()`)
- Booleans: `is`/`has`/`should`/`can` prefix
- Constants: UPPER_SNAKE (`MAX_LOGIN_ATTEMPTS`)