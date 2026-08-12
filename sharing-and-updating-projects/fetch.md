---
title: "git fetch"
source: "https://git-scm.com/docs/git-fetch"
section: "sharing-and-updating-projects"
status: "option-expanded"
---

# `git fetch`

Este caso usa `git fetch` para descargar objetos y referencias sin integrar la rama actual. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git fetch anuncia, descarga o actualiza objetos y referencias entre repositorios. Recibe como entrada el repositorio, las referencias y el sentido de la transferencia. La operación consiste en descargar objetos y referencias sin integrar la rama actual.

Puede persistir el estado implicado por esta operación: descargar objetos y referencias sin integrar la rama actual. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git fetch origin
git log --oneline main..origin/main
```

La invocación `git fetch origin` ejecuta esta operación: descargar objetos y referencias sin integrar la rama actual. Después, las referencias locales y remotas permiten separar descarga, integración y publicación. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git fetch [<options>] [<repository> [<refspec>…]]
git fetch [<options>] <group>
git fetch --multiple [<options>] [(<repository>|<group>)…]
git fetch --all [<options>]
```

### Uso verificado con `git version 2.51.1`

```text
git fetch [<options>] [<repository> [<refspec>...]]
   or: git fetch [<options>] <group>
   or: git fetch --multiple [<options>] [(<repository> | <group>)...]
   or: git fetch --all [<options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git fetch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

descargar objetos y referencias sin integrar la rama actual. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git fetch a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Simulación

Calcular el efecto sin escribir el estado principal. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Compara la simulación con la selección prevista.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git fetch con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--multiple` y `-m`

Activa multiple durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `fetch from multiple remotes`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-m`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git fetch`, multiple modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--multiple`

```bash
git fetch --multiple origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `-m`

```bash
git fetch -m origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --all origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-v`

```bash
git fetch -v origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--verbose`

```bash
git fetch --verbose origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git fetch -q origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--quiet`

```bash
git fetch --quiet origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--set-upstream`

Configura la asociación upstream después de actualizar la referencia remota. En Git 2.51.1, la ayuda corta expresa el contrato como `set upstream for git pull/fetch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fetch`, set upstream modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --set-upstream origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a` y `--append`

Activa append durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `append to .git/FETCH_HEAD instead of overwriting`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-a`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git fetch`, append modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-a`

```bash
git fetch -a origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--append`

```bash
git fetch --append origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--atomic`

Exige que el conjunto se aplique completo o no se aplique.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git fetch --atomic origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--upload-pack`

Define upload pack con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `path to upload pack on remote end`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fetch`, upload pack modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --upload-pack=archivo.txt origin
git branch -vv
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.  La misma línea de ayuda también acepta `-f`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar objetos y referencias sin integrar la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-f`

```bash
git fetch -f origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--force`

```bash
git fetch --force origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-t` y `--tags`

Incluye o selecciona etiquetas según la operación.  La misma línea de ayuda también acepta `-t`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-t`

```bash
git fetch -t origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--tags`

```bash
git fetch --tags origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-n`

Impide n durante esta invocación de `git fetch`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not fetch all tags (--no-tags)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch -n origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tags`

Desactiva el comportamiento `tags` para esta invocación.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --no-tags origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-j` y `--jobs`

Define cuántas tareas puede ejecutar Git en paralelo para la operación. En Git 2.51.1, la ayuda corta expresa el contrato como `number of submodules fetched in parallel`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-j`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-j`

```bash
git fetch -j 5 origin
git branch -vv
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--jobs`

```bash
git fetch --jobs=5 origin
git branch -vv
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--prefetch`

Activa prefetch durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `modify the refspec to place all refs within refs/prefetch/`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --prefetch origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p` y `--prune`

Retira entradas que ya no cumplen la condición documentada.  La misma línea de ayuda también acepta `-p`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla podar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar objetos y referencias sin integrar la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-p`

```bash
git fetch -p origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--prune`

```bash
git fetch --prune origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-P` y `--prune-tags`

Selecciona o modifica referencias dentro del alcance de la orden.  La misma línea de ayuda también acepta `-P`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla podar etiquetas. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar objetos y referencias sin integrar la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-P`

```bash
git fetch -P origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--prune-tags`

```bash
git fetch --prune-tags origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

En `git fetch`, recorrer submódulos modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --recurse-submodules=valor origin
git branch -vv
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git fetch --dry-run origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--porcelain`

Produce un contrato de salida destinado a scripts.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fetch --porcelain origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--write-fetch-head`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción cambia cómo `git fetch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fetch --write-fetch-head origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-k` y `--keep`

Conserva el asunto del mensaje recibido según la forma que define el comando. En Git 2.51.1, la ayuda corta expresa el contrato como `keep downloaded pack`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-k`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git fetch`, conservar modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-k`

```bash
git fetch -k origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--keep`

```bash
git fetch --keep origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-u` y `--update-head-ok`

Selecciona o modifica referencias dentro del alcance de la orden.  La misma línea de ayuda también acepta `-u`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-u`

```bash
git fetch -u origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--update-head-ok`

```bash
git fetch --update-head-ok origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

La opción controla progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar objetos y referencias sin integrar la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git fetch --progress origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--depth`

Establece un límite numérico para la selección o el recorrido.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --depth=2 origin
git branch -vv
```

El ejemplo usa `2` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow-since`

Activa historial shallow desde una fecha durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `deepen history of shallow repository based on time`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --shallow-since=2026-01-15T10:00:00Z origin
git branch -vv
```

El ejemplo usa `2026-01-15T10:00:00Z` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow-exclude`

Excluye elementos que cumplan la condición indicada.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --shallow-exclude=refs/heads/main origin
git branch -vv
```

El ejemplo usa `refs/heads/main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--deepen`

Activa deepen durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `deepen history of shallow clone`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --deepen=5 origin
git branch -vv
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unshallow`

Activa unshallow durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `convert to a complete repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --unshallow origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--refetch`

Activa refetch durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `re-fetch without negotiating common commits`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fetch`, refetch modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --refetch origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--update-shallow`

Actualiza actualizar historial shallow como parte de descargar objetos y referencias sin integrar la rama actual.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --update-shallow origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--refmap`

Define refmap para esta ejecución de `git fetch`. En Git 2.51.1, la ayuda corta expresa el contrato como `specify fetch refmap`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fetch`, refmap modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --refmap=main origin
git branch -vv
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-o` y `--server-option`

Activa server option durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `option to transmit`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-o`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git fetch`, server option modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-o`

```bash
git fetch -o valor origin
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--server-option`

```bash
git fetch --server-option=valor origin
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-4` y `--ipv4`

Limita descargar objetos y referencias sin integrar la rama actual al alcance identificado por ipv4. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv4 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-4`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git fetch`, ipv4 modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-4`

```bash
git fetch -4 origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--ipv4`

```bash
git fetch --ipv4 origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-6` y `--ipv6`

Limita descargar objetos y referencias sin integrar la rama actual al alcance identificado por ipv6. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv6 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-6`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git fetch`, ipv6 modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-6`

```bash
git fetch -6 origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--ipv6`

```bash
git fetch --ipv6 origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--negotiation-tip`

Limita descargar objetos y referencias sin integrar la rama actual al alcance identificado por negotiation tip. En Git 2.51.1, la ayuda corta expresa el contrato como `report that we have only objects reachable from this object`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fetch`, negotiation tip modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --negotiation-tip=valor origin
git branch -vv
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--negotiate-only`

Ejecuta la negociación de objetos sin descargar el pack resultante.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fetch --negotiate-only origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--filter`

Limita los objetos transferidos mediante una especificación de filtro de clon parcial. En Git 2.51.1, la ayuda corta expresa el contrato como `object filtering`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --filter=valor origin
git branch -vv
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--auto-maintenance`

Ejecuta auto maintenance durante descargar objetos y referencias sin integrar la rama actual. En Git 2.51.1, la ayuda corta expresa el contrato como `run 'maintenance --auto' after fetching`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fetch`, auto maintenance modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --auto-maintenance origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--auto` y `--auto-gc`

Ejecuta auto gc durante descargar objetos y referencias sin integrar la rama actual. En Git 2.51.1, la ayuda corta expresa el contrato como `run 'maintenance --auto' after fetching`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `--auto-gc`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git fetch`, auto modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--auto`

```bash
git fetch --auto origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--auto-gc`

```bash
git fetch --auto-gc origin
git branch -vv
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--show-forced-updates`

Incluye información adicional en la salida.

La opción controla mostrar forced updates. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar objetos y referencias sin integrar la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git fetch --show-forced-updates origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--write-commit-graph`

Permite crear o escribir el elemento seleccionado.

En `git fetch`, write commit graph modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --write-commit-graph origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git fetch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fetch --stdin origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-multiple`

Desactiva para esta invocación el comportamiento que habilita `--multiple`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fetch`, desactivar multiple modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --no-multiple origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-all`

Desactiva para esta invocación el comportamiento que habilita `--all`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --no-all origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fetch --no-verbose origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fetch --no-quiet origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-set-upstream`

Desactiva para esta invocación el comportamiento que habilita `--set-upstream`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fetch`, desactivar set upstream modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --no-set-upstream origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-append`

Desactiva para esta invocación el comportamiento que habilita `--append`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fetch`, desactivar append modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --no-append origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-atomic`

Desactiva para esta invocación el comportamiento que habilita `--atomic`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git fetch --no-atomic origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-upload-pack`

Desactiva para esta invocación el comportamiento que habilita `--upload-pack`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fetch`, desactivar upload pack modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --no-upload-pack origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force`

Desactiva para esta invocación el comportamiento que habilita `--force`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar objetos y referencias sin integrar la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git fetch --no-force origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-jobs`

Desactiva para esta invocación el comportamiento que habilita `--jobs`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --no-jobs origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-prefetch`

Desactiva para esta invocación el comportamiento que habilita `--prefetch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --no-prefetch origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-prune`

Desactiva para esta invocación el comportamiento que habilita `--prune`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar podar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar objetos y referencias sin integrar la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git fetch --no-prune origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-prune-tags`

Desactiva para esta invocación el comportamiento que habilita `--prune-tags`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar podar etiquetas. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar objetos y referencias sin integrar la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git fetch --no-prune-tags origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fetch`, desactivar recorrer submódulos modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --no-recurse-submodules origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-dry-run`

Desactiva para esta invocación el comportamiento que habilita `--dry-run`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git fetch --no-dry-run origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-porcelain`

Desactiva para esta invocación el comportamiento que habilita `--porcelain`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fetch --no-porcelain origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-write-fetch-head`

Desactiva para esta invocación el comportamiento que habilita `--write-fetch-head`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git fetch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fetch --no-write-fetch-head origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep`

Desactiva para esta invocación el comportamiento que habilita `--keep`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fetch`, desactivar conservar modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --no-keep origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-update-head-ok`

Desactiva para esta invocación el comportamiento que habilita `--update-head-ok`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --no-update-head-ok origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar objetos y referencias sin integrar la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git fetch --no-progress origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-depth`

Desactiva para esta invocación el comportamiento que habilita `--depth`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --no-depth origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-shallow-since`

Desactiva para esta invocación el comportamiento que habilita `--shallow-since`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --no-shallow-since origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-shallow-exclude`

Desactiva para esta invocación el comportamiento que habilita `--shallow-exclude`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --no-shallow-exclude origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-deepen`

Desactiva para esta invocación el comportamiento que habilita `--deepen`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --no-deepen origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-update-shallow`

Desactiva para esta invocación el comportamiento que habilita `--update-shallow`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --no-update-shallow origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-server-option`

Desactiva para esta invocación el comportamiento que habilita `--server-option`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fetch`, desactivar server option modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --no-server-option origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-negotiation-tip`

Desactiva para esta invocación el comportamiento que habilita `--negotiation-tip`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fetch`, desactivar negotiation tip modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --no-negotiation-tip origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-negotiate-only`

Desactiva para esta invocación el comportamiento que habilita `--negotiate-only`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fetch --no-negotiate-only origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-filter`

Desactiva para esta invocación el comportamiento que habilita `--filter`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos y referencias sin integrar la rama actual. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch --no-filter origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-auto-maintenance`

Desactiva para esta invocación el comportamiento que habilita `--auto-maintenance`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fetch`, desactivar auto maintenance modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --no-auto-maintenance origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-auto`

Desactiva para esta invocación el comportamiento que habilita `--auto`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fetch`, desactivar auto modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --no-auto origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-auto-gc`

Desactiva para esta invocación el comportamiento que habilita `--auto-gc`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fetch`, desactivar auto gc modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --no-auto-gc origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-show-forced-updates`

Desactiva para esta invocación el comportamiento que habilita `--show-forced-updates`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar mostrar forced updates. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque descargar objetos y referencias sin integrar la rama actual puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git fetch --no-show-forced-updates origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-write-commit-graph`

Desactiva para esta invocación el comportamiento que habilita `--write-commit-graph`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fetch`, desactivar write commit graph modifica la forma en que se ejecuta descargar objetos y referencias sin integrar la rama actual. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch --no-write-commit-graph origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stdin`

Desactiva para esta invocación el comportamiento que habilita `--stdin`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git fetch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fetch --no-stdin origin
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El refspec no coincide

Comprueba esta causa: La parte de origen no resuelve una referencia. Comprueba la referencia local y escribe el refspec completo.

### La actualización se rechaza

Comprueba esta causa: El destino perdería commits o una política lo impide. Integra primero o usa una protección con lease tras verificar el remoto.

### La rama no tiene upstream

Comprueba esta causa: No existe asociación entre rama local y remota. Configura el upstream y confirma con `git branch -vv`.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: descargar objetos y referencias sin integrar la rama actual. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git ls-remote`](../sharing-and-updating-projects/ls-remote.md)
- [`git bundle`](../sharing-and-updating-projects/bundle.md)
- [`git pull`](../sharing-and-updating-projects/pull.md)

## Fuente

- [git-fetch - Download objects and refs from another repository](https://git-scm.com/docs/git-fetch)
