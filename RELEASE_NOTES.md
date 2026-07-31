# Notas de la version

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
