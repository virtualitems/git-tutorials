---
title: "git for-each-ref"
source: "https://git-scm.com/docs/git-for-each-ref"
section: "plumbing-read"
status: "option-expanded"
---

# `git for-each-ref`

Este caso usa `git for-each-ref` para filtrar, ordenar y formatear referencias. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git for-each-ref consulta objetos, referencias, índices, packs y relaciones entre commits. Recibe como entrada objetos, referencias, árboles o entradas del índice que debe leer la consulta. La operación consiste en filtrar, ordenar y formatear referencias.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git for-each-ref --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
```

La invocación `git for-each-ref --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/` ejecuta esta operación: filtrar, ordenar y formatear referencias. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git for-each-ref [--count=<count>] [--shell|--perl|--python|--tcl]
		   [(--sort=<key>)…] [--format=<format>]
		   [--include-root-refs] [--points-at=<object>]
		   [--merged[=<object>]] [--no-merged[=<object>]]
```

### Uso verificado con `git version 2.51.1`

```text
git for-each-ref [<options>] [<pattern>]
   or: git for-each-ref [--points-at <object>]
   or: git for-each-ref [--merged [<commit>]] [--no-merged [<commit>]]
   or: git for-each-ref [--contains [<commit>]] [--no-contains [<commit>]]
   or: git for-each-ref [--start-after <marker>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git for-each-ref -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

filtrar, ordenar y formatear referencias. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git for-each-ref a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git for-each-ref con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--count`

Establece un límite numérico para la selección o el recorrido.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --count=5 --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shell` y `-s`

Activa shell durante filtrar, ordenar y formatear referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `quote placeholders suitably for shells`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-s`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git for-each-ref`, shell modifica la forma en que se ejecuta filtrar, ordenar y formatear referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--shell`

```bash
git for-each-ref --shell --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `-s`

```bash
git for-each-ref -s --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--perl` y `-p`

Activa perl durante filtrar, ordenar y formatear referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `quote placeholders suitably for perl`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-p`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git for-each-ref`, perl modifica la forma en que se ejecuta filtrar, ordenar y formatear referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--perl`

```bash
git for-each-ref --perl --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `-p`

```bash
git for-each-ref -p --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--python`

Activa python durante filtrar, ordenar y formatear referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `quote placeholders suitably for python`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git for-each-ref`, python modifica la forma en que se ejecuta filtrar, ordenar y formatear referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-ref --python --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tcl`

Activa tcl durante filtrar, ordenar y formatear referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `quote placeholders suitably for Tcl`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git for-each-ref`, tcl modifica la forma en que se ejecuta filtrar, ordenar y formatear referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-ref --tcl --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sort`

Ordena registros por el campo indicado.

En `git for-each-ref`, ordenar modifica la forma en que se ejecuta filtrar, ordenar y formatear referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-ref --sort=user.name --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `user.name` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--format`

Define los campos y separadores de la salida.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --format=oneline --sort=-committerdate refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include-root-refs`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta filtrar, ordenar y formatear referencias. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git for-each-ref --include-root-refs --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--points-at`

Limita filtrar, ordenar y formatear referencias al alcance identificado por points at. En Git 2.51.1, la ayuda corta expresa el contrato como `print only refs which points at the given object`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --points-at=HEAD --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--merged`

Filtra elementos ya alcanzables desde la revisión indicada.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --merged=HEAD --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-merged`

Filtra elementos no alcanzables desde la revisión indicada.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --no-merged --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--contains`

Filtra referencias cuyo historial contiene el commit indicado.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --contains=HEAD --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-contains`

Filtra referencias cuyo historial no contiene el commit indicado.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --no-contains --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--start-after`

Activa start after durante filtrar, ordenar y formatear referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `start iteration after the provided marker`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git for-each-ref`, start after modifica la forma en que se ejecuta filtrar, ordenar y formatear referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-ref --start-after=valor --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--omit-empty`

Impide omit vacío durante esta invocación de `git for-each-ref`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not output a newline after empty formatted refs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --omit-empty --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--color`

Controla el uso de secuencias de color en la salida.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --color=always --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `always` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude`

Excluye elementos que cumplan la condición indicada.

La opción limita o amplía el conjunto sobre el que se ejecuta filtrar, ordenar y formatear referencias. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git for-each-ref --exclude=TODO --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-case`

Excluye elementos que cumplan la condición indicada.

La opción limita o amplía el conjunto sobre el que se ejecuta filtrar, ordenar y formatear referencias. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git for-each-ref --ignore-case --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git for-each-ref` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git for-each-ref --stdin --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-count`

Desactiva para esta invocación el comportamiento que habilita `--count`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --no-count --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-shell`

Desactiva para esta invocación el comportamiento que habilita `--shell`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git for-each-ref`, desactivar shell modifica la forma en que se ejecuta filtrar, ordenar y formatear referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-ref --no-shell --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-perl`

Desactiva para esta invocación el comportamiento que habilita `--perl`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git for-each-ref`, desactivar perl modifica la forma en que se ejecuta filtrar, ordenar y formatear referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-ref --no-perl --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-python`

Desactiva para esta invocación el comportamiento que habilita `--python`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git for-each-ref`, desactivar python modifica la forma en que se ejecuta filtrar, ordenar y formatear referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-ref --no-python --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tcl`

Desactiva para esta invocación el comportamiento que habilita `--tcl`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git for-each-ref`, desactivar tcl modifica la forma en que se ejecuta filtrar, ordenar y formatear referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-ref --no-tcl --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-sort`

Desactiva para esta invocación el comportamiento que habilita `--sort`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git for-each-ref`, desactivar ordenar modifica la forma en que se ejecuta filtrar, ordenar y formatear referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-ref --no-sort --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-format`

Desactiva para esta invocación el comportamiento que habilita `--format`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --no-format --sort=-committerdate refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-include-root-refs`

Desactiva para esta invocación el comportamiento que habilita `--include-root-refs`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta filtrar, ordenar y formatear referencias. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git for-each-ref --no-include-root-refs --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-points-at`

Desactiva para esta invocación el comportamiento que habilita `--points-at`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --no-points-at --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-start-after`

Desactiva para esta invocación el comportamiento que habilita `--start-after`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git for-each-ref`, desactivar start after modifica la forma en que se ejecuta filtrar, ordenar y formatear referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git for-each-ref --no-start-after --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-omit-empty`

Desactiva para esta invocación el comportamiento que habilita `--omit-empty`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --no-omit-empty --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-color`

Desactiva para esta invocación el comportamiento que habilita `--color`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git for-each-ref --no-color --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-exclude`

Desactiva para esta invocación el comportamiento que habilita `--exclude`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta filtrar, ordenar y formatear referencias. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git for-each-ref --no-exclude --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-case`

Desactiva para esta invocación el comportamiento que habilita `--ignore-case`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta filtrar, ordenar y formatear referencias. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git for-each-ref --no-ignore-case --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stdin`

Desactiva para esta invocación el comportamiento que habilita `--stdin`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git for-each-ref` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git for-each-ref --no-stdin --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git for-each-ref` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El objeto no existe

Comprueba esta causa: El identificador no resuelve o no está disponible en un clon parcial. Valida el hash y la política de descarga.

### La salida se separa mal

Comprueba esta causa: Un nombre contiene espacios o saltos de línea. Usa terminación NUL cuando la función la admita.

### El recorrido incluye más commits

Comprueba esta causa: El rango expresa alcanzabilidad y no una lista literal. Comprueba extremos positivos y negativos del rango.

## Automatización y recuperación

Persistencia: No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git for-each-repo`](../plumbing-read/for-each-repo.md)
- [`git diff-tree`](../plumbing-read/diff-tree.md)
- [`git format-rev`](../plumbing-read/format-rev.md)

## Fuente

- [git-for-each-ref - Output information on each ref](https://git-scm.com/docs/git-for-each-ref)
