# METHOD REFLEX — GitHub Copilot Instructions
> Universal Modular Architecture · v1.0.0 · @exchanet
> Place this file as: .github/copilot-instructions.md

You are building a modular application using Method REFLEX. Follow these instructions for every task in this project.

## Core Principle

Every module declares what it does in a `manifest.json` file before any code is written. The Core reads all manifests and automatically generates the Admin Panel navigation, settings forms, and dashboard widgets. You never manually connect a module to the Admin Panel — the manifest does it.

## Absolute Rules

- Write `manifest.json` before any handler, model, route, or component
- Every configurable value must be in `manifest.settings` and read via `context.settings.get("key")` — never hardcoded
- The Core contains zero business logic
- A module is not done until it appears correctly in the Admin Panel
- Removing a module folder must require zero code changes elsewhere

## When you cannot complete a manifest

Stop. Tell the user:
> "I cannot complete the manifest for [module] because I don't understand [aspect]. Before I continue, I need you to clarify: [question]"

Never proceed with a partial manifest. Never assume. Wait.

## Manifest Structure

```json
{
  "id": "kebab-case-id",
  "name": "Human Readable Name",
  "version": "1.0.0",
  "type": "functional",
  "section": "admin-nav-section",
  "dependencies": [],
  "hooks": { "event.name": "ClassName.method" },
  "settings": {
    "key": { "type": "integer|string|boolean|select", "label": "Label", "default": null, "ui": "slider|toggle|text|select" }
  },
  "capabilities": [
    { "type": "view",   "label": "Label", "data": "ClassName.getAll" },
    { "type": "action", "label": "Label", "handler": "ClassName.execute", "dangerous": false },
    { "type": "metric", "label": "Label", "data": "ClassName.getCount" },
    { "type": "widget", "label": "Label", "data": "ClassName.getData", "component": "ComponentName" }
  ]
}
```

## Standard Admin API (Core must expose these)

```
GET  /api/admin/manifest-registry
GET  /api/admin/navigation
GET  /api/admin/settings/:moduleId
POST /api/admin/settings/:moduleId
GET  /api/admin/dashboard
POST /api/admin/action/:moduleId/:actionId
GET  /api/admin/health
```

## Starting a New Project

Ask for the tech stack and deploy target. Declare the architecture. Wait for confirmation. Then build in order: Core → manifest schema → modules → Admin Panel.

## Module Completion Checklist

Before marking any module done:
- [ ] manifest.json valid
- [ ] All handlers implemented
- [ ] Zero hardcoded values
- [ ] Visible in Admin Panel with correct section
- [ ] All capabilities work (views, actions, metrics, settings)
- [ ] Dangerous actions have confirmation dialog
- [ ] Removing folder leaves no trace in Admin Panel
