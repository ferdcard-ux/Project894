# Project894 Public

Repositorio publico de distribucion de `Project894`.

Este repositorio no incluye el codigo fuente de la aplicacion. Su funcion es centralizar:

- documentacion publica de uso e instalacion
- notas de version
- guia operativa para publicacion de artefactos
- releases binarios validados

## Estado actual

- Release activo: **`v2.0.14`** (Android)
- Fecha de referencia documental: `2026-11-14`
- Artefactos publicados por plataforma:
  - **Android:** `Project894-android-2.0.14.apk`
  - **Linux / Windows:** en desarrollo (las versiones anteriores fueron retiradas; ver [NOTA_ARTEFACTOS.md](NOTA_ARTEFACTOS.md))

## Que incluye la aplicacion

`Project894` esta disponible en tres plataformas:

### Escritorio (Linux / Windows)
Aplicacion de escritorio en PySide6 para automatizar la consulta y gestion local de evidencias academicas desde Zajuna.
- autenticacion con credenciales institucionales
- extraccion de `Todas Las Evidencias`
- consulta de `Evidencias Evaluadas`
- vista hibrida `Card-List`
- filtros por vista y por contexto
- edicion local de instructor, estado y fechas
- exportacion a Excel
- persistencia local cifrada
- mensajes operativos unificados
- control de cambios pendientes antes de cerrar o salir

### Android
Aplicacion nativa Android con Jetpack Compose para consultar evidencias, calificaciones, anuncios y eventos de calendario desde Zajuna SENA, y los juicios evaluativos de Sofia Plus.
- **pestana SofiaPlus** (desde 2.0.14): juicios evaluativos por competencia y resultado de aprendizaje, con filtros y busqueda; usa las mismas credenciales de Zajuna, se actualiza una vez al dia y queda disponible sin conexion (Sofia Plus solo ofrece HTTP: la app lo advierte y pide autorizacion antes de la primera extraccion)
- **pestana Por evaluar** (desde 2.0.14): evidencias entregadas que aun esperan calificacion
- **avisos sin repeticiones** (desde 2.0.14): cada evento se notifica una sola vez y el progreso de sincronizacion usa una unica notificacion
- interfaz moderna con Material Design 3 (incluye tema oscuro con bordes de tarjeta visibles)
- login automatizado mediante WebView, con sesion persistente (fast-path sin re-login cuando la sesion sigue activa)
- scraping integrado con OkHttp + Jsoup (selectores adaptados al CMS de Zajuna)
- persistencia local con Room + SQLCipher
- panel de notificaciones con eventos de calendario (tarjeta clickeable), anuncios con instructor y notificaciones del sistema Zajuna (cabeceras apilables, detalle in-app)
- acciones por pulsacion larga: seleccionar texto, compartir y abrir en navegador
- notificacion persistente "Evento vence hoy" para vencimientos del dia
- sincronizacion en segundo plano con WorkManager
- busqueda, filtros por estado con contador por pestana (Todas, Pendientes, Evaluadas, Por evaluar, Vencidas) y ordenamiento A-Z por codigo por defecto
- etiquetas multiples por tarjeta (por ejemplo EVALUADA + VENCIDA), apiladas solo cuando ambas aplican
- **detalle in-app de evidencia**: al tocar la tarjeta se abre el contenido limpio de la evidencia, incluida la seccion "Estado de la entrega" (intento, estado de la entrega, estado de la calificacion, ultima modificacion, archivos y comentarios), con un bloque informativo que varia segun la pestana de origen
- **descarga de archivos adjuntos** desde la fila "Archivos enviados", eligiendo donde guardarlos sin salir de la app
- **etiquetas manuales** en la pestana "Todas" (ENVIADA, NO ASIGNADA, PENDIENTE, VENCIDA) con bloqueo de las que ya asigna el sistema y retirada automatica si Zajuna evalua la evidencia
- exportacion a Excel de evidencias (por estado, incluida "Por evaluar") y de los juicios de Sofia Plus (escritor XLSX propio, sin dependencias)
- notificaciones push con 5 canales nativos (sincronizacion, alertas, calendario, anuncios y notificaciones del sistema Zajuna)
- cache-first para carga instantanea
- indicador de estado de sincronizacion en la pantalla de evidencias
- actualizacion in-app: deteccion automatica en segundo plano cada 12h + verificacion manual, descarga e instalacion desde la misma app

## Como obtener la aplicacion

Las compilaciones publicas deben descargarse desde la seccion de releases del repositorio.

Artefactos disponibles por plataforma:

- **Linux:** `Project894-x86_64.AppImage`
- **Windows:** `Project894.exe`
- **Android:** `Project894-android-<version>.apk`

## Instalacion rapida

### Linux

1. Descarga `Project894-x86_64.AppImage` desde el release deseado.
2. Otorga permiso de ejecucion.
3. Ejecuta el archivo.

### Windows

1. Descarga `Project894.exe` desde el release deseado.
2. Ejecuta el archivo.
3. Si Windows SmartScreen muestra una advertencia, valida el origen del archivo antes de continuar.

### Android

1. Descarga `Project894-android-<version>.apk` desde el release deseado.
2. En tu dispositivo Android, habilita `Instalar apps desconocidas` si es necesario.
3. Abre el archivo APK e instala.
4. Al abrir la app por primera vez, lee y acepta los terminos y condiciones para continuar.

#### Verificar que el APK es autentico

Todos los APK oficiales desde la `2.0.10` estan firmados con el mismo certificado:

```
SHA-256: bdcf8658236171733ef576587db4db2303a64e9d270e66e9b0c6f3ea6e82e25b
```

Con el Android SDK puedes comprobarlo antes de instalar:

```bash
apksigner verify --print-certs Project894-android-<version>.apk
```

Si la huella no coincide, no instales el archivo. Un APK con otra firma tampoco podria actualizar una instalacion existente.


## Documentacion principal

- [README-Win.md](README-Win.md) — Documentacion para Windows
- [BUILD_WINDOWS.md](BUILD_WINDOWS.md) — Guia de compilacion Windows
- [NOTA_ARTEFACTOS.md](NOTA_ARTEFACTOS.md) — Nota sobre la limpieza de artefactos y estado de las versiones Linux/Windows
- [CHANGELOG.md](CHANGELOG.md) — Historial de versiones (todas las plataformas)
- [RELEASE_NOTES.md](RELEASE_NOTES.md) — Notas de version
- [docs/USERGUIDE.md](docs/USERGUIDE.md) — Guia de usuario escritorio (Linux/Windows)
- [docs/USERGUIDE-Android.md](docs/USERGUIDE-Android.md) — Guia de usuario Android
- [docs/FAQ.md](docs/FAQ.md) — Preguntas frecuentes
- [docs/FAQ-Android.md](docs/FAQ-Android.md) — Preguntas frecuentes Android
- [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) — Arquitectura del repositorio publico
- [docs/PUBLISHING.md](docs/PUBLISHING.md) — Guia de publicacion de artefactos

## Estructura del repositorio

Este repositorio publico mantiene documentacion y material de publicacion:

```text
.
|-- BUILD_WINDOWS.md
|-- CHANGELOG.md
|-- CONTRIBUTING.md
|-- DISCLAIMER.md
|-- LICENSE
|-- NOTA_ARTEFACTOS.md
|-- README.md
|-- README-Win.md
|-- RELEASE_NOTES.md
|-- SECURITY.md
`-- docs/
    |-- ARCHITECTURE.md
    |-- FAQ.md
    |-- FAQ-Android.md
    |-- PUBLISHING.md
    |-- USERGUIDE.md
    `-- USERGUIDE-Android.md
```

## Alcance del repositorio publico

Este repositorio esta pensado para distribucion y comunicacion publica del producto terminado. El desarrollo interno, el empaquetado tecnico y la base de codigo se mantienen en repositorios locales o privados separados.

La documentacion publica debe describir la experiencia del producto de forma coherente con la version publicada. Las tres plataformas (Linux, Windows y Android) comparten este mismo repositorio para distribucion de artefactos.

## Importante

Al descargar y utilizar `Project894`, aceptas los terminos establecidos en [DISCLAIMER.md](DISCLAIMER.md) y [LICENSE](LICENSE).
