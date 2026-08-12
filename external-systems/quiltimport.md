---
title: "git quiltimport"
source: "https://git-scm.com/docs/git-quiltimport"
section: "external-systems"
status: "option-expanded"
---

# `git quiltimport`

Este caso usa `git quiltimport` para importar una serie de parches administrada por quilt. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git quiltimport traduce historial, referencias e identidades entre Git y otro sistema. Recibe como entrada la ubicación y los nombres que deben traducirse desde el sistema de origen. La operación consiste en importar una serie de parches administrada por quilt.

Puede persistir el estado implicado por esta operación: importar una serie de parches administrada por quilt. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Ejemplo mínimo

```bash
git quiltimport --patches parches
```

La invocación `git quiltimport --patches parches` ejecuta esta operación: importar una serie de parches administrada por quilt. Después, el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git quiltimport [--dry-run | -n] [--author <author>] [--patches <dir>]
		[--series <file>] [--keep-non-patch]
```

### Uso verificado con `git version 2.51.1`

```text
git quiltimport [options]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git quiltimport -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

importar una serie de parches administrada por quilt. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git quiltimport a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Simulación

Calcular el efecto sin escribir el estado principal. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Compara la simulación con la selección prevista.

### Validación

Comprobar el resultado de git quiltimport con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--dry-run` y `-n`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.  La misma línea de ayuda también acepta `-n`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

#### Ejemplo con `--dry-run`

```bash
git quiltimport --dry-run --patches parches
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git quiltimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `-n`

```bash
git quiltimport -n --patches parches
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git quiltimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--author`

Limita el resultado a autores que coinciden con el patrón indicado. En Git 2.51.1, la ayuda corta expresa el contrato como `author name and email address for patches without any`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta importar una serie de parches administrada por quilt. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git quiltimport --author --patches parches
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git quiltimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--patches`

Define patches con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `path to the quilt patches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git quiltimport`, patches modifica la forma en que se ejecuta importar una serie de parches administrada por quilt. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git quiltimport --patches parches
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git quiltimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--series`

Define series con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `path to the quilt series file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git quiltimport` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git quiltimport --series --patches parches
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git quiltimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-non-patch` y `-b`

Activa conservar non parche durante importar una serie de parches administrada por quilt. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.  La misma línea de ayuda también acepta `-b`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git quiltimport`, conservar non parche modifica la forma en que se ejecuta importar una serie de parches administrada por quilt. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--keep-non-patch`

```bash
git quiltimport --keep-non-patch --patches parches
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git quiltimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `-b`

```bash
git quiltimport -b --patches parches
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git quiltimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-dry-run`

Desactiva para esta invocación el comportamiento que habilita `--dry-run`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git quiltimport --no-dry-run --patches parches
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git quiltimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-author`

Desactiva para esta invocación el comportamiento que habilita `--author`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta importar una serie de parches administrada por quilt. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git quiltimport --no-author --patches parches
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git quiltimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-patches`

Desactiva para esta invocación el comportamiento que habilita `--patches`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git quiltimport`, desactivar patches modifica la forma en que se ejecuta importar una serie de parches administrada por quilt. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git quiltimport --no-patches parches
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git quiltimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-series`

Desactiva para esta invocación el comportamiento que habilita `--series`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git quiltimport` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git quiltimport --no-series --patches parches
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git quiltimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep-non-patch`

Desactiva para esta invocación el comportamiento que habilita `--keep-non-patch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git quiltimport`, desactivar conservar non parche modifica la forma en que se ejecuta importar una serie de parches administrada por quilt. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git quiltimport --no-keep-non-patch --patches parches
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git quiltimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Faltan revisiones

Comprueba esta causa: El rango, rama o marcador de importación las excluye. Compara conteos y el último identificador importado.

### La identidad cambia

Comprueba esta causa: No existe una regla de mapeo estable. Define el mapa antes de repetir la importación.

### La sincronización duplica cambios

Comprueba esta causa: Se perdió el marcador entre sistemas. Restaura el punto de control y prueba sobre una copia.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: importar una serie de parches administrada por quilt. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git svn`](../external-systems/svn.md)
- [`git p4`](../external-systems/p4.md)
- [`git fast-import`](../external-systems/fast-import.md)

## Fuente

- [git-quiltimport - Applies a quilt patchset onto the current branch](https://git-scm.com/docs/git-quiltimport)
