---
title: "git mergetool"
source: "https://git-scm.com/docs/git-mergetool"
section: "branching-and-merging"
status: "source-audited"
version: "2.55.0"
---

# `git mergetool`

Este caso usa `git mergetool` para abrir una herramienta para resolver conflictos de fusión.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git mergetool
git status --short
```

La invocación `git mergetool` ejecuta esta operación: abrir una herramienta para resolver conflictos de fusión. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Sintaxis y formas de invocación

```text
git mergetool [--tool=<tool>] [-y | --[no-]prompt] [<file>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git mergetool [--tool=tool] [--tool-help] [-y|--no-prompt|--prompt] [-g|--gui|--no-gui] [-O<orderfile>] [file to merge] ...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git mergetool -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--tool`

Activa tool durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git mergetool --tool
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-y`

Activa y durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git mergetool -y
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--prompt`

Activa prompt durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git mergetool --prompt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tool-help`

Activa tool ayuda durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git mergetool --tool-help
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-prompt`

Desactiva el comportamiento `prompt` para esta invocación.

```bash
git mergetool --no-prompt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-g`

Activa g durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git mergetool -g
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--gui`

Activa gui durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git mergetool --gui
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gui`

Desactiva el comportamiento `gui` para esta invocación.

```bash
git mergetool --no-gui
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-O`

Activa O durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git mergetool -O
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git merge-tree`](../branching-and-merging/merge-tree.md)
- [`git merge`](../branching-and-merging/merge.md)
- [`git refs`](../branching-and-merging/refs.md)

## Fuente

- [git-mergetool - Run merge conflict resolution tools to resolve merge conflicts](https://git-scm.com/docs/git-mergetool)
