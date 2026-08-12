---
title: "git commit-tree"
source: "https://git-scm.com/docs/git-commit-tree"
section: "plumbing-write"
status: "option-expanded"
---

# `git commit-tree`

Este caso usa `git commit-tree` para crear un objeto commit a partir de un árbol y sus padres. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git commit-tree crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en crear un objeto commit a partir de un árbol y sus padres.

Puede persistir el estado implicado por esta operación: crear un objeto commit a partir de un árbol y sus padres. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
arbol=$(git write-tree)
commit=$(printf '%s\n' 'Commit de práctica' | git commit-tree "$arbol" -p HEAD)
printf '%s\n' "$commit"
```

La invocación `git commit-tree` ejecuta esta operación: crear un objeto commit a partir de un árbol y sus padres. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git commit-tree <tree> [(-p <parent>)…]
git commit-tree [(-p <parent>)…] [-S[<keyid>]] [(-m <message>)…]
		  [(-F <file>)…] <tree>
```

### Uso verificado con `git version 2.51.1`

```text
git commit-tree <tree> [(-p <parent>)...]
   or: git commit-tree [(-p <parent>)...] [-S[<keyid>]] [(-m <message>)...]
                       [(-F <file>)...] <tree>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git commit-tree -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

crear un objeto commit a partir de un árbol y sus padres. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git commit-tree a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git commit-tree con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-p`

Activa p durante crear un objeto commit a partir de un árbol y sus padres. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `id of a parent commit object`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git commit-tree`, p modifica la forma en que se ejecuta crear un objeto commit a partir de un árbol y sus padres. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit-tree -p valor
git fsck --no-progress
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-S` y `--gpg-sign`

Activa gpg sign durante crear un objeto commit a partir de un árbol y sus padres. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign commit`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-S`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git commit-tree`, gpg sign modifica la forma en que se ejecuta crear un objeto commit a partir de un árbol y sus padres. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-S`

```bash
git commit-tree -S=user.name
git fsck --no-progress
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

#### Ejemplo con `--gpg-sign`

```bash
git commit-tree --gpg-sign=user.name
git fsck --no-progress
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-m`

Activa m durante crear un objeto commit a partir de un árbol y sus padres. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `commit message`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git commit-tree`, m modifica la forma en que se ejecuta crear un objeto commit a partir de un árbol y sus padres. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

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

En `git commit-tree`, desactivar gpg sign modifica la forma en que se ejecuta crear un objeto commit a partir de un árbol y sus padres. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit-tree --no-gpg-sign
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El hash no coincide

Comprueba esta causa: Los bytes, el tipo o la longitud difieren. Compara la entrada byte por byte y no normalices el contenido.

### La referencia no se actualiza

Comprueba esta causa: El valor anterior no coincide con la condición. Lee el valor actual y repite con una condición nueva.

### El índice queda sin resolver

Comprueba esta causa: Una entrada tiene etapas de conflicto. Inspecciona `git ls-files --stage` antes de escribir un árbol.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: crear un objeto commit a partir de un árbol y sus padres. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git hash-object`](../plumbing-write/hash-object.md)
- [`git commit-graph`](../plumbing-write/commit-graph.md)
- [`git index-pack`](../plumbing-write/index-pack.md)

## Fuente

- [git-commit-tree - Create a new commit object](https://git-scm.com/docs/git-commit-tree)
