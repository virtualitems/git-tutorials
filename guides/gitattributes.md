---
title: "gitattributes"
source: "https://git-scm.com/docs/gitattributes"
section: "guides"
status: "expanded"
---

# `gitattributes`

Este caso usa `gitattributes` para asignar atributos a rutas para diff, merge, exportación y filtros. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **patrones y alcance**, **atributos `text` y `eol`**, **drivers de diff y merge**, **filtros `clean` y `smudge`**, **`export-ignore` y `export-subst`**.

## Alcance y responsabilidad

gitattributes define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en asignar atributos a rutas para diff, merge, exportación y filtros.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | el estado de repositorio representado por el caso. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | asignar atributos a rutas para diff, merge, exportación y filtros. | Comprueba el resultado con una orden de lectura. |
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

```ini
# .gitattributes
*.txt text eol=lf
*.bin binary
docs/*.md diff=markdown
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: el estado de repositorio representado por el caso.
- La operación observable es: asignar atributos a rutas para diff, merge, exportación y filtros.
- La comprobación se realiza mediante: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
# .gitattributes
*.txt text eol=lf
*.bin binary
docs/*.md diff=markdown
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | asignar atributos a rutas para diff, merge, exportación y filtros | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| patrones y alcance | Aplicar las reglas de patrones y alcance. | Cambia una entrada y comprueba el efecto que define la guía. |
| atributos `text` y `eol` | Aplicar las reglas de atributos `text` y `eol`. | Cambia una entrada y comprueba el efecto que define la guía. |
| drivers de diff y merge | Aplicar las reglas de drivers de diff y merge. | Cambia una entrada y comprueba el efecto que define la guía. |
| filtros `clean` y `smudge` | Aplicar las reglas de filtros `clean` y `smudge`. | Cambia una entrada y comprueba el efecto que define la guía. |
| `export-ignore` y `export-subst` | Aplicar las reglas de `export-ignore` y `export-subst`. | Cambia una entrada y comprueba el efecto que define la guía. |

## Reglas por área

| Área | Regla | Comprobación reproducible |
| --- | --- | --- |
| Patrones | Un patrón selecciona rutas; un patrón de directorio no recorre su contenido por sí solo. | Ejecuta `git check-attr -a -- ruta`. |
| Texto | `text` controla normalización y `eol` fija el final de línea en checkout. | Añade el archivo y compara el blob con `git show :ruta`. |
| Diff y merge | `diff=<driver>` y `merge=<driver>` asignan drivers configurados por nombre. | Consulta el atributo y provoca un diff o merge en el laboratorio. |
| Filtros | `filter=<driver>` conecta las acciones clean y smudge; clean afecta el contenido que entra al índice. | Compara archivo, índice y blob después de añadir. |
| Exportación | `export-ignore` excluye rutas y `export-subst` sustituye marcadores durante `git archive`. | Lista el archivo generado por `git archive`. |


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

- [`gitcli`](../guides/gitcli.md)
- [`gitworkflows`](../guides/gitworkflows.md)
- [`githooks`](../guides/githooks.md)

## Fuente

- [gitattributes - Defining attributes per path](https://git-scm.com/docs/gitattributes)
