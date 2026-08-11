---
title: "git commit-graph"
source: "https://git-scm.com/docs/git-commit-graph"
section: "plumbing-write"
status: "expanded"
---

# `git commit-graph`

Este caso usa `git commit-graph` para escribir y verificar el archivo que acelera recorridos de commits. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git commit-graph crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en escribir y verificar el archivo que acelera recorridos de commits.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | identificadores, entradas del índice o referencias validadas por el script. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | escribir y verificar el archivo que acelera recorridos de commits. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: escribir y verificar el archivo que acelera recorridos de commits. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
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
git commit-graph write --reachable
git commit-graph verify
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: identificadores, entradas del índice o referencias validadas por el script.
- La operación observable es: escribir y verificar el archivo que acelera recorridos de commits.
- La comprobación se realiza mediante: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git commit-graph verify [--object-dir <dir>] [--shallow] [--[no-]progress]
git commit-graph write [--object-dir <dir>] [--append]
			[--split[=<strategy>]] [--reachable | --stdin-packs | --stdin-commits]
			[--changed-paths] [--[no-]max-new-filters <n>] [--[no-]progress]
```

### Uso verificado con `git version 2.51.1`

```text
git commit-graph verify [--object-dir <dir>] [--shallow] [--[no-]progress]
   or: git commit-graph write [--object-dir <dir>] [--append]
                              [--split[=<strategy>]] [--reachable | --stdin-packs | --stdin-commits]
                              [--changed-paths] [--[no-]max-new-filters <n>] [--[no-]progress]
                              <split-options>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git commit-graph -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | escribir y verificar el archivo que acelera recorridos de commits | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git commit-graph a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git commit-graph con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--object-dir` | Selecciona la representación o tratamiento de identificadores de objeto. |
| `--shallow` | Activa el modo `--shallow`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--progress` | Muestra progreso aunque la salida no sea un terminal. |
| `--append` | Activa el modo `--append`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--split` | Activa el modo `--split`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reachable` | Activa el modo `--reachable`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stdin-packs` | Activa el modo `--stdin-packs`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stdin-commits` | Activa el modo `--stdin-commits`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--changed-paths` | Activa el modo `--changed-paths`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--max-new-filters` | Establece un límite numérico para la selección o el recorrido. |

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

Persistencia: Puede persistir el estado implicado por esta operación: escribir y verificar el archivo que acelera recorridos de commits. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git commit-tree`](../plumbing-write/commit-tree.md)
- [`git checkout-index`](../plumbing-write/checkout-index.md)
- [`git hash-object`](../plumbing-write/hash-object.md)

## Fuente

- [git-commit-graph - Write and verify Git commit-graph files](https://git-scm.com/docs/git-commit-graph)
