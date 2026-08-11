---
title: "git restore"
source: "https://git-scm.com/docs/git-restore"
section: "basic-snapshotting"
status: "expanded"
---

# `git restore`

Este caso usa `git restore` para recuperar contenido de rutas en el índice o el área de trabajo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git restore mueve contenido entre el área de trabajo, el índice y el commit señalado por `HEAD`. Recibe como entrada las rutas y el estado de origen seleccionados por los argumentos. La operación consiste en recuperar contenido de rutas en el índice o el área de trabajo.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | las rutas y el estado de origen seleccionados por los argumentos. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | recuperar contenido de rutas en el índice o el área de trabajo. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: recuperar contenido de rutas en el índice o el área de trabajo. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git status --short`, `git diff` y `git diff --cached`. |

## Requisitos y laboratorio

Crea un repositorio con un commit base. Observa `HEAD`, el índice y el archivo antes y después de cada orden.

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

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

Para comprobar el resultado: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git restore --source=HEAD -- guia.txt
git restore --staged guia.txt
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: las rutas y el estado de origen seleccionados por los argumentos.
- La operación observable es: recuperar contenido de rutas en el índice o el área de trabajo.
- La comprobación se realiza mediante: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git restore [<options>] [--source=<tree>] [--staged] [--worktree] [--] <pathspec>…
git restore [<options>] [--source=<tree>] [--staged] [--worktree] --pathspec-from-file=<file> [--pathspec-file-nul]
git restore (-p|--patch) [<options>] [--source=<tree>] [--staged] [--worktree] [--] [<pathspec>…]
```

### Uso verificado con `git version 2.51.1`

```text
git restore [<options>] [--source=<branch>] <file>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git restore -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | recuperar contenido de rutas en el índice o el área de trabajo | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git restore a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git restore con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--source` | Activa el modo `--source`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--staged` | Selecciona el contenido preparado en el índice. |
| `--worktree` | Selecciona o modifica el área de trabajo. |
| `--pathspec-from-file` | Lee pathspecs desde un archivo o desde stdin. |
| `--pathspec-file-nul` | Interpreta los pathspecs de archivo como registros terminados en NUL. |
| `-p` | Activa la forma corta del modo patch o de una opción propia de la orden. |
| `--patch` | Permite elegir hunks en vez de operar sobre el archivo completo. |
| `-s` | Activa el modo `-s`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-S` | Activa el modo `-S`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-W` | Activa el modo `-W`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ignore-unmerged` | Excluye elementos que cumplan la condición indicada. |
| `--overlay` | Activa el modo `--overlay`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--recurse-submodules` | Propaga la operación a submódulos dentro del alcance. |
| `--progress` | Muestra progreso aunque la salida no sea un terminal. |
| `-m` | Activa el modo `-m`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--merge` | Activa el modo `--merge`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--conflict` | Activa el modo `--conflict`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-2` | Activa el modo `-2`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ours` | Activa el modo `--ours`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-3` | Activa el modo `-3`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--theirs` | Activa el modo `--theirs`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-U` | Activa el modo `-U`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--unified` | Define cuántas líneas de contexto rodean cada hunk. |
| `--inter-hunk-context` | Fusiona hunks cercanos cuando la distancia no supera el límite indicado. |
| `--ignore-skip-worktree-bits` | Excluye elementos que cumplan la condición indicada. |

## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El cambio no entra al commit | El índice no contiene la versión esperada | Compara `git diff` con `git diff --cached`. |
| Un pathspec no coincide | La ruta se evalúa desde otro directorio o está ignorada | Usa `git status --short --untracked-files=all` y separa opciones con `--`. |
| Se reemplaza contenido local | La orden escribe el área de trabajo | Guarda el diff o crea un stash antes de repetir la operación. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: recuperar contenido de rutas en el índice o el área de trabajo. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git rm`](../basic-snapshotting/rm.md)
- [`git reset`](../basic-snapshotting/reset.md)
- [`git status`](../basic-snapshotting/status.md)

## Fuente

- [git-restore - Restore working tree files](https://git-scm.com/docs/git-restore)
