---
title: "git commit"
source: "https://git-scm.com/docs/git-commit"
section: "basic-snapshotting"
status: "expanded"
---

# `git commit`

Este caso usa `git commit` para registrar en el historial el contenido preparado en el índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git commit mueve contenido entre el área de trabajo, el índice y el commit señalado por `HEAD`. Recibe como entrada las rutas y el estado de origen seleccionados por los argumentos. La operación consiste en registrar en el historial el contenido preparado en el índice.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | las rutas y el estado de origen seleccionados por los argumentos. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | registrar en el historial el contenido preparado en el índice. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: registrar en el historial el contenido preparado en el índice. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
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
git add guia.txt
git commit -m "Añade el primer capítulo"
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: las rutas y el estado de origen seleccionados por los argumentos.
- La operación observable es: registrar en el historial el contenido preparado en el índice.
- La comprobación se realiza mediante: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git commit [-a | --interactive | --patch] [-s] [-v] [-u[<mode>]] [--amend]
	   [--dry-run] <commit>_ | --fixup [(amend|reword):"><commit>]
	   [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
	   [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
```

### Uso verificado con `git version 2.51.1`

```text
git commit [-a | --interactive | --patch] [-s] [-v] [-u[<mode>]] [--amend]
                  [--dry-run] [(-c | -C | --squash) <commit> | --fixup [(amend|reword):]<commit>]
                  [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
                  [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
                  [--date=<date>] [--cleanup=<mode>] [--[no-]status]
                  [-i | -o] [--pathspec-from-file=<file> [--pathspec-file-nul]]
                  [(--trailer <token>[(=|:)<value>])...] [-S[<keyid>]]
                  [--] [<pathspec>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git commit -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | registrar en el historial el contenido preparado en el índice | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git commit a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Simulación | Calcular el efecto sin escribir el estado principal. | Compara la simulación con la selección prevista. |
| Salida para scripts | Producir registros con campos y separadores definidos. | Prueba nombres con espacios y saltos de línea. |
| Validación | Comprobar el resultado de git commit con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-a` | Activa la forma corta de selección total o una opción propia de la orden. |
| `--interactive` | Abre una selección interactiva antes de aplicar la operación. |
| `--patch` | Permite elegir hunks en vez de operar sobre el archivo completo. |
| `-s` | Activa el modo `-s`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `-u` | Activa el modo `-u`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--amend` | Activa el modo `--amend`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--dry-run` | Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio. |
| `--fixup` | Activa el modo `--fixup`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-F` | Activa el modo `-F`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-m` | Activa el modo `-m`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reset-author` | Activa el modo `--reset-author`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--allow-empty` | Activa el modo `--allow-empty`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--allow-empty-message` | Activa el modo `--allow-empty-message`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-verify` | Desactiva el comportamiento `verify` para esta invocación. |
| `-e` | Activa el modo `-e`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--author` | Activa el modo `--author`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-c` | Aplica una clave de configuración solo a esta invocación. |
| `-C` | Ejecuta Git como si se hubiera iniciado en el directorio indicado. |
| `--squash` | Activa el modo `--squash`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--date` | Controla la representación o selección por fecha. |
| `--cleanup` | Activa el modo `--cleanup`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--status` | Activa el modo `--status`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-i` | Activa la forma corta del modo interactivo o una opción propia de la orden. |
| `-o` | Activa la forma corta de salida o una opción propia de la orden. |
| `--pathspec-from-file` | Lee pathspecs desde un archivo o desde stdin. |
| `--pathspec-file-nul` | Interpreta los pathspecs de archivo como registros terminados en NUL. |
| `--trailer` | Activa el modo `--trailer`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-S` | Activa el modo `-S`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--verbose` | Aumenta el detalle enviado a la salida. |
| `--file` | Usa el archivo indicado en vez de la ubicación por defecto. |
| `--message` | Activa el modo `--message`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reedit-message` | Activa el modo `--reedit-message`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reuse-message` | Activa el modo `--reuse-message`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--signoff` | Activa el modo `--signoff`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-t` | Activa el modo `-t`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--template` | Controla campos, orden o representación del resultado. |
| `--edit` | Abre la representación editable que define la orden antes de aplicarla. |
| `--gpg-sign` | Activa el modo `--gpg-sign`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--all` | Amplía la selección a todos los elementos del alcance definido. |
| `--include` | Incluye elementos adicionales dentro del alcance indicado. |
| `-p` | Activa la forma corta del modo patch o de una opción propia de la orden. |
| `-U` | Activa el modo `-U`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--unified` | Define cuántas líneas de contexto rodean cada hunk. |
| `--inter-hunk-context` | Fusiona hunks cercanos cuando la distancia no supera el límite indicado. |
| `--only` | Activa el modo `--only`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `--verify` | Exige que el nombre o estructura cumpla el contrato antes de continuar. |
| `--short` | Activa el modo `--short`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--branch` | Selecciona o modifica referencias dentro del alcance de la orden. |
| `--ahead-behind` | Activa el modo `--ahead-behind`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--porcelain` | Produce un contrato de salida destinado a scripts. |
| `--long` | Activa el modo `--long`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-z` | Termina registros con NUL para evitar división por espacios o saltos de línea. |
| `--null` | Usa NUL como terminador para conservar cualquier byte válido de un nombre. |
| `--no-post-rewrite` | Desactiva el comportamiento `post-rewrite` para esta invocación. |
| `--post-rewrite` | Activa el modo `--post-rewrite`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--untracked-files` | Activa el modo `--untracked-files`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

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

Persistencia: Puede persistir el estado implicado por esta operación: registrar en el historial el contenido preparado en el índice. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git mv`](../basic-snapshotting/mv.md)
- [`git add`](../basic-snapshotting/add.md)
- [`git notes`](../basic-snapshotting/notes.md)

## Fuente

- [git-commit - Record changes to the repository](https://git-scm.com/docs/git-commit)
