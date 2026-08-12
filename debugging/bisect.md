---
title: "git bisect"
source: "https://git-scm.com/docs/git-bisect"
section: "debugging"
status: "option-expanded"
---

# `git bisect`

Este caso usa `git bisect` para localizar por búsqueda binaria el commit que introdujo un cambio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git bisect localiza texto, autores, líneas o el commit que introdujo un comportamiento. Recibe como entrada un patrón, una ruta y el rango de historial que limita la búsqueda. La operación consiste en localizar por búsqueda binaria el commit que introdujo un cambio.

Escribe el estado de la sesión de bisección y cambia el commit materializado hasta ejecutar reset.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La búsqueda combina revisiones, rutas y contenido. Primero delimita el conjunto de commits o archivos; después interpreta la evidencia que devuelve Git.

Reduce primero el rango y las rutas. Después interpreta cada coincidencia dentro de ese conjunto, sin atribuir significado a elementos que quedaron fuera.

## Ejemplo mínimo

```bash
git bisect start
git bisect bad
git bisect good v1.0
git bisect run ./prueba.sh
git bisect reset
```

La invocación `git bisect start` ejecuta esta operación: localizar por búsqueda binaria el commit que introdujo un cambio. Después, la salida identifica líneas, archivos o commits que cumplen el criterio. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git bisect start [--term-(bad|new)=<term-new> --term-(good|old)=<term-old>]
		 [--no-checkout] [--first-parent] [<bad> [<good>…]] [--] [<pathspec>…]
git bisect (bad|new|<term-new>) [<rev>]
git bisect (good|old|<term-old>) [<rev>…]
```

### Uso verificado con `git version 2.51.1`

```text
git bisect start [--term-(new|bad)=<term> --term-(old|good)=<term>]    [--no-checkout] [--first-parent] [<bad> [<good>...]] [--]    [<pathspec>...]
   or: git bisect (good|bad) [<rev>...]
   or: git bisect terms [--term-good | --term-bad]
   or: git bisect skip [(<rev>|<range>)...]
   or: git bisect next
   or: git bisect reset [<commit>]
   or: git bisect visualize
   or: git bisect replay <logfile>
   or: git bisect log
   or: git bisect run <cmd> [<arg>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git bisect -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

localizar por búsqueda binaria el commit que introdujo un cambio. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git bisect a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git bisect con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--term-`

Activa term durante localizar por búsqueda binaria el commit que introdujo un cambio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git bisect`, term modifica la forma en que se ejecuta localizar por búsqueda binaria el commit que introdujo un cambio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git bisect --term- start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git bisect` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-checkout`

Desactiva el comportamiento `checkout` para esta invocación.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git bisect --no-checkout start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git bisect` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--first-parent`

Activa first parent durante localizar por búsqueda binaria el commit que introdujo un cambio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git bisect`, first parent modifica la forma en que se ejecuta localizar por búsqueda binaria el commit que introdujo un cambio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git bisect --first-parent start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git bisect` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--term-good`

Activa term good durante localizar por búsqueda binaria el commit que introdujo un cambio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git bisect`, term good modifica la forma en que se ejecuta localizar por búsqueda binaria el commit que introdujo un cambio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git bisect --term-good start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git bisect` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--term-bad`

Activa term bad durante localizar por búsqueda binaria el commit que introdujo un cambio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git bisect`, term bad modifica la forma en que se ejecuta localizar por búsqueda binaria el commit que introdujo un cambio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git bisect --term-bad start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git bisect` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### No hay coincidencias

Comprueba esta causa: El patrón, la revisión o la ruta no abarca el dato. Prueba el patrón sobre `HEAD` y separa la ruta con `--`.

### La atribución parece incorrecta

Comprueba esta causa: El archivo se movió o el bloque se reformateó. Activa detección de movimiento o copia y compara el commit.

### La búsqueda binaria no avanza

Comprueba esta causa: La prueba no clasifica el commit. Marca el commit como `skip` o corrige el comando de prueba.

## Automatización y recuperación

Persistencia: Escribe el estado de la sesión de bisección y cambia el commit materializado hasta ejecutar reset. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Prepara un historial corto con un cambio por commit. Delimita una ruta o un rango para comprobar qué evidencia incluye y cuál excluye el comando.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git blame`](../debugging/blame.md)
- [`git annotate`](../debugging/annotate.md)
- [`git grep`](../debugging/grep.md)

## Fuente

- [git-bisect - Use binary search to find the commit that introduced a bug](https://git-scm.com/docs/git-bisect)
