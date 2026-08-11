---
title: "git diff-pairs"
source: "https://git-scm.com/docs/git-diff-pairs"
section: "plumbing-read"
status: "expanded"
---

# `git diff-pairs`

Este caso usa `git diff-pairs` para comparar pares de blobs recibidos por la entrada estándar. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git diff-pairs consulta objetos, referencias, índices, packs y relaciones entre commits. Recibe como entrada objetos, referencias, árboles o entradas del índice que debe leer la consulta. La operación consiste en comparar pares de blobs recibidos por la entrada estándar.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | objetos, referencias, árboles o entradas del índice que debe leer la consulta. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | comparar pares de blobs recibidos por la entrada estándar. | Comprueba el resultado con una orden de lectura. |
| Persistencia | No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa tipo, tamaño, hash, referencia o etapa impresos por una segunda consulta. |

## Requisitos y laboratorio

Crea un commit base, conserva sus hashes con `git rev-parse` y consulta cada objeto por tipo y contenido.

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

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

Para comprobar el resultado: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
printf '%s\0%s\0' "$blob_a" "$blob_b" | git diff-pairs -z
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- La operación observable es: comparar pares de blobs recibidos por la entrada estándar.
- La comprobación se realiza mediante: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git diff-pairs -z [<diff-options>]
```

### Uso verificado con `git version 2.51.1`

```text
git diff-pairs -z [<diff-options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git diff-pairs -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | comparar pares de blobs recibidos por la entrada estándar | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git diff-pairs a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Salida para scripts | Producir registros con campos y separadores definidos. | Prueba nombres con espacios y saltos de línea. |
| Validación | Comprobar el resultado de git diff-pairs con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-z` | Termina registros con NUL para evitar división por espacios o saltos de línea. |
| `-p` | Activa la forma corta del modo patch o de una opción propia de la orden. |
| `--patch` | Permite elegir hunks en vez de operar sobre el archivo completo. |
| `-s` | Activa el modo `-s`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-patch` | Desactiva el comportamiento `patch` para esta invocación. |
| `-u` | Activa el modo `-u`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-U` | Activa el modo `-U`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--unified` | Define cuántas líneas de contexto rodean cada hunk. |
| `-W` | Activa el modo `-W`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--function-context` | Activa el modo `--function-context`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--raw` | Activa el modo `--raw`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--patch-with-raw` | Activa el modo `--patch-with-raw`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--patch-with-stat` | Activa el modo `--patch-with-stat`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stat` | Resume cambios mediante conteos por ruta. |
| `--numstat` | Activa el modo `--numstat`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--shortstat` | Activa el modo `--shortstat`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-X` | Activa el modo `-X`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--dirstat` | Activa el modo `--dirstat`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--cumulative` | Activa el modo `--cumulative`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--dirstat-by-file` | Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis. |
| `--check` | Valida sin producir el efecto principal de la orden. |
| `--summary` | Activa el modo `--summary`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--name-only` | Muestra nombres de ruta sin el contenido del diff. |
| `--name-status` | Muestra nombres y estado de cada ruta. |
| `--stat-width` | Activa el modo `--stat-width`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stat-name-width` | Activa el modo `--stat-name-width`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stat-graph-width` | Activa el modo `--stat-graph-width`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stat-count` | Establece un límite numérico para la selección o el recorrido. |
| `--compact-summary` | Activa el modo `--compact-summary`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--binary` | Activa el modo `--binary`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--full-index` | Activa el modo `--full-index`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--color` | Controla el uso de secuencias de color en la salida. |
| `--ws-error-highlight` | Activa el modo `--ws-error-highlight`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--abbrev` | Reduce la representación visible del identificador sin cambiar el objeto. |
| `--src-prefix` | Activa el modo `--src-prefix`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--dst-prefix` | Activa el modo `--dst-prefix`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--line-prefix` | Activa el modo `--line-prefix`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-prefix` | Desactiva el comportamiento `prefix` para esta invocación. |
| `--default-prefix` | Activa el modo `--default-prefix`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--inter-hunk-context` | Fusiona hunks cercanos cuando la distancia no supera el límite indicado. |
| `--output-indicator-new` | Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis. |
| `--output-indicator-old` | Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis. |
| `--output-indicator-context` | Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis. |
| `-B` | Activa el modo `-B`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--break-rewrites` | Activa el modo `--break-rewrites`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-M` | Activa el modo `-M`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--find-renames` | Controla detección o búsqueda de relaciones entre entradas. |
| `-D` | Activa el modo `-D`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--irreversible-delete` | Retira elementos según las condiciones de la orden. |
| `-C` | Ejecuta Git como si se hubiera iniciado en el directorio indicado. |
| `--find-copies` | Controla detección o búsqueda de relaciones entre entradas. |
| `--find-copies-harder` | Controla detección o búsqueda de relaciones entre entradas. |
| `--no-renames` | Desactiva el comportamiento `renames` para esta invocación. |
| `--rename-empty` | Activa el modo `--rename-empty`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--follow` | Continúa el historial de una ruta a través de un renombre cuando puede detectarlo. |
| `-l` | Activa el modo `-l`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--minimal` | Activa el modo `--minimal`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-w` | Activa el modo `-w`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ignore-all-space` | Excluye elementos que cumplan la condición indicada. |
| `-b` | Activa el modo `-b`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ignore-space-change` | Excluye elementos que cumplan la condición indicada. |
| `--ignore-space-at-eol` | Excluye elementos que cumplan la condición indicada. |
| `--ignore-cr-at-eol` | Excluye elementos que cumplan la condición indicada. |
| `--ignore-blank-lines` | Excluye elementos que cumplan la condición indicada. |
| `-I` | Activa el modo `-I`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ignore-matching-lines` | Excluye elementos que cumplan la condición indicada. |
| `--indent-heuristic` | Activa el modo `--indent-heuristic`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--patience` | Activa el modo `--patience`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--histogram` | Activa el modo `--histogram`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--diff-algorithm` | Selecciona el algoritmo o estrategia que procesa la entrada. |
| `--anchored` | Activa el modo `--anchored`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--word-diff` | Activa el modo `--word-diff`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--word-diff-regex` | Activa el modo `--word-diff-regex`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--color-words` | Activa el modo `--color-words`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--color-moved` | Activa el modo `--color-moved`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--color-moved-ws` | Activa el modo `--color-moved-ws`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--relative` | Activa el modo `--relative`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-a` | Activa la forma corta de selección total o una opción propia de la orden. |
| `--text` | Activa el modo `--text`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-R` | Activa el modo `-R`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--exit-code` | Activa el modo `--exit-code`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--ext-diff` | Activa el modo `--ext-diff`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--textconv` | Activa el modo `--textconv`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ignore-submodules` | Excluye elementos que cumplan la condición indicada. |
| `--submodule` | Activa el modo `--submodule`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ita-invisible-in-index` | Activa el modo `--ita-invisible-in-index`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-N` | Activa el modo `-N`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ita-visible-in-index` | Activa el modo `--ita-visible-in-index`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-S` | Activa el modo `-S`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-G` | Activa el modo `-G`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--pickaxe-all` | Incluye elementos adicionales dentro del alcance indicado. |
| `--pickaxe-regex` | Activa el modo `--pickaxe-regex`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-O` | Activa el modo `-O`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--rotate-to` | Activa el modo `--rotate-to`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--skip-to` | Activa el modo `--skip-to`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--find-object` | Selecciona la representación o tratamiento de identificadores de objeto. |
| `--diff-filter` | Activa el modo `--diff-filter`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--output` | Escribe el resultado en la ruta indicada. |

## Selección de entradas

Distingue identificadores de objeto, referencias y rutas. Resuelve revisiones con `git rev-parse --verify`; inspecciona tipo y tamaño con `git cat-file`; usa actualización condicional al escribir referencias.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El objeto no existe | El identificador no resuelve o no está disponible en un clon parcial | Valida el hash y la política de descarga. |
| La salida se separa mal | Un nombre contiene espacios o saltos de línea | Usa terminación NUL cuando la función la admita. |
| El recorrido incluye más commits | El rango expresa alcanzabilidad y no una lista literal | Comprueba extremos positivos y negativos del rango. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git diff-tree`](../plumbing-read/diff-tree.md)
- [`git diff-index`](../plumbing-read/diff-index.md)
- [`git for-each-ref`](../plumbing-read/for-each-ref.md)

## Fuente

- [git-diff-pairs - Compare the content and mode of provided blob pairs](https://git-scm.com/docs/git-diff-pairs)
