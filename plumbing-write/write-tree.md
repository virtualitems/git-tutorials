---
title: "git write-tree"
source: "https://git-scm.com/docs/git-write-tree"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git write-tree`

Este caso usa `git write-tree` para crear un objeto árbol a partir del índice.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git add README.md
arbol=$(git write-tree)
git cat-file -t "$arbol"
```

La invocación `git write-tree` ejecuta esta operación: crear un objeto árbol a partir del índice. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git write-tree [--missing-ok] [--prefix=<prefix>/]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git write-tree [--missing-ok] [--prefix=<prefix>/]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git write-tree -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--missing-ok`

Permite missing ok cuando la forma predeterminada de `git write-tree` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow missing objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git write-tree --missing-ok
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--prefix`

Escribe o registra prefix como parte de crear un objeto árbol a partir del índice. En Git 2.51.1, la ayuda corta expresa el contrato como `write tree object for a subdirectory <prefix>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git write-tree --prefix=refs/heads/
git fsck --no-progress
```

El ejemplo usa `refs/heads/` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git update-ref`](../plumbing-write/update-ref.md)
- [`git update-index`](../plumbing-write/update-index.md)

## Fuente

- [git-write-tree - Create a tree object from the current index](https://git-scm.com/docs/git-write-tree)
