---
title: "git history"
source: "https://git-scm.com/docs/git-history"
section: "branching-and-merging"
status: "option-expanded"
---

# `git history`

Este caso usa `git history` para reescribir commits con operaciones de corrección, mensaje o división. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git history consulta o cambia referencias, `HEAD`, worktrees y estados de integración. Recibe como entrada las ramas, commits o rutas que participan en la operación. La operación consiste en reescribir commits con operaciones de corrección, mensaje o división.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git history reword HEAD~2 --dry-run
```

La invocación `git history reword HEAD~2 --dry-run` ejecuta esta operación: reescribir commits con operaciones de corrección, mensaje o división. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git history fixup <commit> [--dry-run] [--update-refs=(branches|head)] [--reedit-message] [--empty=(drop|keep|abort)]
git history reword <commit> [--dry-run] [--update-refs=(branches|head)]
git history split <commit> [--dry-run] [--update-refs=(branches|head)] [--] [<pathspec>…]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git history -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

reescribir commits con operaciones de corrección, mensaje o división. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git history a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Simulación

Calcular el efecto sin escribir el estado principal. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Compara la simulación con la selección prevista.

### Validación

Comprobar el resultado de git history con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git history --dry-run reword HEAD~2
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git history` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--update-refs`

Selecciona o modifica referencias dentro del alcance de la orden.

En `git history`, actualizar referencias modifica la forma en que se ejecuta reescribir commits con operaciones de corrección, mensaje o división. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git history --update-refs reword HEAD~2 --dry-run
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git history` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reedit-message`

Reutiliza un mensaje existente y abre el editor antes de confirmar.

En `git history`, reedit mensaje modifica la forma en que se ejecuta reescribir commits con operaciones de corrección, mensaje o división. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git history --reedit-message reword HEAD~2 --dry-run
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git history` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--empty`

Activa vacío durante reescribir commits con operaciones de corrección, mensaje o división. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git history`, vacío modifica la forma en que se ejecuta reescribir commits con operaciones de corrección, mensaje o división. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git history --empty reword HEAD~2 --dry-run
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git history` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--help`

Muestra la ayuda correspondiente a la versión instalada.

En `git history`, ayuda modifica la forma en que se ejecuta reescribir commits con operaciones de corrección, mensaje o división. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git history --help
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git history` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La referencia es ambigua

Comprueba esta causa: Un nombre coincide con más de un objeto o una ruta. Usa `--` para separar rutas y una revisión completa para el objeto.

### El cambio de rama se rechaza

Comprueba esta causa: Hay modificaciones que serían sobrescritas. Confirma el estado y decide entre commit, stash o descarte.

### La integración se detiene

Comprueba esta causa: Dos cambios afectan la misma región o ruta. Resuelve, añade los archivos y usa la orden `--continue` o `--abort` que corresponda.

## Automatización y recuperación

Persistencia: No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git merge`](../branching-and-merging/merge.md)
- [`git checkout`](../branching-and-merging/checkout.md)
- [`git mergetool`](../branching-and-merging/mergetool.md)

## Fuente

- [git-history - EXPERIMENTAL: Rewrite history](https://git-scm.com/docs/git-history)
