---
title: "gitdiffcore"
source: "https://git-scm.com/docs/gitdiffcore"
section: "guides"
status: "expanded"
---

# `gitdiffcore`

Este caso usa `gitdiffcore` para entender las transformaciones que producen la salida de diff. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **pares de archivos**, **detección de ruptura**, **renombres y copias**, **selección por contenido**, **orden de salida**.

## Alcance y responsabilidad

gitdiffcore define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en entender las transformaciones que producen la salida de diff.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | el estado de repositorio representado por el caso. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | entender las transformaciones que producen la salida de diff. | Comprueba el resultado con una orden de lectura. |
| Persistencia | La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa una consulta que muestre la regla efectiva y su origen. |

## Requisitos y laboratorio

Crea un repositorio con dos commits y archivos bajo dos directorios. Cambia una regla por vez y registra el resultado.

```bash
lab_dir="$(mktemp -d)"
git init "$lab_dir/proyecto"
git -C "$lab_dir/proyecto" config user.name "Persona de prueba"
git -C "$lab_dir/proyecto" config user.email "prueba@example.test"
printf 'línea base\n' > "$lab_dir/proyecto/archivo.txt"
git -C "$lab_dir/proyecto" add archivo.txt
git -C "$lab_dir/proyecto" commit -m "base"
cd "$lab_dir/proyecto"
```

Antes de ejecutar el ejemplo, confirma la raíz con `git rev-parse --show-toplevel` cuando exista un repositorio. Registra `git status --short` y las referencias que puedan cambiar.

## Modelo de funcionamiento

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

Para comprobar el resultado: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git diff -M -C --find-copies-harder HEAD~1 HEAD
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: el estado de repositorio representado por el caso.
- La operación observable es: entender las transformaciones que producen la salida de diff.
- La comprobación se realiza mediante: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git diff *
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | entender las transformaciones que producen la salida de diff | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| pares de archivos | Aplicar las reglas de pares de archivos. | Cambia una entrada y comprueba el efecto que define la guía. |
| detección de ruptura | Aplicar las reglas de detección de ruptura. | Cambia una entrada y comprueba el efecto que define la guía. |
| renombres y copias | Aplicar las reglas de renombres y copias. | Cambia una entrada y comprueba el efecto que define la guía. |
| selección por contenido | Aplicar las reglas de selección por contenido. | Cambia una entrada y comprueba el efecto que define la guía. |
| orden de salida | Aplicar las reglas de orden de salida. | Cambia una entrada y comprueba el efecto que define la guía. |

## Reglas por área

| Área | Regla | Comprobación reproducible |
| --- | --- | --- |
| Pares | El motor recibe pares de archivos antes y después y transforma esa lista. | Observa `--raw` para identificar modos y hashes. |
| Ruptura | La detección de ruptura puede convertir una modificación extensa en borrado y creación. | Varía el umbral de `-B` sobre el mismo cambio. |
| Renombres | La detección relaciona un origen borrado con un destino creado por similitud. | Compara salida con y sin `-M`. |
| Copias | La detección de copia busca un origen cuyo contenido explique el destino. | Compara salida con `-C` y un origen sin cambios. |
| Pickaxe | `-S` y `-G` seleccionan cambios por variación de texto o coincidencia en el parche. | Prueba ambos criterios sobre el mismo commit. |


## Selección de entradas

Identifica primero el tipo de nombre: configuración, referencia, objeto, pathspec, archivo de control o campo de protocolo. La misma cadena cambia de significado cuando cambia su posición o el comando que la recibe.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| La regla no se aplica | El patrón, alcance o precedencia no coincide | Consulta la regla efectiva y el archivo que la definió. |
| Una revisión se interpreta como ruta | El nombre es ambiguo | Separa revisiones y rutas con `--`. |
| El resultado cambia entre equipos | La regla vive en configuración no compartida | Decide qué parte debe versionarse en el repositorio. |

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

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`giteveryday`](../guides/giteveryday.md)
- [`gitcvs-migration`](../guides/gitcvs-migration.md)
- [`gitfaq`](../guides/gitfaq.md)

## Fuente

- [gitdiffcore - Tweaking diff output](https://git-scm.com/docs/gitdiffcore)
