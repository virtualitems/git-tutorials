---
title: "git commit"
source: "https://git-scm.com/docs/git-commit"
section: "basic-snapshotting"
status: "option-expanded"
---

# `git commit`

Este caso usa `git commit` para registrar en el historial el contenido preparado en el índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git commit mueve contenido entre el área de trabajo, el índice y el commit señalado por `HEAD`. Recibe como entrada las rutas y el estado de origen seleccionados por los argumentos. La operación consiste en registrar en el historial el contenido preparado en el índice.

Puede persistir el estado implicado por esta operación: registrar en el historial el contenido preparado en el índice. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Ejemplo mínimo

```bash
git add guia.txt
git commit -m "Añade el primer capítulo"
```

La invocación `git commit -m "Añade el primer capítulo"` ejecuta esta operación: registrar en el historial el contenido preparado en el índice. Después, `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git commit [-a | --interactive | --patch] [-s] [-v] [-u[<mode>]] [--amend]
	   [--dry-run] <commit>_ | --fixup [(amend|reword):"><commit>]
	   [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
	   [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
```

### Uso verificado con `git version 2.51.1`

```text
git commit [-a | --interactive | --patch] [-s] [-v] [-u[<mode>]] [--amend]
                  [--dry-run] [(-c | -C | --squash) <commit> | --fixup [(amend|reword):]<commit>]
                  [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
                  [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
                  [--date=<date>] [--cleanup=<mode>] [--[no-]status]
                  [-i | -o] [--pathspec-from-file=<file> [--pathspec-file-nul]]
                  [(--trailer <token>[(=|:)<value>])...] [-S[<keyid>]]
                  [--] [<pathspec>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git commit -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

registrar en el historial el contenido preparado en el índice. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git commit a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Simulación

Calcular el efecto sin escribir el estado principal. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Compara la simulación con la selección prevista.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git commit con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-a` y `--all`

Amplía la selección a todos los elementos del alcance definido.  La misma línea de ayuda también acepta `-a`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta registrar en el historial el contenido preparado en el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-a`

```bash
git commit -a -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--all`

```bash
git commit --all -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--interactive`

Abre una selección interactiva antes de aplicar la operación.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit --interactive -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--patch` y `-p`

Permite elegir hunks en vez de operar sobre el archivo completo.  La misma línea de ayuda también acepta `-p`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git commit`, parche modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--patch`

```bash
git commit --patch -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `-p`

```bash
git commit -p -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-s` y `--signoff`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-s`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git commit`, añadir Signed-off-by modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-s`

```bash
git commit -s -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--signoff`

```bash
git commit --signoff -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-v`

```bash
git commit -v -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--verbose`

```bash
git commit --verbose -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-u` y `--untracked-files`

Define cuánto detalle muestra Git sobre archivos que todavía no están en el índice. En Git 2.51.1, la ayuda corta expresa el contrato como `show untracked files, optional modes: all, normal, no. (Default: all)`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-u`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-u`

```bash
git commit -u=all -m "Añade el primer capítulo"
git status --short
```

En esta forma, `all` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--untracked-files`

```bash
git commit --untracked-files=all -m "Añade el primer capítulo"
git status --short
```

En esta forma, `all` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--amend`

Crea un commit que reemplaza el commit señalado por `HEAD` y conserva sus padres salvo que otra opción los cambie. En Git 2.51.1, la ayuda corta expresa el contrato como `amend previous commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git commit`, reemplazar el commit actual modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --amend -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --dry-run -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--fixup`

Crea un commit marcado para combinarse con otro mediante rebase autosquash. En Git 2.51.1, la ayuda corta expresa el contrato como `use autosquash formatted message to fixup or amend/reword specified commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --fixup=valor -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-F` y `--file`

Usa el archivo indicado en vez de la ubicación por defecto.  La misma línea de ayuda también acepta `-F`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `-F`

```bash
git commit -F rutas.txt -m "Añade el primer capítulo"
git status --short
```

En esta forma, `rutas.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--file`

```bash
git commit --file=rutas.txt -m "Añade el primer capítulo"
git status --short
```

En esta forma, `rutas.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-m` y `--message`

Activa mensaje durante registrar en el historial el contenido preparado en el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `commit message`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-m`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git commit`, mensaje modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-m`

```bash
git commit -m 'mensaje de ejemplo'
git status --short
```

En esta forma, `mensaje de ejemplo` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--message`

```bash
git commit --message='mensaje de ejemplo'
git status --short
```

En esta forma, `mensaje de ejemplo` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--reset-author`

Declara al committer actual como autor del commit que se vuelve a crear. En Git 2.51.1, la ayuda corta expresa el contrato como `the commit is authored by me now (used with -C/-c/--amend)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta registrar en el historial el contenido preparado en el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git commit --reset-author -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--allow-empty`

Permite continuar cuando el cambio produce un commit sin diferencias.

La opción limita o amplía el conjunto sobre el que se ejecuta registrar en el historial el contenido preparado en el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git commit --allow-empty -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--allow-empty-message`

Permite crear un commit cuyo mensaje está vacío.

La opción limita o amplía el conjunto sobre el que se ejecuta registrar en el historial el contenido preparado en el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git commit --allow-empty-message -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verify`

Desactiva el comportamiento `verify` para esta invocación.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git commit --no-verify -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-e` y `--edit`

Abre la representación editable que define la orden antes de aplicarla.  La misma línea de ayuda también acepta `-e`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla edición. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque registrar en el historial el contenido preparado en el índice puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-e`

```bash
git commit -e -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--edit`

```bash
git commit --edit -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--author`

Limita el resultado a autores que coinciden con el patrón indicado. En Git 2.51.1, la ayuda corta expresa el contrato como `override author for commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta registrar en el historial el contenido preparado en el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git commit --author=Ana -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `Ana` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-c` y `--reedit-message`

Reutiliza un mensaje existente y abre el editor antes de confirmar. En Git 2.51.1, la ayuda corta expresa el contrato como `reuse and edit message from specified commit`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-c`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git commit`, reedit mensaje modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-c`

```bash
git commit -c HEAD -m "Añade el primer capítulo"
git status --short
```

En esta forma, `HEAD` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--reedit-message`

```bash
git commit --reedit-message=HEAD -m "Añade el primer capítulo"
git status --short
```

En esta forma, `HEAD` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-C` y `--reuse-message`

Reutiliza el mensaje y la autoría del commit indicado. En Git 2.51.1, la ayuda corta expresa el contrato como `reuse message from specified commit`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-C`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git commit`, reuse mensaje modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-C`

```bash
git commit -C HEAD -m "Añade el primer capítulo"
git status --short
```

En esta forma, `HEAD` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--reuse-message`

```bash
git commit --reuse-message=HEAD -m "Añade el primer capítulo"
git status --short
```

En esta forma, `HEAD` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--squash`

Crea un commit marcado para fusionar cambios y mensajes durante rebase autosquash. En Git 2.51.1, la ayuda corta expresa el contrato como `use autosquash formatted message to squash specified commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --squash=HEAD -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--date`

Controla la representación o selección por fecha.

En `git commit`, fecha modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --date=2026-01-15 -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `2026-01-15` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cleanup`

Selecciona cómo Git retira comentarios y espacios del mensaje antes de crear el commit.

En `git commit`, cleanup modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --cleanup=all -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--status`

Incluye estado en la entrada, el resultado o el registro que construye `git commit`. En Git 2.51.1, la ayuda corta expresa el contrato como `include status in commit message template`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --status -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-i` y `--include`

Incluye elementos adicionales dentro del alcance indicado.  La misma línea de ayuda también acepta `-i`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta registrar en el historial el contenido preparado en el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-i`

```bash
git commit -i -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--include`

```bash
git commit --include -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-o` y `--only`

Limita registrar en el historial el contenido preparado en el índice al alcance identificado por only. En Git 2.51.1, la ayuda corta expresa el contrato como `commit only specified files`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-o`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `-o`

```bash
git commit -o -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--only`

```bash
git commit --only -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--pathspec-from-file`

Lee pathspecs desde un archivo o desde stdin.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit --pathspec-from-file=rutas.txt -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pathspec-file-nul`

Interpreta los pathspecs de archivo como registros terminados en NUL.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit --pathspec-file-nul -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--trailer`

Incluye trailer en la entrada, el resultado o el registro que construye `git commit`. En Git 2.51.1, la ayuda corta expresa el contrato como `add custom trailer(s)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git commit`, trailer modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --trailer=valor -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-S` y `--gpg-sign`

Activa gpg sign durante registrar en el historial el contenido preparado en el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign commit`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-S`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git commit`, gpg sign modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-S`

```bash
git commit -S=user.name -m "Añade el primer capítulo"
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--gpg-sign`

```bash
git commit --gpg-sign=user.name -m "Añade el primer capítulo"
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git commit -q -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--quiet`

```bash
git commit --quiet -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-t` y `--template`

Usa el directorio indicado como fuente de plantillas para crear archivos iniciales dentro del nuevo repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `use specified template file`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-t`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `-t`

```bash
git commit -t rutas.txt -m "Añade el primer capítulo"
git status --short
```

En esta forma, `rutas.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--template`

```bash
git commit --template=../plantillas -m "Añade el primer capítulo"
git status --short
```

En esta forma, `../plantillas` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-U` y `--unified`

Define cuántas líneas de contexto rodean cada hunk.  La misma línea de ayuda también acepta `-U`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git commit`, unified modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-U`

```bash
git commit -U 5 -m "Añade el primer capítulo"
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--unified`

```bash
git commit --unified=5 -m "Añade el primer capítulo"
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--inter-hunk-context`

Fusiona hunks cercanos cuando la distancia no supera el límite indicado.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --inter-hunk-context=5 -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-n`

Comprueba n antes de aceptar el resultado de `git commit`. En Git 2.51.1, la ayuda corta expresa el contrato como `bypass pre-commit and commit-msg hooks`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `--no-verify`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git commit -n -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git commit --verify -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--short`

Incluye short en la salida o cambia cómo `git commit` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show status concisely`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --short -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--branch`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --branch -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ahead-behind`

Calcula cuántos commits separan una rama de su upstream. En Git 2.51.1, la ayuda corta expresa el contrato como `compute full ahead/behind values`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git commit`, ahead behind modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --ahead-behind -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--porcelain`

Produce un contrato de salida destinado a scripts.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --porcelain -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--long`

Incluye long en la salida o cambia cómo `git commit` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show status in long format (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --long -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z` y `--null`

Usa NUL como terminador para conservar cualquier byte válido de un nombre.  La misma línea de ayuda también acepta `-z`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git commit`, terminación NUL modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-z`

```bash
git commit -z -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--null`

```bash
git commit --null -m "Añade el primer capítulo"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-post-rewrite`

Desactiva el comportamiento `post-rewrite` para esta invocación.

En `git commit`, desactivar post rewrite modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --no-post-rewrite -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--post-rewrite`

Selecciona la relación indicada por post rewrite; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-post-rewrite`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git commit`, post rewrite modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --post-rewrite -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-interactive`

Desactiva para esta invocación el comportamiento que habilita `--interactive`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit --no-interactive -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-patch`

Desactiva para esta invocación el comportamiento que habilita `--patch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git commit`, desactivar parche modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --no-patch -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-amend`

Desactiva para esta invocación el comportamiento que habilita `--amend`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git commit`, desactivar reemplazar el commit actual modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --no-amend -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-dry-run`

Desactiva para esta invocación el comportamiento que habilita `--dry-run`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --no-dry-run -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-fixup`

Desactiva para esta invocación el comportamiento que habilita `--fixup`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --no-fixup -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reset-author`

Desactiva para esta invocación el comportamiento que habilita `--reset-author`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta registrar en el historial el contenido preparado en el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git commit --no-reset-author -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-author`

Desactiva para esta invocación el comportamiento que habilita `--author`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta registrar en el historial el contenido preparado en el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git commit --no-author -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-squash`

Desactiva para esta invocación el comportamiento que habilita `--squash`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --no-squash -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-date`

Desactiva para esta invocación el comportamiento que habilita `--date`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git commit`, desactivar fecha modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --no-date -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cleanup`

Desactiva para esta invocación el comportamiento que habilita `--cleanup`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git commit`, desactivar cleanup modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --no-cleanup -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-status`

Desactiva para esta invocación el comportamiento que habilita `--status`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --no-status -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-pathspec-from-file`

Desactiva para esta invocación el comportamiento que habilita `--pathspec-from-file`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit --no-pathspec-from-file -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-pathspec-file-nul`

Desactiva para esta invocación el comportamiento que habilita `--pathspec-file-nul`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit --no-pathspec-file-nul -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --no-quiet -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --no-verbose -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-file`

Desactiva para esta invocación el comportamiento que habilita `--file`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit --no-file -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-message`

Desactiva para esta invocación el comportamiento que habilita `--message`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git commit`, desactivar mensaje modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --no-message
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reedit-message`

Desactiva para esta invocación el comportamiento que habilita `--reedit-message`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git commit`, desactivar reedit mensaje modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --no-reedit-message -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reuse-message`

Desactiva para esta invocación el comportamiento que habilita `--reuse-message`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git commit`, desactivar reuse mensaje modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --no-reuse-message -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signoff`

Desactiva para esta invocación el comportamiento que habilita `--signoff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git commit`, desactivar añadir Signed-off-by modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --no-signoff -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-template`

Desactiva para esta invocación el comportamiento que habilita `--template`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit --no-template -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-edit`

Conserva el mensaje existente sin abrir el editor.

La opción controla desactivar edición. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque registrar en el historial el contenido preparado en el índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git commit --no-edit -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gpg-sign`

Desactiva para esta invocación el comportamiento que habilita `--gpg-sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git commit`, desactivar gpg sign modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --no-gpg-sign -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-all`

Desactiva para esta invocación el comportamiento que habilita `--all`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta registrar en el historial el contenido preparado en el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git commit --no-all -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-include`

Desactiva para esta invocación el comportamiento que habilita `--include`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta registrar en el historial el contenido preparado en el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git commit --no-include -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-only`

Desactiva para esta invocación el comportamiento que habilita `--only`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit --no-only -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-short`

Desactiva para esta invocación el comportamiento que habilita `--short`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --no-short -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-branch`

Desactiva para esta invocación el comportamiento que habilita `--branch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --no-branch -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ahead-behind`

Desactiva para esta invocación el comportamiento que habilita `--ahead-behind`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git commit`, desactivar ahead behind modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --no-ahead-behind -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-porcelain`

Desactiva para esta invocación el comportamiento que habilita `--porcelain`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --no-porcelain -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-long`

Desactiva para esta invocación el comportamiento que habilita `--long`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --no-long -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-null`

Desactiva para esta invocación el comportamiento que habilita `--null`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git commit`, desactivar terminación NUL modifica la forma en que se ejecuta registrar en el historial el contenido preparado en el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit --no-null -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-untracked-files`

Desactiva para esta invocación el comportamiento que habilita `--untracked-files`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git commit --no-untracked-files -m "Añade el primer capítulo"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El cambio no entra al commit

Comprueba esta causa: El índice no contiene la versión esperada. Compara `git diff` con `git diff --cached`.

### Un pathspec no coincide

Comprueba esta causa: La ruta se evalúa desde otro directorio o está ignorada. Usa `git status --short --untracked-files=all` y separa opciones con `--`.

### Se reemplaza contenido local

Comprueba esta causa: La orden escribe el área de trabajo. Guarda el diff o crea un stash antes de repetir la operación.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: registrar en el historial el contenido preparado en el índice. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git mv`](../basic-snapshotting/mv.md)
- [`git add`](../basic-snapshotting/add.md)
- [`git notes`](../basic-snapshotting/notes.md)

## Fuente

- [git-commit - Record changes to the repository](https://git-scm.com/docs/git-commit)
