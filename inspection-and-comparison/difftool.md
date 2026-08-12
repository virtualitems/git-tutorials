---
title: "git difftool"
source: "https://git-scm.com/docs/git-difftool"
section: "inspection-and-comparison"
status: "source-audited"
version: "2.55.0"
---

# `git difftool`

Este caso usa `git difftool` para ver comparaciones con una herramienta externa.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Ejemplo mínimo

```bash
git difftool main..tema-portada -- README.md
```

La invocación `git difftool main..tema-portada -- README.md` ejecuta esta operación: ver comparaciones con una herramienta externa. Después, la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Sintaxis y formas de invocación

```text
git difftool [<options>] [<commit> [<commit>]] [--] [<path>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git difftool [<options>] [<commit> [<commit>]] [--] [<path>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git difftool -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-g` y `--gui`

Define gui para esta ejecución de `git difftool`. En Git 2.51.1, la ayuda corta expresa el contrato como `use `diff.guitool` instead of `diff.tool``. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--gui`

```bash
git difftool --gui main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

### `-d` y `--dir-diff`

Ejecuta dir diff durante ver comparaciones con una herramienta externa. En Git 2.51.1, la ayuda corta expresa el contrato como `perform a full-directory diff`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--dir-diff`

```bash
git difftool --dir-diff main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

### `-y`

Impide y durante esta invocación de `git difftool`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not prompt before launching a diff tool`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git difftool -y main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

### `--no-prompt`

Desactiva el comportamiento `prompt` para esta invocación.

```bash
git difftool --no-prompt main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

### `--symlinks`

Define symlinks para esta ejecución de `git difftool`. En Git 2.51.1, la ayuda corta expresa el contrato como `use symlinks in dir-diff mode`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git difftool --symlinks main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

### `-t` y `--tool`

Define tool para esta ejecución de `git difftool`. En Git 2.51.1, la ayuda corta expresa el contrato como `use the specified diff tool`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--tool`

```bash
git difftool --tool=valor main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--tool-help`

Incluye tool ayuda en la salida o cambia cómo `git difftool` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print a list of diff tools that may be used with `--tool``. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git difftool --tool-help main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

### `--trust-exit-code`

Activa trust exit code durante ver comparaciones con una herramienta externa. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `make 'git-difftool' exit when an invoked diff tool returns a non-zero exit code`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git difftool --trust-exit-code main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

### `-x` y `--extcmd`

Define extcmd para esta ejecución de `git difftool`. En Git 2.51.1, la ayuda corta expresa el contrato como `specify a custom command for viewing diffs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--extcmd`

```bash
git difftool --extcmd=status main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

En esta forma, `status` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--index`

Incluye el índice en la operación.

```bash
git difftool --index main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

### `--no-gui`

Desactiva para esta invocación el comportamiento que habilita `--gui`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git difftool --no-gui main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

### `--no-symlinks`

Desactiva para esta invocación el comportamiento que habilita `--symlinks`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git difftool --no-symlinks main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

### `--no-trust-exit-code`

Desactiva para esta invocación el comportamiento que habilita `--trust-exit-code`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git difftool --no-trust-exit-code main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

### `--prompt`

Solicita confirmación antes de abrir la herramienta para cada archivo. Es el comportamiento predeterminado y permite revertir una configuración que haya desactivado las preguntas.

```bash
git difftool --prompt HEAD~1 HEAD -- README.md
```

### `--rotate-to` y `--skip-to`

Ambas empiezan por la ruta indicada. `--rotate-to=<archivo>` mueve las rutas anteriores al final; `--skip-to=<archivo>` las omite.

```bash
git difftool --dir-diff --rotate-to=README.md HEAD~1 HEAD
git difftool --dir-diff --skip-to=README.md HEAD~1 HEAD
```

Usa el mismo rango para observar que la primera variante conserva todas las rutas y la segunda reduce el conjunto.

## Páginas relacionadas

- [`git last-modified`](../inspection-and-comparison/last-modified.md)
- [`git diff`](../inspection-and-comparison/diff.md)
- [`git log`](../inspection-and-comparison/log.md)

## Fuente

- [git-difftool - Show changes using common diff tools](https://git-scm.com/docs/git-difftool)
