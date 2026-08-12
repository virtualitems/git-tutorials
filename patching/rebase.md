---
title: "git rebase"
source: "https://git-scm.com/docs/git-rebase"
section: "patching"
status: "source-audited"
version: "2.55.0"
---

# `git rebase`

Este caso usa `git rebase` para reaplicar commits sobre una base distinta.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Ejemplo mínimo

```bash
git switch tema-portada
git rebase main
```

La invocación `git rebase main` ejecuta esta operación: reaplicar commits sobre una base distinta. Después, el diff y el historial muestran si cambiaron archivos, índice o commits.

## Sintaxis y formas de invocación

```text
git rebase [-i | --interactive] [<options>] [--exec <cmd>]
	[--onto <newbase> | --keep-base] [<upstream> [<branch>]]
git rebase [-i | --interactive] [<options>] [--exec <cmd>] [--onto <newbase>]
	--root [<branch>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git rebase [-i] [options] [--exec <cmd>] [--onto <newbase> | --keep-base] [<upstream> [<branch>]]
   or: git rebase [-i] [options] [--exec <cmd>] [--onto <newbase>] --root [<branch>]
   or: git rebase --continue | --abort | --skip | --edit-todo
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git rebase -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-i` y `--interactive`

Abre una selección interactiva antes de aplicar la operación.

#### Ejemplo con `--interactive`

```bash
git rebase --interactive main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--exec` y `-x`

Incluye exec en la entrada, el resultado o el registro que construye `git rebase`. En Git 2.51.1, la ayuda corta expresa el contrato como `add exec lines after each commit of the editable list`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--exec`

```bash
git rebase --exec=valor main
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--onto`

Activa onto durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `rebase onto given branch instead of upstream`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --onto=valor main
git status --short
```

### `--keep-base`

Define conservar base para esta ejecución de `git rebase`. En Git 2.51.1, la ayuda corta expresa el contrato como `use the merge-base of upstream and branch as the current base`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --keep-base main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--root`

Activa root durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `rebase all reachable commits up to the root(s)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --root main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--continue`

Reanuda una secuencia pausada después de resolver su estado.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque continuar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git rebase --continue
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--abort`

Cancela la secuencia y restaura el punto que la orden registró al comenzar.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque abortar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git rebase --abort
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--skip`

Omite el elemento actual y continúa la secuencia.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque omitir el elemento actual actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git rebase --skip
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--edit-todo`

Incluye edición todo en la salida o cambia cómo `git rebase` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `edit the todo list during an interactive rebase`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --edit-todo main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verify`

Desactiva el comportamiento `verify` para esta invocación.

```bash
git rebase --no-verify main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

```bash
git rebase --verify main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git rebase --quiet main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--no-stat`

Desactiva el comportamiento `stat` para esta invocación.

```bash
git rebase --no-stat main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git rebase --verbose main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-n`

Impide n durante esta invocación de `git rebase`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not show diffstat of what changed upstream`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase -n main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stat`

Resume cambios mediante conteos por ruta.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque estadísticas actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git rebase --stat main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signoff`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer to each commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --signoff main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--committer-date-is-author-date`

Aplica una fecha, duración o política de vencimiento.

```bash
git rebase --committer-date-is-author-date main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reset-author-date`

Aplica una fecha, duración o política de vencimiento.

```bash
git rebase --reset-author-date main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

```bash
git rebase -C 5 main
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-whitespace`

Excluye elementos que cumplan la condición indicada.

```bash
git rebase --ignore-whitespace main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--whitespace`

Selecciona la acción que Git ejecuta cuando detecta errores de espacios en un parche. En Git 2.51.1, la ayuda corta expresa el contrato como `passed to 'git apply'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --whitespace=warn main
git status --short
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f` y `--force-rebase`

Omite una protección concreta de la orden; requiere verificar origen y destino.

#### Ejemplo con `--force-rebase`

```bash
git rebase --force-rebase main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--ff`

Selecciona la relación indicada por ff; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-ff`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --ff main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quit`

Sale de la secuencia y conserva el estado que la documentación define.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque salir actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git rebase --quit
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--show-current-patch`

Incluye información adicional en la salida.

```bash
git rebase --show-current-patch main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--apply`

Define apply para esta ejecución de `git rebase`. En Git 2.51.1, la ayuda corta expresa el contrato como `use apply strategies to rebase`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --apply main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--merge`

Define merge para esta ejecución de `git rebase`. En Git 2.51.1, la ayuda corta expresa el contrato como `use merging strategies to rebase`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--merge`

```bash
git rebase --merge main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--rerere-autoupdate`

Actualiza rerere autoupdate como parte de reaplicar commits sobre una base distinta. En Git 2.51.1, la ayuda corta expresa el contrato como `update the index with reused conflict resolution if possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --rerere-autoupdate main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--empty`

Activa vacío durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `how to handle commits that become empty`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --empty=valor main
git status --short
```

### `--autosquash`

Activa autosquash durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `move commits that begin with squash!/fixup! under -i`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --autosquash main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--update-refs`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git rebase --update-refs main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-S` y `--gpg-sign`

Activa gpg sign durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG-sign commits`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--gpg-sign`

```bash
git rebase --gpg-sign=user.name main
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--autostash`

Activa autostash durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `automatically stash/stash pop before and after`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --autostash main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-r` y `--rebase-merges`

Activa rebase merges durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `try to rebase merges instead of skipping them`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque rebase merges actúa sobre el estado que Git registró al iniciar la secuencia.

#### Ejemplo con `--rebase-merges`

```bash
git rebase --rebase-merges=all main
git status --short
```

En esta forma, `all` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--fork-point`

Define fork point para esta ejecución de `git rebase`. En Git 2.51.1, la ayuda corta expresa el contrato como `use 'merge-base --fork-point' to refine upstream`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --fork-point main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-s` y `--strategy`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git rebase` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `--strategy`

```bash
git rebase --strategy=ort main
git status --short
```

En esta forma, `ort` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-X` y `--strategy-option`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git rebase` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `--strategy-option`

```bash
git rebase --strategy-option=valor main
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--reschedule-failed-exec`

Activa reschedule failed exec durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `automatically re-schedule any `exec` that fails`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --reschedule-failed-exec main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reapply-cherry-picks`

Activa reapply cherry picks durante reaplicar commits sobre una base distinta. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `apply all changes, even those already present upstream`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rebase --reapply-cherry-picks main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-rerere-autoupdate`

Desactiva para esta invocación el comportamiento que habilita `--rerere-autoupdate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git rebase --no-rerere-autoupdate main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-autosquash`

Desactiva para esta invocación el comportamiento que habilita `--autosquash`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git rebase --no-autosquash main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gpg-sign`

Desactiva para esta invocación el comportamiento que habilita `--gpg-sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git rebase --no-gpg-sign main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-autostash`

Desactiva para esta invocación el comportamiento que habilita `--autostash`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git rebase --no-autostash main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-rebase-merges`

Desactiva para esta invocación el comportamiento que habilita `--rebase-merges`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

Esta forma se usa cuando `git rebase` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque desactivar rebase merges actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git rebase --no-rebase-merges main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-fork-point`

Desactiva para esta invocación el comportamiento que habilita `--fork-point`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git rebase --no-fork-point main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reschedule-failed-exec`

Desactiva para esta invocación el comportamiento que habilita `--reschedule-failed-exec`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git rebase --no-reschedule-failed-exec main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reapply-cherry-picks`

Desactiva para esta invocación el comportamiento que habilita `--reapply-cherry-picks`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git rebase --no-reapply-cherry-picks main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git replay`](../patching/replay.md)
- [`git cherry-pick`](../patching/cherry-pick.md)
- [`git revert`](../patching/revert.md)

## Fuente

- [git-rebase - Reapply commits on top of another base tip](https://git-scm.com/docs/git-rebase)
