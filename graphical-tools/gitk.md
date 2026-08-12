---
title: "gitk"
source: "https://git-scm.com/docs/gitk"
section: "graphical-tools"
status: "source-audited"
version: "2.55.0"
---

# `gitk`

Este caso usa `gitk` para explorar el historial y sus relaciones en una interfaz gráfica.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La interfaz presenta operaciones que también existen en el modelo de objetos, índice, referencias y commits. La vista cambia; el repositorio conserva el mismo estado.

Relaciona cada acción de la interfaz con índice, commit o referencia. Usa una consulta de Git para comprobar el cambio de estado.

## Ejemplo mínimo

```bash
gitk --all
```

La invocación `gitk --all` ejecuta esta operación: explorar el historial y sus relaciones en una interfaz gráfica. Después, los comandos de consulta confirman el mismo estado que presenta la interfaz.

## Sintaxis y formas de invocación

```text
gitk [<options>] [<revision-range>] [--] [<path>…]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Páginas relacionadas

- [`gitweb`](../graphical-tools/gitweb.md)
- [`git instaweb`](../graphical-tools/instaweb.md)
- [`git gui`](../graphical-tools/gui.md)

## Fuente

- [gitk - The Git repository browser](https://git-scm.com/docs/gitk)
