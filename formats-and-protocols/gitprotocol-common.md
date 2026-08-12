---
title: "gitprotocol-common"
source: "https://git-scm.com/docs/gitprotocol-common"
section: "formats-and-protocols"
status: "source-audited"
version: "2.55.0"
---

# `gitprotocol-common`

Este caso usa `gitprotocol-common` para interpretar pkt-line y reglas compartidas por los protocolos. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **pkt-line**, **flush y delimitadores**, **texto y bytes**, **límites de longitud**, **errores**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```bash
001ecommand=ls-refs
0001
0000
```

La invocación `gitprotocol-common` ejecuta esta operación: interpretar pkt-line y reglas compartidas por los protocolos. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Sintaxis y formas de invocación

```text
<over-the-wire-protocol>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

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

## Páginas relacionadas

- [`gitprotocol-http`](../formats-and-protocols/gitprotocol-http.md)
- [`gitprotocol-capabilities`](../formats-and-protocols/gitprotocol-capabilities.md)
- [`gitprotocol-pack`](../formats-and-protocols/gitprotocol-pack.md)

## Fuente

- [gitprotocol-common - Things common to various protocols](https://git-scm.com/docs/gitprotocol-common)
