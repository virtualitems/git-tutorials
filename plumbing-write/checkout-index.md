---
title: "git checkout-index"
source: "https://git-scm.com/docs/git-checkout-index"
section: "plumbing-write"
status: "option-expanded"
---

# `git checkout-index`

Este caso usa `git checkout-index` para copiar archivos del índice al área de trabajo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git checkout-index crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en copiar archivos del índice al área de trabajo.

Puede persistir el estado implicado por esta operación: copiar archivos del índice al área de trabajo. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
mkdir exportado
git checkout-index --all --prefix=exportado/
```

La invocación `git checkout-index --all --prefix=exportado/` ejecuta esta operación: copiar archivos del índice al área de trabajo. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git checkout-index [-u] [-q] [-a] [-f] [-n] [--prefix=<string>]
		   [--stage=<number>|all]
		   [--temp]
		   [--ignore-skip-worktree-bits]
```

### Uso verificado con `git version 2.51.1`

```text
git checkout-index [<options>] [--] [<file>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git checkout-index -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

copiar archivos del índice al área de trabajo. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git checkout-index a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git checkout-index con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-u` y `--index`

Incluye el índice en la operación.  La misma línea de ayuda también acepta `-u`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-u`

```bash
git checkout-index -u --all --prefix=exportado/
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

#### Ejemplo con `--index`

```bash
git checkout-index --index --all --prefix=exportado/
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git checkout-index -q --all --prefix=exportado/
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

#### Ejemplo con `--quiet`

```bash
git checkout-index --quiet --all --prefix=exportado/
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-a` y `--all`

Amplía la selección a todos los elementos del alcance definido.  La misma línea de ayuda también acepta `-a`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta copiar archivos del índice al área de trabajo. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-a`

```bash
git checkout-index -a --prefix=exportado/
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

#### Ejemplo con `--all`

```bash
git checkout-index --all --prefix=exportado/
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.  La misma línea de ayuda también acepta `-f`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque copiar archivos del índice al área de trabajo puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-f`

```bash
git checkout-index -f --all --prefix=exportado/
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

#### Ejemplo con `--force`

```bash
git checkout-index --force --all --prefix=exportado/
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-n`

Crea n como parte de copiar archivos del índice al área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `don't checkout new files`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `--no-create`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

La opción cambia cómo `git checkout-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout-index -n --all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--prefix`

Antepone prefix al valor que produce `git checkout-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `when creating files, prepend <string>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git checkout-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout-index --prefix=valor --all
git fsck --no-progress
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stage`

Activa stage durante copiar archivos del índice al área de trabajo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `copy out the files from named stage`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta copiar archivos del índice al área de trabajo. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git checkout-index --stage=valor --all --prefix=exportado/
git fsck --no-progress
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--temp`

Escribe o registra temp como parte de copiar archivos del índice al área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `write the content to temporary files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git checkout-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout-index --temp --all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-skip-worktree-bits`

Excluye elementos que cumplan la condición indicada.

Esta forma se usa cuando `git checkout-index` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque ignorar omitir el elemento actual área de trabajo bits actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git checkout-index --ignore-skip-worktree-bits --all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-create`

Desactiva el comportamiento `create` para esta invocación.

En `git checkout-index`, desactivar crear modifica la forma en que se ejecuta copiar archivos del índice al área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git checkout-index --no-create --all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--create`

Permite crear o escribir el elemento seleccionado.

En `git checkout-index`, crear modifica la forma en que se ejecuta copiar archivos del índice al área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git checkout-index --create --all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

En `git checkout-index`, z modifica la forma en que se ejecuta copiar archivos del índice al área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git checkout-index -z --all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git checkout-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout-index --stdin --all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-prefix`

Desactiva para esta invocación el comportamiento que habilita `--prefix`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git checkout-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout-index --no-prefix --all
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-temp`

Desactiva para esta invocación el comportamiento que habilita `--temp`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git checkout-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout-index --no-temp --all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-skip-worktree-bits`

Desactiva para esta invocación el comportamiento que habilita `--ignore-skip-worktree-bits`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

Esta forma se usa cuando `git checkout-index` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque desactivar ignorar omitir el elemento actual área de trabajo bits actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git checkout-index --no-ignore-skip-worktree-bits --all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-all`

Desactiva para esta invocación el comportamiento que habilita `--all`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta copiar archivos del índice al área de trabajo. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git checkout-index --no-all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force`

Desactiva para esta invocación el comportamiento que habilita `--force`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque copiar archivos del índice al área de trabajo puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git checkout-index --no-force --all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git checkout-index --no-quiet --all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-index`

Desactiva para esta invocación el comportamiento que habilita `--index`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git checkout-index --no-index --all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stdin`

Desactiva para esta invocación el comportamiento que habilita `--stdin`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git checkout-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout-index --no-stdin --all --prefix=exportado/
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout-index` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El hash no coincide

Comprueba esta causa: Los bytes, el tipo o la longitud difieren. Compara la entrada byte por byte y no normalices el contenido.

### La referencia no se actualiza

Comprueba esta causa: El valor anterior no coincide con la condición. Lee el valor actual y repite con una condición nueva.

### El índice queda sin resolver

Comprueba esta causa: Una entrada tiene etapas de conflicto. Inspecciona `git ls-files --stage` antes de escribir un árbol.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: copiar archivos del índice al área de trabajo. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git commit-graph`](../plumbing-write/commit-graph.md)
- [`git commit-tree`](../plumbing-write/commit-tree.md)

## Fuente

- [git-checkout-index - Copy files from the index to the working tree](https://git-scm.com/docs/git-checkout-index)
