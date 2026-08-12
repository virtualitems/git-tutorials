---
title: "git grep"
source: "https://git-scm.com/docs/git-grep"
section: "debugging"
status: "source-audited"
version: "2.55.0"
---

# `git grep`

Este caso usa `git grep` para buscar texto en archivos del área de trabajo o de un árbol.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La búsqueda combina revisiones, rutas y contenido. Primero delimita el conjunto de commits o archivos; después interpreta la evidencia que devuelve Git.

Reduce primero el rango y las rutas. Después interpreta cada coincidencia dentro de ese conjunto, sin atribuir significado a elementos que quedaron fuera.

## Ejemplo mínimo

```bash
git grep -n "TODO" -- '*.js'
```

La invocación `git grep -n "TODO" -- '*.js'` ejecuta esta operación: buscar texto en archivos del área de trabajo o de un árbol. Después, la salida identifica líneas, archivos o commits que cumplen el criterio.

## Sintaxis y formas de invocación

```text
git grep [-a | --text] [-I] [--textconv] [-i | --ignore-case] [-w | --word-regexp]
	   [-v | --invert-match] [-h|-H] [--full-name]
	   [-E | --extended-regexp] [-G | --basic-regexp]
	   [-P | --perl-regexp]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git grep [<options>] [-e] <pattern> [<rev>...] [[--] <path>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git grep -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-a` y `--text`

Procesa texto con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `process binary files as text`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git grep` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `--text`

```bash
git grep --text -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-I`

Impide I durante esta invocación de `git grep`. En Git 2.51.1, la ayuda corta expresa el contrato como `don't match patterns in binary files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git grep` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git grep -I -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--textconv`

Procesa textconv con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `process binary files with textconv filters`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git grep --textconv -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-i` y `--ignore-case`

Excluye elementos que cumplan la condición indicada.

#### Ejemplo con `--ignore-case`

```bash
git grep --ignore-case -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-w` y `--word-regexp`

Limita buscar texto en archivos del área de trabajo o de un árbol al alcance identificado por word regexp. En Git 2.51.1, la ayuda corta expresa el contrato como `match patterns only at word boundaries`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--word-regexp`

```bash
git grep --word-regexp -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-v` y `--invert-match`

Incluye invert match en la salida o cambia cómo `git grep` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show non-matching lines`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--invert-match`

```bash
git grep --invert-match -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-h`

Muestra ayuda corta cuando la orden admite esta convención.

```bash
git grep -h
printf 'exit=%s\n' "$?"
```

### `-H`

Incluye H en la salida o cambia cómo `git grep` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show filenames`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git grep -H -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--full-name`

Incluye full nombre en la salida o cambia cómo `git grep` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show filenames relative to top directory`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git grep --full-name -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-E` y `--extended-regexp`

Define extended regexp para esta ejecución de `git grep`. En Git 2.51.1, la ayuda corta expresa el contrato como `use extended POSIX regular expressions`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--extended-regexp`

```bash
git grep --extended-regexp -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-G` y `--basic-regexp`

Define basic regexp para esta ejecución de `git grep`. En Git 2.51.1, la ayuda corta expresa el contrato como `use basic POSIX regular expressions (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--basic-regexp`

```bash
git grep --basic-regexp -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-P` y `--perl-regexp`

Define perl regexp para esta ejecución de `git grep`. En Git 2.51.1, la ayuda corta expresa el contrato como `use Perl-compatible regular expressions`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--perl-regexp`

```bash
git grep --perl-regexp -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-e`

Activa e durante buscar texto en archivos del área de trabajo o de un árbol. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `match <pattern>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git grep -e TODO -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cached`

Usa el índice como origen o destino, sin tratar el área de trabajo de la misma forma.

```bash
git grep --cached -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--no-index`

Desactiva el comportamiento `index` para esta invocación.

```bash
git grep --no-index -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--index`

Incluye el índice en la operación.

```bash
git grep --index -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--untracked`

Activa untracked durante buscar texto en archivos del área de trabajo o de un árbol. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `search in both tracked and untracked files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git grep` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git grep --untracked -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--exclude-standard`

Excluye elementos que cumplan la condición indicada.

```bash
git grep --exclude-standard -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

```bash
git grep --recurse-submodules -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-r` y `--recursive`

Extiende la operación de forma recursiva al ámbito documentado.

#### Ejemplo con `--recursive`

```bash
git grep --recursive -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--max-depth`

Establece un límite numérico para la selección o el recorrido.

```bash
git grep --max-depth=5 -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-F` y `--fixed-strings`

Activa fixed strings durante buscar texto en archivos del área de trabajo o de un árbol. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `interpret patterns as fixed strings`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--fixed-strings`

```bash
git grep --fixed-strings -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-n` y `--line-number`

Incluye line number en la salida o cambia cómo `git grep` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show line numbers`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--line-number`

```bash
git grep --line-number "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--column`

Incluye column en la salida o cambia cómo `git grep` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show column number of first match`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git grep --column -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-l` y `--files-with-matches`

Limita buscar texto en archivos del área de trabajo o de un árbol al alcance identificado por files with matches. En Git 2.51.1, la ayuda corta expresa el contrato como `show only filenames instead of matching lines`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--files-with-matches`

```bash
git grep --files-with-matches -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--name-only`

Muestra nombres de ruta sin el contenido del diff.

```bash
git grep --name-only -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-L` y `--files-without-match`

Limita buscar texto en archivos del área de trabajo o de un árbol al alcance identificado por files without match. En Git 2.51.1, la ayuda corta expresa el contrato como `show only the names of files without match`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--files-without-match`

```bash
git grep --files-without-match -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-z` y `--null`

Usa NUL como terminador para conservar cualquier byte válido de un nombre.

#### Ejemplo con `--null`

```bash
git grep --null -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-o` y `--only-matching`

Limita buscar texto en archivos del área de trabajo o de un árbol al alcance identificado por only matching. En Git 2.51.1, la ayuda corta expresa el contrato como `show only matching parts of a line`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--only-matching`

```bash
git grep --only-matching -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-c` y `--count`

Establece un límite numérico para la selección o el recorrido.

#### Ejemplo con `--count`

```bash
git grep --count -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--color`

Controla el uso de secuencias de color en la salida.

```bash
git grep --color=always -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

El ejemplo usa `always` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--break`

Incluye break en la salida o cambia cómo `git grep` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print empty line between matches from different files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git grep --break -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--heading`

Limita buscar texto en archivos del área de trabajo o de un árbol al alcance identificado por heading. En Git 2.51.1, la ayuda corta expresa el contrato como `show filename only once above matches from same file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git grep --heading -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-C` y `--context`

Incluye context en la salida o cambia cómo `git grep` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show <n> context lines before and after matches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--context`

```bash
git grep --context=5 -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-B` y `--before-context`

Incluye before context en la salida o cambia cómo `git grep` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show <n> context lines before matches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--before-context`

```bash
git grep --before-context=5 -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-A` y `--after-context`

Incluye after context en la salida o cambia cómo `git grep` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show <n> context lines after matches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--after-context`

```bash
git grep --after-context=5 -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--threads`

Define threads para esta ejecución de `git grep`. En Git 2.51.1, la ayuda corta expresa el contrato como `use <n> worker threads`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git grep --threads=5 -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p` y `--show-function`

Incluye información adicional en la salida.

#### Ejemplo con `--show-function`

```bash
git grep --show-function -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-W` y `--function-context`

Incluye function context en la salida o cambia cómo `git grep` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show the surrounding function`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--function-context`

```bash
git grep --function-context -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-f`

Lee f como parte de la entrada de `git grep`. En Git 2.51.1, la ayuda corta expresa el contrato como `read patterns from file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git grep` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git grep -f rutas.txt -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--and`

Activa and durante buscar texto en archivos del área de trabajo o de un árbol. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `combine patterns specified with -e`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git grep --and -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--or`

Activa or durante buscar texto en archivos del área de trabajo o de un árbol. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git grep --or -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--not`

Activa not durante buscar texto en archivos del área de trabajo o de un árbol. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `(`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git grep --not -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git grep --quiet -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--all-match`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git grep --all-match -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-O` y `--open-files-in-pager`

Incluye open files in pager en la salida o cambia cómo `git grep` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show matching files in the pager`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--open-files-in-pager`

```bash
git grep --open-files-in-pager=5 -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--ext-grep`

Permite ext grep cuando la forma predeterminada de `git grep` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow calling of grep(1) (ignored by this build)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git grep --ext-grep -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `-m` y `--max-count`

Limita el número de registros producidos.

#### Ejemplo con `--max-count`

```bash
git grep --max-count=5 -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--no-text`

Desactiva para esta invocación el comportamiento que habilita `--text`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git grep` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git grep --no-text -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--no-textconv`

Desactiva para esta invocación el comportamiento que habilita `--textconv`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git grep --no-textconv -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--no-exclude-standard`

Desactiva para esta invocación el comportamiento que habilita `--exclude-standard`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git grep --no-exclude-standard -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--no-recursive`

Desactiva para esta invocación el comportamiento que habilita `--recursive`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git grep --no-recursive -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

### `--no-color`

Desactiva para esta invocación el comportamiento que habilita `--color`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git grep --no-color -n "TODO" -- '*.js'
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git blame`](../debugging/blame.md)
- [`git bisect`](../debugging/bisect.md)

## Fuente

- [git-grep - Print lines matching a pattern](https://git-scm.com/docs/git-grep)
