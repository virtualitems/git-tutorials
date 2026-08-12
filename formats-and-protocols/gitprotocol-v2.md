---
title: "gitprotocol-v2"
source: "https://git-scm.com/docs/gitprotocol-v2"
section: "formats-and-protocols"
status: "source-audited"
version: "2.55.0"
---

# `gitprotocol-v2`

Este caso usa `gitprotocol-v2` para seguir comandos y capacidades en la versión 2 del protocolo. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **negociación de versión**, **anuncio de capacidades**, **`ls-refs`**, **`fetch`**, **delimitación de secciones**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```text
cliente: Git-Protocol: version=2
servidor: version 2
servidor: ls-refs
servidor: fetch
```

La invocación `gitprotocol-v2` ejecuta esta operación: seguir comandos y capacidades en la versión 2 del protocolo. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Sintaxis y formas de invocación

```text
<over-the-wire-protocol>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Versión

El cliente solicita versión 2 por el mecanismo del transporte.

Confirma que la primera respuesta declara version 2. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Capacidades

El servidor anuncia comandos y capacidades como pkt-lines.

No envíes un comando que no fue anunciado. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### ls-refs

`ls-refs` solicita referencias con prefijos y atributos opcionales.

Termina argumentos con flush y valida cada respuesta. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### fetch

`fetch` negocia wants, haves, shallow, filtros y packfile por secciones.

Respeta delimitadores entre acknowledgments y packfile. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Estado

Cada comando forma una solicitud delimitada; la conexión puede atender más de una.

Restablece el parser al terminar la respuesta. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitprotocol-pack`](../formats-and-protocols/gitprotocol-pack.md)
- [`gitprotocol-http`](../formats-and-protocols/gitprotocol-http.md)

## Fuente

- [gitprotocol-v2 - Git Wire Protocol, Version 2](https://git-scm.com/docs/gitprotocol-v2)
