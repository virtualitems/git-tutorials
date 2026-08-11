---
title: "git citool"
source: "https://git-scm.com/docs/git-citool"
section: "graphical-tools"
---

# `git citool`

## Ejemplo de partida

```bash
git citool
```

Este caso usa `git citool` para preparar y crear commits desde una interfaz gráfica. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el repositorio y la vista u operación elegida en la interfaz.
- Operación: preparar y crear commits desde una interfaz gráfica.
- Comprobación: los comandos de consulta confirman el mismo estado que presenta la interfaz.

## Modelo mental

La interfaz presenta operaciones que también existen en el modelo de objetos, índice, referencias y commits. La vista cambia; el repositorio conserva el mismo estado.

Relaciona cada acción de la interfaz con índice, commit o referencia. Usa una consulta de Git para comprobar el cambio de estado.

## Forma de referencia

```text
git citool
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Realiza una operación en la interfaz y verifica el resultado con `git status`, `git log` o `git show`.

## Páginas relacionadas

- [`git gui`](../graphical-tools/gui.md)
- [`git instaweb`](../graphical-tools/instaweb.md)

## Fuente

- [git-citool - Graphical alternative to git-commit](https://git-scm.com/docs/git-citool)
