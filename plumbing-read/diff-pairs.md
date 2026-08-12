---
title: "git diff-pairs"
source: "https://git-scm.com/docs/git-diff-pairs"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git diff-pairs`

Este caso usa `git diff-pairs` para comparar pares de blobs recibidos por la entrada estándar.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
printf '%s\0%s\0' "$blob_a" "$blob_b" | git diff-pairs -z
```

La invocación `git diff-pairs` ejecuta esta operación: comparar pares de blobs recibidos por la entrada estándar. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git diff-pairs -z [<diff-options>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git diff-pairs -z [<diff-options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git diff-pairs -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git diff-pairs -z
printf 'exit=%s\n' "$?"
```

### `-p` y `--patch`

Permite elegir hunks en vez de operar sobre el archivo completo.

#### Ejemplo con `--patch`

```bash
git diff-pairs --patch
printf 'exit=%s\n' "$?"
```

### `-s`

Suprime s en la salida de esta invocación de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `suppress diff output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs -s
printf 'exit=%s\n' "$?"
```

### `--no-patch`

Desactiva el comportamiento `patch` para esta invocación.

```bash
git diff-pairs --no-patch
printf 'exit=%s\n' "$?"
```

### `-u`

Genera u como parte del resultado de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate patch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs -u
printf 'exit=%s\n' "$?"
```

### `-U` y `--unified`

Define cuántas líneas de contexto rodean cada hunk.

#### Ejemplo con `--unified`

```bash
git diff-pairs --unified=5
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-W` y `--function-context`

Genera function context como parte del resultado de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diffs with <n> lines context`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--function-context`

```bash
git diff-pairs --function-context
printf 'exit=%s\n' "$?"
```

### `--raw`

Genera raw como parte del resultado de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate the diff in raw format`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --raw
printf 'exit=%s\n' "$?"
```

### `--patch-with-raw`

Selecciona la relación indicada por parche with raw; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `synonym for '-p --raw'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --patch-with-raw
printf 'exit=%s\n' "$?"
```

### `--patch-with-stat`

Selecciona la relación indicada por parche with estadísticas; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `synonym for '-p --stat'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --patch-with-stat
printf 'exit=%s\n' "$?"
```

### `--stat`

Selecciona la relación indicada por parche with estadísticas; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `synonym for '-p --stat'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git diff-pairs` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque parche with estadísticas actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git diff-pairs --stat
printf 'exit=%s\n' "$?"
```

### `--numstat`

Activa numstat durante comparar pares de blobs recibidos por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `machine friendly --stat`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --numstat
printf 'exit=%s\n' "$?"
```

### `--shortstat`

Limita comparar pares de blobs recibidos por la entrada estándar al alcance identificado por shortstat. En Git 2.51.1, la ayuda corta expresa el contrato como `output only the last line of --stat`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --shortstat
printf 'exit=%s\n' "$?"
```

### `-X` y `--dirstat`

Incluye dirstat en la salida o cambia cómo `git diff-pairs` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output the distribution of relative amount of changes for each sub-directory`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--dirstat`

```bash
git diff-pairs --dirstat=valor
printf 'exit=%s\n' "$?"
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--cumulative`

Selecciona la relación indicada por cumulative; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `synonym for --dirstat=cumulative`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --cumulative
printf 'exit=%s\n' "$?"
```

### `--dirstat-by-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

```bash
git diff-pairs --dirstat-by-file=valor
printf 'exit=%s\n' "$?"
```

### `--check`

Valida sin producir el efecto principal de la orden.

```bash
git diff-pairs --check
printf 'exit=%s\n' "$?"
```

### `--summary`

Activa summary durante comparar pares de blobs recibidos por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `condensed summary such as creations, renames and mode changes`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción selecciona el procedimiento que `git diff-pairs` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git diff-pairs --summary
printf 'exit=%s\n' "$?"
```

### `--name-only`

Muestra nombres de ruta sin el contenido del diff.

```bash
git diff-pairs --name-only
printf 'exit=%s\n' "$?"
```

### `--name-status`

Muestra nombres y estado de cada ruta.

```bash
git diff-pairs --name-status
printf 'exit=%s\n' "$?"
```

### `--stat-width`

Genera estadísticas width como parte del resultado de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diffstat with a given width`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --stat-width=100
printf 'exit=%s\n' "$?"
```

El ejemplo usa `100` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stat-name-width`

Genera estadísticas nombre width como parte del resultado de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diffstat with a given name width`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --stat-name-width=100
printf 'exit=%s\n' "$?"
```

El ejemplo usa `100` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stat-graph-width`

Genera estadísticas graph width como parte del resultado de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diffstat with a given graph width`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --stat-graph-width=100
printf 'exit=%s\n' "$?"
```

El ejemplo usa `100` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stat-count`

Establece un límite numérico para la selección o el recorrido.

```bash
git diff-pairs --stat-count=5
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--compact-summary`

Genera compact summary como parte del resultado de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate compact summary in diffstat`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --compact-summary
printf 'exit=%s\n' "$?"
```

### `--binary`

Incluye contenido binario en la salida o cambia cómo `git diff-pairs` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output a binary diff that can be applied`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --binary
printf 'exit=%s\n' "$?"
```

### `--full-index`

Incluye full índice en la salida o cambia cómo `git diff-pairs` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show full pre- and post-image object names on the "index" lines`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --full-index
printf 'exit=%s\n' "$?"
```

### `--color`

Controla el uso de secuencias de color en la salida.

```bash
git diff-pairs --color=always
printf 'exit=%s\n' "$?"
```

El ejemplo usa `always` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ws-error-highlight`

Activa ws error highlight durante comparar pares de blobs recibidos por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `highlight whitespace errors in the 'context', 'old' or 'new' lines in the diff`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --ws-error-highlight=all
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--abbrev`

Reduce la representación visible del identificador sin cambiar el objeto.

```bash
git diff-pairs --abbrev=5
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--src-prefix`

Incluye src prefix en la salida o cambia cómo `git diff-pairs` la representa.

```bash
git diff-pairs --src-prefix=refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `refs/heads/` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dst-prefix`

Incluye dst prefix en la salida o cambia cómo `git diff-pairs` la representa.

```bash
git diff-pairs --dst-prefix=refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `refs/heads/` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--line-prefix`

Antepone line prefix al valor que produce `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `prepend an additional prefix to every line of output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --line-prefix=refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `refs/heads/` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-prefix`

Desactiva el comportamiento `prefix` para esta invocación.

```bash
git diff-pairs --no-prefix
printf 'exit=%s\n' "$?"
```

### `--default-prefix`

Define default prefix para esta ejecución de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `use default prefixes a/ and b/`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --default-prefix
printf 'exit=%s\n' "$?"
```

### `--inter-hunk-context`

Fusiona hunks cercanos cuando la distancia no supera el límite indicado.

```bash
git diff-pairs --inter-hunk-context=5
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--output-indicator-new`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

```bash
git diff-pairs --output-indicator-new=valor
printf 'exit=%s\n' "$?"
```

### `--output-indicator-old`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

```bash
git diff-pairs --output-indicator-old=valor
printf 'exit=%s\n' "$?"
```

### `--output-indicator-context`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

```bash
git diff-pairs --output-indicator-context=valor
printf 'exit=%s\n' "$?"
```

### `-B` y `--break-rewrites`

Crea break rewrites como parte de comparar pares de blobs recibidos por la entrada estándar. En Git 2.51.1, la ayuda corta expresa el contrato como `break complete rewrite changes into pairs of delete and create`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--break-rewrites`

```bash
git diff-pairs --break-rewrites=5
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-M` y `--find-renames`

Controla detección o búsqueda de relaciones entre entradas.

La opción selecciona el procedimiento que `git diff-pairs` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `--find-renames`

```bash
git diff-pairs --find-renames=5
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-D` y `--irreversible-delete`

Retira elementos según las condiciones de la orden.

#### Ejemplo con `--irreversible-delete`

```bash
git diff-pairs --irreversible-delete
printf 'exit=%s\n' "$?"
```

### `-C` y `--find-copies`

Controla detección o búsqueda de relaciones entre entradas.

La opción selecciona el procedimiento que `git diff-pairs` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `--find-copies`

```bash
git diff-pairs --find-copies=5
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--find-copies-harder`

Controla detección o búsqueda de relaciones entre entradas.

La opción cambia cómo `git diff-pairs` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git diff-pairs --find-copies-harder
printf 'exit=%s\n' "$?"
```

### `--no-renames`

Desactiva el comportamiento `renames` para esta invocación.

La opción selecciona el procedimiento que `git diff-pairs` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git diff-pairs --no-renames
printf 'exit=%s\n' "$?"
```

### `--rename-empty`

Define renombre vacío para esta ejecución de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `use empty blobs as rename source`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --rename-empty
printf 'exit=%s\n' "$?"
```

### `--follow`

Continúa el historial de una ruta a través de un renombre cuando puede detectarlo.

Esta forma se usa cuando `git diff-pairs` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque seguir renombres actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git diff-pairs --follow
printf 'exit=%s\n' "$?"
```

### `-l`

Limita comparar pares de blobs recibidos por la entrada estándar al alcance identificado por l. En Git 2.51.1, la ayuda corta expresa el contrato como `prevent rename/copy detection if the number of rename/copy targets exceeds given limit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs -l 5
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--minimal`

Genera minimal como parte del resultado de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `produce the smallest possible diff`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --minimal
printf 'exit=%s\n' "$?"
```

### `-w` y `--ignore-all-space`

Excluye elementos que cumplan la condición indicada.

#### Ejemplo con `--ignore-all-space`

```bash
git diff-pairs --ignore-all-space
printf 'exit=%s\n' "$?"
```

### `-b` y `--ignore-space-change`

Excluye elementos que cumplan la condición indicada.

#### Ejemplo con `--ignore-space-change`

```bash
git diff-pairs --ignore-space-change
printf 'exit=%s\n' "$?"
```

### `--ignore-space-at-eol`

Excluye elementos que cumplan la condición indicada.

```bash
git diff-pairs --ignore-space-at-eol
printf 'exit=%s\n' "$?"
```

### `--ignore-cr-at-eol`

Excluye elementos que cumplan la condición indicada.

```bash
git diff-pairs --ignore-cr-at-eol
printf 'exit=%s\n' "$?"
```

### `--ignore-blank-lines`

Excluye elementos que cumplan la condición indicada.

```bash
git diff-pairs --ignore-blank-lines
printf 'exit=%s\n' "$?"
```

### `-I` y `--ignore-matching-lines`

Excluye elementos que cumplan la condición indicada.

#### Ejemplo con `--ignore-matching-lines`

```bash
git diff-pairs --ignore-matching-lines=TODO
printf 'exit=%s\n' "$?"
```

En esta forma, `TODO` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--indent-heuristic`

Activa indent heuristic durante comparar pares de blobs recibidos por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `heuristic to shift diff hunk boundaries for easy reading`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --indent-heuristic
printf 'exit=%s\n' "$?"
```

### `--patience`

Genera patience como parte del resultado de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diff using the "patience diff" algorithm`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción selecciona el procedimiento que `git diff-pairs` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git diff-pairs --patience
printf 'exit=%s\n' "$?"
```

### `--histogram`

Genera histogram como parte del resultado de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diff using the "histogram diff" algorithm`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción selecciona el procedimiento que `git diff-pairs` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git diff-pairs --histogram
printf 'exit=%s\n' "$?"
```

### `--diff-algorithm`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git diff-pairs` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git diff-pairs --diff-algorithm=sha256
printf 'exit=%s\n' "$?"
```

El ejemplo usa `sha256` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--anchored`

Genera anchored como parte del resultado de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate diff using the "anchored diff" algorithm`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción selecciona el procedimiento que `git diff-pairs` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git diff-pairs --anchored=valor
printf 'exit=%s\n' "$?"
```

### `--word-diff`

Incluye word diff en la salida o cambia cómo `git diff-pairs` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show word diff, using <mode> to delimit changed words`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --word-diff=all
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--word-diff-regex`

Define word diff regex para esta ejecución de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `use <regex> to decide what a word is`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --word-diff-regex=TODO
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--color-words`

Selecciona la relación indicada por color words; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `equivalent to --word-diff=color --word-diff-regex=<regex>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --color-words=TODO
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--color-moved`

Activa color moved durante comparar pares de blobs recibidos por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `moved lines of code are colored differently`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --color-moved=all
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--color-moved-ws`

Activa color moved ws durante comparar pares de blobs recibidos por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `how white spaces are ignored in --color-moved`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --color-moved-ws=all
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--relative`

Ejecuta relative durante comparar pares de blobs recibidos por la entrada estándar. En Git 2.51.1, la ayuda corta expresa el contrato como `when run from subdir, exclude changes outside and show relative paths`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --relative=refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `refs/heads/` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a` y `--text`

Procesa texto con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `treat all files as text`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--text`

```bash
git diff-pairs --text
printf 'exit=%s\n' "$?"
```

### `-R`

Activa R durante comparar pares de blobs recibidos por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `swap two inputs, reverse the diff`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git diff-pairs` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git diff-pairs -R
printf 'exit=%s\n' "$?"
```

### `--exit-code`

Activa exit code durante comparar pares de blobs recibidos por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `exit with 1 if there were differences, 0 otherwise`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --exit-code
printf 'exit=%s\n' "$?"
```

### `--quiet`

Reduce mensajes que no representan errores.

```bash
git diff-pairs --quiet
printf 'exit=%s\n' "$?"
```

### `--ext-diff`

Permite ext diff cuando la forma predeterminada de `git diff-pairs` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow an external diff helper to be executed`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --ext-diff
printf 'exit=%s\n' "$?"
```

### `--textconv`

Ejecuta textconv durante comparar pares de blobs recibidos por la entrada estándar. En Git 2.51.1, la ayuda corta expresa el contrato como `run external text conversion filters when comparing binary files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --textconv
printf 'exit=%s\n' "$?"
```

### `--ignore-submodules`

Excluye elementos que cumplan la condición indicada.

```bash
git diff-pairs --ignore-submodules=always
printf 'exit=%s\n' "$?"
```

El ejemplo usa `always` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--submodule`

Define submodule para esta ejecución de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `specify how differences in submodules are shown`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --submodule=oneline
printf 'exit=%s\n' "$?"
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ita-invisible-in-index`

Incluye ita invisible in índice en la entrada, el resultado o el registro que construye `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `hide 'git add -N' entries from the index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --ita-invisible-in-index
printf 'exit=%s\n' "$?"
```

### `-N`

Activa N durante comparar pares de blobs recibidos por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git diff-pairs -N
printf 'exit=%s\n' "$?"
```

### `--ita-visible-in-index`

Incluye ita visible in índice en la entrada, el resultado o el registro que construye `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `treat 'git add -N' entries as real in the index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --ita-visible-in-index
printf 'exit=%s\n' "$?"
```

### `-S`

Activa S durante comparar pares de blobs recibidos por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `look for differences that change the number of occurrences of the specified string`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs -S valor
printf 'exit=%s\n' "$?"
```

### `-G`

Activa G durante comparar pares de blobs recibidos por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `look for differences that change the number of occurrences of the specified regex`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs -G TODO
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pickaxe-all`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git diff-pairs --pickaxe-all
printf 'exit=%s\n' "$?"
```

### `--pickaxe-regex`

Procesa pickaxe regex con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `treat <string> in -S as extended POSIX regular expression`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --pickaxe-regex
printf 'exit=%s\n' "$?"
```

### `-O`

Incluye O en la salida o cambia cómo `git diff-pairs` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `control the order in which files appear in the output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs -O rutas.txt
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--rotate-to`

Incluye rotate to en la salida o cambia cómo `git diff-pairs` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show the change in the specified path first`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --rotate-to=archivo.txt
printf 'exit=%s\n' "$?"
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--skip-to`

Incluye omitir el elemento actual to en la salida o cambia cómo `git diff-pairs` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `skip the output to the specified path`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git diff-pairs` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque omitir el elemento actual to actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git diff-pairs --skip-to=archivo.txt
printf 'exit=%s\n' "$?"
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--find-object`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git diff-pairs --find-object=HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--diff-filter`

Define diff filtro para esta ejecución de `git diff-pairs`. En Git 2.51.1, la ayuda corta expresa el contrato como `select files by diff type`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-pairs --diff-filter=valor
printf 'exit=%s\n' "$?"
```

### `--output`

Escribe el resultado en la ruta indicada.

```bash
git diff-pairs --output=rutas.txt
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-color`

Desactiva para esta invocación el comportamiento que habilita `--color`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git diff-pairs --no-color
printf 'exit=%s\n' "$?"
```

### `--no-rename-empty`

Desactiva para esta invocación el comportamiento que habilita `--rename-empty`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git diff-pairs --no-rename-empty
printf 'exit=%s\n' "$?"
```

### `--no-indent-heuristic`

Desactiva para esta invocación el comportamiento que habilita `--indent-heuristic`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git diff-pairs --no-indent-heuristic
printf 'exit=%s\n' "$?"
```

### `--no-color-moved`

Desactiva para esta invocación el comportamiento que habilita `--color-moved`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git diff-pairs --no-color-moved
printf 'exit=%s\n' "$?"
```

### `--no-color-moved-ws`

Desactiva para esta invocación el comportamiento que habilita `--color-moved-ws`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git diff-pairs --no-color-moved-ws
printf 'exit=%s\n' "$?"
```

### `--no-relative`

Desactiva para esta invocación el comportamiento que habilita `--relative`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git diff-pairs --no-relative
printf 'exit=%s\n' "$?"
```

### `--no-text`

Desactiva para esta invocación el comportamiento que habilita `--text`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git diff-pairs --no-text
printf 'exit=%s\n' "$?"
```

### `--no-ext-diff`

Desactiva para esta invocación el comportamiento que habilita `--ext-diff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git diff-pairs --no-ext-diff
printf 'exit=%s\n' "$?"
```

### `--no-textconv`

Desactiva para esta invocación el comportamiento que habilita `--textconv`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git diff-pairs --no-textconv
printf 'exit=%s\n' "$?"
```

### `--diff-merges`, `--no-diff-merges`, `--cc`, `--dd` y `--remerge-diff`

`--diff-merges=<formato>` controla el diff de los commits de fusión. Acepta `off`/`none`, `on`/`m`, `first-parent`/`1`, `separate`/`m`, `combined`/`c`, `dense-combined`/`cc` y `remerge`/`r`. `--no-diff-merges` equivale a `off`; `--cc`, `--dd` y `--remerge-diff` son atajos para `dense-combined -p`, `first-parent -p` y `remerge -p`.

```bash
git show --diff-merges=dense-combined --patch <commit-de-fusión>
git show --remerge-diff <commit-de-fusión>
```

`remerge` vuelve a fusionar temporalmente los dos padres y compara ese árbol, que puede contener marcadores de conflicto, con el commit real. Su formato de salida puede cambiar entre versiones.

### `--combined-all-paths`

En un diff combinado, muestra el nombre de la ruta en cada padre. Solo produce efecto con `--diff-merges=combined` o `dense-combined`, y resulta relevante cuando se detectan renombres o copias.

```bash
git show --diff-merges=combined --combined-all-paths \
  --find-renames <commit-de-fusión>
```

## Páginas relacionadas

- [`git diff-tree`](../plumbing-read/diff-tree.md)
- [`git diff-index`](../plumbing-read/diff-index.md)
- [`git for-each-ref`](../plumbing-read/for-each-ref.md)

## Fuente

- [git-diff-pairs - Compare the content and mode of provided blob pairs](https://git-scm.com/docs/git-diff-pairs)
