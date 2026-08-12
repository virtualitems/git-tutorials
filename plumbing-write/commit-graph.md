---
title: "git commit-graph"
source: "https://git-scm.com/docs/git-commit-graph"
section: "plumbing-write"
status: "option-expanded"
---

# `git commit-graph`

Este caso usa `git commit-graph` para escribir y verificar el archivo que acelera recorridos de commits. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git commit-graph crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en escribir y verificar el archivo que acelera recorridos de commits.

Puede persistir el estado implicado por esta operación: escribir y verificar el archivo que acelera recorridos de commits. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git commit-graph write --reachable
git commit-graph verify
```

La invocación `git commit-graph write --reachable` ejecuta esta operación: escribir y verificar el archivo que acelera recorridos de commits. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git commit-graph verify [--object-dir <dir>] [--shallow] [--[no-]progress]
git commit-graph write [--object-dir <dir>] [--append]
			[--split[=<strategy>]] [--reachable | --stdin-packs | --stdin-commits]
			[--changed-paths] [--[no-]max-new-filters <n>] [--[no-]progress]
```

### Uso verificado con `git version 2.51.1`

```text
git commit-graph verify [--object-dir <dir>] [--shallow] [--[no-]progress]
   or: git commit-graph write [--object-dir <dir>] [--append]
                              [--split[=<strategy>]] [--reachable | --stdin-packs | --stdin-commits]
                              [--changed-paths] [--[no-]max-new-filters <n>] [--[no-]progress]
                              <split-options>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git commit-graph -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

escribir y verificar el archivo que acelera recorridos de commits. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git commit-graph a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git commit-graph con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--object-dir`

Selecciona la representación o tratamiento de identificadores de objeto.

En `git commit-graph`, objeto dir modifica la forma en que se ejecuta escribir y verificar el archivo que acelera recorridos de commits. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit-graph --object-dir=docs write --reachable
git fsck --no-progress
```

El ejemplo usa `docs` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow`

Activa historial shallow durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta escribir y verificar el archivo que acelera recorridos de commits. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git commit-graph --shallow write --reachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit-graph` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

En `git commit-graph`, progreso modifica la forma en que se ejecuta escribir y verificar el archivo que acelera recorridos de commits. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit-graph --progress write --reachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit-graph` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--append`

Activa append durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git commit-graph`, append modifica la forma en que se ejecuta escribir y verificar el archivo que acelera recorridos de commits. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit-graph --append write --reachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit-graph` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--split`

Activa split durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git commit-graph`, split modifica la forma en que se ejecuta escribir y verificar el archivo que acelera recorridos de commits. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit-graph --split write --reachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit-graph` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reachable`

Activa reachable durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git commit-graph`, reachable modifica la forma en que se ejecuta escribir y verificar el archivo que acelera recorridos de commits. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit-graph --reachable write
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit-graph` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin-packs`

Activa entrada estándar packs durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git commit-graph` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit-graph --stdin-packs write --reachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit-graph` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin-commits`

Activa entrada estándar commits durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git commit-graph` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit-graph --stdin-commits write --reachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit-graph` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--changed-paths`

Activa changed paths durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git commit-graph`, changed paths modifica la forma en que se ejecuta escribir y verificar el archivo que acelera recorridos de commits. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit-graph --changed-paths write --reachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit-graph` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-new-filters`

Establece un límite numérico para la selección o el recorrido.

La opción limita o amplía el conjunto sobre el que se ejecuta escribir y verificar el archivo que acelera recorridos de commits. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git commit-graph --max-new-filters write --reachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit-graph` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-object-dir`

Desactiva para esta invocación el comportamiento que habilita `--object-dir`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git commit-graph`, desactivar objeto dir modifica la forma en que se ejecuta escribir y verificar el archivo que acelera recorridos de commits. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit-graph --no-object-dir write --reachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit-graph` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git commit-graph`, desactivar progreso modifica la forma en que se ejecuta escribir y verificar el archivo que acelera recorridos de commits. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit-graph --no-progress write --reachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit-graph` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-max-new-filters`

Desactiva para esta invocación el comportamiento que habilita `--max-new-filters`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta escribir y verificar el archivo que acelera recorridos de commits. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git commit-graph --no-max-new-filters write --reachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git commit-graph` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El hash no coincide

Comprueba esta causa: Los bytes, el tipo o la longitud difieren. Compara la entrada byte por byte y no normalices el contenido.

### La referencia no se actualiza

Comprueba esta causa: El valor anterior no coincide con la condición. Lee el valor actual y repite con una condición nueva.

### El índice queda sin resolver

Comprueba esta causa: Una entrada tiene etapas de conflicto. Inspecciona `git ls-files --stage` antes de escribir un árbol.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: escribir y verificar el archivo que acelera recorridos de commits. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git commit-tree`](../plumbing-write/commit-tree.md)
- [`git checkout-index`](../plumbing-write/checkout-index.md)
- [`git hash-object`](../plumbing-write/hash-object.md)

## Fuente

- [git-commit-graph - Write and verify Git commit-graph files](https://git-scm.com/docs/git-commit-graph)
