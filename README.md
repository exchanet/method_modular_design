# 🔮 Method Modular Design — Universal Modular Architecture

**Do you want your AI coding agent to build complete, production-ready modular systems — with a WordPress-style Admin Panel — automatically?**

A universal method for any AI coding agent to build clean, modular applications with a logic-free Core, self-describing modules, swappable UI packs, and a fully auto-generated Admin Panel and dashboard. No manual wiring. No hardcoded values. No forgotten UI.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-2.0.0-blue.svg)]()
[![Agent: Any](https://img.shields.io/badge/agent-any-green.svg)]()
[![Stack: Any](https://img.shields.io/badge/stack-any-green.svg)]()
[![Language: ES/EN](https://img.shields.io/badge/Language-ES%2FEN-blue.svg)](./README_ES.md)

**Repository:** [github.com/exchanet/method_modular_design](https://github.com/exchanet/method_modular_design)

---

> ⚠️ **Want pro-grade results?**
> Method Modular Design handles architecture, modularity, and UI generation. For production-quality code with ≥99% test coverage, zero vulnerabilities, and systematic validation cycles, use it alongside **[Method PDCA-T](https://github.com/exchanet/method_pdca-t_coding_Cursor)**.
> Modular Design builds the right system. PDCA-T builds it right.

---

## 🎯 What Does Method Modular Design Do?

Method Modular Design instructs any AI coding agent to build a fully modular application where:

- ✅ **Every module is self-describing** via a `manifest.json` written before any code
- ✅ **The Core has zero business logic** — it only discovers modules and reads manifests
- ✅ **The Admin Panel is auto-generated** by reading all manifests — never coded manually
- ✅ **The dashboard is auto-generated** from declared metrics and widgets
- ✅ **Settings are never hardcoded** — every configurable value lives in the manifest and is editable from the Admin Panel
- ✅ **UI Packs are swappable** — activate or deactivate themes and component overrides from the Admin Panel
- ✅ **Adding a module** = create a folder with `manifest.json` + handlers. Nothing else.
- ✅ **Removing a module** = delete the folder. It disappears from the Admin Panel completely.
- ✅ **Works with any stack** — Python, Node.js, Go, PHP, Java, any language, any framework
- ✅ **Works with any agent** — Cursor, Windsurf, GitHub Copilot, Claude, ChatGPT, Aider

---

## 🧩 What Gets Built

### The Core
A bootstrap engine that scans the modules directory, validates each `manifest.json`, resolves dependencies, boots modules in order, and exposes a standard Admin API. The Core has zero knowledge of what any module does — it only knows modules exist and have manifests.

### The REFLEX Engine
An introspection layer inside the Core that reads all registered manifests and builds the Admin navigation tree, the dashboard widget registry, and the settings schema registry. The Admin Panel is a direct rendering of what REFLEX reads.

### The Modules
Each module is a self-contained folder with a `manifest.json` that declares settings (with UI widgets), capabilities (views, actions, metrics, widgets), hooks, and dependencies.

### The Admin Panel
A dynamic renderer that reads the Core's Admin API and generates the full interface automatically. Zero hardcoded references. Adding a module adds it to the Admin Panel. Removing a module removes it. No frontend code changes required.

### The UI Pack System
Modules of type `ui` that provide themes, component overrides, and style variables. Swappable from the Admin Panel without touching any business logic.

---

## 📐 How It Works

### The manifest is the module

```json
{
  "id": "activity-logger",
  "name": "Activity Logger",
  "section": "monitoring",

  "settings": {
    "retention_days": { "type": "integer", "label": "Retention (days)", "default": 90, "ui": "slider" },
    "log_level":      { "type": "select",  "label": "Log Level", "default": "info",
                        "options": ["debug", "info", "warn", "error"] }
  },

  "capabilities": [
    { "type": "view",   "label": "Activity Logs",  "data": "ActivityLogger.getAll" },
    { "type": "action", "label": "Export CSV",      "handler": "ActivityLogger.exportCsv" },
    { "type": "action", "label": "Clear Old Logs",  "handler": "ActivityLogger.clearOld", "dangerous": true },
    { "type": "metric", "label": "Events Today",    "data": "ActivityLogger.getTodayCount" }
  ]
}
```

This manifest automatically produces — with zero additional UI code:

```
Admin Panel
└── Monitoring
    └── Activity Logger
        ├── Activity Logs              ← data table
        │   ├── [Export CSV]           ← action button
        │   └── [Clear Old Logs] ⚠     ← dangerous action (confirmation dialog)
        └── Settings
            ├── Retention: ━━●━━ 90    ← slider
            └── Log Level: [info ▾]    ← select

Dashboard
└── Events Today: 1,247               ← metric
```

### The Admin API (standard, identical in every project)

```
GET  /api/admin/manifest-registry
GET  /api/admin/navigation
GET  /api/admin/settings/:moduleId
POST /api/admin/settings/:moduleId
GET  /api/admin/dashboard
POST /api/admin/action/:moduleId/:actionId
GET  /api/admin/health
```

---

## 🚀 Quick Start

### Install — 3 options

**Option 1 — enet (recommended)**

[`enet`](https://github.com/exchanet/enet) is the exchanet methods manager. Detects your AI agent automatically and installs the adapter in the right place.

```bash
npm install -g @exchanet/enet
enet install modular-design
```

**Option 2 — enet via GitHub (no npm account needed)**

```bash
npm install -g github:exchanet/enet
enet install modular-design
```

**Option 3 — Manual**

Download the adapter for your agent from the `adapters/` folder:

| Agent | File | Place at |
|---|---|---|
| Cursor | `adapters/cursor.md` | `.cursor/rules/method-modular-design.md` |
| Windsurf | `adapters/windsurf.md` | Append to `.windsurfrules` |
| GitHub Copilot | `adapters/copilot.md` | `.github/copilot-instructions.md` |
| Antigravity | `adapters/antigravity.md` | `.agent/rules/method-modular-design.md` |
| Claude Code | `adapters/claudecode.md` | `CLAUDE.md` |
| Any other agent | `adapters/generic.md` | Paste into your agent's context |

### Give your agent a spectech

```
Build a project management SaaS.
Stack: FastAPI + React. Database: PostgreSQL. Deploy: Railway.
Modules: projects, tasks, team members, billing, activity log.
```

### 4. The agent builds the complete system

1. Declares architecture and waits for your confirmation
2. Builds the Core with REFLEX engine and Admin API
3. Creates each module — manifest first, then handlers
4. Builds the Admin Panel as a pure dynamic renderer
5. Verifies every module appears correctly before marking it complete

---

## 📁 Repository Structure

```
method_modular_design/
├── METHOD.md                    ← Complete method documentation
├── README.md                    ← This file (English)
├── README_ES.md                 ← Spanish version
│
├── adapters/
│   ├── cursor.md                ← Cursor
│   ├── windsurf.md              ← Windsurf
│   ├── copilot.md               ← GitHub Copilot
│   ├── antigravity.md           ← Antigravity (Google)
│   ├── claudecode.md            ← Claude Code
│   └── generic.md               ← Any other agent
│
└── schemas/
    └── manifest.schema.json     ← Universal manifest contract (JSON Schema)
```

---

## 🔮 Core Concepts

### Module types

| Type | Purpose |
|---|---|
| `functional` | Business logic — products, users, billing, etc. |
| `integration` | External services — Stripe, SendGrid, S3, etc. |
| `ui` | Themes and component packs — swappable |
| `core` | System-level — auth, database, cache, etc. |

### Capability types

| Type | Produces in the UI |
|---|---|
| `view` | Data table with filters in the Admin Panel |
| `action` | Button that executes logic (with optional confirmation) |
| `metric` | Number or stat card on the dashboard |
| `widget` | Rich dashboard component with custom UI |
| `page` | Full custom page in the Admin Panel |

---

## 📏 The Non-Negotiable Rules

The agent must never violate these, regardless of context or user request:

```
1. No manifest = module does not exist.
2. Manifest before code. Always.
3. Zero hardcoded configuration.
4. Core has no business logic.
5. Admin Panel is a renderer, not a destination.
6. A module is complete only when Admin Panel reflects it.
7. Removing a module folder removes it completely.
```

---

## 🌍 Compatibility

| Dimension | Supported |
|---|---|
| Agents | Cursor, Windsurf, GitHub Copilot, Claude, ChatGPT, Aider, any |
| Backend | Python, Node.js, Go, Ruby, PHP, Java, any |
| Frontend | React, Vue, Angular, Svelte, plain HTML, any |
| Database | PostgreSQL, MySQL, MongoDB, SQLite, any |
| Deploy | Vercel, Railway, Fly.io, AWS, Docker, any |

---

## 📖 Related Methods

Method Modular Design works best alongside:

- **[Method PDCA-T](https://github.com/exchanet/method_pdca-t_coding_Cursor)** ⭐ Recommended — ≥99% test coverage, zero vulnerabilities, systematic quality validation. Modular Design builds the right system. PDCA-T builds it right.
- **[Method IRIS](https://github.com/exchanet/method_IRIS)** — Continuous improvement of existing systems.
- **[Method Enterprise Builder](https://github.com/exchanet/method_enterprise_builder_planning)** — Large-scale planning for complex projects.

---

## 🌐 Read in Spanish

**📖 [Leer en Español](./README_ES.md)**

---

## 🤝 Contributing

Contributions are welcome. Issues, new stack examples, and complete project demos are especially appreciated.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes
4. Push and open a Pull Request

---

## 📝 License

MIT — Free to use, modify, and distribute.

---

## 👤 Author

**Francisco J Bernades**
- GitHub: [@exchanet](https://github.com/exchanet)
- Repository: [github.com/exchanet/method_modular_design](https://github.com/exchanet/method_modular_design)

---

**Ready to build modular systems that actually work end to end?** 🔮
