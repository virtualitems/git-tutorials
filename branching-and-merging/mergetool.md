---
title: "git mergetool"
source: "https://git-scm.com/docs/git-mergetool"
section: "branching-and-merging"
status: "option-expanded"
---

# `git mergetool`

Este caso usa `git mergetool` para abrir una herramienta para resolver conflictos de fusión. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git mergetool consulta o cambia referencias, `HEAD`, worktrees y estados de integración. Recibe como entrada las ramas, commits o rutas que participan en la operación. La operación consiste en abrir una herramienta para resolver conflictos de fusión.

Puede persistir el estado implicado por esta operación: abrir una herramienta para resolver conflictos de fusión. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git mergetool
git status --short
```

La invocación `git mergetool` ejecuta esta operación: abrir una herramienta para resolver conflictos de fusión. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git mergetool [--tool=<tool>] [-y | --[no-]prompt] [<file>…]
```

### Uso verificado con `git version 2.51.1`

```text
git mergetool [--tool=tool] [--tool-help] [-y|--no-prompt|--prompt] [-g|--gui|--no-gui] [-O<orderfile>] [file to merge] ...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git mergetool -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

abrir una herramienta para resolver conflictos de fusión. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git mergetool a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git mergetool con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--tool`

Activa tool durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git mergetool`, tool modifica la forma en que se ejecuta abrir una herramienta para resolver conflictos de fusión. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mergetool --tool
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mergetool` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-y`

Activa y durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git mergetool`, y modifica la forma en que se ejecuta abrir una herramienta para resolver conflictos de fusión. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mergetool -y
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mergetool` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--prompt`

Activa prompt durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git mergetool`, prompt modifica la forma en que se ejecuta abrir una herramienta para resolver conflictos de fusión. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mergetool --prompt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mergetool` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tool-help`

Activa tool ayuda durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git mergetool`, tool ayuda modifica la forma en que se ejecuta abrir una herramienta para resolver conflictos de fusión. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mergetool --tool-help
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mergetool` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-prompt`

Desactiva el comportamiento `prompt` para esta invocación.

En `git mergetool`, desactivar prompt modifica la forma en que se ejecuta abrir una herramienta para resolver conflictos de fusión. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mergetool --no-prompt
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mergetool` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-g`

Activa g durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git mergetool`, g modifica la forma en que se ejecuta abrir una herramienta para resolver conflictos de fusión. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mergetool -g
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mergetool` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--gui`

Activa gui durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git mergetool`, gui modifica la forma en que se ejecuta abrir una herramienta para resolver conflictos de fusión. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mergetool --gui
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mergetool` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gui`

Desactiva el comportamiento `gui` para esta invocación.

En `git mergetool`, desactivar gui modifica la forma en que se ejecuta abrir una herramienta para resolver conflictos de fusión. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mergetool --no-gui
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mergetool` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-O`

Activa O durante abrir una herramienta para resolver conflictos de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git mergetool`, O modifica la forma en que se ejecuta abrir una herramienta para resolver conflictos de fusión. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mergetool -O
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mergetool` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La referencia es ambigua

Comprueba esta causa: Un nombre coincide con más de un objeto o una ruta. Usa `--` para separar rutas y una revisión completa para el objeto.

### El cambio de rama se rechaza

Comprueba esta causa: Hay modificaciones que serían sobrescritas. Confirma el estado y decide entre commit, stash o descarte.

### La integración se detiene

Comprueba esta causa: Dos cambios afectan la misma región o ruta. Resuelve, añade los archivos y usa la orden `--continue` o `--abort` que corresponda.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: abrir una herramienta para resolver conflictos de fusión. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git merge-tree`](../branching-and-merging/merge-tree.md)
- [`git merge`](../branching-and-merging/merge.md)
- [`git refs`](../branching-and-merging/refs.md)

## Fuente

- [git-mergetool - Run merge conflict resolution tools to resolve merge conflicts](https://git-scm.com/docs/git-mergetool)
