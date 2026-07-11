# Changelog

Todos los cambios relevantes de este proyecto se documentan en este archivo.

Este documento sigue una convencion inspirada en Keep a Changelog y versionado semantico cuando aplique.

## [Unreleased]

## [1.8.0] - 2026-07-10

### Added
- **Nueva plataforma: Android** (`Project894-android-1.8.0.apk`).
- Pop-up de terminos y condiciones obligatorio en la primera ejecucion en Android.
- Pantalla de notificaciones con eventos de calendario y anuncios.
- Auto-limpieza de logs: conserva solo los 3 archivos mas recientes en `.Project894`.
- Correccion de anuncios en Android: eliminado auth check que bloqueaba el scraping.
- **Sistema de actualizacion in-app en Android**: la app consulta los releases de GitHub, notifica al usuario si hay una nueva version, descarga el APK con barra de progreso y abre el instalador del sistema.

### Changed
- Version de Android actualizada a `1.8.0` en toda la documentacion y codigo.
- APK renombrado a formato `Project894-android-<version>.apk`.
- Directorio de logs cambiado a `.Project894` (oculto).
- Los archivos de log ahora se sobrescriben en lugar de duplicarse en MediaStore.

## [1.3.0] - 2026-04-28

Actualizacion documental y de artefacto Windows sincronizada publicamente el `2026-04-29` sobre el release activo `v1.3.0`.

### Added

- Control centralizado para ediciones pendientes en campos de instructor y fechas, con confirmacion antes de descartar cambios al perder foco, cerrar sesion o cerrar la ventana principal.
- Worker dedicado para el inicio de sesion, con notificaciones de progreso visibles durante la validacion y preparacion de la sesion local.
- Guia publica especifica para Windows en `README-Win.md`.
- Guia publica de flujo de reemplazo del ejecutable en `BUILD_WINDOWS.md`.

### Changed

- Validacion y normalizacion del instructor ajustadas para aceptar un area opcional al final del nombre, por ejemplo `NOMBRE APELLIDO - TIC`, manteniendo el formato en mayusculas.
- Sincronizacion de sugerencias de instructor entre tarjetas despues de guardar cambios locales.
- Estilo visual de los `QMessageBox` renovado con iconografia personalizada, botones consistentes y ancho adaptable al contenido.
- Dialogo de acceso ampliado en altura para dar mas espacio al contenido y a los estados de error.
- Arranque de la ventana principal ajustado para diferir la carga inicial de tarjetas y mejorar la percepcion de rapidez al abrir la interfaz.
- Extraccion de `Todas Las Evidencias` optimizada para reutilizar fechas visibles desde el listado del curso antes de navegar al detalle de cada actividad.
- Flujo de vistas sin datos locales simplificado para mostrar un unico modal por vista, combinando la notificacion de ausencia de evidencias y la advertencia sobre la duracion estimada de la extraccion.
- README, FAQ, guia de usuario y guia de publicacion actualizados para reflejar el reemplazo del `Project894.exe` dentro del release activo `v1.3.0`.

### Fixed

- Correccion del flujo de edicion en fechas e instructor para evitar perdidas silenciosas de cambios y permitir reintento inmediato cuando la validacion falla.
- Correccion de los cuadros de dialogo para que el texto largo se ajuste automaticamente sin quedar recortado.
- Correccion de los avisos de validacion y mensajes operativos para que utilicen la misma presentacion visual en toda la interfaz.
- Correccion del flujo de autenticacion para evitar bloqueos de la UI durante fallos externos de Zajuna o de conectividad, con reintentos automaticos y mensajes claros al usuario.
- Correccion del proceso de extraccion para reducir la sensacion de bloqueo durante sincronizaciones largas y reportar mejor el progreso mientras se guarda en la base local.
- Correccion del traspaso entre `LoginDialog` y `MainWindow` para cerrar el dialogo de acceso antes de procesar la carga inicial y evitar que quede en segundo plano tras abrir la interfaz principal.
- Correccion del arranque del navegador interno en extraccion y validacion para evitar fallos por deteccion incompleta del runtime empaquetado.
- Correccion de la resolucion de rutas de datos y logs en el `.exe` de Windows, mostrando al usuario la ubicacion exacta de `auth_debug.log`.

## [1.2.0] - 2026-04-26

### Added

- Distribucion publica prevista para `Project894-x86_64.AppImage` y `Project894.exe`.
- Documentacion de la version `1.2.0` alineada con la interfaz `Hybrid Card-List View`.
- Filtros por vista para `Todas Las Evidencias` y `Evidencias Evaluadas`.
- Opcion `Proximas a vencer` para deteccion rapida de evidencias cercanas al vencimiento.

### Changed

- Presentacion del producto adaptada a un esquema de releases por plataforma en lugar de un repositorio de codigo.
- Release notes actualizadas para cubrir Linux y Windows dentro de la misma version publica.

### Fixed

- Referencias publicas obsoletas a una UI basada unicamente en tablas.

## [1.1.0] - 2026-04-21

### Added

- Primera distribucion publica del paquete AppImage para Linux.

### Fixed

- Resiliencia del scraper ante redirecciones inesperadas de Zajuna al dashboard mediante deteccion temprana.
- Descubrimiento dinamico de `COURSE_ID` activo, eliminando la dependencia estricta de IDs estaticos.
- Implementacion de fallback para la apertura del reporte de calificaciones a traves del perfil del usuario cuando el acceso directo es rechazado.
- Incorporacion inicial del ejecutable validado para Windows dentro de la linea publica del producto.

## [1.0.0] - 2026-04-21

### Added

- Aplicacion nativa en `PySide6`.
- Dialogo de acceso para autenticacion con Zajuna.
- Soporte para cache local cifrada de credenciales.
- Soporte para cifrado de la base de datos local.
- Vista `Todas Las Evidencias`.
- Vista `Evidencias Evaluadas`.
- Edicion local de instructor y estado desde la vista principal.
- Busqueda sobre la vista activa.
- Exportacion a Excel.
- Extraccion automatizada con `Playwright`.

### Changed

- Migracion de la interfaz desde una aproximacion previa en Flet hacia ejecucion nativa con `PySide6`.
- Reestructuracion del flujo de datos para persistencia local sobre SQLite.

### Security

- Separacion entre clave de cache local y clave de cifrado de base de datos.
- Preparacion de compatibilidad con claves heredadas para descifrado de sesiones previas.
