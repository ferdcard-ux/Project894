# Release Notes

## Version 1.2.0

Fecha de referencia: `2026-04-26`

### Resumen

`Project894` consolida una aplicación de escritorio para automatizar la consulta y gestión de evidencias académicas en Zajuna. Esta release pública unifica la distribución de Linux y Windows bajo una misma versión funcional, con mejoras de usabilidad, filtros por vista y una experiencia visual basada en `Hybrid Card-List View`.

### Artefactos publicados

- `Project894-x86_64.AppImage` para Linux
- `Project894.exe` para Windows

### Novedades funcionales

- Vista híbrida `Card-List` para `Todas Las Evidencias`
- Vista de `Evidencias Evaluadas` con filtros específicos
- Filtros separados por vista
- Filtro `Próximas a vencer`
- Exportación a Excel respetando la vista filtrada actual
- Mejora de la cabecera visual del login
- Validación de instructor más estable

### Mejoras técnicas visibles en la release

- Lógica de evaluación corregida para aceptar únicamente letras válidas
- Barra de herramientas simplificada para reducir ruido operativo
- Documentación pública alineada con la versión 1.2.0
- Distribución preparada para dos plataformas sin exponer código fuente

### Consideraciones operativas

- Linux: usar el archivo `.AppImage` con permisos de ejecución
- Windows: ejecutar `Project894.exe`
- Los datos siguen siendo locales al equipo del usuario
- La aplicación puede depender de conectividad con Zajuna para tareas de extracción en línea
