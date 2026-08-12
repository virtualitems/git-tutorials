---
title: "git read-tree"
source: "https://git-scm.com/docs/git-read-tree"
section: "plumbing-write"
status: "option-expanded"
---

# `git read-tree`

Este caso usa `git read-tree` para cargar información de árboles en el índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git read-tree crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en cargar información de árboles en el índice.

Puede persistir el estado implicado por esta operación: cargar información de árboles en el índice. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git read-tree HEAD
git ls-files --stage
```

La invocación `git read-tree HEAD` ejecuta esta operación: cargar información de árboles en el índice. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git read-tree [(-m [--trivial] [--aggressive] | --reset | --prefix=<prefix>)
		[-u | -i]] [--index-output=<file>] [--no-sparse-checkout]
		(--empty | <tree-ish1> [<tree-ish2> [<tree-ish3>]])
```

### Uso verificado con `git version 2.51.1`

```text
git read-tree [(-m [--trivial] [--aggressive] | --reset | --prefix=<prefix>)
                     [-u | -i]] [--index-output=<file>] [--no-sparse-checkout]
                     (--empty | <tree-ish1> [<tree-ish2> [<tree-ish3>]])
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git read-tree -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

cargar información de árboles en el índice. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git read-tree a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Simulación

Calcular el efecto sin escribir el estado principal. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Compara la simulación con la selección prevista.

### Validación

Comprobar el resultado de git read-tree con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-m`

Ejecuta m durante cargar información de árboles en el índice. En Git 2.51.1, la ayuda corta expresa el contrato como `perform a merge in addition to a read`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git read-tree`, m modifica la forma en que se ejecuta cargar información de árboles en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git read-tree -m HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--trivial`

Activa trivial durante cargar información de árboles en el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `3-way merge if no file level merging required`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git read-tree` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git read-tree --trivial HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--aggressive`

Activa aggressive durante cargar información de árboles en el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `3-way merge in presence of adds and removes`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción controla aggressive. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cargar información de árboles en el índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git read-tree --aggressive HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reset`

Restablece restablecer como parte de cargar información de árboles en el índice. En Git 2.51.1, la ayuda corta expresa el contrato como `same as -m, but discard unmerged entries`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción controla restablecer. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cargar información de árboles en el índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git read-tree --reset HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--prefix`

Lee prefix como parte de la entrada de `git read-tree`. En Git 2.51.1, la ayuda corta expresa el contrato como `read the tree into the index under <subdirectory>/`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git read-tree`, prefix modifica la forma en que se ejecuta cargar información de árboles en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git read-tree --prefix=valor HEAD
git fsck --no-progress
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-u`

Actualiza u como parte de cargar información de árboles en el índice. En Git 2.51.1, la ayuda corta expresa el contrato como `update working tree with merge result`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git read-tree`, u modifica la forma en que se ejecuta cargar información de árboles en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git read-tree -u HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-i`

Impide i durante esta invocación de `git read-tree`. En Git 2.51.1, la ayuda corta expresa el contrato como `don't check the working tree after merging`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git read-tree -i HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index-output`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git read-tree --index-output=rutas.txt HEAD
git fsck --no-progress
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-sparse-checkout`

Desactiva el comportamiento `sparse-checkout` para esta invocación.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git read-tree --no-sparse-checkout HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--empty`

Limita cargar información de árboles en el índice al alcance identificado por vacío. En Git 2.51.1, la ayuda corta expresa el contrato como `only empty the index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git read-tree`, vacío modifica la forma en que se ejecuta cargar información de árboles en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git read-tree --empty HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-v`

```bash
git read-tree -v HEAD
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

#### Ejemplo con `--verbose`

```bash
git read-tree --verbose HEAD
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--exclude-per-directory`

Excluye elementos que cumplan la condición indicada.

La opción limita o amplía el conjunto sobre el que se ejecuta cargar información de árboles en el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git read-tree --exclude-per-directory=valor HEAD
git fsck --no-progress
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-n` y `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.  La misma línea de ayuda también acepta `-n`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

#### Ejemplo con `-n`

```bash
git read-tree -n HEAD
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

#### Ejemplo con `--dry-run`

```bash
git read-tree --dry-run HEAD
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--sparse-checkout`

Selecciona la relación indicada por sparse checkout; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-sparse-checkout`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git read-tree --sparse-checkout HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--debug-unpack`

Activa debug unpack durante cargar información de árboles en el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `debug unpack-trees`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git read-tree`, debug unpack modifica la forma en que se ejecuta cargar información de árboles en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git read-tree --debug-unpack HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git read-tree --recurse-submodules=valor HEAD
git fsck --no-progress
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git read-tree -q HEAD
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

#### Ejemplo con `--quiet`

```bash
git read-tree --quiet HEAD
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-trivial`

Desactiva para esta invocación el comportamiento que habilita `--trivial`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git read-tree` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git read-tree --no-trivial HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-aggressive`

Desactiva para esta invocación el comportamiento que habilita `--aggressive`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar aggressive. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cargar información de árboles en el índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git read-tree --no-aggressive HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reset`

Desactiva para esta invocación el comportamiento que habilita `--reset`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar restablecer. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cargar información de árboles en el índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git read-tree --no-reset HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-empty`

Desactiva para esta invocación el comportamiento que habilita `--empty`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git read-tree`, desactivar vacío modifica la forma en que se ejecuta cargar información de árboles en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git read-tree --no-empty HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git read-tree --no-verbose HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-dry-run`

Desactiva para esta invocación el comportamiento que habilita `--dry-run`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git read-tree --no-dry-run HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-debug-unpack`

Desactiva para esta invocación el comportamiento que habilita `--debug-unpack`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git read-tree`, desactivar debug unpack modifica la forma en que se ejecuta cargar información de árboles en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git read-tree --no-debug-unpack HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git read-tree --no-recurse-submodules HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git read-tree --no-quiet HEAD
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git read-tree` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El hash no coincide

Comprueba esta causa: Los bytes, el tipo o la longitud difieren. Compara la entrada byte por byte y no normalices el contenido.

### La referencia no se actualiza

Comprueba esta causa: El valor anterior no coincide con la condición. Lee el valor actual y repite con una condición nueva.

### El índice queda sin resolver

Comprueba esta causa: Una entrada tiene etapas de conflicto. Inspecciona `git ls-files --stage` antes de escribir un árbol.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: cargar información de árboles en el índice. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git symbolic-ref`](../plumbing-write/symbolic-ref.md)
- [`git prune-packed`](../plumbing-write/prune-packed.md)
- [`git unpack-objects`](../plumbing-write/unpack-objects.md)

## Fuente

- [git-read-tree - Reads tree information into the index](https://git-scm.com/docs/git-read-tree)
