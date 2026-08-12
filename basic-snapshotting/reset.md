---
title: "git reset"
source: "https://git-scm.com/docs/git-reset"
section: "basic-snapshotting"
status: "option-expanded"
---

# `git reset`

Este caso usa `git reset` para mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git reset mueve contenido entre el área de trabajo, el índice y el commit señalado por `HEAD`. Recibe como entrada las rutas y el estado de origen seleccionados por los argumentos. La operación consiste en mover HEAD o restablecer el índice y, según el modo, el área de trabajo.

Puede persistir el estado implicado por esta operación: mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Ejemplo mínimo

```bash
git add guia.txt
git reset HEAD -- guia.txt
git status --short
```

La invocación `git reset HEAD -- guia.txt` ejecuta esta operación: mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Después, `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git reset [--soft | --mixed [-N] | --hard | --merge | --keep] [-q] [<commit>]
git reset [-q] [<tree-ish>] [--] <pathspec>…
git reset [-q] [--pathspec-from-file=<file> [--pathspec-file-nul]] [<tree-ish>]
git reset (--patch | -p) [<tree-ish>] [--] [<pathspec>…]
```

### Uso verificado con `git version 2.51.1`

```text
git reset [--mixed | --soft | --hard | --merge | --keep] [-q] [<commit>]
   or: git reset [-q] [<tree-ish>] [--] <pathspec>...
   or: git reset [-q] [--pathspec-from-file [--pathspec-file-nul]] [<tree-ish>]
   or: git reset --patch [<tree-ish>] [--] [<pathspec>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git reset -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git reset a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git reset con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--soft`

Restablece soft como parte de mover HEAD o restablecer el índice y, según el modo, el área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `reset only HEAD`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git reset`, soft modifica la forma en que se ejecuta mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git reset --soft HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mixed`

Restablece mixed como parte de mover HEAD o restablecer el índice y, según el modo, el área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `reset HEAD and index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git reset`, mixed modifica la forma en que se ejecuta mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git reset --mixed HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-N` y `--intent-to-add`

Registra una entrada sin preparar todavía su contenido.  La misma línea de ayuda también acepta `-N`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla intent to add. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque mover HEAD o restablecer el índice y, según el modo, el área de trabajo puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-N`

```bash
git reset -N HEAD -- guia.txt
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--intent-to-add`

```bash
git reset --intent-to-add HEAD -- guia.txt
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--hard`

Restablece hard como parte de mover HEAD o restablecer el índice y, según el modo, el área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `reset HEAD, index and working tree`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git reset`, hard modifica la forma en que se ejecuta mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git reset --hard HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--merge`

Restablece merge como parte de mover HEAD o restablecer el índice y, según el modo, el área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `reset HEAD, index and working tree`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git reset`, merge modifica la forma en que se ejecuta mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git reset --merge HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep`

Conserva el asunto del mensaje recibido según la forma que define el comando. En Git 2.51.1, la ayuda corta expresa el contrato como `reset HEAD but keep local changes`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git reset`, conservar modifica la forma en que se ejecuta mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git reset --keep HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git reset -q HEAD -- guia.txt
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--quiet`

```bash
git reset --quiet HEAD -- guia.txt
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--pathspec-from-file`

Lee pathspecs desde un archivo o desde stdin.

La opción cambia cómo `git reset` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git reset --pathspec-from-file=rutas.txt HEAD -- guia.txt
git status --short
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pathspec-file-nul`

Interpreta los pathspecs de archivo como registros terminados en NUL.

La opción cambia cómo `git reset` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git reset --pathspec-file-nul HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--patch` y `-p`

Permite elegir hunks en vez de operar sobre el archivo completo.  La misma línea de ayuda también acepta `-p`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git reset`, parche modifica la forma en que se ejecuta mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--patch`

```bash
git reset --patch HEAD -- guia.txt
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `-p`

```bash
git reset -p HEAD -- guia.txt
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-refresh`

Desactiva el comportamiento `refresh` para esta invocación.

En `git reset`, desactivar refresh modifica la forma en que se ejecuta mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git reset --no-refresh HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--refresh`

Actualiza metadatos de comprobación sin copiar contenido nuevo al índice.

En `git reset`, refresh modifica la forma en que se ejecuta mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git reset --refresh HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

En `git reset`, recorrer submódulos modifica la forma en que se ejecuta mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git reset --recurse-submodules=valor HEAD -- guia.txt
git status --short
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-U` y `--unified`

Define cuántas líneas de contexto rodean cada hunk.  La misma línea de ayuda también acepta `-U`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git reset`, unified modifica la forma en que se ejecuta mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-U`

```bash
git reset -U 5 HEAD -- guia.txt
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--unified`

```bash
git reset --unified=5 HEAD -- guia.txt
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--inter-hunk-context`

Fusiona hunks cercanos cuando la distancia no supera el límite indicado.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git reset --inter-hunk-context=5 HEAD -- guia.txt
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-pathspec-from-file`

Desactiva para esta invocación el comportamiento que habilita `--pathspec-from-file`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git reset` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git reset --no-pathspec-from-file HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-pathspec-file-nul`

Desactiva para esta invocación el comportamiento que habilita `--pathspec-file-nul`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git reset` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git reset --no-pathspec-file-nul HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-patch`

Desactiva para esta invocación el comportamiento que habilita `--patch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git reset`, desactivar parche modifica la forma en que se ejecuta mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git reset --no-patch HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git reset --no-quiet HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git reset`, desactivar recorrer submódulos modifica la forma en que se ejecuta mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git reset --no-recurse-submodules HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-intent-to-add`

Desactiva para esta invocación el comportamiento que habilita `--intent-to-add`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar intent to add. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque mover HEAD o restablecer el índice y, según el modo, el área de trabajo puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git reset --no-intent-to-add HEAD -- guia.txt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git reset` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El cambio no entra al commit

Comprueba esta causa: El índice no contiene la versión esperada. Compara `git diff` con `git diff --cached`.

### Un pathspec no coincide

Comprueba esta causa: La ruta se evalúa desde otro directorio o está ignorada. Usa `git status --short --untracked-files=all` y separa opciones con `--`.

### Se reemplaza contenido local

Comprueba esta causa: La orden escribe el área de trabajo. Guarda el diff o crea un stash antes de repetir la operación.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git restore`](../basic-snapshotting/restore.md)
- [`git notes`](../basic-snapshotting/notes.md)
- [`git rm`](../basic-snapshotting/rm.md)

## Fuente

- [git-reset - Set HEAD or the index to a known state](https://git-scm.com/docs/git-reset)
