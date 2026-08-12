---
title: "git update-ref"
source: "https://git-scm.com/docs/git-update-ref"
section: "plumbing-write"
status: "option-expanded"
---

# `git update-ref`

Este caso usa `git update-ref` para actualizar referencias con comprobaciones de valor anterior. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git update-ref crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en actualizar referencias con comprobaciones de valor anterior.

Puede persistir el estado implicado por esta operación: actualizar referencias con comprobaciones de valor anterior. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git update-ref refs/heads/prueba HEAD
git show-ref --verify refs/heads/prueba
```

La invocación `git update-ref refs/heads/prueba HEAD` ejecuta esta operación: actualizar referencias con comprobaciones de valor anterior. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git update-ref [-m <reason>] [--no-deref] -d <ref> [<old-oid>]
git update-ref [-m <reason>] [--no-deref] [--create-reflog] <ref> <new-oid> [<old-oid>]
git update-ref [-m <reason>] [--no-deref] --stdin [-z] [--batch-updates]
```

### Uso verificado con `git version 2.51.1`

```text
git update-ref [<options>] -d <refname> [<old-oid>]
   or: git update-ref [<options>]    <refname> <new-oid> [<old-oid>]
   or: git update-ref [<options>] --stdin [-z] [--batch-updates]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git update-ref -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

actualizar referencias con comprobaciones de valor anterior. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git update-ref a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git update-ref con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-m`

Actualiza m como parte de actualizar referencias con comprobaciones de valor anterior. En Git 2.51.1, la ayuda corta expresa el contrato como `reason of the update`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git update-ref`, m modifica la forma en que se ejecuta actualizar referencias con comprobaciones de valor anterior. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-ref -m valor refs/heads/prueba HEAD
git fsck --no-progress
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-deref`

Desactiva el comportamiento `deref` para esta invocación.

En `git update-ref`, desactivar deref modifica la forma en que se ejecuta actualizar referencias con comprobaciones de valor anterior. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-ref --no-deref refs/heads/prueba HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-ref` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d`

Retira d del alcance que procesa `git update-ref`. En Git 2.51.1, la ayuda corta expresa el contrato como `delete the reference`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción controla d. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque actualizar referencias con comprobaciones de valor anterior puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git update-ref -d refs/heads/prueba HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-ref` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--create-reflog`

Permite crear o escribir el elemento seleccionado.

En `git update-ref`, crear reflog modifica la forma en que se ejecuta actualizar referencias con comprobaciones de valor anterior. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-ref --create-reflog refs/heads/prueba HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-ref` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git update-ref` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-ref --stdin refs/heads/prueba HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-ref` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

La opción cambia cómo `git update-ref` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-ref -z refs/heads/prueba HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-ref` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--batch-updates` y `-0`

Activa batch updates durante actualizar referencias con comprobaciones de valor anterior. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `batch reference updates`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-0`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia cómo `git update-ref` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `--batch-updates`

```bash
git update-ref --batch-updates refs/heads/prueba HEAD
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git update-ref` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

#### Ejemplo con `-0`

```bash
git update-ref -0 refs/heads/prueba HEAD
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git update-ref` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--deref`

Selecciona la relación indicada por deref; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-deref`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git update-ref`, deref modifica la forma en que se ejecuta actualizar referencias con comprobaciones de valor anterior. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-ref --deref refs/heads/prueba HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-ref` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-create-reflog`

Desactiva para esta invocación el comportamiento que habilita `--create-reflog`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git update-ref`, desactivar crear reflog modifica la forma en que se ejecuta actualizar referencias con comprobaciones de valor anterior. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-ref --no-create-reflog refs/heads/prueba HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-ref` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stdin`

Desactiva para esta invocación el comportamiento que habilita `--stdin`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git update-ref` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-ref --no-stdin refs/heads/prueba HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-ref` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-batch-updates`

Desactiva para esta invocación el comportamiento que habilita `--batch-updates`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git update-ref` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-ref --no-batch-updates refs/heads/prueba HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-ref` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El hash no coincide

Comprueba esta causa: Los bytes, el tipo o la longitud difieren. Compara la entrada byte por byte y no normalices el contenido.

### La referencia no se actualiza

Comprueba esta causa: El valor anterior no coincide con la condición. Lee el valor actual y repite con una condición nueva.

### El índice queda sin resolver

Comprueba esta causa: Una entrada tiene etapas de conflicto. Inspecciona `git ls-files --stage` antes de escribir un árbol.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: actualizar referencias con comprobaciones de valor anterior. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git write-tree`](../plumbing-write/write-tree.md)
- [`git update-index`](../plumbing-write/update-index.md)
- [`git unpack-objects`](../plumbing-write/unpack-objects.md)

## Fuente

- [git-update-ref - Update the object name stored in a ref safely](https://git-scm.com/docs/git-update-ref)
