# FAQ

## Que hace Project894?

Automatiza la consulta y gestion local de evidencias academicas desde Zajuna en una aplicacion de escritorio.

## Necesita internet?

Si, para validar credenciales y extraer informacion desde Zajuna. Solo algunos accesos pueden funcionar en modo offline si ya existe cache local valida.

## Este repositorio contiene el codigo fuente?

No. Este repositorio es unicamente para distribucion publica, documentacion y releases binarios.

## Donde descargo la aplicacion?

Desde la seccion de releases del repositorio.

## Que plataformas estan publicadas?

- Linux mediante `Project894-x86_64.AppImage`
- Windows mediante `Project894.exe`

## Que cambia en la version 1.3.0?

La version `1.3.0` incorpora mejoras visibles para el usuario:

- mejor control de cambios pendientes al editar instructor y fechas
- mensajes y confirmaciones mas consistentes en la interfaz
- aviso unico cuando no existen datos locales en una vista
- transicion de acceso mas limpia al abrir la ventana principal
- mejor trazabilidad de errores en Windows gracias a la ruta explicita de `auth_debug.log`

## Donde se guardan los datos en Windows?

El `.exe` guarda sus datos operativos en `LOCALAPPDATA\\Project894\\data`.

Alli se encuentran la base local, la cache cifrada y los logs de soporte.

## Donde encuentro el log si falla Zajuna o la extraccion?

El archivo principal es `auth_debug.log`.

- En el `.exe` de Windows queda en `LOCALAPPDATA\\Project894\\data\\auth_debug.log`
- La aplicacion muestra esa ruta exacta cuando ocurre un error de autenticacion o scraping

## Que tecnologias usa?

- `PySide6`
- `Playwright`
- `SQLite`
- `cryptography`
- `pandas`
- `openpyxl`

## Como instalo la version Linux?

Descarga `Project894-x86_64.AppImage`, dale permiso de ejecucion y ejecutalo.

## Como instalo la version Windows?

Descarga `Project894.exe` y ejecutalo directamente. Si Windows SmartScreen muestra una advertencia, verifica el origen del archivo antes de continuar.

## Linux y Windows comparten la misma version funcional?

Si. Este repositorio publico se organiza para que un mismo release pueda agrupar artefactos de Linux y Windows cuando ambos correspondan a la misma linea funcional.

## Puedo construir la app desde este repositorio?

No. El build y el codigo fuente se mantienen fuera de este repositorio publico.

## Puedo compartir binarios descargados con otros usuarios?

Solo si provienen de una release publica verificada y respetando la licencia y el disclaimer del proyecto.

## Donde se documenta el proceso de publicacion?

En [docs/PUBLISHING.md](PUBLISHING.md).
