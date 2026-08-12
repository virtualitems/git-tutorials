---
title: "git worktree"
source: "https://git-scm.com/docs/git-worktree"
section: "branching-and-merging"
status: "option-expanded"
---

# `git worktree`

Este caso usa `git worktree` para vincular varias áreas de trabajo al mismo repositorio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git worktree consulta o cambia referencias, `HEAD`, worktrees y estados de integración. Recibe como entrada las ramas, commits o rutas que participan en la operación. La operación consiste en vincular varias áreas de trabajo al mismo repositorio.

Puede persistir el estado implicado por esta operación: vincular varias áreas de trabajo al mismo repositorio. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git worktree add ../biblioteca-release release
git worktree list
```

La invocación `git worktree add ../biblioteca-release release` ejecuta esta operación: vincular varias áreas de trabajo al mismo repositorio. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git worktree add [-f] [--detach] [--checkout] [--lock [--reason <string>]]
		 [--orphan] [(-b | -B) <new-branch>] <path> [<commit-ish>]
git worktree list [-v | --porcelain [-z]]
git worktree lock [--reason <string>] <worktree>
```

### Uso verificado con `git version 2.51.1`

```text
git worktree add [-f] [--detach] [--checkout] [--lock [--reason <string>]]
                        [--orphan] [(-b | -B) <new-branch>] <path> [<commit-ish>]
   or: git worktree list [-v | --porcelain [-z]]
   or: git worktree lock [--reason <string>] <worktree>
   or: git worktree move <worktree> <new-path>
   or: git worktree prune [-n] [-v] [--expire <expire>]
   or: git worktree remove [-f] <worktree>
   or: git worktree repair [<path>...]
   or: git worktree unlock <worktree>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git worktree -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

vincular varias áreas de trabajo al mismo repositorio. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git worktree a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git worktree con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-f`

Activa f durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git worktree`, f modifica la forma en que se ejecuta vincular varias áreas de trabajo al mismo repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git worktree -f add ../biblioteca-release release
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git worktree` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--detach`

Hace que `HEAD` apunte directamente a un commit.

En `git worktree`, HEAD separado modifica la forma en que se ejecuta vincular varias áreas de trabajo al mismo repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git worktree --detach add ../biblioteca-release release
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git worktree` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--checkout`

Activa checkout durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git worktree --checkout add ../biblioteca-release release
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git worktree` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--lock`

Activa lock durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git worktree`, lock modifica la forma en que se ejecuta vincular varias áreas de trabajo al mismo repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git worktree --lock add ../biblioteca-release release
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git worktree` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reason`

Activa reason durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git worktree`, reason modifica la forma en que se ejecuta vincular varias áreas de trabajo al mismo repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git worktree --reason add ../biblioteca-release release
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git worktree` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--orphan`

Crea o cambia a una rama sin padres en el historial existente.

En `git worktree`, rama sin padre modifica la forma en que se ejecuta vincular varias áreas de trabajo al mismo repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git worktree --orphan add ../biblioteca-release release
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git worktree` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-b`

Activa b durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git worktree`, b modifica la forma en que se ejecuta vincular varias áreas de trabajo al mismo repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git worktree -b add ../biblioteca-release release
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git worktree` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-B`

Activa B durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git worktree`, B modifica la forma en que se ejecuta vincular varias áreas de trabajo al mismo repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git worktree -B add ../biblioteca-release release
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git worktree` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v`

Activa v durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta vincular varias áreas de trabajo al mismo repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git worktree -v add ../biblioteca-release release
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git worktree` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--porcelain`

Produce un contrato de salida destinado a scripts.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git worktree --porcelain add ../biblioteca-release release
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git worktree` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

En `git worktree`, z modifica la forma en que se ejecuta vincular varias áreas de trabajo al mismo repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git worktree -z add ../biblioteca-release release
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git worktree` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-n`

Activa n durante vincular varias áreas de trabajo al mismo repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git worktree`, n modifica la forma en que se ejecuta vincular varias áreas de trabajo al mismo repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git worktree -n add ../biblioteca-release release
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git worktree` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--expire`

Aplica una fecha, duración o política de vencimiento.

La opción controla expire. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque vincular varias áreas de trabajo al mismo repositorio puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git worktree --expire add ../biblioteca-release release
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git worktree` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La referencia es ambigua

Comprueba esta causa: Un nombre coincide con más de un objeto o una ruta. Usa `--` para separar rutas y una revisión completa para el objeto.

### El cambio de rama se rechaza

Comprueba esta causa: Hay modificaciones que serían sobrescritas. Confirma el estado y decide entre commit, stash o descarte.

### La integración se detiene

Comprueba esta causa: Dos cambios afectan la misma región o ruta. Resuelve, añade los archivos y usa la orden `--continue` o `--abort` que corresponda.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: vincular varias áreas de trabajo al mismo repositorio. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git tag`](../branching-and-merging/tag.md)
- [`git switch`](../branching-and-merging/switch.md)

## Fuente

- [git-worktree - Manage multiple working trees](https://git-scm.com/docs/git-worktree)
