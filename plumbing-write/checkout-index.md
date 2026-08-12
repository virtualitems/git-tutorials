---
title: "git checkout-index"
source: "https://git-scm.com/docs/git-checkout-index"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git checkout-index`

Este caso usa `git checkout-index` para copiar archivos del índice al área de trabajo.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
mkdir exportado
git checkout-index --all --prefix=exportado/
```

La invocación `git checkout-index --all --prefix=exportado/` ejecuta esta operación: copiar archivos del índice al área de trabajo. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git checkout-index [-u] [-q] [-a] [-f] [-n] [--prefix=<string>]
		   [--stage=<number>|all]
		   [--temp]
		   [--ignore-skip-worktree-bits]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git checkout-index [<options>] [--] [<file>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git checkout-index -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-u` y `--index`

Incluye el índice en la operación.

#### Ejemplo con `--index`

```bash
git checkout-index --index --all --prefix=exportado/
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git checkout-index --quiet --all --prefix=exportado/
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `-a` y `--all`

Amplía la selección a todos los elementos del alcance definido.

#### Ejemplo con `--all`

```bash
git checkout-index --all --prefix=exportado/
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git checkout-index --force --all --prefix=exportado/
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `-n`

Crea n como parte de copiar archivos del índice al área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `don't checkout new files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git checkout-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout-index -n --all --prefix=exportado/
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--prefix`

Antepone prefix al valor que produce `git checkout-index`. En Git 2.51.1, la ayuda corta expresa el contrato como `when creating files, prepend <string>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git checkout-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout-index --prefix=valor --all
git fsck --no-progress
```

### `--stage`

Activa stage durante copiar archivos del índice al área de trabajo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `copy out the files from named stage`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git checkout-index --stage=valor --all --prefix=exportado/
git fsck --no-progress
```

### `--temp`

Escribe o registra temp como parte de copiar archivos del índice al área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `write the content to temporary files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git checkout-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout-index --temp --all --prefix=exportado/
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-skip-worktree-bits`

Excluye elementos que cumplan la condición indicada.

Esta forma se usa cuando `git checkout-index` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque ignorar omitir el elemento actual área de trabajo bits actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git checkout-index --ignore-skip-worktree-bits --all --prefix=exportado/
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--create`

Permite crear o escribir el elemento seleccionado.

```bash
git checkout-index --create --all --prefix=exportado/
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git checkout-index -z --all --prefix=exportado/
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git checkout-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout-index --stdin --all --prefix=exportado/
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git commit-graph`](../plumbing-write/commit-graph.md)
- [`git commit-tree`](../plumbing-write/commit-tree.md)

## Fuente

- [git-checkout-index - Copy files from the index to the working tree](https://git-scm.com/docs/git-checkout-index)
