# Contributing

## Objetivo

Este documento define una base mínima para colaborar de forma consistente sobre `Project894`.

## Requisitos de desarrollo

- Python 3.10 o superior
- Entorno virtual local
- Dependencias de `requirements.txt`
- Navegador de Playwright instalado

## Preparación del entorno

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
playwright install chromium
```

## Ejecución local

```bash
venv/bin/python app.py
```

## Convenciones recomendadas

- Mantener la UI en `src/ui/`
- Mantener la lógica de persistencia y seguridad en `src/core/`
- Mantener scraping y navegación web en `src/scraper/`
- Evitar mezclar lógica de acceso a datos dentro de la interfaz
- No subir datos reales ni secretos almacenados en `data/`
- Documentar cambios funcionales relevantes en `CHANGELOG.md`

## Antes de abrir cambios

- Verificar sintaxis mínima de Python:

```bash
venv/bin/python -m py_compile app.py src/ui/main_window.py
```

- Probar manualmente, al menos:
  - inicio de sesión
  - carga de vistas
  - edición de instructor
  - edición de estado
  - exportación a Excel

## Alcance de futuras contribuciones

Áreas especialmente sensibles:

- autenticación con Zajuna
- cifrado y caché local
- integridad de la base SQLite
- scraping frente a cambios de selectores
- empaquetado AppImage

## Commits

Se recomienda usar mensajes breves y orientados a intención, por ejemplo:

- `feat: add AppImage metadata`
- `fix: preserve status colors in evidence table`
- `docs: add repository guides`
