---
title: "git show-branch"
source: "https://git-scm.com/docs/git-show-branch"
section: "inspection-and-comparison"
status: "source-audited"
version: "2.55.0"
---

# `git show-branch`

Este caso usa `git show-branch` para comparar el desarrollo representado por varias ramas.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Ejemplo mínimo

```bash
git show-branch main tema-portada
```

La invocación `git show-branch main tema-portada` ejecuta esta operación: comparar el desarrollo representado por varias ramas. Después, la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Sintaxis y formas de invocación

```text
git show-branch [-a | --all] [-r | --remotes] [--topo-order | --date-order]
		[--current] [--color[=<when>] | --no-color] [--sparse]
		[--more=<n> | --list | --independent | --merge-base]
		[--no-name | --sha1-name] [--topics]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git show-branch [-a | --all] [-r | --remotes] [--topo-order | --date-order]
                       [--current] [--color[=<when>] | --no-color] [--sparse]
                       [--more=<n> | --list | --independent | --merge-base]
                       [--no-name | --sha1-name] [--topics]
                       [(<rev> | <glob>)...]
   or: git show-branch (-g | --reflog)[=<n>[,<base>]] [--list] [<ref>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git show-branch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-a` y `--all`

Amplía la selección a todos los elementos del alcance definido.

#### Ejemplo con `--all`

```bash
git show-branch --all main tema-portada
printf 'exit=%s\n' "$?"
```

### `-r` y `--remotes`

Incluye remotes en la salida o cambia cómo `git show-branch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show remote-tracking branches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--remotes`

```bash
git show-branch --remotes main tema-portada
printf 'exit=%s\n' "$?"
```

### `--topo-order`

Incluye topo order en la salida o cambia cómo `git show-branch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show commits in topological order`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git show-branch --topo-order main tema-portada
printf 'exit=%s\n' "$?"
```

### `--date-order`

Aplica una fecha, duración o política de vencimiento.

```bash
git show-branch --date-order main tema-portada
printf 'exit=%s\n' "$?"
```

### `--current`

Incluye actual en la entrada, el resultado o el registro que construye `git show-branch`. En Git 2.51.1, la ayuda corta expresa el contrato como `include the current branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git show-branch --current main tema-portada
printf 'exit=%s\n' "$?"
```

### `--color`

Controla el uso de secuencias de color en la salida.

```bash
git show-branch --color=always main tema-portada
printf 'exit=%s\n' "$?"
```

El ejemplo usa `always` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-color`

Desactiva secuencias de color.

```bash
git show-branch --no-color main tema-portada
printf 'exit=%s\n' "$?"
```

### `--sparse`

Permite operar sobre entradas que quedan fuera de la selección sparse activa.

```bash
git show-branch --sparse main tema-portada
printf 'exit=%s\n' "$?"
```

### `--more`

Incluye more en la salida o cambia cómo `git show-branch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show <n> more commits after the common ancestor`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git show-branch --more=5 main tema-portada
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--list`

Incluye información adicional en la salida.

```bash
git show-branch --list main tema-portada
printf 'exit=%s\n' "$?"
```

### `--independent`

Incluye independent en la salida o cambia cómo `git show-branch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show refs unreachable from any other ref`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git show-branch --independent main tema-portada
printf 'exit=%s\n' "$?"
```

### `--merge-base`

Incluye merge base en la salida o cambia cómo `git show-branch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show possible merge bases`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git show-branch --merge-base main tema-portada
printf 'exit=%s\n' "$?"
```

### `--no-name`

Desactiva el comportamiento `name` para esta invocación.

```bash
git show-branch --no-name main tema-portada
printf 'exit=%s\n' "$?"
```

### `--sha1-name`

Activa sha1 nombre durante comparar el desarrollo representado por varias ramas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `name commits with their object names`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git show-branch --sha1-name main tema-portada
printf 'exit=%s\n' "$?"
```

### `--topics`

Limita comparar el desarrollo representado por varias ramas al alcance identificado por topics. En Git 2.51.1, la ayuda corta expresa el contrato como `show only commits not on the first branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git show-branch --topics main tema-portada
printf 'exit=%s\n' "$?"
```

### `-g` y `--reflog`

Incluye reflog en la salida o cambia cómo `git show-branch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show <n> most recent ref-log entries starting at base`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--reflog`

```bash
git show-branch --reflog=5 main tema-portada
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--name`

Selecciona la relación indicada por nombre; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-name`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git show-branch --name main tema-portada
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git verify-commit`](../inspection-and-comparison/verify-commit.md)
- [`git show`](../inspection-and-comparison/show.md)
- [`git verify-tag`](../inspection-and-comparison/verify-tag.md)

## Fuente

- [git-show-branch - Show branches and their commits](https://git-scm.com/docs/git-show-branch)
