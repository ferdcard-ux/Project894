# Build de Windows

## Alcance

Este documento describe el flujo publico de reemplazo del ejecutable Windows en un release existente.

No es una guia para compilar desde este repositorio, ya que el codigo fuente y el empaquetado tecnico viven fuera de este arbol publico.

## Release activo

- tag: `v1.3.0`
- artefacto a reemplazar: `Project894.exe`

## Flujo publico de actualizacion

1. Obtener la compilacion validada desde el entorno interno de Windows.
2. Confirmar que el binario corresponde a la linea funcional `1.3.0`.
3. Actualizar esta documentacion publica con los cambios visibles de la variante Windows.
4. Eliminar el asset anterior `Project894.exe` del release `v1.3.0`.
5. Subir el nuevo `Project894.exe`.
6. Verificar tamano, nombre y descarga del asset publicado.

## Verificaciones minimas

- nombre exacto del archivo: `Project894.exe`
- documentacion sincronizada con la experiencia visible de Windows
- release notes actualizadas
- descarga valida desde la pagina del release
