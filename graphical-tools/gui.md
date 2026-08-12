---
title: "git gui"
source: "https://git-scm.com/docs/git-gui"
section: "graphical-tools"
status: "source-audited"
version: "2.55.0"
---

# `git gui`

Este caso usa `git gui` para usar una interfaz gráfica para preparar cambios y crear commits.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La interfaz presenta operaciones que también existen en el modelo de objetos, índice, referencias y commits. La vista cambia; el repositorio conserva el mismo estado.

Relaciona cada acción de la interfaz con índice, commit o referencia. Usa una consulta de Git para comprobar el cambio de estado.

## Ejemplo mínimo

```bash
git gui
```

La invocación `git gui` ejecuta esta operación: usar una interfaz gráfica para preparar cambios y crear commits. Después, los comandos de consulta confirman el mismo estado que presenta la interfaz.

## Sintaxis y formas de invocación

```text
git gui [<command>] [<arguments>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git gui -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-h`

Activa h durante usar una interfaz gráfica para preparar cambios y crear commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git gui -h
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git instaweb`](../graphical-tools/instaweb.md)
- [`git citool`](../graphical-tools/citool.md)
- [`gitk`](../graphical-tools/gitk.md)

## Fuente

- [git-gui - A portable graphical interface to Git](https://git-scm.com/docs/git-gui)
