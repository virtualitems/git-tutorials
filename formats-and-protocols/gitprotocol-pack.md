---
title: "gitprotocol-pack"
source: "https://git-scm.com/docs/gitprotocol-pack"
section: "formats-and-protocols"
---

# `gitprotocol-pack`

## Ejemplo de partida

```text
cliente: want <oid>
servidor: ACK <oid>
servidor: <pack>
```

Este caso usa `gitprotocol-pack` para seguir la negociación y transferencia de un pack. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

## Qué se deriva del ejemplo

- Entrada: los campos o mensajes producidos en el orden definido por el formato.
- Operación: seguir la negociación y transferencia de un pack.
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

- [`gitprotocol-v2`](../formats-and-protocols/gitprotocol-v2.md)
- [`gitprotocol-http`](../formats-and-protocols/gitprotocol-http.md)
- [`gitprotocol-common`](../formats-and-protocols/gitprotocol-common.md)

## Fuente

- [gitprotocol-pack - How packs are transferred over-the-wire](https://git-scm.com/docs/gitprotocol-pack)
