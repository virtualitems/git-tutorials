---
title: "git apply"
source: "https://git-scm.com/docs/git-apply"
section: "patching"
status: "option-expanded"
---

# `git apply`

Este caso usa `git apply` para aplicar un parche sobre archivos o sobre el índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git apply aplica diffs o commits y mantiene un estado que puede continuar o abortarse. Recibe como entrada un parche, un commit o un rango que representa cambios. La operación consiste en aplicar un parche sobre archivos o sobre el índice.

Puede persistir el estado implicado por esta operación: aplicar un parche sobre archivos o sobre el índice. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Ejemplo mínimo

```bash
git apply --check cambio.patch
git apply cambio.patch
```

La invocación `git apply --check cambio.patch` ejecuta esta operación: aplicar un parche sobre archivos o sobre el índice. Después, el diff y el historial muestran si cambiaron archivos, índice o commits. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git apply [--stat] [--numstat] [--summary] [--check]
	  [--index | --intent-to-add] [--3way] [--ours | --theirs | --union]
	  [--apply] [--no-add] [--build-fake-ancestor=<file>] [-R | --reverse]
	  [--allow-binary-replacement | --binary] [--reject] [-z]
```

### Uso verificado con `git version 2.51.1`

```text
git apply [<options>] [<patch>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git apply -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

aplicar un parche sobre archivos o sobre el índice. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git apply a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git apply con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--stat`

Resume cambios mediante conteos por ruta.

Esta forma se usa cuando `git apply` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque estadísticas actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git apply --stat --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--numstat`

Incluye numstat en la salida o cambia cómo `git apply` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show number of added and deleted lines in decimal notation`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción controla numstat. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque aplicar un parche sobre archivos o sobre el índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git apply --numstat --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--summary`

Incluye summary en la salida o cambia cómo `git apply` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `instead of applying the patch, output a summary for the input`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git apply --summary --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--check`

Valida sin producir el efecto principal de la orden.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git apply --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index`

Incluye el índice en la operación.

En `git apply`, índice modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --index --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--intent-to-add` y `-N`

Registra una entrada sin preparar todavía su contenido.  La misma línea de ayuda también acepta `-N`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia cómo `git apply` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `--intent-to-add`

```bash
git apply --intent-to-add --check cambio.patch
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `-N`

```bash
git apply -N --check cambio.patch
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--3way` y `-3`

Intenta una fusión de tres vías cuando el parche no se aplica directamente y existen los blobs necesarios. En Git 2.51.1, la ayuda corta expresa el contrato como `attempt three-way merge, fall back on normal patch if that fails`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-3`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar un parche sobre archivos o sobre el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `--3way`

```bash
git apply --3way --check cambio.patch
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `-3`

```bash
git apply -3 --check cambio.patch
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--ours`

Selecciona la versión de la etapa ours para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use our version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git apply`, ours modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --ours --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--theirs`

Selecciona la versión de la etapa theirs para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use their version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git apply`, theirs modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --theirs --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--union`

Define union para esta ejecución de `git apply`. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use a union version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git apply`, union modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --union --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--apply`

Comprueba apply antes de aceptar el resultado de `git apply`. En Git 2.51.1, la ayuda corta expresa el contrato como `also apply the patch (use with --stat/--summary/--check)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git apply --apply --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-add`

Desactiva el comportamiento `add` para esta invocación.

En `git apply`, desactivar add modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --no-add --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--build-fake-ancestor`

Activa build fake ancestor durante aplicar un parche sobre archivos o sobre el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `build a temporary index based on embedded index information`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git apply --build-fake-ancestor=rutas.txt --check cambio.patch
git status --short
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-R` y `--reverse`

Invierte el orden del recorrido o resultado.  La misma línea de ayuda también acepta `-R`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git apply`, invertir modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-R`

```bash
git apply -R --check cambio.patch
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--reverse`

```bash
git apply --reverse --check cambio.patch
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--allow-binary-replacement`

Activa permitir contenido binario replacement durante aplicar un parche sobre archivos o sobre el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar un parche sobre archivos o sobre el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git apply --allow-binary-replacement --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--binary`

Activa contenido binario durante aplicar un parche sobre archivos o sobre el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git apply`, contenido binario modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --binary --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reject`

Conserva hunks que no pudieron aplicarse en archivos de rechazo para inspección manual. En Git 2.51.1, la ayuda corta expresa el contrato como `leave the rejected hunks in corresponding *.rej files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git apply` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git apply --reject --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

En `git apply`, z modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply -z --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude`

Excluye elementos que cumplan la condición indicada.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar un parche sobre archivos o sobre el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git apply --exclude=archivo.txt --check cambio.patch
git status --short
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include`

Incluye elementos adicionales dentro del alcance indicado.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar un parche sobre archivos o sobre el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git apply --include=archivo.txt --check cambio.patch
git status --short
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p`

Retira p del alcance que procesa `git apply`. En Git 2.51.1, la ayuda corta expresa el contrato como `remove <num> leading slashes from traditional diff paths`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción controla p. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque aplicar un parche sobre archivos o sobre el índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git apply -p 5 --check cambio.patch
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--add`

Permite crear o escribir el elemento seleccionado.

En `git apply`, add modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --add --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cached`

Usa el índice como origen o destino, sin tratar el área de trabajo de la misma forma.

En `git apply`, índice modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --cached --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unsafe-paths`

Activa unsafe paths durante aplicar un parche sobre archivos o sobre el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `accept a patch that touches outside the working area`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git apply`, unsafe paths modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --unsafe-paths --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

En `git apply`, C modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply -C 5 --check cambio.patch
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--whitespace`

Selecciona la acción que Git ejecuta cuando detecta errores de espacios en un parche. En Git 2.51.1, la ayuda corta expresa el contrato como `detect new or modified lines that have whitespace errors`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git apply`, espacios en blanco modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --whitespace=warn --check cambio.patch
git status --short
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-space-change`

Excluye elementos que cumplan la condición indicada.

En `git apply`, ignorar espacios change modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --ignore-space-change --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-whitespace`

Excluye elementos que cumplan la condición indicada.

En `git apply`, ignorar espacios en blanco modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --ignore-whitespace --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unidiff-zero`

Impide unidiff zero durante esta invocación de `git apply`. En Git 2.51.1, la ayuda corta expresa el contrato como `don't expect at least one line of context`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git apply`, unidiff zero modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --unidiff-zero --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--allow-overlap`

Permite permitir overlap cuando la forma predeterminada de `git apply` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow overlapping hunks`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar un parche sobre archivos o sobre el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git apply --allow-overlap --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-v`

```bash
git apply -v --check cambio.patch
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--verbose`

```bash
git apply --verbose --check cambio.patch
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git apply -q --check cambio.patch
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--quiet`

```bash
git apply --quiet --check cambio.patch
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--inaccurate-eof`

Activa inaccurate eof durante aplicar un parche sobre archivos o sobre el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.  La misma línea de ayuda también acepta `-line`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

La opción cambia cómo `git apply` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git apply --inaccurate-eof --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recount`

Impide recount durante esta invocación de `git apply`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not trust the line counts in the hunk headers`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git apply`, recount modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --recount --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--directory`

Añade el prefijo indicado a las rutas afectadas antes de procesarlas. En Git 2.51.1, la ayuda corta expresa el contrato como `prepend <root> to all filenames`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar un parche sobre archivos o sobre el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git apply --directory=valor --check cambio.patch
git status --short
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--allow-empty`

Permite continuar cuando el cambio produce un commit sin diferencias. En Git 2.51.1, la ayuda corta expresa el contrato como `don't return error for empty patches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar un parche sobre archivos o sobre el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git apply --allow-empty --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stat`

Desactiva para esta invocación el comportamiento que habilita `--stat`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git apply --no-stat --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-numstat`

Desactiva para esta invocación el comportamiento que habilita `--numstat`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar numstat. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque aplicar un parche sobre archivos o sobre el índice puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git apply --no-numstat --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-summary`

Desactiva para esta invocación el comportamiento que habilita `--summary`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git apply --no-summary --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-check`

Desactiva para esta invocación el comportamiento que habilita `--check`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git apply --no-check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-index`

Desactiva para esta invocación el comportamiento que habilita `--index`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git apply`, desactivar índice modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --no-index --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-intent-to-add`

Desactiva para esta invocación el comportamiento que habilita `--intent-to-add`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git apply` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git apply --no-intent-to-add --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-3way`

Desactiva para esta invocación el comportamiento que habilita `--3way`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar un parche sobre archivos o sobre el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git apply --no-3way --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-apply`

Desactiva para esta invocación el comportamiento que habilita `--apply`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git apply --no-apply --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-build-fake-ancestor`

Desactiva para esta invocación el comportamiento que habilita `--build-fake-ancestor`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git apply --no-build-fake-ancestor --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reverse`

Desactiva para esta invocación el comportamiento que habilita `--reverse`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git apply`, desactivar invertir modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --no-reverse --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reject`

Desactiva para esta invocación el comportamiento que habilita `--reject`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git apply` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git apply --no-reject --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cached`

Desactiva para esta invocación el comportamiento que habilita `--cached`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git apply`, desactivar índice modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --no-cached --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-unsafe-paths`

Desactiva para esta invocación el comportamiento que habilita `--unsafe-paths`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git apply`, desactivar unsafe paths modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --no-unsafe-paths --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-whitespace`

Desactiva para esta invocación el comportamiento que habilita `--whitespace`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git apply`, desactivar espacios en blanco modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --no-whitespace --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-space-change`

Desactiva para esta invocación el comportamiento que habilita `--ignore-space-change`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git apply`, desactivar ignorar espacios change modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --no-ignore-space-change --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-whitespace`

Desactiva para esta invocación el comportamiento que habilita `--ignore-whitespace`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git apply`, desactivar ignorar espacios en blanco modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --no-ignore-whitespace --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-unidiff-zero`

Desactiva para esta invocación el comportamiento que habilita `--unidiff-zero`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git apply`, desactivar unidiff zero modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --no-unidiff-zero --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-allow-overlap`

Desactiva para esta invocación el comportamiento que habilita `--allow-overlap`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar un parche sobre archivos o sobre el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git apply --no-allow-overlap --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git apply --no-verbose --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git apply --no-quiet --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-inaccurate-eof`

Desactiva para esta invocación el comportamiento que habilita `--inaccurate-eof`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git apply` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git apply --no-inaccurate-eof --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recount`

Desactiva para esta invocación el comportamiento que habilita `--recount`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git apply`, desactivar recount modifica la forma en que se ejecuta aplicar un parche sobre archivos o sobre el índice. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git apply --no-recount --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-directory`

Desactiva para esta invocación el comportamiento que habilita `--directory`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar un parche sobre archivos o sobre el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git apply --no-directory --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-allow-empty`

Desactiva para esta invocación el comportamiento que habilita `--allow-empty`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar un parche sobre archivos o sobre el índice. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git apply --no-allow-empty --check cambio.patch
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git apply` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un parche no aplica

Comprueba esta causa: El contexto no coincide con el contenido actual. Inspecciona los rechazos o resuelve el conflicto antes de continuar.

### La secuencia queda en pausa

Comprueba esta causa: Git espera una resolución o una decisión. Consulta `git status` y usa `--continue`, `--skip` o `--abort`.

### El resultado contiene commits vacíos

Comprueba esta causa: Los cambios ya existen o se resolvieron sin diferencias. Revisa el diff y aplica la política de commits vacíos de la orden.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: aplicar un parche sobre archivos o sobre el índice. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Trabaja en una rama de prueba. Compara `git diff`, `git diff --staged` y `git log --oneline --graph` antes y después.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git cherry-pick`](../patching/cherry-pick.md)
- [`git rebase`](../patching/rebase.md)

## Fuente

- [git-apply - Apply a patch to files and/or to the index](https://git-scm.com/docs/git-apply)
