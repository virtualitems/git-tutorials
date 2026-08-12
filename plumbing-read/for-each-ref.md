---
title: "git for-each-ref"
source: "https://git-scm.com/docs/git-for-each-ref"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git for-each-ref`

Este caso usa `git for-each-ref` para filtrar, ordenar y formatear referencias.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git for-each-ref --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
```

La invocación `git for-each-ref --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/` ejecuta esta operación: filtrar, ordenar y formatear referencias. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git for-each-ref [--count=<count>] [--shell|--perl|--python|--tcl]
		   [(--sort=<key>)…] [--format=<format>]
		   [--include-root-refs] [--points-at=<object>]
		   [--merged[=<object>]] [--no-merged[=<object>]]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git for-each-ref [<options>] [<pattern>]
   or: git for-each-ref [--points-at <object>]
   or: git for-each-ref [--merged [<commit>]] [--no-merged [<commit>]]
   or: git for-each-ref [--contains [<commit>]] [--no-contains [<commit>]]
   or: git for-each-ref [--start-after <marker>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git for-each-ref -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--count`

Establece un límite numérico para la selección o el recorrido.

```bash
git for-each-ref --count=5 --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shell` y `-s`

Activa shell durante filtrar, ordenar y formatear referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `quote placeholders suitably for shells`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--shell`

```bash
git for-each-ref --shell --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

### `--perl` y `-p`

Activa perl durante filtrar, ordenar y formatear referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `quote placeholders suitably for perl`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--perl`

```bash
git for-each-ref --perl --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

### `--python`

Activa python durante filtrar, ordenar y formatear referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `quote placeholders suitably for python`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git for-each-ref --python --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

### `--tcl`

Activa tcl durante filtrar, ordenar y formatear referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `quote placeholders suitably for Tcl`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git for-each-ref --tcl --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

### `--sort`

Ordena registros por el campo indicado.

```bash
git for-each-ref --sort=user.name --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `user.name` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--format`

Define los campos y separadores de la salida.

```bash
git for-each-ref --format=oneline --sort=-committerdate refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include-root-refs`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git for-each-ref --include-root-refs --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

### `--points-at`

Limita filtrar, ordenar y formatear referencias al alcance identificado por points at. En Git 2.51.1, la ayuda corta expresa el contrato como `print only refs which points at the given object`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git for-each-ref --points-at=HEAD --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--merged`

Filtra elementos ya alcanzables desde la revisión indicada.

```bash
git for-each-ref --merged=HEAD --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-merged`

Filtra elementos no alcanzables desde la revisión indicada.

```bash
git for-each-ref --no-merged --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

### `--contains`

Filtra referencias cuyo historial contiene el commit indicado.

```bash
git for-each-ref --contains=HEAD --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-contains`

Filtra referencias cuyo historial no contiene el commit indicado.

```bash
git for-each-ref --no-contains --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

### `--start-after`

Activa start after durante filtrar, ordenar y formatear referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `start iteration after the provided marker`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git for-each-ref --start-after=valor --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

### `--omit-empty`

Impide omit vacío durante esta invocación de `git for-each-ref`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not output a newline after empty formatted refs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git for-each-ref --omit-empty --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

### `--color`

Controla el uso de secuencias de color en la salida.

```bash
git for-each-ref --color=always --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `always` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude`

Excluye elementos que cumplan la condición indicada.

```bash
git for-each-ref --exclude=TODO --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-case`

Excluye elementos que cumplan la condición indicada.

```bash
git for-each-ref --ignore-case --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git for-each-ref` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git for-each-ref --stdin --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git for-each-repo`](../plumbing-read/for-each-repo.md)
- [`git diff-tree`](../plumbing-read/diff-tree.md)
- [`git format-rev`](../plumbing-read/format-rev.md)

## Fuente

- [git-for-each-ref - Output information on each ref](https://git-scm.com/docs/git-for-each-ref)
