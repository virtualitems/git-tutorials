---
title: "gitformat-commit-graph"
source: "https://git-scm.com/docs/gitformat-commit-graph"
section: "formats-and-protocols"
status: "source-audited"
version: "2.55.0"
---

# `gitformat-commit-graph`

Este caso usa `gitformat-commit-graph` para interpretar el archivo commit-graph y sus cadenas. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **cabecera**, **fanout de OID**, **datos de commit**, **generaciones**, **cadenas por capas**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```text
commit-graph: cabecera | tabla de fragmentos | OIDF | OIDL | CDAT
```

La invocación `gitformat-commit-graph` ejecuta esta operación: interpretar el archivo commit-graph y sus cadenas. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Sintaxis y formas de invocación

```text
$GIT_DIR/objects/info/commit-graph
$GIT_DIR/objects/info/commit-graphs/*
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Cabecera

La firma, versión, algoritmo hash y número de chunks gobiernan el resto.

Valida antes de leer offsets. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Fanout

La tabla fanout limita el rango de búsqueda por prefijo de OID.

Comprueba que los conteos no disminuyan. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Commits

Los chunks de lookup y datos relacionan OID, tree, padres, fecha y generación.

Cruza un commit con `cat-file`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Generación

Los números de generación aceleran recorridos bajo reglas de monotonía.

Valida padres y correcciones de overflow. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Cadenas

Una cadena divide el grafo en capas con hashes y orden definidos.

Ejecuta verificación del commit-graph. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitformat-index`](../formats-and-protocols/gitformat-index.md)
- [`gitformat-chunk`](../formats-and-protocols/gitformat-chunk.md)
- [`gitformat-pack`](../formats-and-protocols/gitformat-pack.md)

## Fuente

- [gitformat-commit-graph - Git commit-graph format](https://git-scm.com/docs/gitformat-commit-graph)
