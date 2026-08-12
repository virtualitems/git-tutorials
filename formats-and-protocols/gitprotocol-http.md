---
title: "gitprotocol-http"
source: "https://git-scm.com/docs/gitprotocol-http"
section: "formats-and-protocols"
status: "source-audited"
version: "2.55.0"
---

# `gitprotocol-http`

Este caso usa `gitprotocol-http` para seguir una operación Git sobre HTTP entre cliente y servidor. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **descubrimiento de referencias**, **HTTP dumb**, **HTTP smart**, **tipos de contenido**, **sesiones sin estado**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```bash
GET /biblioteca.git/info/refs?service=git-upload-pack
POST /biblioteca.git/git-upload-pack
```

La invocación `gitprotocol-http` ejecuta esta operación: seguir una operación Git sobre HTTP entre cliente y servidor. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Sintaxis y formas de invocación

```text
<over-the-wire-protocol>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Dumb

El modo dumb publica archivos auxiliares y objetos mediante solicitudes HTTP.

Comprueba `info/refs` y `objects/info/packs`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Smart discovery

El cliente solicita `info/refs` con un parámetro service.

Valida tipo de contenido y anuncio inicial. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### RPC

El cliente envía pkt-lines al endpoint del servicio seleccionado.

Conserva cuerpo binario sin recodificar. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Estado

El protocolo smart permite solicitudes sin estado de sesión del servidor.

Incluye en cada solicitud los datos exigidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### HTTP

Autenticación, redirecciones y caché obedecen reglas HTTP además del protocolo Git.

No reenvíes credenciales a un host distinto. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitprotocol-pack`](../formats-and-protocols/gitprotocol-pack.md)
- [`gitprotocol-common`](../formats-and-protocols/gitprotocol-common.md)
- [`gitprotocol-v2`](../formats-and-protocols/gitprotocol-v2.md)

## Fuente

- [gitprotocol-http - Git HTTP-based protocols](https://git-scm.com/docs/gitprotocol-http)
