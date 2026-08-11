---
title: "git notes"
source: "https://git-scm.com/docs/git-notes"
section: "basic-snapshotting"
status: "expanded"
---

# `git notes`

Este caso usa `git notes` para asociar anotaciones a objetos sin cambiar los objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git notes mueve contenido entre el área de trabajo, el índice y el commit señalado por `HEAD`. Recibe como entrada las rutas y el estado de origen seleccionados por los argumentos. La operación consiste en asociar anotaciones a objetos sin cambiar los objetos.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | las rutas y el estado de origen seleccionados por los argumentos. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | asociar anotaciones a objetos sin cambiar los objetos. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: asociar anotaciones a objetos sin cambiar los objetos. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
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
git notes add -m "Revisado en clase" HEAD
git notes show HEAD
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: las rutas y el estado de origen seleccionados por los argumentos.
- La operación observable es: asociar anotaciones a objetos sin cambiar los objetos.
- La comprobación se realiza mediante: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git notes [list [<object>]]
git notes add [-f] [--allow-empty] [--[no-]separator | --separator=<paragraph-break>] [--[no-]stripspace] [-F <file> | -m <msg> | (-c | -C) <object>] [-e] [<object>]
git notes copy [-f] ( --stdin | <from-object> [<to-object>] )
git notes append [--allow-empty] [--[no-]separator | --separator=<paragraph-break>] [--[no-]stripspace] [-F <file> | -m <msg> | (-c | -C) <object>] [-e] [<object>]
```

### Uso verificado con `git version 2.51.1`

```text
git notes [--ref <notes-ref>] [list [<object>]]
   or: git notes [--ref <notes-ref>] add [-f] [--allow-empty] [--[no-]separator|--separator=<paragraph-break>] [--[no-]stripspace] [-m <msg> | -F <file> | (-c | -C) <object>] [<object>] [-e]
   or: git notes [--ref <notes-ref>] copy [-f] <from-object> <to-object>
   or: git notes [--ref <notes-ref>] append [--allow-empty] [--[no-]separator|--separator=<paragraph-break>] [--[no-]stripspace] [-m <msg> | -F <file> | (-c | -C) <object>] [<object>] [-e]
   or: git notes [--ref <notes-ref>] edit [--allow-empty] [<object>]
   or: git notes [--ref <notes-ref>] show [<object>]
   or: git notes [--ref <notes-ref>] merge [-v | -q] [-s <strategy>] <notes-ref>
   or: git notes merge --commit [-v | -q]
   or: git notes merge --abort [-v | -q]
   or: git notes [--ref <notes-ref>] remove [<object>...]
   or: git notes [--ref <notes-ref>] prune [-n] [-v]
   or: git notes [--ref <notes-ref>] get-ref
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git notes -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | asociar anotaciones a objetos sin cambiar los objetos | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git notes a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Sesión interrumpida | Continuar o cancelar una secuencia después de revisar el estado. | Consulta `git status` antes de elegir la acción. |
| Validación | Comprobar el resultado de git notes con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-f` | Activa la forma corta de la operación forzada. |
| `--allow-empty` | Activa el modo `--allow-empty`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--separator` | Activa el modo `--separator`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stripspace` | Activa el modo `--stripspace`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-F` | Activa el modo `-F`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-m` | Activa el modo `-m`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-c` | Aplica una clave de configuración solo a esta invocación. |
| `-C` | Ejecuta Git como si se hubiera iniciado en el directorio indicado. |
| `-e` | Activa el modo `-e`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stdin` | Lee registros o nombres desde la entrada estándar. |
| `--ref` | Selecciona o modifica referencias dentro del alcance de la orden. |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `-s` | Activa el modo `-s`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--commit` | Activa el modo `--commit`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--abort` | Cancela la secuencia y restaura el punto que la orden registró al comenzar. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |

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

Persistencia: Puede persistir el estado implicado por esta operación: asociar anotaciones a objetos sin cambiar los objetos. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git reset`](../basic-snapshotting/reset.md)
- [`git mv`](../basic-snapshotting/mv.md)
- [`git restore`](../basic-snapshotting/restore.md)

## Fuente

- [git-notes - Add or inspect object notes](https://git-scm.com/docs/git-notes)
