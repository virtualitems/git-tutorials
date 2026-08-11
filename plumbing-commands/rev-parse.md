---
title: "git rev-parse"
source: "https://git-scm.com/docs/git-rev-parse"
section: "plumbing-commands"
canonical_file: "plumbing-read/rev-parse.md"
status: "expanded"
---

# `git rev-parse`

> Esta ruta conserva la clasificación `plumbing-commands`. La guía canónica está en [`plumbing-read/rev-parse.md`](../plumbing-read/rev-parse.md). Ambas documentan la misma URL del sitemap.

Este caso usa `git rev-parse` para resolver revisiones y separar opciones para scripts. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git rev-parse consulta objetos, referencias, índices, packs y relaciones entre commits. Recibe como entrada objetos, referencias, árboles o entradas del índice que debe leer la consulta. La operación consiste en resolver revisiones y separar opciones para scripts.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | objetos, referencias, árboles o entradas del índice que debe leer la consulta. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | resolver revisiones y separar opciones para scripts. | Comprueba el resultado con una orden de lectura. |
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
git rev-parse --show-toplevel
git rev-parse HEAD^{tree}
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- La operación observable es: resolver revisiones y separar opciones para scripts.
- La comprobación se realiza mediante: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git rev-parse [<options>] <arg>…
```

### Uso verificado con `git version 2.51.1`

```text
git rev-parse --parseopt [<options>] -- [<args>...]
   or: git rev-parse --sq-quote [<arg>...]
   or: git rev-parse [<options>] [<arg>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git rev-parse -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | resolver revisiones y separar opciones para scripts | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git rev-parse a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git rev-parse con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--parseopt` | Activa el modo `--parseopt`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--sq-quote` | Activa el modo `--sq-quote`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-h` | Muestra ayuda corta cuando la orden admite esta convención. |

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

- [`git show-index`](../plumbing-read/show-index.md)
- [`git rev-list`](../plumbing-read/rev-list.md)
- [`git show-ref`](../plumbing-read/show-ref.md)

## Fuente

- [git-rev-parse - Pick out and massage parameters](https://git-scm.com/docs/git-rev-parse)
