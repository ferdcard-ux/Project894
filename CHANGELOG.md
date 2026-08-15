# Changelog

Todos los cambios relevantes de este proyecto se documentan en este archivo.

Este documento sigue una convencion inspirada en Keep a Changelog y versionado semantico cuando aplique.

## [Unreleased]

## [2.0.8] - 2026-08-15

### Fixed
- **Exportar logs no abria el share sheet** (Toast "No se pudo compartir el log"): la configuracion
  del FileProvider usaba `root-path`, que en la libreria androidx apunta a la raiz del filesystem
  (`/`), no al almacenamiento externo. La URI quedaba en `/Android/data/...` y nunca coincidia con
  la ruta real → "Failed to find configured root". Se cambio a `external-path` (raiz =
  `/storage/emulated/0`), que si contiene la ruta de los logs.

### Changed
- **Exportar logs ahora comprime todos los registros en `.zip`**: `Project894_logs_<fecha>.zip`
  con los ultimos `app_log_*.txt` de `.logs` (hasta 3, ~3 dias) en la cache privada de la app y lo
  comparte con el share sheet del sistema. Reemplaza el comportamiento anterior que solo compartia
  el log del dia.
- Toasts diferenciados en Configuracion: "No hay registros para exportar" (sin logs) y
  "No se pudo compartir el log" (fallo).
- Descripcion del boton actualizada: "Comprime y comparte los registros de depuracion".
- Version actualizada a `2.0.8` (versionCode 18).

## [2.0.7] - 2026-08-04

### Fixed
- **Actualizacion in-app rota**: GitHub ahora devuelve el resumen SHA-256 del APK con el prefijo
  `sha256:`, y la app lo comparaba contra el hash calculado (sin prefijo), por lo que la
  verificacion fallaba siempre y la descarga terminaba con "Error al descargar la actualizacion".
  Ahora la app normaliza el prefijo y la actualizacion desde Ajustes vuelve a funcionar.
  Los dispositivos con versiones 2.0.0-2.0.5 requieren instalar el APK 2.0.7 manualmente una vez
  para recuperar la actualizacion automatica.

### Changed
- Version actualizada a `2.0.7` (versionCode 17).

## [2.0.6] - 2026-08-04

### Fixed
- **Eventos de Calendario desactualizados**: la vista de "proximos eventos" del sitio se renderiza
  por JavaScript y la app recibia un contenedor vacio, por lo que la pantalla mostraba datos en
  cache de dias anteriores. Ahora la app lee la vista mensual del calendario (que incluye los
  eventos directamente en el HTML) y muestra siempre los eventos actuales del curso, con su fecha.
- **Sincronizacion con el curso correcto desde Notificaciones**: la pantalla de Notificaciones ahora
  sincroniza usando el curso configurado por el usuario (igual que la sincronizacion periodica).

### Changed
- Version actualizada a `2.0.6` (versionCode 16).

## [2.0.5] - 2026-08-01

### Added
- **Acciones por pulsacion larga en anuncios**: al mantener presionada una tarjeta de anuncio (en el
  panel de Notificaciones) o el contenido del anuncio en su detalle (incluidos los enlaces del
  cuerpo), se abre un dialogo con "Seleccionar texto" (copia al portapapeles), "Compartir anuncio",
  "Abrir en navegador" y "Cancelar".
- **Eventos de calendario con tarjeta clickeable**: se elimino el boton OpenInBrowser; toda la tarjeta
  del evento abre su enlace al tocarla. La pulsacion larga abre el dialogo de acciones.
- **Notificacion persistente "Evento vence hoy"**: cuando un evento de calendario vence el dia actual,
  la app muestra una notificacion fija (no descartable) con el titulo y la fecha del evento. Se retira
  automaticamente cuando ya no hay eventos que venzan hoy.
- **Instructor en anuncios y eventos**: los anuncios muestran titulo, fecha e instructor en lineas
  separadas, y sin duplicados.

### Fixed
- **Tarjetas invisibles en tema oscuro**: en dark mode las tarjetas usaban el mismo tono que el fondo
  del panel. Ahora tienen un contenedor mas claro y un borde visible que las delimita.
- **Instructor duplicando la fecha en anuncios**: los selectores del foro de Zajuna capturaban la
  celda completa ("NOMBRE DD MMM AAAA"); se ajustaron para separar correctamente fecha e instructor.
- **Error de base de datos al actualizar**: la nueva version anade columnas a las tablas de anuncios y
  eventos; se registra una migracion declarativa (Room 2 → 3) que conserva los datos existentes.

### Changed
- Version actualizada a `2.0.5` (versionCode 15).

## [2.0.4] - 2026-07-31

### Fixed
- **Error HTTP 400 al sincronizar**: el almacen de cookies acumulaba miles de cookies duplicadas, lo
  que inflaba el encabezado `Cookie` de cada peticion y hacia que el cortafuegos del sitio rechazara
  las conexiones. Ahora las cookies se deduplican y se limitan por peticion.
- **Sesion valida marcada como expirada**: se distingue ahora entre un bloqueo temporal del
  cortafuegos del sitio y una sesion realmente caducada, evitando ciclos de re-inicio de sesion.
- **Auto-login repetido al abrir la app**: el inicio de sesion automatico ya no se relanza en cada
  actualizacion de pantalla; ademas, si la sesion guardada sigue activa, entra directo sin repetir el
  navegador web.
- **Contenido de anuncios con restos de la pagina**: el detalle del anuncio se recorta con mayor
  precision para mostrar solo el mensaje real del foro.

### Changed
- Exportacion de registros (logs): ahora se comparte mediante el selector de aplicaciones del sistema
  en lugar de copiarse automaticamente a la carpeta Descargas.
- Version actualizada a `2.0.4` (versionCode 14).

## [2.0.3] - 2026-07-31

### Fixed
- **Login SENA por TLS**: en algunos dispositivos (Moto G22 / Android 12) el almacen seguro del
  sistema no incluye la raiz Sectigo con la que firma el certificado de zajuna.sena.edu.co, y el
  WebView de login fallaba con error de certificado (net_error -202) aunque el navegador si permitia
  entrar. La 2.0.3 incluye la raiz Sectigo Public Server Authentication Root R46 como ancla de
  confianza adicional, solo para el dominio de SENA (sin abrir el resto de conexiones).
- **Dialogo de actualizacion obsoleto**: si quedaba una actualizacion pendiente de una version ya
  retirada, la app ya no la ofrece; la descarta automaticamente.

### Changed
- Version actualizada a `2.0.3` (versionCode 13).

## [2.0.2] - 2026-07-31

### Fixed
- **Cierre al abrir la aplicacion**: la clave de la base de datos dependia de un byte[] que el
  almacen seguro del dispositivo no puede exportar en algunos telefonos (TEE/StrongBox), lo que
  hacia fallar la app al arrancar. Ahora la clave es aleatoria y se guarda cifrada con el MasterKey
  del dispositivo (EncryptedSharedPreferences).

### Changed
- Version actualizada a `2.0.2` (versionCode 12) para permitir actualizar sobre la 2.0.1.

## [2.0.1] - 2026-07-31

### Fixed
- **Crash al abrir la aplicacion**: se desactivo la minificacion R8 en las compilaciones de
  produccion (medida intermedia; la causa raiz se resolvio por completo en la 2.0.2).
- **Migracion de base de datos cifrada**: si no se puede abrir con la clave nueva, la BD se
  descarta y se vuelve a sincronizar desde Zajuna.

### Changed
- Version actualizada a `2.0.1` (versionCode 11).

## [2.0.0] - 2026-07-31

### Added
- **Selector de curso activo** en Configuracion: se sincronizan evidencias, anuncios y calendario del curso elegido (antes estaba fijado un solo curso).
- **Alertas de evidencias proximas a vencer**: notificacion cuando hay actividades pendientes que vencen en 0-3 dias.
- **Sesion persistente**: las cookies se guardan cifradas, evitando volver a iniciar sesion en cada reinicio de la app.
- **Colores dinamicos (Material You)** en Android 12+ y tema oscuro completo.
- **Solicitud de permiso de notificaciones con contexto** y re-intento desde Configuracion.

### Security
- Conexion TLS real en las compilaciones de produccion (el modo que confia en cualquier certificado quedo limitado a debug).
- Errores SSL graves ya no permiten continuar el login (solo errores menores como fecha del certificado).
- Clave de cifrado de la base de datos derivada del almacen seguro del dispositivo (AndroidKeyStore).
- Verificacion SHA-256 del APK descargado antes de instalarlo (proteccion contra suministro corrupto).
- Logout completo: elimina credenciales, cookies y (opcional) datos locales.
- Logs sin numeros de documento (enmascarados) y sin copia automatica a Descargas.
- Contenido de anuncios sanitizado antes de mostrarse; navegacion restringida a sitios de SENA.
- Componentes de cifrado actualizados a la version estable.

### Changed
- La sincronizacion se reprograma con el intervalo configurado por el usuario (1-6 horas).
- Auto-login fallido redirige a la pantalla de inicio de sesion con aviso.
- Si el re-login en segundo plano falla, se notifica al usuario.
- Arranque en segundo plano sin bloqueos (evita cuelgues del sistema).
- Exportacion a Excel mas rapida, sin bloquear la interfaz.
- La verificacion de actualizaciones automatica esta limitada (1 vez cada 6 horas).
- Textos de la interfaz centralizados para soportar idiomas.
- Version actualizada a `2.0.0` (versionCode 10).

## [1.10.0] - 2026-07-28

### Added
- **Actualización automática en segundo plano**: `UpdateWorker` (WorkManager) verifica nuevas versiones en GitHub cada 12 horas y publica una notificación en la bandeja del sistema cuando hay una actualización disponible.
- **Diálogo de actualización global**: Al abrir la app, si hay una actualización pendiente descubierta en segundo plano, el diálogo se muestra automáticamente desde cualquier pantalla.
- **Nuevo canal de notificación**: `CHANNEL_UPDATES` para notificaciones de actualizaciones disponibles.

### Changed
- La verificación manual desde Configuración ahora también persiste el resultado para que el diálogo global lo muestre al reabrir la app.
- `Project894App.onCreate()` programa `UpdateWorker` al iniciar la app.

## [1.9.0] - 2026-07-18

### Added
- **Indicador de estado de sincronizacion** en la pantalla de evidencias: barra visual que muestra fecha/hora de la ultima sincronizacion, cantidad de evidencias y estado de exito/error.
- Campo `LAST_SYNC_TIME` y `LAST_SYNC_SUCCESS` en preferencias de usuario para persistir el estado de sincronizacion entre sesiones.

### Fixed
- **Correccion critica de login**: el sitio Zajuna fue reestructurado durante mantenimiento y la pagina de login se movio de `/zajuna/login/index.php` a la raiz `https://zajuna.sena.edu.co/`. Se reescribio el flujo de login en `WebViewLoginHelper` para detectar y rellenar el formulario de login en cualquier pagina, eliminando el bucle infinito de fallbacks SSL que causaba timeout.
- `LOGIN_URL` actualizado para apuntar a la raiz del sitio (nuevo CMS).
- `isAuthenticatedUrl` ampliado para reconocer cualquier ruta `/zajuna/` post-login.
- Eliminado codigo muerto: `scheduleSslFallback`, `sslErrorHandled`, `fallbackAttempts`.

### Changed
- Version de Android actualizada a `1.9.0` (versionCode 3).
- Delay de 1.5s antes de inyectar credenciales para permitir que el contenido JavaScript se renderice completamente.
- `injectCredentials` siempre intenta `buildLoginJs` primero, con fallback a `buildDirectPostJs` hacia `controllers/login_user/singIn.php`.

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
