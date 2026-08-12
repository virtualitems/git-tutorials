---
title: "git cherry-pick"
source: "https://git-scm.com/docs/git-cherry-pick"
section: "patching"
status: "option-expanded"
---

# `git cherry-pick`

Este caso usa `git cherry-pick` para aplicar en la rama actual el cambio de commits existentes. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git cherry-pick aplica diffs o commits y mantiene un estado que puede continuar o abortarse. Recibe como entrada un parche, un commit o un rango que representa cambios. La operación consiste en aplicar en la rama actual el cambio de commits existentes.

Puede persistir el estado implicado por esta operación: aplicar en la rama actual el cambio de commits existentes. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Ejemplo mínimo

```bash
git switch release
git cherry-pick a1b2c3d
```

La invocación `git cherry-pick a1b2c3d` ejecuta esta operación: aplicar en la rama actual el cambio de commits existentes. Después, el diff y el historial muestran si cambiaron archivos, índice o commits. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git cherry-pick [--edit] [-n] [-m <parent-number>] [-s] [-x] [--ff]
		  [-S[<keyid>]] <commit>…
git cherry-pick (--continue | --skip | --abort | --quit)
```

### Uso verificado con `git version 2.51.1`

```text
git cherry-pick [--edit] [-n] [-m <parent-number>] [-s] [-x] [--ff]
                       [-S[<keyid>]] <commit>...
   or: git cherry-pick (--continue | --skip | --abort | --quit)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git cherry-pick -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

aplicar en la rama actual el cambio de commits existentes. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git cherry-pick a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Sesión interrumpida

Continuar o cancelar una secuencia después de revisar el estado. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Consulta `git status` antes de elegir la acción.

### Validación

Comprobar el resultado de git cherry-pick con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--edit` y `-e`

Abre la representación editable que define la orden antes de aplicarla.  La misma línea de ayuda también acepta `-e`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git cherry-pick`, edición modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--edit`

```bash
git cherry-pick --edit a1b2c3d
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `-e`

```bash
git cherry-pick -e a1b2c3d
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-n`

Impide n durante esta invocación de `git cherry-pick`. En Git 2.51.1, la ayuda corta expresa el contrato como `don't automatically commit`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `--no-commit`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar en la rama actual el cambio de commits existentes. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git cherry-pick -n a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--mainline`

Define mainline para esta ejecución de `git cherry-pick`. En Git 2.51.1, la ayuda corta expresa el contrato como `select mainline parent`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-m`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git cherry-pick`, mainline modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-m`

```bash
git cherry-pick -m 5 a1b2c3d
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--mainline`

```bash
git cherry-pick --mainline=5 a1b2c3d
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-s` y `--signoff`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-s`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git cherry-pick`, añadir Signed-off-by modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-s`

```bash
git cherry-pick -s a1b2c3d
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--signoff`

```bash
git cherry-pick --signoff a1b2c3d
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-x`

Activa x durante aplicar en la rama actual el cambio de commits existentes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `append commit name`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git cherry-pick`, x modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick -x a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ff`

Permite ff cuando la forma predeterminada de `git cherry-pick` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow fast-forward`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar en la rama actual el cambio de commits existentes. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git cherry-pick --ff a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-S` y `--gpg-sign`

Activa gpg sign durante aplicar en la rama actual el cambio de commits existentes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign commit`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-S`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git cherry-pick`, gpg sign modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-S`

```bash
git cherry-pick -S=user.name a1b2c3d
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--gpg-sign`

```bash
git cherry-pick --gpg-sign=user.name a1b2c3d
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--continue`

Reanuda una secuencia pausada después de resolver su estado.

Esta forma se usa cuando `git cherry-pick` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque continuar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git cherry-pick --continue
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--skip`

Omite el elemento actual y continúa la secuencia.

Esta forma se usa cuando `git cherry-pick` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque omitir el elemento actual actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git cherry-pick --skip
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--abort`

Cancela la secuencia y restaura el punto que la orden registró al comenzar.

Esta forma se usa cuando `git cherry-pick` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque abortar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git cherry-pick --abort
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quit`

Sale de la secuencia y conserva el estado que la documentación define.

Esta forma se usa cuando `git cherry-pick` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque salir actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git cherry-pick --quit
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cleanup`

Selecciona cómo Git retira comentarios y espacios del mensaje antes de crear el commit.

En `git cherry-pick`, cleanup modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick --cleanup=all a1b2c3d
git status --short
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-commit`

Desactiva el comportamiento `commit` para esta invocación.

En `git cherry-pick`, desactivar commit modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick --no-commit a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--commit`

Selecciona la relación indicada por commit; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git cherry-pick`, commit modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick --commit a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--rerere-autoupdate`

Actualiza rerere autoupdate como parte de aplicar en la rama actual el cambio de commits existentes. En Git 2.51.1, la ayuda corta expresa el contrato como `update the index with reused conflict resolution if possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git cherry-pick`, rerere autoupdate modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick --rerere-autoupdate a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--strategy`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git cherry-pick` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git cherry-pick --strategy=ort a1b2c3d
git status --short
```

El ejemplo usa `ort` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-X` y `--strategy-option`

Selecciona el algoritmo o estrategia que procesa la entrada.  La misma línea de ayuda también acepta `-X`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción selecciona el procedimiento que `git cherry-pick` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `-X`

```bash
git cherry-pick -X valor a1b2c3d
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--strategy-option`

```bash
git cherry-pick --strategy-option=valor a1b2c3d
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--allow-empty`

Permite continuar cuando el cambio produce un commit sin diferencias. En Git 2.51.1, la ayuda corta expresa el contrato como `preserve initially empty commits`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar en la rama actual el cambio de commits existentes. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git cherry-pick --allow-empty a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--allow-empty-message`

Permite crear un commit cuyo mensaje está vacío. En Git 2.51.1, la ayuda corta expresa el contrato como `allow commits with empty messages`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar en la rama actual el cambio de commits existentes. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git cherry-pick --allow-empty-message a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-redundant-commits`

Define conservar redundant commits para esta ejecución de `git cherry-pick`. En Git 2.51.1, la ayuda corta expresa el contrato como `deprecated: use --empty=keep instead`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git cherry-pick`, conservar redundant commits modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick --keep-redundant-commits a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--empty`

Activa vacío durante aplicar en la rama actual el cambio de commits existentes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `how to handle commits that become empty`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git cherry-pick`, vacío modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick --empty=valor a1b2c3d
git status --short
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-edit`

Conserva el mensaje existente sin abrir el editor.

En `git cherry-pick`, desactivar edición modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick --no-edit a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ff`

Desactiva para esta invocación el comportamiento que habilita `--ff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar en la rama actual el cambio de commits existentes. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git cherry-pick --no-ff a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cleanup`

Desactiva para esta invocación el comportamiento que habilita `--cleanup`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git cherry-pick`, desactivar cleanup modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick --no-cleanup a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signoff`

Desactiva para esta invocación el comportamiento que habilita `--signoff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git cherry-pick`, desactivar añadir Signed-off-by modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick --no-signoff a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-mainline`

Desactiva para esta invocación el comportamiento que habilita `--mainline`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git cherry-pick`, desactivar mainline modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick --no-mainline a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-rerere-autoupdate`

Desactiva para esta invocación el comportamiento que habilita `--rerere-autoupdate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git cherry-pick`, desactivar rerere autoupdate modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick --no-rerere-autoupdate a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-strategy`

Desactiva para esta invocación el comportamiento que habilita `--strategy`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción selecciona el procedimiento que `git cherry-pick` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git cherry-pick --no-strategy a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-strategy-option`

Desactiva para esta invocación el comportamiento que habilita `--strategy-option`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción selecciona el procedimiento que `git cherry-pick` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git cherry-pick --no-strategy-option a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gpg-sign`

Desactiva para esta invocación el comportamiento que habilita `--gpg-sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git cherry-pick`, desactivar gpg sign modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick --no-gpg-sign a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-allow-empty`

Desactiva para esta invocación el comportamiento que habilita `--allow-empty`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar en la rama actual el cambio de commits existentes. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git cherry-pick --no-allow-empty a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-allow-empty-message`

Desactiva para esta invocación el comportamiento que habilita `--allow-empty-message`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar en la rama actual el cambio de commits existentes. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git cherry-pick --no-allow-empty-message a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep-redundant-commits`

Desactiva para esta invocación el comportamiento que habilita `--keep-redundant-commits`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git cherry-pick`, desactivar conservar redundant commits modifica la forma en que se ejecuta aplicar en la rama actual el cambio de commits existentes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cherry-pick --no-keep-redundant-commits a1b2c3d
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cherry-pick` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un parche no aplica

Comprueba esta causa: El contexto no coincide con el contenido actual. Inspecciona los rechazos o resuelve el conflicto antes de continuar.

### La secuencia queda en pausa

Comprueba esta causa: Git espera una resolución o una decisión. Consulta `git status` y usa `--continue`, `--skip` o `--abort`.

### El resultado contiene commits vacíos

Comprueba esta causa: Los cambios ya existen o se resolvieron sin diferencias. Revisa el diff y aplica la política de commits vacíos de la orden.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: aplicar en la rama actual el cambio de commits existentes. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Trabaja en una rama de prueba. Compara `git diff`, `git diff --staged` y `git log --oneline --graph` antes y después.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git rebase`](../patching/rebase.md)
- [`git apply`](../patching/apply.md)
- [`git replay`](../patching/replay.md)

## Fuente

- [git-cherry-pick - Apply the changes introduced by some existing commits](https://git-scm.com/docs/git-cherry-pick)
