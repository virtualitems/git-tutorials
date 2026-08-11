---
title: "gitprotocol-v2"
source: "https://git-scm.com/docs/gitprotocol-v2"
section: "formats-and-protocols"
---

# `gitprotocol-v2`

## Ejemplo de partida

```text
cliente: Git-Protocol: version=2
servidor: version 2
servidor: ls-refs
servidor: fetch
```

Este caso usa `gitprotocol-v2` para seguir comandos y capacidades en la versión 2 del protocolo. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

## Qué se deriva del ejemplo

- Entrada: los campos o mensajes producidos en el orden definido por el formato.
- Operación: seguir comandos y capacidades en la versión 2 del protocolo.
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

- [`gitprotocol-pack`](../formats-and-protocols/gitprotocol-pack.md)
- [`gitprotocol-http`](../formats-and-protocols/gitprotocol-http.md)

## Fuente

- [gitprotocol-v2 - Git Wire Protocol, Version 2](https://git-scm.com/docs/gitprotocol-v2)
