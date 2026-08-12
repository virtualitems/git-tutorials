---
title: "git branch"
source: "https://git-scm.com/docs/git-branch"
section: "branching-and-merging"
status: "source-audited"
version: "2.55.0"
---

# `git branch`

Este caso usa `git branch` para listar, crear, renombrar y eliminar ramas.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git branch tema-portada
git branch --list
git branch -d tema-portada
```

La invocación `git branch tema-portada` ejecuta esta operación: listar, crear, renombrar y eliminar ramas. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Sintaxis y formas de invocación

```text
git branch [--color[=<when>] | --no-color] [--show-current]
	   [-v [--abbrev=<n> | --no-abbrev]]
	   [--column[=<options>] | --no-column] [--sort=<key>]
	   [--merged [<commit>]] [--no-merged [<commit>]]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git branch [<options>] [-r | -a] [--merged] [--no-merged]
   or: git branch [<options>] [-f] [--recurse-submodules] <branch-name> [<start-point>]
   or: git branch [<options>] [-l] [<pattern>...]
   or: git branch [<options>] [-r] (-d | -D) <branch-name>...
   or: git branch [<options>] (-m | -M) [<old-branch>] <new-branch>
   or: git branch [<options>] (-c | -C) [<old-branch>] <new-branch>
   or: git branch [<options>] [-r | -a] [--points-at]
   or: git branch [<options>] [-r | -a] [--format]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git branch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--color`

Controla el uso de secuencias de color en la salida.

```bash
git branch --color=always tema-portada
git status --short
```

El ejemplo usa `always` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-color`

Desactiva secuencias de color.

```bash
git branch --no-color tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--show-current`

Incluye información adicional en la salida.

```bash
git branch --show-current tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git branch --verbose tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--abbrev`

Reduce la representación visible del identificador sin cambiar el objeto.

```bash
git branch --abbrev=5 tema-portada
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-abbrev`

Desactiva el comportamiento `abbrev` para esta invocación.

```bash
git branch --no-abbrev tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--column`

Incluye column en la salida o cambia cómo `git branch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `list branches in columns`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git branch --column=short tema-portada
git status --short
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-column`

Desactiva el comportamiento `column` para esta invocación.

```bash
git branch --no-column tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sort`

Ordena registros por el campo indicado.

```bash
git branch --sort=user.name tema-portada
git status --short
```

El ejemplo usa `user.name` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--merged`

Filtra elementos ya alcanzables desde la revisión indicada.

```bash
git branch --merged=HEAD tema-portada
git status --short
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-merged`

Filtra elementos no alcanzables desde la revisión indicada.

```bash
git branch --no-merged tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-r` y `--remotes`

Activa remotes durante listar, crear, renombrar y eliminar ramas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `act on remote-tracking branches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--remotes`

```bash
git branch --remotes tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-a` y `--all`

Amplía la selección a todos los elementos del alcance definido.

#### Ejemplo con `--all`

```bash
git branch --all tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git branch --force tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

```bash
git branch --recurse-submodules tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-l` y `--list`

Incluye información adicional en la salida.

#### Ejemplo con `--list`

```bash
git branch --list tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-d` y `--delete`

Elimina el elemento seleccionado.

#### Ejemplo con `--delete`

```bash
git branch --delete tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-D`

Retira D del alcance que procesa `git branch`. En Git 2.51.1, la ayuda corta expresa el contrato como `delete branch (even if not merged)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git branch -D tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--move`

Activa move durante listar, crear, renombrar y eliminar ramas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `move/rename a branch and its reflog`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--move`

```bash
git branch --move tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-M`

Activa M durante listar, crear, renombrar y eliminar ramas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `move/rename a branch, even if target exists`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git branch -M tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-c` y `--copy`

Activa copy durante listar, crear, renombrar y eliminar ramas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `copy a branch and its reflog`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--copy`

```bash
git branch --copy tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

```bash
git branch -C tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--points-at`

Limita listar, crear, renombrar y eliminar ramas al alcance identificado por points at. En Git 2.51.1, la ayuda corta expresa el contrato como `print only branches of the object`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git branch --points-at=HEAD tema-portada
git status --short
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--format`

Define los campos y separadores de la salida.

```bash
git branch --format=oneline tema-portada
git status --short
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git branch --quiet tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-t` y `--track`

Crea o ajusta la asociación de seguimiento solicitada.

#### Ejemplo con `--track`

```bash
git branch --track=valor tema-portada
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-u` y `--set-upstream-to`

Asocia la rama con una rama upstream.

#### Ejemplo con `--set-upstream-to`

```bash
git branch --set-upstream-to=valor tema-portada
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--unset-upstream`

Retira la asociación upstream.

```bash
git branch --unset-upstream tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--contains`

Filtra referencias cuyo historial contiene el commit indicado.

```bash
git branch --contains=HEAD tema-portada
git status --short
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-contains`

Filtra referencias cuyo historial no contiene el commit indicado.

```bash
git branch --no-contains tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--omit-empty`

Impide omit vacío durante esta invocación de `git branch`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not output a newline after empty formatted refs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git branch --omit-empty tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--create-reflog`

Permite crear o escribir el elemento seleccionado.

```bash
git branch --create-reflog tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--edit-description`

Activa edición description durante listar, crear, renombrar y eliminar ramas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `edit the description for the branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git branch --edit-description tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-i` y `--ignore-case`

Excluye elementos que cumplan la condición indicada.

#### Ejemplo con `--ignore-case`

```bash
git branch --ignore-case tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--no-track`

Desactiva para esta invocación el comportamiento que habilita `--track`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git branch --no-track tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-create-reflog`

Desactiva para esta invocación el comportamiento que habilita `--create-reflog`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git branch --no-create-reflog tema-portada
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--set-upstream` (retirada)

Git 2.55.0 conserva el nombre en el manual para indicar que ya no admite esta opción porque su sintaxis era ambigua. Usa `--track` al crear la rama o `--set-upstream-to=<upstream>` para una rama existente.

```bash
git branch --track tema origin/main
git branch --set-upstream-to=origin/main tema
git branch --verbose --verbose
```

La última orden muestra el upstream asociado a `tema`. No uses `--set-upstream` en scripts.

## Páginas relacionadas

- [`git checkout`](../branching-and-merging/checkout.md)
- [`git history`](../branching-and-merging/history.md)

## Fuente

- [git-branch - List, create, or delete branches](https://git-scm.com/docs/git-branch)
