# FAQ

## ¿Qué hace Project894?

Automatiza la consulta y gestión local de evidencias académicas desde Zajuna en una aplicación de escritorio.

## ¿Necesita internet?

Sí, para validar credenciales y extraer información desde Zajuna. Solo algunos accesos pueden funcionar en modo offline si ya existe caché local válida.

## ¿Dónde se guardan los datos?

En la carpeta `data/`, principalmente en una base SQLite local.

## ¿La base de datos está protegida?

Sí. El proyecto incluye cifrado de base de datos y caché local cifrada de credenciales.

## ¿Qué pasa si Zajuna cambia su interfaz?

El scraping puede fallar si cambian selectores, formularios, rutas o el flujo de autenticación. En ese caso debe revisarse `src/scraper/scraper_engine.py`.

## ¿Qué tecnologías usa?

- `PySide6`
- `Playwright`
- `SQLite`
- `cryptography`
- `pandas`
- `openpyxl`

## ¿Cómo ejecuto la app en desarrollo?

```bash
venv/bin/python app.py
```

## ¿Necesito instalar algo adicional además de `pip install -r requirements.txt`?

Sí. También debes instalar Chromium para Playwright:

```bash
playwright install chromium
```

## ¿La aplicación ya está lista para AppImage?

Todavía no. Antes debe incorporarse el icono final y luego preparar el empaquetado.

## ¿Puedo compartir la carpeta `data/`?

No es recomendable. Allí pueden existir claves locales, caché cifrada y base de datos con información operativa.

## ¿Puedo usar varias cuentas?

La capa de seguridad ya contempla varias cuentas en caché local, aunque la sesión activa se maneja de una a la vez.
