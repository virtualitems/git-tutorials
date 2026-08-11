---
title: "git rev-list"
source: "https://git-scm.com/docs/git-rev-list"
section: "plumbing-commands"
canonical_file: "plumbing-read/rev-list.md"
status: "expanded"
---

# `git rev-list`

> Esta ruta conserva la clasificación `plumbing-commands`. La guía canónica está en [`plumbing-read/rev-list.md`](../plumbing-read/rev-list.md). Ambas documentan la misma URL del sitemap.

Este caso usa `git rev-list` para enumerar commits alcanzables según límites y filtros. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git rev-list consulta objetos, referencias, índices, packs y relaciones entre commits. Recibe como entrada objetos, referencias, árboles o entradas del índice que debe leer la consulta. La operación consiste en enumerar commits alcanzables según límites y filtros.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | objetos, referencias, árboles o entradas del índice que debe leer la consulta. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | enumerar commits alcanzables según límites y filtros. | Comprueba el resultado con una orden de lectura. |
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
git rev-list --count main
git rev-list main --not origin/main
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- La operación observable es: enumerar commits alcanzables según límites y filtros.
- La comprobación se realiza mediante: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git rev-list [<options>] <commit>… [--] [<path>…]
```

### Uso verificado con `git version 2.51.1`

```text
git rev-list [<options>] <commit>... [--] [<path>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git rev-list -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | enumerar commits alcanzables según límites y filtros | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git rev-list a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Salida para scripts | Producir registros con campos y separadores definidos. | Prueba nombres con espacios y saltos de línea. |
| Validación | Comprobar el resultado de git rev-list con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--max-count` | Limita el número de registros producidos. |
| `--max-age` | Aplica una fecha, duración o política de vencimiento. |
| `--min-age` | Aplica una fecha, duración o política de vencimiento. |
| `--sparse` | Permite operar sobre entradas que quedan fuera de la selección sparse activa. |
| `--no-merges` | Desactiva el comportamiento `merges` para esta invocación. |
| `--min-parents` | Establece un límite numérico para la selección o el recorrido. |
| `--no-min-parents` | Desactiva el comportamiento `min-parents` para esta invocación. |
| `--max-parents` | Establece un límite numérico para la selección o el recorrido. |
| `--no-max-parents` | Desactiva el comportamiento `max-parents` para esta invocación. |
| `--remove-empty` | Retira elementos según las condiciones de la orden. |
| `--all` | Amplía la selección a todos los elementos del alcance definido. |
| `--branches` | Incluye o selecciona ramas según la operación. |
| `--tags` | Incluye o selecciona etiquetas según la operación. |
| `--remotes` | Activa el modo `--remotes`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stdin` | Lee registros o nombres desde la entrada estándar. |
| `--exclude-hidden` | Excluye elementos que cumplan la condición indicada. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--topo-order` | Activa el modo `--topo-order`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--date-order` | Aplica una fecha, duración o política de vencimiento. |
| `--reverse` | Invierte el orden del recorrido o resultado. |
| `--parents` | Activa el modo `--parents`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--children` | Activa el modo `--children`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--objects` | Incluye identificadores de objeto en el resultado. |
| `--objects-edge` | Selecciona la representación o tratamiento de identificadores de objeto. |
| `--disk-usage` | Activa el modo `--disk-usage`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--unpacked` | Activa el modo `--unpacked`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--header` | Activa el modo `--header`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--pretty` | Controla campos, orden o representación del resultado. |
| `--object-names` | Selecciona la representación o tratamiento de identificadores de objeto. |
| `--abbrev` | Reduce la representación visible del identificador sin cambiar el objeto. |
| `--no-abbrev` | Desactiva el comportamiento `abbrev` para esta invocación. |
| `--abbrev-commit` | Activa el modo `--abbrev-commit`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--left-right` | Activa el modo `--left-right`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--count` | Establece un límite numérico para la selección o el recorrido. |
| `-z` | Termina registros con NUL para evitar división por espacios o saltos de línea. |
| `--bisect` | Activa el modo `--bisect`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--bisect-vars` | Activa el modo `--bisect-vars`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--bisect-all` | Incluye elementos adicionales dentro del alcance indicado. |

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

- [`git rev-parse`](../plumbing-read/rev-parse.md)
- [`git repo`](../plumbing-read/repo.md)
- [`git show-index`](../plumbing-read/show-index.md)

## Fuente

- [git-rev-list - Lists commit objects in reverse chronological order](https://git-scm.com/docs/git-rev-list)
