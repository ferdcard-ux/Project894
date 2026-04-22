# Changelog

Todos los cambios relevantes de este proyecto se documentan en este archivo.

Este documento sigue una convención inspirada en Keep a Changelog y versionado semántico cuando aplique.

## [1.1.0] - 2026-04-21

### Added

- Generación del paquete AppImage distribuible para Linux.

### Fixed

- Resiliencia del scraper ante redirecciones inesperadas de Zajuna al dashboard mediante detección temprana.
- Descubrimiento dinámico de `COURSE_ID` activo, eliminando la dependencia estricta de IDs estáticos.
- Implementación de fallback para la apertura del reporte de calificaciones a través del perfil del usuario cuando el acceso directo es rechazado.

## [1.0.0] - 2026-04-21

### Added

- Aplicación nativa en `PySide6`.
- Diálogo de acceso para autenticación con Zajuna.
- Soporte para caché local cifrada de credenciales.
- Soporte para cifrado de la base de datos local.
- Vista `Todas Las Evidencias`.
- Vista `Evidencias Evaluadas`.
- Edición local de instructor y estado desde tabla.
- Búsqueda sobre la tabla activa.
- Exportación a Excel.
- Extracción automatizada con `Playwright`.

### Changed

- Migración de la interfaz desde una aproximación previa en Flet hacia ejecución nativa con `PySide6`.
- Reestructuración del flujo de datos para persistencia local sobre SQLite.

### Security

- Separación entre clave de caché local y clave de cifrado de base de datos.
- Preparación de compatibilidad con claves heredadas para descifrado de sesiones previas.
