---
title: "git update-index"
source: "https://git-scm.com/docs/git-update-index"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git update-index`

Este caso usa `git update-index` para modificar directamente entradas y bits del índice.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git update-index --assume-unchanged config.local
git ls-files -v config.local
```

La invocación `git update-index --assume-unchanged config.local` ejecuta esta operación: modificar directamente entradas y bits del índice. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git update-index
	     [--add] [--remove | --force-remove] [--replace]
	     [--refresh] [-q] [--unmerged] [--ignore-missing]
	     [(--cacheinfo <mode>,<object>,<file>)…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git update-index [<options>] [--] [<file>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git update-index -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--add`

Permite crear o escribir el elemento seleccionado.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --add --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--remove`

Retira elementos según las condiciones de la orden.

```bash
git update-index --remove --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-remove`

Retira elementos según las condiciones de la orden.

```bash
git update-index --force-remove --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--replace`

Activa replace durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `let files replace directories and vice-versa`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --replace --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--refresh`

Actualiza metadatos de comprobación sin copiar contenido nuevo al índice.

```bash
git update-index --refresh --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q`

Actualiza q como parte de modificar directamente entradas y bits del índice. En Git 2.51.1, la ayuda corta expresa el contrato como `continue refresh even when index needs update`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git update-index` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque q actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git update-index -q --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unmerged`

Activa unmerged durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `refresh even if index contains unmerged entries`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git update-index --unmerged --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-missing`

Permite comprobar rutas ausentes bajo las condiciones que define la orden.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --ignore-missing --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cacheinfo`

Incluye cacheinfo en la entrada, el resultado o el registro que construye `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `add the specified entry to the index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git update-index --cacheinfo=all --assume-unchanged config.local
git fsck --no-progress
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-submodules`

Excluye elementos que cumplan la condición indicada.

```bash
git update-index --ignore-submodules --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--really-refresh`

Ignora really refresh dentro del alcance que procesa `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `like --refresh, but ignore assume-unchanged setting`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git update-index --really-refresh --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--chmod`

Cambia el bit ejecutable registrado en el índice, no el permiso del archivo en disco.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --chmod=valor --assume-unchanged config.local
git fsck --no-progress
```

### `--assume-unchanged`

Activa assume unchanged durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `mark files as "not changing"`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-assume-unchanged`

Desactiva el comportamiento `assume-unchanged` para esta invocación.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --no-assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--skip-worktree`

Limita modificar directamente entradas y bits del índice al alcance identificado por omitir el elemento actual área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `mark files as "index-only"`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git update-index` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque omitir el elemento actual área de trabajo actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git update-index --skip-worktree --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-skip-worktree-entries`

Excluye elementos que cumplan la condición indicada.

Esta forma se usa cuando `git update-index` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque ignorar omitir el elemento actual área de trabajo entries actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git update-index --ignore-skip-worktree-entries --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--info-only`

Incluye info only en la entrada, el resultado o el registro que construye `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `add to index only; do not add content to object database`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git update-index --info-only --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index -z --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --stdin --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index-info`

Incluye índice info en la entrada, el resultado o el registro que construye `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `add entries from standard input to the index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --index-info --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unresolve`

Activa unresolve durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `repopulate stages #2 and #3 for the listed paths`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git update-index --unresolve --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-g` y `--again`

Actualiza again como parte de modificar directamente entradas y bits del índice. En Git 2.51.1, la ayuda corta expresa el contrato como `only update entries that differ from HEAD`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--again`

```bash
git update-index --again --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `--verbose`

Aumenta el detalle enviado a la salida.

```bash
git update-index --verbose --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--clear-resolve-undo`

Activa clear resolución undo durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `(for porcelains) forget saved unresolved conflicts`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git update-index --clear-resolve-undo --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index-version`

Escribe o registra índice versión como parte de modificar directamente entradas y bits del índice. En Git 2.51.1, la ayuda corta expresa el contrato como `write index in this format`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git update-index --index-version=5 --assume-unchanged config.local
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--show-index-version`

Incluye información adicional en la salida.

```bash
git update-index --show-index-version --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--split-index`

Impide split índice durante esta invocación de `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `enable or disable split index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git update-index --split-index --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--untracked-cache`

Impide untracked cache durante esta invocación de `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `enable/disable untracked cache`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git update-index --untracked-cache --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--test-untracked-cache`

Activa test untracked cache durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `test if the filesystem supports untracked cache`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --test-untracked-cache --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-untracked-cache`

Omite una protección concreta de la orden; requiere verificar origen y destino.

```bash
git update-index --force-untracked-cache --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-write-index`

Permite crear o escribir el elemento seleccionado.

```bash
git update-index --force-write-index --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--fsmonitor`

Impide fsmonitor durante esta invocación de `git update-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `enable or disable file system monitor`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --fsmonitor --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--fsmonitor-valid`

Activa fsmonitor valid durante modificar directamente entradas y bits del índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `mark files as fsmonitor valid`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git update-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-index --fsmonitor-valid --assume-unchanged config.local
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git update-ref`](../plumbing-write/update-ref.md)
- [`git unpack-objects`](../plumbing-write/unpack-objects.md)
- [`git write-tree`](../plumbing-write/write-tree.md)

## Fuente

- [git-update-index - Register file contents in the working tree to the index](https://git-scm.com/docs/git-update-index)
