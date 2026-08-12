---
title: "git merge"
source: "https://git-scm.com/docs/git-merge"
section: "branching-and-merging"
status: "source-audited"
version: "2.55.0"
---

# `git merge`

Este caso usa `git merge` para integrar una o más líneas de desarrollo en la rama actual.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git switch main
git merge tema-portada
```

La invocación `git merge tema-portada` ejecuta esta operación: integrar una o más líneas de desarrollo en la rama actual. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Sintaxis y formas de invocación

```text
git merge [-n] [--stat] [--compact-summary] [--no-commit] [--squash] [--[no-]edit]
	[--no-verify] [-s <strategy>] [-X <strategy-option>] [-S[<keyid>]]
	[--[no-]allow-unrelated-histories]
	[--[no-]rerere-autoupdate] [-m <msg>] [-F <file>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git merge [<options>] [<commit>...]
   or: git merge --abort
   or: git merge --continue
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git merge -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-n`

Impide n durante esta invocación de `git merge`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not show a diffstat at the end of the merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge -n tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stat`

Resume cambios mediante conteos por ruta.

Esta forma se usa cuando `git merge` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque estadísticas actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git merge --stat tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--compact-summary`

Incluye compact summary en la salida o cambia cómo `git merge` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show a compact-summary at the end of the merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge --compact-summary tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-commit`

Desactiva el comportamiento `commit` para esta invocación.

```bash
git merge --no-commit tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--squash`

Crea un commit marcado para fusionar cambios y mensajes durante rebase autosquash. En Git 2.51.1, la ayuda corta expresa el contrato como `create a single commit instead of doing a merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge --squash tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--edit` y `-e`

Abre la representación editable que define la orden antes de aplicarla.

#### Ejemplo con `--edit`

```bash
git merge --edit tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--no-verify`

Desactiva el comportamiento `verify` para esta invocación.

```bash
git merge --no-verify tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-s` y `--strategy`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git merge` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `--strategy`

```bash
git merge --strategy=ort tema-portada
git status --short
```

En esta forma, `ort` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-X` y `--strategy-option`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git merge` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `--strategy-option`

```bash
git merge --strategy-option=Ana tema-portada
git status --short
```

En esta forma, `Ana` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-S` y `--gpg-sign`

Activa gpg sign durante integrar una o más líneas de desarrollo en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--gpg-sign`

```bash
git merge --gpg-sign=user.name tema-portada
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--allow-unrelated-histories`

Permite permitir unrelated histories cuando la forma predeterminada de `git merge` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow merging unrelated histories`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge --allow-unrelated-histories tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--rerere-autoupdate`

Actualiza rerere autoupdate como parte de integrar una o más líneas de desarrollo en la rama actual. En Git 2.51.1, la ayuda corta expresa el contrato como `update the index with reused conflict resolution if possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge --rerere-autoupdate tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--message`

Activa mensaje durante integrar una o más líneas de desarrollo en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `merge commit message (for a non-fast-forward merge)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--message`

```bash
git merge --message='mensaje de ejemplo' tema-portada
git status --short
```

En esta forma, `mensaje de ejemplo` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-F` y `--file`

Usa el archivo indicado en vez de la ubicación por defecto.

La opción cambia cómo `git merge` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `--file`

```bash
git merge --file=archivo.txt tema-portada
git status --short
```

En esta forma, `archivo.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--abort`

Cancela la secuencia y restaura el punto que la orden registró al comenzar.

Esta forma se usa cuando `git merge` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque abortar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git merge --abort
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--continue`

Reanuda una secuencia pausada después de resolver su estado.

Esta forma se usa cuando `git merge` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque continuar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git merge --continue
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--summary`

Activa summary durante integrar una o más líneas de desarrollo en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `(synonym to --stat)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge --summary tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--log`

Incluye log en la entrada, el resultado o el registro que construye `git merge`. En Git 2.51.1, la ayuda corta expresa el contrato como `add (at most <n>) entries from shortlog to merge commit message`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge --log=5 tema-portada
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--commit`

Ejecuta commit durante integrar una o más líneas de desarrollo en la rama actual. En Git 2.51.1, la ayuda corta expresa el contrato como `perform a commit if the merge succeeds (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge --commit tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cleanup`

Selecciona cómo Git retira comentarios y espacios del mensaje antes de crear el commit.

```bash
git merge --cleanup=all tema-portada
git status --short
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ff`

Permite ff cuando la forma predeterminada de `git merge` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow fast-forward (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge --ff tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ff-only`

Limita integrar una o más líneas de desarrollo en la rama actual al alcance identificado por ff only. En Git 2.51.1, la ayuda corta expresa el contrato como `abort if fast-forward is not possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git merge` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque ff only actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git merge --ff-only tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify-signatures`

Valida el dato o estado antes de producir el resultado.

```bash
git merge --verify-signatures tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--into-name`

Define into nombre para esta ejecución de `git merge`. En Git 2.51.1, la ayuda corta expresa el contrato como `use <name> instead of the real target`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge --into-name=tema tema-portada
git status --short
```

El ejemplo usa `tema` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git merge --verbose tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git merge --quiet tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--quit`

Sale de la secuencia y conserva el estado que la documentación define.

Esta forma se usa cuando `git merge` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque salir actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git merge --quit
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git merge --progress tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--autostash`

Activa autostash durante integrar una o más líneas de desarrollo en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `automatically stash/stash pop before and after`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge --autostash tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--overwrite-ignore`

Excluye elementos que cumplan la condición indicada.

```bash
git merge --overwrite-ignore tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signoff`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge --signoff tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

```bash
git merge --verify tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stat`

Desactiva para esta invocación el comportamiento que habilita `--stat`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git merge --no-stat tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-squash`

Desactiva para esta invocación el comportamiento que habilita `--squash`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git merge --no-squash tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-edit`

Conserva el mensaje existente sin abrir el editor.

```bash
git merge --no-edit tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-rerere-autoupdate`

Desactiva para esta invocación el comportamiento que habilita `--rerere-autoupdate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git merge --no-rerere-autoupdate tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-summary`

Desactiva para esta invocación el comportamiento que habilita `--summary`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git merge --no-summary tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-log`

Desactiva para esta invocación el comportamiento que habilita `--log`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git merge --no-log tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ff`

Desactiva para esta invocación el comportamiento que habilita `--ff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git merge --no-ff tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verify-signatures`

Desactiva para esta invocación el comportamiento que habilita `--verify-signatures`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git merge --no-verify-signatures tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git merge --no-progress tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gpg-sign`

Desactiva para esta invocación el comportamiento que habilita `--gpg-sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git merge --no-gpg-sign tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-autostash`

Desactiva para esta invocación el comportamiento que habilita `--autostash`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git merge --no-autostash tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-overwrite-ignore`

Desactiva para esta invocación el comportamiento que habilita `--overwrite-ignore`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git merge --no-overwrite-ignore tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signoff`

Desactiva para esta invocación el comportamiento que habilita `--signoff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git merge --no-signoff tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git mergetool`](../branching-and-merging/mergetool.md)
- [`git history`](../branching-and-merging/history.md)
- [`git merge-tree`](../branching-and-merging/merge-tree.md)

## Fuente

- [git-merge - Join two or more development histories together](https://git-scm.com/docs/git-merge)
