---
title: "gitformat-chunk"
source: "https://git-scm.com/docs/gitformat-chunk"
section: "formats-and-protocols"
---

# `gitformat-chunk`

## Ejemplo de partida

```text
cabecera -> tabla de fragmentos -> fragmento A -> fragmento B
```

Este caso usa `gitformat-chunk` para interpretar formatos que usan una tabla de fragmentos. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

## Qué se deriva del ejemplo

- Entrada: los campos o mensajes producidos en el orden definido por el formato.
- Operación: interpretar formatos que usan una tabla de fragmentos.
- Comprobación: longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Modelo mental

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Forma de referencia

```text
cabecera -> tabla de fragmentos -> fragmento A -> fragmento B
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Representa el ejemplo como una secuencia de campos. Calcula longitudes y terminadores antes de intentar leer o producir bytes.

## Páginas relacionadas

- [`gitformat-commit-graph`](../formats-and-protocols/gitformat-commit-graph.md)
- [`gitformat-bundle`](../formats-and-protocols/gitformat-bundle.md)
- [`gitformat-index`](../formats-and-protocols/gitformat-index.md)

## Fuente

- [gitformat-chunk - Chunk-based file formats](https://git-scm.com/docs/gitformat-chunk)
