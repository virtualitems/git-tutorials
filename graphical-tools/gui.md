---
title: "git gui"
source: "https://git-scm.com/docs/git-gui"
section: "graphical-tools"
---

# `git gui`

## Ejemplo de partida

```bash
git gui
```

Este caso usa `git gui` para usar una interfaz gráfica para preparar cambios y crear commits. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el repositorio y la vista u operación elegida en la interfaz.
- Operación: usar una interfaz gráfica para preparar cambios y crear commits.
- Comprobación: los comandos de consulta confirman el mismo estado que presenta la interfaz.

## Modelo mental

La interfaz presenta operaciones que también existen en el modelo de objetos, índice, referencias y commits. La vista cambia; el repositorio conserva el mismo estado.

Relaciona cada acción de la interfaz con índice, commit o referencia. Usa una consulta de Git para comprobar el cambio de estado.

## Forma de referencia

```text
git gui [<command>] [<arguments>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Realiza una operación en la interfaz y verifica el resultado con `git status`, `git log` o `git show`.

## Páginas relacionadas

- [`git instaweb`](../graphical-tools/instaweb.md)
- [`git citool`](../graphical-tools/citool.md)
- [`gitk`](../graphical-tools/gitk.md)

## Fuente

- [git-gui - A portable graphical interface to Git](https://git-scm.com/docs/git-gui)
