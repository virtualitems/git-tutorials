---
title: "git merge-base"
source: "https://git-scm.com/docs/git-merge-base"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git merge-base`

Este caso usa `git merge-base` para calcular ancestros comunes para una fusión.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
base=$(git merge-base main tema-portada)
git show --oneline --no-patch "$base"
```

La invocación `git merge-base` ejecuta esta operación: calcular ancestros comunes para una fusión. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git merge-base [-a | --all] <commit> <commit>…
git merge-base [-a | --all] --octopus <commit>…
git merge-base --is-ancestor <commit> <commit>
git merge-base --independent <commit>…
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git merge-base [-a | --all] <commit> <commit>...
   or: git merge-base [-a | --all] --octopus <commit>...
   or: git merge-base --is-ancestor <commit> <commit>
   or: git merge-base --independent <commit>...
   or: git merge-base --fork-point <ref> [<commit>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git merge-base -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-a` y `--all`

Amplía la selección a todos los elementos del alcance definido.

#### Ejemplo con `--all`

```bash
git merge-base --all
printf 'exit=%s\n' "$?"
```

### `--octopus`

Activa octopus durante calcular ancestros comunes para una fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `find ancestors for a single n-way merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-base --octopus
printf 'exit=%s\n' "$?"
```

### `--is-ancestor`

Activa is ancestor durante calcular ancestros comunes para una fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `is the first one ancestor of the other?`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-base --is-ancestor
printf 'exit=%s\n' "$?"
```

### `--independent`

Incluye independent en la salida o cambia cómo `git merge-base` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `list revs not reachable from others`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-base --independent
printf 'exit=%s\n' "$?"
```

### `--fork-point`

Activa fork point durante calcular ancestros comunes para una fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `find where <commit> forked from reflog of <ref>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-base --fork-point
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git name-rev`](../plumbing-read/name-rev.md)
- [`git ls-tree`](../plumbing-read/ls-tree.md)
- [`git pack-redundant`](../plumbing-read/pack-redundant.md)

## Fuente

- [git-merge-base - Find as good common ancestors as possible for a merge](https://git-scm.com/docs/git-merge-base)
