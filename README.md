# Project894

Aplicación de escritorio en PySide6 para automatizar la extracción, revisión y gestión local de evidencias académicas desde Zajuna.

La aplicación permite autenticarse con credenciales de Zajuna, extraer evidencias del curso, consultar evidencias evaluadas, editar instructor y estado en una base SQLite local cifrada, y exportar resultados a Excel.

## Estado del proyecto

- Versión actual de la aplicación: `1.1.0`
- Estado del empaquetado AppImage: completado
- Ubicación del AppImage: `dist/Project894-x86_64.AppImage`

## Características principales

- Interfaz nativa en `PySide6`
- Inicio de sesión con validación en Zajuna
- Caché local cifrada de credenciales para contingencias offline
- Base de datos local cifrada durante el reposo
- Vista `Todas Las Evidencias` con edición de `Instructor` y `Estado`
- Vista `Evidencias Evaluadas` con ítem, calificación y retroalimentación
- Búsqueda dentro de la tabla activa
- Exportación a Excel
- Scraping automatizado con `Playwright`

## Requisitos

- Python 3.10 o superior
- Linux de escritorio
- Dependencias de `requirements.txt`
- Navegador de Playwright instalado

## Puesta en marcha

1. Crear y activar un entorno virtual.
2. Instalar dependencias:

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
playwright install chromium
```

3. Ejecutar la aplicación:

```bash
python3 app.py
```

Si el proyecto ya trae un entorno local funcional, también puede ejecutarse con:

```bash
venv/bin/python app.py
```

## Estructura del repositorio

```text
.
├── app.py
├── requirements.txt
├── src/
│   ├── core/
│   ├── scraper/
│   └── ui/
├── data/
├── docs/
└── scratch/
```

## Módulos principales

- `app.py`: punto de entrada y estado global de la sesión
- `src/ui/login_dialog.py`: autenticación inicial
- `src/ui/main_window.py`: interfaz principal, tablas, búsqueda y exportación
- `src/ui/workers.py`: ejecución en segundo plano
- `src/core/database.py`: persistencia SQLite
- `src/core/security.py`: cifrado, claves y caché local
- `src/core/export_engine.py`: exportación a Excel
- `src/scraper/scraper_engine.py`: integración con Zajuna por Playwright

## Documentación disponible

- [CHANGELOG.md](CHANGELOG.md)
- [RELEASE_NOTES.md](RELEASE_NOTES.md)
- [CONTRIBUTING.md](CONTRIBUTING.md)
- [SECURITY.md](SECURITY.md)
- [docs/USERGUIDE.md](docs/USERGUIDE.md)
- [docs/FAQ.md](docs/FAQ.md)
- [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)

## Datos y seguridad

- La base local se maneja en `data/project894.db`
- El archivo puede mantenerse cifrado fuera de la sesión activa
- Las credenciales en caché se guardan cifradas localmente
- Los archivos sensibles de `data/` no deben publicarse en un repositorio remoto

## Alcance actual

El proyecto cuenta con una versión estable (1.1.0) con capacidades de extracción resiliente y empaquetado distribuible mediante AppImage para facilitar su uso en sistemas Linux.

## IMPORTANTE:

Al descargar y utilizar Project894, aceptas los términos establecidos en nuestro DISCLAIMER.md y LICENSE. Esta herramienta es de uso personal y académico.
