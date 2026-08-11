---
title: "gitprotocol-common"
source: "https://git-scm.com/docs/gitprotocol-common"
section: "formats-and-protocols"
---

# `gitprotocol-common`

## Ejemplo de partida

```bash
001ecommand=ls-refs
0001
0000
```

Este caso usa `gitprotocol-common` para interpretar pkt-line y reglas compartidas por los protocolos. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

## Qué se deriva del ejemplo

- Entrada: los campos o mensajes producidos en el orden definido por el formato.
- Operación: interpretar pkt-line y reglas compartidas por los protocolos.
- Comprobación: longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Modelo mental

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Forma de referencia

```text
<over-the-wire-protocol>
```

Los elementos entre `<` y `>` se sustituyen por valores.

## Práctica

Representa el ejemplo como una secuencia de campos. Calcula longitudes y terminadores antes de intentar leer o producir bytes.

## Páginas relacionadas

- [`gitprotocol-http`](../formats-and-protocols/gitprotocol-http.md)
- [`gitprotocol-capabilities`](../formats-and-protocols/gitprotocol-capabilities.md)
- [`gitprotocol-pack`](../formats-and-protocols/gitprotocol-pack.md)

## Fuente

- [gitprotocol-common - Things common to various protocols](https://git-scm.com/docs/gitprotocol-common)
