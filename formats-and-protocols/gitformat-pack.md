---
title: "gitformat-pack"
source: "https://git-scm.com/docs/gitformat-pack"
section: "formats-and-protocols"
---

# `gitformat-pack`

## Ejemplo de partida

```text
pack: 'PACK' | versión | cantidad | objetos y deltas | suma de comprobación
```

Este caso usa `gitformat-pack` para interpretar objetos, deltas e índices de archivos pack. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

## Qué se deriva del ejemplo

- Entrada: los campos o mensajes producidos en el orden definido por el formato.
- Operación: interpretar objetos, deltas e índices de archivos pack.
- Comprobación: longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Modelo mental

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Forma de referencia

```text
$GIT_DIR/objects/pack/pack-.{pack,idx}
$GIT_DIR/objects/pack/pack-.rev
$GIT_DIR/objects/pack/pack-*.mtimes
$GIT_DIR/objects/pack/multi-pack-index
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Representa el ejemplo como una secuencia de campos. Calcula longitudes y terminadores antes de intentar leer o producir bytes.

## Páginas relacionadas

- [`gitformat-signature`](../formats-and-protocols/gitformat-signature.md)
- [`gitformat-index`](../formats-and-protocols/gitformat-index.md)
- [`gitprotocol-capabilities`](../formats-and-protocols/gitprotocol-capabilities.md)

## Fuente

- [gitformat-pack - Git pack format](https://git-scm.com/docs/gitformat-pack)
