---
title: "git unpack-objects"
source: "https://git-scm.com/docs/git-unpack-objects"
section: "plumbing-write"
status: "option-expanded"
---

# `git unpack-objects`

Este caso usa `git unpack-objects` para extraer objetos de un flujo pack. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git unpack-objects crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en extraer objetos de un flujo pack.

Puede persistir el estado implicado por esta operación: extraer objetos de un flujo pack. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git unpack-objects < paquete.pack
```

La invocación `git unpack-objects < paquete.pack` ejecuta esta operación: extraer objetos de un flujo pack. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git unpack-objects [-n] [-q] [-r] [--strict]
```

### Uso verificado con `git version 2.51.1`

```text
git unpack-objects [-n] [-q] [-r] [--strict]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git unpack-objects -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

extraer objetos de un flujo pack. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git unpack-objects a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git unpack-objects con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-n`

Activa n durante extraer objetos de un flujo pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git unpack-objects`, n modifica la forma en que se ejecuta extraer objetos de un flujo pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git unpack-objects -n < paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git unpack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q`

Activa q durante extraer objetos de un flujo pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git unpack-objects`, q modifica la forma en que se ejecuta extraer objetos de un flujo pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git unpack-objects -q < paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git unpack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-r`

Activa r durante extraer objetos de un flujo pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git unpack-objects`, r modifica la forma en que se ejecuta extraer objetos de un flujo pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git unpack-objects -r < paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git unpack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--strict`

Activa strict durante extraer objetos de un flujo pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git unpack-objects`, strict modifica la forma en que se ejecuta extraer objetos de un flujo pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git unpack-objects --strict < paquete.pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git unpack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El hash no coincide

Comprueba esta causa: Los bytes, el tipo o la longitud difieren. Compara la entrada byte por byte y no normalices el contenido.

### La referencia no se actualiza

Comprueba esta causa: El valor anterior no coincide con la condición. Lee el valor actual y repite con una condición nueva.

### El índice queda sin resolver

Comprueba esta causa: Una entrada tiene etapas de conflicto. Inspecciona `git ls-files --stage` antes de escribir un árbol.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: extraer objetos de un flujo pack. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git update-index`](../plumbing-write/update-index.md)
- [`git symbolic-ref`](../plumbing-write/symbolic-ref.md)
- [`git update-ref`](../plumbing-write/update-ref.md)

## Fuente

- [git-unpack-objects - Unpack objects from a packed archive](https://git-scm.com/docs/git-unpack-objects)
