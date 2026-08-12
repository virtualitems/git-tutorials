---
title: "git tag"
source: "https://git-scm.com/docs/git-tag"
section: "branching-and-merging"
status: "option-expanded"
---

# `git tag`

Este caso usa `git tag` para crear, listar, verificar y eliminar etiquetas. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git tag consulta o cambia referencias, `HEAD`, worktrees y estados de integración. Recibe como entrada las ramas, commits o rutas que participan en la operación. La operación consiste en crear, listar, verificar y eliminar etiquetas.

Puede persistir el estado implicado por esta operación: crear, listar, verificar y eliminar etiquetas. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git tag -a v1.0 -m "Primera entrega"
git show v1.0
```

La invocación `git tag -a v1.0 -m "Primera entrega"` ejecuta esta operación: crear, listar, verificar y eliminar etiquetas. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git tag [-a | -s | -u <key-id>] [-f] [-m <msg> | -F <file>] [-e]
	[(--trailer <token>[(=|:)<value>])…]
	<tagname> [<commit> | <object>]
git tag -d <tagname>…
```

### Uso verificado con `git version 2.51.1`

```text
git tag [-a | -s | -u <key-id>] [-f] [-m <msg> | -F <file>] [-e]
               [(--trailer <token>[(=|:)<value>])...]
               <tagname> [<commit> | <object>]
   or: git tag -d <tagname>...
   or: git tag [-n[<num>]] -l [--contains <commit>] [--no-contains <commit>]
               [--points-at <object>] [--column[=<options>] | --no-column]
               [--create-reflog] [--sort=<key>] [--format=<format>]
               [--merged <commit>] [--no-merged <commit>] [<pattern>...]
   or: git tag -v [--format=<format>] <tagname>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git tag -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

crear, listar, verificar y eliminar etiquetas. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git tag a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git tag con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-a` y `--annotate`

Activa annotate durante crear, listar, verificar y eliminar etiquetas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `annotated tag, needs a message`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-a`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta crear, listar, verificar y eliminar etiquetas. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-a`

```bash
git tag -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--annotate`

```bash
git tag --annotate v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-s` y `--sign`

Activa sign durante crear, listar, verificar y eliminar etiquetas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `annotated and GPG-signed tag`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-s`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta crear, listar, verificar y eliminar etiquetas. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-s`

```bash
git tag -s -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--sign`

```bash
git tag --sign -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-u` y `--local-user`

Define alcance local user para esta ejecución de `git tag`. En Git 2.51.1, la ayuda corta expresa el contrato como `use another key to sign the tag`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-u`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta crear, listar, verificar y eliminar etiquetas. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-u`

```bash
git tag -u user.name -a v1.0 -m "Primera entrega"
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--local-user`

```bash
git tag --local-user=user.name -a v1.0 -m "Primera entrega"
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.  La misma línea de ayuda también acepta `-f`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque crear, listar, verificar y eliminar etiquetas puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-f`

```bash
git tag -f -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--force`

```bash
git tag --force -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-m` y `--message`

Activa mensaje durante crear, listar, verificar y eliminar etiquetas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `tag message`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-m`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta crear, listar, verificar y eliminar etiquetas. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-m`

```bash
git tag -m 'mensaje de ejemplo' -a v1.0
git status --short
```

En esta forma, `mensaje de ejemplo` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--message`

```bash
git tag --message='mensaje de ejemplo' -a v1.0
git status --short
```

En esta forma, `mensaje de ejemplo` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-F` y `--file`

Usa el archivo indicado en vez de la ubicación por defecto.  La misma línea de ayuda también acepta `-F`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia cómo `git tag` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `-F`

```bash
git tag -F rutas.txt -a v1.0 -m "Primera entrega"
git status --short
```

En esta forma, `rutas.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--file`

```bash
git tag --file=rutas.txt -a v1.0 -m "Primera entrega"
git status --short
```

En esta forma, `rutas.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-e` y `--edit`

Abre la representación editable que define la orden antes de aplicarla.  La misma línea de ayuda también acepta `-e`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla edición. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque crear, listar, verificar y eliminar etiquetas puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-e`

```bash
git tag -e -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--edit`

```bash
git tag --edit -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--trailer`

Incluye trailer en la entrada, el resultado o el registro que construye `git tag`. En Git 2.51.1, la ayuda corta expresa el contrato como `add custom trailer(s)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git tag`, trailer modifica la forma en que se ejecuta crear, listar, verificar y eliminar etiquetas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git tag --trailer=valor -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d` y `--delete`

Elimina el elemento seleccionado.  La misma línea de ayuda también acepta `-d`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla eliminar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque crear, listar, verificar y eliminar etiquetas puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-d`

```bash
git tag -d -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--delete`

```bash
git tag --delete -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-n`

Incluye n en la salida o cambia cómo `git tag` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print <n> lines of each tag message`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag -n 5 -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-l` y `--list`

Incluye información adicional en la salida.  La misma línea de ayuda también acepta `-l`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta crear, listar, verificar y eliminar etiquetas. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-l`

```bash
git tag -l -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--list`

```bash
git tag --list -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--contains`

Filtra referencias cuyo historial contiene el commit indicado.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --contains=HEAD -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-contains`

Filtra referencias cuyo historial no contiene el commit indicado.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --no-contains -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--points-at`

Limita crear, listar, verificar y eliminar etiquetas al alcance identificado por points at. En Git 2.51.1, la ayuda corta expresa el contrato como `print only tags of the object`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --points-at=HEAD -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--column`

Incluye column en la salida o cambia cómo `git tag` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show tag list in columns`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --column=short -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-column`

Desactiva el comportamiento `column` para esta invocación.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --no-column -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--create-reflog`

Permite crear o escribir el elemento seleccionado.

En `git tag`, crear reflog modifica la forma en que se ejecuta crear, listar, verificar y eliminar etiquetas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git tag --create-reflog -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sort`

Ordena registros por el campo indicado.

En `git tag`, ordenar modifica la forma en que se ejecuta crear, listar, verificar y eliminar etiquetas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git tag --sort=user.name -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `user.name` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--format`

Define los campos y separadores de la salida.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --format=oneline -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--merged`

Filtra elementos ya alcanzables desde la revisión indicada.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --merged=HEAD -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-merged`

Filtra elementos no alcanzables desde la revisión indicada.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --no-merged -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta crear, listar, verificar y eliminar etiquetas. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-v`

```bash
git tag -v -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--verify`

```bash
git tag --verify -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--cleanup`

Selecciona cómo Git retira comentarios y espacios del mensaje antes de crear el commit.

En `git tag`, cleanup modifica la forma en que se ejecuta crear, listar, verificar y eliminar etiquetas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git tag --cleanup=all -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--omit-empty`

Impide omit vacío durante esta invocación de `git tag`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not output a newline after empty formatted refs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --omit-empty -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--color`

Controla el uso de secuencias de color en la salida.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --color=always -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `always` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-i` y `--ignore-case`

Excluye elementos que cumplan la condición indicada.  La misma línea de ayuda también acepta `-i`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta crear, listar, verificar y eliminar etiquetas. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-i`

```bash
git tag -i -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--ignore-case`

```bash
git tag --ignore-case -a v1.0 -m "Primera entrega"
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-points-at`

Desactiva para esta invocación el comportamiento que habilita `--points-at`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --no-points-at -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-create-reflog`

Desactiva para esta invocación el comportamiento que habilita `--create-reflog`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git tag`, desactivar crear reflog modifica la forma en que se ejecuta crear, listar, verificar y eliminar etiquetas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git tag --no-create-reflog -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-sort`

Desactiva para esta invocación el comportamiento que habilita `--sort`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git tag`, desactivar ordenar modifica la forma en que se ejecuta crear, listar, verificar y eliminar etiquetas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git tag --no-sort -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-format`

Desactiva para esta invocación el comportamiento que habilita `--format`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --no-format -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-annotate`

Desactiva para esta invocación el comportamiento que habilita `--annotate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear, listar, verificar y eliminar etiquetas. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git tag --no-annotate v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-file`

Desactiva para esta invocación el comportamiento que habilita `--file`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git tag` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git tag --no-file -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-edit`

Conserva el mensaje existente sin abrir el editor.

La opción controla desactivar edición. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque crear, listar, verificar y eliminar etiquetas puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git tag --no-edit -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-sign`

Desactiva para esta invocación el comportamiento que habilita `--sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear, listar, verificar y eliminar etiquetas. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git tag --no-sign -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cleanup`

Desactiva para esta invocación el comportamiento que habilita `--cleanup`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git tag`, desactivar cleanup modifica la forma en que se ejecuta crear, listar, verificar y eliminar etiquetas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git tag --no-cleanup -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-local-user`

Desactiva para esta invocación el comportamiento que habilita `--local-user`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear, listar, verificar y eliminar etiquetas. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git tag --no-local-user -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force`

Desactiva para esta invocación el comportamiento que habilita `--force`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque crear, listar, verificar y eliminar etiquetas puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git tag --no-force -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-omit-empty`

Desactiva para esta invocación el comportamiento que habilita `--omit-empty`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --no-omit-empty -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-color`

Desactiva para esta invocación el comportamiento que habilita `--color`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git tag --no-color -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-case`

Desactiva para esta invocación el comportamiento que habilita `--ignore-case`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear, listar, verificar y eliminar etiquetas. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git tag --no-ignore-case -a v1.0 -m "Primera entrega"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git tag` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La referencia es ambigua

Comprueba esta causa: Un nombre coincide con más de un objeto o una ruta. Usa `--` para separar rutas y una revisión completa para el objeto.

### El cambio de rama se rechaza

Comprueba esta causa: Hay modificaciones que serían sobrescritas. Confirma el estado y decide entre commit, stash o descarte.

### La integración se detiene

Comprueba esta causa: Dos cambios afectan la misma región o ruta. Resuelve, añade los archivos y usa la orden `--continue` o `--abort` que corresponda.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: crear, listar, verificar y eliminar etiquetas. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git worktree`](../branching-and-merging/worktree.md)
- [`git switch`](../branching-and-merging/switch.md)
- [`git stash`](../branching-and-merging/stash.md)

## Fuente

- [git-tag - Create, list, delete or verify tags](https://git-scm.com/docs/git-tag)
