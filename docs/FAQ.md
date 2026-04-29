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

## ¿Qué cambia en la versión 1.3.0?

La versión `1.3.0` incorpora mejoras visibles para el usuario:

- mejor control de cambios pendientes al editar instructor y fechas
- mensajes y confirmaciones más consistentes en la interfaz
- aviso único cuando no existen datos locales en una vista
- transición de acceso más limpia al abrir la ventana principal

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

## ¿Linux y Windows comparten la misma versión funcional?

Sí. Este repositorio público se organiza para que una misma versión publicada agrupe los artefactos de Linux y Windows dentro del mismo release, siempre que ambos correspondan al mismo estado funcional del producto.

## ¿Puedo construir la app desde este repositorio?

No. El build y el código fuente se mantienen fuera de este repositorio público.

## ¿Puedo compartir binarios descargados con otros usuarios?

Solo si provienen de una release pública verificada y respetando la licencia y el disclaimer del proyecto.

## ¿Dónde se documenta el proceso de publicación?

En [docs/PUBLISHING.md](PUBLISHING.md).
