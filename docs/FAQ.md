# FAQ

## Que hace Project894?

Project894 permite consultar, gestionar y dar seguimiento a evidencias academicas desde la plataforma Zajuna SENA. Esta disponible como aplicacion de escritorio (Linux/Windows) y aplicacion nativa Android.

## Necesita internet?

Si, para validar credenciales y extraer informacion desde Zajuna. Solo algunos accesos pueden funcionar en modo offline si ya existe cache local valida.

## Este repositorio contiene el codigo fuente?

No. Este repositorio es unicamente para distribucion publica, documentacion y releases binarios.

## Donde descargo la aplicacion?

Desde la seccion de releases del repositorio.

## Que plataformas estan publicadas?

- **Linux** mediante `Project894-x86_64.AppImage`
- **Windows** mediante `Project894.exe`
- **Android** mediante `Project894-android-<version>.apk`

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

### Escritorio (Windows)
El archivo principal es `auth_debug.log`.

- En el `.exe` de Windows queda en `LOCALAPPDATA\\Project894\\data\\auth_debug.log`
- La aplicacion muestra esa ruta exacta cuando ocurre un error de autenticacion o scraping

### Android
Los logs de la aplicacion Android se almacenan en `Descargas/.Project894/`. Puedes copiarlos desde la pantalla de Ajustes > "Copiar registro de la aplicacion". La app te mostrara la ruta del archivo copiado.

## Que tecnologias usa?

### Escritorio (Linux/Windows)
- `PySide6`
- `Playwright`
- `SQLite`
- `cryptography`
- `pandas`
- `openpyxl`

### Android
- `Jetpack Compose` + `Material Design 3`
- `OkHttp` + `Jsoup` (scraping)
- `Room` + `SQLCipher` (base de datos local)
- `WorkManager` (sincronizacion en segundo plano)
- `Koin` (inyeccion de dependencias)
- `Navigation Compose` (navegacion)
- `DataStore` (preferencias de usuario)

## Como instalo la version Linux?

Descarga `Project894-x86_64.AppImage`, dale permiso de ejecucion y ejecutalo.

## Como instalo la version Windows?

Descarga `Project894.exe` y ejecutalo directamente. Si Windows SmartScreen muestra una advertencia, verifica el origen del archivo antes de continuar.

## Como instalo la version Android?

Descarga `Project894-android-<version>.apk` desde la seccion de releases, habilita la instalacion de apps de origenes desconocidos si es necesario, y abre el archivo APK para instalar.

## En Android, que pasa al abrir la app por primera vez?

Aparece un pop-up de terminos y condiciones que debes leer completamente y aceptar marcando la casilla de verificacion (se habilita al final del scroll). Si rechazas los terminos, la app se cierra.

## Donde se guardan los logs en Android?

Los logs se guardan en la carpeta `Descargas/.Project894/`. La app conserva automaticamente solo los 3 archivos de log mas recientes.

## Como funciona la actualización in-app en Android?

La app consulta la API de GitHub (`api.github.com/repos/ferdcard-ux/Project894/releases`) al abrir la pantalla de Ajustes. Si existe una version mas reciente de `Project894-android-*.apk`, muestra un dialogo con la nueva version, las notas del release y un boton para descargar. La descarga muestra una barra de progreso y al completarse, la app abre el instalador del sistema para que el usuario confirme la instalacion. Todo sin salir de la aplicacion.

## Que pasa si no hay internet al buscar actualizaciones?

La verificacion falla silenciosamente y no se muestra ningun dialogo. Puedes intentar de nuevo manualmente desde Ajustes > Buscar actualizaciones.

> Para preguntas especificas de Android, consulta [FAQ-Android.md](FAQ-Android.md).

## Linux y Windows comparten la misma version funcional?

Si. Este repositorio publico se organiza para que un mismo release pueda agrupar artefactos de Linux y Windows cuando ambos correspondan a la misma linea funcional.

## Puedo construir la app desde este repositorio?

No. El build y el codigo fuente se mantienen fuera de este repositorio publico.

## Puedo compartir binarios descargados con otros usuarios?

Solo si provienen de una release publica verificada y respetando la licencia y el disclaimer del proyecto.

## Donde se documenta el proceso de publicacion?

En [docs/PUBLISHING.md](PUBLISHING.md).
