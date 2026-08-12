---
title: "git difftool"
source: "https://git-scm.com/docs/git-difftool"
section: "inspection-and-comparison"
status: "option-expanded"
---

# `git difftool`

Este caso usa `git difftool` para ver comparaciones con una herramienta externa. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git difftool selecciona objetos o rangos y produce una vista sin cambiar el repositorio. Recibe como entrada los estados u objetos que la consulta debe mostrar o comparar. La operación consiste en ver comparaciones con una herramienta externa.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Ejemplo mínimo

```bash
git difftool main..tema-portada -- README.md
```

La invocación `git difftool main..tema-portada -- README.md` ejecuta esta operación: ver comparaciones con una herramienta externa. Después, la salida cambia cuando se modifica una sola revisión, ruta u opción de formato. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git difftool [<options>] [<commit> [<commit>]] [--] [<path>…]
```

### Uso verificado con `git version 2.51.1`

```text
git difftool [<options>] [<commit> [<commit>]] [--] [<path>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git difftool -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

ver comparaciones con una herramienta externa. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git difftool a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git difftool con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-g` y `--gui`

Define gui para esta ejecución de `git difftool`. En Git 2.51.1, la ayuda corta expresa el contrato como `use `diff.guitool` instead of `diff.tool``. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-g`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git difftool`, gui modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-g`

```bash
git difftool -g main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--gui`

```bash
git difftool --gui main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-d` y `--dir-diff`

Ejecuta dir diff durante ver comparaciones con una herramienta externa. En Git 2.51.1, la ayuda corta expresa el contrato como `perform a full-directory diff`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-d`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git difftool`, dir diff modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-d`

```bash
git difftool -d main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--dir-diff`

```bash
git difftool --dir-diff main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-y`

Impide y durante esta invocación de `git difftool`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not prompt before launching a diff tool`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `--no-prompt`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

En `git difftool`, y modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git difftool -y main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-prompt`

Desactiva el comportamiento `prompt` para esta invocación.

En `git difftool`, desactivar prompt modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git difftool --no-prompt main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--symlinks`

Define symlinks para esta ejecución de `git difftool`. En Git 2.51.1, la ayuda corta expresa el contrato como `use symlinks in dir-diff mode`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git difftool`, symlinks modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git difftool --symlinks main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-t` y `--tool`

Define tool para esta ejecución de `git difftool`. En Git 2.51.1, la ayuda corta expresa el contrato como `use the specified diff tool`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-t`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git difftool`, tool modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-t`

```bash
git difftool -t valor main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--tool`

```bash
git difftool --tool=valor main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--tool-help`

Incluye tool ayuda en la salida o cambia cómo `git difftool` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print a list of diff tools that may be used with `--tool``. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git difftool --tool-help main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--trust-exit-code`

Activa trust exit code durante ver comparaciones con una herramienta externa. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `make 'git-difftool' exit when an invoked diff tool returns a non-zero exit code`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git difftool`, trust exit code modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git difftool --trust-exit-code main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-x` y `--extcmd`

Define extcmd para esta ejecución de `git difftool`. En Git 2.51.1, la ayuda corta expresa el contrato como `specify a custom command for viewing diffs`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-x`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git difftool`, extcmd modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-x`

```bash
git difftool -x status main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

En esta forma, `status` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--extcmd`

```bash
git difftool --extcmd=status main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

En esta forma, `status` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-index`

Desactiva el comportamiento `index` para esta invocación.

En `git difftool`, desactivar índice modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git difftool --no-index main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index`

Incluye el índice en la operación.

En `git difftool`, índice modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git difftool --index main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gui`

Desactiva para esta invocación el comportamiento que habilita `--gui`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git difftool`, desactivar gui modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git difftool --no-gui main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-dir-diff`

Desactiva para esta invocación el comportamiento que habilita `--dir-diff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git difftool`, desactivar dir diff modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git difftool --no-dir-diff main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-symlinks`

Desactiva para esta invocación el comportamiento que habilita `--symlinks`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git difftool`, desactivar symlinks modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git difftool --no-symlinks main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tool`

Desactiva para esta invocación el comportamiento que habilita `--tool`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git difftool`, desactivar tool modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git difftool --no-tool main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tool-help`

Desactiva para esta invocación el comportamiento que habilita `--tool-help`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git difftool --no-tool-help main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-trust-exit-code`

Desactiva para esta invocación el comportamiento que habilita `--trust-exit-code`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git difftool`, desactivar trust exit code modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git difftool --no-trust-exit-code main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-extcmd`

Desactiva para esta invocación el comportamiento que habilita `--extcmd`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git difftool`, desactivar extcmd modifica la forma en que se ejecuta ver comparaciones con una herramienta externa. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git difftool --no-extcmd main..tema-portada -- README.md
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git difftool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

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

- [`git last-modified`](../inspection-and-comparison/last-modified.md)
- [`git diff`](../inspection-and-comparison/diff.md)
- [`git log`](../inspection-and-comparison/log.md)

## Fuente

- [git-difftool - Show changes using common diff tools](https://git-scm.com/docs/git-difftool)
