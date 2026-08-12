---
title: "gitformat-commit-graph"
source: "https://git-scm.com/docs/gitformat-commit-graph"
section: "formats-and-protocols"
status: "option-expanded"
---

# `gitformat-commit-graph`

Este caso usa `gitformat-commit-graph` para interpretar el archivo commit-graph y sus cadenas. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **cabecera**, **fanout de OID**, **datos de commit**, **generaciones**, **cadenas por capas**.

## Responsabilidad y efecto

gitformat-commit-graph define campos, orden, codificación, extensiones y negociación entre productor y consumidor. Recibe como entrada los campos o mensajes producidos en el orden definido por el formato. La operación consiste en interpretar el archivo commit-graph y sus cadenas.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

## Ejemplo mínimo

```text
commit-graph: cabecera | tabla de fragmentos | OIDF | OIDL | CDAT
```

La invocación `gitformat-commit-graph` ejecuta esta operación: interpretar el archivo commit-graph y sus cadenas. Después, longitudes, separadores y tipos permiten al consumidor reconocer cada límite. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
$GIT_DIR/objects/info/commit-graph
$GIT_DIR/objects/info/commit-graphs/*
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

interpretar el archivo commit-graph y sus cadenas. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### cabecera

Aplicar las reglas de cabecera. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### fanout de OID

Aplicar las reglas de fanout de OID. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### datos de commit

Aplicar las reglas de datos de commit. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### generaciones

Aplicar las reglas de generaciones. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### cadenas por capas

Aplicar las reglas de cadenas por capas. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

## Funciones y reglas

### Cabecera

La firma, versión, algoritmo hash y número de chunks gobiernan el resto.

Valida antes de leer offsets. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Fanout

La tabla fanout limita el rango de búsqueda por prefijo de OID.

Comprueba que los conteos no disminuyan. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Commits

Los chunks de lookup y datos relacionan OID, tree, padres, fecha y generación.

Cruza un commit con `cat-file`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Generación

Los números de generación aceleran recorridos bajo reglas de monotonía.

Valida padres y correcciones de overflow. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Cadenas

Una cadena divide el grafo en capas con hashes y orden definidos.

Ejecuta verificación del commit-graph. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

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

- [`gitformat-index`](../formats-and-protocols/gitformat-index.md)
- [`gitformat-chunk`](../formats-and-protocols/gitformat-chunk.md)
- [`gitformat-pack`](../formats-and-protocols/gitformat-pack.md)

## Fuente

- [gitformat-commit-graph - Git commit-graph format](https://git-scm.com/docs/gitformat-commit-graph)
