---
title: "git range-diff"
source: "https://git-scm.com/docs/git-range-diff"
section: "inspection-and-comparison"
status: "source-audited"
version: "2.55.0"
---

# `git range-diff`

Este caso usa `git range-diff` para comparar dos versiones de una serie de commits.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Ejemplo mínimo

```bash
git range-diff main..tema-v1 main..tema-v2
```

La invocación `git range-diff main..tema-v1 main..tema-v2` ejecuta esta operación: comparar dos versiones de una serie de commits. Después, la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Sintaxis y formas de invocación

```text
git range-diff [--color=[<when>]] [--no-color] [<diff-options>]
	[--no-dual-color] [--creation-factor=<factor>]
	[--left-only | --right-only] [--diff-merges=<format>]
	[--remerge-diff] [--no-notes | --notes[=<ref>]]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git range-diff [<options>] <old-base>..<old-tip> <new-base>..<new-tip>
   or: git range-diff [<options>] <old-tip>...<new-tip>
   or: git range-diff [<options>] <base> <old-tip> <new-tip>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git range-diff -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--color`

Controla el uso de secuencias de color en la salida.

```bash
git range-diff --color=always main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `always` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-color`

Desactiva secuencias de color.

```bash
git range-diff --no-color main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--no-dual-color`

Desactiva el comportamiento `dual-color` para esta invocación.

```bash
git range-diff --no-dual-color main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--creation-factor`

Activa creation factor durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `percentage by which creation is weighted`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --creation-factor=5 main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--left-only`

Limita comparar dos versiones de una serie de commits al alcance identificado por left only. En Git 2.51.1, la ayuda corta expresa el contrato como `only emit output related to the first range`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --left-only main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--right-only`

Limita comparar dos versiones de una serie de commits al alcance identificado por right only. En Git 2.51.1, la ayuda corta expresa el contrato como `only emit output related to the second range`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --right-only main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--diff-merges`

Activa diff merges durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `passed to 'git log'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --diff-merges=short main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--remerge-diff`

Activa remerge diff durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `passed to 'git log'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --remerge-diff main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--no-notes`

Desactiva el comportamiento `notes` para esta invocación.

```bash
git range-diff --no-notes main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--notes`

Activa notas durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `passed to 'git log'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --notes=valor main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--dual-color`

Selecciona la relación indicada por dual color; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-dual-color`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --dual-color main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-p` y `--patch`

Permite elegir hunks en vez de operar sobre el archivo completo.

#### Ejemplo con `--patch`

```bash
git range-diff --patch main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-s`

Suprime s en la salida de esta invocación de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `suppress diff output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff -s main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-u`

Genera u como parte del resultado de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate patch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff -u main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-U` y `--unified`

Define cuántas líneas de contexto rodean cada hunk.

#### Ejemplo con `--unified`

```bash
git range-diff --unified=5 main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-W` y `--function-context`

Genera function context como parte del resultado de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diffs with <n> lines context`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--function-context`

```bash
git range-diff --function-context main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--raw`

Genera raw como parte del resultado de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate the diff in raw format`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --raw main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--patch-with-raw`

Selecciona la relación indicada por parche with raw; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `synonym for '-p --raw'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --patch-with-raw main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--patch-with-stat`

Selecciona la relación indicada por parche with estadísticas; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `synonym for '-p --stat'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --patch-with-stat main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--stat`

Selecciona la relación indicada por parche with estadísticas; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `synonym for '-p --stat'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git range-diff` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque parche with estadísticas actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git range-diff --stat main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--numstat`

Activa numstat durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `machine friendly --stat`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --numstat main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--shortstat`

Limita comparar dos versiones de una serie de commits al alcance identificado por shortstat. En Git 2.51.1, la ayuda corta expresa el contrato como `output only the last line of --stat`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --shortstat main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-X` y `--dirstat`

Incluye dirstat en la salida o cambia cómo `git range-diff` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output the distribution of relative amount of changes for each sub-directory`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--dirstat`

```bash
git range-diff --dirstat=valor main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--cumulative`

Selecciona la relación indicada por cumulative; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `synonym for --dirstat=cumulative`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --cumulative main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--dirstat-by-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

```bash
git range-diff --dirstat-by-file=valor main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--check`

Valida sin producir el efecto principal de la orden.

```bash
git range-diff --check main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--summary`

Activa summary durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `condensed summary such as creations, renames and mode changes`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción selecciona el procedimiento que `git range-diff` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git range-diff --summary main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--name-only`

Muestra nombres de ruta sin el contenido del diff.

```bash
git range-diff --name-only main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--name-status`

Muestra nombres y estado de cada ruta.

```bash
git range-diff --name-status main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--stat-width`

Genera estadísticas width como parte del resultado de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diffstat with a given width`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --stat-width=100 main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `100` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stat-name-width`

Genera estadísticas nombre width como parte del resultado de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diffstat with a given name width`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --stat-name-width=100 main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `100` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stat-graph-width`

Genera estadísticas graph width como parte del resultado de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diffstat with a given graph width`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --stat-graph-width=100 main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `100` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stat-count`

Establece un límite numérico para la selección o el recorrido.

```bash
git range-diff --stat-count=5 main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--compact-summary`

Genera compact summary como parte del resultado de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate compact summary in diffstat`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --compact-summary main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--binary`

Incluye contenido binario en la salida o cambia cómo `git range-diff` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output a binary diff that can be applied`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --binary main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--full-index`

Incluye full índice en la salida o cambia cómo `git range-diff` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show full pre- and post-image object names on the "index" lines`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --full-index main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--ws-error-highlight`

Activa ws error highlight durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `highlight whitespace errors in the 'context', 'old' or 'new' lines in the diff`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --ws-error-highlight=all main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git range-diff -z main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--abbrev`

Reduce la representación visible del identificador sin cambiar el objeto.

```bash
git range-diff --abbrev=5 main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--src-prefix`

Incluye src prefix en la salida o cambia cómo `git range-diff` la representa.

```bash
git range-diff --src-prefix=refs/heads/ main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `refs/heads/` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dst-prefix`

Incluye dst prefix en la salida o cambia cómo `git range-diff` la representa.

```bash
git range-diff --dst-prefix=refs/heads/ main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `refs/heads/` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--line-prefix`

Antepone line prefix al valor que produce `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `prepend an additional prefix to every line of output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --line-prefix=refs/heads/ main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `refs/heads/` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--default-prefix`

Define default prefix para esta ejecución de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `use default prefixes a/ and b/`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --default-prefix main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--inter-hunk-context`

Fusiona hunks cercanos cuando la distancia no supera el límite indicado.

```bash
git range-diff --inter-hunk-context=5 main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--output-indicator-new`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

```bash
git range-diff --output-indicator-new=valor main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--output-indicator-old`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

```bash
git range-diff --output-indicator-old=valor main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--output-indicator-context`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

```bash
git range-diff --output-indicator-context=valor main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-B` y `--break-rewrites`

Crea break rewrites como parte de comparar dos versiones de una serie de commits. En Git 2.51.1, la ayuda corta expresa el contrato como `break complete rewrite changes into pairs of delete and create`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--break-rewrites`

```bash
git range-diff --break-rewrites=5 main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-M` y `--find-renames`

Controla detección o búsqueda de relaciones entre entradas.

La opción selecciona el procedimiento que `git range-diff` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `--find-renames`

```bash
git range-diff --find-renames=5 main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-D` y `--irreversible-delete`

Retira elementos según las condiciones de la orden.

#### Ejemplo con `--irreversible-delete`

```bash
git range-diff --irreversible-delete main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-C` y `--find-copies`

Controla detección o búsqueda de relaciones entre entradas.

La opción selecciona el procedimiento que `git range-diff` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `--find-copies`

```bash
git range-diff --find-copies=5 main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--find-copies-harder`

Controla detección o búsqueda de relaciones entre entradas.

La opción cambia cómo `git range-diff` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git range-diff --find-copies-harder main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--rename-empty`

Define renombre vacío para esta ejecución de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `use empty blobs as rename source`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --rename-empty main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--follow`

Continúa el historial de una ruta a través de un renombre cuando puede detectarlo.

Esta forma se usa cuando `git range-diff` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque seguir renombres actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git range-diff --follow main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-l`

Limita comparar dos versiones de una serie de commits al alcance identificado por l. En Git 2.51.1, la ayuda corta expresa el contrato como `prevent rename/copy detection if the number of rename/copy targets exceeds given limit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff -l 5 main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--minimal`

Genera minimal como parte del resultado de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `produce the smallest possible diff`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --minimal main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-w` y `--ignore-all-space`

Excluye elementos que cumplan la condición indicada.

#### Ejemplo con `--ignore-all-space`

```bash
git range-diff --ignore-all-space main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-b` y `--ignore-space-change`

Excluye elementos que cumplan la condición indicada.

#### Ejemplo con `--ignore-space-change`

```bash
git range-diff --ignore-space-change main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--ignore-space-at-eol`

Excluye elementos que cumplan la condición indicada.

```bash
git range-diff --ignore-space-at-eol main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--ignore-cr-at-eol`

Excluye elementos que cumplan la condición indicada.

```bash
git range-diff --ignore-cr-at-eol main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--ignore-blank-lines`

Excluye elementos que cumplan la condición indicada.

```bash
git range-diff --ignore-blank-lines main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-I` y `--ignore-matching-lines`

Excluye elementos que cumplan la condición indicada.

#### Ejemplo con `--ignore-matching-lines`

```bash
git range-diff --ignore-matching-lines=TODO main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

En esta forma, `TODO` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--indent-heuristic`

Activa indent heuristic durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `heuristic to shift diff hunk boundaries for easy reading`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --indent-heuristic main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--patience`

Genera patience como parte del resultado de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diff using the "patience diff" algorithm`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción selecciona el procedimiento que `git range-diff` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git range-diff --patience main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--histogram`

Genera histogram como parte del resultado de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diff using the "histogram diff" algorithm`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción selecciona el procedimiento que `git range-diff` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git range-diff --histogram main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--diff-algorithm`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git range-diff` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git range-diff --diff-algorithm=sha256 main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `sha256` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--anchored`

Genera anchored como parte del resultado de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diff using the "anchored diff" algorithm`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción selecciona el procedimiento que `git range-diff` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git range-diff --anchored=valor main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--word-diff`

Incluye word diff en la salida o cambia cómo `git range-diff` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show word diff, using <mode> to delimit changed words`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --word-diff=all main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--word-diff-regex`

Define word diff regex para esta ejecución de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `use <regex> to decide what a word is`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --word-diff-regex=TODO main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--color-words`

Selecciona la relación indicada por color words; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `equivalent to --word-diff=color --word-diff-regex=<regex>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --color-words=TODO main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--color-moved`

Activa color moved durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `moved lines of code are colored differently`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --color-moved=all main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--color-moved-ws`

Activa color moved ws durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `how white spaces are ignored in --color-moved`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --color-moved-ws=all main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--relative`

Ejecuta relative durante comparar dos versiones de una serie de commits. En Git 2.51.1, la ayuda corta expresa el contrato como `when run from subdir, exclude changes outside and show relative paths`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --relative=refs/heads/ main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `refs/heads/` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a` y `--text`

Procesa texto con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `treat all files as text`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--text`

```bash
git range-diff --text main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-R`

Activa R durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `swap two inputs, reverse the diff`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git range-diff` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git range-diff -R main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--exit-code`

Activa exit code durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `exit with 1 if there were differences, 0 otherwise`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --exit-code main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--quiet`

Reduce mensajes que no representan errores.

```bash
git range-diff --quiet main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--ext-diff`

Permite ext diff cuando la forma predeterminada de `git range-diff` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow an external diff helper to be executed`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --ext-diff main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--textconv`

Ejecuta textconv durante comparar dos versiones de una serie de commits. En Git 2.51.1, la ayuda corta expresa el contrato como `run external text conversion filters when comparing binary files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --textconv main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--ignore-submodules`

Excluye elementos que cumplan la condición indicada.

```bash
git range-diff --ignore-submodules=always main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `always` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--submodule`

Define submodule para esta ejecución de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `specify how differences in submodules are shown`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --submodule=oneline main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ita-invisible-in-index`

Incluye ita invisible in índice en la entrada, el resultado o el registro que construye `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `hide 'git add -N' entries from the index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --ita-invisible-in-index main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-N`

Activa N durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git range-diff -N main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--ita-visible-in-index`

Incluye ita visible in índice en la entrada, el resultado o el registro que construye `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `treat 'git add -N' entries as real in the index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --ita-visible-in-index main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-S`

Activa S durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `look for differences that change the number of occurrences of the specified string`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff -S valor main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-G`

Activa G durante comparar dos versiones de una serie de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `look for differences that change the number of occurrences of the specified regex`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff -G TODO main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pickaxe-all`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git range-diff --pickaxe-all main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--pickaxe-regex`

Procesa pickaxe regex con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `treat <string> in -S as extended POSIX regular expression`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --pickaxe-regex main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `-O`

Incluye O en la salida o cambia cómo `git range-diff` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `control the order in which files appear in the output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff -O rutas.txt main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--rotate-to`

Incluye rotate to en la salida o cambia cómo `git range-diff` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show the change in the specified path first`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --rotate-to=archivo.txt main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--skip-to`

Incluye omitir el elemento actual to en la salida o cambia cómo `git range-diff` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `skip the output to the specified path`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git range-diff` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque omitir el elemento actual to actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git range-diff --skip-to=archivo.txt main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--find-object`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git range-diff --find-object=HEAD main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--diff-filter`

Define diff filtro para esta ejecución de `git range-diff`. En Git 2.51.1, la ayuda corta expresa el contrato como `select files by diff type`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git range-diff --diff-filter=valor main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

### `--output`

Escribe el resultado en la ruta indicada.

```bash
git range-diff --output=rutas.txt main..tema-v1 main..tema-v2
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git shortlog`](../inspection-and-comparison/shortlog.md)
- [`git log`](../inspection-and-comparison/log.md)
- [`git show`](../inspection-and-comparison/show.md)

## Fuente

- [git-range-diff - Compare two commit ranges (e.g. two versions of a branch)](https://git-scm.com/docs/git-range-diff)
