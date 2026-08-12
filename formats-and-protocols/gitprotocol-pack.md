---
title: "gitprotocol-pack"
source: "https://git-scm.com/docs/gitprotocol-pack"
section: "formats-and-protocols"
status: "source-audited"
version: "2.55.0"
---

# `gitprotocol-pack`

Este caso usa `gitprotocol-pack` para seguir la negociación y transferencia de un pack. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **anuncio de referencias**, **wants y haves**, **negociación**, **shallow y filtros**, **packfile**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```text
cliente: want <oid>
servidor: ACK <oid>
servidor: <pack>
```

La invocación `gitprotocol-pack` ejecuta esta operación: seguir la negociación y transferencia de un pack. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Sintaxis y formas de invocación

```text
<over-the-wire-protocol>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Referencias

El servidor anuncia tips y capacidades antes de negociar.

Valida OID y nombres de referencia. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Want

El cliente declara objetos que quiere y capacidades seleccionadas.

Solicita solo OID permitidos por el anuncio y política. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Have

El cliente comunica commits que ya posee para hallar una base común.

Registra ACK y NAK por ronda. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Shallow y filtros

Las extensiones limitan historia u objetos cuando ambas partes las admiten.

Conserva los límites en el repositorio receptor. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Pack

La respuesta final transporta objetos faltantes en un pack, a veces por side-band.

Desmultiplexa y valida el pack. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitprotocol-v2`](../formats-and-protocols/gitprotocol-v2.md)
- [`gitprotocol-http`](../formats-and-protocols/gitprotocol-http.md)
- [`gitprotocol-common`](../formats-and-protocols/gitprotocol-common.md)

## Fuente

- [gitprotocol-pack - How packs are transferred over-the-wire](https://git-scm.com/docs/gitprotocol-pack)
