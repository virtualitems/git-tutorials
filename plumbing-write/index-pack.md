---
title: "git index-pack"
source: "https://git-scm.com/docs/git-index-pack"
section: "plumbing-write"
status: "option-expanded"
---

# `git index-pack`

Este caso usa `git index-pack` para crear un índice para un pack y comprobar sus objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git index-pack crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en crear un índice para un pack y comprobar sus objetos.

Puede persistir el estado implicado por esta operación: crear un índice para un pack y comprobar sus objetos. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git index-pack paquete.pack
```

La invocación `git index-pack paquete.pack` ejecuta esta operación: crear un índice para un pack y comprobar sus objetos. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git index-pack [-v] [-o <index-file>] [--[no-]rev-index] <pack-file>
git index-pack --stdin [--fix-thin] [--keep] [-v] [-o <index-file>]
		  [--[no-]rev-index] [<pack-file>]
```

### Uso verificado con `git version 2.51.1`

```text
git index-pack [-v] [-o <index-file>] [--keep | --keep=<msg>] [--[no-]rev-index] [--verify] [--strict[=<msg-id>=<severity>...]] [--fsck-objects[=<msg-id>=<severity>...]] (<pack-file> | --stdin [--fix-thin] [<pack-file>])
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git index-pack -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

crear un índice para un pack y comprobar sus objetos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git index-pack a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git index-pack con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-v`

Activa v durante crear un índice para un pack y comprobar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un índice para un pack y comprobar sus objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git index-pack -v paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git index-pack` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-o`

Activa o durante crear un índice para un pack y comprobar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git index-pack`, o modifica la forma en que se ejecuta crear un índice para un pack y comprobar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git index-pack -o paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git index-pack` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--rev-index`

Activa rev índice durante crear un índice para un pack y comprobar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git index-pack`, rev índice modifica la forma en que se ejecuta crear un índice para un pack y comprobar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git index-pack --rev-index paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git index-pack` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git index-pack` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git index-pack --stdin paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git index-pack` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--fix-thin`

Activa fix thin durante crear un índice para un pack y comprobar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git index-pack`, fix thin modifica la forma en que se ejecuta crear un índice para un pack y comprobar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git index-pack --fix-thin paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git index-pack` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep`

Conserva el asunto del mensaje recibido según la forma que define el comando.

En `git index-pack`, conservar modifica la forma en que se ejecuta crear un índice para un pack y comprobar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git index-pack --keep paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git index-pack` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git index-pack --verify paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git index-pack` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--strict`

Activa strict durante crear un índice para un pack y comprobar sus objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git index-pack`, strict modifica la forma en que se ejecuta crear un índice para un pack y comprobar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git index-pack --strict paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git index-pack` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--fsck-objects`

Selecciona la representación o tratamiento de identificadores de objeto.

En `git index-pack`, fsck objetos modifica la forma en que se ejecuta crear un índice para un pack y comprobar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git index-pack --fsck-objects paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git index-pack` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-rev-index`

Desactiva para esta invocación el comportamiento que habilita `--rev-index`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git index-pack`, desactivar rev índice modifica la forma en que se ejecuta crear un índice para un pack y comprobar sus objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git index-pack --no-rev-index paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git index-pack` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El hash no coincide

Comprueba esta causa: Los bytes, el tipo o la longitud difieren. Compara la entrada byte por byte y no normalices el contenido.

### La referencia no se actualiza

Comprueba esta causa: El valor anterior no coincide con la condición. Lee el valor actual y repite con una condición nueva.

### El índice queda sin resolver

Comprueba esta causa: Una entrada tiene etapas de conflicto. Inspecciona `git ls-files --stage` antes de escribir un árbol.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: crear un índice para un pack y comprobar sus objetos. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git merge-file`](../plumbing-write/merge-file.md)
- [`git hash-object`](../plumbing-write/hash-object.md)
- [`git merge-index`](../plumbing-write/merge-index.md)

## Fuente

- [git-index-pack - Build pack index file for an existing packed archive](https://git-scm.com/docs/git-index-pack)
