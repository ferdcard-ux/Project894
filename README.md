# Project894 Public

Repositorio publico de distribucion de `Project894`.

Este repositorio no incluye el codigo fuente de la aplicacion. Su funcion es centralizar:

- documentacion publica de uso e instalacion
- notas de version
- guia operativa para publicacion de artefactos
- releases binarios validados

## Estado actual

- Release activo: `v1.3.0`
- Fecha de referencia documental: `2026-04-29`
- Artefactos publicados en el release:
  - `Project894-x86_64.AppImage`
  - `Project894.exe`
- Estado Windows del release `v1.3.0`:
  - ejecutable `Project894.exe` reemplazado por la compilacion validada mas reciente de Windows
  - documentacion publica sincronizada con los cambios funcionales visibles de la linea Windows `1.3.0`

## Que incluye la aplicacion

`Project894` es una aplicacion de escritorio para automatizar la consulta y gestion local de evidencias academicas desde Zajuna.

Funciones principales:

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

## Como obtener la aplicacion

Las compilaciones publicas deben descargarse desde la seccion de releases del repositorio.

Artefactos disponibles por plataforma:

- Linux: `Project894-x86_64.AppImage`
- Windows: `Project894.exe`

El release `v1.3.0` conserva ambos artefactos, pero la presente actualizacion sincroniza especificamente la documentacion y el ejecutable de Windows.

## Instalacion rapida

### Linux

1. Descarga `Project894-x86_64.AppImage` desde el release deseado.
2. Otorga permiso de ejecucion.
3. Ejecuta el archivo.

### Windows

1. Descarga `Project894.exe` desde el release deseado.
2. Ejecuta el archivo.
3. Si Windows SmartScreen muestra una advertencia, valida el origen del archivo antes de continuar.

## Documentacion principal

- [README-Win.md](README-Win.md)
- [BUILD_WINDOWS.md](BUILD_WINDOWS.md)
- [CHANGELOG.md](CHANGELOG.md)
- [RELEASE_NOTES.md](RELEASE_NOTES.md)
- [docs/USERGUIDE.md](docs/USERGUIDE.md)
- [docs/FAQ.md](docs/FAQ.md)
- [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)
- [docs/PUBLISHING.md](docs/PUBLISHING.md)

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

La documentacion publica debe describir la experiencia del producto de forma coherente con la version publicada y con especial claridad para los usuarios de Windows, que es la variante actualizada en este ciclo.

## Importante

Al descargar y utilizar `Project894`, aceptas los terminos establecidos en [DISCLAIMER.md](DISCLAIMER.md) y [LICENSE](LICENSE).
