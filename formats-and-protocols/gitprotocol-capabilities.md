---
title: "gitprotocol-capabilities"
source: "https://git-scm.com/docs/gitprotocol-capabilities"
section: "formats-and-protocols"
status: "source-audited"
version: "2.55.0"
---

# `gitprotocol-capabilities`

Este caso usa `gitprotocol-capabilities` para negociar capacidades en las versiones 0 y 1 del protocolo. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **anuncio**, **capacidades por servicio**, **agente**, **side-band**, **compatibilidad**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```bash
multi_ack thin-pack side-band-64k ofs-delta
```

La invocación `gitprotocol-capabilities` ejecuta esta operación: negociar capacidades en las versiones 0 y 1 del protocolo. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Sintaxis y formas de invocación

```text
<over-the-wire-protocol>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Anuncio

En v0/v1 las capacidades acompañan la primera referencia anunciada.

Separa el OID y la lista después de NUL. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Negociación

El cliente solicita solo capacidades que el servidor anunció.

Rechaza combinaciones no anunciadas. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Side-band

Side-band multiplexa pack, progreso y error por banda.

Desmultiplexa el primer byte de cada payload. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Agente

agent comunica una versión informativa, no una autorización.

No la uses como única decisión de compatibilidad. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Servicio

Upload-pack y receive-pack no comparten todas las capacidades.

Mantén conjuntos separados por servicio. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitprotocol-common`](../formats-and-protocols/gitprotocol-common.md)
- [`gitformat-signature`](../formats-and-protocols/gitformat-signature.md)
- [`gitprotocol-http`](../formats-and-protocols/gitprotocol-http.md)

## Fuente

- [gitprotocol-capabilities - Protocol v0 and v1 capabilities](https://git-scm.com/docs/gitprotocol-capabilities)
