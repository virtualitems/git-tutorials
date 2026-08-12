---
title: "gitformat-bundle"
source: "https://git-scm.com/docs/gitformat-bundle"
section: "formats-and-protocols"
status: "source-audited"
version: "2.55.0"
---

# `gitformat-bundle`

Este caso usa `gitformat-bundle` para interpretar la cabecera, prerrequisitos y referencias de un bundle. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **firma de cabecera**, **prerrequisitos**, **referencias**, **pack embebido**, **validación**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```bash
# v2 git bundle
-<oid> base requerida
<oid> refs/heads/main

<datos del pack>
```

La invocación `gitformat-bundle` ejecuta esta operación: interpretar la cabecera, prerrequisitos y referencias de un bundle. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Sintaxis y formas de invocación

```text
*.bundle
*.bdl
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Cabecera

El archivo comienza con una firma de versión de bundle.

Lee la primera línea y rechaza otra firma. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Prerrequisitos

Las líneas con OID negativo declaran objetos que el receptor debe poseer.

```bash
git bundle verify
```

Ejecuta `git bundle verify`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Referencias

Las líneas con OID positivo anuncian tips que el bundle transporta.

```bash
git bundle list-heads
```

Lista con `git bundle list-heads`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Pack

Después de la línea vacía aparece un packfile.

Valida el pack con herramientas de índice y fsck. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Versión

La versión del formato cambia qué capacidades o filtros puede representar.

Comprueba compatibilidad antes de crear. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitformat-chunk`](../formats-and-protocols/gitformat-chunk.md)
- [`gitformat-commit-graph`](../formats-and-protocols/gitformat-commit-graph.md)

## Fuente

- [gitformat-bundle - The bundle file format](https://git-scm.com/docs/gitformat-bundle)
