---
title: "gitnamespaces"
source: "https://git-scm.com/docs/gitnamespaces"
section: "guides"
status: "expanded"
---

# `gitnamespaces`

Este caso usa `gitnamespaces` para aislar conjuntos de referencias dentro de un repositorio servidor. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **aislamiento de referencias**, **selección de namespace**, **servicios de transporte**, **alcance de objetos**, **operación en servidor**.

## Alcance y responsabilidad

gitnamespaces define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en aislar conjuntos de referencias dentro de un repositorio servidor.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | el estado de repositorio representado por el caso. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | aislar conjuntos de referencias dentro de un repositorio servidor. | Comprueba el resultado con una orden de lectura. |
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
GIT_NAMESPACE=curso-a git upload-pack /srv/git/biblioteca.git
GIT_NAMESPACE=curso-b git upload-pack /srv/git/biblioteca.git
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: el estado de repositorio representado por el caso.
- La operación observable es: aislar conjuntos de referencias dentro de un repositorio servidor.
- La comprobación se realiza mediante: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
GIT_NAMESPACE=<namespace> git upload-pack
GIT_NAMESPACE=<namespace> git receive-pack
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | aislar conjuntos de referencias dentro de un repositorio servidor | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| aislamiento de referencias | Aplicar las reglas de aislamiento de referencias. | Cambia una entrada y comprueba el efecto que define la guía. |
| selección de namespace | Aplicar las reglas de selección de namespace. | Cambia una entrada y comprueba el efecto que define la guía. |
| servicios de transporte | Aplicar las reglas de servicios de transporte. | Cambia una entrada y comprueba el efecto que define la guía. |
| alcance de objetos | Aplicar las reglas de alcance de objetos. | Cambia una entrada y comprueba el efecto que define la guía. |
| operación en servidor | Aplicar las reglas de operación en servidor. | Cambia una entrada y comprueba el efecto que define la guía. |

## Reglas por área

| Área | Regla | Comprobación reproducible |
| --- | --- | --- |
| Prefijo | Un namespace inserta un prefijo interno en las referencias visibles. | Compara `git show-ref` con y sin `GIT_NAMESPACE`. |
| Objetos | Los objetos se comparten aunque las referencias queden separadas. | Resuelve un hash conocido bajo dos namespaces. |
| Transporte | Los procesos de servidor pueden seleccionar namespace por solicitud o configuración. | Clona dos vistas desde un servidor de prueba. |
| HEAD | Cada namespace puede exponer referencias distintas y requiere un HEAD coherente. | Consulta el anuncio de referencias. |
| Administración | Eliminar un namespace afecta sus referencias, no implica borrar de inmediato objetos compartidos. | Ejecuta fsck antes de mantenimiento. |


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

- [`gitremote-helpers`](../guides/gitremote-helpers.md)
- [`gitglossary`](../guides/gitglossary.md)
- [`gitsubmodules`](../guides/gitsubmodules.md)

## Fuente

- [gitnamespaces - Git namespaces](https://git-scm.com/docs/gitnamespaces)
