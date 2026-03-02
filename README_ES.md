# 🔮 Method REFLEX — Arquitectura Modular Universal

**¿Quieres que tu agente de codificación IA construya sistemas modulares completos y listos para producción — con un Panel Admin estilo WordPress — de forma automática?**

Un método universal para cualquier agente de codificación IA para construir aplicaciones modulares limpias con un Core sin lógica, módulos auto-descriptivos, UI Packs intercambiables y un Panel Admin y dashboard completamente auto-generados. Sin cableado manual. Sin valores hardcodeados. Sin UI olvidada.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-2.0.0-blue.svg)]()
[![Agent: Any](https://img.shields.io/badge/agente-cualquiera-green.svg)]()
[![Stack: Any](https://img.shields.io/badge/stack-cualquiera-green.svg)]()
[![Language: ES/EN](https://img.shields.io/badge/Idioma-ES%2FEN-blue.svg)](./README.md)

**Repositorio:** [github.com/exchanet/method_modular_design](https://github.com/exchanet/method_modular_design)

---

> ⚠️ **¿Quieres resultados de nivel profesional?**
> Method REFLEX se ocupa de la arquitectura, la modularidad y la generación de UI. Para código de calidad producción con cobertura de tests ≥99%, cero vulnerabilidades y ciclos de validación sistemáticos, úsalo junto a **[Method PDCA-T](https://github.com/exchanet/method_pdca-t_coding_Cursor)**.
> REFLEX construye el sistema correcto. PDCA-T lo construye correctamente.

---

## 🎯 ¿Qué Hace Method REFLEX?

Method REFLEX instruye a cualquier agente de codificación IA para construir una aplicación completamente modular donde:

- ✅ **Cada módulo es auto-descriptivo** mediante un `manifest.json` escrito antes que cualquier código
- ✅ **El Core tiene cero lógica de negocio** — solo descubre módulos y lee manifests
- ✅ **El Panel Admin se auto-genera** leyendo todos los manifests — nunca se codifica manualmente
- ✅ **El dashboard se auto-genera** a partir de las métricas y widgets declarados
- ✅ **Los settings nunca están hardcodeados** — todo valor configurable vive en el manifest y es editable desde el Panel Admin
- ✅ **Los UI Packs son intercambiables** — activa o desactiva temas y overrides desde el Panel Admin
- ✅ **Añadir un módulo** = crear una carpeta con `manifest.json` + handlers. Nada más.
- ✅ **Eliminar un módulo** = borrar la carpeta. Desaparece completamente del Panel Admin.
- ✅ **Funciona con cualquier stack** — Python, Node.js, Go, PHP, Java, cualquier lenguaje y framework
- ✅ **Funciona con cualquier agente** — Cursor, Windsurf, GitHub Copilot, Claude, ChatGPT, Aider

---

## 🧩 Qué Se Construye

### El Core
Motor de arranque que escanea el directorio de módulos, valida cada `manifest.json`, resuelve dependencias, arranca módulos en orden y expone una Admin API estándar. El Core no tiene ningún conocimiento de lo que hace cada módulo.

### El Motor REFLEX
Capa de introspección dentro del Core que lee todos los manifests y construye el árbol de navegación del Admin, el registro de widgets del dashboard y el registro de schemas de settings.

### Los Módulos
Cada módulo es una carpeta autocontenida con un `manifest.json` que declara settings, capacidades, hooks y dependencias.

### El Panel Admin
Renderer dinámico que lee la Admin API del Core y genera la interfaz completa automáticamente. Cero referencias hardcodeadas. Añadir un módulo lo añade al Panel Admin. Eliminar un módulo lo elimina.

### El Sistema de UI Packs
Módulos de tipo `ui` que proporcionan temas, overrides de componentes y variables de estilo. Intercambiables desde el Panel Admin.

---

## 📐 Cómo Funciona

### El manifest es el módulo

```json
{
  "id": "activity-logger",
  "name": "Activity Logger",
  "section": "monitoring",

  "settings": {
    "retention_days": { "type": "integer", "label": "Retención (días)", "default": 90, "ui": "slider" },
    "log_level":      { "type": "select",  "label": "Nivel de Log", "default": "info",
                        "options": ["debug", "info", "warn", "error"] }
  },

  "capabilities": [
    { "type": "view",   "label": "Activity Logs",   "data": "ActivityLogger.getAll" },
    { "type": "action", "label": "Exportar CSV",     "handler": "ActivityLogger.exportCsv" },
    { "type": "action", "label": "Limpiar Logs",     "handler": "ActivityLogger.clearOld", "dangerous": true },
    { "type": "metric", "label": "Eventos Hoy",      "data": "ActivityLogger.getTodayCount" }
  ]
}
```

Este manifest produce automáticamente — con cero código UI adicional:

```
Panel Admin
└── Monitoring
    └── Activity Logger
        ├── Activity Logs               ← tabla de datos
        │   ├── [Exportar CSV]          ← botón de acción
        │   └── [Limpiar Logs] ⚠        ← acción peligrosa (confirmación)
        └── Configuración
            ├── Retención: ━━●━━ 90     ← slider
            └── Nivel de Log: [info ▾]  ← select

Dashboard
└── Eventos Hoy: 1.247                 ← métrica
```

---

## 🚀 Inicio Rápido

### 1. Instala enet (una vez, global)

```bash
npm install -g @exchanet/enet
```

[`enet`](https://github.com/exchanet/enet) es el gestor de methods de exchanet. Detecta tu agente automáticamente e instala los adapters en el lugar correcto.

### 2. Instala Method REFLEX en tu proyecto

```bash
enet install reflex
```

enet detecta si usas Cursor, Windsurf o GitHub Copilot y coloca el adapter correctamente. Sin copiar nada manualmente.

> **Instalación manual (sin enet):** copia el adapter para tu agente desde la carpeta `adapters/` — `cursor.md`, `windsurf.md`, `copilot.md` o `generic.md`.

### 3. Dale un spectech a tu agente

```
Construye un SaaS de gestión de proyectos.
Stack: FastAPI + React. Base de datos: PostgreSQL. Deploy: Railway.
Módulos: proyectos, tareas, miembros del equipo, facturación, registro de actividad.
```

### 4. El agente construye el sistema completo

1. Declara la arquitectura y espera tu confirmación
2. Construye el Core con motor REFLEX y Admin API
3. Crea cada módulo — manifest primero, luego handlers
4. Construye el Panel Admin como renderer dinámico puro
5. Verifica que cada módulo aparece correctamente antes de marcarlo como completo

---

## 📁 Estructura del Repositorio

```
method-reflex/
├── METHOD.md                    ← Documentación completa del método
├── README.md                    ← Versión en inglés
├── README_ES.md                 ← Este archivo (español)
│
├── adapters/
│   ├── cursor.md                ← Formato de reglas para Cursor
│   ├── windsurf.md              ← Formato de reglas para Windsurf
│   ├── copilot.md               ← Instrucciones para GitHub Copilot
│   └── generic.md               ← Cualquier agente
│
└── schemas/
    └── manifest.schema.json     ← Contrato universal del manifest (JSON Schema)
```

---

## 🔮 Conceptos Clave

### Tipos de módulo

| Tipo | Propósito |
|---|---|
| `functional` | Lógica de negocio — productos, usuarios, facturación, etc. |
| `integration` | Servicios externos — Stripe, SendGrid, S3, etc. |
| `ui` | Packs de temas y componentes — intercambiables |
| `core` | Sistema — auth, base de datos, caché, etc. |

### Tipos de capacidad

| Tipo | Produce en la UI |
|---|---|
| `view` | Tabla de datos con filtros en el Panel Admin |
| `action` | Botón que ejecuta lógica (con confirmación opcional) |
| `metric` | Número o tarjeta de estadística en el dashboard |
| `widget` | Componente rico de dashboard con UI personalizada |
| `page` | Página personalizada completa en el Panel Admin |

---

## 📏 Las Reglas No Negociables

```
1. Sin manifest = el módulo no existe.
2. Manifest antes que código. Siempre.
3. Cero configuración hardcodeada.
4. El Core no tiene lógica de negocio.
5. El Panel Admin es un renderer, no un destino.
6. Un módulo está completo solo cuando el Panel Admin lo refleja.
7. Eliminar la carpeta de un módulo lo elimina completamente.
```

---

## 🌍 Compatibilidad

| Dimensión | Compatible |
|---|---|
| Agentes | Cursor, Windsurf, GitHub Copilot, Claude, ChatGPT, Aider, cualquiera |
| Backend | Python, Node.js, Go, Ruby, PHP, Java, cualquiera |
| Frontend | React, Vue, Angular, Svelte, HTML puro, cualquiera |
| Base de datos | PostgreSQL, MySQL, MongoDB, SQLite, cualquiera |
| Deploy | Vercel, Railway, Fly.io, AWS, Docker, cualquiera |

---

## 📖 Métodos Relacionados

- **[Method PDCA-T](https://github.com/exchanet/method_pdca-t_coding_Cursor)** ⭐ Recomendado — ≥99% cobertura de tests, cero vulnerabilidades, validación sistemática. REFLEX construye el sistema correcto. PDCA-T lo construye correctamente.
- **[Method IRIS](https://github.com/exchanet/method_IRIS)** — Mejora continua de sistemas existentes.
- **[Method Enterprise Builder](https://github.com/exchanet/method_enterprise_builder_planning)** — Planificación a gran escala para proyectos complejos.

---

## 🌐 Read in English

**📖 [Read in English](./README.md)**

---

## 🤝 Contribuir

1. Fork del repositorio
2. Crea una rama (`git checkout -b feature/MejoraNueva`)
3. Commit y Push
4. Abre un Pull Request

---

## 📝 Licencia

MIT — Libre para usar, modificar y distribuir.

---

## 👤 Autor

**Francisco J Bernades**
- GitHub: [@exchanet](https://github.com/exchanet)
- Repositorio: [github.com/exchanet/method_modular_design](https://github.com/exchanet/method_modular_design)

---

**¿Listo para construir sistemas modulares que realmente funcionen de principio a fin?** 🔮
