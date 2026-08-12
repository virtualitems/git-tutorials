---
title: "git log"
source: "https://git-scm.com/docs/git-log"
section: "inspection-and-comparison"
status: "option-expanded"
---

# `git log`

Este caso usa `git log` para consultar commits con filtros y formatos de salida. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git log selecciona objetos o rangos y produce una vista sin cambiar el repositorio. Recibe como entrada los estados u objetos que la consulta debe mostrar o comparar. La operación consiste en consultar commits con filtros y formatos de salida.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Ejemplo mínimo

```bash
git log --oneline --decorate --graph --all
```

La invocación `git log --oneline --decorate --graph --all` ejecuta esta operación: consultar commits con filtros y formatos de salida. Después, la salida cambia cuando se modifica una sola revisión, ruta u opción de formato. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git log [<options>] [<revision-range>] [[--] <path>…]
```

### Uso verificado con `git version 2.51.1`

```text
git log [<options>] [<revision-range>] [[--] <path>...]
   or: git show [<options>] <object>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git log -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

consultar commits con filtros y formatos de salida. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git log a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git log con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git log -q --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git log` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--quiet`

```bash
git log --quiet --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git log` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--source`

Incluye source en la salida o cambia cómo `git log` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show source`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git log --source --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git log` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--use-mailmap`

Define use mailmap para esta ejecución de `git log`. En Git 2.51.1, la ayuda corta expresa el contrato como `use mail map file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git log` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git log --use-mailmap --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git log` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mailmap`

Define mailmap para esta ejecución de `git log`. En Git 2.51.1, la ayuda corta expresa el contrato como `alias of --use-mailmap`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git log`, mailmap modifica la forma en que se ejecuta consultar commits con filtros y formatos de salida. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git log --mailmap --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git log` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--clear-decorations`

Activa clear decorations durante consultar commits con filtros y formatos de salida. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `clear all previously-defined decoration filters`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta consultar commits con filtros y formatos de salida. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git log --clear-decorations --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git log` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--decorate-refs`

Selecciona o modifica referencias dentro del alcance de la orden.

En `git log`, decorate referencias modifica la forma en que se ejecuta consultar commits con filtros y formatos de salida. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git log --decorate-refs=TODO --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--decorate-refs-exclude`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta consultar commits con filtros y formatos de salida. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git log --decorate-refs-exclude=TODO --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--decorate`

Activa decorate durante consultar commits con filtros y formatos de salida. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git log`, decorate modifica la forma en que se ejecuta consultar commits con filtros y formatos de salida. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git log --decorate=valor --oneline --all
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-L`

Activa L durante consultar commits con filtros y formatos de salida. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `trace the evolution of line range <start>,<end> or function :<funcname> in <file>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git log` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git log -L rutas.txt --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git log --no-quiet --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git log` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-source`

Desactiva para esta invocación el comportamiento que habilita `--source`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git log --no-source --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git log` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-use-mailmap`

Desactiva para esta invocación el comportamiento que habilita `--use-mailmap`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git log` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git log --no-use-mailmap --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git log` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-mailmap`

Desactiva para esta invocación el comportamiento que habilita `--mailmap`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git log`, desactivar mailmap modifica la forma en que se ejecuta consultar commits con filtros y formatos de salida. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git log --no-mailmap --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git log` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-decorate-refs`

Desactiva para esta invocación el comportamiento que habilita `--decorate-refs`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git log`, desactivar decorate referencias modifica la forma en que se ejecuta consultar commits con filtros y formatos de salida. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git log --no-decorate-refs --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git log` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-decorate-refs-exclude`

Desactiva para esta invocación el comportamiento que habilita `--decorate-refs-exclude`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta consultar commits con filtros y formatos de salida. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git log --no-decorate-refs-exclude --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git log` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-decorate`

Desactiva para esta invocación el comportamiento que habilita `--decorate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git log`, desactivar decorate modifica la forma en que se ejecuta consultar commits con filtros y formatos de salida. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git log --no-decorate --oneline --all
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git log` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La salida está vacía

Comprueba esta causa: El rango o el pathspec no contiene cambios. Resuelve cada revisión con `git rev-parse --verify`.

### El orden no coincide con el esperado

Comprueba esta causa: La función usa un recorrido o criterio de orden. Declara el criterio con opciones de fecha, topología o formato.

### Un script interpreta colores

Comprueba esta causa: La salida está destinada a terminal. Usa una forma de formato y desactiva color para datos de máquina.

## Automatización y recuperación

Persistencia: No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Ejecuta la consulta sobre dos revisiones conocidas. Cambia un solo argumento y explica qué conjunto de objetos o rutas cambió.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git range-diff`](../inspection-and-comparison/range-diff.md)
- [`git last-modified`](../inspection-and-comparison/last-modified.md)
- [`git shortlog`](../inspection-and-comparison/shortlog.md)

## Fuente

- [git-log - Show commit logs](https://git-scm.com/docs/git-log)
