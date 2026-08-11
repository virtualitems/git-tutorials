---
title: "gitprotocol-pack"
source: "https://git-scm.com/docs/gitprotocol-pack"
section: "formats-and-protocols"
status: "expanded"
---

# `gitprotocol-pack`

Este caso usa `gitprotocol-pack` para seguir la negociación y transferencia de un pack. Los identificadores y campos del ejemplo representan valores de una captura o archivo de práctica. Conserva el orden y los delimitadores cuando cambies esos valores.

La guía cubre **anuncio de referencias**, **wants y haves**, **negociación**, **shallow y filtros**, **packfile**.

## Alcance y responsabilidad

gitprotocol-pack define campos, orden, codificación, extensiones y negociación entre productor y consumidor. Recibe como entrada los campos o mensajes producidos en el orden definido por el formato. La operación consiste en seguir la negociación y transferencia de un pack.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | los campos o mensajes producidos en el orden definido por el formato. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | seguir la negociación y transferencia de un pack. | Comprueba el resultado con una orden de lectura. |
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
cliente: want <oid>
servidor: ACK <oid>
servidor: <pack>
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: los campos o mensajes producidos en el orden definido por el formato.
- La operación observable es: seguir la negociación y transferencia de un pack.
- La comprobación se realiza mediante: longitudes, separadores y tipos permiten al consumidor reconocer cada límite.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
<over-the-wire-protocol>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | seguir la negociación y transferencia de un pack | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| anuncio de referencias | Aplicar las reglas de anuncio de referencias. | Cambia una entrada y comprueba el efecto que define la guía. |
| wants y haves | Aplicar las reglas de wants y haves. | Cambia una entrada y comprueba el efecto que define la guía. |
| negociación | Aplicar las reglas de negociación. | Cambia una entrada y comprueba el efecto que define la guía. |
| shallow y filtros | Aplicar las reglas de shallow y filtros. | Cambia una entrada y comprueba el efecto que define la guía. |
| packfile | Aplicar las reglas de packfile. | Cambia una entrada y comprueba el efecto que define la guía. |

## Reglas por área

| Área | Regla | Comprobación reproducible |
| --- | --- | --- |
| Referencias | El servidor anuncia tips y capacidades antes de negociar. | Valida OID y nombres de referencia. |
| Want | El cliente declara objetos que quiere y capacidades seleccionadas. | Solicita solo OID permitidos por el anuncio y política. |
| Have | El cliente comunica commits que ya posee para hallar una base común. | Registra ACK y NAK por ronda. |
| Shallow y filtros | Las extensiones limitan historia u objetos cuando ambas partes las admiten. | Conserva los límites en el repositorio receptor. |
| Pack | La respuesta final transporta objetos faltantes en un pack, a veces por side-band. | Desmultiplexa y valida el pack. |


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

- [`gitprotocol-v2`](../formats-and-protocols/gitprotocol-v2.md)
- [`gitprotocol-http`](../formats-and-protocols/gitprotocol-http.md)
- [`gitprotocol-common`](../formats-and-protocols/gitprotocol-common.md)

## Fuente

- [gitprotocol-pack - How packs are transferred over-the-wire](https://git-scm.com/docs/gitprotocol-pack)
