---
title: "git shortlog"
source: "https://git-scm.com/docs/git-shortlog"
section: "inspection-and-comparison"
status: "source-audited"
version: "2.55.0"
---

# `git shortlog`

Este caso usa `git shortlog` para agrupar el historial por autor y resumir sus commits.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Ejemplo mínimo

```bash
git shortlog --summary --numbered --all
```

La invocación `git shortlog --summary --numbered --all` ejecuta esta operación: agrupar el historial por autor y resumir sus commits. Después, la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Sintaxis y formas de invocación

```text
git shortlog [<options>] [<revision-range>] [[--] <path>…]
git log --pretty=short | git shortlog [<options>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git shortlog [<options>] [<revision-range>] [[--] <path>...]
   or: git log --pretty=short | git shortlog [<options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git shortlog -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--pretty`

Selecciona un formato para representar commits.

```bash
git shortlog --pretty --summary --numbered --all
printf 'exit=%s\n' "$?"
```

### `-c` y `--committer`

Activa committer durante agrupar el historial por autor y resumir sus commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `group by committer rather than author`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--committer`

```bash
git shortlog --committer --summary --numbered --all
printf 'exit=%s\n' "$?"
```

### `-n` y `--numbered`

Incluye numbered en la salida o cambia cómo `git shortlog` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `sort output according to the number of commits per author`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--numbered`

```bash
git shortlog --numbered --summary --all
printf 'exit=%s\n' "$?"
```

### `-s` y `--summary`

Suprime summary en la salida de esta invocación de `git shortlog`. En Git 2.51.1, la ayuda corta expresa el contrato como `suppress commit descriptions, only provides commit count`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--summary`

```bash
git shortlog --summary --numbered --all
printf 'exit=%s\n' "$?"
```

### `-e` y `--email`

Incluye email en la salida o cambia cómo `git shortlog` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show the email address of each author`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--email`

```bash
git shortlog --email --summary --numbered --all
printf 'exit=%s\n' "$?"
```

### `-w`

Incluye w en la salida o cambia cómo `git shortlog` la representa.

```bash
git shortlog -w valor --summary --numbered --all
printf 'exit=%s\n' "$?"
```

### `--group`

Activa group durante agrupar el historial por autor y resumir sus commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `group by field`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git shortlog --group=valor --summary --numbered --all
printf 'exit=%s\n' "$?"
```

### `--format`

Sustituye el asunto del commit por un formato aceptado por `git log`. Sin valor usa el formato predeterminado; con un valor opcional, escríbelo unido mediante `=`.

```bash
git shortlog --format='[%h] %s' HEAD
```

### `--date`

Formatea las fechas que incluya `--format` o `--group=format:<formato>`. Acepta los formatos de fecha de `git log`.

```bash
git shortlog --group='format:%ad' --date=short HEAD
```

La salida agrupa commits por la fecha de autor en formato `AAAA-MM-DD`.

## Páginas relacionadas

- [`git show`](../inspection-and-comparison/show.md)
- [`git range-diff`](../inspection-and-comparison/range-diff.md)
- [`git show-branch`](../inspection-and-comparison/show-branch.md)

## Fuente

- [git-shortlog - Summarize git log output](https://git-scm.com/docs/git-shortlog)
