# Notas de la versión

## Versión 1.3.0

Fecha de referencia: `2026-04-28`

### Resumen

`Project894` consolida una aplicación de escritorio para automatizar la consulta y gestión de evidencias académicas en Zajuna. Esta publicación distribuye la versión `1.3.0` en formato `AppImage` para Linux y `exe` para Windows, con mejoras de estabilidad operativa, edición local más segura y una experiencia multiplataforma coherente.

### Artefactos publicados

- `Project894-x86_64.AppImage` para Linux
- `Project894.exe` para Windows

### Novedades funcionales

- edición local protegida para instructor y fechas
- mensajes operativos unificados en la interfaz
- aviso único cuando una vista no tiene datos locales y requiere extracción
- liberación correcta del diálogo de acceso al abrir la ventana principal
- reutilización mejorada de datos visibles durante la extracción general
- exportación a Excel respetando la vista filtrada actual

### Mejoras técnicas visibles en la release

- validación de acceso desacoplada para mantener la interfaz responsiva
- normalización de instructor ampliada para aceptar áreas opcionales
- conteos directos para detectar si una vista tiene datos locales
- documentación pública alineada con la versión `1.3.0`
- distribución multiplataforma publicada sin exponer código fuente

### Consideraciones operativas

- En Linux, otorgue permisos de ejecución al archivo `.AppImage` antes de abrirlo
- En Windows, valide el origen del ejecutable antes de permitir su ejecución
- Los datos siguen siendo locales al equipo del usuario
- La aplicación puede depender de conectividad con Zajuna para tareas de extracción en línea
