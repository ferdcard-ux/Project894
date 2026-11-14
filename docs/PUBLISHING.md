# Publicacion de Releases

## Objetivo

Esta guia define como usar `Project894 Public` como repositorio oficial de distribucion sin publicar codigo fuente.

## Artefactos esperados

Cada release publica puede considerar, cuando aplique:

- `Project894-x86_64.AppImage`
- `Project894.exe`
- `Project894-android-<version>.apk`

En el caso del release activo `v1.3.0`, el ajuste actual consiste en reemplazar el artefacto `Project894.exe` sin crear un nuevo tag. Para las versiones de Android, cada nueva version (por ejemplo la `2.0.9`) se publica como un nuevo tag/release con su APK `Project894-android-<version>.apk`.

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

## Flujo recomendado para publicar una version de Android

1. Compilar el release en el entorno interno con la clave de publicacion (el script interno de build verifica la firma).
2. Verificar el APK:
   - `apksigner verify --print-certs Project894-android-<version>.apk` → SHA-256 `bdcf8658236171733ef576587db4db2303a64e9d270e66e9b0c6f3ea6e82e25b`
   - version (`versionName`/`versionCode`) correcta
3. Mover la seccion `[Unreleased]` del `CHANGELOG.md` a la nueva version y actualizar `RELEASE_NOTES.md`, `README.md` (release activo), `NOTA_ARTEFACTOS.md` y las guias Android si hubo cambios visibles.
4. Crear el tag/release `v<version>` y adjuntar `Project894-android-<version>.apk`.
5. Comprobar desde un dispositivo con la version anterior que la actualizacion in-app la detecta e instala.

Un APK firmado con otra clave no actualiza las instalaciones existentes: no se publica.

## Checklist previo a publicar

- nombre correcto del archivo (`Project894.exe`, `Project894-android-<version>.apk`)
- en Android, huella SHA-256 de firma identica a la de las versiones anteriores
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
