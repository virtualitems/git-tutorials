---
title: "gitformat-signature"
source: "https://git-scm.com/docs/gitformat-signature"
section: "formats-and-protocols"
---

# `gitformat-signature`

## Ejemplo de partida

```bash
-----BEGIN PGP SIGNATURE-----
<datos de firma>
-----END PGP SIGNATURE-----
```

Este caso usa `gitformat-signature` para identificar firmas criptográficas en commits, etiquetas y protocolos. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

## Qué se deriva del ejemplo

- Entrada: los campos o mensajes producidos en el orden definido por el formato.
- Operación: identificar firmas criptográficas en commits, etiquetas y protocolos.
- Comprobación: longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Modelo mental

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Forma de referencia

```text
<[tag|commit] object header(s)>
<over-the-wire protocol>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Representa el ejemplo como una secuencia de campos. Calcula longitudes y terminadores antes de intentar leer o producir bytes.

## Páginas relacionadas

- [`gitprotocol-capabilities`](../formats-and-protocols/gitprotocol-capabilities.md)
- [`gitformat-pack`](../formats-and-protocols/gitformat-pack.md)
- [`gitprotocol-common`](../formats-and-protocols/gitprotocol-common.md)

## Fuente

- [gitformat-signature - Git cryptographic signature formats](https://git-scm.com/docs/gitformat-signature)
