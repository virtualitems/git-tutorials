---
title: "git format-patch"
source: "https://git-scm.com/docs/git-format-patch"
section: "email-and-patches"
status: "option-expanded"
---

# `git format-patch`

Este caso usa `git format-patch` para representar commits como archivos de parche para correo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git format-patch genera, transporta o aplica series de parches conservando autoría y orden. Recibe como entrada una serie de commits, parches o mensajes de correo. La operación consiste en representar commits como archivos de parche para correo.

Genera un archivo o flujo de salida; no mueve referencias por sí mismo.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Cada parche puede transportar autoría, mensaje y diferencias. El receptor valida, aplica y registra la serie en su propio historial.

Conserva el orden de la serie y separa autor de quien aplica el parche. Los conflictos se resuelven antes de continuar con el siguiente mensaje.

## Ejemplo mínimo

```bash
git format-patch origin/main..HEAD --output-directory parches/
```

La invocación `git format-patch origin/main..HEAD --output-directory parches/` ejecuta esta operación: representar commits como archivos de parche para correo. Después, el receptor obtiene parches o commits con el orden, autoría y mensaje esperados. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git format-patch [-k] [(-o|--output-directory) <dir> | --stdout]
		   [--no-thread | --thread[=<style>]]
		   [(--attach|--inline)[=<boundary>] | --no-attach]
		   [-s | --signoff]
```

### Uso verificado con `git version 2.51.1`

```text
git format-patch [<options>] [<since> | <revision-range>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git format-patch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

representar commits como archivos de parche para correo. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git format-patch a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git format-patch con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-k` y `--keep-subject`

Incluye conservar subject en la entrada, el resultado o el registro que construye `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `don't strip/add [PATCH]`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-k`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git format-patch`, conservar subject modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-k`

```bash
git format-patch -k origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--keep-subject`

```bash
git format-patch --keep-subject origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-o` y `--output-directory`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.  La misma línea de ayuda también acepta `-o`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-o`

```bash
git format-patch -o docs origin/main..HEAD
printf 'exit=%s\n' "$?"
```

En esta forma, `docs` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--output-directory`

```bash
git format-patch --output-directory=docs origin/main..HEAD
printf 'exit=%s\n' "$?"
```

En esta forma, `docs` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--stdout`

Incluye salida estándar en la salida o cambia cómo `git format-patch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print patches to standard out`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --stdout origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-thread`

Desactiva el comportamiento `thread` para esta invocación.

La opción limita o amplía el conjunto sobre el que se ejecuta representar commits como archivos de parche para correo. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git format-patch --no-thread origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--thread`

Activa thread durante representar commits como archivos de parche para correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `enable message threading, styles: shallow, deep`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta representar commits como archivos de parche para correo. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git format-patch --thread=short origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--attach`

Activa attach durante representar commits como archivos de parche para correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `attach the patch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git format-patch`, attach modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --attach=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--inline`

Activa inline durante representar commits como archivos de parche para correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git format-patch`, inline modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --inline=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-attach`

Desactiva el comportamiento `attach` para esta invocación.

En `git format-patch`, desactivar attach modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-attach origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-s` y `--signoff`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-s`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git format-patch`, añadir Signed-off-by modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-s`

```bash
git format-patch -s origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--signoff`

```bash
git format-patch --signoff origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-n` y `--numbered`

Define numbered para esta ejecución de `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `use [PATCH n/m] even with a single patch`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-n`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git format-patch`, numbered modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-n`

```bash
git format-patch -n origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--numbered`

```bash
git format-patch --numbered origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-N`

Define N para esta ejecución de `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `use [PATCH] even with multiple patches`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `--no-numbered`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

En `git format-patch`, N modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch -N origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-numbered`

Desactiva el comportamiento `numbered` para esta invocación.

En `git format-patch`, desactivar numbered modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-numbered origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cover-letter`

Genera cover letter como parte del resultado de `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate a cover letter`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git format-patch`, cover letter modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --cover-letter origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--numbered-files`

Incluye numbered files en la salida o cambia cómo `git format-patch` la representa.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --numbered-files origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--suffix`

Define suffix para esta ejecución de `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `use <sfx> instead of '.patch'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git format-patch`, suffix modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --suffix=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--start-number`

Activa start number durante representar commits como archivos de parche para correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `start numbering patches at <n> instead of 1`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git format-patch`, start number modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --start-number=5 origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--reroll-count`

Establece un límite numérico para la selección o el recorrido.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git format-patch`, reroll cantidad modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-v`

```bash
git format-patch -v 5 origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--reroll-count`

```bash
git format-patch --reroll-count=5 origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--filename-max-length`

Establece un límite numérico para la selección o el recorrido.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --filename-max-length=5 origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--rfc`

Incluye rfc en la entrada, el resultado o el registro que construye `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `add <rfc> (default 'RFC') before 'PATCH'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git format-patch`, rfc modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --rfc=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cover-from-description`

Genera cover from description como parte del resultado de `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate parts of a cover letter based on a branch's description`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta representar commits como archivos de parche para correo. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git format-patch --cover-from-description=all origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--description-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción limita o amplía el conjunto sobre el que se ejecuta representar commits como archivos de parche para correo. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git format-patch --description-file=rutas.txt origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--subject-prefix`

Define subject prefix para esta ejecución de `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `use [<prefix>] instead of [PATCH]`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git format-patch`, subject prefix modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --subject-prefix=refs/heads/ origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `refs/heads/` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-binary`

Desactiva el comportamiento `binary` para esta invocación.

En `git format-patch`, desactivar contenido binario modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-binary origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--binary`

Selecciona la relación indicada por contenido binario; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-binary`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git format-patch`, contenido binario modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --binary origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--zero-commit`

Incluye zero commit en la salida o cambia cómo `git format-patch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output all-zero hash in From header`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --zero-commit origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-if-in-upstream`

Excluye elementos que cumplan la condición indicada.

La opción limita o amplía el conjunto sobre el que se ejecuta representar commits como archivos de parche para correo. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git format-patch --ignore-if-in-upstream origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p`

Incluye p en la salida o cambia cómo `git format-patch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show patch format instead of default (patch + stat)`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `--no-stat`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch -p origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stat`

Desactiva el comportamiento `stat` para esta invocación.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --no-stat origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--add-header`

Permite crear o escribir el elemento seleccionado.

En `git format-patch`, add header modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --add-header=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--to`

Incluye to en la entrada, el resultado o el registro que construye `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `add To: header`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git format-patch`, to modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --to=user@example.com origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `user@example.com` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cc`

Incluye cc en la entrada, el resultado o el registro que construye `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `add Cc: header`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git format-patch`, cc modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --cc=user@example.com origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `user@example.com` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--from`

Define from para esta ejecución de `git format-patch`.

En `git format-patch`, from modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --from=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--in-reply-to`

Activa in reply to durante representar commits como archivos de parche para correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `make first mail a reply to <message-id>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git format-patch`, in reply to modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --in-reply-to='mensaje de ejemplo' origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `mensaje de ejemplo` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signature`

Incluye firma en la entrada, el resultado o el registro que construye `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `add a signature`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git format-patch`, firma modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --signature=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--base`

Incluye base en la entrada, el resultado o el registro que construye `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `add prerequisite tree info to the patch series`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git format-patch`, base modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --base=HEAD origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signature-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia cómo `git format-patch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git format-patch --signature-file=rutas.txt origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git format-patch -q origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--quiet`

```bash
git format-patch --quiet origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --progress origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--interdiff`

Incluye interdiff en la salida o cambia cómo `git format-patch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show changes against <rev> in cover letter or single patch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --interdiff=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--range-diff`

Incluye range diff en la salida o cambia cómo `git format-patch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show changes against <refspec> in cover letter or single patch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --range-diff=main origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--creation-factor`

Activa creation factor durante representar commits como archivos de parche para correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `percentage by which creation is weighted`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta representar commits como archivos de parche para correo. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git format-patch --creation-factor=5 origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-in-body-from`

Omite una protección concreta de la orden; requiere verificar origen y destino.

La opción controla omitir la protección in body from. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque representar commits como archivos de parche para correo puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git format-patch --force-in-body-from origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stdout`

Desactiva para esta invocación el comportamiento que habilita `--stdout`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --no-stdout origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signoff`

Desactiva para esta invocación el comportamiento que habilita `--signoff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git format-patch`, desactivar añadir Signed-off-by modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-signoff origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cover-letter`

Desactiva para esta invocación el comportamiento que habilita `--cover-letter`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git format-patch`, desactivar cover letter modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-cover-letter origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-numbered-files`

Desactiva para esta invocación el comportamiento que habilita `--numbered-files`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --no-numbered-files origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-suffix`

Desactiva para esta invocación el comportamiento que habilita `--suffix`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git format-patch`, desactivar suffix modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-suffix origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-start-number`

Desactiva para esta invocación el comportamiento que habilita `--start-number`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git format-patch`, desactivar start number modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-start-number origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reroll-count`

Desactiva para esta invocación el comportamiento que habilita `--reroll-count`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git format-patch`, desactivar reroll cantidad modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-reroll-count origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-filename-max-length`

Desactiva para esta invocación el comportamiento que habilita `--filename-max-length`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --no-filename-max-length origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-rfc`

Desactiva para esta invocación el comportamiento que habilita `--rfc`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git format-patch`, desactivar rfc modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-rfc origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cover-from-description`

Desactiva para esta invocación el comportamiento que habilita `--cover-from-description`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta representar commits como archivos de parche para correo. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git format-patch --no-cover-from-description origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-description-file`

Desactiva para esta invocación el comportamiento que habilita `--description-file`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta representar commits como archivos de parche para correo. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git format-patch --no-description-file origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-zero-commit`

Desactiva para esta invocación el comportamiento que habilita `--zero-commit`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --no-zero-commit origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-if-in-upstream`

Desactiva para esta invocación el comportamiento que habilita `--ignore-if-in-upstream`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta representar commits como archivos de parche para correo. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git format-patch --no-ignore-if-in-upstream origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-add-header`

Desactiva para esta invocación el comportamiento que habilita `--add-header`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git format-patch`, desactivar add header modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-add-header origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-to`

Desactiva para esta invocación el comportamiento que habilita `--to`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git format-patch`, desactivar to modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-to origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cc`

Desactiva para esta invocación el comportamiento que habilita `--cc`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git format-patch`, desactivar cc modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-cc origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-from`

Desactiva para esta invocación el comportamiento que habilita `--from`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git format-patch`, desactivar from modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-from origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-in-reply-to`

Desactiva para esta invocación el comportamiento que habilita `--in-reply-to`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git format-patch`, desactivar in reply to modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-in-reply-to origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signature`

Desactiva para esta invocación el comportamiento que habilita `--signature`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git format-patch`, desactivar firma modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-signature origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-base`

Desactiva para esta invocación el comportamiento que habilita `--base`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git format-patch`, desactivar base modifica la forma en que se ejecuta representar commits como archivos de parche para correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git format-patch --no-base origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signature-file`

Desactiva para esta invocación el comportamiento que habilita `--signature-file`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git format-patch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git format-patch --no-signature-file origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --no-quiet origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --no-progress origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-interdiff`

Desactiva para esta invocación el comportamiento que habilita `--interdiff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --no-interdiff origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-range-diff`

Desactiva para esta invocación el comportamiento que habilita `--range-diff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git format-patch --no-range-diff origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-creation-factor`

Desactiva para esta invocación el comportamiento que habilita `--creation-factor`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta representar commits como archivos de parche para correo. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git format-patch --no-creation-factor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force-in-body-from`

Desactiva para esta invocación el comportamiento que habilita `--force-in-body-from`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección in body from. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque representar commits como archivos de parche para correo puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git format-patch --no-force-in-body-from origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git format-patch` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La numeración no coincide

Comprueba esta causa: El rango o la revisión de la serie cambió. Regenera la serie completa con el mismo punto base.

### La aplicación se detiene

Comprueba esta causa: El parche no coincide o falta información de autor. Corrige el parche o resuelve y continúa la sesión.

### El transporte rechaza el mensaje

Comprueba esta causa: La configuración SMTP o IMAP no autoriza la operación. Prueba autenticación fuera del contenido del mensaje y evita secretos en argumentos.

## Automatización y recuperación

Persistencia: Genera un archivo o flujo de salida; no mueve referencias por sí mismo. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Genera una serie de dos commits en una rama de prueba. Inspecciona los archivos de parche y aplícalos en otro clon.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git imap-send`](../email-and-patches/imap-send.md)
- [`git am`](../email-and-patches/am.md)
- [`git send-email`](../email-and-patches/send-email.md)

## Fuente

- [git-format-patch - Prepare patches for e-mail submission](https://git-scm.com/docs/git-format-patch)
