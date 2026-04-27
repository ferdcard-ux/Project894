# Changelog

Todos los cambios relevantes de este proyecto se documentan en este archivo.

Este documento sigue una convención inspirada en Keep a Changelog y versionado semántico cuando aplique.

## [Unreleased]

### Changed

- Repositorio público reestructurado para funcionar como canal de distribución sin código fuente.
- Documentación principal adaptada para publicar releases binarios de Linux y Windows desde un único punto.
- Guías actualizadas para reflejar instalación pública, consumo de releases y responsabilidades de publicación.
- Documentación pública de la versión 1.2.0 ajustada para reflejar la convivencia de `Project894-x86_64.AppImage` y `Project894.exe` dentro del mismo release.

### Added

- Guía de publicación en `docs/PUBLISHING.md` para centralizar el proceso de releases multiplataforma.

## [1.2.0] - 2026-04-26

### Added

- Distribución pública prevista para `Project894-x86_64.AppImage` y `Project894.exe`.
- Documentación de la versión 1.2.0 alineada con la interfaz `Hybrid Card-List View`.
- Filtros por vista para `Todas Las Evidencias` y `Evidencias Evaluadas`.
- Opción `Próximas a vencer` para detección rápida de evidencias cercanas al vencimiento.

### Changed

- Presentación del producto adaptada a un esquema de releases por plataforma en lugar de un repositorio de código.
- Release notes actualizadas para cubrir Linux y Windows dentro de la misma versión pública.

### Fixed

- Referencias públicas obsoletas a una UI basada únicamente en tablas.

## [1.1.0] - 2026-04-21

### Added

- Primera distribución pública del paquete AppImage para Linux.

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
- Edición local de instructor y estado desde la vista principal.
- Búsqueda sobre la vista activa.
- Exportación a Excel.
- Extracción automatizada con `Playwright`.

### Changed

- Migración de la interfaz desde una aproximación previa en Flet hacia ejecución nativa con `PySide6`.
- Reestructuración del flujo de datos para persistencia local sobre SQLite.

### Security

- Separación entre clave de caché local y clave de cifrado de base de datos.
- Preparación de compatibilidad con claves heredadas para descifrado de sesiones previas.
