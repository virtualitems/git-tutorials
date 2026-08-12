---
title: "git pull"
source: "https://git-scm.com/docs/git-pull"
section: "sharing-and-updating-projects"
status: "option-expanded"
---

# `git pull`

Este caso usa `git pull` para descargar cambios e integrarlos en la rama actual. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git pull anuncia, descarga o actualiza objetos y referencias entre repositorios. Recibe como entrada el repositorio, las referencias y el sentido de la transferencia. La operación consiste en descargar cambios e integrarlos en la rama actual.

Puede persistir el estado implicado por esta operación: descargar cambios e integrarlos en la rama actual. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git pull --ff-only origin main
```

La invocación `git pull --ff-only origin main` ejecuta esta operación: descargar cambios e integrarlos en la rama actual. Después, las referencias locales y remotas permiten separar descarga, integración y publicación. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git pull [<options>] [<repository> [<refspec>…]]
```

### Uso verificado con `git version 2.51.1`

```text
git pull [<options>] [<repository> [<refspec>...]]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git pull -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

descargar cambios e integrarlos en la rama actual. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git pull a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Simulación

Calcular el efecto sin escribir el estado principal. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Compara la simulación con la selección prevista.

### Validación

Comprobar el resultado de git pull con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-v`

```bash
git pull -v --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--verbose`

```bash
git pull --verbose --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git pull -q --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--quiet`

```bash
git pull --quiet --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

La opción controla progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar cambios e integrarlos en la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git pull --progress --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

En `git pull`, recorrer submódulos modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --recurse-submodules=valor --ff-only origin main
git branch -vv
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-r` y `--rebase`

Activa rebase durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `incorporate changes by rebasing rather than merging`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-r`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git pull`, rebase modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-r`

```bash
git pull -r=valor --ff-only origin main
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--rebase`

```bash
git pull --rebase=valor --ff-only origin main
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-n`

Impide n durante esta invocación de `git pull`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not show a diffstat at the end of the merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pull -n --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stat`

Resume cambios mediante conteos por ruta.

Esta forma se usa cuando `git pull` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque estadísticas actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git pull --stat --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--compact-summary`

Incluye compact summary en la salida o cambia cómo `git pull` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show a compact-summary at the end of the merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pull --compact-summary --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--log`

Incluye log en la entrada, el resultado o el registro que construye `git pull`. En Git 2.51.1, la ayuda corta expresa el contrato como `add (at most <n>) entries from shortlog to merge commit message`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pull`, log modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --log=5 --ff-only origin main
git branch -vv
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signoff`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pull`, añadir Signed-off-by modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --signoff=valor --ff-only origin main
git branch -vv
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--squash`

Crea un commit marcado para fusionar cambios y mensajes durante rebase autosquash. En Git 2.51.1, la ayuda corta expresa el contrato como `create a single commit instead of doing a merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pull`, squash modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --squash --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--commit`

Ejecuta commit durante descargar cambios e integrarlos en la rama actual. En Git 2.51.1, la ayuda corta expresa el contrato como `perform a commit if the merge succeeds (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pull`, commit modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --commit --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--edit`

Abre la representación editable que define la orden antes de aplicarla.

En `git pull`, edición modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --edit --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cleanup`

Selecciona cómo Git retira comentarios y espacios del mensaje antes de crear el commit.

En `git pull`, cleanup modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --cleanup=all --ff-only origin main
git branch -vv
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ff`

Permite ff cuando la forma predeterminada de `git pull` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow fast-forward`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --ff --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ff-only`

Limita descargar cambios e integrarlos en la rama actual al alcance identificado por ff only. En Git 2.51.1, la ayuda corta expresa el contrato como `abort if fast-forward is not possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git pull` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque ff only actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git pull --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git pull --verify --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify-signatures`

Valida el dato o estado antes de producir el resultado.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git pull --verify-signatures --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--autostash`

Activa autostash durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `automatically stash/stash pop before and after`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --autostash --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-s` y `--strategy`

Selecciona el algoritmo o estrategia que procesa la entrada.  La misma línea de ayuda también acepta `-s`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción selecciona el procedimiento que `git pull` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `-s`

```bash
git pull -s ort --ff-only origin main
git branch -vv
```

En esta forma, `ort` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--strategy`

```bash
git pull --strategy=ort --ff-only origin main
git branch -vv
```

En esta forma, `ort` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-X` y `--strategy-option`

Selecciona el algoritmo o estrategia que procesa la entrada.  La misma línea de ayuda también acepta `-X`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción selecciona el procedimiento que `git pull` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `-X`

```bash
git pull -X Ana --ff-only origin main
git branch -vv
```

En esta forma, `Ana` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--strategy-option`

```bash
git pull --strategy-option=Ana --ff-only origin main
git branch -vv
```

En esta forma, `Ana` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-S` y `--gpg-sign`

Activa gpg sign durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign commit`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-S`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git pull`, gpg sign modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-S`

```bash
git pull -S=user.name --ff-only origin main
git branch -vv
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--gpg-sign`

```bash
git pull --gpg-sign=user.name --ff-only origin main
git branch -vv
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--allow-unrelated-histories`

Permite permitir unrelated histories cuando la forma predeterminada de `git pull` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow merging unrelated histories`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --allow-unrelated-histories --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --all --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a` y `--append`

Activa append durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `append to .git/FETCH_HEAD instead of overwriting`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-a`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git pull`, append modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-a`

```bash
git pull -a --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--append`

```bash
git pull --append --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--upload-pack`

Define upload pack con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `path to upload pack on remote end`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pull`, upload pack modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --upload-pack=archivo.txt --ff-only origin main
git branch -vv
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.  La misma línea de ayuda también acepta `-f`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar cambios e integrarlos en la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-f`

```bash
git pull -f --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--force`

```bash
git pull --force --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-t` y `--tags`

Incluye o selecciona etiquetas según la operación.  La misma línea de ayuda también acepta `-t`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-t`

```bash
git pull -t --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--tags`

```bash
git pull --tags --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-p` y `--prune`

Retira entradas que ya no cumplen la condición documentada.  La misma línea de ayuda también acepta `-p`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla podar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar cambios e integrarlos en la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-p`

```bash
git pull -p --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--prune`

```bash
git pull --prune --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-j` y `--jobs`

Define cuántas tareas puede ejecutar Git en paralelo para la operación.  La misma línea de ayuda también acepta `-j`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-j`

```bash
git pull -j=5 --ff-only origin main
git branch -vv
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--jobs`

```bash
git pull --jobs=5 --ff-only origin main
git branch -vv
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git pull --dry-run --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-k` y `--keep`

Conserva el asunto del mensaje recibido según la forma que define el comando. En Git 2.51.1, la ayuda corta expresa el contrato como `keep downloaded pack`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-k`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git pull`, conservar modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-k`

```bash
git pull -k --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--keep`

```bash
git pull --keep --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--depth`

Establece un límite numérico para la selección o el recorrido.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --depth=2 --ff-only origin main
git branch -vv
```

El ejemplo usa `2` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow-since`

Activa historial shallow desde una fecha durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `deepen history of shallow repository based on time`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --shallow-since=2026-01-15T10:00:00Z --ff-only origin main
git branch -vv
```

El ejemplo usa `2026-01-15T10:00:00Z` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow-exclude`

Excluye elementos que cumplan la condición indicada.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --shallow-exclude=refs/heads/main --ff-only origin main
git branch -vv
```

El ejemplo usa `refs/heads/main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--deepen`

Activa deepen durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `deepen history of shallow clone`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --deepen=5 --ff-only origin main
git branch -vv
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unshallow`

Activa unshallow durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `convert to a complete repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --unshallow --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--update-shallow`

Actualiza actualizar historial shallow como parte de descargar cambios e integrarlos en la rama actual.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --update-shallow --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--refmap`

Define refmap para esta ejecución de `git pull`. En Git 2.51.1, la ayuda corta expresa el contrato como `specify fetch refmap`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pull`, refmap modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --refmap=main --ff-only origin main
git branch -vv
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-o` y `--server-option`

Activa server option durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `option to transmit`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-o`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git pull`, server option modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-o`

```bash
git pull -o valor --ff-only origin main
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--server-option`

```bash
git pull --server-option=valor --ff-only origin main
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-4` y `--ipv4`

Limita descargar cambios e integrarlos en la rama actual al alcance identificado por ipv4. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv4 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-4`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git pull`, ipv4 modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-4`

```bash
git pull -4 --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--ipv4`

```bash
git pull --ipv4 --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-6` y `--ipv6`

Limita descargar cambios e integrarlos en la rama actual al alcance identificado por ipv6. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv6 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-6`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git pull`, ipv6 modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-6`

```bash
git pull -6 --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--ipv6`

```bash
git pull --ipv6 --ff-only origin main
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--negotiation-tip`

Limita descargar cambios e integrarlos en la rama actual al alcance identificado por negotiation tip. En Git 2.51.1, la ayuda corta expresa el contrato como `report that we have only objects reachable from this object`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pull`, negotiation tip modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --negotiation-tip=valor --ff-only origin main
git branch -vv
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--show-forced-updates`

Incluye información adicional en la salida.

La opción controla mostrar forced updates. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar cambios e integrarlos en la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git pull --show-forced-updates --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--set-upstream`

Configura la asociación upstream después de actualizar la referencia remota. En Git 2.51.1, la ayuda corta expresa el contrato como `set upstream for git pull/fetch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pull`, set upstream modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --set-upstream --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pull --no-verbose --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pull --no-quiet --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar cambios e integrarlos en la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git pull --no-progress --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar recorrer submódulos modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-recurse-submodules --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-rebase`

Desactiva para esta invocación el comportamiento que habilita `--rebase`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar rebase modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-rebase --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stat`

Desactiva para esta invocación el comportamiento que habilita `--stat`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pull --no-stat --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-compact-summary`

Desactiva para esta invocación el comportamiento que habilita `--compact-summary`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pull --no-compact-summary --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-log`

Desactiva para esta invocación el comportamiento que habilita `--log`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar log modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-log --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signoff`

Desactiva para esta invocación el comportamiento que habilita `--signoff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar añadir Signed-off-by modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-signoff --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-squash`

Desactiva para esta invocación el comportamiento que habilita `--squash`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar squash modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-squash --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-commit`

Desactiva para esta invocación el comportamiento que habilita `--commit`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar commit modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-commit --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-edit`

Conserva el mensaje existente sin abrir el editor.

En `git pull`, desactivar edición modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-edit --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cleanup`

Desactiva para esta invocación el comportamiento que habilita `--cleanup`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar cleanup modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-cleanup --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ff`

Desactiva para esta invocación el comportamiento que habilita `--ff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --no-ff --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verify`

Desactiva para esta invocación el comportamiento que habilita `--verify`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git pull --no-verify --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verify-signatures`

Desactiva para esta invocación el comportamiento que habilita `--verify-signatures`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git pull --no-verify-signatures --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-autostash`

Desactiva para esta invocación el comportamiento que habilita `--autostash`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --no-autostash --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-strategy`

Desactiva para esta invocación el comportamiento que habilita `--strategy`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción selecciona el procedimiento que `git pull` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git pull --no-strategy --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-strategy-option`

Desactiva para esta invocación el comportamiento que habilita `--strategy-option`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción selecciona el procedimiento que `git pull` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git pull --no-strategy-option --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gpg-sign`

Desactiva para esta invocación el comportamiento que habilita `--gpg-sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar gpg sign modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-gpg-sign --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-allow-unrelated-histories`

Desactiva para esta invocación el comportamiento que habilita `--allow-unrelated-histories`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --no-allow-unrelated-histories --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-all`

Desactiva para esta invocación el comportamiento que habilita `--all`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --no-all --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-append`

Desactiva para esta invocación el comportamiento que habilita `--append`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar append modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-append --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-upload-pack`

Desactiva para esta invocación el comportamiento que habilita `--upload-pack`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar upload pack modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-upload-pack --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force`

Desactiva para esta invocación el comportamiento que habilita `--force`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar cambios e integrarlos en la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git pull --no-force --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tags`

Desactiva para esta invocación el comportamiento que habilita `--tags`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --no-tags --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-prune`

Desactiva para esta invocación el comportamiento que habilita `--prune`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar podar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar cambios e integrarlos en la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git pull --no-prune --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-jobs`

Desactiva para esta invocación el comportamiento que habilita `--jobs`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --no-jobs --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-dry-run`

Desactiva para esta invocación el comportamiento que habilita `--dry-run`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git pull --no-dry-run --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep`

Desactiva para esta invocación el comportamiento que habilita `--keep`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar conservar modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-keep --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-depth`

Desactiva para esta invocación el comportamiento que habilita `--depth`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --no-depth --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-shallow-since`

Desactiva para esta invocación el comportamiento que habilita `--shallow-since`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --no-shallow-since --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-shallow-exclude`

Desactiva para esta invocación el comportamiento que habilita `--shallow-exclude`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --no-shallow-exclude --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-deepen`

Desactiva para esta invocación el comportamiento que habilita `--deepen`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --no-deepen --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-update-shallow`

Desactiva para esta invocación el comportamiento que habilita `--update-shallow`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar cambios e integrarlos en la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pull --no-update-shallow --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-server-option`

Desactiva para esta invocación el comportamiento que habilita `--server-option`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar server option modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-server-option --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ipv4`

Desactiva para esta invocación el comportamiento que habilita `--ipv4`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar ipv4 modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-ipv4 --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ipv6`

Desactiva para esta invocación el comportamiento que habilita `--ipv6`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar ipv6 modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-ipv6 --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-negotiation-tip`

Desactiva para esta invocación el comportamiento que habilita `--negotiation-tip`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar negotiation tip modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-negotiation-tip --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-show-forced-updates`

Desactiva para esta invocación el comportamiento que habilita `--show-forced-updates`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar mostrar forced updates. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar cambios e integrarlos en la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git pull --no-show-forced-updates --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-set-upstream`

Desactiva para esta invocación el comportamiento que habilita `--set-upstream`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pull`, desactivar set upstream modifica la forma en que se ejecuta descargar cambios e integrarlos en la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pull --no-set-upstream --ff-only origin main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El refspec no coincide

Comprueba esta causa: La parte de origen no resuelve una referencia. Comprueba la referencia local y escribe el refspec completo.

### La actualización se rechaza

Comprueba esta causa: El destino perdería commits o una política lo impide. Integra primero o usa una protección con lease tras verificar el remoto.

### La rama no tiene upstream

Comprueba esta causa: No existe asociación entre rama local y remota. Configura el upstream y confirma con `git branch -vv`.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: descargar cambios e integrarlos en la rama actual. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git push`](../sharing-and-updating-projects/push.md)
- [`git ls-remote`](../sharing-and-updating-projects/ls-remote.md)
- [`git remote`](../sharing-and-updating-projects/remote.md)

## Fuente

- [git-pull - Fetch from and integrate with another repository or a local branch](https://git-scm.com/docs/git-pull)
