# Contributing

## Objetivo

Este repositorio recibe cambios relacionados con distribución pública, documentación y publicación de releases de `Project894`.

No es un repositorio de desarrollo de código fuente.

## Alcance permitido

Cambios apropiados para este repositorio:

- documentación pública
- changelog y release notes
- instrucciones de instalación por plataforma
- material de publicación de releases
- referencias a artefactos binarios

Cambios fuera de alcance:

- lógica de aplicación
- interfaz interna
- scraping
- seguridad implementativa
- empaquetado técnico dentro del código fuente privado

## Antes de abrir cambios

Verifica al menos:

- que la documentación no revele código o rutas internas innecesarias
- que los nombres de artefactos públicos sean correctos
- que Linux y Windows estén cubiertos cuando la versión pública aplique a ambas plataformas
- que `CHANGELOG.md` y `RELEASE_NOTES.md` estén sincronizados

## Publicación de releases

La guía operativa para publicar nuevas versiones está en:

- [docs/PUBLISHING.md](docs/PUBLISHING.md)

## Commits

Se recomiendan mensajes breves y orientados a intención, por ejemplo:

- `docs: update public installation guide`
- `release: publish notes for 1.2.0`
- `docs: standardize public distribution workflow`
