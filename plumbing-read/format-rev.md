---
title: "git format-rev"
source: "https://git-scm.com/docs/git-format-rev"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git format-rev`

Este caso usa `git format-rev` para formatear revisiones recibidas por la entrada estándar.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
printf '%s\n' HEAD~2 HEAD~1 HEAD | git format-rev --stdin-mode=single --format='%h %s'
```

La invocación `git format-rev` ejecuta esta operación: formatear revisiones recibidas por la entrada estándar. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
(EXPERIMENTAL!) git format-rev --stdin-mode=<mode> --format=<pretty> [--[no-]notes=<ref>] [-z] [--[no-]null-output] [--[no-]null-input]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git format-rev -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--stdin-mode`

Activa entrada estándar mode durante formatear revisiones recibidas por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git format-rev` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git format-rev --stdin-mode
printf 'exit=%s\n' "$?"
```

### `--format`

Define los campos y separadores de la salida.

```bash
git format-rev --format
printf 'exit=%s\n' "$?"
```

### `--notes`

Activa notas durante formatear revisiones recibidas por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git format-rev --notes
printf 'exit=%s\n' "$?"
```

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git format-rev -z
printf 'exit=%s\n' "$?"
```

### `--null-output`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

```bash
git format-rev --null-output
printf 'exit=%s\n' "$?"
```

### `--null-input`

Activa terminación NUL entrada durante formatear revisiones recibidas por la entrada estándar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git format-rev` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git format-rev --null-input
printf 'exit=%s\n' "$?"
```

### `--help`

Muestra la ayuda correspondiente a la versión instalada.

```bash
git format-rev --help
printf 'exit=%s\n' "$?"
```

### `--notes` y `--no-notes`

`--notes=<ref>` selecciona la referencia de notas que usa el átomo `%N`; `--no-notes` desactiva una selección anterior.

```bash
git format-rev --format='%h %N' --notes=refs/notes/commits HEAD
```

### `--null`/`-z`, `--null-input`, `--no-null-input`, `--null-output` y `--no-null-output`

`--null` termina con NUL tanto las expresiones de entrada como los registros de salida y no admite negación. `--null-input` y `--null-output` cambian cada canal por separado; sus formas `--no-null-input` y `--no-null-output` restauran los saltos de línea predeterminados.

```bash
printf 'HEAD\0' | git format-rev --stdin-mode=revs \
  --null-input --null-output --format='%H'
```

El resultado termina en el byte `00`, por lo que debe consumirse con una herramienta que admita registros NUL y no como texto delimitado por líneas.

## Páginas relacionadas

- [`git get-tar-commit-id`](../plumbing-read/get-tar-commit-id.md)
- [`git for-each-repo`](../plumbing-read/for-each-repo.md)
- [`git ls-files`](../plumbing-read/ls-files.md)

## Fuente

- [git-format-rev - EXPERIMENTAL: Pretty format revisions on demand](https://git-scm.com/docs/git-format-rev)
