# Guía de Usuario

## 1. Propósito de la aplicación

`Project894` permite consultar y administrar evidencias académicas desde Zajuna en una interfaz de escritorio, con persistencia local para trabajo operativo y exportación a Excel.

## 2. Inicio de sesión

Al abrir la aplicación:

1. Selecciona el tipo de documento.
2. Ingresa tu número de documento.
3. Ingresa tu contraseña de Zajuna.
4. Presiona `Ingresar`.

Si la validación online falla por conectividad, la aplicación puede permitir acceso offline solo si las credenciales ya existen en caché local cifrada.

## 3. Pantalla principal

La ventana principal ofrece:

- selector de vista
- barra de búsqueda
- botón de exportación a Excel
- botón de cierre de sesión
- tabla principal de resultados

## 4. Vistas disponibles

### Todas Las Evidencias

Muestra:

- enlace
- título de la evidencia
- instructor
- fecha de apertura
- fecha de vencimiento
- estado

Acciones disponibles:

- editar instructor
- cambiar estado
- buscar por texto
- exportar la vista actual

### Evidencias Evaluadas

Muestra:

- ítem de calificación
- calificación por letra
- retroalimentación

## 5. Extracción de información

Desde el botón principal de extracción puedes cambiar entre:

- `Todas Las Evidencias`
- `Evidencias Evaluadas`

Al iniciar una extracción:

- la barra de progreso se activa
- la tabla se refresca al finalizar
- el resultado queda almacenado en la base local

## 6. Edición manual

### Instructor

- Se puede editar directamente desde la tabla.
- Si escribes un nombre nuevo, puede quedar disponible luego como opción reutilizable.

### Estado

Los estados disponibles actualmente son:

- `ENTREGADA`
- `EVALUADA`
- `NO ASIGNADA`
- `PENDIENTE`
- `VENCIDA`

Cada estado se representa con color visual en la tabla.

## 7. Búsqueda

La barra de búsqueda trabaja sobre la vista activa.

En `Todas Las Evidencias` permite buscar por:

- evidencia
- instructor
- fecha
- estado

En `Evidencias Evaluadas` permite buscar por:

- ítem
- calificación
- retroalimentación

## 8. Exportación

El botón `Exportar Excel` genera un archivo `.xlsx` de la vista visible en ese momento.

La exportación:

- incluye encabezados
- ajusta anchos de columna
- agrega filtro automático

## 9. Cierre de sesión

Al cerrar sesión:

- la aplicación solicita confirmación
- la base local puede volver a cifrarse
- la ventana principal se cierra

## 10. Recomendaciones de uso

- Verifica conexión antes de lanzar extracciones masivas
- Usa credenciales correctas y vigentes de Zajuna
- Exporta resultados cuando necesites compartir evidencias fuera de la app
- Evita manipular manualmente los archivos de `data/` mientras la aplicación esté abierta
