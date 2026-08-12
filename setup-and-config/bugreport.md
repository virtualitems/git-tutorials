---
title: "git bugreport"
source: "https://git-scm.com/docs/git-bugreport"
section: "setup-and-config"
status: "source-audited"
version: "2.55.0"
---

# `git bugreport`

Este caso usa `git bugreport` para reunir información para informar un problema de Git.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

## Ejemplo mínimo

```bash
mkdir diagnostico
git bugreport --output-directory diagnostico
```

La invocación `git bugreport --output-directory diagnostico` ejecuta esta operación: reunir información para informar un problema de Git. Después, una consulta posterior muestra el valor efectivo o la información generada.

## Sintaxis y formas de invocación

```text
git bugreport [(-o | --output-directory) <path>]
		[(-s | --suffix) <format> | --no-suffix]
		[--diagnose[=<mode>]]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git bugreport [(-o | --output-directory) <path>]
                     [(-s | --suffix) <format> | --no-suffix]
                     [--diagnose[=<mode>]]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git bugreport -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-o` y `--output-directory`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

#### Ejemplo con `--output-directory`

```bash
git bugreport --output-directory=archivo.txt
printf 'exit=%s\n' "$?"
```

En esta forma, `archivo.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-s` y `--suffix`

Define suffix para esta ejecución de `git bugreport`. En Git 2.51.1, la ayuda corta expresa el contrato como `specify a strftime format suffix for the filename(s)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--suffix`

```bash
git bugreport --suffix=oneline --output-directory diagnostico
printf 'exit=%s\n' "$?"
```

En esta forma, `oneline` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--no-suffix`

Desactiva el comportamiento `suffix` para esta invocación.

```bash
git bugreport --no-suffix --output-directory diagnostico
printf 'exit=%s\n' "$?"
```

### `--diagnose`

Crea diagnose como parte de reunir información para informar un problema de Git. En Git 2.51.1, la ayuda corta expresa el contrato como `create an additional zip archive of detailed diagnostics (default 'stats')`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git bugreport --diagnose=all --output-directory diagnostico
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git diagnose`](../setup-and-config/diagnose.md)
- [`git config`](../setup-and-config/config.md)
- [`git help`](../setup-and-config/help.md)

## Fuente

- [git-bugreport - Collect information for user to file a bug report](https://git-scm.com/docs/git-bugreport)
