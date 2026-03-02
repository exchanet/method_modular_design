# METHOD MODULAR DESIGN — Windsurf Rules
> Universal Modular Architecture · v1.0.0 · @exchanet
> Place this file as: .windsurfrules

## PRIMARY DIRECTIVE

You are building a modular application using Method Modular Design. Every module is self-describing via `manifest.json`, written BEFORE any code. The Core reads manifests to auto-generate the Admin Panel, dashboard, and settings UI automatically. You never manually connect backend logic to the Admin Panel.

## ABSOLUTE RULES

1. **No manifest = module does not exist.**
2. **Manifest before code.** Always. No exceptions.
3. **Zero hardcoded configuration.** Every configurable value in `manifest.settings`, read via `context.settings.get("key")`.
4. **Core has no business logic.**
5. **Admin Panel is a renderer, never a destination.**
6. **Module is complete only when Admin Panel reflects it.**
7. **Remove module folder = zero code changes elsewhere.**

## WORKFLOW

**New project:**
Ask for spectech → declare architecture → wait for confirmation → build Core → manifest schema → modules → Admin Panel.

**New module:**
Write manifest.json → validate → implement handlers → place in modules dir → verify in Admin Panel → custom components only if needed.

**Cannot complete manifest?**
Stop immediately. Ask the user what you don't understand. Never proceed with a partial manifest. Never make assumptions.

## MANIFEST

```json
{
  "id": "module-id",
  "name": "Human Name",
  "version": "1.0.0",
  "type": "functional",
  "section": "section-name",
  "dependencies": [],
  "hooks": { "event.name": "ClassName.method" },
  "settings": {
    "key": { "type": "integer|string|boolean|select", "label": "Label", "default": null, "ui": "slider|toggle|text|select" }
  },
  "capabilities": [
    { "type": "view|action|metric|widget", "label": "Label", "data": "Class.method", "handler": "Class.method" }
  ]
}
```

## ADMIN API (standard, same in every project)

```
GET  /api/admin/manifest-registry
GET  /api/admin/navigation
GET  /api/admin/settings/:moduleId
POST /api/admin/settings/:moduleId
GET  /api/admin/dashboard
POST /api/admin/action/:moduleId/:actionId
GET  /api/admin/health
```

## MODULE COMPLETION CHECKLIST

- [ ] manifest.json valid
- [ ] All handlers implemented, zero hardcoded values
- [ ] Appears in Admin Panel with all capabilities working
- [ ] Settings render and save correctly
- [ ] Dangerous actions show confirmation dialog
- [ ] Adding required zero Core changes
- [ ] Removing folder removes it completely from Admin Panel
