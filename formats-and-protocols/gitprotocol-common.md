---
title: "gitprotocol-common"
source: "https://git-scm.com/docs/gitprotocol-common"
section: "formats-and-protocols"
status: "option-expanded"
---

# `gitprotocol-common`

Este caso usa `gitprotocol-common` para interpretar pkt-line y reglas compartidas por los protocolos. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **pkt-line**, **flush y delimitadores**, **texto y bytes**, **límites de longitud**, **errores**.

## Responsabilidad y efecto

gitprotocol-common define campos, orden, codificación, extensiones y negociación entre productor y consumidor. Recibe como entrada los campos o mensajes producidos en el orden definido por el formato. La operación consiste en interpretar pkt-line y reglas compartidas por los protocolos.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

 Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```bash
001ecommand=ls-refs
0001
0000
```

La invocación `gitprotocol-common` ejecuta esta operación: interpretar pkt-line y reglas compartidas por los protocolos. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
<over-the-wire-protocol>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

interpretar pkt-line y reglas compartidas por los protocolos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### pkt-line

Aplicar las reglas de pkt-line. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### flush y delimitadores

Aplicar las reglas de flush y delimitadores. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### texto y bytes

Aplicar las reglas de texto y bytes. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### límites de longitud

Aplicar las reglas de límites de longitud. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### errores

Aplicar las reglas de errores. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

## Funciones y reglas

### Longitud

Una pkt-line comienza con cuatro dígitos hexadecimales que incluyen el prefijo.

Rechaza longitudes menores al mínimo de datos. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Flush

0000 termina una lista o fase según el protocolo.

No lo entregues como payload vacío. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Delimiter

0001 separa secciones cuando la versión lo define.

Conserva el estado de sección del parser. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Response end

0002 marca final de respuesta en contextos que lo admiten.

Comprueba la versión antes de aceptarlo. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Payload

El contenido puede ser texto o bytes; la longitud gobierna el límite.

No busques saltos de línea fuera del payload. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

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

- [`gitprotocol-http`](../formats-and-protocols/gitprotocol-http.md)
- [`gitprotocol-capabilities`](../formats-and-protocols/gitprotocol-capabilities.md)
- [`gitprotocol-pack`](../formats-and-protocols/gitprotocol-pack.md)

## Fuente

- [gitprotocol-common - Things common to various protocols](https://git-scm.com/docs/gitprotocol-common)
