---
title: "git diff-files"
source: "https://git-scm.com/docs/git-diff-files"
section: "plumbing-read"
status: "expanded"
---

# `git diff-files`

Este caso usa `git diff-files` para comparar el área de trabajo con el índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git diff-files consulta objetos, referencias, índices, packs y relaciones entre commits. Recibe como entrada objetos, referencias, árboles o entradas del índice que debe leer la consulta. La operación consiste en comparar el área de trabajo con el índice.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | objetos, referencias, árboles o entradas del índice que debe leer la consulta. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | comparar el área de trabajo con el índice. | Comprueba el resultado con una orden de lectura. |
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
git diff-files -- README.md
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- La operación observable es: comparar el área de trabajo con el índice.
- La comprobación se realiza mediante: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git diff-files [-q] [-0 | -1 | -2 | -3 | -c | --cc] [<common-diff-options>] [<path>…]
```

### Uso verificado con `git version 2.51.1`

```text
git diff-files [-q] [-0 | -1 | -2 | -3 | -c | --cc] [<common-diff-options>] [<path>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git diff-files -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | comparar el área de trabajo con el índice | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git diff-files a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Salida para scripts | Producir registros con campos y separadores definidos. | Prueba nombres con espacios y saltos de línea. |
| Validación | Comprobar el resultado de git diff-files con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `-0` | Activa el modo `-0`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-1` | Activa el modo `-1`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-2` | Activa el modo `-2`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-3` | Activa el modo `-3`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-c` | Aplica una clave de configuración solo a esta invocación. |
| `--cc` | Activa el modo `--cc`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-z` | Termina registros con NUL para evitar división por espacios o saltos de línea. |
| `-p` | Activa la forma corta del modo patch o de una opción propia de la orden. |
| `-u` | Activa el modo `-u`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--patch-with-raw` | Activa el modo `--patch-with-raw`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stat` | Resume cambios mediante conteos por ruta. |
| `--numstat` | Activa el modo `--numstat`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--patch-with-stat` | Activa el modo `--patch-with-stat`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--name-only` | Muestra nombres de ruta sin el contenido del diff. |
| `--name-status` | Muestra nombres y estado de cada ruta. |
| `--full-index` | Activa el modo `--full-index`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--abbrev` | Reduce la representación visible del identificador sin cambiar el objeto. |
| `-R` | Activa el modo `-R`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-B` | Activa el modo `-B`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-M` | Activa el modo `-M`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-C` | Ejecuta Git como si se hubiera iniciado en el directorio indicado. |
| `--find-copies-harder` | Controla detección o búsqueda de relaciones entre entradas. |
| `-l` | Activa el modo `-l`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-O` | Activa el modo `-O`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-S` | Activa el modo `-S`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--pickaxe-all` | Incluye elementos adicionales dentro del alcance indicado. |
| `-a` | Activa la forma corta de selección total o una opción propia de la orden. |
| `--text` | Activa el modo `--text`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

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

- [`git diff-index`](../plumbing-read/diff-index.md)
- [`git cherry`](../plumbing-read/cherry.md)
- [`git diff-pairs`](../plumbing-read/diff-pairs.md)

## Fuente

- [git-diff-files - Compares files in the working tree and the index](https://git-scm.com/docs/git-diff-files)
