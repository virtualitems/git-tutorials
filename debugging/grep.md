---
title: "git grep"
source: "https://git-scm.com/docs/git-grep"
section: "debugging"
status: "expanded"
---

# `git grep`

Este caso usa `git grep` para buscar texto en archivos del área de trabajo o de un árbol. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git grep localiza texto, autores, líneas o el commit que introdujo un comportamiento. Recibe como entrada un patrón, una ruta y el rango de historial que limita la búsqueda. La operación consiste en buscar texto en archivos del área de trabajo o de un árbol.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | un patrón, una ruta y el rango de historial que limita la búsqueda. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | buscar texto en archivos del área de trabajo o de un árbol. | Comprueba el resultado con una orden de lectura. |
| Persistencia | No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa la salida, el código de terminación y una revisión manual del commit hallado. |

## Requisitos y laboratorio

Crea tres commits que cambien la misma línea. Usa un patrón que exista y otro que no exista para observar los códigos de salida.

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

La búsqueda combina revisiones, rutas y contenido. Primero delimita el conjunto de commits o archivos; después interpreta la evidencia que devuelve Git.

Reduce primero el rango y las rutas. Después interpreta cada coincidencia dentro de ese conjunto, sin atribuir significado a elementos que quedaron fuera.

Para comprobar el resultado: la salida identifica líneas, archivos o commits que cumplen el criterio. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git grep -n "TODO" -- '*.js'
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: un patrón, una ruta y el rango de historial que limita la búsqueda.
- La operación observable es: buscar texto en archivos del área de trabajo o de un árbol.
- La comprobación se realiza mediante: la salida identifica líneas, archivos o commits que cumplen el criterio.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git grep [-a | --text] [-I] [--textconv] [-i | --ignore-case] [-w | --word-regexp]
	   [-v | --invert-match] [-h|-H] [--full-name]
	   [-E | --extended-regexp] [-G | --basic-regexp]
	   [-P | --perl-regexp]
```

### Uso verificado con `git version 2.51.1`

```text
git grep [<options>] [-e] <pattern> [<rev>...] [[--] <path>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git grep -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | buscar texto en archivos del área de trabajo o de un árbol | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git grep a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Salida para scripts | Producir registros con campos y separadores definidos. | Prueba nombres con espacios y saltos de línea. |
| Validación | Comprobar el resultado de git grep con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-a` | Activa la forma corta de selección total o una opción propia de la orden. |
| `--text` | Activa el modo `--text`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-I` | Activa el modo `-I`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--textconv` | Activa el modo `--textconv`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-i` | Activa la forma corta del modo interactivo o una opción propia de la orden. |
| `--ignore-case` | Excluye elementos que cumplan la condición indicada. |
| `-w` | Activa el modo `-w`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--word-regexp` | Activa el modo `--word-regexp`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `--invert-match` | Activa el modo `--invert-match`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-h` | Muestra ayuda corta cuando la orden admite esta convención. |
| `-H` | Activa el modo `-H`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--full-name` | Activa el modo `--full-name`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-E` | Activa el modo `-E`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--extended-regexp` | Activa el modo `--extended-regexp`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-G` | Activa el modo `-G`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--basic-regexp` | Activa el modo `--basic-regexp`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-P` | Activa el modo `-P`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--perl-regexp` | Activa el modo `--perl-regexp`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-e` | Activa el modo `-e`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--cached` | Usa el índice como origen o destino, sin tratar el área de trabajo de la misma forma. |
| `--no-index` | Desactiva el comportamiento `index` para esta invocación. |
| `--index` | Incluye el índice en la operación. |
| `--untracked` | Activa el modo `--untracked`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--exclude-standard` | Excluye elementos que cumplan la condición indicada. |
| `--recurse-submodules` | Propaga la operación a submódulos dentro del alcance. |
| `-r` | Activa el modo `-r`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--recursive` | Extiende la operación de forma recursiva al ámbito documentado. |
| `--max-depth` | Establece un límite numérico para la selección o el recorrido. |
| `-F` | Activa el modo `-F`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--fixed-strings` | Activa el modo `--fixed-strings`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `--line-number` | Activa el modo `--line-number`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--column` | Activa el modo `--column`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-l` | Activa el modo `-l`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--files-with-matches` | Activa el modo `--files-with-matches`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--name-only` | Muestra nombres de ruta sin el contenido del diff. |
| `-L` | Activa el modo `-L`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--files-without-match` | Activa el modo `--files-without-match`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-z` | Termina registros con NUL para evitar división por espacios o saltos de línea. |
| `--null` | Usa NUL como terminador para conservar cualquier byte válido de un nombre. |
| `-o` | Activa la forma corta de salida o una opción propia de la orden. |
| `--only-matching` | Activa el modo `--only-matching`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-c` | Aplica una clave de configuración solo a esta invocación. |
| `--count` | Establece un límite numérico para la selección o el recorrido. |
| `--color` | Controla el uso de secuencias de color en la salida. |
| `--break` | Activa el modo `--break`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--heading` | Activa el modo `--heading`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-C` | Ejecuta Git como si se hubiera iniciado en el directorio indicado. |
| `--context` | Activa el modo `--context`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-B` | Activa el modo `-B`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--before-context` | Activa el modo `--before-context`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-A` | Activa el modo `-A`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--after-context` | Activa el modo `--after-context`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--threads` | Activa el modo `--threads`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-p` | Activa la forma corta del modo patch o de una opción propia de la orden. |
| `--show-function` | Incluye información adicional en la salida. |
| `-W` | Activa el modo `-W`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--function-context` | Activa el modo `--function-context`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-f` | Activa la forma corta de la operación forzada. |
| `--and` | Activa el modo `--and`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--or` | Activa el modo `--or`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--not` | Activa el modo `--not`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--all-match` | Incluye elementos adicionales dentro del alcance indicado. |
| `-O` | Activa el modo `-O`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--open-files-in-pager` | Activa el modo `--open-files-in-pager`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ext-grep` | Activa el modo `--ext-grep`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-m` | Activa el modo `-m`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--max-count` | Limita el número de registros producidos. |

## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

`git grep` devuelve 0 si encuentra coincidencias, 1 si no encuentra y un valor mayor ante error.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| No hay coincidencias | El patrón, la revisión o la ruta no abarca el dato | Prueba el patrón sobre `HEAD` y separa la ruta con `--`. |
| La atribución parece incorrecta | El archivo se movió o el bloque se reformateó | Activa detección de movimiento o copia y compara el commit. |
| La búsqueda binaria no avanza | La prueba no clasifica el commit | Marca el commit como `skip` o corrige el comando de prueba. |

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

Prepara un historial corto con un cambio por commit. Delimita una ruta o un rango para comprobar qué evidencia incluye y cuál excluye el comando.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git blame`](../debugging/blame.md)
- [`git bisect`](../debugging/bisect.md)

## Fuente

- [git-grep - Print lines matching a pattern](https://git-scm.com/docs/git-grep)
