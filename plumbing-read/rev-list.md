---
title: "git rev-list"
source: "https://git-scm.com/docs/git-rev-list"
section: "plumbing-read"
status: "option-expanded"
---

# `git rev-list`

Este caso usa `git rev-list` para enumerar commits alcanzables según límites y filtros. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git rev-list consulta objetos, referencias, índices, packs y relaciones entre commits. Recibe como entrada objetos, referencias, árboles o entradas del índice que debe leer la consulta. La operación consiste en enumerar commits alcanzables según límites y filtros.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git rev-list --count main
git rev-list main --not origin/main
```

La invocación `git rev-list --count main` ejecuta esta operación: enumerar commits alcanzables según límites y filtros. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git rev-list [<options>] <commit>… [--] [<path>…]
```

### Uso verificado con `git version 2.51.1`

```text
git rev-list [<options>] <commit>... [--] [<path>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git rev-list -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

enumerar commits alcanzables según límites y filtros. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git rev-list a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git rev-list con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--max-count`

Limita el número de registros producidos.

La opción limita o amplía el conjunto sobre el que se ejecuta enumerar commits alcanzables según límites y filtros. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rev-list --max-count=5 --count main
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-age`

Aplica una fecha, duración o política de vencimiento.

En `git rev-list`, máximo age modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --max-age=valor --count main
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--min-age`

Aplica una fecha, duración o política de vencimiento.

En `git rev-list`, mínimo age modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --min-age=valor --count main
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sparse`

Permite operar sobre entradas que quedan fuera de la selección sparse activa.

En `git rev-list`, sparse modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --sparse --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-merges`

Desactiva el comportamiento `merges` para esta invocación.

En `git rev-list`, desactivar merges modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --no-merges --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--min-parents`

Establece un límite numérico para la selección o el recorrido.

En `git rev-list`, mínimo parents modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --min-parents=5 --count main
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-min-parents`

Desactiva el comportamiento `min-parents` para esta invocación.

En `git rev-list`, desactivar mínimo parents modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --no-min-parents --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-parents`

Establece un límite numérico para la selección o el recorrido.

En `git rev-list`, máximo parents modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --max-parents=5 --count main
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-max-parents`

Desactiva el comportamiento `max-parents` para esta invocación.

En `git rev-list`, desactivar máximo parents modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --no-max-parents --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--remove-empty`

Retira elementos según las condiciones de la orden.

La opción controla retirar vacío. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque enumerar commits alcanzables según límites y filtros puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git rev-list --remove-empty --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

La opción limita o amplía el conjunto sobre el que se ejecuta enumerar commits alcanzables según límites y filtros. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rev-list --all --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--branches`

Incluye o selecciona ramas según la operación.

La opción limita o amplía el conjunto sobre el que se ejecuta enumerar commits alcanzables según límites y filtros. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rev-list --branches --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tags`

Incluye o selecciona etiquetas según la operación.

La opción limita o amplía el conjunto sobre el que se ejecuta enumerar commits alcanzables según límites y filtros. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rev-list --tags --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--remotes`

Activa remotes durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git rev-list`, remotes modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --remotes --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git rev-list` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git rev-list --stdin --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude-hidden`

Excluye elementos que cumplan la condición indicada.

La opción limita o amplía el conjunto sobre el que se ejecuta enumerar commits alcanzables según límites y filtros. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rev-list --exclude-hidden=valor --count main
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quiet`

Reduce mensajes que no representan errores.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git rev-list --quiet --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--topo-order`

Activa topo order durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git rev-list`, topo order modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --topo-order --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--date-order`

Aplica una fecha, duración o política de vencimiento.

En `git rev-list`, fecha order modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --date-order --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reverse`

Invierte el orden del recorrido o resultado.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git rev-list --reverse --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--parents`

Activa parents durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git rev-list`, parents modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --parents --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--children`

Activa children durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git rev-list`, children modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --children --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--objects` y `--objects-edge`

Selecciona la representación o tratamiento de identificadores de objeto.  La misma línea de ayuda también acepta `--objects-edge`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git rev-list`, objetos modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--objects`

```bash
git rev-list --objects --count main
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--objects-edge`

```bash
git rev-list --objects-edge --count main
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--disk-usage`

Activa disk usage durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git rev-list`, disk usage modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --disk-usage=valor --count main
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unpacked`

Activa unpacked durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git rev-list`, unpacked modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --unpacked --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--header` y `--pretty`

Selecciona un formato para representar commits.  La misma línea de ayuda también acepta `--pretty`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `--header`

```bash
git rev-list --header --count main
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--pretty`

```bash
git rev-list --pretty --count main
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--object-names`

Selecciona la representación o tratamiento de identificadores de objeto.

En `git rev-list`, objeto names modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --object-names --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--abbrev`

Reduce la representación visible del identificador sin cambiar el objeto.  La misma línea de ayuda también acepta `--no-abbrev`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

En `git rev-list`, abbrev modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --abbrev=5 --count main
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-abbrev`

Desactiva el comportamiento `abbrev` para esta invocación.

En `git rev-list`, desactivar abbrev modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --no-abbrev --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--abbrev-commit`

Activa abbrev commit durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git rev-list`, abbrev commit modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --abbrev-commit --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--left-right`

Activa left right durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git rev-list`, left right modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --left-right --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--count`

Establece un límite numérico para la selección o el recorrido.

En `git rev-list`, cantidad modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

En `git rev-list`, z modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list -z --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--bisect`

Activa bisect durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git rev-list`, bisect modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --bisect --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--bisect-vars`

Activa bisect vars durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git rev-list`, bisect vars modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --bisect-vars --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--bisect-all`

Incluye elementos adicionales dentro del alcance indicado.

La opción limita o amplía el conjunto sobre el que se ejecuta enumerar commits alcanzables según límites y filtros. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git rev-list --bisect-all --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-object-names`

Desactiva para esta invocación el comportamiento que habilita `--object-names`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git rev-list`, desactivar objeto names modifica la forma en que se ejecuta enumerar commits alcanzables según límites y filtros. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git rev-list --no-object-names --count main
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git rev-list` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

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

- [`git rev-parse`](../plumbing-read/rev-parse.md)
- [`git repo`](../plumbing-read/repo.md)
- [`git show-index`](../plumbing-read/show-index.md)

## Fuente

- [git-rev-list - Lists commit objects in reverse chronological order](https://git-scm.com/docs/git-rev-list)
