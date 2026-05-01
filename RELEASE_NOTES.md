# Notas de la version

## Version 1.3.0

Fecha funcional de la version: `2026-04-28`
Fecha de actualizacion publica del artefacto Windows: `2026-04-29`

### Resumen

`Project894` consolida una aplicacion de escritorio para automatizar la consulta y gestion de evidencias academicas en Zajuna. El release `v1.3.0` mantiene los artefactos de Linux y Windows, y esta actualizacion reemplaza especificamente `Project894.exe` por la compilacion Windows validada mas reciente junto con la documentacion faltante de esta variante.

### Artefactos publicados

- `Project894-x86_64.AppImage` para Linux
- `Project894.exe` para Windows

### Novedades funcionales visibles en Windows

- edicion local protegida para instructor y fechas
- mensajes operativos unificados en la interfaz
- aviso unico cuando una vista no tiene datos locales y requiere extraccion
- liberacion correcta del dialogo de acceso al abrir la ventana principal
- reutilizacion mejorada de datos visibles durante la extraccion general
- exportacion a Excel respetando la vista filtrada actual

### Mejoras tecnicas visibles en la release

- validacion de acceso desacoplada con `worker` para mantener la interfaz responsiva
- normalizacion de instructor ampliada para aceptar areas opcionales
- rutas de datos y logs del `.exe` resueltas de forma estable en `LOCALAPPDATA\\Project894\\data`
- documentacion publica actualizada para reflejar el estado real de la variante Windows `1.3.0`

### Consideraciones operativas

- En Linux, otorgue permisos de ejecucion al archivo `.AppImage` antes de abrirlo
- En Windows, valide el origen del ejecutable antes de permitir su ejecucion
- Los datos siguen siendo locales al equipo del usuario
- Si ocurre un error de autenticacion o scraping en Windows, revise `auth_debug.log` en `LOCALAPPDATA\\Project894\\data`
