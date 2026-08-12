---
title: "gitformat-pack"
source: "https://git-scm.com/docs/gitformat-pack"
section: "formats-and-protocols"
status: "source-audited"
version: "2.55.0"
---

# `gitformat-pack`

Este caso usa `gitformat-pack` para interpretar objetos, deltas e índices de archivos pack. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **cabecera**, **representación de objetos**, **deltas**, **tráiler**, **índice asociado**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```text
pack: 'PACK' | versión | cantidad | objetos y deltas | suma de comprobación
```

La invocación `gitformat-pack` ejecuta esta operación: interpretar objetos, deltas e índices de archivos pack. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Sintaxis y formas de invocación

```text
$GIT_DIR/objects/pack/pack-.{pack,idx}
$GIT_DIR/objects/pack/pack-.rev
$GIT_DIR/objects/pack/pack-*.mtimes
$GIT_DIR/objects/pack/multi-pack-index
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Cabecera

PACK, versión y número de objetos abren el archivo.

Valida antes de recorrer objetos. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Objeto

Cada entrada declara tipo y tamaño mediante enteros de longitud variable.

Rechaza entradas que excedan el archivo. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Delta

OFS_DELTA usa distancia dentro del pack y REF_DELTA usa OID base.

Resuelve la base antes de aplicar instrucciones. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Tráiler

El hash final cubre el contenido anterior del pack.

Compara con `index-pack`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Índice

El índice externo relaciona OID con offsets y checksums.

Ejecuta `verify-pack` sobre el índice. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitformat-signature`](../formats-and-protocols/gitformat-signature.md)
- [`gitformat-index`](../formats-and-protocols/gitformat-index.md)
- [`gitprotocol-capabilities`](../formats-and-protocols/gitprotocol-capabilities.md)

## Fuente

- [gitformat-pack - Git pack format](https://git-scm.com/docs/gitformat-pack)
