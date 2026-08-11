---
title: "git checkout-index"
source: "https://git-scm.com/docs/git-checkout-index"
section: "plumbing-commands"
canonical_file: "plumbing-write/checkout-index.md"
status: "expanded"
---

# `git checkout-index`

> Esta ruta conserva la clasificación `plumbing-commands`. La guía canónica está en [`plumbing-write/checkout-index.md`](../plumbing-write/checkout-index.md). Ambas documentan la misma URL del sitemap.

Este caso usa `git checkout-index` para copiar archivos del índice al área de trabajo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git checkout-index crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en copiar archivos del índice al área de trabajo.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | identificadores, entradas del índice o referencias validadas por el script. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | copiar archivos del índice al área de trabajo. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: copiar archivos del índice al área de trabajo. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git fsck`, `git cat-file`, `git ls-tree`, `git show-ref` y el hash devuelto. |

## Requisitos y laboratorio

Usa un repositorio sin datos de valor. Guarda los hashes producidos y crea referencias solo con actualización condicional.

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

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

Para comprobar el resultado: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
mkdir exportado
git checkout-index --all --prefix=exportado/
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: identificadores, entradas del índice o referencias validadas por el script.
- La operación observable es: copiar archivos del índice al área de trabajo.
- La comprobación se realiza mediante: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git checkout-index [-u] [-q] [-a] [-f] [-n] [--prefix=<string>]
		   [--stage=<number>|all]
		   [--temp]
		   [--ignore-skip-worktree-bits]
```

### Uso verificado con `git version 2.51.1`

```text
git checkout-index [<options>] [--] [<file>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git checkout-index -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | copiar archivos del índice al área de trabajo | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git checkout-index a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Salida para scripts | Producir registros con campos y separadores definidos. | Prueba nombres con espacios y saltos de línea. |
| Validación | Comprobar el resultado de git checkout-index con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-u` | Activa el modo `-u`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `-a` | Activa la forma corta de selección total o una opción propia de la orden. |
| `-f` | Activa la forma corta de la operación forzada. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `--prefix` | Activa el modo `--prefix`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stage` | Activa el modo `--stage`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--temp` | Activa el modo `--temp`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ignore-skip-worktree-bits` | Excluye elementos que cumplan la condición indicada. |
| `--all` | Amplía la selección a todos los elementos del alcance definido. |
| `--force` | Omite una protección concreta; úsala solo después de verificar el estado objetivo. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--no-create` | Desactiva el comportamiento `create` para esta invocación. |
| `--create` | Permite crear o escribir el elemento seleccionado. |
| `--index` | Incluye el índice en la operación. |
| `-z` | Termina registros con NUL para evitar división por espacios o saltos de línea. |
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
| El hash no coincide | Los bytes, el tipo o la longitud difieren | Compara la entrada byte por byte y no normalices el contenido. |
| La referencia no se actualiza | El valor anterior no coincide con la condición | Lee el valor actual y repite con una condición nueva. |
| El índice queda sin resolver | Una entrada tiene etapas de conflicto | Inspecciona `git ls-files --stage` antes de escribir un árbol. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: copiar archivos del índice al área de trabajo. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git commit-graph`](../plumbing-write/commit-graph.md)
- [`git commit-tree`](../plumbing-write/commit-tree.md)

## Fuente

- [git-checkout-index - Copy files from the index to the working tree](https://git-scm.com/docs/git-checkout-index)
