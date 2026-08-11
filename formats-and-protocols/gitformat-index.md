---
title: "gitformat-index"
source: "https://git-scm.com/docs/gitformat-index"
section: "formats-and-protocols"
---

# `gitformat-index`

## Ejemplo de partida

```text
índice: cabecera DIRC | entradas ordenadas por ruta | extensiones | hash
```

Este caso usa `gitformat-index` para interpretar el archivo que representa el índice. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

## Qué se deriva del ejemplo

- Entrada: los campos o mensajes producidos en el orden definido por el formato.
- Operación: interpretar el archivo que representa el índice.
- Comprobación: longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Modelo mental

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Forma de referencia

```text
$GIT_DIR/index
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Representa el ejemplo como una secuencia de campos. Calcula longitudes y terminadores antes de intentar leer o producir bytes.

## Páginas relacionadas

- [`gitformat-pack`](../formats-and-protocols/gitformat-pack.md)
- [`gitformat-commit-graph`](../formats-and-protocols/gitformat-commit-graph.md)
- [`gitformat-signature`](../formats-and-protocols/gitformat-signature.md)

## Fuente

- [gitformat-index - Git index format](https://git-scm.com/docs/gitformat-index)
