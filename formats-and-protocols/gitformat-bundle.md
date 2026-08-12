---
title: "gitformat-bundle"
source: "https://git-scm.com/docs/gitformat-bundle"
section: "formats-and-protocols"
status: "option-expanded"
---

# `gitformat-bundle`

Este caso usa `gitformat-bundle` para interpretar la cabecera, prerrequisitos y referencias de un bundle. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **firma de cabecera**, **prerrequisitos**, **referencias**, **pack embebido**, **validación**.

## Responsabilidad y efecto

gitformat-bundle define campos, orden, codificación, extensiones y negociación entre productor y consumidor. Recibe como entrada los campos o mensajes producidos en el orden definido por el formato. La operación consiste en interpretar la cabecera, prerrequisitos y referencias de un bundle.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

 Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```bash
# v2 git bundle
-<oid> base requerida
<oid> refs/heads/main

<datos del pack>
```

La invocación `gitformat-bundle` ejecuta esta operación: interpretar la cabecera, prerrequisitos y referencias de un bundle. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
*.bundle
*.bdl
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

interpretar la cabecera, prerrequisitos y referencias de un bundle. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### firma de cabecera

Aplicar las reglas de firma de cabecera. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### prerrequisitos

Aplicar las reglas de prerrequisitos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### referencias

Aplicar las reglas de referencias. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### pack embebido

Aplicar las reglas de pack embebido. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### validación

Aplicar las reglas de validación. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

## Funciones y reglas

### Cabecera

El archivo comienza con una firma de versión de bundle.

Lee la primera línea y rechaza otra firma. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Prerrequisitos

Las líneas con OID negativo declaran objetos que el receptor debe poseer.

```bash
git bundle verify
```

Ejecuta `git bundle verify`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Referencias

Las líneas con OID positivo anuncian tips que el bundle transporta.

```bash
git bundle list-heads
```

Lista con `git bundle list-heads`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Pack

Después de la línea vacía aparece un packfile.

Valida el pack con herramientas de índice y fsck. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Versión

La versión del formato cambia qué capacidades o filtros puede representar.

Comprueba compatibilidad antes de crear. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Errores y diagnóstico

### El lector pierde el límite

Comprueba esta causa: Una longitud o terminador se interpretó como contenido. Avanza por longitudes declaradas y valida el final.

### Una extensión no se reconoce

Comprueba esta causa: Productor y consumidor soportan versiones distintas. Aplica la regla de extensiones obligatorias y opcionales del formato.

### El hash falla

Comprueba esta causa: El contenido cambió o se calculó sobre otro rango. Define el rango exacto de bytes cubierto por el checksum.

## Automatización y recuperación

Persistencia: La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Representa el ejemplo como una secuencia de campos. Calcula longitudes y terminadores antes de intentar leer o producir bytes.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`gitformat-chunk`](../formats-and-protocols/gitformat-chunk.md)
- [`gitformat-commit-graph`](../formats-and-protocols/gitformat-commit-graph.md)

## Fuente

- [gitformat-bundle - The bundle file format](https://git-scm.com/docs/gitformat-bundle)
