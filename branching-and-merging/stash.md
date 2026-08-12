---
title: "git stash"
source: "https://git-scm.com/docs/git-stash"
section: "branching-and-merging"
status: "option-expanded"
---

# `git stash`

Este caso usa `git stash` para guardar cambios sin commit y recuperar un área de trabajo limpia. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git stash consulta o cambia referencias, `HEAD`, worktrees y estados de integración. Recibe como entrada las ramas, commits o rutas que participan en la operación. La operación consiste en guardar cambios sin commit y recuperar un área de trabajo limpia.

Puede persistir el estado implicado por esta operación: guardar cambios sin commit y recuperar un área de trabajo limpia. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git stash push -m "portada incompleta"
git switch main
git stash pop
```

La invocación `git stash push -m "portada incompleta"` ejecuta esta operación: guardar cambios sin commit y recuperar un área de trabajo limpia. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git stash list [<log-options>]
git stash show [-u | --include-untracked | --only-untracked] [<diff-options>] [<stash>]
git stash drop [-q | --quiet] [<stash>]
git stash pop [--index] [-q | --quiet] [<stash>]
```

### Uso verificado con `git version 2.51.1`

```text
git stash list [<log-options>]
   or: git stash show [-u | --include-untracked | --only-untracked] [<diff-options>] [<stash>]
   or: git stash drop [-q | --quiet] [<stash>]
   or: git stash pop [--index] [-q | --quiet] [<stash>]
   or: git stash apply [--index] [-q | --quiet] [<stash>]
   or: git stash branch <branchname> [<stash>]
   or: git stash [push [-p | --patch] [-S | --staged] [-k | --[no-]keep-index] [-q | --quiet]
                 [-u | --include-untracked] [-a | --all] [(-m | --message) <message>]
                 [--pathspec-from-file=<file> [--pathspec-file-nul]]
                 [--] [<pathspec>...]]
   or: git stash save [-p | --patch] [-S | --staged] [-k | --[no-]keep-index] [-q | --quiet]
                 [-u | --include-untracked] [-a | --all] [<message>]
   or: git stash clear
   or: git stash create [<message>]
   or: git stash store [(-m | --message) <message>] [-q | --quiet] <commit>
   or: git stash export (--print | --to-ref <ref>) [<stash>...]
   or: git stash import <commit>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git stash -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

guardar cambios sin commit y recuperar un área de trabajo limpia. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git stash a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git stash con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-u`

Activa u durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git stash`, u modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash -u push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include-untracked`

Incluye elementos adicionales dentro del alcance indicado.

La opción limita o amplía el conjunto sobre el que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git stash --include-untracked push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--only-untracked`

Activa only untracked durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git stash`, only untracked modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash --only-untracked push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q`

Activa q durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git stash`, q modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash -q push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quiet`

Reduce mensajes que no representan errores.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git stash --quiet push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index`

Incluye el índice en la operación.

En `git stash`, índice modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash --index push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p`

Activa p durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git stash`, p modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash -p push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--patch`

Permite elegir hunks en vez de operar sobre el archivo completo.

En `git stash`, parche modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash --patch push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-S`

Activa S durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git stash`, S modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash -S push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--staged`

Selecciona el contenido preparado en el índice.

La opción limita o amplía el conjunto sobre el que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git stash --staged push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-k`

Activa k durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git stash`, k modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash -k push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-index`

Activa conservar índice durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git stash`, conservar índice modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash --keep-index push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a`

Activa a durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git stash`, a modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash -a push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

La opción limita o amplía el conjunto sobre el que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git stash --all push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m`

Activa m durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git stash`, m modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash -m push "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--message`

Activa mensaje durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git stash`, mensaje modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash --message push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pathspec-from-file`

Lee pathspecs desde un archivo o desde stdin.

La opción cambia cómo `git stash` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git stash --pathspec-from-file push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pathspec-file-nul`

Interpreta los pathspecs de archivo como registros terminados en NUL.

La opción cambia cómo `git stash` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git stash --pathspec-file-nul push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--print`

Incluye información adicional en la salida.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git stash --print push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--to-ref`

Selecciona o modifica referencias dentro del alcance de la orden.

En `git stash`, to referencia modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash --to-ref push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep-index`

Desactiva para esta invocación el comportamiento que habilita `--keep-index`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git stash`, desactivar conservar índice modifica la forma en que se ejecuta guardar cambios sin commit y recuperar un área de trabajo limpia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git stash --no-keep-index push -m "portada incompleta"
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git stash` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La referencia es ambigua

Comprueba esta causa: Un nombre coincide con más de un objeto o una ruta. Usa `--` para separar rutas y una revisión completa para el objeto.

### El cambio de rama se rechaza

Comprueba esta causa: Hay modificaciones que serían sobrescritas. Confirma el estado y decide entre commit, stash o descarte.

### La integración se detiene

Comprueba esta causa: Dos cambios afectan la misma región o ruta. Resuelve, añade los archivos y usa la orden `--continue` o `--abort` que corresponda.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: guardar cambios sin commit y recuperar un área de trabajo limpia. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git switch`](../branching-and-merging/switch.md)
- [`git rerere`](../branching-and-merging/rerere.md)
- [`git tag`](../branching-and-merging/tag.md)

## Fuente

- [git-stash - Stash the changes in a dirty working directory away](https://git-scm.com/docs/git-stash)
