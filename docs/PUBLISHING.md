# Publicación de Releases

## Objetivo

Esta guía define cómo usar `Project894-Public` como repositorio oficial de distribución para Linux y Windows sin publicar código fuente.

## Artefactos esperados

Cada release pública debe considerar, cuando aplique:

- `Project894-x86_64.AppImage`
- `Project894.exe`

## Fuente de los binarios

Los binarios deben venir de los repositorios internos o locales donde se mantiene el código fuente y el flujo de empaquetado.

Este repositorio no debe generar builds por sí mismo.

## Flujo recomendado

1. Validar internamente la versión Linux.
2. Validar internamente la versión Windows.
3. Confirmar que ambos artefactos correspondan a la misma versión funcional.
4. Actualizar en este repositorio:
   - `README.md`
   - `CHANGELOG.md`
   - `RELEASE_NOTES.md`
   - documentación adicional si hubo cambios visibles al usuario
5. Crear o actualizar el tag/release público.
6. Adjuntar los binarios correspondientes.
7. Si el release ya existe para esa versión, anexar el nuevo artefacto faltante sin crear un release adicional.

## Checklist previo a publicar

- nombre correcto de archivos
- versión correcta en changelog y release notes
- cobertura de plataformas correcta
- licencia y disclaimer presentes
- ausencia total de código fuente
- ausencia de datos de usuario o artefactos intermedios

## Checklist posterior a publicar

- probar descarga del `.AppImage`
- probar descarga del `.exe`
- verificar que los enlaces públicos funcionen
- revisar que la descripción del release coincida con la versión
- confirmar que Linux y Windows conviven en el mismo release cuando aplique

## Qué no subir a este repositorio

- carpetas `src/`, `build/`, `dist/` internas
- scripts privados de build
- archivos temporales de empaquetado
- bases de datos, cachés o datos reales
- documentación que revele implementación interna innecesaria
