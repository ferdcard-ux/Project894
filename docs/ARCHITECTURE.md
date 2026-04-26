# Arquitectura Pública del Repositorio

## Resumen

Este repositorio no documenta la arquitectura interna del código fuente. Documenta únicamente la arquitectura pública de distribución.

## Componentes públicos

El repositorio se organiza en cuatro piezas:

- documentación principal del producto
- changelog y release notes
- guías de instalación para usuarios finales
- guía de publicación de releases binarios

## Modelo de distribución

```text
Repositorios privados / locales
  ├── build Linux
  ├── build Windows
  └── validación interna
           │
           ▼
Project894-Public
  ├── README público
  ├── documentación de uso
  ├── changelog
  ├── release notes
  └── releases binarios
        ├── Project894-x86_64.AppImage
        └── Project894.exe
```

## Separación de responsabilidades

### Repositorios internos

- desarrollo del código fuente
- empaquetado técnico
- pruebas de implementación
- mantenimiento de seguridad interna

### Repositorio público

- distribución de binarios finales
- comunicación de cambios por versión
- documentación de instalación y uso
- referencias públicas de soporte y licencia

## Objetivo de esta separación

- evitar exponer código fuente
- concentrar las descargas en un único punto público
- mantener Linux y Windows bajo una sola narrativa de release
- reducir el riesgo de publicar material interno por error
