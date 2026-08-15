# Notas de la version

## Version 2.0.8 (Android)

**Fecha:** `2026-08-15`
**Plataforma:** Android (API 26+)

### Resumen
Correccion de la opcion "Exportar logs" de Configuracion, que no abria el share sheet y mostraba
"Failed to find configured root". Ademas, la exportacion ahora comprime todos los registros de
depuracion (ultimos 3 dias) en un unico `.zip`.

### Artefacto publicado
- `Project894-android-2.0.8.apk`

### Correcciones
- **Exportar logs no abria el share sheet**: la configuracion del FileProvider usaba `root-path`,
  que en la libreria androidx apunta a la raiz del filesystem (`/`) y no al almacenamiento externo,
  por lo que la URI nunca coincidia con la ruta real de los logs. Se cambio a `external-path`
  (raiz = `/storage/emulated/0`) y el compartir vuelve a funcionar.

### Cambios
- La exportacion comprime los ultimos `app_log_*.txt` de `.logs` (hasta 3, ~3 dias) en
  `Project894_logs_<fecha>.zip` dentro de la cache privada de la app y lo comparte con el share
  sheet del sistema.
- Toasts diferenciados: "No hay registros para exportar" (sin logs) y "No se pudo compartir el
  log" (fallo).
- Descripcion del boton: "Comprime y comparte los registros de depuracion".

### Notas de la version anterior (2.0.7)

## Version 2.0.7 (Android)

**Fecha:** `2026-08-04`
**Plataforma:** Android (API 26+)

### Resumen
Correccion del sistema de actualizacion in-app. GitHub comenzó a devolver el resumen SHA-256 de
los APK con el prefijo `sha256:`, y la app lo comparaba contra el hash calculado (sin prefijo), por
lo que la verificacion fallaba siempre y la descarga terminaba con "Error al descargar la
actualizacion".

### Artefacto publicado
- `Project894-android-2.0.7.apk`

### Correcciones
- **Actualizacion in-app rota**: la verificacion de integridad del APK fallaba por el prefijo
  `sha256:` en el resumen proporcionado por GitHub. Ahora la app normaliza el prefijo y la
  actualizacion desde Ajustes vuelve a funcionar.

### Nota de instalacion
- Los dispositivos con versiones **2.0.0 a 2.0.5** no pueden actualizarse automaticamente (el bug
  esta en la app instalada). Deben instalar este APK manualmente una vez; a partir de ahi la
  actualizacion automatica vuelve a funcionar.
- Los dispositivos con versiones 1.8.0 a 1.10.0 (sin verificacion de integridad) pueden actualizarse
  automaticamente como siempre.

### Notas de la version anterior (2.0.6)

## Version 2.0.6 (Android)

**Fecha:** `2026-08-04`
**Plataforma:** Android (API 26+)

### Resumen
Correccion de sincronizacion: la seccion "Eventos de Calendario" del panel de Notificaciones
mostraba datos en cache de hace varios dias porque la vista de proximos eventos del sitio se
renderiza por JavaScript y llegaba vacia a la app. La 2.0.6 lee la vista mensual del calendario
(incluye los eventos en el HTML) y muestra siempre los eventos actuales del curso.

### Artefacto publicado
- `Project894-android-2.0.6.apk`

### Correcciones
- **Eventos de Calendario desactualizados**: la vista `upcoming` del calendario del sitio se carga
  por JavaScript, por lo que la app recibia un contenedor vacio ("No hay eventos proximos") y
  conservaba los datos en cache de dias anteriores. Ahora se consulta la vista mensual, que incrusta
  los eventos directamente en el HTML, y cada evento muestra su fecha (ej. "15 de agosto de 2026").
- **Sincronizacion desde Notificaciones con el curso correcto**: la pantalla de Notificaciones usa
  ahora el curso configurado por el usuario, igual que la sincronizacion periodica.

### Notas de la version anterior (2.0.5)

## Version 2.0.5 (Android)

**Fecha:** `2026-08-01`
**Plataforma:** Android (API 26+)

### Resumen
Mejoras de experiencia de usuario y correcciones tras validar la 2.0.4 en hardware (Redmi Note 12 y
Moto G22): acciones por pulsacion larga en anuncios, tarjeta de calendario clickeable completa,
notificacion persistente para eventos que vencen hoy, instructor visible en anuncios y eventos, y
tarjetas con borde visible en tema oscuro.

### Artefacto publicado
- `Project894-android-2.0.5.apk`

### Novedades
- **Pulsacion larga en anuncios**: en el panel de Notificaciones y en el detalle del anuncio, mantener
  presionado abre un dialogo con "Seleccionar texto" (copiar al portapapeles), "Compartir anuncio",
  "Abrir en navegador" y "Cancelar".
- **Tarjeta de calendario clickeable**: se quito el boton OpenInBrowser; toda la tarjeta del evento
  abre el enlace. La pulsacion larga abre el mismo dialogo de acciones.
- **Notificacion "Evento vence hoy"**: notificacion fija y visible cuando un evento vence el dia
  actual, retirada automaticamente cuando deja de aplicarse.
- **Instructor en anuncios**: los anuncios muestran titulo, fecha e instructor separados y sin
  duplicados.
- **Tema oscuro mejorado**: las tarjetas tienen un contenedor propio y un borde visible en dark mode.

### Correcciones
- **Migracion de base de datos**: la nueva version incorpora una migracion declarativa de Room (2 → 3)
  que anade columnas de instructor y vencimiento a anuncios y eventos sin perder los datos guardados.
- **Instructor duplicado con la fecha** en la lista de anuncios (selectores del foro ajustados).

### Notas de la version anterior (2.0.4)

## Version 2.0.4 (Android)

**Fecha:** `2026-07-31`
**Plataforma:** Android (API 26+)

### Resumen
Hotfix de sincronizacion: el sitio de SENA empezo a rechazar las peticiones de la app con HTTP 400
debido a la acumulacion de miles de cookies duplicadas en el almacen local. Ademas se corrigen ciclos
de re-inicio de sesion y la exportacion de registros ahora usa el selector del sistema.

> Nota: la 2.0.4 se distribuyo como actualizacion directa (hotfix) y sus cambios quedan incluidos en
> la 2.0.5, que es el release publicado oficialmente para esta linea.

### Correcciones
- **HTTP 400 al sincronizar**: las cookies se deduplican y se limitan por peticion, evitando el
  rechazo del cortafuegos del sitio.
- **Sesion valida marcada como expirada**: se distingue el bloqueo temporal del cortafuegos de una
  sesion caducada real (AuthStatus de tres estados).
- **Auto-login repetido**: el auto-login corre una sola vez y aprovecha la sesion persistente
  (fast-path) cuando sigue activa.
- **Contenido de anuncios**: el detalle se recorta con `.post-content-container` para mostrar solo el
  mensaje real.
- **Logs**: exportacion mediante el selector de aplicaciones del sistema (share sheet), ya no se copia
  a Descargas automaticamente.

### Notas de la version anterior (2.0.3)

## Version 2.0.3 (Android)

**Fecha:** `2026-07-31`
**Plataforma:** Android (API 26+)

### Resumen
Correcciones de compatibilidad y robustez tras validar la 2.0.2 en hardware real (Moto G22).
El login a SENA podia fallar con error de certificado en telefonos cuyo sistema no incluye la raiz
Sectigo con la que firma zajuna.sena.edu.co; la 2.0.3 empaqueta esa raiz como ancla de confianza
adicional (solo para el dominio de SENA). Ademas, la app ya no ofrece actualizaciones de versiones
que fueron retiradas de la publicacion.

### Artefacto publicado
- `Project894-android-2.0.3.apk`

### Correcciones
- **Login SENA por TLS**: se incluye la raiz `Sectigo Public Server Authentication Root R46` como
  ancla de confianza del WebView y de las conexiones HTTPS de la app, unicamente para
  `zajuna.sena.edu.co`. Corrige el error `net_error -202` (autoridad de certificado no valida) en
  dispositivos sin raices Sectigo en el sistema, sin ampliar la confianza del resto de conexiones.
- **Dialogo de actualizacion obsoleto**: una actualizacion pendiente persistida de una version ya
  eliminada ya no se ofrece; se descarta al arrancar si la version pendiente no supera a la
  instalada.

### Notas de la version anterior (2.0.2)

## Version 2.0.2 (Android)

**Fecha:** `2026-07-31`
**Plataforma:** Android (API 26+)

### Resumen
Correccion definitiva del cierre al abrir la aplicacion. Las versiones 2.0.0 y 2.0.1 derivaban
la clave de cifrado de la base de datos desde el almacen seguro del dispositivo; en telefonos
cuyo hardware no permite exportar la clave (TEE/StrongBox), eso devolvia `null` y la aplicacion
fallaba al arrancar (Redmi Note 12, Moto G22). La 2.0.2 genera una clave aleatoria propia y la
protege con el almacen seguro, lo que funciona en todos los dispositivos.

### Artefacto publicado
- `Project894-android-2.0.2.apk`

### Correcciones
- **Clave de la base de datos**: se elimina la dependencia del byte[] exportable del almacen
  seguro. La clave es aleatoria y se guarda cifrada con el MasterKey del dispositivo
  (`EncryptedSharedPreferences`), el mismo mecanismo ya usado para las cookies de sesion.
- **Actualizable desde 2.0.1**: la version sube a `versionCode 12` para que el instalador permita
  reemplazar la instalacion rota.

### Notas de la version anterior (2.0.1)

## Version 2.0.1 (Android)

**Fecha:** `2026-07-31`
**Plataforma:** Android (API 26+)

### Resumen
Hotfix intermedio para el cierre al abrir la aplicacion. Se desactivo la minificacion (R8) y se
agrego proteccion ante fallos de apertura de la base de datos, pero la causa raiz (clave del
almacen seguro no exportable) persistia; se corrige por completo en la 2.0.2. Esta release ya no
esta disponible para descarga.

### Correcciones
- **Crash al abrir la aplicacion**: se desactiva la minificacion R8 en las compilaciones de
  produccion.
- **Migracion de la base de datos cifrada**: si la apertura falla, la BD se descarta y se vuelve
  a sincronizar desde Zajuna automaticamente.
- **Actualizable desde 2.0.0**: version `versionCode 11`.

### Notas de la version anterior (2.0.0)

## Version 2.0.0 (Android)

**Fecha:** `2026-07-31`
**Plataforma:** Android (API 26+)

### Resumen
Version mayor con una auditoria completa de seguridad (11 riesgos corregidos) y mejoras de funcionalidad, rendimiento, experiencia de usuario y calidad. Se introduce el selector de curso activo, alertas de evidencias proximas a vencer y sesion persistente.

### Artefacto publicado
- `Project894-android-2.0.0.apk`

### Seguridad
- **TLS real**: la app ya no acepta cualquier certificado; en produccion valida contra los certificados del sistema.
- **SSL estricto en el login**: errores SSL graves cancelan el acceso (solo se toleran errores menores).
- **Base de datos cifrada con clave del dispositivo**: la passphrase se deriva de AndroidKeyStore, no esta incrustada en el APK.
- **APK verificado por SHA-256** antes de instalar actualizaciones.
- **Logout completo** (credenciales + cookies + datos locales opcional) y **logs sin PII** (documentos enmascarados).
- **Anuncios sanitizados** y navegacion restringida a sitios SENA.
- Componentes de cifrado actualizados a version estable.

### Funcionalidad
- **Selector de curso activo** en Configuracion (evidencias, anuncios y calendario del curso elegido).
- **Alertas de evidencias a vencer** en 0-3 dias.
- **Sesion persistente**: cookies cifradas, sin re-login en cada reinicio.
- **Colores dinamicos (Material You)** y tema oscuro completo.
- Solicitud de permiso de notificaciones con contexto.

### Rendimiento y calidad
- Sincronizacion en segundo plano sin bloqueos (goAsync) y con tope de reintentos.
- Exportacion Excel en segundo plano y mas rapida.
- Intervalo de sincronizacion configurable respetado.
- Suite de tests unitarios y limpieza de codigo muerto.
- Firma consistente con las versiones anteriores.

### Notas de la version anterior (1.10.0)

## Version 1.10.0 (Android)

**Fecha:** `2026-07-28`
**Plataforma:** Android (API 26+)

### Resumen
Sistema de actualizacion automatica en segundo plano. La app ahora verifica nuevas versiones cada 12 horas sin necesidad de abrir la pantalla de configuracion, y notifica al usuario mediante la bandeja del sistema.

### Artefacto publicado
- `Project894-android-1.10.0.apk`

### Cambios en esta version
- **Actualizacion automatica**: `UpdateWorker` (WorkManager) se ejecuta cada 12 horas, consulta GitHub y persiste el resultado.
- **Notificacion nativa**: Cuando hay una nueva version, aparece una notificacion en la bandeja del sistema.
- **Dialogo global**: Al abrir la app, si hay una actualizacion pendiente, el dialogo se muestra automaticamente desde cualquier pantalla.
- **Persistencia**: El resultado de la ultima verificacion se almacena en preferencias de usuario para mostrarlo al reabrir la app.

### Notas de la version anterior (1.9.0)

## Version 1.9.0 (Android)

**Fecha:** `2026-07-18`
**Plataforma:** Android (API 26+)

### Resumen
Correccion critica del login para adaptarse a la reestructuracion del sitio Zajuna, que migro de Moodle a un CMS personalizado. Se agrega indicador visual de estado de sincronizacion en la pantalla de evidencias.

### Artefacto publicado
- `Project894-android-1.9.0.apk`

### Cambios en esta version
- **Login corregido**: el sitio Zajuna cambio la ubicacion de la pagina de login durante mantenimiento. La app ahora detecta y utiliza el nuevo formulario de login en la raiz del sitio.
- **Indicador de sincronizacion**: nueva barra visual en la pantalla de evidencias que muestra cuando fue la ultima sincronizacion y si fue exitosa.
- **Rendimiento**: delay optimizado de 1.5s antes de inyectar credenciales para asegurar que el DOM este completamente renderizado.
- **Limpieza de codigo**: eliminados mecanismos de fallback SSL que ya no son necesarios.

### Notas de la version anterior (1.8.0)

**Fecha:** `2026-07-10`

#### Novedades de Android
- Interfaz nativa Android con Jetpack Compose y Material Design 3
- Login automatizado mediante WebView con inyeccion de credenciales
- Scraping integrado con OkHttp + Jsoup (sin Playwright)
- Persistencia local con Room + SQLCipher para almacenamiento cifrado
- Panel de notificaciones con eventos de calendario y anuncios del foro
- Sincronizacion en segundo plano con WorkManager
- Notificaciones push con 4 canales nativos (Sync, Alertas, Calendario, Anuncios)
- Terminos y condiciones: pop-up obligatorio en primera ejecucion
- Auto-limpieza de logs: conserva solo los 3 archivos mas recientes
- Actualizacion in-app: detecta nuevas versiones en GitHub, descarga e instala desde la misma app

### Requisitos del sistema
- Android 8.0 (API 26) o superior.
- Conexion a internet para extraer datos de Zajuna.

---

## Version 1.3.0 (Escritorio)

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
