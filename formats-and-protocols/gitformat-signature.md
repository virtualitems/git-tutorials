---
title: "gitformat-signature"
source: "https://git-scm.com/docs/gitformat-signature"
section: "formats-and-protocols"
status: "source-audited"
version: "2.55.0"
---

# `gitformat-signature`

Este caso usa `gitformat-signature` para identificar firmas criptográficas en commits, etiquetas y protocolos. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **firmas abiertas**, **firmas SSH**, **firmas X.509**, **ubicación en objetos**, **verificación**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```bash
-----BEGIN PGP SIGNATURE-----
<datos de firma>
-----END PGP SIGNATURE-----
```

La invocación `gitformat-signature` ejecuta esta operación: identificar firmas criptográficas en commits, etiquetas y protocolos. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite.

## Sintaxis y formas de invocación

```text
<[tag|commit] object header(s)>
<over-the-wire protocol>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### OpenPGP

Una firma armored se reconoce por sus delimitadores y cubre el payload definido.

Verifica con la herramienta configurada. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### SSH

Una firma SSH usa su contenedor y una clave permitida para asociar identidad.

Configura el archivo de firmantes permitidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### X.509

Una firma X.509 se valida contra certificados y confianza configurada.

Comprueba cadena y vigencia. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Commit

En un commit firmado la firma ocupa el encabezado gpgsig con continuación de líneas.

Inspecciona el objeto sin formato. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Tag

En un tag firmado la firma sigue al payload del tag.

Separa payload y bloque antes de verificar. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitprotocol-capabilities`](../formats-and-protocols/gitprotocol-capabilities.md)
- [`gitformat-pack`](../formats-and-protocols/gitformat-pack.md)
- [`gitprotocol-common`](../formats-and-protocols/gitprotocol-common.md)

## Fuente

- [gitformat-signature - Git cryptographic signature formats](https://git-scm.com/docs/gitformat-signature)
