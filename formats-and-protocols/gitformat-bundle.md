---
title: "gitformat-bundle"
source: "https://git-scm.com/docs/gitformat-bundle"
section: "formats-and-protocols"
---

# `gitformat-bundle`

## Ejemplo de partida

```bash
# v2 git bundle
-<oid> base requerida
<oid> refs/heads/main

<datos del pack>
```

Este caso usa `gitformat-bundle` para interpretar la cabecera, prerrequisitos y referencias de un bundle. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

## Qué se deriva del ejemplo

- Entrada: los campos o mensajes producidos en el orden definido por el formato.
- Operación: interpretar la cabecera, prerrequisitos y referencias de un bundle.
- Comprobación: longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Modelo mental

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Forma de referencia

```text
*.bundle
*.bdl
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Representa el ejemplo como una secuencia de campos. Calcula longitudes y terminadores antes de intentar leer o producir bytes.

## Páginas relacionadas

- [`gitformat-chunk`](../formats-and-protocols/gitformat-chunk.md)
- [`gitformat-commit-graph`](../formats-and-protocols/gitformat-commit-graph.md)

## Fuente

- [gitformat-bundle - The bundle file format](https://git-scm.com/docs/gitformat-bundle)
