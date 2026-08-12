---
title: "gitformat-chunk"
source: "https://git-scm.com/docs/gitformat-chunk"
section: "formats-and-protocols"
status: "source-audited"
version: "2.55.0"
---

# `gitformat-chunk`

Este caso usa `gitformat-chunk` para interpretar formatos que usan una tabla de fragmentos. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **tabla de chunks**, **identificadores**, **offsets**, **chunk terminal**, **extensión**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```text
cabecera -> tabla de fragmentos -> fragmento A -> fragmento B
```

La invocación `gitformat-chunk` ejecuta esta operación: interpretar formatos que usan una tabla de fragmentos. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Sintaxis y formas de invocación

```text
cabecera -> tabla de fragmentos -> fragmento A -> fragmento B
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Tabla

La tabla asocia un identificador de chunk con su offset.

Comprueba orden y número de entradas. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Offset

El tamaño de un chunk se deriva del siguiente offset.

Rechaza offsets fuera del archivo o en retroceso. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Terminal

Una entrada terminal marca el final de datos de chunks.

Comprueba que no se trate como contenido. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Identificador

El consumidor decide qué IDs entiende y qué regla aplica a desconocidos.

Prueba un ID opcional desconocido. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Extensión

Añadir chunks permite ampliar el formato sin cambiar campos existentes.

Conserva los chunks desconocidos cuando el contrato lo requiera. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitformat-commit-graph`](../formats-and-protocols/gitformat-commit-graph.md)
- [`gitformat-bundle`](../formats-and-protocols/gitformat-bundle.md)
- [`gitformat-index`](../formats-and-protocols/gitformat-index.md)

## Fuente

- [gitformat-chunk - Chunk-based file formats](https://git-scm.com/docs/gitformat-chunk)
