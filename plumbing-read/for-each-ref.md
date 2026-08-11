---
title: "git for-each-ref"
source: "https://git-scm.com/docs/git-for-each-ref"
section: "plumbing-read"
status: "expanded"
---

# `git for-each-ref`

Este caso usa `git for-each-ref` para filtrar, ordenar y formatear referencias. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git for-each-ref consulta objetos, referencias, índices, packs y relaciones entre commits. Recibe como entrada objetos, referencias, árboles o entradas del índice que debe leer la consulta. La operación consiste en filtrar, ordenar y formatear referencias.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | objetos, referencias, árboles o entradas del índice que debe leer la consulta. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | filtrar, ordenar y formatear referencias. | Comprueba el resultado con una orden de lectura. |
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
git for-each-ref --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- La operación observable es: filtrar, ordenar y formatear referencias.
- La comprobación se realiza mediante: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git for-each-ref [--count=<count>] [--shell|--perl|--python|--tcl]
		   [(--sort=<key>)…] [--format=<format>]
		   [--include-root-refs] [--points-at=<object>]
		   [--merged[=<object>]] [--no-merged[=<object>]]
```

### Uso verificado con `git version 2.51.1`

```text
git for-each-ref [<options>] [<pattern>]
   or: git for-each-ref [--points-at <object>]
   or: git for-each-ref [--merged [<commit>]] [--no-merged [<commit>]]
   or: git for-each-ref [--contains [<commit>]] [--no-contains [<commit>]]
   or: git for-each-ref [--start-after <marker>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git for-each-ref -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | filtrar, ordenar y formatear referencias | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git for-each-ref a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Salida para scripts | Producir registros con campos y separadores definidos. | Prueba nombres con espacios y saltos de línea. |
| Validación | Comprobar el resultado de git for-each-ref con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--count` | Establece un límite numérico para la selección o el recorrido. |
| `--shell` | Activa el modo `--shell`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--perl` | Activa el modo `--perl`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--python` | Activa el modo `--python`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--tcl` | Activa el modo `--tcl`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--sort` | Ordena registros por el campo indicado. |
| `--format` | Define los campos y separadores de la salida. |
| `--include-root-refs` | Selecciona o modifica referencias dentro del alcance de la orden. |
| `--points-at` | Activa el modo `--points-at`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--merged` | Filtra elementos ya alcanzables desde la revisión indicada. |
| `--no-merged` | Filtra elementos no alcanzables desde la revisión indicada. |
| `--contains` | Filtra referencias cuyo historial contiene el commit indicado. |
| `--no-contains` | Filtra referencias cuyo historial no contiene el commit indicado. |
| `--start-after` | Activa el modo `--start-after`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-s` | Activa el modo `-s`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-p` | Activa la forma corta del modo patch o de una opción propia de la orden. |
| `--omit-empty` | Activa el modo `--omit-empty`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--color` | Controla el uso de secuencias de color en la salida. |
| `--exclude` | Excluye elementos que cumplan la condición indicada. |
| `--ignore-case` | Excluye elementos que cumplan la condición indicada. |
| `--stdin` | Lee registros o nombres desde la entrada estándar. |

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

- [`git for-each-repo`](../plumbing-read/for-each-repo.md)
- [`git diff-tree`](../plumbing-read/diff-tree.md)
- [`git format-rev`](../plumbing-read/format-rev.md)

## Fuente

- [git-for-each-ref - Output information on each ref](https://git-scm.com/docs/git-for-each-ref)
