---
title: "git rebase"
source: "https://git-scm.com/docs/git-rebase"
section: "patching"
status: "option-expanded"
---

# `git rebase`

Este caso usa `git rebase` para reaplicar commits sobre una base distinta. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git rebase aplica diffs o commits y mantiene un estado que puede continuar o abortarse. Recibe como entrada un parche, un commit o un rango que representa cambios. La operación consiste en reaplicar commits sobre una base distinta.

Puede persistir el estado implicado por esta operación: reaplicar commits sobre una base distinta. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Ejemplo mínimo

```bash
git switch tema-portada
git rebase main
```

La invocación `git rebase main` ejecuta esta operación: reaplicar commits sobre una base distinta. Después, el diff y el historial muestran si cambiaron archivos, índice o commits. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git rebase [-i | --interactive] [<options>] [--exec <cmd>]
	[--onto <newbase> | --keep-base] [<upstream> [<branch>]]
git rebase [-i | --interactive] [<options>] [--exec <cmd>] [--onto <newbase>]
	--root [<branch>]
```

### Uso verificado con `git version 2.51.1`

```text
git rebase [-i] [options] [--exec <cmd>] [--onto <newbase> | --keep-base] [<upstream> [<branch>]]
   or: git rebase [-i] [options] [--exec <cmd>] [--onto <newbase>] --root [<branch>]
   or: git rebase --continue | --abort | --skip | --edit-todo
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git rebase -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

reaplicar commits sobre una base distinta. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git rebase a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Sesión interrumpida

Continuar o cancelar una secuencia después de revisar el estado. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Consulta `git status` antes de elegir la acción.

### Validación

Comprobar el resultado de git rebase con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-i` y `--interactive`

Abre una selección interactiva antes de aplicar la operación.  La misma línea de ayuda también acepta `-i`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git rebase`, selección interactiva modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-i`

```bash
git rebase -i main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--interactive`

```bash
git rebase --interactive main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--exec` y `-x`

Incluye exec en la entrada, el resultado o el registro que construye `git rebase`. En Git 2.51.1, la ayuda corta expresa el contrato como `add exec lines after each commit of the editable list`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-x`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git rebase`, exec modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--exec`

```bash
git rebase --exec=valor main
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `-x`

```bash
git rebase -x valor main
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--onto`

Activa onto durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `rebase onto given branch instead of upstream`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --onto=valor main
git status --short
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-base`

Define conservar base para esta ejecución de `git rebase`. En Git 2.51.1, la ayuda corta expresa el contrato como `use the merge-base of upstream and branch as the current base`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --keep-base main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--root`

Activa root durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `rebase all reachable commits up to the root(s)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --root main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--continue`

Reanuda una secuencia pausada después de resolver su estado.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque continuar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git rebase --continue
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--abort`

Cancela la secuencia y restaura el punto que la orden registró al comenzar.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque abortar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git rebase --abort
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--skip`

Omite el elemento actual y continúa la secuencia.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque omitir el elemento actual actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git rebase --skip
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--edit-todo`

Incluye edición todo en la salida o cambia cómo `git rebase` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `edit the todo list during an interactive rebase`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git rebase`, edición todo modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --edit-todo main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verify`

Desactiva el comportamiento `verify` para esta invocación.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git rebase --no-verify main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git rebase --verify main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git rebase -q main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--quiet`

```bash
git rebase --quiet main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-stat`

Desactiva el comportamiento `stat` para esta invocación.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git rebase --no-stat main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-v`

```bash
git rebase -v main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--verbose`

```bash
git rebase --verbose main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-n`

Impide n durante esta invocación de `git rebase`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not show diffstat of what changed upstream`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `--no-stat`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git rebase -n main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stat`

Resume cambios mediante conteos por ruta.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque estadísticas actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git rebase --stat main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signoff`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer to each commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git rebase`, añadir Signed-off-by modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --signoff main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--committer-date-is-author-date`

Aplica una fecha, duración o política de vencimiento.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --committer-date-is-author-date main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reset-author-date`

Aplica una fecha, duración o política de vencimiento.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --reset-author-date main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

En `git rebase`, C modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase -C 5 main
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-whitespace`

Excluye elementos que cumplan la condición indicada.

En `git rebase`, ignorar espacios en blanco modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --ignore-whitespace main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--whitespace`

Selecciona la acción que Git ejecuta cuando detecta errores de espacios en un parche. En Git 2.51.1, la ayuda corta expresa el contrato como `passed to 'git apply'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git rebase`, espacios en blanco modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --whitespace=warn main
git status --short
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f` y `--force-rebase`

Omite una protección concreta de la orden; requiere verificar origen y destino.  La misma línea de ayuda también acepta `-f`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla omitir la protección rebase. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque reaplicar commits sobre una base distinta puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-f`

```bash
git rebase -f main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--force-rebase`

```bash
git rebase --force-rebase main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-ff`

Desactiva el comportamiento `ff` para esta invocación.

En `git rebase`, desactivar ff modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --no-ff main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ff`

Selecciona la relación indicada por ff; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-ff`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git rebase`, ff modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --ff main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quit`

Sale de la secuencia y conserva el estado que la documentación define.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque salir actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git rebase --quit
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--show-current-patch`

Incluye información adicional en la salida.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git rebase --show-current-patch main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--apply`

Define apply para esta ejecución de `git rebase`. En Git 2.51.1, la ayuda corta expresa el contrato como `use apply strategies to rebase`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git rebase`, apply modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --apply main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--merge`

Define merge para esta ejecución de `git rebase`. En Git 2.51.1, la ayuda corta expresa el contrato como `use merging strategies to rebase`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-m`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git rebase`, merge modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-m`

```bash
git rebase -m main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--merge`

```bash
git rebase --merge main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--rerere-autoupdate`

Actualiza rerere autoupdate como parte de reaplicar commits sobre una base distinta. En Git 2.51.1, la ayuda corta expresa el contrato como `update the index with reused conflict resolution if possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git rebase`, rerere autoupdate modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --rerere-autoupdate main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--empty`

Activa vacío durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `how to handle commits that become empty`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git rebase`, vacío modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --empty=valor main
git status --short
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--autosquash`

Activa autosquash durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `move commits that begin with squash!/fixup! under -i`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git rebase`, autosquash modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --autosquash main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--update-refs`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --update-refs main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-S` y `--gpg-sign`

Activa gpg sign durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG-sign commits`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-S`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git rebase`, gpg sign modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-S`

```bash
git rebase -S=user.name main
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--gpg-sign`

```bash
git rebase --gpg-sign=user.name main
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--autostash`

Activa autostash durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `automatically stash/stash pop before and after`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --autostash main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-r` y `--rebase-merges`

Activa rebase merges durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `try to rebase merges instead of skipping them`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-r`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque rebase merges actúa sobre el estado que Git registró al iniciar la secuencia.

#### Ejemplo con `-r`

```bash
git rebase -r=all main
git status --short
```

En esta forma, `all` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--rebase-merges`

```bash
git rebase --rebase-merges=all main
git status --short
```

En esta forma, `all` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--fork-point`

Define fork point para esta ejecución de `git rebase`. En Git 2.51.1, la ayuda corta expresa el contrato como `use 'merge-base --fork-point' to refine upstream`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git rebase`, fork point modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --fork-point main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-s` y `--strategy`

Selecciona el algoritmo o estrategia que procesa la entrada.  La misma línea de ayuda también acepta `-s`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción selecciona el procedimiento que `git rebase` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `-s`

```bash
git rebase -s ort main
git status --short
```

En esta forma, `ort` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--strategy`

```bash
git rebase --strategy=ort main
git status --short
```

En esta forma, `ort` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-X` y `--strategy-option`

Selecciona el algoritmo o estrategia que procesa la entrada.  La misma línea de ayuda también acepta `-X`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción selecciona el procedimiento que `git rebase` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `-X`

```bash
git rebase -X valor main
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--strategy-option`

```bash
git rebase --strategy-option=valor main
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--reschedule-failed-exec`

Activa reschedule failed exec durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `automatically re-schedule any `exec` that fails`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --reschedule-failed-exec main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reapply-cherry-picks`

Activa reapply cherry picks durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `apply all changes, even those already present upstream`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --reapply-cherry-picks main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-exec`

Desactiva para esta invocación el comportamiento que habilita `--exec`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git rebase`, desactivar exec modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --no-exec main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-onto`

Desactiva para esta invocación el comportamiento que habilita `--onto`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --no-onto main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep-base`

Desactiva para esta invocación el comportamiento que habilita `--keep-base`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --no-keep-base main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-root`

Desactiva para esta invocación el comportamiento que habilita `--root`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --no-root main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git rebase --no-quiet main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git rebase --no-verbose main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signoff`

Desactiva para esta invocación el comportamiento que habilita `--signoff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git rebase`, desactivar añadir Signed-off-by modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --no-signoff main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-committer-date-is-author-date`

Desactiva para esta invocación el comportamiento que habilita `--committer-date-is-author-date`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --no-committer-date-is-author-date main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reset-author-date`

Desactiva para esta invocación el comportamiento que habilita `--reset-author-date`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --no-reset-author-date main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-whitespace`

Desactiva para esta invocación el comportamiento que habilita `--ignore-whitespace`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git rebase`, desactivar ignorar espacios en blanco modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --no-ignore-whitespace main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-whitespace`

Desactiva para esta invocación el comportamiento que habilita `--whitespace`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git rebase`, desactivar espacios en blanco modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --no-whitespace main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force-rebase`

Desactiva para esta invocación el comportamiento que habilita `--force-rebase`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección rebase. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque reaplicar commits sobre una base distinta puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git rebase --no-force-rebase main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-rerere-autoupdate`

Desactiva para esta invocación el comportamiento que habilita `--rerere-autoupdate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git rebase`, desactivar rerere autoupdate modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --no-rerere-autoupdate main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-autosquash`

Desactiva para esta invocación el comportamiento que habilita `--autosquash`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git rebase`, desactivar autosquash modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --no-autosquash main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-update-refs`

Desactiva para esta invocación el comportamiento que habilita `--update-refs`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --no-update-refs main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gpg-sign`

Desactiva para esta invocación el comportamiento que habilita `--gpg-sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git rebase`, desactivar gpg sign modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --no-gpg-sign main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-autostash`

Desactiva para esta invocación el comportamiento que habilita `--autostash`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --no-autostash main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-rebase-merges`

Desactiva para esta invocación el comportamiento que habilita `--rebase-merges`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque desactivar rebase merges actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git rebase --no-rebase-merges main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-fork-point`

Desactiva para esta invocación el comportamiento que habilita `--fork-point`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git rebase`, desactivar fork point modifica la forma en que se ejecuta reaplicar commits sobre una base distinta. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rebase --no-fork-point main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-strategy`

Desactiva para esta invocación el comportamiento que habilita `--strategy`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción selecciona el procedimiento que `git rebase` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git rebase --no-strategy main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-strategy-option`

Desactiva para esta invocación el comportamiento que habilita `--strategy-option`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción selecciona el procedimiento que `git rebase` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git rebase --no-strategy-option main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reschedule-failed-exec`

Desactiva para esta invocación el comportamiento que habilita `--reschedule-failed-exec`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --no-reschedule-failed-exec main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reapply-cherry-picks`

Desactiva para esta invocación el comportamiento que habilita `--reapply-cherry-picks`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta reaplicar commits sobre una base distinta. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rebase --no-reapply-cherry-picks main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rebase` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un parche no aplica

Comprueba esta causa: El contexto no coincide con el contenido actual. Inspecciona los rechazos o resuelve el conflicto antes de continuar.

### La secuencia queda en pausa

Comprueba esta causa: Git espera una resolución o una decisión. Consulta `git status` y usa `--continue`, `--skip` o `--abort`.

### El resultado contiene commits vacíos

Comprueba esta causa: Los cambios ya existen o se resolvieron sin diferencias. Revisa el diff y aplica la política de commits vacíos de la orden.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: reaplicar commits sobre una base distinta. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Trabaja en una rama de prueba. Compara `git diff`, `git diff --staged` y `git log --oneline --graph` antes y después.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git replay`](../patching/replay.md)
- [`git cherry-pick`](../patching/cherry-pick.md)
- [`git revert`](../patching/revert.md)

## Fuente

- [git-rebase - Reapply commits on top of another base tip](https://git-scm.com/docs/git-rebase)
