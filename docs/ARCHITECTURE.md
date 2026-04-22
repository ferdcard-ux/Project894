# Arquitectura

## Resumen

`Project894` está organizado en tres capas principales:

- interfaz de usuario
- núcleo de aplicación
- automatización y scraping

## Diagrama conceptual

```text
app.py
  ├── SecurityManager
  ├── LoginDialog
  │     ├── validate_zajuna_credentials()
  │     ├── prepare_database_for_session()
  │     └── DatabaseManager
  └── MainWindow
        ├── DataWorker
        │     └── scraper_engine.py
        ├── DatabaseManager
        └── export_engine.py
```

## Componentes

### 1. app.py

- Inicializa `QApplication`
- Carga `style.qss`
- Crea el estado compartido de sesión
- Abre `LoginDialog`
- Lanza `MainWindow` si la autenticación fue exitosa

### 2. Capa UI

#### `src/ui/login_dialog.py`

- Captura documento, tipo de documento y contraseña
- Carga credenciales cacheadas
- Valida acceso online con Zajuna
- Permite contingencia offline si la caché coincide

#### `src/ui/main_window.py`

- Gestiona las vistas principales
- Renderiza la tabla de evidencias
- Permite editar instructor y estado
- Permite buscar y exportar
- Coordina tareas en segundo plano

#### `src/ui/workers.py`

- Ejecuta scraping sin bloquear la interfaz
- Emite señales de progreso, error y finalización

### 3. Capa core

#### `src/core/database.py`

- Crea y migra la base local
- Administra `course_evidences`, `graded_items` e `instructors`
- Sincroniza datos de evidencias
- Persiste cambios manuales de instructor y estado

#### `src/core/security.py`

- Genera o carga salt y claves locales
- Deriva claves heredadas por usuario
- Cifra y descifra archivos
- Administra la caché local de acceso

#### `src/core/export_engine.py`

- Exporta tablas a Excel con `pandas` y `openpyxl`

### 4. Capa scraper

#### `src/scraper/scraper_engine.py`

- Valida conectividad a Zajuna
- Automatiza login con Playwright
- Extrae evidencias del curso
- Extrae ítems evaluados
- Normaliza fechas y enlaces

## Persistencia

Tablas principales:

- `course_evidences`
- `graded_items`
- `instructors`
- `configuracion`
- `catalogos`

## Flujo principal

1. El usuario inicia sesión.
2. Se valida acceso online o se autoriza contingencia offline.
3. Se prepara la base para la sesión.
4. La UI principal permite extraer, buscar, editar y exportar.
5. Al cerrar, la base local puede volver a cifrarse.

## Observaciones de mantenimiento

- Los cambios en scraping suelen impactar autenticación y extracción.
- Los cambios en seguridad pueden afectar compatibilidad con bases antiguas.
- Los cambios de UI deben revisarse junto con `style.qss`.
