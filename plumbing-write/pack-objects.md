---
title: "git pack-objects"
source: "https://git-scm.com/docs/git-pack-objects"
section: "plumbing-write"
status: "option-expanded"
---

# `git pack-objects`

Este caso usa `git pack-objects` para crear un archivo pack a partir de objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git pack-objects crea objetos, índices, packs o referencias mediante contratos de bajo nivel. Recibe como entrada identificadores, entradas del índice o referencias validadas por el script. La operación consiste en crear un archivo pack a partir de objetos.

Puede persistir el estado implicado por esta operación: crear un archivo pack a partir de objetos. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
mkdir -p packs
git rev-list --objects --all | git pack-objects packs/pack
```

La invocación `git pack-objects` ejecuta esta operación: crear un archivo pack a partir de objetos. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git pack-objects [-q | --progress | --all-progress] [--all-progress-implied]
		   [--no-reuse-delta] [--delta-base-offset] [--non-empty]
		   [--local] [--incremental] [--window=<n>] [--depth=<n>]
		   [--revs [--unpacked | --all]] [--keep-pack=<pack-name>]
```

### Uso verificado con `git version 2.51.1`

```text
git pack-objects [-q | --progress | --all-progress] [--all-progress-implied]
                        [--no-reuse-delta] [--delta-base-offset] [--non-empty]
                        [--local] [--incremental] [--window=<n>] [--depth=<n>]
                        [--revs [--unpacked | --all]] [--keep-pack=<pack-name>]
                        [--cruft] [--cruft-expiration=<time>]
                        [--stdout [--filter=<filter-spec>] | <base-name>]
                        [--shallow] [--keep-true-parents] [--[no-]sparse]
                        [--name-hash-version=<n>] [--path-walk] < <object-list>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git pack-objects -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

crear un archivo pack a partir de objetos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git pack-objects a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git pack-objects con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git pack-objects -q
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

#### Ejemplo con `--quiet`

```bash
git pack-objects --quiet
git fsck --no-progress
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pack-objects --progress
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all-progress`

Incluye elementos adicionales dentro del alcance indicado.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pack-objects --all-progress
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all-progress-implied`

Incluye elementos adicionales dentro del alcance indicado.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pack-objects --all-progress-implied
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reuse-delta`

Desactiva el comportamiento `reuse-delta` para esta invocación.

En `git pack-objects`, desactivar reuse delta modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-reuse-delta
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--delta-base-offset`

Define delta base offset para esta ejecución de `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `use OFS_DELTA objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, delta base offset modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --delta-base-offset
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--non-empty`

Crea non vacío como parte de crear un archivo pack a partir de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `do not create an empty pack output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pack-objects --non-empty
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--local`

Opera sobre la configuración del repositorio.

En `git pack-objects`, alcance local modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--incremental`

Ignora incremental dentro del alcance que procesa `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `ignore packed objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, incremental modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --incremental
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--window`

Limita crear un archivo pack a partir de objetos al alcance identificado por window. En Git 2.51.1, la ayuda corta expresa el contrato como `limit pack window by objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, window modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --window=5
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--depth`

Establece un límite numérico para la selección o el recorrido.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --depth=5
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--revs`

Lee revs como parte de la entrada de `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `read revision arguments from standard input`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git pack-objects` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git pack-objects --revs
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unpacked`

Limita crear un archivo pack a partir de objetos al alcance identificado por unpacked. En Git 2.51.1, la ayuda corta expresa el contrato como `limit the objects to those that are not yet packed`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, unpacked modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --unpacked
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --all
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-pack`

Ignora conservar pack dentro del alcance que procesa `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `ignore this pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, conservar pack modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --keep-pack=tema
git fsck --no-progress
```

El ejemplo usa `tema` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cruft`

Crea cruft como parte de crear un archivo pack a partir de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `create a cruft pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, cruft modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --cruft
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cruft-expiration`

Retira cruft expiration del alcance que procesa `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `expire cruft objects older than <time>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción controla cruft expiration. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque crear un archivo pack a partir de objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git pack-objects --cruft-expiration=2026-01-15T10:00:00Z
git fsck --no-progress
```

El ejemplo usa `2026-01-15T10:00:00Z` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdout`

Incluye salida estándar en la salida o cambia cómo `git pack-objects` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output pack to stdout`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pack-objects --stdout
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--filter`

Limita los objetos transferidos mediante una especificación de filtro de clon parcial. En Git 2.51.1, la ayuda corta expresa el contrato como `object filtering`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --filter=valor
git fsck --no-progress
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow`

Crea historial shallow como parte de crear un archivo pack a partir de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `create packs suitable for shallow fetches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --shallow
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-true-parents`

Impide conservar true parents durante esta invocación de `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not hide commits by grafts`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, conservar true parents modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --keep-true-parents
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sparse`

Permite operar sobre entradas que quedan fuera de la selección sparse activa.

La opción selecciona el procedimiento que `git pack-objects` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git pack-objects --sparse
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--name-hash-version`

Selecciona la representación o tratamiento de identificadores de objeto.

En `git pack-objects`, nombre hash versión modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --name-hash-version=5
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--path-walk`

Define ruta walk para esta ejecución de `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `use the path-walk API to walk objects when possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, ruta walk modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --path-walk
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index-version`

Escribe o registra índice versión como parte de crear un archivo pack a partir de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `write the pack index file in the specified idx format version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pack-objects --index-version=valor
git fsck --no-progress
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-pack-size`

Establece un límite numérico para la selección o el recorrido.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pack-objects --max-pack-size=5
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--window-memory`

Limita crear un archivo pack a partir de objetos al alcance identificado por window memory. En Git 2.51.1, la ayuda corta expresa el contrato como `limit pack window by memory in addition to object limit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, window memory modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --window-memory=5
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reuse-delta`

Reutiliza reuse delta en vez de volver a calcularlo o crearlo durante crear un archivo pack a partir de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `reuse existing deltas`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, reuse delta modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --reuse-delta
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reuse-object`

Selecciona la representación o tratamiento de identificadores de objeto.

En `git pack-objects`, reuse objeto modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --reuse-object
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--threads`

Define threads para esta ejecución de `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `use threads when searching for best delta matches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, threads modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --threads=5
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reflog`

Incluye reflog en la entrada, el resultado o el registro que construye `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `include objects referred by reflog entries`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --reflog
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--indexed-objects`

Selecciona la representación o tratamiento de identificadores de objeto.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --indexed-objects
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin-packs`

Lee entrada estándar packs como parte de la entrada de `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `read packs from stdin`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git pack-objects` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git pack-objects --stdin-packs=all
git fsck --no-progress
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include-tag`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --include-tag
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-unreachable`

Activa conservar unreachable durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `keep unreachable objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, conservar unreachable modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --keep-unreachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pack-loose-unreachable`

Activa pack loose unreachable durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pack loose unreachable objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, pack loose unreachable modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --pack-loose-unreachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unpack-unreachable`

Activa unpack unreachable durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `unpack unreachable objects newer than <time>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, unpack unreachable modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --unpack-unreachable=2026-01-15T10:00:00Z
git fsck --no-progress
```

El ejemplo usa `2026-01-15T10:00:00Z` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--thin`

Crea thin como parte de crear un archivo pack a partir de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `create thin packs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, thin modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --thin
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--honor-pack-keep`

Ignora honor pack conservar dentro del alcance que procesa `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `ignore packs that have companion .keep file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git pack-objects` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git pack-objects --honor-pack-keep
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--compression`

Activa compression durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pack compression level`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, compression modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --compression=5
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--use-bitmap-index`

Define use bitmap índice para esta ejecución de `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `use a bitmap index if available to speed up counting objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, use bitmap índice modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --use-bitmap-index
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--write-bitmap-index`

Permite crear o escribir el elemento seleccionado.

En `git pack-objects`, write bitmap índice modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --write-bitmap-index
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--missing`

Activa missing durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `handling for missing objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, missing modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --missing=warn
git fsck --no-progress
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude-promisor-objects`

Selecciona la representación o tratamiento de identificadores de objeto.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --exclude-promisor-objects
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude-promisor-objects-best-effort`

Selecciona la representación o tratamiento de identificadores de objeto.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --exclude-promisor-objects-best-effort
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--delta-islands`

Activa delta islands durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `respect islands during delta compression`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git pack-objects`, delta islands modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --delta-islands
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--uri-protocol`

Activa uri protocol durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `exclude any configured uploadpack.blobpackfileuri with this protocol`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --uri-protocol=valor
git fsck --no-progress
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pack-objects --no-progress
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-all-progress`

Desactiva para esta invocación el comportamiento que habilita `--all-progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pack-objects --no-all-progress
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-all-progress-implied`

Desactiva para esta invocación el comportamiento que habilita `--all-progress-implied`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pack-objects --no-all-progress-implied
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-delta-base-offset`

Desactiva para esta invocación el comportamiento que habilita `--delta-base-offset`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar delta base offset modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-delta-base-offset
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-non-empty`

Desactiva para esta invocación el comportamiento que habilita `--non-empty`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pack-objects --no-non-empty
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-local`

Desactiva para esta invocación el comportamiento que habilita `--local`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar alcance local modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-local
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-incremental`

Desactiva para esta invocación el comportamiento que habilita `--incremental`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar incremental modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-incremental
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-window`

Desactiva para esta invocación el comportamiento que habilita `--window`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar window modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-window
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-depth`

Desactiva para esta invocación el comportamiento que habilita `--depth`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --no-depth
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-revs`

Desactiva para esta invocación el comportamiento que habilita `--revs`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git pack-objects` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git pack-objects --no-revs
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-all`

Desactiva para esta invocación el comportamiento que habilita `--all`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --no-all
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep-pack`

Desactiva para esta invocación el comportamiento que habilita `--keep-pack`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar conservar pack modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-keep-pack
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cruft`

Desactiva para esta invocación el comportamiento que habilita `--cruft`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar cruft modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-cruft
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-cruft-expiration`

Desactiva para esta invocación el comportamiento que habilita `--cruft-expiration`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar cruft expiration. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque crear un archivo pack a partir de objetos puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git pack-objects --no-cruft-expiration
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stdout`

Desactiva para esta invocación el comportamiento que habilita `--stdout`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pack-objects --no-stdout
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-filter`

Desactiva para esta invocación el comportamiento que habilita `--filter`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --no-filter
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-shallow`

Desactiva para esta invocación el comportamiento que habilita `--shallow`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --no-shallow
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep-true-parents`

Desactiva para esta invocación el comportamiento que habilita `--keep-true-parents`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar conservar true parents modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-keep-true-parents
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-sparse`

Desactiva para esta invocación el comportamiento que habilita `--sparse`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción selecciona el procedimiento que `git pack-objects` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git pack-objects --no-sparse
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-name-hash-version`

Desactiva para esta invocación el comportamiento que habilita `--name-hash-version`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar nombre hash versión modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-name-hash-version
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-path-walk`

Desactiva para esta invocación el comportamiento que habilita `--path-walk`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar ruta walk modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-path-walk
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git pack-objects --no-quiet
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reuse-object`

Desactiva para esta invocación el comportamiento que habilita `--reuse-object`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar reuse objeto modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-reuse-object
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-threads`

Desactiva para esta invocación el comportamiento que habilita `--threads`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar threads modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-threads
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stdin-packs`

Desactiva para esta invocación el comportamiento que habilita `--stdin-packs`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git pack-objects` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git pack-objects --no-stdin-packs
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-include-tag`

Desactiva para esta invocación el comportamiento que habilita `--include-tag`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --no-include-tag
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep-unreachable`

Desactiva para esta invocación el comportamiento que habilita `--keep-unreachable`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar conservar unreachable modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-keep-unreachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-pack-loose-unreachable`

Desactiva para esta invocación el comportamiento que habilita `--pack-loose-unreachable`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar pack loose unreachable modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-pack-loose-unreachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-unpack-unreachable`

Desactiva para esta invocación el comportamiento que habilita `--unpack-unreachable`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar unpack unreachable modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-unpack-unreachable
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-thin`

Desactiva para esta invocación el comportamiento que habilita `--thin`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar thin modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-thin
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-honor-pack-keep`

Desactiva para esta invocación el comportamiento que habilita `--honor-pack-keep`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git pack-objects` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git pack-objects --no-honor-pack-keep
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-compression`

Desactiva para esta invocación el comportamiento que habilita `--compression`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar compression modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-compression
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-use-bitmap-index`

Desactiva para esta invocación el comportamiento que habilita `--use-bitmap-index`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar use bitmap índice modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-use-bitmap-index
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-write-bitmap-index`

Desactiva para esta invocación el comportamiento que habilita `--write-bitmap-index`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar write bitmap índice modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-write-bitmap-index
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-exclude-promisor-objects`

Desactiva para esta invocación el comportamiento que habilita `--exclude-promisor-objects`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --no-exclude-promisor-objects
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-exclude-promisor-objects-best-effort`

Desactiva para esta invocación el comportamiento que habilita `--exclude-promisor-objects-best-effort`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --no-exclude-promisor-objects-best-effort
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-delta-islands`

Desactiva para esta invocación el comportamiento que habilita `--delta-islands`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git pack-objects`, desactivar delta islands modifica la forma en que se ejecuta crear un archivo pack a partir de objetos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git pack-objects --no-delta-islands
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-uri-protocol`

Desactiva para esta invocación el comportamiento que habilita `--uri-protocol`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un archivo pack a partir de objetos. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git pack-objects --no-uri-protocol
git fsck --no-progress
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git pack-objects` o a otra opción. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El hash no coincide

Comprueba esta causa: Los bytes, el tipo o la longitud difieren. Compara la entrada byte por byte y no normalices el contenido.

### La referencia no se actualiza

Comprueba esta causa: El valor anterior no coincide con la condición. Lee el valor actual y repite con una condición nueva.

### El índice queda sin resolver

Comprueba esta causa: Una entrada tiene etapas de conflicto. Inspecciona `git ls-files --stage` antes de escribir un árbol.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: crear un archivo pack a partir de objetos. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git prune-packed`](../plumbing-write/prune-packed.md)
- [`git multi-pack-index`](../plumbing-write/multi-pack-index.md)
- [`git read-tree`](../plumbing-write/read-tree.md)

## Fuente

- [git-pack-objects - Create a packed archive of objects](https://git-scm.com/docs/git-pack-objects)
