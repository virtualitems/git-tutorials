---
title: "git notes"
source: "https://git-scm.com/docs/git-notes"
section: "basic-snapshotting"
status: "option-expanded"
---

# `git notes`

Este caso usa `git notes` para asociar anotaciones a objetos sin cambiar los objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git notes mueve contenido entre el área de trabajo, el índice y el commit señalado por `HEAD`. Recibe como entrada las rutas y el estado de origen seleccionados por los argumentos. La operación consiste en asociar anotaciones a objetos sin cambiar los objetos.

Puede persistir el estado implicado por esta operación: asociar anotaciones a objetos sin cambiar los objetos. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Ejemplo mínimo

```bash
git notes add -m "Revisado en clase" HEAD
git notes show HEAD
```

La invocación `git notes add -m "Revisado en clase" HEAD` ejecuta esta operación: asociar anotaciones a objetos sin cambiar los objetos. Después, `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git notes [list [<object>]]
git notes add [-f] [--allow-empty] [--[no-]separator | --separator=<paragraph-break>] [--[no-]stripspace] [-F <file> | -m <msg> | (-c | -C) <object>] [-e] [<object>]
git notes copy [-f] ( --stdin | <from-object> [<to-object>] )
git notes append [--allow-empty] [--[no-]separator | --separator=<paragraph-break>] [--[no-]stripspace] [-F <file> | -m <msg> | (-c | -C) <object>] [-e] [<object>]
```

### Uso verificado con `git version 2.51.1`

```text
git notes [--ref <notes-ref>] [list [<object>]]
   or: git notes [--ref <notes-ref>] add [-f] [--allow-empty] [--[no-]separator|--separator=<paragraph-break>] [--[no-]stripspace] [-m <msg> | -F <file> | (-c | -C) <object>] [<object>] [-e]
   or: git notes [--ref <notes-ref>] copy [-f] <from-object> <to-object>
   or: git notes [--ref <notes-ref>] append [--allow-empty] [--[no-]separator|--separator=<paragraph-break>] [--[no-]stripspace] [-m <msg> | -F <file> | (-c | -C) <object>] [<object>] [-e]
   or: git notes [--ref <notes-ref>] edit [--allow-empty] [<object>]
   or: git notes [--ref <notes-ref>] show [<object>]
   or: git notes [--ref <notes-ref>] merge [-v | -q] [-s <strategy>] <notes-ref>
   or: git notes merge --commit [-v | -q]
   or: git notes merge --abort [-v | -q]
   or: git notes [--ref <notes-ref>] remove [<object>...]
   or: git notes [--ref <notes-ref>] prune [-n] [-v]
   or: git notes [--ref <notes-ref>] get-ref
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git notes -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

asociar anotaciones a objetos sin cambiar los objetos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git notes a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Sesión interrumpida

Continuar o cancelar una secuencia después de revisar el estado. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Consulta `git status` antes de elegir la acción.

### Validación

Comprobar el resultado de git notes con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-f`

Activa f durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git notes`, f modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes -f add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--allow-empty`

Permite continuar cuando el cambio produce un commit sin diferencias.

La opción limita o amplía el conjunto sobre el que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git notes --allow-empty add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--separator`

Activa separator durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git notes`, separator modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes --separator add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stripspace`

Activa stripspace durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git notes`, stripspace modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes --stripspace add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-F`

Activa F durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git notes`, F modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes -F add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m`

Activa m durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git notes`, m modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes -m add "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-c`

Aplica una clave de configuración solo a esta invocación.

En `git notes`, c modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes -c add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

En `git notes`, C modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes -C add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-e`

Activa e durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git notes`, e modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes -e add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git notes` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git notes --stdin add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ref`

Selecciona o modifica referencias dentro del alcance de la orden.

En `git notes`, referencia modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes --ref=refs/heads/main add -m "Revisado en clase" HEAD
git status --short
```

El ejemplo usa `refs/heads/main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v`

Activa v durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git notes -v add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q`

Activa q durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git notes`, q modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes -q add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-s`

Activa s durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git notes`, s modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes -s add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--commit`

Activa commit durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git notes`, commit modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes --commit add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--abort`

Cancela la secuencia y restaura el punto que la orden registró al comenzar.

Esta forma se usa cuando `git notes` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque abortar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git notes --abort
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-n`

Activa n durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git notes`, n modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes -n add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-separator`

Desactiva para esta invocación el comportamiento que habilita `--separator`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git notes`, desactivar separator modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes --no-separator add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stripspace`

Desactiva para esta invocación el comportamiento que habilita `--stripspace`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git notes`, desactivar stripspace modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes --no-stripspace add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ref`

Desactiva para esta invocación el comportamiento que habilita `--ref`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git notes`, desactivar referencia modifica la forma en que se ejecuta asociar anotaciones a objetos sin cambiar los objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git notes --no-ref add -m "Revisado en clase" HEAD
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git notes` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El cambio no entra al commit

Comprueba esta causa: El índice no contiene la versión esperada. Compara `git diff` con `git diff --cached`.

### Un pathspec no coincide

Comprueba esta causa: La ruta se evalúa desde otro directorio o está ignorada. Usa `git status --short --untracked-files=all` y separa opciones con `--`.

### Se reemplaza contenido local

Comprueba esta causa: La orden escribe el área de trabajo. Guarda el diff o crea un stash antes de repetir la operación.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: asociar anotaciones a objetos sin cambiar los objetos. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git reset`](../basic-snapshotting/reset.md)
- [`git mv`](../basic-snapshotting/mv.md)
- [`git restore`](../basic-snapshotting/restore.md)

## Fuente

- [git-notes - Add or inspect object notes](https://git-scm.com/docs/git-notes)
