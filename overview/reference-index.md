---
title: "Referencia de Git"
source: "https://git-scm.com/docs"
section: "overview"
status: "expanded"
---

# `Referencia de Git`

Este caso usa `Referencia de Git` para localizar comandos y guías dentro de la referencia de Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

Referencia de Git organiza las páginas por estado, tipo de entrada y efecto observable. Recibe como entrada el nombre del comando o concepto que quieres consultar. La operación consiste en localizar comandos y guías dentro de la referencia de Git.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | el nombre del comando o concepto que quieres consultar. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | localizar comandos y guías dentro de la referencia de Git. | Comprueba el resultado con una orden de lectura. |
| Persistencia | La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git help -a` y los enlaces del índice. |

## Requisitos y laboratorio

No requiere un repositorio. Usa `git --version` y `git help -a` para comparar la instalación con el índice.



Antes de ejecutar el ejemplo, confirma la raíz con `git rev-parse --show-toplevel` cuando exista un repositorio. Registra `git status --short` y las referencias que puedan cambiar.

## Modelo de funcionamiento

La referencia organiza comandos de usuario, comandos de plomería, guías y formatos. El nombre de una página identifica una operación o un modelo que otras páginas reutilizan.

Usa el nombre de la operación como punto de entrada. Sigue los enlaces conceptuales cuando la sintaxis dependa de revisiones, rutas, atributos o protocolos.

Para comprobar el resultado: la página elegida enlaza su sintaxis, su modelo y sus referencias relacionadas. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git help --all
git help revisions
git help gitignore
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: el nombre del comando o concepto que quieres consultar.
- La operación observable es: localizar comandos y guías dentro de la referencia de Git.
- La comprobación se realiza mediante: la página elegida enlaza su sintaxis, su modelo y sus referencias relacionadas.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git help --all
git help revisions
git help gitignore
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | localizar comandos y guías dentro de la referencia de Git | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar Referencia de Git a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de Referencia de Git con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--all` | Amplía la selección a todos los elementos del alcance definido. |

## Selección de entradas

Identifica primero el tipo de nombre: configuración, referencia, objeto, pathspec, archivo de control o campo de protocolo. La misma cadena cambia de significado cuando cambia su posición o el comando que la recibe.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| Una página no aparece | La versión instalada no contiene ese comando | Consulta `git --version` y la fuente enlazada. |
| Un nombre no se reconoce | Se confundió una orden con una guía o un formato | Comprueba si se invoca como `git <orden>` o se consulta como documento. |
| La ruta lleva a otra sección | Una función participa en más de un flujo | Usa la página canónica indicada por el índice. |

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

Abre la página de referencia, elige un comando y sigue sus enlaces hacia una guía conceptual y un formato relacionado.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- Consulta el índice de la sección.

## Fuente

- [Referencia de Git](https://git-scm.com/docs)
