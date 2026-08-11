---
title: "gitprotocol-capabilities"
source: "https://git-scm.com/docs/gitprotocol-capabilities"
section: "formats-and-protocols"
---

# `gitprotocol-capabilities`

## Ejemplo de partida

```bash
multi_ack thin-pack side-band-64k ofs-delta
```

Este caso usa `gitprotocol-capabilities` para negociar capacidades en las versiones 0 y 1 del protocolo. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

## Qué se deriva del ejemplo

- Entrada: los campos o mensajes producidos en el orden definido por el formato.
- Operación: negociar capacidades en las versiones 0 y 1 del protocolo.
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

- [`gitprotocol-common`](../formats-and-protocols/gitprotocol-common.md)
- [`gitformat-signature`](../formats-and-protocols/gitformat-signature.md)
- [`gitprotocol-http`](../formats-and-protocols/gitprotocol-http.md)

## Fuente

- [gitprotocol-capabilities - Protocol v0 and v1 capabilities](https://git-scm.com/docs/gitprotocol-capabilities)
