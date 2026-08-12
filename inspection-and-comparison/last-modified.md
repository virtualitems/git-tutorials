---
title: "git last-modified"
source: "https://git-scm.com/docs/git-last-modified"
section: "inspection-and-comparison"
status: "source-audited"
version: "2.55.0"
---

# `git last-modified`

Este caso usa `git last-modified` para mostrar el commit que modificó por última vez cada ruta.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Ejemplo mínimo

```bash
git last-modified --recursive HEAD -- docs/
```

La invocación `git last-modified --recursive HEAD -- docs/` ejecuta esta operación: mostrar el commit que modificó por última vez cada ruta. Después, la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Sintaxis y formas de invocación

```text
git last-modified [--recursive] [--show-trees] [--max-depth=<depth>] [-z]
		  [<revision-range>] [[--] <pathspec>…]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git last-modified -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--recursive`

Extiende la operación de forma recursiva al ámbito documentado.

```bash
git last-modified --recursive HEAD -- docs/
printf 'exit=%s\n' "$?"
```

### `--show-trees`

Incluye información adicional en la salida.

```bash
git last-modified --show-trees --recursive HEAD -- docs/
printf 'exit=%s\n' "$?"
```

### `--max-depth`

Establece un límite numérico para la selección o el recorrido.

```bash
git last-modified --max-depth --recursive HEAD -- docs/
printf 'exit=%s\n' "$?"
```

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git last-modified -z --recursive HEAD -- docs/
printf 'exit=%s\n' "$?"
```

### `--help`

Muestra la ayuda correspondiente a la versión instalada.

```bash
git last-modified --help
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git log`](../inspection-and-comparison/log.md)
- [`git difftool`](../inspection-and-comparison/difftool.md)
- [`git range-diff`](../inspection-and-comparison/range-diff.md)

## Fuente

- [git-last-modified - EXPERIMENTAL: Show when files were last modified](https://git-scm.com/docs/git-last-modified)
