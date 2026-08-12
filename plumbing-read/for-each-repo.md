---
title: "git for-each-repo"
source: "https://git-scm.com/docs/git-for-each-repo"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git for-each-repo`

Este caso usa `git for-each-repo` para ejecutar un comando Git en repositorios enumerados por configuración.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git config --global --add repos.proyectos ~/codigo/biblioteca
git for-each-repo --config=repos.proyectos status --short
```

La invocación `git for-each-repo --config=repos.proyectos status --short` ejecuta esta operación: ejecutar un comando Git en repositorios enumerados por configuración. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git for-each-repo --config=<config> [--] <arguments>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git for-each-repo --config=<config> [--] <arguments>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git for-each-repo -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--config`

Incluye config en la salida o cambia cómo `git for-each-repo` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `config key storing a list of repository paths`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git for-each-repo --config=valor status --short
printf 'exit=%s\n' "$?"
```

### `--keep-going`

Activa conservar going durante ejecutar un comando Git en repositorios enumerados por configuración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `keep going even if command fails in a repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git for-each-repo --keep-going --config=repos.proyectos status --short
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git format-rev`](../plumbing-read/format-rev.md)
- [`git for-each-ref`](../plumbing-read/for-each-ref.md)
- [`git get-tar-commit-id`](../plumbing-read/get-tar-commit-id.md)

## Fuente

- [git-for-each-repo - Run a Git command on a list of repositories](https://git-scm.com/docs/git-for-each-repo)
