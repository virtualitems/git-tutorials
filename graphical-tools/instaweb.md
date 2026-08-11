---
title: "git instaweb"
source: "https://git-scm.com/docs/git-instaweb"
section: "graphical-tools"
---

# `git instaweb`

## Ejemplo de partida

```bash
git instaweb --start
git instaweb --stop
```

Este caso usa `git instaweb` para iniciar una instancia temporal de gitweb. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el repositorio y la vista u operación elegida en la interfaz.
- Operación: iniciar una instancia temporal de gitweb.
- Comprobación: los comandos de consulta confirman el mismo estado que presenta la interfaz.

## Modelo mental

La interfaz presenta operaciones que también existen en el modelo de objetos, índice, referencias y commits. La vista cambia; el repositorio conserva el mismo estado.

Relaciona cada acción de la interfaz con índice, commit o referencia. Usa una consulta de Git para comprobar el cambio de estado.

## Forma de referencia

```text
git instaweb [--local] [--httpd=<httpd>] [--port=<port>]
               [--browser=<browser>]
git instaweb [--start] [--stop] [--restart]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Realiza una operación en la interfaz y verifica el resultado con `git status`, `git log` o `git show`.

## Páginas relacionadas

- [`gitk`](../graphical-tools/gitk.md)
- [`git gui`](../graphical-tools/gui.md)
- [`gitweb`](../graphical-tools/gitweb.md)

## Fuente

- [git-instaweb - Instantly browse your working repository in gitweb](https://git-scm.com/docs/git-instaweb)
