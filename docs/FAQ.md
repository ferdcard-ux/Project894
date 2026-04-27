# FAQ

## ¿Qué hace Project894?

Automatiza la consulta y gestión local de evidencias académicas desde Zajuna en una aplicación de escritorio.

## ¿Necesita internet?

Sí, para validar credenciales y extraer información desde Zajuna. Solo algunos accesos pueden funcionar en modo offline si ya existe caché local válida.

## ¿Este repositorio contiene el código fuente?

No. Este repositorio es únicamente para distribución pública, documentación y releases binarios.

## ¿Dónde descargo la aplicación?

Desde la sección de releases del repositorio.

## ¿Qué plataformas están publicadas?

- Linux mediante `Project894-x86_64.AppImage`
- Windows mediante `Project894.exe`

## ¿La versión 1.2.0 publica Linux y Windows al mismo tiempo?

Sí. Cuando ambos artefactos están disponibles, la publicación pública de `1.2.0` debe conservar juntos `Project894-x86_64.AppImage` y `Project894.exe`.

## ¿Qué tecnologías usa?

- `PySide6`
- `Playwright`
- `SQLite`
- `cryptography`
- `pandas`
- `openpyxl`

## ¿Cómo instalo la versión Linux?

Descarga `Project894-x86_64.AppImage`, dale permiso de ejecución y ejecútalo.

## ¿Cómo instalo la versión Windows?

Descarga `Project894.exe` y ejecútalo directamente. Si Windows SmartScreen muestra una advertencia, verifica el origen del archivo antes de continuar.

## ¿Puedo construir la app desde este repositorio?

No. El build y el código fuente se mantienen fuera de este repositorio público.

## ¿Puedo compartir binarios descargados con otros usuarios?

Solo si provienen de una release pública verificada y respetando la licencia y el disclaimer del proyecto.

## ¿Dónde se documenta el proceso de publicación?

En [docs/PUBLISHING.md](PUBLISHING.md).
