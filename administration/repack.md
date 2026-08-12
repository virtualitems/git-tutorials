---
title: "git repack"
source: "https://git-scm.com/docs/git-repack"
section: "administration"
status: "option-expanded"
---

# `git repack`

Este caso usa `git repack` para reorganizar objetos dentro de archivos pack. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git repack comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Recibe como entrada los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. La operación consiste en reorganizar objetos dentro de archivos pack.

Puede persistir el estado implicado por esta operación: reorganizar objetos dentro de archivos pack. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git count-objects -v
git repack -ad
git count-objects -v
```

La invocación `git repack -ad` ejecuta esta operación: reorganizar objetos dentro de archivos pack. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git repack [-a] [-A] [-d] [-f] [-F] [-l] [-n] [-q] [-b] [-m]
	[--window=<n>] [--depth=<n>] [--threads=<n>] [--keep-pack=<pack-name>]
	[--write-midx[=<mode>]] [--name-hash-version=<n>] [--path-walk]
```

### Uso verificado con `git version 2.51.1`

```text
git repack [-a] [-A] [-d] [-f] [-F] [-l] [-n] [-q] [-b] [-m]
       [--window=<n>] [--depth=<n>] [--threads=<n>] [--keep-pack=<pack-name>]
       [--write-midx] [--name-hash-version=<n>] [--path-walk]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git repack -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

reorganizar objetos dentro de archivos pack. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git repack a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git repack con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-a`

Activa a durante reorganizar objetos dentro de archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pack everything in a single pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git repack`, a modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack -a -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-A`

Selecciona la relación indicada por A; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `same as -a, and turn unreachable objects loose`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git repack`, A modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack -A -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d`

Ejecuta d durante reorganizar objetos dentro de archivos pack. En Git 2.51.1, la ayuda corta expresa el contrato como `remove redundant packs, and run git-prune-packed`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción controla d. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque reorganizar objetos dentro de archivos pack puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git repack -d -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f`

Reutiliza f en vez de volver a calcularlo o crearlo durante reorganizar objetos dentro de archivos pack. En Git 2.51.1, la ayuda corta expresa el contrato como `pass --no-reuse-delta to git-pack-objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git repack`, f modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack -f -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-F`

Reutiliza F en vez de volver a calcularlo o crearlo durante reorganizar objetos dentro de archivos pack. En Git 2.51.1, la ayuda corta expresa el contrato como `pass --no-reuse-object to git-pack-objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git repack`, F modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack -F -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-l` y `--local`

Opera sobre la configuración del repositorio.  La misma línea de ayuda también acepta `-l`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git repack`, alcance local modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-l`

```bash
git repack -l -ad
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--local`

```bash
git repack --local -ad
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-n`

Ejecuta n durante reorganizar objetos dentro de archivos pack. En Git 2.51.1, la ayuda corta expresa el contrato como `do not run git-update-server-info`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git repack`, n modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack -n -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git repack -q -ad
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--quiet`

```bash
git repack --quiet -ad
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-b` y `--write-bitmap-index`

Permite crear o escribir el elemento seleccionado.  La misma línea de ayuda también acepta `-b`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git repack`, write bitmap índice modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-b`

```bash
git repack -b -ad
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--write-bitmap-index`

```bash
git repack --write-bitmap-index -ad
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-m` y `--write-midx`

Permite crear o escribir el elemento seleccionado.  La misma línea de ayuda también acepta `-m` y `-pack`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git repack`, write midx modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-m`

```bash
git repack -m -ad
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--write-midx`

```bash
git repack --write-midx -ad
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--window`

Activa window durante reorganizar objetos dentro de archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `size of the window used for delta compression`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git repack`, window modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --window=5 -ad
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--depth`

Establece un límite numérico para la selección o el recorrido.

En `git repack`, profundidad modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --depth=5 -ad
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--threads`

Define el límite representado por threads para esta ejecución. En Git 2.51.1, la ayuda corta expresa el contrato como `limits the maximum number of threads`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git repack`, threads modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --threads=5 -ad
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-pack`

Impide conservar pack durante esta invocación de `git repack`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not repack this pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git repack`, conservar pack modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --keep-pack=tema -ad
git count-objects -vH
```

El ejemplo usa `tema` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--name-hash-version`

Selecciona la representación o tratamiento de identificadores de objeto.

En `git repack`, nombre hash versión modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --name-hash-version=5 -ad
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--path-walk`

Activa ruta walk durante reorganizar objetos dentro de archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pass --path-walk to git-pack-objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git repack`, ruta walk modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --path-walk -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cruft`

Selecciona la relación indicada por cruft; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `same as -a, pack unreachable cruft objects separately`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git repack`, cruft modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --cruft -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cruft-expiration`

Retira cruft expiration del alcance que procesa `git repack`. En Git 2.51.1, la ayuda corta expresa el contrato como `with --cruft, expire objects older than this`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción controla cruft expiration. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque reorganizar objetos dentro de archivos pack puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git repack --cruft-expiration=2026-01-15 -ad
git count-objects -vH
```

El ejemplo usa `2026-01-15` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--combine-cruft-below-size`

Limita reorganizar objetos dentro de archivos pack al alcance identificado por combine cruft below size. En Git 2.51.1, la ayuda corta expresa el contrato como `with --cruft, only repack cruft packs smaller than this`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta reorganizar objetos dentro de archivos pack. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git repack --combine-cruft-below-size=5 -ad
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-cruft-size`

Establece un límite numérico para la selección o el recorrido.

En `git repack`, máximo cruft size modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --max-cruft-size=5 -ad
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reuse-delta`

Desactiva el comportamiento `reuse-delta` para esta invocación.

En `git repack`, desactivar reuse delta modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-reuse-delta -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reuse-object`

Desactiva el comportamiento `reuse-object` para esta invocación.

En `git repack`, desactivar reuse objeto modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-reuse-object -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-i` y `--delta-islands`

Activa delta islands durante reorganizar objetos dentro de archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pass --delta-islands to git-pack-objects`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-i`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git repack`, delta islands modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-i`

```bash
git repack -i -ad
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--delta-islands`

```bash
git repack --delta-islands -ad
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--unpack-unreachable`

Impide unpack unreachable durante esta invocación de `git repack`. En Git 2.51.1, la ayuda corta expresa el contrato como `with -A, do not loosen objects older than this`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git repack`, unpack unreachable modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --unpack-unreachable=2026-01-15 -ad
git count-objects -vH
```

El ejemplo usa `2026-01-15` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-k` y `--keep-unreachable`

Activa conservar unreachable durante reorganizar objetos dentro de archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `with -a, repack unreachable objects`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-k`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git repack`, conservar unreachable modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-k`

```bash
git repack -k -ad
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--keep-unreachable`

```bash
git repack --keep-unreachable -ad
git count-objects -vH
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--window-memory`

Selecciona la relación indicada por window memory; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `same as the above, but limit memory size instead of entries count`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git repack`, window memory modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --window-memory=valor -ad
git count-objects -vH
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-pack-size`

Establece un límite numérico para la selección o el recorrido.

La opción cambia cómo `git repack` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git repack --max-pack-size=5 -ad
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--filter`

Limita los objetos transferidos mediante una especificación de filtro de clon parcial. En Git 2.51.1, la ayuda corta expresa el contrato como `object filtering`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta reorganizar objetos dentro de archivos pack. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git repack --filter=valor -ad
git count-objects -vH
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pack-kept-objects`

Selecciona la representación o tratamiento de identificadores de objeto.

En `git repack`, pack kept objetos modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --pack-kept-objects -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-g` y `--geometric`

Activa geometric durante reorganizar objetos dentro de archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `find a geometric progression with factor <N>`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-g`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git repack`, geometric modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-g`

```bash
git repack -g 5 -ad
git count-objects -vH
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comprobar objetos sueltos, packs y espacio registrado.

#### Ejemplo con `--geometric`

```bash
git repack --geometric=5 -ad
git count-objects -vH
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comprobar objetos sueltos, packs y espacio registrado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--expire-to`

Aplica una fecha, duración o política de vencimiento.

La opción controla expire to. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque reorganizar objetos dentro de archivos pack puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git repack --expire-to=docs -ad
git count-objects -vH
```

El ejemplo usa `docs` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--filter-to`

Escribe o registra filtro to como parte de reorganizar objetos dentro de archivos pack. En Git 2.51.1, la ayuda corta expresa el contrato como `pack prefix to store a pack containing filtered out objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta reorganizar objetos dentro de archivos pack. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git repack --filter-to=docs -ad
git count-objects -vH
```

El ejemplo usa `docs` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-window`

Desactiva para esta invocación el comportamiento que habilita `--window`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar window modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-window -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-depth`

Desactiva para esta invocación el comportamiento que habilita `--depth`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar profundidad modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-depth -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-threads`

Desactiva para esta invocación el comportamiento que habilita `--threads`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar threads modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-threads -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep-pack`

Desactiva para esta invocación el comportamiento que habilita `--keep-pack`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar conservar pack modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-keep-pack -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-write-midx`

Desactiva para esta invocación el comportamiento que habilita `--write-midx`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar write midx modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-write-midx -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-name-hash-version`

Desactiva para esta invocación el comportamiento que habilita `--name-hash-version`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar nombre hash versión modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-name-hash-version -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-path-walk`

Desactiva para esta invocación el comportamiento que habilita `--path-walk`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar ruta walk modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-path-walk -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cruft`

Desactiva para esta invocación el comportamiento que habilita `--cruft`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar cruft modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-cruft -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cruft-expiration`

Desactiva para esta invocación el comportamiento que habilita `--cruft-expiration`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar cruft expiration. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque reorganizar objetos dentro de archivos pack puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git repack --no-cruft-expiration -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git repack --no-quiet -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-local`

Desactiva para esta invocación el comportamiento que habilita `--local`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar alcance local modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-local -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-write-bitmap-index`

Desactiva para esta invocación el comportamiento que habilita `--write-bitmap-index`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar write bitmap índice modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-write-bitmap-index -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-delta-islands`

Desactiva para esta invocación el comportamiento que habilita `--delta-islands`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar delta islands modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-delta-islands -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-unpack-unreachable`

Desactiva para esta invocación el comportamiento que habilita `--unpack-unreachable`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar unpack unreachable modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-unpack-unreachable -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep-unreachable`

Desactiva para esta invocación el comportamiento que habilita `--keep-unreachable`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar conservar unreachable modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-keep-unreachable -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-window-memory`

Desactiva para esta invocación el comportamiento que habilita `--window-memory`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar window memory modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-window-memory -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-filter`

Desactiva para esta invocación el comportamiento que habilita `--filter`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta reorganizar objetos dentro de archivos pack. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git repack --no-filter -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-pack-kept-objects`

Desactiva para esta invocación el comportamiento que habilita `--pack-kept-objects`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar pack kept objetos modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-pack-kept-objects -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-geometric`

Desactiva para esta invocación el comportamiento que habilita `--geometric`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git repack`, desactivar geometric modifica la forma en que se ejecuta reorganizar objetos dentro de archivos pack. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git repack --no-geometric -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-expire-to`

Desactiva para esta invocación el comportamiento que habilita `--expire-to`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar expire to. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque reorganizar objetos dentro de archivos pack puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git repack --no-expire-to -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-filter-to`

Desactiva para esta invocación el comportamiento que habilita `--filter-to`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta reorganizar objetos dentro de archivos pack. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git repack --no-filter-to -ad
git count-objects -vH
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git repack` o a otra opción. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un objeto aparece como inalcanzable

Comprueba esta causa: Ninguna referencia o reflog lo conserva. Determina si debe recuperarse antes de podar.

### El tamaño no disminuye

Comprueba esta causa: Los objetos siguen alcanzables o aún están protegidos por reflogs. Inspecciona alcanzabilidad y vencimientos.

### La operación se interrumpe

Comprueba esta causa: Otro proceso mantiene un lock. Comprueba procesos activos antes de retirar un lock obsoleto.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: reorganizar objetos dentro de archivos pack. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git replace`](../administration/replace.md)
- [`git reflog`](../administration/reflog.md)
- [`scalar`](../administration/scalar.md)

## Fuente

- [git-repack - Pack unpacked objects in a repository](https://git-scm.com/docs/git-repack)
