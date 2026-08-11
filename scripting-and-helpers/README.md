# Automatización y comandos auxiliares

Esta sección ofrece contratos de entrada y salida para scripts, hooks y procesos auxiliares. Lee stdin, argumentos, configuración o metadatos del repositorio y puede escribir stdout, cachés o archivos indicados por cada contrato.

## Modelo de la sección

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | stdin, argumentos, configuración o metadatos del repositorio. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | ofrece contratos de entrada y salida para scripts, hooks y procesos auxiliares. | Comprueba el resultado con una orden de lectura. |
| Persistencia | stdout, cachés o archivos indicados por cada contrato | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa stdout, stderr y el código de terminación con casos positivos y negativos. |

## Preparación

Ejecuta los ejemplos en un script con `set -u`. Captura la salida y el código antes de activar `set -e`.

## Ruta de trabajo

1. Abre la guía de la función que produce el estado de entrada.
2. Ejecuta el ejemplo en el laboratorio de esa guía.
3. Comprueba el resultado con una operación de lectura.
4. Prueba un caso sin coincidencias o con una entrada inválida.
5. Registra la versión con `git --version` cuando el resultado forme parte de una automatización.

## Inventario

| Página | Responsabilidad |
| --- | --- |
| [`git check-attr`](check-attr.md) | consultar los atributos que se aplican a una ruta |
| [`git check-ignore`](check-ignore.md) | explicar qué regla de exclusión afecta a una ruta |
| [`git check-mailmap`](check-mailmap.md) | convertir identidades mediante las reglas de mailmap |
| [`git check-ref-format`](check-ref-format.md) | validar la sintaxis de un nombre de referencia |
| [`git column`](column.md) | organizar líneas de entrada en columnas |
| [`git credential-cache`](credential-cache.md) | mantener credenciales durante un tiempo en memoria |
| [`git credential-store`](credential-store.md) | guardar credenciales sin cifrado en un archivo |
| [`git credential`](credential.md) | intercambiar credenciales con los ayudantes configurados |
| [`git fmt-merge-msg`](fmt-merge-msg.md) | generar el mensaje de un commit de fusión |
| [`git hook`](hook.md) | enumerar o ejecutar hooks mediante Git |
| [`git interpret-trailers`](interpret-trailers.md) | analizar y añadir campos al final de mensajes de commit |
| [`git mailinfo`](mailinfo.md) | separar metadatos, mensaje y parche de un correo |
| [`git mailsplit`](mailsplit.md) | dividir un buzón mbox o Maildir en mensajes |
| [`git merge-one-file`](merge-one-file.md) | resolver una ruta durante una fusión de tres vías |
| [`git patch-id`](patch-id.md) | calcular una identidad estable para el contenido de un parche |
| [`git sh-i18n`](sh-i18n.md) | cargar funciones de internacionalización en scripts de shell |
| [`git sh-setup`](sh-setup.md) | cargar funciones comunes para scripts de shell de Git |
| [`git stripspace`](stripspace.md) | normalizar espacios, líneas vacías y comentarios de un mensaje |
| [`git url-parse`](url-parse.md) | extraer componentes de una URL aceptada por Git |

## Diagnóstico compartido

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| Un nombre se divide | El script usa espacios como separador para rutas | Usa NUL o el formato estructurado que admita la orden. |
| Un predicado detiene el script | El código 1 representa una respuesta negativa | Evalúa el código de forma explícita. |
| El helper espera más datos | El protocolo de stdin requiere una línea vacía o longitud | Escribe el terminador definido y conserva el orden de campos. |

## Convenciones

- `HEAD` identifica el commit actual o la referencia simbólica que lo selecciona.
- Una revisión selecciona objetos; un pathspec selecciona rutas.
- `--` separa opciones y revisiones de rutas cuando la sintaxis lo admite.
- stdout transporta resultados; stderr transporta diagnósticos.
- Un código distinto de cero puede representar una respuesta negativa en comandos de consulta.
