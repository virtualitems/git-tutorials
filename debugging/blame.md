---
title: "git blame"
source: "https://git-scm.com/docs/git-blame"
section: "debugging"
status: "source-audited"
version: "2.55.0"
---

# `git blame`

Este caso usa `git blame` para mostrar el commit y autor asociados con cada línea de un archivo.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La búsqueda combina revisiones, rutas y contenido. Primero delimita el conjunto de commits o archivos; después interpreta la evidencia que devuelve Git.

Reduce primero el rango y las rutas. Después interpreta cada coincidencia dentro de ese conjunto, sin atribuir significado a elementos que quedaron fuera.

## Ejemplo mínimo

```bash
git blame -L 10,20 -- README.md
```

La invocación `git blame -L 10,20 -- README.md` ejecuta esta operación: mostrar el commit y autor asociados con cada línea de un archivo. Después, la salida identifica líneas, archivos o commits que cumplen el criterio.

## Sintaxis y formas de invocación

```text
git blame [-c] [-b] [-l] [--root] [-t] [-f] [-n] [-s] [-e] [-p] [-w] [--incremental]
	  [-L <range>] [-S <revs-file>] [-M] [-C] [-C] [-C] [--since=<date>]
	  [--ignore-rev <rev>] [--ignore-revs-file <file>]
	  [--color-lines] [--color-by-age] [--progress] [--abbrev=<n>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git blame [<options>] [<rev-opts>] [<rev>] [--] <file>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git blame -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-c`

Aplica una clave de configuración solo a esta invocación.

```bash
git blame -c -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `-b`

Impide b durante esta invocación de `git blame`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not show object names of boundary commits (Default: off)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git blame -b -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `-l`

Incluye l en la salida o cambia cómo `git blame` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show long commit SHA1 (Default: off)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git blame -l -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `--root`

Procesa root con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `do not treat root commits as boundaries (Default: off)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git blame --root -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `-t`

Incluye t en la salida o cambia cómo `git blame` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show raw timestamp (Default: off)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git blame -t -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `-f` y `--show-name`

Incluye información adicional en la salida.

#### Ejemplo con `--show-name`

```bash
git blame --show-name -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `-n` y `--show-number`

Incluye información adicional en la salida.

#### Ejemplo con `--show-number`

```bash
git blame --show-number -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `-s`

Suprime s en la salida de esta invocación de `git blame`. En Git 2.51.1, la ayuda corta expresa el contrato como `suppress author name and timestamp (Default: off)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git blame -s -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `-e` y `--show-email`

Incluye información adicional en la salida.

#### Ejemplo con `--show-email`

```bash
git blame --show-email -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-p` y `--porcelain`

Produce un contrato de salida destinado a scripts.

#### Ejemplo con `--porcelain`

```bash
git blame --porcelain -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `-w`

Ignora w dentro del alcance que procesa `git blame`. En Git 2.51.1, la ayuda corta expresa el contrato como `ignore whitespace differences`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git blame -w -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `--incremental`

Incluye incremental en la salida o cambia cómo `git blame` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show blame entries as we find them, incrementally`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git blame --incremental -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `-L`

Procesa L con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `process only line range <start>,<end> or function :<funcname>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git blame -L valor -- README.md
printf 'exit=%s\n' "$?"
```

### `-S`

Incluye S en la salida o cambia cómo `git blame` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `use revisions from <file> instead of calling git-rev-list`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git blame -S rutas.txt -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-M`

Activa M durante mostrar el commit y autor asociados con cada línea de un archivo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `find line movements within and across files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git blame` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git blame -M valor -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

La opción cambia cómo `git blame` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git blame -C valor -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `--since`

Limita a entradas posteriores al instante indicado.

```bash
git blame --since -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `--ignore-rev`

Excluye elementos que cumplan la condición indicada.

```bash
git blame --ignore-rev=valor -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `--ignore-revs-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia cómo `git blame` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git blame --ignore-revs-file=rutas.txt -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--color-lines`

Activa color lines durante mostrar el commit y autor asociados con cada línea de un archivo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `color redundant metadata from previous line differently`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git blame --color-lines -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `--color-by-age`

Aplica una fecha, duración o política de vencimiento.

```bash
git blame --color-by-age -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git blame --progress -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `--abbrev`

Reduce la representación visible del identificador sin cambiar el objeto.

```bash
git blame --abbrev=5 -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--show-stats`

Incluye información adicional en la salida.

```bash
git blame --show-stats -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `--score-debug`

Incluye score debug en la salida o cambia cómo `git blame` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show output score for blame entries`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git blame --score-debug -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `--line-porcelain`

Incluye line salida para scripts en la salida o cambia cómo `git blame` la representa.

```bash
git blame --line-porcelain -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `--minimal`

Activa minimal durante mostrar el commit y autor asociados con cada línea de un archivo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `spend extra cycles to find better match`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git blame --minimal -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

### `--contents`

Define contents para esta ejecución de `git blame`. En Git 2.51.1, la ayuda corta expresa el contrato como `use <file>'s contents as the final image`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git blame` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git blame --contents=rutas.txt -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git blame --no-progress -L 10,20 -- README.md
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git grep`](../debugging/grep.md)
- [`git bisect`](../debugging/bisect.md)
- [`git annotate`](../debugging/annotate.md)

## Fuente

- [git-blame - Show what revision and author last modified each line of a file](https://git-scm.com/docs/git-blame)
