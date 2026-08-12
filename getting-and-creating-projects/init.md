---
title: "git init"
source: "https://git-scm.com/docs/git-init"
section: "getting-and-creating-projects"
status: "source-audited"
version: "2.55.0"
---

# `git init`

Este caso usa `git init` para crear un repositorio vacío o reinicializar uno existente.

## Laboratorio base

Crea este repositorio una vez. Las demás guías enlazan este apartado y continúan desde el commit `base`.

```bash
lab_dir="$(mktemp -d)"
git init "$lab_dir/proyecto"
git -C "$lab_dir/proyecto" config user.name "Persona de prueba"
git -C "$lab_dir/proyecto" config user.email "user@example.com"
printf 'línea base\n' > "$lab_dir/proyecto/archivo.txt"
git -C "$lab_dir/proyecto" add archivo.txt
git -C "$lab_dir/proyecto" commit -m "base"
cd "$lab_dir/proyecto"
```

`mktemp -d` crea una ruta que puedes eliminar cuando termines. `git init` crea el directorio Git. Las dos órdenes `git config` guardan nombre y correo solo dentro de este repositorio. `git add` copia `archivo.txt` al índice y `git commit` registra el estado que usarán los ejemplos posteriores. Comprueba el punto de partida con `git status --short`; una salida vacía indica que el área de trabajo y el índice coinciden con `HEAD`.

## Cómo funciona

Un repositorio contiene objetos y referencias. Un área de trabajo materializa un commit para que los archivos puedan editarse.

Separa los datos del repositorio de los archivos materializados. Un repositorio bare conserva objetos y referencias sin área de trabajo.

## Ejemplo mínimo

```bash
mkdir biblioteca
cd biblioteca
git init -b main
git status
```

La invocación `git init -b main` ejecuta esta operación: crear un repositorio vacío o reinicializar uno existente. Después, el directorio resultante contiene el repositorio y, cuando corresponde, un área de trabajo.

## Sintaxis y formas de invocación

```text
git init [-q | --quiet] [--bare] [--template=<template-directory>]
	 [--separate-git-dir <git-dir>] [--object-format=<format>]
	 [--ref-format=<format>]
	 [-b <branch-name> | --initial-branch=<branch-name>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git init [-q | --quiet] [--bare] [--template=<template-directory>]
                [--separate-git-dir <git-dir>] [--object-format=<format>]
                [--ref-format=<format>]
                [-b <branch-name> | --initial-branch=<branch-name>]
                [--shared[=<permissions>]] [<directory>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git init -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git init --quiet "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

 La salida identifica el directorio que almacena el repositorio recién creado.

### `--bare`

Opera sin un área de trabajo asociada.

```bash
git init --bare "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

 La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--template`

Usa el directorio indicado como fuente de plantillas para crear archivos iniciales dentro del nuevo repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `directory from which templates will be used`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
mkdir -p "$lab_dir/plantillas"
printf 'plantilla del laboratorio\n' > "$lab_dir/plantillas/description"
git init --template="$lab_dir/plantillas" "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

El ejemplo usa `../plantillas` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--separate-git-dir`

Guarda los datos del repositorio en otra ruta y deja en el área de trabajo un archivo que apunta a esa ubicación. En Git 2.51.1, la ayuda corta expresa el contrato como `separate git dir from working tree`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git init --separate-git-dir="$lab_dir/datos-git" "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

El ejemplo usa `../datos-git` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--object-format`

Selecciona el algoritmo de hash con el que el repositorio identifica objetos nuevos. En Git 2.51.1, la ayuda corta expresa el contrato como `specify the hash algorithm to use`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git init --object-format=sha256 "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

El ejemplo usa `sha256` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ref-format`

Selecciona el formato de almacenamiento de referencias que usará el repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `specify the reference format to use`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git init --ref-format=reftable "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

El ejemplo usa `reftable` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-b` y `--initial-branch`

Selecciona o modifica referencias dentro del alcance de la orden.

#### Ejemplo con `--initial-branch`

```bash
git init --initial-branch=main "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

En esta forma, `main` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida identifica el directorio que almacena el repositorio recién creado.

### `--shared`

Ajusta permisos y configuración para que varios usuarios del sistema operativo puedan escribir el repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `specify that the git repository is to be shared amongst several users`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git init --shared=group "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

El ejemplo usa `group` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git clone`](../getting-and-creating-projects/clone.md)
- [`git sparse-checkout`](../getting-and-creating-projects/sparse-checkout.md)

## Fuente

- [git-init - Create an empty Git repository or reinitialize an existing one](https://git-scm.com/docs/git-init)
