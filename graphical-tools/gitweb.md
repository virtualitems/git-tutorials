---
title: "gitweb"
source: "https://git-scm.com/docs/gitweb"
section: "graphical-tools"
---

# `gitweb`

## Ejemplo de partida

```bash
GITWEB_CONFIG=/etc/gitweb.conf gitweb.cgi
```

Este caso usa `gitweb` para publicar repositorios mediante una interfaz web. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el repositorio y la vista u operación elegida en la interfaz.
- Operación: publicar repositorios mediante una interfaz web.
- Comprobación: los comandos de consulta confirman el mismo estado que presenta la interfaz.

## Modelo mental

La interfaz presenta operaciones que también existen en el modelo de objetos, índice, referencias y commits. La vista cambia; el repositorio conserva el mismo estado.

Relaciona cada acción de la interfaz con índice, commit o referencia. Usa una consulta de Git para comprobar el cambio de estado.

## Forma de referencia

```text
GITWEB_CONFIG=/etc/gitweb.conf gitweb.cgi
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Realiza una operación en la interfaz y verifica el resultado con `git status`, `git log` o `git show`.

## Páginas relacionadas

- [`gitk`](../graphical-tools/gitk.md)
- [`git instaweb`](../graphical-tools/instaweb.md)

## Fuente

- [gitweb - Git web interface (web frontend to Git repositories)](https://git-scm.com/docs/gitweb)
