---
title: "git annotate"
source: "https://git-scm.com/docs/git-annotate"
section: "debugging"
status: "expanded"
---

# `git annotate`

Este caso usa `git annotate` para atribuir cada línea de un archivo a un commit. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git annotate localiza texto, autores, líneas o el commit que introdujo un comportamiento. Recibe como entrada un patrón, una ruta y el rango de historial que limita la búsqueda. La operación consiste en atribuir cada línea de un archivo a un commit.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | un patrón, una ruta y el rango de historial que limita la búsqueda. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | atribuir cada línea de un archivo a un commit. | Comprueba el resultado con una orden de lectura. |
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
git annotate README.md
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: un patrón, una ruta y el rango de historial que limita la búsqueda.
- La operación observable es: atribuir cada línea de un archivo a un commit.
- La comprobación se realiza mediante: la salida identifica líneas, archivos o commits que cumplen el criterio.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git annotate [<options>] [<rev-opts>] [<rev>] [--] <file>
```

### Uso verificado con `git version 2.51.1`

```text
git annotate [<options>] [<rev-opts>] [<rev>] [--] <file>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git annotate -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | atribuir cada línea de un archivo a un commit | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git annotate a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Salida para scripts | Producir registros con campos y separadores definidos. | Prueba nombres con espacios y saltos de línea. |
| Validación | Comprobar el resultado de git annotate con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--incremental` | Activa el modo `--incremental`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-b` | Activa el modo `-b`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--root` | Activa el modo `--root`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--show-stats` | Incluye información adicional en la salida. |
| `--progress` | Muestra progreso aunque la salida no sea un terminal. |
| `--score-debug` | Activa el modo `--score-debug`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-f` | Activa la forma corta de la operación forzada. |
| `--show-name` | Incluye información adicional en la salida. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `--show-number` | Incluye información adicional en la salida. |
| `-p` | Activa la forma corta del modo patch o de una opción propia de la orden. |
| `--porcelain` | Produce un contrato de salida destinado a scripts. |
| `--line-porcelain` | Activa el modo `--line-porcelain`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-c` | Aplica una clave de configuración solo a esta invocación. |
| `-t` | Activa el modo `-t`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-l` | Activa el modo `-l`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-s` | Activa el modo `-s`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-e` | Activa el modo `-e`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--show-email` | Incluye información adicional en la salida. |
| `-w` | Activa el modo `-w`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ignore-rev` | Excluye elementos que cumplan la condición indicada. |
| `--ignore-revs-file` | Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis. |
| `--color-lines` | Activa el modo `--color-lines`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--color-by-age` | Aplica una fecha, duración o política de vencimiento. |
| `--minimal` | Activa el modo `--minimal`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-S` | Activa el modo `-S`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--contents` | Activa el modo `--contents`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-C` | Ejecuta Git como si se hubiera iniciado en el directorio indicado. |
| `-M` | Activa el modo `-M`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-L` | Activa el modo `-L`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--abbrev` | Reduce la representación visible del identificador sin cambiar el objeto. |

## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

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

- [`git bisect`](../debugging/bisect.md)
- [`git blame`](../debugging/blame.md)

## Fuente

- [git-annotate - Annotate file lines with commit information](https://git-scm.com/docs/git-annotate)
