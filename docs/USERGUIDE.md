# Guía de Usuario

## 1. Propósito

`Project894` permite consultar, organizar y exportar evidencias académicas desde Zajuna en una aplicación de escritorio.

## 2. Instalación

### Linux

1. Descarga `Project894-x86_64.AppImage`.
2. Otorga permiso de ejecución.
3. Ejecuta el archivo.

### Windows

1. Descarga `Project894.exe`.
2. Ejecuta el archivo.
3. Si el sistema muestra una advertencia de seguridad, valida que el binario provenga de una release oficial.

## 3. Inicio de sesión

Al abrir la aplicación:

1. selecciona el tipo de documento
2. ingresa tu número de documento
3. ingresa tu contraseña
4. presiona `Ingresar`

Si la validación en línea falla por conectividad, la aplicación puede permitir acceso offline si ya existe caché local válida.

Durante el acceso, la aplicación puede mostrar mensajes de progreso mientras valida la sesión y prepara la interfaz principal.

## 4. Vista principal

La interfaz ofrece:

- selector de vista
- búsqueda sobre la vista activa
- filtros por contexto
- exportación a Excel
- controles de sesión

## 5. Vistas disponibles

### Todas Las Evidencias

Permite consultar evidencias del curso y editar campos operativos como instructor, estado y fechas.

### Evidencias Evaluadas

Permite consultar ítems, calificaciones y retroalimentación.

## 6. Filtros

La aplicación incluye filtros separados por vista:

- en `Todas Las Evidencias`, filtrado por estado y `Próximas a vencer`
- en `Evidencias Evaluadas`, filtrado entre `Todas`, `Evaluadas` y `No Evaluadas`

Si una vista no tiene datos locales, la aplicación muestra un aviso unificado indicando que debe ejecutar la extracción desde Zajuna y que el proceso puede tardar algunos minutos.

## 7. Exportación

La exportación genera un archivo `.xlsx` a partir de la vista filtrada actual.

## 8. Recomendaciones

- usa únicamente binarios descargados desde releases oficiales
- verifica conexión antes de extracciones masivas
- evita compartir archivos locales con información operativa
- confirma o descarta cambios pendientes antes de cerrar la aplicación cuando estés editando datos locales
