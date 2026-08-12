---
title: "gitprotocol-pack"
source: "https://git-scm.com/docs/gitprotocol-pack"
section: "formats-and-protocols"
status: "option-expanded"
---

# `gitprotocol-pack`

Este caso usa `gitprotocol-pack` para seguir la negociación y transferencia de un pack. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **anuncio de referencias**, **wants y haves**, **negociación**, **shallow y filtros**, **packfile**.

## Responsabilidad y efecto

gitprotocol-pack define campos, orden, codificación, extensiones y negociación entre productor y consumidor. Recibe como entrada los campos o mensajes producidos en el orden definido por el formato. La operación consiste en seguir la negociación y transferencia de un pack.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

 Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```text
cliente: want <oid>
servidor: ACK <oid>
servidor: <pack>
```

La invocación `gitprotocol-pack` ejecuta esta operación: seguir la negociación y transferencia de un pack. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
<over-the-wire-protocol>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

seguir la negociación y transferencia de un pack. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### anuncio de referencias

Aplicar las reglas de anuncio de referencias. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### wants y haves

Aplicar las reglas de wants y haves. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### negociación

Aplicar las reglas de negociación. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### shallow y filtros

Aplicar las reglas de shallow y filtros. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### packfile

Aplicar las reglas de packfile. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

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

- [`gitprotocol-v2`](../formats-and-protocols/gitprotocol-v2.md)
- [`gitprotocol-http`](../formats-and-protocols/gitprotocol-http.md)
- [`gitprotocol-common`](../formats-and-protocols/gitprotocol-common.md)

## Fuente

- [gitprotocol-pack - How packs are transferred over-the-wire](https://git-scm.com/docs/gitprotocol-pack)
