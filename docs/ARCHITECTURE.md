# Arquitectura Publica del Repositorio

## Resumen

Este repositorio no documenta el codigo fuente interno. Documenta la arquitectura publica de distribucion usada para publicar releases y explicar el comportamiento visible de los artefactos.

## Componentes publicos

El repositorio se organiza en estas piezas:

- documentacion principal del producto
- changelog y release notes
- guias de instalacion y uso para usuarios finales
- guias operativas para reemplazo de artefactos
- releases binarios publicados en GitHub

## Modelo de distribucion

```text
Repositorios privados / locales
  |-- build Linux
  |-- build Windows
  `-- validacion interna
           |
           v
Project894 Public
  |-- README publico
  |-- README-Win
  |-- BUILD_WINDOWS
  |-- changelog
  |-- release notes
  `-- releases binarios
        |-- Project894-x86_64.AppImage
        `-- Project894.exe
```

## Separacion de responsabilidades

### Repositorios internos

- desarrollo del codigo fuente
- empaquetado tecnico
- pruebas funcionales antes de publicar
- mantenimiento de seguridad y datos sensibles

### Repositorio publico

- distribucion de binarios finales
- comunicacion de cambios por version
- documentacion de instalacion y uso
- referencias publicas de soporte, licencia y disclaimer
- conservacion del historial de releases

## Flujo del artefacto Windows

1. El ejecutable se genera y valida en el entorno interno de Windows.
2. Se confirma que la compilacion corresponde a la linea funcional deseada, en este caso `v1.3.0`.
3. Se sincroniza la documentacion publica con los cambios visibles de Windows.
4. Se reemplaza `Project894.exe` en el release activo cuando la actualizacion no requiere un nuevo tag.

## Objetivo de esta separacion

- evitar exponer codigo fuente
- concentrar las descargas en un unico punto publico
- reducir el riesgo de publicar material interno por error
- permitir reemplazos controlados de binarios dentro de un release existente cuando aplique
- asegurar que la documentacion publica represente fielmente el comportamiento del ejecutable publicado
