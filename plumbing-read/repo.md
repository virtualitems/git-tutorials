---
title: "git repo"
source: "https://git-scm.com/docs/git-repo"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git repo`

Este caso usa `git repo` para consultar propiedades y estructura del repositorio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git repo info --all
git repo structure
```

La invocación `git repo info --all` ejecuta esta operación: consultar propiedades y estructura del repositorio. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git repo info [--format=(lines|nul) | -z] [--all | <key>…]
git repo info --keys [--format=(lines|nul) | -z]
git repo structure [--format=(table|lines|nul) | -z]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git repo -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--format`

Define los campos y separadores de la salida.

```bash
git repo --format info --all
printf 'exit=%s\n' "$?"
```

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git repo -z info --all
printf 'exit=%s\n' "$?"
```

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git repo --all info
printf 'exit=%s\n' "$?"
```

### `--keys`

Activa keys durante consultar propiedades y estructura del repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git repo --keys info --all
printf 'exit=%s\n' "$?"
```

### `--help`

Muestra la ayuda correspondiente a la versión instalada.

```bash
git repo --help
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git rev-list`](../plumbing-read/rev-list.md)
- [`git pack-redundant`](../plumbing-read/pack-redundant.md)
- [`git rev-parse`](../plumbing-read/rev-parse.md)

## Fuente

- [git-repo - Retrieve information about the repository](https://git-scm.com/docs/git-repo)
