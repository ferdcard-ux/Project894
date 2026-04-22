# Release Notes

## Version 1.1.0

Fecha de referencia: `2026-04-21`

### Resumen

`Project894` consolida una aplicación de escritorio para automatizar la consulta y gestión de evidencias de curso en Zajuna, con enfoque en operación local, edición rápida y resguardo de información sensible. Esta versión introduce mejoras críticas en la estabilidad de la extracción y el empaquetado oficial.

### Incluye

- Interfaz nativa de escritorio en `PySide6`
- Inicio de sesión con documento, tipo de documento y contraseña de Zajuna
- Extracción de:
  - todas las evidencias del curso
  - evidencias evaluadas
- Persistencia local con SQLite
- Edición manual de `Instructor` y `Estado`
- Búsqueda integrada en la tabla actual
- Exportación a archivos `.xlsx`
- Cifrado de base de datos y caché local de acceso
- **Paquete AppImage para Linux**

### Mejoras relevantes de la iteración actual

- **Resiliencia en Scraping**: Detección de redirecciones y descubrimiento dinámico de cursos.
- **Fallbacks de Navegación**: Rutas alternativas para acceder a reportes de calificaciones.
- Tabla principal optimizada para edición rápida.
- Anchos de columnas ajustados para mejorar legibilidad.
- Altura de filas autoajustable según el contenido de `Evidencia`.
- Mejor separación entre extracción, persistencia y UI.

### Dependencias principales

- `PySide6`
- `playwright`
- `cryptography`
- `pandas`
- `openpyxl`
- `plyer`

### Consideraciones operativas

- Requiere `playwright install chromium` antes del primer uso en un entorno limpio (o usar el AppImage que ya lo gestiona).
- El empaquetado AppImage está disponible en `dist/`.
- Se implementaron fallbacks de navegación para mitigar inestabilidades en el portal de Zajuna.
