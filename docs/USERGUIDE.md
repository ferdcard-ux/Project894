# Guia de Usuario

## 1. Proposito

`Project894` permite consultar, organizar y exportar evidencias academicas desde Zajuna en una aplicacion de escritorio.

## 2. Instalacion

### Linux

1. Descarga `Project894-x86_64.AppImage`.
2. Otorga permiso de ejecucion.
3. Ejecuta el archivo.

### Windows

1. Descarga `Project894.exe`.
2. Ejecuta el archivo.
3. Si el sistema muestra una advertencia de seguridad, valida que el binario provenga de una release oficial.

## 3. Inicio de sesion

Al abrir la aplicacion:

1. selecciona el tipo de documento
2. ingresa tu numero de documento
3. ingresa tu contrasena
4. presiona `Ingresar`

Si la validacion en linea falla por conectividad, la aplicacion puede permitir acceso offline si ya existe cache local valida.

Durante el acceso, la aplicacion puede mostrar mensajes de progreso mientras valida la sesion y prepara la interfaz principal.

## 4. Vista principal

La interfaz ofrece:

- selector de vista
- busqueda sobre la vista activa
- filtros por contexto
- exportacion a Excel
- controles de sesion

## 5. Vistas disponibles

### Todas Las Evidencias

Permite consultar evidencias del curso y editar campos operativos como instructor, estado y fechas.

### Evidencias Evaluadas

Permite consultar items, calificaciones y retroalimentacion.

## 6. Filtros y extraccion

La aplicacion incluye filtros separados por vista:

- en `Todas Las Evidencias`, filtrado por estado y `Proximas a vencer`
- en `Evidencias Evaluadas`, filtrado entre `Todas`, `Evaluadas` y `No Evaluadas`

Si una vista no tiene datos locales, la aplicacion muestra un aviso unificado indicando que debe ejecutar la extraccion desde Zajuna y que el proceso puede tardar algunos minutos.

## 7. Edicion local

La version `1.3.0` refuerza el manejo de cambios pendientes:

- al editar instructor o fechas, la aplicacion solicita confirmacion antes de descartar cambios no guardados
- los mensajes operativos mantienen una presentacion visual consistente
- el flujo de acceso evita que el dialogo de login quede retenido en segundo plano

## 8. Exportacion

La exportacion genera un archivo `.xlsx` a partir de la vista filtrada actual.

## 9. Datos y logs en Windows

En Windows, el `.exe` crea y utiliza la carpeta:

`LOCALAPPDATA\\Project894\\data`

En esa ubicacion se almacenan:

- base local
- cache cifrada
- logs operativos

Si ocurre un fallo durante autenticacion o scraping, revise `auth_debug.log` en esa misma carpeta.

## 10. Recomendaciones

- usa unicamente binarios descargados desde releases oficiales
- verifica conexion antes de extracciones masivas
- evita compartir archivos locales con informacion operativa
- confirma o descarta cambios pendientes antes de cerrar la aplicacion cuando estes editando datos locales
