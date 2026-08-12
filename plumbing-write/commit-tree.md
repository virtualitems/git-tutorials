---
title: "git commit-tree"
source: "https://git-scm.com/docs/git-commit-tree"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git commit-tree`

Este caso usa `git commit-tree` para crear un objeto commit a partir de un árbol y sus padres.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
arbol=$(git write-tree)
commit=$(printf '%s\n' 'Commit de práctica' | git commit-tree "$arbol" -p HEAD)
printf '%s\n' "$commit"
```

La invocación `git commit-tree` ejecuta esta operación: crear un objeto commit a partir de un árbol y sus padres. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git commit-tree <tree> [(-p <parent>)…]
git commit-tree [(-p <parent>)…] [-S[<keyid>]] [(-m <message>)…]
		  [(-F <file>)…] <tree>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git commit-tree <tree> [(-p <parent>)...]
   or: git commit-tree [(-p <parent>)...] [-S[<keyid>]] [(-m <message>)...]
                       [(-F <file>)...] <tree>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git commit-tree -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-p`

Activa p durante crear un objeto commit a partir de un árbol y sus padres. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `id of a parent commit object`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit-tree -p valor
git fsck --no-progress
```

### `-S` y `--gpg-sign`

Activa gpg sign durante crear un objeto commit a partir de un árbol y sus padres. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--gpg-sign`

```bash
git commit-tree --gpg-sign=user.name
git fsck --no-progress
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `-m`

Activa m durante crear un objeto commit a partir de un árbol y sus padres. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `commit message`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit-tree -m 'mensaje de ejemplo'
git fsck --no-progress
```

El ejemplo usa `mensaje de ejemplo` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-F`

Lee F como parte de la entrada de `git commit-tree`. En Git 2.51.1, la ayuda corta expresa el contrato como `read commit log message from file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git commit-tree` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit-tree -F rutas.txt
git fsck --no-progress
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gpg-sign`

Desactiva para esta invocación el comportamiento que habilita `--gpg-sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git commit-tree --no-gpg-sign
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git hash-object`](../plumbing-write/hash-object.md)
- [`git commit-graph`](../plumbing-write/commit-graph.md)
- [`git index-pack`](../plumbing-write/index-pack.md)

## Fuente

- [git-commit-tree - Create a new commit object](https://git-scm.com/docs/git-commit-tree)
