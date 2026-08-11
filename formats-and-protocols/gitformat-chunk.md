---
title: "gitformat-chunk"
source: "https://git-scm.com/docs/gitformat-chunk"
section: "formats-and-protocols"
status: "expanded"
---

# `gitformat-chunk`

Este caso usa `gitformat-chunk` para interpretar formatos que usan una tabla de fragmentos. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **tabla de chunks**, **identificadores**, **offsets**, **chunk terminal**, **extensión**.

## Alcance y responsabilidad

gitformat-chunk define campos, orden, codificación, extensiones y negociación entre productor y consumidor. Recibe como entrada los campos o mensajes producidos en el orden definido por el formato. La operación consiste en interpretar formatos que usan una tabla de fragmentos.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | los campos o mensajes producidos en el orden definido por el formato. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | interpretar formatos que usan una tabla de fragmentos. | Comprueba el resultado con una orden de lectura. |
| Persistencia | La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa longitudes, delimitadores, versión, hash y rechazo de entradas truncadas. |

## Requisitos y laboratorio

Trabaja con una copia de bytes y un volcado hexadecimal. No modifiques archivos dentro de `.git` para probar un parser.



Antes de ejecutar el ejemplo, confirma la raíz con `git rev-parse --show-toplevel` cuando exista un repositorio. Registra `git status --short` y las referencias que puedan cambiar.

## Modelo de funcionamiento

Un formato define campos, orden y codificación. Productores y consumidores deben interpretar los mismos bytes; una diferencia de longitud o terminador cambia el mensaje.

Lee primero la cabecera y las tablas que describen el resto. Usa las longitudes declaradas para avanzar, no patrones de texto que puedan aparecer dentro de los datos.

Para comprobar el resultado: longitudes, separadores y tipos permiten al consumidor reconocer cada límite. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```text
cabecera -> tabla de fragmentos -> fragmento A -> fragmento B
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: los campos o mensajes producidos en el orden definido por el formato.
- La operación observable es: interpretar formatos que usan una tabla de fragmentos.
- La comprobación se realiza mediante: longitudes, separadores y tipos permiten al consumidor reconocer cada límite.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
cabecera -> tabla de fragmentos -> fragmento A -> fragmento B
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | interpretar formatos que usan una tabla de fragmentos | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| tabla de chunks | Aplicar las reglas de tabla de chunks. | Cambia una entrada y comprueba el efecto que define la guía. |
| identificadores | Aplicar las reglas de identificadores. | Cambia una entrada y comprueba el efecto que define la guía. |
| offsets | Aplicar las reglas de offsets. | Cambia una entrada y comprueba el efecto que define la guía. |
| chunk terminal | Aplicar las reglas de chunk terminal. | Cambia una entrada y comprueba el efecto que define la guía. |
| extensión | Aplicar las reglas de extensión. | Cambia una entrada y comprueba el efecto que define la guía. |

## Reglas por área

| Área | Regla | Comprobación reproducible |
| --- | --- | --- |
| Tabla | La tabla asocia un identificador de chunk con su offset. | Comprueba orden y número de entradas. |
| Offset | El tamaño de un chunk se deriva del siguiente offset. | Rechaza offsets fuera del archivo o en retroceso. |
| Terminal | Una entrada terminal marca el final de datos de chunks. | Comprueba que no se trate como contenido. |
| Identificador | El consumidor decide qué IDs entiende y qué regla aplica a desconocidos. | Prueba un ID opcional desconocido. |
| Extensión | Añadir chunks permite ampliar el formato sin cambiar campos existentes. | Conserva los chunks desconocidos cuando el contrato lo requiera. |


## Selección de entradas

Conserva los bytes de entrada. Verifica la firma o versión antes de interpretar campos dependientes. Rechaza longitudes fuera del archivo, offsets que retrocedan, solapamientos no permitidos y checksums que no coincidan.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El lector pierde el límite | Una longitud o terminador se interpretó como contenido | Avanza por longitudes declaradas y valida el final. |
| Una extensión no se reconoce | Productor y consumidor soportan versiones distintas | Aplica la regla de extensiones obligatorias y opcionales del formato. |
| El hash falla | El contenido cambió o se calculó sobre otro rango | Define el rango exacto de bytes cubierto por el checksum. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Representa el ejemplo como una secuencia de campos. Calcula longitudes y terminadores antes de intentar leer o producir bytes.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`gitformat-commit-graph`](../formats-and-protocols/gitformat-commit-graph.md)
- [`gitformat-bundle`](../formats-and-protocols/gitformat-bundle.md)
- [`gitformat-index`](../formats-and-protocols/gitformat-index.md)

## Fuente

- [gitformat-chunk - Chunk-based file formats](https://git-scm.com/docs/gitformat-chunk)
