---
title: "git merge-file"
source: "https://git-scm.com/docs/git-merge-file"
section: "plumbing-write"
status: "option-expanded"
---

# `git merge-file`

Este caso usa `git merge-file` para fusionar tres versiones de un archivo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git merge-file crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en fusionar tres versiones de un archivo.

Puede persistir el estado implicado por esta operación: fusionar tres versiones de un archivo. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git merge-file actual.txt base.txt otra.txt
```

La invocación `git merge-file actual.txt base.txt otra.txt` ejecuta esta operación: fusionar tres versiones de un archivo. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git merge-file [-L <current-name> [-L <base-name> [-L <other-name>]]]
	[--ours|--theirs|--union] [-p|--stdout] [-q|--quiet] [--marker-size=<n>]
	[--[no-]diff3] [--object-id] <current> <base> <other>
```

### Uso verificado con `git version 2.51.1`

```text
git merge-file [<options>] [-L <name1> [-L <orig> [-L <name2>]]] <file1> <orig-file> <file2>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git merge-file -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

fusionar tres versiones de un archivo. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git merge-file a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git merge-file con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-L`

Define L para esta ejecución de `git merge-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `set labels for file1/orig-file/file2`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git merge-file` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git merge-file -L tema actual.txt base.txt otra.txt
git fsck --no-progress
```

El ejemplo usa `tema` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ours`

Selecciona la versión de la etapa ours para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use our version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge-file`, ours modifica la forma en que se ejecuta fusionar tres versiones de un archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-file --ours actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--theirs`

Selecciona la versión de la etapa theirs para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use their version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge-file`, theirs modifica la forma en que se ejecuta fusionar tres versiones de un archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-file --theirs actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--union`

Define union para esta ejecución de `git merge-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use a union version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge-file`, union modifica la forma en que se ejecuta fusionar tres versiones de un archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-file --union actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p` y `--stdout`

Incluye salida estándar en la salida o cambia cómo `git merge-file` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `send results to standard output`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-p`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-p`

```bash
git merge-file -p actual.txt base.txt otra.txt
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

#### Ejemplo con `--stdout`

```bash
git merge-file --stdout actual.txt base.txt otra.txt
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git merge-file -q actual.txt base.txt otra.txt
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

#### Ejemplo con `--quiet`

```bash
git merge-file --quiet actual.txt base.txt otra.txt
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--marker-size`

Define marker size para esta ejecución de `git merge-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use this marker size`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge-file`, marker size modifica la forma en que se ejecuta fusionar tres versiones de un archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-file --marker-size=5 actual.txt base.txt otra.txt
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--diff3`

Define diff3 para esta ejecución de `git merge-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `use a diff3 based merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge-file`, diff3 modifica la forma en que se ejecuta fusionar tres versiones de un archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-file --diff3 actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--object-id`

Selecciona la representación o tratamiento de identificadores de objeto.

La opción cambia cómo `git merge-file` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git merge-file --object-id actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--zdiff3`

Define zdiff3 para esta ejecución de `git merge-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `use a zealous diff3 based merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge-file`, zdiff3 modifica la forma en que se ejecuta fusionar tres versiones de un archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-file --zdiff3 actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--diff-algorithm`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git merge-file` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git merge-file --diff-algorithm=sha256 actual.txt base.txt otra.txt
git fsck --no-progress
```

El ejemplo usa `sha256` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ours`

Desactiva para esta invocación el comportamiento que habilita `--ours`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge-file`, desactivar ours modifica la forma en que se ejecuta fusionar tres versiones de un archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-file --no-ours actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-theirs`

Desactiva para esta invocación el comportamiento que habilita `--theirs`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge-file`, desactivar theirs modifica la forma en que se ejecuta fusionar tres versiones de un archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-file --no-theirs actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-union`

Desactiva para esta invocación el comportamiento que habilita `--union`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge-file`, desactivar union modifica la forma en que se ejecuta fusionar tres versiones de un archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-file --no-union actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stdout`

Desactiva para esta invocación el comportamiento que habilita `--stdout`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git merge-file --no-stdout actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git merge-file --no-quiet actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-marker-size`

Desactiva para esta invocación el comportamiento que habilita `--marker-size`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge-file`, desactivar marker size modifica la forma en que se ejecuta fusionar tres versiones de un archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-file --no-marker-size actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-diff3`

Desactiva para esta invocación el comportamiento que habilita `--diff3`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge-file`, desactivar diff3 modifica la forma en que se ejecuta fusionar tres versiones de un archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-file --no-diff3 actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-object-id`

Desactiva para esta invocación el comportamiento que habilita `--object-id`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git merge-file` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git merge-file --no-object-id actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-zdiff3`

Desactiva para esta invocación el comportamiento que habilita `--zdiff3`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge-file`, desactivar zdiff3 modifica la forma en que se ejecuta fusionar tres versiones de un archivo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge-file --no-zdiff3 actual.txt base.txt otra.txt
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge-file` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El hash no coincide

Comprueba esta causa: Los bytes, el tipo o la longitud difieren. Compara la entrada byte por byte y no normalices el contenido.

### La referencia no se actualiza

Comprueba esta causa: El valor anterior no coincide con la condición. Lee el valor actual y repite con una condición nueva.

### El índice queda sin resolver

Comprueba esta causa: Una entrada tiene etapas de conflicto. Inspecciona `git ls-files --stage` antes de escribir un árbol.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: fusionar tres versiones de un archivo. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git merge-index`](../plumbing-write/merge-index.md)
- [`git index-pack`](../plumbing-write/index-pack.md)
- [`git mktag`](../plumbing-write/mktag.md)

## Fuente

- [git-merge-file - Run a three-way file merge](https://git-scm.com/docs/git-merge-file)
