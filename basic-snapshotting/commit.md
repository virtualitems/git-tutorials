---
title: "git commit"
source: "https://git-scm.com/docs/git-commit"
section: "basic-snapshotting"
status: "source-audited"
version: "2.55.0"
---

# `git commit`

Este caso usa `git commit` para registrar en el historial el contenido preparado en el índice.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Ejemplo mínimo

```bash
git add guia.txt
git commit -m "Añade el primer capítulo"
```

La invocación `git commit -m "Añade el primer capítulo"` ejecuta esta operación: registrar en el historial el contenido preparado en el índice. Después, `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Sintaxis y formas de invocación

```text
git commit [-a | --interactive | --patch] [-s] [-v] [-u[<mode>]] [--amend]
	   [--dry-run] <commit>_ | --fixup [(amend|reword):"><commit>]
	   [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
	   [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

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

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-a` y `--all`

Amplía la selección a todos los elementos del alcance definido.

#### Ejemplo con `--all`

```bash
git commit --all -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--interactive`

Abre una selección interactiva antes de aplicar la operación.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit --interactive -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--patch` y `-p`

Permite elegir hunks en vez de operar sobre el archivo completo.

#### Ejemplo con `--patch`

```bash
git commit --patch -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-s` y `--signoff`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--signoff`

```bash
git commit --signoff -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git commit --verbose -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-u` y `--untracked-files`

Define cuánto detalle muestra Git sobre archivos que todavía no están en el índice. En Git 2.51.1, la ayuda corta expresa el contrato como `show untracked files, optional modes: all, normal, no. (Default: all)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--untracked-files`

```bash
git commit --untracked-files=all -m "Añade el primer capítulo"
git status --short
```

En esta forma, `all` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--amend`

Crea un commit que reemplaza el commit señalado por `HEAD` y conserva sus padres salvo que otra opción los cambie. En Git 2.51.1, la ayuda corta expresa el contrato como `amend previous commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit --amend -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

```bash
git commit --dry-run -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--fixup`

Crea un commit marcado para combinarse con otro mediante rebase autosquash. En Git 2.51.1, la ayuda corta expresa el contrato como `use autosquash formatted message to fixup or amend/reword specified commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit --fixup=valor -m "Añade el primer capítulo"
git status --short
```

### `-F` y `--file`

Usa el archivo indicado en vez de la ubicación por defecto.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `--file`

```bash
git commit --file=rutas.txt -m "Añade el primer capítulo"
git status --short
```

En esta forma, `rutas.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-m` y `--message`

Activa mensaje durante registrar en el historial el contenido preparado en el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `commit message`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--message`

```bash
git commit --message='mensaje de ejemplo'
git status --short
```

En esta forma, `mensaje de ejemplo` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--reset-author`

Declara al committer actual como autor del commit que se vuelve a crear. En Git 2.51.1, la ayuda corta expresa el contrato como `the commit is authored by me now (used with -C/-c/--amend)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit --reset-author -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--allow-empty`

Permite continuar cuando el cambio produce un commit sin diferencias.

```bash
git commit --allow-empty -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--allow-empty-message`

Permite crear un commit cuyo mensaje está vacío.

```bash
git commit --allow-empty-message -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verify`

Desactiva el comportamiento `verify` para esta invocación.

```bash
git commit --no-verify -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-e` y `--edit`

Abre la representación editable que define la orden antes de aplicarla.

#### Ejemplo con `--edit`

```bash
git commit --edit -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--author`

Limita el resultado a autores que coinciden con el patrón indicado. En Git 2.51.1, la ayuda corta expresa el contrato como `override author for commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit --author=Ana -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `Ana` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-c` y `--reedit-message`

Reutiliza un mensaje existente y abre el editor antes de confirmar. En Git 2.51.1, la ayuda corta expresa el contrato como `reuse and edit message from specified commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--reedit-message`

```bash
git commit --reedit-message=HEAD -m "Añade el primer capítulo"
git status --short
```

En esta forma, `HEAD` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-C` y `--reuse-message`

Reutiliza el mensaje y la autoría del commit indicado. En Git 2.51.1, la ayuda corta expresa el contrato como `reuse message from specified commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--reuse-message`

```bash
git commit --reuse-message=HEAD -m "Añade el primer capítulo"
git status --short
```

En esta forma, `HEAD` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--squash`

Crea un commit marcado para fusionar cambios y mensajes durante rebase autosquash. En Git 2.51.1, la ayuda corta expresa el contrato como `use autosquash formatted message to squash specified commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit --squash=HEAD -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--date`

Controla la representación o selección por fecha.

```bash
git commit --date=2026-01-15 -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `2026-01-15` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cleanup`

Selecciona cómo Git retira comentarios y espacios del mensaje antes de crear el commit.

```bash
git commit --cleanup=all -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--status`

Incluye estado en la entrada, el resultado o el registro que construye `git commit`. En Git 2.51.1, la ayuda corta expresa el contrato como `include status in commit message template`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit --status -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-i` y `--include`

Incluye elementos adicionales dentro del alcance indicado.

#### Ejemplo con `--include`

```bash
git commit --include -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-o` y `--only`

Limita registrar en el historial el contenido preparado en el índice al alcance identificado por only. En Git 2.51.1, la ayuda corta expresa el contrato como `commit only specified files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `--only`

```bash
git commit --only -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--pathspec-from-file`

Lee pathspecs desde un archivo o desde stdin.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit --pathspec-from-file=rutas.txt -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pathspec-file-nul`

Interpreta los pathspecs de archivo como registros terminados en NUL.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit --pathspec-file-nul -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--trailer`

Incluye trailer en la entrada, el resultado o el registro que construye `git commit`. En Git 2.51.1, la ayuda corta expresa el contrato como `add custom trailer(s)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit --trailer=valor -m "Añade el primer capítulo"
git status --short
```

### `-S` y `--gpg-sign`

Activa gpg sign durante registrar en el historial el contenido preparado en el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--gpg-sign`

```bash
git commit --gpg-sign=user.name -m "Añade el primer capítulo"
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git commit --quiet -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-t` y `--template`

Usa el directorio indicado como fuente de plantillas para crear archivos iniciales dentro del nuevo repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `use specified template file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git commit` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `--template`

```bash
git commit --template=../plantillas -m "Añade el primer capítulo"
git status --short
```

En esta forma, `../plantillas` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-U` y `--unified`

Define cuántas líneas de contexto rodean cada hunk.

#### Ejemplo con `--unified`

```bash
git commit --unified=5 -m "Añade el primer capítulo"
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--inter-hunk-context`

Fusiona hunks cercanos cuando la distancia no supera el límite indicado.

```bash
git commit --inter-hunk-context=5 -m "Añade el primer capítulo"
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-n`

Comprueba n antes de aceptar el resultado de `git commit`. En Git 2.51.1, la ayuda corta expresa el contrato como `bypass pre-commit and commit-msg hooks`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit -n -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

```bash
git commit --verify -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--short`

Incluye short en la salida o cambia cómo `git commit` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show status concisely`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit --short -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--branch`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git commit --branch -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ahead-behind`

Calcula cuántos commits separan una rama de su upstream. En Git 2.51.1, la ayuda corta expresa el contrato como `compute full ahead/behind values`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit --ahead-behind -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--porcelain`

Produce un contrato de salida destinado a scripts.

```bash
git commit --porcelain -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--long`

Incluye long en la salida o cambia cómo `git commit` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show status in long format (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit --long -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z` y `--null`

Usa NUL como terminador para conservar cualquier byte válido de un nombre.

#### Ejemplo con `--null`

```bash
git commit --null -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--no-post-rewrite`

Desactiva el comportamiento `post-rewrite` para esta invocación.

```bash
git commit --no-post-rewrite -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--post-rewrite`

Selecciona la relación indicada por post rewrite; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-post-rewrite`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git commit --post-rewrite -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-status`

Desactiva para esta invocación el comportamiento que habilita `--status`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git commit --no-status -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signoff`

Desactiva para esta invocación el comportamiento que habilita `--signoff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git commit --no-signoff -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-edit`

Conserva el mensaje existente sin abrir el editor.

```bash
git commit --no-edit -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gpg-sign`

Desactiva para esta invocación el comportamiento que habilita `--gpg-sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git commit --no-gpg-sign -m "Añade el primer capítulo"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git mv`](../basic-snapshotting/mv.md)
- [`git add`](../basic-snapshotting/add.md)
- [`git notes`](../basic-snapshotting/notes.md)

## Fuente

- [git-commit - Record changes to the repository](https://git-scm.com/docs/git-commit)
