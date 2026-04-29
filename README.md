# Project894 Public

Repositorio público de distribución de `Project894`.

Este repositorio no incluye código fuente de la aplicación. Su propósito es centralizar:

- documentación pública de uso e instalación
- notas de versión
- instrucciones de publicación de artefactos
- releases binarios para Linux y Windows

## Estado actual

- Versión pública actual: `1.3.0`
- Plataformas distribuidas: `Linux x86_64` y `Windows x64`
- Artefactos esperados por release:
  - `Project894-x86_64.AppImage`
  - `Project894.exe`
- Estado de validación de la versión 1.2.0:
  - Linux: release pública compartida
  - Windows: ejecutable nativo validado antes de publicación

## Qué incluye la aplicación

`Project894` es una aplicación de escritorio para automatizar la consulta y gestión local de evidencias académicas desde Zajuna.

Funciones principales:

- autenticación con credenciales institucionales
- extracción de `Todas Las Evidencias`
- consulta de `Evidencias Evaluadas`
- vista híbrida `Card-List`
- filtros por vista y por contexto
- edición local de instructor, estado y fechas
- exportación a Excel
- persistencia local cifrada
- mensajes operativos unificados
- control de cambios pendientes antes de cerrar o salir

## Cómo obtener la aplicación

Las compilaciones públicas deben descargarse desde la sección de releases del repositorio.

Versiones publicadas por plataforma:

- Linux: `Project894-x86_64.AppImage`
- Windows: `Project894.exe`

Ambos artefactos deben corresponder a la misma versión funcional publicada en el release.

## Instalación rápida

### Linux

1. Descarga `Project894-x86_64.AppImage` desde el release deseado.
2. Otorga permiso de ejecución:

```bash
chmod +x Project894-x86_64.AppImage
```

3. Ejecuta la aplicación:

```bash
./Project894-x86_64.AppImage
```

### Windows

1. Descarga `Project894.exe` desde el release deseado.
2. Ejecuta el archivo.
3. Si Windows SmartScreen muestra una advertencia, valida el origen del archivo antes de continuar.

## Estructura del repositorio

Este repositorio público mantiene únicamente documentación y material de publicación:

```text
.
├── CHANGELOG.md
├── CONTRIBUTING.md
├── DISCLAIMER.md
├── LICENSE
├── README.md
├── RELEASE_NOTES.md
├── SECURITY.md
└── docs/
```

## Documentación disponible

- [CHANGELOG.md](CHANGELOG.md)
- [RELEASE_NOTES.md](RELEASE_NOTES.md)
- [CONTRIBUTING.md](CONTRIBUTING.md)
- [SECURITY.md](SECURITY.md)
- [docs/USERGUIDE.md](docs/USERGUIDE.md)
- [docs/FAQ.md](docs/FAQ.md)
- [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)
- [docs/PUBLISHING.md](docs/PUBLISHING.md)

## Alcance del repositorio público

Este repositorio está pensado para distribución y comunicación pública del producto terminado. El desarrollo interno, el empaquetado técnico y la base de código se mantienen en repositorios locales o privados separados.

La documentación pública debe describir la experiencia del producto de forma consistente entre Linux y Windows, aun cuando cada plataforma utilice un artefacto binario distinto.

## Importante

Al descargar y utilizar `Project894`, aceptas los términos establecidos en [DISCLAIMER.md](DISCLAIMER.md) y [LICENSE](LICENSE).
