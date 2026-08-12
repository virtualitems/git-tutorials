---
title: "git diff-files"
source: "https://git-scm.com/docs/git-diff-files"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git diff-files`

Este caso usa `git diff-files` para comparar el área de trabajo con el índice.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git diff-files -- README.md
```

La invocación `git diff-files -- README.md` ejecuta esta operación: comparar el área de trabajo con el índice. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git diff-files [-q] [-0 | -1 | -2 | -3 | -c | --cc] [<common-diff-options>] [<path>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git diff-files [-q] [-0 | -1 | -2 | -3 | -c | --cc] [<common-diff-options>] [<path>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git diff-files -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-q`

Activa q durante comparar el área de trabajo con el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git diff-files -q -- README.md
printf 'exit=%s\n' "$?"
```

### `-0`

Activa 0 durante comparar el área de trabajo con el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git diff-files -0 -- README.md
printf 'exit=%s\n' "$?"
```

### `-1`

Activa 1 durante comparar el área de trabajo con el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git diff-files -1 -- README.md
printf 'exit=%s\n' "$?"
```

### `-2`

Activa 2 durante comparar el área de trabajo con el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git diff-files -2 -- README.md
printf 'exit=%s\n' "$?"
```

### `-3`

Activa 3 durante comparar el área de trabajo con el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git diff-files -3 -- README.md
printf 'exit=%s\n' "$?"
```

### `-c`

Aplica una clave de configuración solo a esta invocación.

```bash
git diff-files -c -- README.md
printf 'exit=%s\n' "$?"
```

### `--cc`

Activa cc durante comparar el área de trabajo con el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git diff-files --cc -- README.md
printf 'exit=%s\n' "$?"
```

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git diff-files -z -- README.md
printf 'exit=%s\n' "$?"
```

### `-p`

Incluye p en la salida o cambia cómo `git diff-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output patch format.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-files -p -- README.md
printf 'exit=%s\n' "$?"
```

### `-u`

Selecciona la relación indicada por u; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `synonym for -p.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-files -u -- README.md
printf 'exit=%s\n' "$?"
```

### `--patch-with-raw`

Incluye parche with raw en la salida o cambia cómo `git diff-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output both a patch and the diff-raw format.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-files --patch-with-raw -- README.md
printf 'exit=%s\n' "$?"
```

### `--stat`

Resume cambios mediante conteos por ruta.

Esta forma se usa cuando `git diff-files` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque estadísticas actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git diff-files --stat -- README.md
printf 'exit=%s\n' "$?"
```

### `--numstat`

Incluye numstat en la salida o cambia cómo `git diff-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show numeric diffstat instead of patch.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-files --numstat -- README.md
printf 'exit=%s\n' "$?"
```

### `--patch-with-stat`

Antepone parche with estadísticas al valor que produce `git diff-files`. En Git 2.51.1, la ayuda corta expresa el contrato como `output a patch and prepend its diffstat.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-files --patch-with-stat -- README.md
printf 'exit=%s\n' "$?"
```

### `--name-only`

Muestra nombres de ruta sin el contenido del diff.

```bash
git diff-files --name-only -- README.md
printf 'exit=%s\n' "$?"
```

### `--name-status`

Muestra nombres y estado de cada ruta.

```bash
git diff-files --name-status -- README.md
printf 'exit=%s\n' "$?"
```

### `--full-index`

Incluye full índice en la salida o cambia cómo `git diff-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show full object name on index lines.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-files --full-index -- README.md
printf 'exit=%s\n' "$?"
```

### `--abbrev`

Reduce la representación visible del identificador sin cambiar el objeto.

```bash
git diff-files --abbrev=5 -- README.md
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-R`

Lee R como parte de la entrada de `git diff-files`. En Git 2.51.1, la ayuda corta expresa el contrato como `swap input file pairs.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git diff-files` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git diff-files -R -- README.md
printf 'exit=%s\n' "$?"
```

### `-B`

Activa B durante comparar el área de trabajo con el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `detect complete rewrites.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-files -B -- README.md
printf 'exit=%s\n' "$?"
```

### `-M`

Activa M durante comparar el área de trabajo con el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `detect renames.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción selecciona el procedimiento que `git diff-files` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git diff-files -M -- README.md
printf 'exit=%s\n' "$?"
```

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

La opción selecciona el procedimiento que `git diff-files` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git diff-files -C -- README.md
printf 'exit=%s\n' "$?"
```

### `--find-copies-harder`

Controla detección o búsqueda de relaciones entre entradas.

La opción cambia cómo `git diff-files` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git diff-files --find-copies-harder -- README.md
printf 'exit=%s\n' "$?"
```

### `-l`

Limita comparar el área de trabajo con el índice al alcance identificado por l. En Git 2.51.1, la ayuda corta expresa el contrato como `limit rename attempts up to <n> paths.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-files -l5 -- README.md
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-O`

Activa O durante comparar el área de trabajo con el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `reorder diffs according to the <file>.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git diff-files` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git diff-files -Orutas.txt -- README.md
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-S`

Limita comparar el área de trabajo con el índice al alcance identificado por S. En Git 2.51.1, la ayuda corta expresa el contrato como `find filepair whose only one side contains the string.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-files -Svalor -- README.md
printf 'exit=%s\n' "$?"
```

### `--pickaxe-all`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git diff-files --pickaxe-all -- README.md
printf 'exit=%s\n' "$?"
```

### `-a`

Procesa a con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `--text treat all files as text.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-files -a -- README.md
printf 'exit=%s\n' "$?"
```

### `--text`

Procesa texto con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `--text treat all files as text.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-files --text -- README.md
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git diff-index`](../plumbing-read/diff-index.md)
- [`git cherry`](../plumbing-read/cherry.md)
- [`git diff-pairs`](../plumbing-read/diff-pairs.md)

## Fuente

- [git-diff-files - Compares files in the working tree and the index](https://git-scm.com/docs/git-diff-files)
