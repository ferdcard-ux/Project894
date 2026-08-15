# Plan de Sincronización — Repositorio Público de Distribución (Project894-Public)

> Repo público: https://github.com/ferdcard-ux/Project894 (rama `master`).
> Local: `/home/ferdcard/DEV/Project894-Public`.
> Fecha del análisis: 2026-08-11.

## Propósito

Este repositorio **no contiene código fuente**; centraliza la documentación pública de las tres
plataformas y los releases binarios. Al implementar los planes de mejora de **Linux** y **Windows**
(ver `PLAN_MEJORAS.md` en cada repo), hay que **sincronizar aquí la documentación** y publicar los
nuevos artefactos.

> Estado actual: la documentación está alineada con **Android 2.0.8** y con **escritorio 1.3.0**,
> pero Linux local ya es **1.5.0** y Windows pasará a **1.5.0+** con el plan. Hay desfase.

## Estado actual del repositorio público

| Documento | Estado |
|---|---|
| `README.md` | Dice "Release activo: v1.3.0 (escritorio) / v2.0.8 (Android)" |
| `README-Win.md` | Describe Windows 1.3.0 |
| `BUILD_WINDOWS.md` | Instrucciones de build Windows |
| `CHANGELOG.md` | Tiene entradas 2.0.x de Android; escritorio quedó en 1.3.0 |
| `RELEASE_NOTES.md` | Última entrada Android 2.0.8; faltan notas de escritorio ≥1.4.0 |
| `docs/USERGUIDE.md` | Guía de escritorio (Linux/Windows), aún describe v1.3.0 |
| `docs/USERGUIDE-Android.md` | Alineada a Android 2.0.x |
| `docs/FAQ.md` | FAQ escritorio |
| `docs/FAQ-Android.md` | FAQ Android |
| `docs/ARCHITECTURE.md` | Arquitectura del repo público |
| `docs/PUBLISHING.md` | Guía de publicación de artefactos |
| `LICENSE`, `SECURITY.md`, `CONTRIBUTING.md`, `DISCLAIMER.md` | Legales |

---

## Tarea 1 — Actualizar la documentación de escritorio (Linux 1.5.0 + Windows 1.5.0)

### 1.1 `README.md`
- Actualizar "Estado actual":
  - `Release activo: v1.5.0 (escritorio) / v2.0.8 (Android)` (tras liberar Linux y Windows 1.5.0).
- En la sección "Escritorio (Linux / Windows)", añadir la lista de capacidades que Linux ya tiene y
  que Windows adoptará con el plan:
  - sistema de notificaciones nativas (bandeja/tray) con alertas de evidencias a vencer,
  - auto-scraping periódico configurable (1–6h),
  - panel de notificaciones con eventos de calendario y anuncios,
  - scraper de anuncios con instructor y fecha correcta,
  - calendario leído desde vista mensual (eventos actuales),
  - selector de curso persistido (opcional, cuando se implemente en escritorio),
  - exportación con plantilla estricta, formato condicional e hipervínculos activos.

### 1.2 `README-Win.md`
- Alinear con la versión Windows **1.5.0** y las nuevas capacidades (notificaciones, panel,
  auto-scraping, exportación con plantilla).

### 1.3 `CHANGELOG.md`
- Añadir entrada `[1.5.0] - escritorio (Linux y Windows)` con:
  - notificaciones nativas con auto-scraping de calendario y anuncios,
  - panel de notificaciones desplegable,
  - configuración (auto-start, notificaciones, intervalo de auto-scraping),
  - persistencia de configuración (`app_settings.json`),
  - minimización a bandeja,
  - logging a archivo (`debug_logger.py`),
  - sincronización de fechas de evidencias en cada ciclo,
  - filtro de títulos genéricos en calendario,
  - mejoras de exportación 1.4.0 (código, orden natural, hipervínculos).
- Registrar cuando corresponda las entradas de scraping 2.0.4–2.0.6 portadas a escritorio
  (calendario mensual, instructor, WAF tri-estado) con su numeración de versión final.

### 1.4 `RELEASE_NOTES.md`
- Añadir notas de versión de escritorio **1.5.0** (Linux) y **1.5.0** (Windows) cuando se liberen.

### 1.5 `docs/USERGUIDE.md` (escritorio)
- Documentar:
  - el uso de la campana/panel de notificaciones,
  - la configuración de auto-scraping (intervalo) y notificaciones,
  - la minimización a bandeja y cómo restaurar la ventana,
  - las alertas de evidencias próximas a vencer,
  - el selector de curso (si se implementa),
  - rutas de datos y logs actualizadas (Linux: `~/.local/share/...`; Windows: `LOCALAPPDATA\Project894\data`).

### 1.6 `docs/FAQ.md`
- Añadir entradas nuevas detectadas en el plan:
  - "¿Por qué el calendario mostró eventos vacíos?" → explicar el fix de vista mensual.
  - "¿Por qué no me deja entrar si el sitio responde error de cortafuegos?" → tri-estado WAF.
  - "¿Cómo cambio el curso consultado?" (cuando exista el selector).
  - "¿Los anuncios muestran el instructor?".

### 1.7 `SECURITY.md`
- Mantener las notas de seguridad de escritorio (cifrado local, no PII en logs tras el plan).

---

## Tarea 2 — Publicar artefactos (flujo según `docs/PUBLISHING.md`)

1. Esperar la **build validada** de Linux (`dist/Project894-x86_64.AppImage`) y Windows
   (`dist/Project894.exe`) de los planes respectivos.
2. Publicar release para escritorio `v1.5.0` (Linux y/o Windows según se liberen):
   - assets: `Project894-x86_64.AppImage` y `Project894.exe`.
3. Mantener el release Android **2.0.8** vigente (sin cambios).
4. Verificar:
   - nombres de archivo correctos,
   - versiones coherentes en `README`, `CHANGELOG`, `RELEASE_NOTES`,
   - ausencia de código fuente o datos de usuario,
   - enlaces de descarga operativos.

---

## Tarea 3 — Verificación final

- Revisar que `README.md` y `docs/ARCHITECTURE.md` describan el modelo de distribución con las tres
  plataformas coherentes entre sí.
- Confirmar que no queden referencias a "1.3.0" como versión activa de escritorio.
- Confirmar que `RELEASE_NOTES.md` y `CHANGELOG.md` mantengan el formato y convención actuales
  (Keep a Changelog, sin tildes en este repo).

---

## Orden de ejecución

1. Liberar **Linux 1.5.0** (implementar `PLAN_MEJORAS.md` de Linux → construir AppImage).
2. Liberar **Windows 1.5.0** (implementar `PLAN_MEJORAS.md` de Windows → construir `.exe`).
3. Ejecutar **Tarea 1** (docs) y **Tarea 2** (releases) de este plan en el orden que se libere cada
   plataforma.
4. Ejecutar **Tarea 3** (verificación).

## Archivos afectados (resumen)

- `README.md`
- `README-Win.md`
- `CHANGELOG.md`
- `RELEASE_NOTES.md`
- `docs/USERGUIDE.md`
- `docs/FAQ.md`
- `SECURITY.md`
- Releases de GitHub (assets `AppImage` / `.exe`)
