---
title: "gitformat-index"
source: "https://git-scm.com/docs/gitformat-index"
section: "formats-and-protocols"
status: "source-audited"
version: "2.55.0"
---

# `gitformat-index`

Este caso usa `gitformat-index` para interpretar el archivo que representa el índice. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **firma y versión**, **entradas de caché**, **etapas**, **extensiones**, **checksum**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```text
índice: cabecera DIRC | entradas ordenadas por ruta | extensiones | hash
```

La invocación `gitformat-index` ejecuta esta operación: interpretar el archivo que representa el índice. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Sintaxis y formas de invocación

```text
$GIT_DIR/index
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Cabecera

DIRC, versión y número de entradas preceden el contenido.

Rechaza versiones no soportadas. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Entrada

Cada entrada contiene metadatos stat, OID, flags y ruta.

Compara con `ls-files --stage --debug`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Etapas

Los bits de etapa representan base, ours y theirs durante conflictos.

Crea un conflicto y consulta las tres entradas. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Extensiones

La firma de una extensión determina si puede ignorarse o es obligatoria.

Aplica la regla por mayúscula o minúscula inicial. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Checksum

El tráiler protege los bytes anteriores del archivo.

Calcula con el algoritmo del repositorio. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitformat-pack`](../formats-and-protocols/gitformat-pack.md)
- [`gitformat-commit-graph`](../formats-and-protocols/gitformat-commit-graph.md)
- [`gitformat-signature`](../formats-and-protocols/gitformat-signature.md)

## Fuente

- [gitformat-index - Git index format](https://git-scm.com/docs/gitformat-index)
