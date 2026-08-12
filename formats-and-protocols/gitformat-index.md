---
title: "gitformat-index"
source: "https://git-scm.com/docs/gitformat-index"
section: "formats-and-protocols"
status: "option-expanded"
---

# `gitformat-index`

Este caso usa `gitformat-index` para interpretar el archivo que representa el índice. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **firma y versión**, **entradas de caché**, **etapas**, **extensiones**, **checksum**.

## Responsabilidad y efecto

gitformat-index define campos, orden, codificación, extensiones y negociación entre productor y consumidor. Recibe como entrada los campos o mensajes producidos en el orden definido por el formato. La operación consiste en interpretar el archivo que representa el índice.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

 Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```text
índice: cabecera DIRC | entradas ordenadas por ruta | extensiones | hash
```

La invocación `gitformat-index` ejecuta esta operación: interpretar el archivo que representa el índice. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
$GIT_DIR/index
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

interpretar el archivo que representa el índice. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### firma y versión

Aplicar las reglas de firma y versión. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### entradas de caché

Aplicar las reglas de entradas de caché. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### etapas

Aplicar las reglas de etapas. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### extensiones

Aplicar las reglas de extensiones. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### checksum

Aplicar las reglas de checksum. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

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

- [`gitformat-pack`](../formats-and-protocols/gitformat-pack.md)
- [`gitformat-commit-graph`](../formats-and-protocols/gitformat-commit-graph.md)
- [`gitformat-signature`](../formats-and-protocols/gitformat-signature.md)

## Fuente

- [gitformat-index - Git index format](https://git-scm.com/docs/gitformat-index)
