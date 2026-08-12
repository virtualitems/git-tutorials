---
title: "git switch"
source: "https://git-scm.com/docs/git-switch"
section: "branching-and-merging"
status: "source-audited"
version: "2.55.0"
---

# `git switch`

Este caso usa `git switch` para cambiar de rama o crear una rama antes de cambiar.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git switch -c tema-portada
git switch main
```

La invocación `git switch -c tema-portada` ejecuta esta operación: cambiar de rama o crear una rama antes de cambiar. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Sintaxis y formas de invocación

```text
git switch [<options>] [--no-guess] <branch>
git switch [<options>] --detach [<start-point>]
git switch [<options>] (-c|-C) <new-branch> [<start-point>]
git switch [<options>] --orphan <new-branch>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git switch [<options>] [<branch>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git switch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--no-guess`

Desactiva el comportamiento `guess` para esta invocación.

```bash
git switch --no-guess -c tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--detach` y `-d`

Hace que `HEAD` apunte directamente a un commit.

#### Ejemplo con `--detach`

```bash
git switch --detach -c tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-c` y `--create`

Permite crear o escribir el elemento seleccionado.

#### Ejemplo con `--create`

```bash
git switch --create=main
git status --short
```

En esta forma, `main` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-C` y `--force-create`

Permite crear o escribir el elemento seleccionado.

#### Ejemplo con `--force-create`

```bash
git switch --force-create=main -c tema-portada
git status --short
```

En esta forma, `main` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--orphan`

Crea o cambia a una rama sin padres en el historial existente. En Git 2.51.1, la ayuda corta expresa el contrato como `new unborn branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git switch --orphan=main -c tema-portada
git status --short
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--guess`

Permite deducir una rama local a partir de una rama remota con el mismo nombre. En Git 2.51.1, la ayuda corta expresa el contrato como `second guess 'git switch <no-such-branch>'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git switch --guess -c tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--discard-changes`

Activa discard changes durante cambiar de rama o crear una rama antes de cambiar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `throw away local modifications`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git switch --discard-changes -c tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git switch --quiet -c tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

```bash
git switch --recurse-submodules -c tema-portada
git status --short
```

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git switch --progress -c tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--merge`

Ejecuta merge durante cambiar de rama o crear una rama antes de cambiar. En Git 2.51.1, la ayuda corta expresa el contrato como `perform a 3-way merge with the new branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--merge`

```bash
git switch --merge -c tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--conflict`

Selecciona el estilo de marcadores que Git escribe al materializar un conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `conflict style (merge, diff3, or zdiff3)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git switch --conflict=short -c tema-portada
git status --short
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-t` y `--track`

Crea o ajusta la asociación de seguimiento solicitada.

#### Ejemplo con `--track`

```bash
git switch --track=valor -c tema-portada
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git switch --force -c tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--overwrite-ignore`

Excluye elementos que cumplan la condición indicada.

```bash
git switch --overwrite-ignore -c tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-other-worktrees`

Excluye elementos que cumplan la condición indicada.

```bash
git switch --ignore-other-worktrees -c tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git switch --no-recurse-submodules -c tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git switch --no-progress -c tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-track`

Desactiva para esta invocación el comportamiento que habilita `--track`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git switch --no-track -c tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git tag`](../branching-and-merging/tag.md)
- [`git stash`](../branching-and-merging/stash.md)
- [`git worktree`](../branching-and-merging/worktree.md)

## Fuente

- [git-switch - Switch branches](https://git-scm.com/docs/git-switch)
