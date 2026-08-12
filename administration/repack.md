---
title: "git repack"
source: "https://git-scm.com/docs/git-repack"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `git repack`

Este caso usa `git repack` para reorganizar objetos dentro de archivos pack.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git count-objects -v
git repack -ad
git count-objects -v
```

La invocación `git repack -ad` ejecuta esta operación: reorganizar objetos dentro de archivos pack. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
git repack [-a] [-A] [-d] [-f] [-F] [-l] [-n] [-q] [-b] [-m]
	[--window=<n>] [--depth=<n>] [--threads=<n>] [--keep-pack=<pack-name>]
	[--write-midx[=<mode>]] [--name-hash-version=<n>] [--path-walk]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git repack [-a] [-A] [-d] [-f] [-F] [-l] [-n] [-q] [-b] [-m]
       [--window=<n>] [--depth=<n>] [--threads=<n>] [--keep-pack=<pack-name>]
       [--write-midx] [--name-hash-version=<n>] [--path-walk]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git repack -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-a`

Activa a durante reorganizar objetos dentro de archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pack everything in a single pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack -a -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-A`

Selecciona la relación indicada por A; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `same as -a, and turn unreachable objects loose`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack -A -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d`

Ejecuta d durante reorganizar objetos dentro de archivos pack. En Git 2.51.1, la ayuda corta expresa el contrato como `remove redundant packs, and run git-prune-packed`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack -d -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f`

Reutiliza f en vez de volver a calcularlo o crearlo durante reorganizar objetos dentro de archivos pack. En Git 2.51.1, la ayuda corta expresa el contrato como `pass --no-reuse-delta to git-pack-objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack -f -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-F`

Reutiliza F en vez de volver a calcularlo o crearlo durante reorganizar objetos dentro de archivos pack. En Git 2.51.1, la ayuda corta expresa el contrato como `pass --no-reuse-object to git-pack-objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack -F -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-l` y `--local`

Opera sobre la configuración del repositorio.

#### Ejemplo con `--local`

```bash
git repack --local -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `-n`

Ejecuta n durante reorganizar objetos dentro de archivos pack. En Git 2.51.1, la ayuda corta expresa el contrato como `do not run git-update-server-info`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack -n -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git repack --quiet -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `-b` y `--write-bitmap-index`

Permite crear o escribir el elemento seleccionado.

#### Ejemplo con `--write-bitmap-index`

```bash
git repack --write-bitmap-index -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `-m` y `--write-midx`

Permite crear o escribir el elemento seleccionado.  La misma línea de ayuda también acepta `-m` y `-pack`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

#### Ejemplo con `--write-midx`

```bash
git repack --write-midx -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--window`

Activa window durante reorganizar objetos dentro de archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `size of the window used for delta compression`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack --window=5 -ad
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--depth`

Establece un límite numérico para la selección o el recorrido.

```bash
git repack --depth=5 -ad
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--threads`

Define el límite representado por threads para esta ejecución. En Git 2.51.1, la ayuda corta expresa el contrato como `limits the maximum number of threads`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack --threads=5 -ad
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-pack`

Impide conservar pack durante esta invocación de `git repack`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not repack this pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack --keep-pack=tema -ad
git count-objects -vH
```

El ejemplo usa `tema` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--name-hash-version`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git repack --name-hash-version=5 -ad
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--path-walk`

Activa ruta walk durante reorganizar objetos dentro de archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pass --path-walk to git-pack-objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack --path-walk -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cruft`

Selecciona la relación indicada por cruft; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `same as -a, pack unreachable cruft objects separately`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack --cruft -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cruft-expiration`

Retira cruft expiration del alcance que procesa `git repack`. En Git 2.51.1, la ayuda corta expresa el contrato como `with --cruft, expire objects older than this`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack --cruft-expiration=2026-01-15 -ad
git count-objects -vH
```

El ejemplo usa `2026-01-15` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--combine-cruft-below-size`

Limita reorganizar objetos dentro de archivos pack al alcance identificado por combine cruft below size. En Git 2.51.1, la ayuda corta expresa el contrato como `with --cruft, only repack cruft packs smaller than this`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack --combine-cruft-below-size=5 -ad
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-cruft-size`

Establece un límite numérico para la selección o el recorrido.

```bash
git repack --max-cruft-size=5 -ad
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reuse-delta`

Desactiva el comportamiento `reuse-delta` para esta invocación.

```bash
git repack --no-reuse-delta -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reuse-object`

Desactiva el comportamiento `reuse-object` para esta invocación.

```bash
git repack --no-reuse-object -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-i` y `--delta-islands`

Activa delta islands durante reorganizar objetos dentro de archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pass --delta-islands to git-pack-objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--delta-islands`

```bash
git repack --delta-islands -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--unpack-unreachable`

Impide unpack unreachable durante esta invocación de `git repack`. En Git 2.51.1, la ayuda corta expresa el contrato como `with -A, do not loosen objects older than this`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack --unpack-unreachable=2026-01-15 -ad
git count-objects -vH
```

El ejemplo usa `2026-01-15` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-k` y `--keep-unreachable`

Activa conservar unreachable durante reorganizar objetos dentro de archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `with -a, repack unreachable objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--keep-unreachable`

```bash
git repack --keep-unreachable -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--window-memory`

Selecciona la relación indicada por window memory; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `same as the above, but limit memory size instead of entries count`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack --window-memory=valor -ad
git count-objects -vH
```

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

```bash
git repack --filter=valor -ad
git count-objects -vH
```

### `--pack-kept-objects`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git repack --pack-kept-objects -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-g` y `--geometric`

Activa geometric durante reorganizar objetos dentro de archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `find a geometric progression with factor <N>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--geometric`

```bash
git repack --geometric=5 -ad
git count-objects -vH
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--expire-to`

Aplica una fecha, duración o política de vencimiento.

```bash
git repack --expire-to=docs -ad
git count-objects -vH
```

El ejemplo usa `docs` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--filter-to`

Escribe o registra filtro to como parte de reorganizar objetos dentro de archivos pack. En Git 2.51.1, la ayuda corta expresa el contrato como `pack prefix to store a pack containing filtered out objects`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git repack --filter-to=docs -ad
git count-objects -vH
```

El ejemplo usa `docs` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-write-bitmap-index`

Desactiva para esta invocación el comportamiento que habilita `--write-bitmap-index`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git repack --no-write-bitmap-index -ad
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git replace`](../administration/replace.md)
- [`git reflog`](../administration/reflog.md)
- [`scalar`](../administration/scalar.md)

## Fuente

- [git-repack - Pack unpacked objects in a repository](https://git-scm.com/docs/git-repack)
