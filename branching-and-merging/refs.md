---
title: "git refs"
source: "https://git-scm.com/docs/git-refs"
section: "branching-and-merging"
status: "source-audited"
version: "2.55.0"
---

# `git refs`

Este caso usa `git refs` para consultar y modificar referencias mediante transacciones.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git refs list refs/heads
git refs verify --strict
```

La invocación `git refs list refs/heads` ejecuta esta operación: consultar y modificar referencias mediante transacciones. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Sintaxis y formas de invocación

```text
git refs migrate --ref-format=<format> [--no-reflog] [--dry-run]
git refs verify [--strict] [--verbose]
git refs list [--count=<count>] [--shell|--perl|--python|--tcl]
		   [(--sort=<key>)…] [--format=<format>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git refs migrate --ref-format=<format> [--no-reflog] [--dry-run]
   or: git refs verify [--strict] [--verbose]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git refs -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--ref-format`

Selecciona el formato de almacenamiento de referencias que usará el repositorio.

```bash
git refs --ref-format list refs/heads
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reflog`

Desactiva el comportamiento `reflog` para esta invocación.

```bash
git refs --no-reflog list refs/heads
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

```bash
git refs --dry-run list refs/heads
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--strict`

Activa strict durante consultar y modificar referencias mediante transacciones. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git refs --strict list refs/heads
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verbose`

Aumenta el detalle enviado a la salida.

```bash
git refs --verbose list refs/heads
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--count`

Establece un límite numérico para la selección o el recorrido.

```bash
git refs --count list refs/heads
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shell`

Activa shell durante consultar y modificar referencias mediante transacciones. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git refs --shell list refs/heads
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--perl`

Activa perl durante consultar y modificar referencias mediante transacciones. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git refs --perl list refs/heads
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--python`

Activa python durante consultar y modificar referencias mediante transacciones. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git refs --python list refs/heads
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tcl`

Activa tcl durante consultar y modificar referencias mediante transacciones. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git refs --tcl list refs/heads
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sort`

Ordena registros por el campo indicado.

```bash
git refs --sort list refs/heads
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--format`

Define los campos y separadores de la salida.

```bash
git refs --format list refs/heads
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reflog` y `--no-reflog`

En `git refs migrate`, seleccionan si la migración conserva o descarta los reflogs. `--reflog` es el valor predeterminado.

```bash
git refs migrate --ref-format=reftable --dry-run --reflog
```

`--dry-run` prepara la migración sin ejecutarla. Repite primero esta comprobación y conserva una copia del repositorio antes de cambiar el backend de referencias.

## Páginas relacionadas

- [`git rerere`](../branching-and-merging/rerere.md)
- [`git merge-tree`](../branching-and-merging/merge-tree.md)
- [`git stash`](../branching-and-merging/stash.md)

## Fuente

- [git-refs - Low-level access to refs](https://git-scm.com/docs/git-refs)
