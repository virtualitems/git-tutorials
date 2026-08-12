---
title: "git switch"
source: "https://git-scm.com/docs/git-switch"
section: "branching-and-merging"
status: "option-expanded"
---

# `git switch`

Este caso usa `git switch` para cambiar de rama o crear una rama antes de cambiar. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git switch consulta o cambia referencias, `HEAD`, worktrees y estados de integración. Recibe como entrada las ramas, commits o rutas que participan en la operación. La operación consiste en cambiar de rama o crear una rama antes de cambiar.

Puede persistir el estado implicado por esta operación: cambiar de rama o crear una rama antes de cambiar. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git switch -c tema-portada
git switch main
```

La invocación `git switch -c tema-portada` ejecuta esta operación: cambiar de rama o crear una rama antes de cambiar. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git switch [<options>] [--no-guess] <branch>
git switch [<options>] --detach [<start-point>]
git switch [<options>] (-c|-C) <new-branch> [<start-point>]
git switch [<options>] --orphan <new-branch>
```

### Uso verificado con `git version 2.51.1`

```text
git switch [<options>] [<branch>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git switch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

cambiar de rama o crear una rama antes de cambiar. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git switch a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git switch con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--no-guess`

Desactiva el comportamiento `guess` para esta invocación.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o crear una rama antes de cambiar. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git switch --no-guess -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--detach` y `-d`

Hace que `HEAD` apunte directamente a un commit.  La misma línea de ayuda también acepta `-d`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git switch`, HEAD separado modifica la forma en que se ejecuta cambiar de rama o crear una rama antes de cambiar. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--detach`

```bash
git switch --detach -c tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `-d`

```bash
git switch -d -c tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-c` y `--create`

Permite crear o escribir el elemento seleccionado.  La misma línea de ayuda también acepta `-c`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o crear una rama antes de cambiar. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-c`

```bash
git switch -c main
git status --short
```

En esta forma, `main` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--create`

```bash
git switch --create=main
git status --short
```

En esta forma, `main` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-C` y `--force-create`

Permite crear o escribir el elemento seleccionado.  La misma línea de ayuda también acepta `-C`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla omitir la protección crear. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o crear una rama antes de cambiar puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-C`

```bash
git switch -C main -c tema-portada
git status --short
```

En esta forma, `main` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--force-create`

```bash
git switch --force-create=main -c tema-portada
git status --short
```

En esta forma, `main` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--orphan`

Crea o cambia a una rama sin padres en el historial existente. En Git 2.51.1, la ayuda corta expresa el contrato como `new unborn branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o crear una rama antes de cambiar. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git switch --orphan=main -c tema-portada
git status --short
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--guess`

Permite deducir una rama local a partir de una rama remota con el mismo nombre. En Git 2.51.1, la ayuda corta expresa el contrato como `second guess 'git switch <no-such-branch>'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o crear una rama antes de cambiar. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git switch --guess -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--discard-changes`

Activa discard changes durante cambiar de rama o crear una rama antes de cambiar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `throw away local modifications`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción controla discard changes. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o crear una rama antes de cambiar puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git switch --discard-changes -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git switch -q -c tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--quiet`

```bash
git switch --quiet -c tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git switch --recurse-submodules=valor -c tema-portada
git status --short
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

La opción controla progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o crear una rama antes de cambiar puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git switch --progress -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--merge`

Ejecuta merge durante cambiar de rama o crear una rama antes de cambiar. En Git 2.51.1, la ayuda corta expresa el contrato como `perform a 3-way merge with the new branch`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-m`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o crear una rama antes de cambiar. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-m`

```bash
git switch -m -c tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--merge`

```bash
git switch --merge -c tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--conflict`

Selecciona el estilo de marcadores que Git escribe al materializar un conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `conflict style (merge, diff3, or zdiff3)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git switch`, conflict modifica la forma en que se ejecuta cambiar de rama o crear una rama antes de cambiar. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git switch --conflict=short -c tema-portada
git status --short
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-t` y `--track`

Crea o ajusta la asociación de seguimiento solicitada.  La misma línea de ayuda también acepta `-t`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o crear una rama antes de cambiar. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-t`

```bash
git switch -t=valor -c tema-portada
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--track`

```bash
git switch --track=valor -c tema-portada
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.  La misma línea de ayuda también acepta `-f`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o crear una rama antes de cambiar puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-f`

```bash
git switch -f -c tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--force`

```bash
git switch --force -c tema-portada
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--overwrite-ignore`

Excluye elementos que cumplan la condición indicada.

La opción controla overwrite ignorar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o crear una rama antes de cambiar puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git switch --overwrite-ignore -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-other-worktrees`

Excluye elementos que cumplan la condición indicada.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o crear una rama antes de cambiar. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git switch --ignore-other-worktrees -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-detach`

Desactiva para esta invocación el comportamiento que habilita `--detach`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git switch`, desactivar HEAD separado modifica la forma en que se ejecuta cambiar de rama o crear una rama antes de cambiar. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git switch --no-detach -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-orphan`

Desactiva para esta invocación el comportamiento que habilita `--orphan`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o crear una rama antes de cambiar. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git switch --no-orphan -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-create`

Desactiva para esta invocación el comportamiento que habilita `--create`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o crear una rama antes de cambiar. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git switch --no-create
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force-create`

Desactiva para esta invocación el comportamiento que habilita `--force-create`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección crear. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o crear una rama antes de cambiar puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git switch --no-force-create -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-discard-changes`

Desactiva para esta invocación el comportamiento que habilita `--discard-changes`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar discard changes. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o crear una rama antes de cambiar puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git switch --no-discard-changes -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git switch --no-quiet -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git switch --no-recurse-submodules -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o crear una rama antes de cambiar puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git switch --no-progress -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-merge`

Desactiva para esta invocación el comportamiento que habilita `--merge`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o crear una rama antes de cambiar. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git switch --no-merge -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-conflict`

Desactiva para esta invocación el comportamiento que habilita `--conflict`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git switch`, desactivar conflict modifica la forma en que se ejecuta cambiar de rama o crear una rama antes de cambiar. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git switch --no-conflict -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-track`

Desactiva para esta invocación el comportamiento que habilita `--track`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o crear una rama antes de cambiar. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git switch --no-track -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force`

Desactiva para esta invocación el comportamiento que habilita `--force`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o crear una rama antes de cambiar puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git switch --no-force -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-overwrite-ignore`

Desactiva para esta invocación el comportamiento que habilita `--overwrite-ignore`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar overwrite ignorar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o crear una rama antes de cambiar puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git switch --no-overwrite-ignore -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-other-worktrees`

Desactiva para esta invocación el comportamiento que habilita `--ignore-other-worktrees`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o crear una rama antes de cambiar. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git switch --no-ignore-other-worktrees -c tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git switch` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La referencia es ambigua

Comprueba esta causa: Un nombre coincide con más de un objeto o una ruta. Usa `--` para separar rutas y una revisión completa para el objeto.

### El cambio de rama se rechaza

Comprueba esta causa: Hay modificaciones que serían sobrescritas. Confirma el estado y decide entre commit, stash o descarte.

### La integración se detiene

Comprueba esta causa: Dos cambios afectan la misma región o ruta. Resuelve, añade los archivos y usa la orden `--continue` o `--abort` que corresponda.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: cambiar de rama o crear una rama antes de cambiar. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git tag`](../branching-and-merging/tag.md)
- [`git stash`](../branching-and-merging/stash.md)
- [`git worktree`](../branching-and-merging/worktree.md)

## Fuente

- [git-switch - Switch branches](https://git-scm.com/docs/git-switch)
