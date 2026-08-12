---
title: "gitprotocol-v2"
source: "https://git-scm.com/docs/gitprotocol-v2"
section: "formats-and-protocols"
status: "option-expanded"
---

# `gitprotocol-v2`

Este caso usa `gitprotocol-v2` para seguir comandos y capacidades en la versión 2 del protocolo. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **negociación de versión**, **anuncio de capacidades**, **`ls-refs`**, **`fetch`**, **delimitación de secciones**.

## Responsabilidad y efecto

gitprotocol-v2 define campos, orden, codificación, extensiones y negociación entre productor y consumidor. Recibe como entrada los campos o mensajes producidos en el orden definido por el formato. La operación consiste en seguir comandos y capacidades en la versión 2 del protocolo.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

 Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```text
cliente: Git-Protocol: version=2
servidor: version 2
servidor: ls-refs
servidor: fetch
```

La invocación `gitprotocol-v2` ejecuta esta operación: seguir comandos y capacidades en la versión 2 del protocolo. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
<over-the-wire-protocol>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

seguir comandos y capacidades en la versión 2 del protocolo. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### negociación de versión

Aplicar las reglas de negociación de versión. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### anuncio de capacidades

Aplicar las reglas de anuncio de capacidades. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### `ls-refs`

Aplicar las reglas de `ls-refs`. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### `fetch`

Aplicar las reglas de `fetch`. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### delimitación de secciones

Aplicar las reglas de delimitación de secciones. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

## Funciones y reglas

### Versión

El cliente solicita versión 2 por el mecanismo del transporte.

Confirma que la primera respuesta declara version 2. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Capacidades

El servidor anuncia comandos y capacidades como pkt-lines.

No envíes un comando que no fue anunciado. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### ls-refs

`ls-refs` solicita referencias con prefijos y atributos opcionales.

Termina argumentos con flush y valida cada respuesta. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### fetch

`fetch` negocia wants, haves, shallow, filtros y packfile por secciones.

Respeta delimitadores entre acknowledgments y packfile. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Estado

Cada comando forma una solicitud delimitada; la conexión puede atender más de una.

Restablece el parser al terminar la respuesta. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Errores y diagnóstico

### El lector pierde el límite

Comprueba esta causa: Una longitud o terminador se interpretó como contenido. Avanza por longitudes declaradas y valida el final.

### Una extensión no se reconoce

Comprueba esta causa: Productor y consumidor soportan versiones distintas. Aplica la regla de extensiones obligatorias y opcionales del formato.

### El hash falla

Comprueba esta causa: El contenido cambió o se calculó sobre otro rango. Define el rango exacto de bytes cubierto por el checksum.

## Automatización y recuperación

Persistencia: La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Representa el ejemplo como una secuencia de campos. Calcula longitudes y terminadores antes de intentar leer o producir bytes.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`gitprotocol-pack`](../formats-and-protocols/gitprotocol-pack.md)
- [`gitprotocol-http`](../formats-and-protocols/gitprotocol-http.md)

## Fuente

- [gitprotocol-v2 - Git Wire Protocol, Version 2](https://git-scm.com/docs/gitprotocol-v2)
