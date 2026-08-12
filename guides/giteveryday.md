---
title: "giteveryday"
source: "https://git-scm.com/docs/giteveryday"
section: "guides"
status: "option-expanded"
---

# `giteveryday`

Este caso usa `giteveryday` para resolver tareas diarias con un conjunto de comandos. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **trabajo individual**, **colaboración**, **integración**, **administración**, **comandos por rol**.

## Responsabilidad y efecto

giteveryday define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en resolver tareas diarias con un conjunto de comandos.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
git status
git add README.md
git commit -m "Actualiza instrucciones"
git log --oneline -3
```

La invocación `giteveryday` ejecuta esta operación: resolver tareas diarias con un conjunto de comandos. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git status
git add README.md
git commit -m "Actualiza instrucciones"
git log --oneline -3
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

resolver tareas diarias con un conjunto de comandos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### trabajo individual

Aplicar las reglas de trabajo individual. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### colaboración

Aplicar las reglas de colaboración. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### integración

Aplicar las reglas de integración. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### administración

Aplicar las reglas de administración. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### comandos por rol

Aplicar las reglas de comandos por rol. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

## Funciones y reglas

### Trabajo

El flujo individual alterna editar, inspeccionar, preparar y registrar.

Comprueba trabajo e índice antes del commit. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Colaboración

Fetch actualiza referencias remotas y merge o rebase integra el resultado.

Distingue descarga de integración en el log. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Integración

Una persona integradora revisa rangos y conserva la relación con la rama origen.

Compara los tips antes de fusionar. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Publicación

Push propone una actualización de referencias en otro repositorio.

Verifica el refspec y el valor remoto. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Administración

Mantenimiento, respaldo y recuperación operan sobre objetos y referencias.

Registra hashes antes de podar o reescribir. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-m`

Activa m durante resolver tareas diarias con un conjunto de comandos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `giteveryday`, m modifica la forma en que se ejecuta resolver tareas diarias con un conjunto de comandos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git commit -m "Actualiza instrucciones"
printf 'exit=%s\n' "$?"
```

El ejemplo usa `"Actualiza` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--oneline`

Condensa cada registro en una línea.

En `giteveryday`, oneline modifica la forma en que se ejecuta resolver tareas diarias con un conjunto de comandos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git log --oneline -3
printf 'exit=%s\n' "$?"
```

El ejemplo usa `-3` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-3`

Activa 3 durante resolver tareas diarias con un conjunto de comandos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `giteveryday`, 3 modifica la forma en que se ejecuta resolver tareas diarias con un conjunto de comandos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git log --oneline -3
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `giteveryday` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La regla no se aplica

Comprueba esta causa: El patrón, alcance o precedencia no coincide. Consulta la regla efectiva y el archivo que la definió.

### Una revisión se interpreta como ruta

Comprueba esta causa: El nombre es ambiguo. Separa revisiones y rutas con `--`.

### El resultado cambia entre equipos

Comprueba esta causa: La regla vive en configuración no compartida. Decide qué parte debe versionarse en el repositorio.

## Automatización y recuperación

Persistencia: La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`gitfaq`](../guides/gitfaq.md)
- [`gitdiffcore`](../guides/gitdiffcore.md)
- [`gitglossary`](../guides/gitglossary.md)

## Fuente

- [giteveryday - A useful minimum set of commands for Everyday Git](https://git-scm.com/docs/giteveryday)
