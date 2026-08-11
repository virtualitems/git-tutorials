# Formatos y protocolos

Esta sección define campos, orden, codificación, extensiones y negociación entre productor y consumidor. Lee bytes, encabezados, chunks, pkt-lines, capacidades u objetos y puede escribir ningún repositorio durante la lectura; un productor debe emitir el formato exacto.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | bytes, encabezados, chunks, pkt-lines, capacidades u objetos. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | define campos, orden, codificación, extensiones y negociación entre productor y consumidor. | Comprueba el resultado con una orden de lectura. |
| Persistencia | ningún repositorio durante la lectura; un productor debe emitir el formato exacto | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa longitudes, delimitadores, versión, hash y rechazo de entradas truncadas. |

## Preparación

Trabaja con una copia de bytes y un volcado hexadecimal. No modifiques archivos dentro de `.git` para probar un parser.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`gitformat-bundle`](gitformat-bundle.md) | interpretar la cabecera, prerrequisitos y referencias de un bundle |
| [`gitformat-chunk`](gitformat-chunk.md) | interpretar formatos que usan una tabla de fragmentos |
| [`gitformat-commit-graph`](gitformat-commit-graph.md) | interpretar el archivo commit-graph y sus cadenas |
| [`gitformat-index`](gitformat-index.md) | interpretar el archivo que representa el índice |
| [`gitformat-pack`](gitformat-pack.md) | interpretar objetos, deltas e índices de archivos pack |
| [`gitformat-signature`](gitformat-signature.md) | identificar firmas criptográficas en commits, etiquetas y protocolos |
| [`gitprotocol-capabilities`](gitprotocol-capabilities.md) | negociar capacidades en las versiones 0 y 1 del protocolo |
| [`gitprotocol-common`](gitprotocol-common.md) | interpretar pkt-line y reglas compartidas por los protocolos |
| [`gitprotocol-http`](gitprotocol-http.md) | seguir una operación Git sobre HTTP entre cliente y servidor |
| [`gitprotocol-pack`](gitprotocol-pack.md) | seguir la negociación y transferencia de un pack |
| [`gitprotocol-v2`](gitprotocol-v2.md) | seguir comandos y capacidades en la versión 2 del protocolo |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El lector pierde el límite | Una longitud o terminador se interpretó como contenido | Avanza por longitudes declaradas y valida el final. |
| Una extensión no se reconoce | Productor y consumidor soportan versiones distintas | Aplica la regla de extensiones obligatorias y opcionales del formato. |
| El hash falla | El contenido cambió o se calculó sobre otro rango | Define el rango exacto de bytes cubierto por el checksum. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
