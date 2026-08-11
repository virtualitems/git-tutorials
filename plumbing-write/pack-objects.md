---
title: "git pack-objects"
source: "https://git-scm.com/docs/git-pack-objects"
section: "plumbing-write"
status: "expanded"
---

# `git pack-objects`

Este caso usa `git pack-objects` para crear un archivo pack a partir de objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git pack-objects crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en crear un archivo pack a partir de objetos.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | identificadores, entradas del índice o referencias validadas por el script. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | crear un archivo pack a partir de objetos. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: crear un archivo pack a partir de objetos. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
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
mkdir -p packs
git rev-list --objects --all | git pack-objects packs/pack
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: identificadores, entradas del índice o referencias validadas por el script.
- La operación observable es: crear un archivo pack a partir de objetos.
- La comprobación se realiza mediante: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git pack-objects [-q | --progress | --all-progress] [--all-progress-implied]
		   [--no-reuse-delta] [--delta-base-offset] [--non-empty]
		   [--local] [--incremental] [--window=<n>] [--depth=<n>]
		   [--revs [--unpacked | --all]] [--keep-pack=<pack-name>]
```

### Uso verificado con `git version 2.51.1`

```text
git pack-objects [-q | --progress | --all-progress] [--all-progress-implied]
                        [--no-reuse-delta] [--delta-base-offset] [--non-empty]
                        [--local] [--incremental] [--window=<n>] [--depth=<n>]
                        [--revs [--unpacked | --all]] [--keep-pack=<pack-name>]
                        [--cruft] [--cruft-expiration=<time>]
                        [--stdout [--filter=<filter-spec>] | <base-name>]
                        [--shallow] [--keep-true-parents] [--[no-]sparse]
                        [--name-hash-version=<n>] [--path-walk] < <object-list>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git pack-objects -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | crear un archivo pack a partir de objetos | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git pack-objects a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git pack-objects con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `--progress` | Muestra progreso aunque la salida no sea un terminal. |
| `--all-progress` | Incluye elementos adicionales dentro del alcance indicado. |
| `--all-progress-implied` | Incluye elementos adicionales dentro del alcance indicado. |
| `--no-reuse-delta` | Desactiva el comportamiento `reuse-delta` para esta invocación. |
| `--delta-base-offset` | Activa el modo `--delta-base-offset`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--non-empty` | Activa el modo `--non-empty`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--local` | Opera sobre la configuración del repositorio. |
| `--incremental` | Activa el modo `--incremental`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--window` | Activa el modo `--window`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--depth` | Establece un límite numérico para la selección o el recorrido. |
| `--revs` | Activa el modo `--revs`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--unpacked` | Activa el modo `--unpacked`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--all` | Amplía la selección a todos los elementos del alcance definido. |
| `--keep-pack` | Activa el modo `--keep-pack`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--cruft` | Activa el modo `--cruft`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--cruft-expiration` | Activa el modo `--cruft-expiration`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stdout` | Activa el modo `--stdout`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--filter` | Activa el modo `--filter`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--shallow` | Activa el modo `--shallow`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--keep-true-parents` | Activa el modo `--keep-true-parents`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--sparse` | Permite operar sobre entradas que quedan fuera de la selección sparse activa. |
| `--name-hash-version` | Selecciona la representación o tratamiento de identificadores de objeto. |
| `--path-walk` | Activa el modo `--path-walk`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--index-version` | Activa el modo `--index-version`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--max-pack-size` | Establece un límite numérico para la selección o el recorrido. |
| `--window-memory` | Activa el modo `--window-memory`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reuse-delta` | Activa el modo `--reuse-delta`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reuse-object` | Selecciona la representación o tratamiento de identificadores de objeto. |
| `--threads` | Activa el modo `--threads`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reflog` | Activa el modo `--reflog`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--indexed-objects` | Selecciona la representación o tratamiento de identificadores de objeto. |
| `--stdin-packs` | Activa el modo `--stdin-packs`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--include-tag` | Selecciona o modifica referencias dentro del alcance de la orden. |
| `--keep-unreachable` | Activa el modo `--keep-unreachable`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--pack-loose-unreachable` | Activa el modo `--pack-loose-unreachable`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--unpack-unreachable` | Activa el modo `--unpack-unreachable`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--thin` | Activa el modo `--thin`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--honor-pack-keep` | Activa el modo `--honor-pack-keep`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--compression` | Activa el modo `--compression`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--use-bitmap-index` | Activa el modo `--use-bitmap-index`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--write-bitmap-index` | Permite crear o escribir el elemento seleccionado. |
| `--missing` | Activa el modo `--missing`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--exclude-promisor-objects` | Selecciona la representación o tratamiento de identificadores de objeto. |
| `--exclude-promisor-objects-best-effort` | Selecciona la representación o tratamiento de identificadores de objeto. |
| `--delta-islands` | Activa el modo `--delta-islands`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--uri-protocol` | Activa el modo `--uri-protocol`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

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

Persistencia: Puede persistir el estado implicado por esta operación: crear un archivo pack a partir de objetos. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git prune-packed`](../plumbing-write/prune-packed.md)
- [`git multi-pack-index`](../plumbing-write/multi-pack-index.md)
- [`git read-tree`](../plumbing-write/read-tree.md)

## Fuente

- [git-pack-objects - Create a packed archive of objects](https://git-scm.com/docs/git-pack-objects)
