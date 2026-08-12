---
title: "git get-tar-commit-id"
source: "https://git-scm.com/docs/git-get-tar-commit-id"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git get-tar-commit-id`

Este caso usa `git get-tar-commit-id` para extraer el identificador incluido por git archive en un tar.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git archive HEAD | git get-tar-commit-id
```

La invocación `git get-tar-commit-id` ejecuta esta operación: extraer el identificador incluido por git archive en un tar. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git get-tar-commit-id
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git get-tar-commit-id
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git get-tar-commit-id -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-h`

Activa h durante extraer el identificador incluido por git archive en un tar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git get-tar-commit-id -h
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git ls-files`](../plumbing-read/ls-files.md)
- [`git format-rev`](../plumbing-read/format-rev.md)
- [`git ls-tree`](../plumbing-read/ls-tree.md)

## Fuente

- [git-get-tar-commit-id - Extract commit ID from an archive created using git-archive](https://git-scm.com/docs/git-get-tar-commit-id)
