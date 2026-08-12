---
title: "git mktree"
source: "https://git-scm.com/docs/git-mktree"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git mktree`

Este caso usa `git mktree` para crear un objeto árbol a partir de una lista de entradas.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git ls-tree HEAD | git mktree
```

La invocación `git mktree` ejecuta esta operación: crear un objeto árbol a partir de una lista de entradas. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git mktree [-z] [--missing] [--batch]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git mktree [-z] [--missing] [--batch]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git mktree -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

La opción cambia cómo `git mktree` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git mktree -z
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--missing`

Permite missing cuando la forma predeterminada de `git mktree` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow missing objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git mktree --missing
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--batch`

Permite batch cuando la forma predeterminada de `git mktree` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow creation of more than one tree`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git mktree --batch
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git multi-pack-index`](../plumbing-write/multi-pack-index.md)
- [`git mktag`](../plumbing-write/mktag.md)
- [`git pack-objects`](../plumbing-write/pack-objects.md)

## Fuente

- [git-mktree - Build a tree-object from ls-tree formatted text](https://git-scm.com/docs/git-mktree)
