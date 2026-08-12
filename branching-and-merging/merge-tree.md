---
title: "git merge-tree"
source: "https://git-scm.com/docs/git-merge-tree"
section: "branching-and-merging"
status: "source-audited"
version: "2.55.0"
---

# `git merge-tree`

Este caso usa `git merge-tree` para calcular una fusión y exponer su resultado sin cambiar el índice.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git merge-tree --write-tree main tema-portada
```

La invocación `git merge-tree --write-tree main tema-portada` ejecuta esta operación: calcular una fusión y exponer su resultado sin cambiar el índice. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Sintaxis y formas de invocación

```text
git merge-tree [--write-tree] [<options>] <branch1> <branch2>
git merge-tree [--trivial-merge] <base-tree> <branch1> <branch2> (deprecated)
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git merge-tree [--write-tree] [<options>] <branch1> <branch2>
   or: git merge-tree [--trivial-merge] <base-tree> <branch1> <branch2>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git merge-tree -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--write-tree`

Permite crear o escribir el elemento seleccionado.

```bash
git merge-tree --write-tree main tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--trivial-merge`

Limita calcular una fusión y exponer su resultado sin cambiar el índice al alcance identificado por trivial merge. En Git 2.51.1, la ayuda corta expresa el contrato como `do a trivial merge only`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-tree --trivial-merge --write-tree main tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--messages`

Incluye messages en la salida o cambia cómo `git merge-tree` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `also show informational/conflict messages`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-tree --messages --write-tree main tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quiet`

Reduce mensajes que no representan errores.

```bash
git merge-tree --quiet --write-tree main tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git merge-tree -z --write-tree main tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--name-only`

Muestra nombres de ruta sin el contenido del diff.

```bash
git merge-tree --name-only --write-tree main tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--allow-unrelated-histories`

Permite permitir unrelated histories cuando la forma predeterminada de `git merge-tree` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow merging unrelated histories`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-tree --allow-unrelated-histories --write-tree main tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git merge-tree` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git merge-tree --stdin --write-tree main tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--merge-base`

Define merge base para esta ejecución de `git merge-tree`. En Git 2.51.1, la ayuda corta expresa el contrato como `specify a merge-base for the merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-tree --merge-base=HEAD^{tree} --write-tree main tema-portada
git status --short
```

El ejemplo usa `HEAD^{tree}` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-X` y `--strategy-option`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git merge-tree` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `--strategy-option`

```bash
git merge-tree --strategy-option=Ana --write-tree main tema-portada
git status --short
```

En esta forma, `Ana` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

## Páginas relacionadas

- [`git refs`](../branching-and-merging/refs.md)
- [`git mergetool`](../branching-and-merging/mergetool.md)
- [`git rerere`](../branching-and-merging/rerere.md)

## Fuente

- [git-merge-tree - Perform merge without touching index or working tree](https://git-scm.com/docs/git-merge-tree)
