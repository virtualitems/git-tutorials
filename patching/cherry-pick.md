---
title: "git cherry-pick"
source: "https://git-scm.com/docs/git-cherry-pick"
section: "patching"
status: "source-audited"
version: "2.55.0"
---

# `git cherry-pick`

Este caso usa `git cherry-pick` para aplicar en la rama actual el cambio de commits existentes.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Ejemplo mínimo

```bash
git switch release
git cherry-pick a1b2c3d
```

La invocación `git cherry-pick a1b2c3d` ejecuta esta operación: aplicar en la rama actual el cambio de commits existentes. Después, el diff y el historial muestran si cambiaron archivos, índice o commits.

## Sintaxis y formas de invocación

```text
git cherry-pick [--edit] [-n] [-m <parent-number>] [-s] [-x] [--ff]
		  [-S[<keyid>]] <commit>…
git cherry-pick (--continue | --skip | --abort | --quit)
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git cherry-pick [--edit] [-n] [-m <parent-number>] [-s] [-x] [--ff]
                       [-S[<keyid>]] <commit>...
   or: git cherry-pick (--continue | --skip | --abort | --quit)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git cherry-pick -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--edit` y `-e`

Abre la representación editable que define la orden antes de aplicarla.

#### Ejemplo con `--edit`

```bash
git cherry-pick --edit a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-n`

Impide n durante esta invocación de `git cherry-pick`. En Git 2.51.1, la ayuda corta expresa el contrato como `don't automatically commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cherry-pick -n a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--mainline`

Define mainline para esta ejecución de `git cherry-pick`. En Git 2.51.1, la ayuda corta expresa el contrato como `select mainline parent`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--mainline`

```bash
git cherry-pick --mainline=5 a1b2c3d
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-s` y `--signoff`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--signoff`

```bash
git cherry-pick --signoff a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-x`

Activa x durante aplicar en la rama actual el cambio de commits existentes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `append commit name`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cherry-pick -x a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ff`

Permite ff cuando la forma predeterminada de `git cherry-pick` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow fast-forward`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cherry-pick --ff a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-S` y `--gpg-sign`

Activa gpg sign durante aplicar en la rama actual el cambio de commits existentes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--gpg-sign`

```bash
git cherry-pick --gpg-sign=user.name a1b2c3d
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--continue`

Reanuda una secuencia pausada después de resolver su estado.

Esta forma se usa cuando `git cherry-pick` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque continuar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git cherry-pick --continue
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--skip`

Omite el elemento actual y continúa la secuencia.

Esta forma se usa cuando `git cherry-pick` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque omitir el elemento actual actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git cherry-pick --skip
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--abort`

Cancela la secuencia y restaura el punto que la orden registró al comenzar.

Esta forma se usa cuando `git cherry-pick` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque abortar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git cherry-pick --abort
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quit`

Sale de la secuencia y conserva el estado que la documentación define.

Esta forma se usa cuando `git cherry-pick` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque salir actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git cherry-pick --quit
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cleanup`

Selecciona cómo Git retira comentarios y espacios del mensaje antes de crear el commit.

```bash
git cherry-pick --cleanup=all a1b2c3d
git status --short
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--commit`

Selecciona la relación indicada por commit; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cherry-pick --commit a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--rerere-autoupdate`

Actualiza rerere autoupdate como parte de aplicar en la rama actual el cambio de commits existentes. En Git 2.51.1, la ayuda corta expresa el contrato como `update the index with reused conflict resolution if possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cherry-pick --rerere-autoupdate a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--strategy`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git cherry-pick` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git cherry-pick --strategy=ort a1b2c3d
git status --short
```

El ejemplo usa `ort` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-X` y `--strategy-option`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git cherry-pick` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `--strategy-option`

```bash
git cherry-pick --strategy-option=valor a1b2c3d
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--allow-empty`

Permite continuar cuando el cambio produce un commit sin diferencias. En Git 2.51.1, la ayuda corta expresa el contrato como `preserve initially empty commits`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cherry-pick --allow-empty a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--allow-empty-message`

Permite crear un commit cuyo mensaje está vacío. En Git 2.51.1, la ayuda corta expresa el contrato como `allow commits with empty messages`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cherry-pick --allow-empty-message a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-redundant-commits`

Define conservar redundant commits para esta ejecución de `git cherry-pick`. En Git 2.51.1, la ayuda corta expresa el contrato como `deprecated: use --empty=keep instead`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cherry-pick --keep-redundant-commits a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--empty`

Activa vacío durante aplicar en la rama actual el cambio de commits existentes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `how to handle commits that become empty`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cherry-pick --empty=valor a1b2c3d
git status --short
```

### `--no-rerere-autoupdate`

Desactiva para esta invocación el comportamiento que habilita `--rerere-autoupdate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git cherry-pick --no-rerere-autoupdate a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gpg-sign`

Desactiva para esta invocación el comportamiento que habilita `--gpg-sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git cherry-pick --no-gpg-sign a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git rebase`](../patching/rebase.md)
- [`git apply`](../patching/apply.md)
- [`git replay`](../patching/replay.md)

## Fuente

- [git-cherry-pick - Apply the changes introduced by some existing commits](https://git-scm.com/docs/git-cherry-pick)
