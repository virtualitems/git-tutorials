---
title: "git merge"
source: "https://git-scm.com/docs/git-merge"
section: "branching-and-merging"
status: "option-expanded"
---

# `git merge`

Este caso usa `git merge` para integrar una o más líneas de desarrollo en la rama actual. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git merge consulta o cambia referencias, `HEAD`, worktrees y estados de integración. Recibe como entrada las ramas, commits o rutas que participan en la operación. La operación consiste en integrar una o más líneas de desarrollo en la rama actual.

Puede persistir el estado implicado por esta operación: integrar una o más líneas de desarrollo en la rama actual. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git switch main
git merge tema-portada
```

La invocación `git merge tema-portada` ejecuta esta operación: integrar una o más líneas de desarrollo en la rama actual. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git merge [-n] [--stat] [--compact-summary] [--no-commit] [--squash] [--[no-]edit]
	[--no-verify] [-s <strategy>] [-X <strategy-option>] [-S[<keyid>]]
	[--[no-]allow-unrelated-histories]
	[--[no-]rerere-autoupdate] [-m <msg>] [-F <file>]
```

### Uso verificado con `git version 2.51.1`

```text
git merge [<options>] [<commit>...]
   or: git merge --abort
   or: git merge --continue
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git merge -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

integrar una o más líneas de desarrollo en la rama actual. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git merge a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Sesión interrumpida

Continuar o cancelar una secuencia después de revisar el estado. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Consulta `git status` antes de elegir la acción.

### Validación

Comprobar el resultado de git merge con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-n`

Impide n durante esta invocación de `git merge`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not show a diffstat at the end of the merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git merge -n tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stat`

Resume cambios mediante conteos por ruta.

Esta forma se usa cuando `git merge` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque estadísticas actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git merge --stat tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--compact-summary`

Incluye compact summary en la salida o cambia cómo `git merge` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show a compact-summary at the end of the merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git merge --compact-summary tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-commit`

Desactiva el comportamiento `commit` para esta invocación.

En `git merge`, desactivar commit modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --no-commit tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--squash`

Crea un commit marcado para fusionar cambios y mensajes durante rebase autosquash. En Git 2.51.1, la ayuda corta expresa el contrato como `create a single commit instead of doing a merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge`, squash modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --squash tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--edit` y `-e`

Abre la representación editable que define la orden antes de aplicarla.  La misma línea de ayuda también acepta `-e`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git merge`, edición modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--edit`

```bash
git merge --edit tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `-e`

```bash
git merge -e tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-verify`

Desactiva el comportamiento `verify` para esta invocación.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git merge --no-verify tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-s` y `--strategy`

Selecciona el algoritmo o estrategia que procesa la entrada.  La misma línea de ayuda también acepta `-s`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción selecciona el procedimiento que `git merge` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `-s`

```bash
git merge -s ort tema-portada
git status --short
```

En esta forma, `ort` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--strategy`

```bash
git merge --strategy=ort tema-portada
git status --short
```

En esta forma, `ort` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-X` y `--strategy-option`

Selecciona el algoritmo o estrategia que procesa la entrada.  La misma línea de ayuda también acepta `-X`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción selecciona el procedimiento que `git merge` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `-X`

```bash
git merge -X Ana tema-portada
git status --short
```

En esta forma, `Ana` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--strategy-option`

```bash
git merge --strategy-option=Ana tema-portada
git status --short
```

En esta forma, `Ana` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-S` y `--gpg-sign`

Activa gpg sign durante integrar una o más líneas de desarrollo en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign commit`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-S`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git merge`, gpg sign modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-S`

```bash
git merge -S=user.name tema-portada
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--gpg-sign`

```bash
git merge --gpg-sign=user.name tema-portada
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--allow-unrelated-histories`

Permite permitir unrelated histories cuando la forma predeterminada de `git merge` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow merging unrelated histories`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git merge --allow-unrelated-histories tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--rerere-autoupdate`

Actualiza rerere autoupdate como parte de integrar una o más líneas de desarrollo en la rama actual. En Git 2.51.1, la ayuda corta expresa el contrato como `update the index with reused conflict resolution if possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge`, rerere autoupdate modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --rerere-autoupdate tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--message`

Activa mensaje durante integrar una o más líneas de desarrollo en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `merge commit message (for a non-fast-forward merge)`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-m`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git merge`, mensaje modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-m`

```bash
git merge -m 'mensaje de ejemplo' tema-portada
git status --short
```

En esta forma, `mensaje de ejemplo` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--message`

```bash
git merge --message='mensaje de ejemplo' tema-portada
git status --short
```

En esta forma, `mensaje de ejemplo` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-F` y `--file`

Usa el archivo indicado en vez de la ubicación por defecto.  La misma línea de ayuda también acepta `-F`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia cómo `git merge` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `-F`

```bash
git merge -F archivo.txt tema-portada
git status --short
```

En esta forma, `archivo.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--file`

```bash
git merge --file=archivo.txt tema-portada
git status --short
```

En esta forma, `archivo.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--abort`

Cancela la secuencia y restaura el punto que la orden registró al comenzar.

Esta forma se usa cuando `git merge` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque abortar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git merge --abort
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--continue`

Reanuda una secuencia pausada después de resolver su estado.

Esta forma se usa cuando `git merge` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque continuar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git merge --continue
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--summary`

Activa summary durante integrar una o más líneas de desarrollo en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `(synonym to --stat)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git merge --summary tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--log`

Incluye log en la entrada, el resultado o el registro que construye `git merge`. En Git 2.51.1, la ayuda corta expresa el contrato como `add (at most <n>) entries from shortlog to merge commit message`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge`, log modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --log=5 tema-portada
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--commit`

Ejecuta commit durante integrar una o más líneas de desarrollo en la rama actual. En Git 2.51.1, la ayuda corta expresa el contrato como `perform a commit if the merge succeeds (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge`, commit modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --commit tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cleanup`

Selecciona cómo Git retira comentarios y espacios del mensaje antes de crear el commit.

En `git merge`, cleanup modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --cleanup=all tema-portada
git status --short
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ff`

Permite ff cuando la forma predeterminada de `git merge` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow fast-forward (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git merge --ff tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ff-only`

Limita integrar una o más líneas de desarrollo en la rama actual al alcance identificado por ff only. En Git 2.51.1, la ayuda corta expresa el contrato como `abort if fast-forward is not possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git merge` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque ff only actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git merge --ff-only tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify-signatures`

Valida el dato o estado antes de producir el resultado.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git merge --verify-signatures tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--into-name`

Define into nombre para esta ejecución de `git merge`. En Git 2.51.1, la ayuda corta expresa el contrato como `use <name> instead of the real target`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge`, into nombre modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --into-name=tema tema-portada
git status --short
```

El ejemplo usa `tema` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-v`

```bash
git merge -v tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--verbose`

```bash
git merge --verbose tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git merge -q tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--quiet`

```bash
git merge --quiet tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--quit`

Sale de la secuencia y conserva el estado que la documentación define.

Esta forma se usa cuando `git merge` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque salir actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git merge --quit
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

La opción controla progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque integrar una o más líneas de desarrollo en la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git merge --progress tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--autostash`

Activa autostash durante integrar una o más líneas de desarrollo en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `automatically stash/stash pop before and after`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git merge --autostash tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--overwrite-ignore`

Excluye elementos que cumplan la condición indicada.

La opción controla overwrite ignorar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque integrar una o más líneas de desarrollo en la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git merge --overwrite-ignore tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signoff`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git merge`, añadir Signed-off-by modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --signoff tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git merge --verify tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stat`

Desactiva para esta invocación el comportamiento que habilita `--stat`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git merge --no-stat tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-compact-summary`

Desactiva para esta invocación el comportamiento que habilita `--compact-summary`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git merge --no-compact-summary tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-squash`

Desactiva para esta invocación el comportamiento que habilita `--squash`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge`, desactivar squash modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --no-squash tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-edit`

Conserva el mensaje existente sin abrir el editor.

En `git merge`, desactivar edición modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --no-edit tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-allow-unrelated-histories`

Desactiva para esta invocación el comportamiento que habilita `--allow-unrelated-histories`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git merge --no-allow-unrelated-histories tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-rerere-autoupdate`

Desactiva para esta invocación el comportamiento que habilita `--rerere-autoupdate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge`, desactivar rerere autoupdate modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --no-rerere-autoupdate tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-abort`

Desactiva para esta invocación el comportamiento que habilita `--abort`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

Esta forma se usa cuando `git merge` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque desactivar abortar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git merge --no-abort tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-continue`

Desactiva para esta invocación el comportamiento que habilita `--continue`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

Esta forma se usa cuando `git merge` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque desactivar continuar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git merge --no-continue tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-summary`

Desactiva para esta invocación el comportamiento que habilita `--summary`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git merge --no-summary tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-log`

Desactiva para esta invocación el comportamiento que habilita `--log`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge`, desactivar log modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --no-log tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cleanup`

Desactiva para esta invocación el comportamiento que habilita `--cleanup`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge`, desactivar cleanup modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --no-cleanup tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ff`

Desactiva para esta invocación el comportamiento que habilita `--ff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git merge --no-ff tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verify-signatures`

Desactiva para esta invocación el comportamiento que habilita `--verify-signatures`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git merge --no-verify-signatures tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-strategy`

Desactiva para esta invocación el comportamiento que habilita `--strategy`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción selecciona el procedimiento que `git merge` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git merge --no-strategy tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-strategy-option`

Desactiva para esta invocación el comportamiento que habilita `--strategy-option`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción selecciona el procedimiento que `git merge` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git merge --no-strategy-option tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-message`

Desactiva para esta invocación el comportamiento que habilita `--message`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge`, desactivar mensaje modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --no-message tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-into-name`

Desactiva para esta invocación el comportamiento que habilita `--into-name`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge`, desactivar into nombre modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --no-into-name tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git merge --no-verbose tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git merge --no-quiet tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quit`

Desactiva para esta invocación el comportamiento que habilita `--quit`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

Esta forma se usa cuando `git merge` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque desactivar salir actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git merge --no-quit tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque integrar una o más líneas de desarrollo en la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git merge --no-progress tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gpg-sign`

Desactiva para esta invocación el comportamiento que habilita `--gpg-sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge`, desactivar gpg sign modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --no-gpg-sign tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-autostash`

Desactiva para esta invocación el comportamiento que habilita `--autostash`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git merge --no-autostash tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-overwrite-ignore`

Desactiva para esta invocación el comportamiento que habilita `--overwrite-ignore`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar overwrite ignorar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque integrar una o más líneas de desarrollo en la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git merge --no-overwrite-ignore tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signoff`

Desactiva para esta invocación el comportamiento que habilita `--signoff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git merge`, desactivar añadir Signed-off-by modifica la forma en que se ejecuta integrar una o más líneas de desarrollo en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git merge --no-signoff tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git merge` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La referencia es ambigua

Comprueba esta causa: Un nombre coincide con más de un objeto o una ruta. Usa `--` para separar rutas y una revisión completa para el objeto.

### El cambio de rama se rechaza

Comprueba esta causa: Hay modificaciones que serían sobrescritas. Confirma el estado y decide entre commit, stash o descarte.

### La integración se detiene

Comprueba esta causa: Dos cambios afectan la misma región o ruta. Resuelve, añade los archivos y usa la orden `--continue` o `--abort` que corresponda.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: integrar una o más líneas de desarrollo en la rama actual. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git mergetool`](../branching-and-merging/mergetool.md)
- [`git history`](../branching-and-merging/history.md)
- [`git merge-tree`](../branching-and-merging/merge-tree.md)

## Fuente

- [git-merge - Join two or more development histories together](https://git-scm.com/docs/git-merge)
