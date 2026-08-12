---
title: "git revert"
source: "https://git-scm.com/docs/git-revert"
section: "patching"
status: "source-audited"
version: "2.55.0"
---

# `git revert`

Este caso usa `git revert` para crear un commit que invierte el efecto de otro commit.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Ejemplo mínimo

```bash
git revert a1b2c3d
```

La invocación `git revert a1b2c3d` ejecuta esta operación: crear un commit que invierte el efecto de otro commit. Después, el diff y el historial muestran si cambiaron archivos, índice o commits.

## Sintaxis y formas de invocación

```text
git revert [--[no-]edit] [-n] [-m <parent-number>] [-s] [-S[<keyid>]] <commit>…
git revert (--continue | --skip | --abort | --quit)
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git revert [--[no-]edit] [-n] [-m <parent-number>] [-s] [-S[<keyid>]] <commit>...
   or: git revert (--continue | --skip | --abort | --quit)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git revert -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--edit` y `-e`

Abre la representación editable que define la orden antes de aplicarla.

#### Ejemplo con `--edit`

```bash
git revert --edit a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-n`

Impide n durante esta invocación de `git revert`. En Git 2.51.1, la ayuda corta expresa el contrato como `don't automatically commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git revert -n a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--mainline`

Define mainline para esta ejecución de `git revert`. En Git 2.51.1, la ayuda corta expresa el contrato como `select mainline parent`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--mainline`

```bash
git revert --mainline=5 a1b2c3d
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-s` y `--signoff`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--signoff`

```bash
git revert --signoff a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-S` y `--gpg-sign`

Activa gpg sign durante crear un commit que invierte el efecto de otro commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--gpg-sign`

```bash
git revert --gpg-sign=user.name a1b2c3d
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--continue`

Reanuda una secuencia pausada después de resolver su estado.

Esta forma se usa cuando `git revert` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque continuar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git revert --continue
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--skip`

Omite el elemento actual y continúa la secuencia.

Esta forma se usa cuando `git revert` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque omitir el elemento actual actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git revert --skip
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--abort`

Cancela la secuencia y restaura el punto que la orden registró al comenzar.

Esta forma se usa cuando `git revert` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque abortar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git revert --abort
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quit`

Sale de la secuencia y conserva el estado que la documentación define.

Esta forma se usa cuando `git revert` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque salir actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git revert --quit
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cleanup`

Selecciona cómo Git retira comentarios y espacios del mensaje antes de crear el commit.

```bash
git revert --cleanup=all a1b2c3d
git status --short
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--commit`

Selecciona la relación indicada por commit; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git revert --commit a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--rerere-autoupdate`

Actualiza rerere autoupdate como parte de crear un commit que invierte el efecto de otro commit. En Git 2.51.1, la ayuda corta expresa el contrato como `update the index with reused conflict resolution if possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git revert --rerere-autoupdate a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--strategy`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git revert` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git revert --strategy=ort a1b2c3d
git status --short
```

El ejemplo usa `ort` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-X` y `--strategy-option`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git revert` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `--strategy-option`

```bash
git revert --strategy-option=valor a1b2c3d
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--reference`

Define reference para esta ejecución de `git revert`. En Git 2.51.1, la ayuda corta expresa el contrato como `use the 'reference' format to refer to commits`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git revert --reference a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-rerere-autoupdate`

Desactiva para esta invocación el comportamiento que habilita `--rerere-autoupdate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git revert --no-rerere-autoupdate a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gpg-sign`

Desactiva para esta invocación el comportamiento que habilita `--gpg-sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git revert --no-gpg-sign a1b2c3d
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git replay`](../patching/replay.md)
- [`git rebase`](../patching/rebase.md)

## Fuente

- [git-revert - Revert some existing commits](https://git-scm.com/docs/git-revert)
