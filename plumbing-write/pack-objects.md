---
title: "git pack-objects"
source: "https://git-scm.com/docs/git-pack-objects"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git pack-objects`

Este caso usa `git pack-objects` para crear un archivo pack a partir de objetos.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
mkdir -p packs
git rev-list --objects --all | git pack-objects packs/pack
```

La invocación `git pack-objects` ejecuta esta operación: crear un archivo pack a partir de objetos. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git pack-objects [-q | --progress | --all-progress] [--all-progress-implied]
		   [--no-reuse-delta] [--delta-base-offset] [--non-empty]
		   [--local] [--incremental] [--window=<n>] [--depth=<n>]
		   [--revs [--unpacked | --all]] [--keep-pack=<pack-name>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

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

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git pack-objects --quiet
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git pack-objects --progress
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all-progress`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git pack-objects --all-progress
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all-progress-implied`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git pack-objects --all-progress-implied
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reuse-delta`

Desactiva el comportamiento `reuse-delta` para esta invocación.

```bash
git pack-objects --no-reuse-delta
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--delta-base-offset`

Define delta base offset para esta ejecución de `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `use OFS_DELTA objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --delta-base-offset
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--non-empty`

Crea non vacío como parte de crear un archivo pack a partir de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `do not create an empty pack output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --non-empty
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--local`

Opera sobre la configuración del repositorio.

```bash
git pack-objects --local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--incremental`

Ignora incremental dentro del alcance que procesa `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `ignore packed objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --incremental
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--window`

Limita crear un archivo pack a partir de objetos al alcance identificado por window. En Git 2.51.1, la ayuda corta expresa el contrato como `limit pack window by objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --window=5
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--depth`

Establece un límite numérico para la selección o el recorrido.

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

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unpacked`

Limita crear un archivo pack a partir de objetos al alcance identificado por unpacked. En Git 2.51.1, la ayuda corta expresa el contrato como `limit the objects to those that are not yet packed`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --unpacked
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git pack-objects --all
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-pack`

Ignora conservar pack dentro del alcance que procesa `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `ignore this pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --keep-pack=tema
git fsck --no-progress
```

El ejemplo usa `tema` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cruft`

Crea cruft como parte de crear un archivo pack a partir de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `create a cruft pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --cruft
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cruft-expiration`

Retira cruft expiration del alcance que procesa `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `expire cruft objects older than <time>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --cruft-expiration=2026-01-15T10:00:00Z
git fsck --no-progress
```

El ejemplo usa `2026-01-15T10:00:00Z` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdout`

Incluye salida estándar en la salida o cambia cómo `git pack-objects` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output pack to stdout`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --stdout
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--filter`

Limita los objetos transferidos mediante una especificación de filtro de clon parcial. En Git 2.51.1, la ayuda corta expresa el contrato como `object filtering`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --filter=valor
git fsck --no-progress
```

### `--shallow`

Crea historial shallow como parte de crear un archivo pack a partir de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `create packs suitable for shallow fetches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --shallow
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-true-parents`

Impide conservar true parents durante esta invocación de `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not hide commits by grafts`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --keep-true-parents
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sparse`

Permite operar sobre entradas que quedan fuera de la selección sparse activa.

La opción selecciona el procedimiento que `git pack-objects` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git pack-objects --sparse
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--name-hash-version`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git pack-objects --name-hash-version=5
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--path-walk`

Define ruta walk para esta ejecución de `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `use the path-walk API to walk objects when possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --path-walk
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index-version`

Escribe o registra índice versión como parte de crear un archivo pack a partir de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `write the pack index file in the specified idx format version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --index-version=valor
git fsck --no-progress
```

### `--max-pack-size`

Establece un límite numérico para la selección o el recorrido.

```bash
git pack-objects --max-pack-size=5
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--window-memory`

Limita crear un archivo pack a partir de objetos al alcance identificado por window memory. En Git 2.51.1, la ayuda corta expresa el contrato como `limit pack window by memory in addition to object limit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --window-memory=5
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reuse-delta`

Reutiliza reuse delta en vez de volver a calcularlo o crearlo durante crear un archivo pack a partir de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `reuse existing deltas`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --reuse-delta
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reuse-object`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git pack-objects --reuse-object
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--threads`

Define threads para esta ejecución de `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `use threads when searching for best delta matches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --threads=5
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reflog`

Incluye reflog en la entrada, el resultado o el registro que construye `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `include objects referred by reflog entries`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --reflog
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--indexed-objects`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git pack-objects --indexed-objects
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

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

```bash
git pack-objects --include-tag
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-unreachable`

Activa conservar unreachable durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `keep unreachable objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --keep-unreachable
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pack-loose-unreachable`

Activa pack loose unreachable durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pack loose unreachable objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --pack-loose-unreachable
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unpack-unreachable`

Activa unpack unreachable durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `unpack unreachable objects newer than <time>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --unpack-unreachable=2026-01-15T10:00:00Z
git fsck --no-progress
```

El ejemplo usa `2026-01-15T10:00:00Z` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--thin`

Crea thin como parte de crear un archivo pack a partir de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `create thin packs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --thin
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--honor-pack-keep`

Ignora honor pack conservar dentro del alcance que procesa `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `ignore packs that have companion .keep file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git pack-objects` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git pack-objects --honor-pack-keep
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--compression`

Activa compression durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pack compression level`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --compression=5
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--use-bitmap-index`

Define use bitmap índice para esta ejecución de `git pack-objects`. En Git 2.51.1, la ayuda corta expresa el contrato como `use a bitmap index if available to speed up counting objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --use-bitmap-index
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--write-bitmap-index`

Permite crear o escribir el elemento seleccionado.

```bash
git pack-objects --write-bitmap-index
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--missing`

Activa missing durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `handling for missing objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --missing=warn
git fsck --no-progress
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude-promisor-objects`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git pack-objects --exclude-promisor-objects
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude-promisor-objects-best-effort`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git pack-objects --exclude-promisor-objects-best-effort
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--delta-islands`

Activa delta islands durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `respect islands during delta compression`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --delta-islands
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--uri-protocol`

Activa uri protocol durante crear un archivo pack a partir de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `exclude any configured uploadpack.blobpackfileuri with this protocol`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pack-objects --uri-protocol=valor
git fsck --no-progress
```

## Páginas relacionadas

- [`git prune-packed`](../plumbing-write/prune-packed.md)
- [`git multi-pack-index`](../plumbing-write/multi-pack-index.md)
- [`git read-tree`](../plumbing-write/read-tree.md)

## Fuente

- [git-pack-objects - Create a packed archive of objects](https://git-scm.com/docs/git-pack-objects)
