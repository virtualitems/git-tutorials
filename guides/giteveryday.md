---
title: "giteveryday"
source: "https://git-scm.com/docs/giteveryday"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `giteveryday`

Este caso usa `giteveryday` para resolver tareas diarias con un conjunto de comandos.

La guía cubre **trabajo individual**, **colaboración**, **integración**, **administración**, **comandos por rol**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

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

La invocación `giteveryday` ejecuta esta operación: resolver tareas diarias con un conjunto de comandos. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
git status
git add README.md
git commit -m "Actualiza instrucciones"
git log --oneline -3
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

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

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-m`

Activa m durante resolver tareas diarias con un conjunto de comandos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git commit -m "Actualiza instrucciones"
printf 'exit=%s\n' "$?"
```

El ejemplo usa `"Actualiza` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--oneline`

Condensa cada registro en una línea.

```bash
git log --oneline -3
printf 'exit=%s\n' "$?"
```

El ejemplo usa `-3` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-3`

Activa 3 durante resolver tareas diarias con un conjunto de comandos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git log --oneline -3
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`gitfaq`](../guides/gitfaq.md)
- [`gitdiffcore`](../guides/gitdiffcore.md)
- [`gitglossary`](../guides/gitglossary.md)

## Fuente

- [giteveryday - A useful minimum set of commands for Everyday Git](https://git-scm.com/docs/giteveryday)
