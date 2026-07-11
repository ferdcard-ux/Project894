# Project894 Public

Repositorio publico de distribucion de `Project894`.

Este repositorio no incluye el codigo fuente de la aplicacion. Su funcion es centralizar:

- documentacion publica de uso e instalacion
- notas de version
- guia operativa para publicacion de artefactos
- releases binarios validados

## Estado actual

- Release activo: `v1.3.0` (escritorio) / `v1.8.0` (Android)
- Fecha de referencia documental: `2026-07-10`
- Artefactos publicados por plataforma:
  - **Linux:** `Project894-x86_64.AppImage`
  - **Windows:** `Project894.exe`
  - **Android:** `Project894-android-1.8.0.apk`

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
Aplicacion nativa Android con Jetpack Compose para consultar evidencias, calificaciones, anuncios y eventos de calendario desde Zajuna SENA.
- interfaz moderna con Material Design 3
- login automatizado mediante WebView
- scraping integrado con OkHttp + Jsoup
- persistencia local con Room + SQLCipher
- panel de notificaciones con eventos de calendario y anuncios
- sincronizacion en segundo plano con WorkManager
- busqueda, filtros por estado y ordenamiento dinamico
- exportacion de evidencias a Excel
- notificaciones push con 4 canales nativos
- cache-first para carga instantanea
- actualizacion in-app: detecta nuevas versiones, descarga e instala desde la misma app

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

## Documentacion principal

- [README-Win.md](README-Win.md) — Documentacion para Windows
- [BUILD_WINDOWS.md](BUILD_WINDOWS.md) — Guia de compilacion Windows
- [CHANGELOG.md](CHANGELOG.md) — Historial de versiones (todas las plataformas)
- [RELEASE_NOTES.md](RELEASE_NOTES.md) — Notas de version
- [docs/USERGUIDE.md](docs/USERGUIDE.md) — Guia de usuario (escritorio)
- [docs/FAQ.md](docs/FAQ.md) — Preguntas frecuentes
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
|-- README.md
|-- README-Win.md
|-- RELEASE_NOTES.md
|-- SECURITY.md
`-- docs/
```

## Alcance del repositorio publico

Este repositorio esta pensado para distribucion y comunicacion publica del producto terminado. El desarrollo interno, el empaquetado tecnico y la base de codigo se mantienen en repositorios locales o privados separados.

La documentacion publica debe describir la experiencia del producto de forma coherente con la version publicada. Las tres plataformas (Linux, Windows y Android) comparten este mismo repositorio para distribucion de artefactos.

## Importante

Al descargar y utilizar `Project894`, aceptas los terminos establecidos en [DISCLAIMER.md](DISCLAIMER.md) y [LICENSE](LICENSE).
