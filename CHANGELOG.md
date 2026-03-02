# Changelog

All notable changes to Method Modular Design are documented here.

---

## [2.0.0] — 2026-03-01

### Summary
Complete evolution of Method Modular Design. The core concept — a logic-free Core that discovers self-describing modules — is unchanged. Everything around it has been rebuilt to be universal, stricter, and more complete.

### Breaking Changes
- `pack.json` replaced by `manifest.json` with a formal JSON Schema (`manifest.schema.json`)
- Module directory renamed from `packs/` convention to `modules/` (configurable)
- Multiple `.cursor/rules/MODULAR_*.md` files consolidated into a single `METHOD.md` source of truth
- Cursor-only rules replaced by universal adapters per agent

### Added
- **Universal agent support** — Cursor, Windsurf, GitHub Copilot, Claude, ChatGPT, Aider, any agent
- **`manifest.schema.json`** — formal JSON Schema contract that every module must fulfill
- **REFLEX engine** — Core introspection layer that reads all manifests and auto-generates Admin Panel navigation, dashboard widgets, and settings forms
- **Standard Admin API** — identical endpoints in every project regardless of stack (`/api/admin/manifest-registry`, `/api/admin/navigation`, `/api/admin/settings/:id`, `/api/admin/dashboard`, `/api/admin/action/:moduleId/:actionId`, `/api/admin/health`)
- **Capability types** — `view`, `action`, `metric`, `widget`, `page` declared in manifest and rendered automatically
- **Settings UI generation** — settings declared in manifest render as sliders, toggles, selects, etc. in Admin Panel. Zero manual form code.
- **Dangerous action confirmation** — actions marked `"dangerous": true` automatically get a confirmation dialog
- **Hook system** — modules declare which events they listen to in manifest
- **Dependency resolution** — Core boots modules in correct order based on declared dependencies
- **UI Pack system** — modules of type `ui` provide swappable themes and component overrides
- **8-phase method** — structured phases from stack detection to continuous refinement
- **Adapters** — `cursor.md`, `windsurf.md`, `copilot.md`, `generic.md` for each agent
- **`enet` CLI** — install via `npm install -g @exchanet/enet`, then `enet install modular-design`
- **Completion gate** — explicit checklist the agent must pass before marking any module done
- **Agent behavior specification** — explicit instructions for what the agent does when it cannot complete a manifest

### Changed
- Method documentation consolidated from 7 separate rule files into one `METHOD.md`
- Admin Panel is now strictly a renderer — zero hardcoded module references allowed
- Settings must use `context.settings.get('key')` — `os.getenv()` and config files explicitly forbidden
- Module is not considered complete until it appears correctly in Admin Panel (was implicit, now a hard rule)

### Removed
- Cursor-specific `.cursor/rules/` file structure (replaced by universal adapters)
- `pack.json` format (replaced by `manifest.json` with formal schema validation)
- Cursor Skills system (consolidated into METHOD.md)

---

## [1.0.0] — 2025-01-01

### Summary
Initial release as `method_modular_design_cursor`. Cursor-only method for building modular applications with a Core + Packs pattern.

### Features
- Core + Packs architecture
- Auto-detection of packs in `/packs/` directory
- `pack.json` metadata per pack
- `config.schema.json` for pack configuration
- Hook system (init, activate, deactivate)
- Frontend slots system
- Admin Panel integration
- Security sandboxing spec
- Cursor Rules and Skills
- Documentation in English and Spanish
