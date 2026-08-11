---
title: "git update-ref"
source: "https://git-scm.com/docs/git-update-ref"
section: "plumbing-write"
status: "expanded"
---

# `git update-ref`

Este caso usa `git update-ref` para actualizar referencias con comprobaciones de valor anterior. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git update-ref crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en actualizar referencias con comprobaciones de valor anterior.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | identificadores, entradas del índice o referencias validadas por el script. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | actualizar referencias con comprobaciones de valor anterior. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: actualizar referencias con comprobaciones de valor anterior. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
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
git update-ref refs/heads/prueba HEAD
git show-ref --verify refs/heads/prueba
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: identificadores, entradas del índice o referencias validadas por el script.
- La operación observable es: actualizar referencias con comprobaciones de valor anterior.
- La comprobación se realiza mediante: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git update-ref [-m <reason>] [--no-deref] -d <ref> [<old-oid>]
git update-ref [-m <reason>] [--no-deref] [--create-reflog] <ref> <new-oid> [<old-oid>]
git update-ref [-m <reason>] [--no-deref] --stdin [-z] [--batch-updates]
```

### Uso verificado con `git version 2.51.1`

```text
git update-ref [<options>] -d <refname> [<old-oid>]
   or: git update-ref [<options>]    <refname> <new-oid> [<old-oid>]
   or: git update-ref [<options>] --stdin [-z] [--batch-updates]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git update-ref -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | actualizar referencias con comprobaciones de valor anterior | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git update-ref a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Salida para scripts | Producir registros con campos y separadores definidos. | Prueba nombres con espacios y saltos de línea. |
| Validación | Comprobar el resultado de git update-ref con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-m` | Activa el modo `-m`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-deref` | Desactiva el comportamiento `deref` para esta invocación. |
| `-d` | Activa la forma corta de eliminación o una opción propia de la orden. |
| `--create-reflog` | Permite crear o escribir el elemento seleccionado. |
| `--stdin` | Lee registros o nombres desde la entrada estándar. |
| `-z` | Termina registros con NUL para evitar división por espacios o saltos de línea. |
| `--batch-updates` | Activa el modo `--batch-updates`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--deref` | Activa el modo `--deref`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-0` | Activa el modo `-0`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

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

Persistencia: Puede persistir el estado implicado por esta operación: actualizar referencias con comprobaciones de valor anterior. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git write-tree`](../plumbing-write/write-tree.md)
- [`git update-index`](../plumbing-write/update-index.md)
- [`git unpack-objects`](../plumbing-write/unpack-objects.md)

## Fuente

- [git-update-ref - Update the object name stored in a ref safely](https://git-scm.com/docs/git-update-ref)
