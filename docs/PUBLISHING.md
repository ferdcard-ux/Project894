# Publicacion de Releases

## Objetivo

Esta guia define como usar `Project894 Public` como repositorio oficial de distribucion sin publicar codigo fuente.

## Artefactos esperados

Cada release publica puede considerar, cuando aplique:

- `Project894-x86_64.AppImage`
- `Project894.exe`

En el caso del release activo `v1.3.0`, el ajuste actual consiste en reemplazar el artefacto `Project894.exe` sin crear un nuevo tag.

## Fuente de los binarios

Los binarios deben venir de los repositorios internos o locales donde se mantiene el codigo fuente y el flujo de empaquetado.

Este repositorio no debe generar builds por si mismo.

## Flujo recomendado para reemplazar el ejecutable de Windows

1. Validar internamente la compilacion Windows.
2. Confirmar que corresponde funcionalmente a `v1.3.0`.
3. Actualizar en este repositorio:
   - `README.md`
   - `README-Win.md`
   - `BUILD_WINDOWS.md`
   - `CHANGELOG.md`
   - `RELEASE_NOTES.md`
   - documentacion adicional si hubo cambios visibles al usuario
4. Reemplazar el asset `Project894.exe` dentro del release activo `v1.3.0`.
5. Verificar que el release conserve la descripcion correcta y que el enlace de descarga apunte al binario actualizado.

## Checklist previo a publicar

- nombre correcto del archivo `Project894.exe`
- version correcta en changelog y release notes
- ausencia total de codigo fuente
- ausencia de datos de usuario o artefactos intermedios
- coherencia entre la documentacion publica y el comportamiento real del ejecutable

## Checklist posterior a publicar

- probar descarga del `.exe`
- revisar que la descripcion del release coincida con la version
- confirmar que el asset reemplazado sea el mas reciente
- verificar que los enlaces publicos funcionen

## Que no subir a este repositorio

- carpetas `src/`, `build/`, `dist/` internas
- scripts privados de build
- archivos temporales de empaquetado
- bases de datos, caches o datos reales
- documentacion que revele implementacion interna sensible
