---
title: "git update-index"
source: "https://git-scm.com/docs/git-update-index"
section: "plumbing-write"
status: "option-expanded"
---

# `git update-index`

Este caso usa `git update-index` para modificar directamente entradas y bits del índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git update-index crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en modificar directamente entradas y bits del índice.

Puede persistir el estado implicado por esta operación: modificar directamente entradas y bits del índice. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git update-index --assume-unchanged config.local
git ls-files -v config.local
```

La invocación `git update-index --assume-unchanged config.local` ejecuta esta operación: modificar directamente entradas y bits del índice. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git update-index
	     [--add] [--remove | --force-remove] [--replace]
	     [--refresh] [-q] [--unmerged] [--ignore-missing]
	     [(--cacheinfo <mode>,<object>,<file>)…]
```

### Uso verificado con `git version 2.51.1`

```text
git update-index [<options>] [--] [<file>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git update-index -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

modificar directamente entradas y bits del índice. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git update-index a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git update-index con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--add`

Permite crear o escribir el elemento seleccionado.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --add --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--remove`

Retira elementos según las condiciones de la orden.

La opción controla retirar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque modificar directamente entradas y bits del índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git update-index --remove --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-remove`

Retira elementos según las condiciones de la orden.

La opción controla omitir la protección retirar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque modificar directamente entradas y bits del índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git update-index --force-remove --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--replace`

Activa replace durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `let files replace directories and vice-versa`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --replace --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--refresh`

Actualiza metadatos de comprobación sin copiar contenido nuevo al índice.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git update-index --refresh --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q`

Actualiza q como parte de modificar directamente entradas y bits del índice. En Git 2.51.1, la ayuda corta expresa el contrato como `continue refresh even when index needs update`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git update-index` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque q actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git update-index -q --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unmerged`

Activa unmerged durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `refresh even if index contains unmerged entries`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta modificar directamente entradas y bits del índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git update-index --unmerged --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-missing`

Permite comprobar rutas ausentes bajo las condiciones que define la orden.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --ignore-missing --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cacheinfo`

Incluye cacheinfo en la entrada, el resultado o el registro que construye `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `add the specified entry to the index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git update-index`, cacheinfo modifica la forma en que se ejecuta modificar directamente entradas y bits del índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-index --cacheinfo=all --assume-unchanged config.local
git fsck --no-progress
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-submodules`

Excluye elementos que cumplan la condición indicada.

En `git update-index`, ignorar submódulos modifica la forma en que se ejecuta modificar directamente entradas y bits del índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-index --ignore-submodules --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--really-refresh`

Ignora really refresh dentro del alcance que procesa `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `like --refresh, but ignore assume-unchanged setting`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta modificar directamente entradas y bits del índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git update-index --really-refresh --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--chmod`

Cambia el bit ejecutable registrado en el índice, no el permiso del archivo en disco.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --chmod=valor --assume-unchanged config.local
git fsck --no-progress
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--assume-unchanged`

Activa assume unchanged durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `mark files as "not changing"`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-assume-unchanged`

Desactiva el comportamiento `assume-unchanged` para esta invocación.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --no-assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--skip-worktree`

Limita modificar directamente entradas y bits del índice al alcance identificado por omitir el elemento actual área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `mark files as "index-only"`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git update-index` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque omitir el elemento actual área de trabajo actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git update-index --skip-worktree --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-skip-worktree`

Desactiva el comportamiento `skip-worktree` para esta invocación.

Esta forma se usa cuando `git update-index` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque desactivar omitir el elemento actual área de trabajo actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git update-index --no-skip-worktree --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-skip-worktree-entries`

Excluye elementos que cumplan la condición indicada.

Esta forma se usa cuando `git update-index` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque ignorar omitir el elemento actual área de trabajo entries actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git update-index --ignore-skip-worktree-entries --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--info-only`

Incluye info only en la entrada, el resultado o el registro que construye `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `add to index only; do not add content to object database`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git update-index`, info only modifica la forma en que se ejecuta modificar directamente entradas y bits del índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-index --info-only --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index -z --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.  La misma línea de ayuda también acepta `-z`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --stdin --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index-info`

Incluye índice info en la entrada, el resultado o el registro que construye `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `add entries from standard input to the index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --index-info --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unresolve`

Activa unresolve durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `repopulate stages #2 and #3 for the listed paths`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta modificar directamente entradas y bits del índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git update-index --unresolve --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-g` y `--again`

Actualiza again como parte de modificar directamente entradas y bits del índice. En Git 2.51.1, la ayuda corta expresa el contrato como `only update entries that differ from HEAD`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-g`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git update-index`, again modifica la forma en que se ejecuta modificar directamente entradas y bits del índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-g`

```bash
git update-index -g --assume-unchanged config.local
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

#### Ejemplo con `--again`

```bash
git update-index --again --assume-unchanged config.local
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--verbose`

Aumenta el detalle enviado a la salida.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git update-index --verbose --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--clear-resolve-undo`

Activa clear resolución undo durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `(for porcelains) forget saved unresolved conflicts`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git update-index --clear-resolve-undo --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index-version`

Escribe o registra índice versión como parte de modificar directamente entradas y bits del índice. En Git 2.51.1, la ayuda corta expresa el contrato como `write index in this format`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git update-index --index-version=5 --assume-unchanged config.local
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--show-index-version`

Incluye información adicional en la salida.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git update-index --show-index-version --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--split-index`

Impide split índice durante esta invocación de `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `enable or disable split index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git update-index`, split índice modifica la forma en que se ejecuta modificar directamente entradas y bits del índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-index --split-index --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--untracked-cache`

Impide untracked cache durante esta invocación de `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `enable/disable untracked cache`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git update-index`, untracked cache modifica la forma en que se ejecuta modificar directamente entradas y bits del índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-index --untracked-cache --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--test-untracked-cache`

Activa test untracked cache durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `test if the filesystem supports untracked cache`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --test-untracked-cache --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-untracked-cache`

Omite una protección concreta de la orden; requiere verificar origen y destino.

La opción controla omitir la protección untracked cache. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque modificar directamente entradas y bits del índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git update-index --force-untracked-cache --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-write-index`

Permite crear o escribir el elemento seleccionado.

La opción controla omitir la protección write índice. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque modificar directamente entradas y bits del índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git update-index --force-write-index --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--fsmonitor`

Impide fsmonitor durante esta invocación de `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `enable or disable file system monitor`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --fsmonitor --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--fsmonitor-valid`

Activa fsmonitor valid durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `mark files as fsmonitor valid`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --fsmonitor-valid --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-fsmonitor-valid`

Desactiva el comportamiento `fsmonitor-valid` para esta invocación.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --no-fsmonitor-valid --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-add`

Desactiva para esta invocación el comportamiento que habilita `--add`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --no-add --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-remove`

Desactiva para esta invocación el comportamiento que habilita `--remove`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar retirar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque modificar directamente entradas y bits del índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git update-index --no-remove --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force-remove`

Desactiva para esta invocación el comportamiento que habilita `--force-remove`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección retirar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque modificar directamente entradas y bits del índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git update-index --no-force-remove --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-replace`

Desactiva para esta invocación el comportamiento que habilita `--replace`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --no-replace --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-unmerged`

Desactiva para esta invocación el comportamiento que habilita `--unmerged`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta modificar directamente entradas y bits del índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git update-index --no-unmerged --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-missing`

Desactiva para esta invocación el comportamiento que habilita `--ignore-missing`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --no-ignore-missing --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-submodules`

Desactiva para esta invocación el comportamiento que habilita `--ignore-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git update-index`, desactivar ignorar submódulos modifica la forma en que se ejecuta modificar directamente entradas y bits del índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-index --no-ignore-submodules --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-skip-worktree-entries`

Desactiva para esta invocación el comportamiento que habilita `--ignore-skip-worktree-entries`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

Esta forma se usa cuando `git update-index` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque desactivar ignorar omitir el elemento actual área de trabajo entries actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git update-index --no-ignore-skip-worktree-entries --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-info-only`

Desactiva para esta invocación el comportamiento que habilita `--info-only`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git update-index`, desactivar info only modifica la forma en que se ejecuta modificar directamente entradas y bits del índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-index --no-info-only --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git update-index --no-verbose --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-index-version`

Desactiva para esta invocación el comportamiento que habilita `--index-version`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git update-index --no-index-version --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-show-index-version`

Desactiva para esta invocación el comportamiento que habilita `--show-index-version`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git update-index --no-show-index-version --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-split-index`

Desactiva para esta invocación el comportamiento que habilita `--split-index`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git update-index`, desactivar split índice modifica la forma en que se ejecuta modificar directamente entradas y bits del índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-index --no-split-index --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-untracked-cache`

Desactiva para esta invocación el comportamiento que habilita `--untracked-cache`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git update-index`, desactivar untracked cache modifica la forma en que se ejecuta modificar directamente entradas y bits del índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git update-index --no-untracked-cache --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-test-untracked-cache`

Desactiva para esta invocación el comportamiento que habilita `--test-untracked-cache`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --no-test-untracked-cache --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force-untracked-cache`

Desactiva para esta invocación el comportamiento que habilita `--force-untracked-cache`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección untracked cache. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque modificar directamente entradas y bits del índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git update-index --no-force-untracked-cache --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force-write-index`

Desactiva para esta invocación el comportamiento que habilita `--force-write-index`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección write índice. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque modificar directamente entradas y bits del índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git update-index --no-force-write-index --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-fsmonitor`

Desactiva para esta invocación el comportamiento que habilita `--fsmonitor`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --no-fsmonitor --assume-unchanged config.local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git update-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El hash no coincide

Comprueba esta causa: Los bytes, el tipo o la longitud difieren. Compara la entrada byte por byte y no normalices el contenido.

### La referencia no se actualiza

Comprueba esta causa: El valor anterior no coincide con la condición. Lee el valor actual y repite con una condición nueva.

### El índice queda sin resolver

Comprueba esta causa: Una entrada tiene etapas de conflicto. Inspecciona `git ls-files --stage` antes de escribir un árbol.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: modificar directamente entradas y bits del índice. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git update-ref`](../plumbing-write/update-ref.md)
- [`git unpack-objects`](../plumbing-write/unpack-objects.md)
- [`git write-tree`](../plumbing-write/write-tree.md)

## Fuente

- [git-update-index - Register file contents in the working tree to the index](https://git-scm.com/docs/git-update-index)
