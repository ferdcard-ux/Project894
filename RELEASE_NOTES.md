# Notas de la version

## Version 2.0.13 (Android)

**Fecha:** `2026-10-15`
**Plataforma:** Android (API 26+)

### Resumen
Correccion de la fiabilidad de las etiquetas de estado: la insignia EVALUADA ya no se asigna a
evidencias que Zajuna no tiene calificadas. En el camino se elimino el inventario de evidencias
ficticias y se recupero la insignia de tres evidencias cuyo codigo no se extraccion. Incluye ademas
el detalle in-app de la evidencia (con la seccion completa "Estado de la entrega"), etiquetas
manuales en la pestana "Todas" y la descarga de los archivos adjuntos.

### Artefacto publicado
- `Project894-android-2.0.13.apk`

### Correcciones
- **EVALUADA solo con nota real**: el reporte de notas de Zajuna incluye actividades sin calificar
  cuya celda de nota viene como "-". Se marcaba como evaluada **toda** fila sin comprobar la nota, de
  modo que evidencias nunca calificadas aparecian como evaluadas. Ahora solo se toman las que tienen
  calificacion real (letra A-F, verbal "Excelente" o numerica "10 / 10"): de 199 filas del reporte,
  **108 estan calificadas y 91 se descartan**.
- **Sin evidencias ficticias**: los items del reporte que no corresponden a una evidencia del curso
  ya no se insertan como tarjetas sueltas. El inventario pasa de **211 a 198** evidencias reales y las
  evaluadas de **199 a 99**.
- **El estado real de Zajuna manda**: un dato del reporte ya no se impone sobre el estado que Zajuna
  informa.
- **Tres evidencias recuperadas** (`Infografia. AA1-EV01`, `Cuadro sinoptico. AA4-EV01`,
  `Taller. AA4-EV02`): su codigo corto no se extraia, por lo que no podia fusionarse con el reporte
  de notas y quedaban sin EVALUADA aunque Zajuna las mostrara calificadas. Ahora muestran su codigo y
  son buscables por el.
- **Tabla "Estado de la entrega" conservada** en el detalle: la limpieza del contenido descartaba las
  tablas y la seccion llegaba como un bloque de texto corrido.

### Novedades
- **Detalle in-app de evidencia**: tocar la tarjeta (en cualquier pestaña) abre dentro de la app el
  contenido limpio, incluida la seccion **"Estado de la entrega"** (numero de intento, estado de la
  entrega, estado de la calificacion, tiempo restante, ultima modificacion, archivos enviados y
  comentarios) y, en evidencias calificadas, la tabla de calificacion y retroalimentacion del
  instructor. El bloque informativo superior cambia segun la pestaña desde la que se abrio. El titulo
  sigue abriendo la evidencia en el navegador.
- **Etiquetas manuales** en la pestana "Todas": boton en la esquina inferior derecha que despliega
  `ENVIADA`, `NO ASIGNADA`, `PENDIENTE` y `VENCIDA`. `EVALUADA` nunca es asignable, lo ya asignado
  por el sistema aparece bloqueado con candado y la etiqueta manual se retira sola si Zajuna evalua
  la evidencia.
- **Descarga de archivos adjuntos**: al tocar un archivo de la fila "Archivos enviados" se elige
  donde guardarlo y se descarga con la sesion de Zajuna.

### Mejoras
- **Sin imagenes en el detalle de evidencias**: en Zajuna son imagenes decorativas que no cargan y el
  WebView terminaba mostrando su texto alternativo. Los anuncios y notificaciones del sistema si las
  conservan.
- Las etiquetas manuales se conservan entre sincronizaciones.
- La columna "Estado" del Excel exporta todas las etiquetas (por ejemplo `EVALUADA + VENCIDA`).
- Version actualizada a `2.0.13` (versionCode 23).

### Notas de instalacion
- **Actualizacion OTA compatible**: misma firma que 2.0.10/2.0.11/2.0.12 (SHA-256
  `bdcf8658236171733ef576587db4db2303a64e9d270e66e9b0c6f3ea6e82e25b`). Los dispositivos en 2.0.10 o
  posteriores actualizan normalmente.
- **Desde 2.0.9 o anterior**: requiere reinstalacion manual unica (rotacion de keystore en 2.0.10).

### Validacion en hardware
- Moto G22: inventario de 198 evidencias con **102 evaluadas** (todas con calificacion real) y 7
  pendientes; descarga verificada de un PDF (368 KB) y de un ZIP (254 KB, 4 entradas); tabla de
  entrega, etiquetas manuales y detalle in-app comprobados en las cuatro pestanas.

---

## Version 2.0.12 (Android)

**Fecha:** `2026-10-12`
**Plataforma:** Android (API 26+)

### Resumen
Paquete de mejoras de usabilidad sobre la gestion de evidencias y el panel de notificaciones: contadores por pestana, etiquetas multiples por tarjeta, orden A-Z por defecto, cabeceras apilables, detalle in-app de notificaciones del sistema, notas del instructor solo en Evaluadas y exportacion a Excel con un escritor XLSX propio (sin dependencias).

### Artefacto publicado
- `Project894-android-2.0.12.apk`

### Novedades
- **Contadores por pestana** en Evidencias: cada chip muestra su total ("Todas: 211", "Pendientes: 4", "Evaluadas: 199", "Vencidas: 3"), recalculado con cada cambio de datos.
- **Etiquetas multiples por tarjeta**: se apilan cuando aplican varias (por ejemplo EVALUADA + VENCIDA); el estado real se deriva de fechas/flags aunque Zajuna envie el texto vacio.
- **Detalle in-app de notificaciones del sistema**: se abren dentro de la app con formato limpio (titulo + fecha + mensaje), sin el chrome de la pagina.
- **Notificaciones del sistema via AJAX** (`message_popup_get_popup_notifications`, con fallback al popover HTML).
- **Exportacion XLSX propia** (`XlsxWriter`), sin dependencias.

### Mejoras
- **Orden A-Z por codigo por defecto** (orden natural: GA1, GA2... GA10..., EV01...).
- **Cabeceras del panel de Notificaciones apiladas**: cada una se fija al llegar arriba y las siguientes se apilan debajo sin ocultar a las anteriores; solo se contrae su contenido.
- **Tocar una pestana** recarga su contenido y sube la lista al inicio (sin extraccion fresca).
- **Notas del instructor (Calificacion/Comentario) solo en la pestana Evaluadas**.
- **Limite de notificaciones no leidas** ampliado de 10 a 100.
- **Room v5** (`MIGRATION_4_5`): columna `full_html` para el detalle in-app.
- Version actualizada a `2.0.12` (versionCode 22).

### Correcciones
- **Exportacion a Excel en release**: Apache POI lanzaba `ExceptionInInitializerError`/`NoClassDefFoundError` bajo R8; reemplazado por el escritor propio.
- **Etiqueta duplicada**: retirado el chip rosa "Vencida" que duplicaba la insignia de estado.

### Notas de instalacion
- **Actualizacion OTA compatible**: misma firma que 2.0.10/2.0.11 (SHA-256 `bdcf8658236171733ef576587db4db2303a64e9d270e66e9b0c6f3ea6e82e25b`). Los dispositivos en 2.0.10 o 2.0.11 actualizan normalmente.
- **Desde 2.0.9 o anterior**: requiere reinstalacion manual unica (rotacion de keystore en 2.0.10).

### Validacion en hardware
- Moto G22: contadores en vivo, notas ocultas en Todas, cabeceras apiladas progresivas y re-tocar pestana sin nueva extraccion. Redmi Note 12 reservado para la prueba OTA de 2.0.12.

---

## Version 2.0.11 (Android)

**Fecha:** `2026-08-26`
**Plataforma:** Android (API 26+)

### Resumen
Implementacion del sistema de notificaciones nativas de Zajuna/Moodle: captura, persistencia y visualizacion de mensajes privados, suscripciones a foros, tareas, quizzes, calificaciones y avisos del sistema. Incluye push nativo, panel con mark-as-read y deep link. Ademas, se resolvio un incidente de ANR en Moto G22 causado por el daemon keystore2 del sistema (no de la app).

### Artefacto publicado
- `Project894-android-2.0.11.apk`

### Novedades
- **Notificaciones del sistema Zajuna**: scraping de `message/output/popup/notifications.php` con parseo server-rendered. Clasificacion heuristica `inferType()` (MESSAGE, FORUM_SUBSCRIPTION, ASSIGNMENT, QUIZ, GRADE, SYSTEM, GENERAL) con prioridad MESSAGE y tolerancia a tildes. ID determinista por hash titulo+URL para evitar push duplicados.
- **Push nativo**: canal `channel_zajuna_notifications` (IMPORTANCE_HIGH). Tap en push abre el panel de notificaciones con deep link (`EXTRA_OPEN_NOTIFICATIONS_PANEL`).
- **Panel de notificaciones**: nueva seccion "Notificaciones del sistema" con contador de no leidas, tarjeta clickeable (abre URL + mark-as-read), long-press con dialogo de acciones (Seleccionar texto / Compartir / Abrir en navegador).
- **Toggle en Configuracion**: "Notificaciones del sistema Zajuna" para habilitar/deshabilitar individualmente.
- **Room v4**: entidad `zajuna_notifications` + `app_metadata` (timestamp limpieza >30 dias), migracion `MIGRATION_3_4` con 3 indices. Upsert preservando estado local `read`.
- **Tests**: 8 casos unitarios en `ZajunaNotificationTypeTest` (clasificacion, valueOf defensivo, tildes, prioridad MESSAGE).

### Correcciones
- **ANR en Moto G22 (keystore2 del sistema)**: el daemon `keystore2` del dispositivo estaba en bucle `KEY_REQUIRES_UPGRADE` (63% CPU, 65 ANRs/noche, bitwarden incluido). La app se colgaba en `EncryptedSharedPreferences.create()` en hilo principal durante inyeccion Hilt. **No es bug de la app** — la app era victima visible. Resuelto con reboot (reinicia keystore2). Mejora futura: mover creacion passphrase/DB a `Dispatchers.IO`.
- **Keystore de firma recuperado**: `release.jks` no existia en el equipo de build; recuperado desde equipo anterior (SHA-256 verificado `ae123c42...356a39` contra LEEME). `.gitignore` corregido a `*.jks`.
- **Extraccion automatica no autorizada en instalacion limpia**: SyncWorker ejecutaba la sincronizacion de evidencias sin esperar la autorizacion del usuario. Corregido con flag `first_evidences_extraction_authorized` en DataStore; SyncWorker omite la extraccion si no hay autorizacion y la BD esta vacia; dialogo de autorizacion en UI con botones "Extraer ahora" / "Ahora no"; SyncWorker omite evidencias sin autorizacion cuando la BD esta vacia.

### Notas de instalacion
- **Actualizacion OTA compatible**: misma firma que 2.0.10 (SHA-256 `bdcf8658236171733ef576587db4db2303a64e9d270e66e9b0c6f3ea6e82e25b`). Dispositivos en 2.0.10 actualizan normalmente.
- **Desde 2.0.9 o anterior**: requiere reinstalacion manual unica (rotacion de keystore en 2.0.10).

### Pendiente E2E real
Validacion del ciclo completo (panel -> push -> deep link -> mark-as-read) requiere notificacion genuina en la cuenta Zajuna (mensaje privado o mencion en foro); la cuenta de prueba tiene 0.

---

## Version 2.0.10 (Android)

**Fecha:** `2026-08-20`
**Plataforma:** Android (API 26+)

### Resumen
Release de hardening (Fase 1) + correccion de terminos legales. Implementa ofuscacion, R8/shrinkResources, verificacion de firma en runtime, anti-tampering y keystore propio. Corrige el pop-up de Terminos para reflejar que el proyecto es desarrollo privado (no open source).

### Artefacto publicado
- `Project894-android-2.0.10.apk`

### Seguridad (Hardening Fase 1)
- **R8 + shrinkResources** habilitado en release con reglas `-keep` para Hilt/WorkManager/Compose/FileProvider.
- **Verificacion de firma en runtime**: la app calcula SHA-256 de su certificado de firma y lo compara contra hash embebido ofuscado. Si no coincide (APK re-firmado/reempaquetado), muestra dialogo de bloqueo y cierra.
- **Ofuscacion XOR** (clave `0x5A`) de strings criticos: URLs de login/SENA/GitHub, host/dominio, hash de firma esperado.
- **Keystore de release propio**: `~/.config/project894/release.jks` (alias `project894`). Nuevo fingerprint SHA-256: `bdcf8658236171733ef576587db4db2303a64e9d270e66e9b0c6f3ea6e82e25b`.
- **APK minificado**: 21 MB (vs ~43 MB sin minificar). Endpoints `/zajuna/*` (estructura, sin host) siguen visibles en DEX: limitacion aceptada en Fase 1.

### Cambios legales
- **Terminos y Condiciones (secciones 6 y 7)**: "Project894 es un desarrollo privado y NO es codigo abierto. Solo el repositorio de distribucion y su contenido son publicos; cualquier usuario puede solicitar copia del codigo fuente, sugerir mejoras o reportar/corregir fallos, sujeto a aprobacion del desarrollador, que se reserva los derechos de aprobacion o admision". Enlace a "Repositorio de distribucion: github.com/ferdcard-ux/Project894" y "Guia de contribuciones y contacto: CONTRIBUTING.md".
- **DISCLAIMER.md**: nuevas secciones "Propiedad Intelectual" y "Enlaces a Repositorios y Contribuciones" alineadas.

### Importante: Rotacion de keystore
La 2.0.10 usa un **nuevo keystore de release** (distinto al de 2.0.0-2.0.9). La actualizacion OTA 2.0.9 -> 2.0.10 es **incompatible** (Android rechaza la actualizacion por firma distinta). Los dispositivos con 2.0.9 o anterior requieren **reinstalacion manual unica** del APK 2.0.10. Esto es por decision de diseño (base de usuarios minima, ver `docs/PLAN_HARDENING.md` §5.3).

### Validacion en hardware
- **Moto G22 + Redmi Note 12**: auto-login online exitoso (sesion AUTHENTICATED), 385 evidencias cargadas, sin FATAL/ANR. Diagnostico de cuelgue de sistema (ANR SystemUI) descartado Project894; culpable: fork KDE Connect (heartbeat/reconexion con timeout falso bajo Doze/optimizacion bateria MIUI).

---

## Version 2.0.9 (Android)

**Fecha:** `2026-08-15`
**Plataforma:** Android (API 26+)

### Resumen
Correccion del boton "Instalar ahora" de la actualizacion in-app, que en Android 14+ abria el
dialogo generico "Abrir con" en lugar del instalador y no instalaba el APK. Ademas, se corrige el
pop-up de Terminos y Condiciones para que los botones no queden ocultos bajo la barra de
navegacion, y "Exportar logs" ahora pide confirmacion con una advertencia de privacidad.

### Artefacto publicado
- `Project894-android-2.0.9.apk`

### Correcciones
- **Instalacion de la actualizacion in-app no instalaba**: `Intent.ACTION_VIEW` con
  `application/vnd.android.package-archive` ya no resuelve al instalador de paquetes con targetSdk
  34+ (resolvia a `com.android.intentresolver/ResolverActivity`, el dialogo "Abrir con"). Se cambio
  a `ACTION_INSTALL_PACKAGE` (resuelve directo al instalador), se declaro el permiso
  `REQUEST_INSTALL_PACKAGES` y, si no esta concedido, la app guia al usuario a "Instalar apps
  desconocidas" y reintenta la instalacion al volver.
- **Terminos y Condiciones bajo la barra de navegacion**: con edge-to-edge los botones inferiores
  quedaban ocultos en dispositivos con botones de navegacion. Se aplica `WindowInsets.safeDrawing`.

### Cambios
- "Exportar logs" abre un dialogo de confirmacion (Aceptar/Cancelar) que advierte que los registros
  pueden contener informacion del dispositivo, del curso y trazas de actividad, y que el
  desarrollador solo los usara para depuracion con la autorizacion del usuario.
- Terminos y Condiciones: nueva seccion 9 "Registros de Depuracion". `DISCLAIMER.md`: nueva seccion
  4 "Registros de Depuracion (logs)".
- El repositorio publico ahora contiene solo documentacion tecnica, legal y de seguridad (se retiro
  el plan de documentacion interno).

### Notas de la version anterior (2.0.8)

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
