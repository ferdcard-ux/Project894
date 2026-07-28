# Project894 para Windows

Version publica actual: `1.3.0`

Este documento resume el comportamiento y la instalacion del ejecutable `Project894.exe` publicado en el release activo.

## Instalacion

1. Descarga `Project894.exe` desde la seccion de releases.
2. Ejecuta el archivo.
3. Si Windows SmartScreen muestra una advertencia, valida el origen del binario antes de continuar.

## Cambios visibles en la linea 1.3.0

- control de cambios pendientes al editar instructor y fechas
- validacion de acceso desacoplada para mantener la interfaz responsiva
- mensajes operativos mas consistentes
- aviso unico cuando una vista no tiene datos locales
- mejor traspaso entre login y ventana principal
- mejor trazabilidad de errores mediante la ruta explicita de `auth_debug.log`

## Datos locales

El ejecutable de Windows guarda sus datos operativos en:

`LOCALAPPDATA\\Project894\\data`

Alli se almacenan la base local, la cache cifrada y los logs necesarios para soporte.

## Log principal

Si ocurre un fallo de autenticacion o scraping, revise:

`LOCALAPPDATA\\Project894\\data\\auth_debug.log`
