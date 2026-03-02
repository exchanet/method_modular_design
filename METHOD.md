# METHOD MODULAR DESIGN — Universal Modular Architecture Method
> Version 1.0.0 · Author: Francisco J Bernades (@exchanet) · License: MIT

---

## / EN / What This Is

A universal method for AI coding agents to build **production-grade modular applications** from scratch, in any language or stack, that automatically generate an Admin Panel, user dashboard, and full configuration UI — without hardcoded values, without manual UI wiring, and without the agent "forgetting" to connect logic to the interface.

This method is **not tied to any framework, language, or tool**. It works with Cursor, Windsurf, GitHub Copilot, Claude, Aider, or any AI coding agent capable of reading instructions.

## / ES / Qué Es Esto

Un método universal para agentes de codificación IA para construir **aplicaciones modulares de nivel producción** desde cero, en cualquier lenguaje o stack, que generen automáticamente un Panel Admin, dashboard de usuario y UI de configuración completa — sin valores hardcodeados, sin cableado manual de UI, y sin que el agente "olvide" conectar la lógica con la interfaz.

Este método **no está vinculado a ningún framework, lenguaje ni herramienta**. Funciona con Cursor, Windsurf, GitHub Copilot, Claude, Aider, o cualquier agente de codificación IA capaz de leer instrucciones.

---

## / EN / The Core Problem This Solves
## / ES / El Problema Central Que Resuelve

**EN:** Standard vibe coding produces systems where:
- Configuration is hardcoded and requires code changes to modify
- The Admin Panel is built manually and disconnects from logic over time
- Adding or removing a module requires touching multiple files across the project
- The agent builds backend logic correctly but "forgets" to surface it in the UI
- There is no single source of truth for what a module does

**This method makes it structurally impossible for those problems to occur.**

---

**ES:** El vibe coding estándar produce sistemas donde:
- La configuración está hardcodeada y requiere cambios de código para modificarse
- El Panel Admin se construye manualmente y se desconecta de la lógica con el tiempo
- Añadir o eliminar un módulo requiere tocar múltiples archivos en el proyecto
- El agente construye la lógica backend correctamente pero "olvida" mostrarla en la UI
- No existe una única fuente de verdad sobre qué hace un módulo

**Este método hace estructuralmente imposible que esos problemas ocurran.**

---

## / EN / The Fundamental Principle
## / ES / El Principio Fundamental

> **EN: A module is its manifest. If it isn't declared, it doesn't exist.**
>
> **ES: Un módulo es su manifest. Si no está declarado, no existe.**

Every module in a system built with this method is self-describing. It declares what it does, what it exposes to the Admin Panel, what settings it offers, and what it shows in the dashboard — before a single line of logic is written.

The Core reads those declarations and generates the Admin Panel, settings UI, and dashboard automatically. The agent never manually wires backend to frontend. **The UI is a consequence of the manifest, not a separate task.**

---

Todo módulo en un sistema construido con este método es auto-descriptivo. Declara qué hace, qué expone al Panel Admin, qué configuraciones ofrece y qué muestra en el dashboard — antes de escribir una sola línea de lógica.

El Core lee esas declaraciones y genera el Panel Admin, la UI de configuración y el dashboard automáticamente. El agente nunca cablea manualmente backend con frontend. **La UI es una consecuencia del manifest, no una tarea separada.**

---

## Glossary / Glosario

| Term / Término | EN Definition | ES Definición |
|---|---|---|
| **Core** | Bootstrap engine. Discovers modules, reads manifests, starts the system. Zero business logic. | Motor de arranque. Descubre módulos, lee manifests, inicia el sistema. Cero lógica de negocio. |
| **Module / Módulo** | Independent, self-contained unit of business logic with its own manifest and handlers. | Unidad independiente y autocontenida de lógica de negocio con su propio manifest y handlers. |
| **Manifest** | `manifest.json` at the root of every module. Single source of truth for what the module is and does. | `manifest.json` en la raíz de cada módulo. Única fuente de verdad sobre qué es y hace el módulo. |
| **Capability / Capacidad** | A declared unit of functionality: a view, action, metric, or setting. | Unidad declarada de funcionalidad: una vista, acción, métrica o configuración. |
| **Admin Panel** | Dynamically generated interface built by reading all manifests. Never coded manually. | Interfaz generada dinámicamente leyendo todos los manifests. Nunca codificada manualmente. |
| **UI Pack** | Optional module of type `ui` that provides themes and component overrides. Swappable. | Módulo opcional de tipo `ui` que provee temas y overrides de componentes. Intercambiable. |
| **Handler** | A function in the module's business logic, referenced by name from the manifest. | Función en la lógica de negocio del módulo, referenciada por nombre desde el manifest. |
| **REFLEX Engine** | The Core's introspection engine that reads manifests and generates the Admin Panel and dashboard. | Motor de introspección del Core que lee manifests y genera el Panel Admin y dashboard. |
| **Settings Store** | Persistent key-value store for all module configuration. Namespaced per module. | Almacén persistente clave-valor para toda la configuración de módulos. Espaciado por módulo. |

---

## The Method: Eight Phases / El Método: Ocho Fases

---

### PHASE 0 — Stack Detection & Architecture Declaration
### FASE 0 — Detección de Stack y Declaración de Arquitectura

**Trigger / Disparador:** Start of every new project / Inicio de cada proyecto nuevo.

**Goal / Objetivo:** Understand the user's context before writing anything / Entender el contexto del usuario antes de escribir nada.

**EN:** The agent must:

1. **Read the user's spectech** (technical specification). If none is provided, ask before proceeding. Minimum required:
   - Backend language and framework
   - Frontend framework (if applicable)
   - Database
   - Deployment target (Vercel, Railway, Docker, etc.)

2. **Declare the architecture** it will build. Example:

```
ARCHITECTURE DECLARATION / DECLARACIÓN DE ARQUITECTURA
──────────────────────────────────────────────────────
Backend:     FastAPI (Python)
Frontend:    React + Vite
Database:    PostgreSQL via SQLAlchemy
Deploy:      Railway (monorepo)

Structure:
→ Core lives in:         /backend/core/
→ Modules live in:       /backend/modules/
→ Admin Panel lives in:  /frontend/src/admin/
→ Admin API lives in:    /backend/api/admin/
→ Manifest schema:       /manifest.schema.json

Awaiting confirmation before proceeding.
En espera de confirmación antes de continuar.
──────────────────────────────────────────────────────
```

3. **Wait for user confirmation.** Do not write any code until confirmed.

**ES:** El agente debe:

1. **Leer el spectech del usuario** (especificación técnica). Si no se proporciona, preguntar antes de continuar. Mínimo requerido:
   - Lenguaje y framework backend
   - Framework frontend (si aplica)
   - Base de datos
   - Destino de despliegue (Vercel, Railway, Docker, etc.)

2. **Declarar la arquitectura** que va a construir (ver ejemplo arriba).

3. **Esperar confirmación del usuario.** No escribir ningún código hasta confirmación.

**Rule / Regla:** If the stack is ambiguous, ask. Never assume silently. / Si el stack es ambiguo, preguntar. Nunca asumir en silencio.

---

### PHASE 1 — Core Construction
### FASE 1 — Construcción del Core

**Trigger / Disparador:** Once architecture is confirmed / Una vez confirmada la arquitectura.

**Goal / Objetivo:** Build the foundation all modules depend on / Construir la base de la que dependen todos los módulos.

The Core implements exactly these responsibilities and **no others**:

**1.1 Module Discovery / Descubrimiento de Módulos**
Scan the modules directory. Detect all subdirectories with a valid `manifest.json`. Register them in dependency order.

**1.2 Manifest Validation / Validación de Manifests**
Validate each manifest against `manifest.schema.json`. A module with an invalid or missing manifest is **rejected at boot with a clear error**. Never silent failure.

**1.3 Dependency Resolution / Resolución de Dependencias**
Read `manifest.dependencies`. Boot modules in correct order. If a required dependency is missing, halt and report.

**1.4 Handler Registry / Registro de Handlers**
Build a registry mapping every `ModuleName.methodName` reference to its actual implementation.

**1.5 Hook System / Sistema de Hooks**
Implement an event/hook system. Modules declare hooks in their manifest. The Core dispatches events to registered handlers.

**1.6 Settings Store / Almacén de Configuración**
Persistent key-value store, namespaced by module ID. Settings from `manifest.settings` are initialized with their defaults on first boot. **Never hardcoded elsewhere.**

**1.7 REFLEX Engine / Motor REFLEX**
Read all registered manifests and build:
- Admin navigation tree (grouped by `section`)
- Dashboard widget registry
- Settings schema registry (for generating forms)
- Capabilities index (for Admin API)

**1.8 Admin API / API Admin**
Expose these standard endpoints (identical regardless of stack):

```
GET  /api/admin/manifest-registry          → All registered manifests
GET  /api/admin/navigation                 → Admin nav tree from REFLEX
GET  /api/admin/settings/:moduleId         → Current settings for a module
POST /api/admin/settings/:moduleId         → Update settings for a module
GET  /api/admin/dashboard                  → All dashboard widget configs
POST /api/admin/action/:moduleId/:actionId → Execute a declared action
GET  /api/admin/health                     → Health status of all modules
```

**Core rules / Reglas del Core:**
- The Core has **no business logic. None. / Cero lógica de negocio. Ninguna.**
- The Core does not know what any module does. It only knows modules exist and have manifests.
- Adding a module requires **zero Core changes**.
- Removing a module requires **zero Core changes**.

---

### PHASE 2 — Manifest Schema Definition
### FASE 2 — Definición del Schema del Manifest

**Trigger / Disparador:** Immediately after Core structure is established / Inmediatamente después de establecer la estructura del Core.

**Goal / Objetivo:** Define the contract every module must fulfill / Definir el contrato que todo módulo debe cumplir.

Create `manifest.schema.json` at the project root. The manifest the agent writes is **intentionally simple**:

```json
{
  "id": "module-id",
  "name": "Human Readable Name",
  "version": "1.0.0",
  "type": "functional",
  "section": "admin-section-name",

  "dependencies": [],

  "hooks": {
    "event.name": "ModuleName.handlerMethod"
  },

  "settings": {
    "setting_key": {
      "type": "integer|string|boolean|select",
      "label": "Human readable label",
      "default": "default_value",
      "ui": "slider|toggle|text|select|textarea|code"
    }
  },

  "capabilities": [
    {
      "type": "view|action|metric|widget|page",
      "label": "Human readable label",
      "data": "ModuleName.handlerMethod",
      "handler": "ModuleName.handlerMethod",
      "dangerous": false,
      "permissions": ["scope:action"],
      "description": "Shown in Admin Panel"
    }
  ]
}
```

**Capability types / Tipos de capacidad:**

| Type | EN Purpose | ES Propósito | Required fields |
|---|---|---|---|
| `view` | Data table or list in Admin Panel | Tabla de datos o lista en Panel Admin | `label`, `data` |
| `action` | Button that executes logic | Botón que ejecuta lógica | `label`, `handler` |
| `metric` | Number or stat for dashboard | Número o estadística para dashboard | `label`, `data` |
| `widget` | Rich dashboard component | Componente rico de dashboard | `label`, `data`, `component` |
| `page` | Full custom page in Admin Panel | Página personalizada completa en Panel Admin | `label`, `route`, `component` |

**Rule / Regla:** This simplified manifest is what the agent writes. REFLEX expands it internally. **The agent never writes the expanded form.**

---

### PHASE 3 — Module Creation Protocol
### FASE 3 — Protocolo de Creación de Módulos

**Trigger / Disparador:** Every time a new module is created / Cada vez que se crea un nuevo módulo.

**Goal / Objetivo:** Ensure every module is complete and connected to Admin Panel from birth / Garantizar que cada módulo está completo y conectado al Panel Admin desde su creación.

This phase is a **strict sequence**. The agent cannot proceed to the next step until the current one is complete.

---

#### Step 3.1 — Write the manifest first / Escribir el manifest primero

Before any logic, route, model, or component: **write `manifest.json`.**

The manifest is complete when:
- All settings the module will use are declared / Todos los settings que usará el módulo están declarados
- All capabilities the module will expose are declared / Todas las capacidades que expondrá están declaradas
- All hooks the module listens to are declared / Todos los hooks que escucha están declarados
- All dependencies are listed / Todas las dependencias están listadas

**If the agent cannot complete the manifest, it must stop and ask:**

```
EN: "I cannot complete the manifest for [module name] because I don't 
    understand [specific aspect]. Before I continue, I need you to clarify: 
    [specific question]."

ES: "No puedo completar el manifest de [nombre del módulo] porque no entiendo 
    [aspecto específico]. Antes de continuar, necesito que aclares: 
    [pregunta específica]."
```

**The agent must never proceed with a partial manifest.** A partial manifest produces a partially visible module in the Admin Panel, which is a broken experience.

---

#### Step 3.2 — Validate the manifest / Validar el manifest

Run validation against `manifest.schema.json`. Fix all errors before proceeding. Do not move to step 3.3 with validation errors.

---

#### Step 3.3 — Implement handlers / Implementar handlers

Implement every handler referenced in the manifest. Each handler:
- Receives a `context` object (user, permissions, settings access)
- Reads settings via `context.settings.get('key')` — **never from hardcoded values**
- Returns typed data
- Has **no knowledge of HTTP, routes, or UI**

---

#### Step 3.4 — Register the module / Registrar el módulo

Place the module in the modules directory. The Core discovers it on next boot. **No other registration required.**

---

#### Step 3.5 — Verify Admin Panel integration / Verificar integración con Panel Admin

Boot the system. Confirm:
- The module appears in Admin navigation under the correct section
- All declared views render with data
- All declared actions appear as buttons
- All declared settings appear with correct UI widgets
- All declared metrics appear in the dashboard

**This step is not optional. / Este paso no es opcional.**
A module is not complete until step 3.5 passes.

---

#### Step 3.6 — Implement custom UI components (if needed) / Implementar componentes UI personalizados (si es necesario)

If a capability declares a `component` field, build that component now. Custom components:
- Receive `data` and `settings` as props
- **Never fetch data directly** — data comes from the manifest's `data` handler via Admin API
- The manifest remains the source of truth

---

### PHASE 4 — UI Pack System
### FASE 4 — Sistema de UI Packs

**Trigger / Disparador:** When the user wants to customize the interface / Cuando el usuario quiere personalizar la interfaz.

**Goal / Objetivo:** Make the UI completely swappable without touching module logic / Hacer la UI completamente intercambiable sin tocar la lógica de módulos.

A UI Pack is a module of type `ui`:

```json
{
  "id": "my-theme",
  "name": "My Custom Theme",
  "version": "1.0.0",
  "type": "ui",
  "section": "appearance",

  "capabilities": [
    {
      "type": "theme",
      "variables": {
        "primary-color": "#6366f1",
        "font-family": "Inter, sans-serif"
      }
    },
    {
      "type": "component-override",
      "target": "DataTable",
      "component": "CustomDataTable"
    }
  ]
}
```

**Rules / Reglas:**
- Only one UI Pack of type `theme` can be active at a time / Solo un UI Pack de tipo `theme` puede estar activo a la vez
- Activating/deactivating a UI Pack happens from the Admin Panel / La activación/desactivación ocurre desde el Panel Admin
- Removing a UI Pack folder removes it on next boot / Eliminar la carpeta del UI Pack lo elimina en el próximo arranque
- Module logic is **never aware** of which UI Pack is active / La lógica de módulo nunca sabe qué UI Pack está activo

---

### PHASE 5 — Admin Panel Construction
### FASE 5 — Construcción del Panel Admin

**Trigger / Disparador:** After Core and at least one module exist / Después de que el Core y al menos un módulo existen.

**Goal / Objetivo:** Build the universal Admin Panel renderer / Construir el renderer universal del Panel Admin.

The Admin Panel is a frontend application (in whatever framework the user chose) that:

1. Fetches `/api/admin/manifest-registry` on load
2. Renders navigation from `/api/admin/navigation`
3. Renders settings forms dynamically from the settings schema in each manifest
4. Renders data views by calling the `data` handler via Admin API
5. Renders action buttons that call `/api/admin/action/:moduleId/:actionId`
6. Renders dashboard from `/api/admin/dashboard`

**The Admin Panel contains zero hardcoded references to any module. It is a pure renderer.**

**Required Admin Panel sections / Secciones requeridas del Panel Admin:**

| Section / Sección | EN Content | ES Contenido |
|---|---|---|
| Dashboard | All `metric` and `widget` capabilities | Todas las capacidades `metric` y `widget` |
| Modules | Navigation by `section` field | Navegación por campo `section` |
| Settings | One form per module from `manifest.settings` | Un formulario por módulo desde `manifest.settings` |
| System | Module health, active UI Pack, system info | Salud de módulos, UI Pack activo, info del sistema |

**Admin Panel rules / Reglas del Panel Admin:**
- Never import a module directly / Nunca importar un módulo directamente
- Never hardcode module names, routes, or settings keys / Nunca hardcodear nombres de módulo, rutas o keys
- All data comes from the Admin API / Todos los datos vienen de la Admin API
- Dangerous actions (`"dangerous": true`) require a confirmation dialog / Las acciones peligrosas requieren diálogo de confirmación

---

### PHASE 6 — Settings & Configuration
### FASE 6 — Configuración y Ajustes

**Trigger / Disparador:** Embedded in Phase 3, formalized here / Integrado en Fase 3, formalizado aquí.

**Goal / Objetivo:** Guarantee zero hardcoded configuration anywhere / Garantizar cero configuración hardcodeada en ningún lugar.

**The rule is absolute / La regla es absoluta:** Every value that could ever change without a code deployment must be a declared setting in a manifest.

This includes / Esto incluye:
- Pagination sizes / Tamaños de paginación
- Feature flags / Flags de funcionalidades
- Retention periods / Períodos de retención
- API keys and external service URLs / API keys y URLs de servicios externos
- Email templates / Plantillas de email
- Rate limits / Límites de velocidad
- Display preferences / Preferencias de visualización

**Implementation pattern / Patrón de implementación:**

```python
# NEVER / NUNCA
RETENTION_DAYS = 30

# NEVER / NUNCA
retention = os.getenv("RETENTION_DAYS", 30)

# ALWAYS / SIEMPRE
retention = context.settings.get("retention_days")
# Where "retention_days" is declared in manifest.settings
# Donde "retention_days" está declarado en manifest.settings
```

The settings store is the **only** place where configuration lives. The Admin Panel is the **only** place where configuration is changed. Code never changes configuration.

---

### PHASE 7 — Quality & Completion Gate
### FASE 7 — Control de Calidad y Completitud

**Trigger / Disparador:** Before declaring any module or system "done" / Antes de declarar cualquier módulo o sistema "terminado".

**Goal / Objetivo:** Ensure the system is complete, not just functional / Asegurar que el sistema está completo, no solo funcional.

**Module completeness / Completitud del módulo:**
- [ ] `manifest.json` exists and is valid / existe y es válido
- [ ] All handlers declared in manifest are implemented / Todos los handlers declarados están implementados
- [ ] All settings use `context.settings.get()` — zero hardcoded / Todos los settings usan `context.settings.get()` — cero hardcoded
- [ ] Module appears correctly in Admin Panel navigation / El módulo aparece correctamente en la navegación del Panel Admin
- [ ] All declared views render with real data / Todas las vistas declaradas renderizan con datos reales
- [ ] All declared actions execute without errors / Todas las acciones declaradas ejecutan sin errores
- [ ] All declared metrics show in dashboard / Todas las métricas declaradas aparecen en el dashboard
- [ ] All declared settings render and save correctly / Todos los settings declarados renderizan y guardan correctamente
- [ ] Adding this module required zero Core changes / Añadir este módulo requirió cero cambios en el Core
- [ ] Removing this module folder makes it disappear completely from Admin Panel / Eliminar la carpeta hace que desaparezca completamente del Panel Admin

**System completeness / Completitud del sistema:**
- [ ] Core boots cleanly with all modules / El Core arranca limpiamente con todos los módulos
- [ ] Invalid/missing manifest produces a clear error, not silent failure / Un manifest inválido/ausente produce un error claro, no fallo silencioso
- [ ] Admin Panel loads without errors / El Panel Admin carga sin errores
- [ ] Settings persist across restarts / Los settings persisten entre reinicios
- [ ] Dangerous actions show confirmation dialogs / Las acciones peligrosas muestran diálogos de confirmación
- [ ] System works with zero modules (Core boots, Admin Panel shows empty state) / El sistema funciona con cero módulos
- [ ] System works when a module is removed mid-development / El sistema funciona cuando se elimina un módulo durante el desarrollo

---

### PHASE 8 — Continuous Refinement
### FASE 8 — Refinamiento Continuo

**Trigger / Disparador:** Post-build, on improvement requests / Post-construcción, ante peticiones de mejora.

**Goal / Objetivo:** Improve the system without breaking its architecture / Mejorar el sistema sin romper su arquitectura.

When improving an existing system / Al mejorar un sistema existente:

1. **Never add logic to the Core.** New cross-cutting behavior becomes a module with hooks. / Nunca añadir lógica al Core. El nuevo comportamiento transversal se convierte en un módulo con hooks.
2. **Never hardcode in modules what belongs in settings.** / Nunca hardcodear en módulos lo que pertenece a settings.
3. **If a capability is added to a module, it must be declared in the manifest first.** / Si se añade una capacidad a un módulo, debe declararse en el manifest primero.
4. **If a module is removed, verify the Admin Panel shows no remnants.** / Si se elimina un módulo, verificar que el Panel Admin no muestre restos.
5. **Settings schema changes must be backward compatible** — new settings need default values. / Los cambios en el schema de settings deben ser retrocompatibles — los nuevos settings necesitan valores por defecto.

---

## Non-Negotiable Rules / Reglas No Negociables

These rules are absolute. The agent must never violate them regardless of context, user request, or apparent convenience.

Estas reglas son absolutas. El agente nunca debe violarlas independientemente del contexto, solicitud del usuario o conveniencia aparente.

```
RULE 1 / REGLA 1
EN: No manifest = module does not exist.
    The Core rejects modules without a valid manifest.json. No exceptions.
ES: Sin manifest = el módulo no existe.
    El Core rechaza módulos sin manifest.json válido. Sin excepciones.

RULE 2 / REGLA 2
EN: Manifest before code. Always.
    The manifest.json must be complete before any handler, model,
    route, or component is written.
ES: Manifest antes que código. Siempre.
    El manifest.json debe estar completo antes de escribir cualquier
    handler, modelo, ruta o componente.

RULE 3 / REGLA 3
EN: Zero hardcoded configuration.
    Every configurable value is a declared setting.
    os.getenv() and config files are not settings — they are
    hardcoding with extra steps.
ES: Cero configuración hardcodeada.
    Todo valor configurable es un setting declarado.
    os.getenv() y archivos de config no son settings — son
    hardcoding con pasos extra.

RULE 4 / REGLA 4
EN: Core has no business logic.
    If you find yourself adding domain logic to the Core,
    you are building a module. Create a module.
ES: El Core no tiene lógica de negocio.
    Si estás añadiendo lógica de dominio al Core,
    estás construyendo un módulo. Crea un módulo.

RULE 5 / REGLA 5
EN: Admin Panel is a renderer, not a destination.
    You do not code the Admin Panel to show module X.
    You declare module X's capabilities in its manifest.
    The Admin Panel reads and renders automatically.
ES: El Panel Admin es un renderer, no un destino.
    No codificas el Panel Admin para mostrar el módulo X.
    Declaras las capacidades del módulo X en su manifest.
    El Panel Admin lee y renderiza automáticamente.

RULE 6 / REGLA 6
EN: A module is complete only when the Admin Panel reflects it.
    Working logic + no Admin Panel representation = incomplete module.
    This is not optional.
ES: Un módulo está completo solo cuando el Panel Admin lo refleja.
    Lógica funcionando + sin representación en Panel Admin = módulo incompleto.
    Esto no es opcional.

RULE 7 / REGLA 7
EN: Removing a module folder removes it completely.
    If removing a module requires code changes anywhere else,
    the architecture is broken. Fix it.
ES: Eliminar la carpeta de un módulo lo elimina completamente.
    Si eliminar un módulo requiere cambios de código en otro lugar,
    la arquitectura está rota. Corrígela.
```

---

## Agent Behavior Specification / Especificación de Comportamiento del Agente

### When starting a new project / Al iniciar un proyecto nuevo:
1. Execute Phase 0 — ask for spectech if not provided
2. Declare architecture and **wait for confirmation**
3. Build Core (Phase 1)
4. Define manifest schema (Phase 2)
5. Build modules one by one (Phase 3)
6. Build Admin Panel (Phase 5)
7. Run completion gate (Phase 7)

### When adding a module to an existing project / Al añadir un módulo a un proyecto existente:
1. Write the manifest (Phase 3, Step 3.1)
2. Validate it (Step 3.2)
3. Implement handlers (Step 3.3)
4. Verify Admin Panel integration (Step 3.5)
5. Build custom components if needed (Step 3.6)
6. Run module completion checklist (Phase 7)

### When the agent cannot complete a manifest / Cuando el agente no puede completar un manifest:

The agent **stops immediately** and asks:

```
EN: "I cannot complete the manifest for [module name] because I don't 
    understand [specific aspect]. Before I continue, I need you to clarify:
    [specific question]"

ES: "No puedo completar el manifest de [nombre del módulo] porque no entiendo 
    [aspecto específico]. Antes de continuar, necesito que aclares:
    [pregunta específica]"
```

The agent does not proceed, does not create a partial manifest, does not make assumptions. It waits for the user's answer.

El agente no continúa, no crea un manifest parcial, no hace suposiciones. Espera la respuesta del usuario.

### When a capability requires complex UI / Cuando una capacidad requiere UI compleja:
Declare it in the manifest with `"component": "ComponentName"`. Build the component after the manifest is validated. The component receives data from the handler via the Admin API — **it never fetches directly.**

### When the user requests a hardcoded value / Cuando el usuario solicita un valor hardcodeado:
The agent explains that the value should be a declared setting and offers to add it to the manifest. If the user insists, the agent adds a comment noting the architectural debt.

---

## Manifest Quick Reference / Referencia Rápida del Manifest

```json
{
  "id": "string — kebab-case, unique / único",
  "name": "string — human readable / legible por humanos",
  "version": "string — semver",
  "type": "core | functional | integration | ui",
  "section": "string — admin nav group / grupo de navegación admin",

  "dependencies": ["other-module-id"],

  "hooks": {
    "event.name": "ClassName.methodName"
  },

  "settings": {
    "key_name": {
      "type": "integer | string | boolean | select",
      "label": "string",
      "default": "any / cualquier valor",
      "ui": "slider | toggle | text | select | textarea | number",
      "options": ["only for select type / solo para tipo select"]
    }
  },

  "capabilities": [
    {
      "type": "view | action | metric | widget | page",
      "label": "string",
      "data": "ClassName.method — for view/metric/widget / para view/metric/widget",
      "handler": "ClassName.method — for action / para action",
      "component": "ComponentName — for widget/page with custom UI / para widget/page con UI personalizada",
      "dangerous": false,
      "permissions": ["scope:action"],
      "description": "string — shown in Admin Panel / mostrado en Panel Admin"
    }
  ]
}
```

---

## Complete Example / Ejemplo Completo: Activity Logger Module

### 1. manifest.json (written first / escrito primero)
```json
{
  "id": "activity-logger",
  "name": "Activity Logger",
  "version": "1.0.0",
  "type": "functional",
  "section": "monitoring",

  "dependencies": [],

  "hooks": {
    "user.login":  "ActivityLogger.onLogin",
    "user.logout": "ActivityLogger.onLogout",
    "data.change": "ActivityLogger.onChange"
  },

  "settings": {
    "retention_days": {
      "type": "integer",
      "label": "Log Retention (days)",
      "default": 90,
      "ui": "slider"
    },
    "log_level": {
      "type": "select",
      "label": "Log Level",
      "default": "info",
      "options": ["debug", "info", "warn", "error"],
      "ui": "select"
    },
    "track_reads": {
      "type": "boolean",
      "label": "Track Read Operations",
      "default": false,
      "ui": "toggle"
    }
  },

  "capabilities": [
    {
      "type": "view",
      "label": "Activity Logs",
      "data": "ActivityLogger.getAll",
      "description": "Full log history with filters"
    },
    {
      "type": "action",
      "label": "Export CSV",
      "handler": "ActivityLogger.exportCsv",
      "permissions": ["activity:export"]
    },
    {
      "type": "action",
      "label": "Clear Old Logs",
      "handler": "ActivityLogger.clearOld",
      "dangerous": true,
      "description": "Removes logs older than retention period"
    },
    {
      "type": "metric",
      "label": "Events Today",
      "data": "ActivityLogger.getTodayCount"
    },
    {
      "type": "metric",
      "label": "Active Users (24h)",
      "data": "ActivityLogger.getActiveUsers"
    }
  ]
}
```

### 2. Handler implementation (written after manifest / escrito después del manifest)

```python
class ActivityLogger:
    def __init__(self, context):
        self.ctx = context
        self.db  = context.db

    # Hook handlers
    def onLogin(self, event):
        self._log("user.login", event.user_id)

    def onLogout(self, event):
        self._log("user.logout", event.user_id)

    def onChange(self, event):
        if self.ctx.settings.get("track_reads") or event.type != "read":
            self._log("data.change", event.user_id, event.data)

    # Capability handlers
    def getAll(self, ctx, page=1, limit=50):
        return self.db.query(
            "SELECT * FROM activity_logs ORDER BY created_at DESC"
        )

    def exportCsv(self, ctx):
        logs = self.getAll(ctx, limit=10000)
        return generate_csv(logs)

    def clearOld(self, ctx):
        retention = self.ctx.settings.get("retention_days")
        return self.db.execute(
            "DELETE FROM activity_logs WHERE created_at < NOW() - INTERVAL ? DAY",
            retention
        )

    def getTodayCount(self, ctx):
        return self.db.scalar(
            "SELECT COUNT(*) FROM activity_logs WHERE DATE(created_at) = TODAY()"
        )

    def getActiveUsers(self, ctx):
        return self.db.scalar(
            "SELECT COUNT(DISTINCT user_id) FROM activity_logs "
            "WHERE created_at > NOW() - INTERVAL 24 HOUR"
        )

    # Internal
    def _log(self, event_type, user_id, data=None):
        self.db.insert("activity_logs", {
            "event_type": event_type,
            "user_id":    user_id,
            "data":       data,
            "level":      self.ctx.settings.get("log_level")
        })
```

### 3. Result in Admin Panel (automatic, zero additional code)
### 3. Resultado en Panel Admin (automático, cero código adicional)

```
Admin Panel
└── Monitoring
    └── Activity Logger
        ├── Activity Logs                 ← view capability
        │   ├── [Export CSV]              ← action (requires activity:export)
        │   └── [Clear Old Logs] ⚠        ← dangerous action (confirmation dialog)
        └── Settings
            ├── Log Retention: ━━●━━ 90 days    ← slider
            ├── Log Level:     [info ▾]           ← select
            └── Track Reads:   ○                  ← toggle

Dashboard
├── Events Today:       1,247    ← metric
└── Active Users (24h):    89    ← metric
```

---

## Adapter Notes / Notas sobre Adaptadores

This METHOD.md is the source of truth. The adapters contain the same content formatted for specific tools:

Este METHOD.md es la fuente de verdad. Los adaptadores contienen el mismo contenido formateado para herramientas específicas:

- `adapters/cursor.md`  — Cursor rules format (`.cursor/rules/`)
- `adapters/windsurf.md` — Windsurf rules format (`.windsurfrules`)
- `adapters/copilot.md`  — GitHub Copilot instructions (`.github/copilot-instructions.md`)
- `adapters/generic.md`  — Any agent: Claude, ChatGPT, Aider, etc.

When in doubt, use `adapters/generic.md`. / En caso de duda, usa `adapters/generic.md`.

---

*Method Modular Design v2.0.0 · Francisco J Bernades (@exchanet) · MIT License*
*Contributions welcome / Contribuciones bienvenidas: github.com/exchanet/method_modular_design*
