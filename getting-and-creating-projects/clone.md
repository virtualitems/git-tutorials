---
title: "git clone"
source: "https://git-scm.com/docs/git-clone"
section: "getting-and-creating-projects"
status: "source-audited"
version: "2.55.0"
---

# `git clone`

Este caso usa `git clone` para crear un repositorio local a partir de otro repositorio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un repositorio contiene objetos y referencias. Un área de trabajo materializa un commit para que los archivos puedan editarse.

Separa los datos del repositorio de los archivos materializados. Un repositorio bare conserva objetos y referencias sin área de trabajo.

## Ejemplo mínimo

```bash
git clone https://example.com/equipo/biblioteca.git
cd biblioteca
git status
```

La invocación `git clone https://example.com/equipo/biblioteca.git` ejecuta esta operación: crear un repositorio local a partir de otro repositorio. Después, el directorio resultante contiene el repositorio y, cuando corresponde, un área de trabajo.

## Sintaxis y formas de invocación

```text
git clone [--template=<template-directory>]
	  [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror]
	  [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>]
	  [--dissociate] [--separate-git-dir <git-dir>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git clone [<options>] [--] <repo> [<dir>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git clone -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--template`

Usa el directorio indicado como fuente de plantillas para crear archivos iniciales dentro del nuevo repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `directory from which templates will be used`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --template=../plantillas https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `../plantillas` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-l` y `--local`

Opera sobre la configuración del repositorio.

#### Ejemplo con `--local`

```bash
git clone --local https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `-s` y `--shared`

Ajusta permisos y configuración para que varios usuarios del sistema operativo puedan escribir el repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `setup as shared repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--shared`

```bash
git clone --shared https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--no-hardlinks`

Desactiva el comportamiento `hardlinks` para esta invocación.

```bash
git clone --no-hardlinks https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git clone --quiet https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `-n`

Crea n como parte de crear un repositorio local a partir de otro repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `don't create a checkout`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone -n https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--bare`

Opera sin un área de trabajo asociada.

```bash
git clone --bare https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--mirror`

Crea espejo como parte de crear un repositorio local a partir de otro repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `create a mirror repository (implies --bare)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --mirror https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `-o` y `--origin`

Define origin para esta ejecución de `git clone`. En Git 2.51.1, la ayuda corta expresa el contrato como `use <name> instead of 'origin' to track upstream`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--origin`

```bash
git clone --origin=tema https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `tema` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-b` y `--branch`

Selecciona o modifica referencias dentro del alcance de la orden.

#### Ejemplo con `--branch`

```bash
git clone --branch=main https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `main` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-u` y `--upload-pack`

Define upload pack con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `path to git-upload-pack on the remote`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--upload-pack`

```bash
git clone --upload-pack=archivo.txt https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `archivo.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--reference`

Activa reference durante crear un repositorio local a partir de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `reference repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --reference=valor https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--dissociate`

Limita crear un repositorio local a partir de otro repositorio al alcance identificado por dissociate. En Git 2.51.1, la ayuda corta expresa el contrato como `use --reference only while cloning`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --dissociate https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--separate-git-dir`

Guarda los datos del repositorio en otra ruta y deja en el área de trabajo un archivo que apunta a esa ubicación. En Git 2.51.1, la ayuda corta expresa el contrato como `separate git dir from working tree`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --separate-git-dir=../datos-git https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `../datos-git` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git clone --verbose https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git clone --progress https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--reject-shallow`

Impide rechazos historial shallow durante esta invocación de `git clone`.

```bash
git clone --reject-shallow https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--no-checkout`

Desactiva el comportamiento `checkout` para esta invocación.

```bash
git clone --no-checkout https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--checkout`

Selecciona la relación indicada por checkout; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-checkout`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --checkout https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--hardlinks`

Selecciona la relación indicada por hardlinks; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-hardlinks`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --hardlinks https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

```bash
git clone --recurse-submodules=archivo.txt https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recursive`

Extiende la operación de forma recursiva al ámbito documentado.

```bash
git clone --recursive=archivo.txt https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-j` y `--jobs`

Define cuántas tareas puede ejecutar Git en paralelo para la operación. En Git 2.51.1, la ayuda corta expresa el contrato como `number of submodules cloned in parallel`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--jobs`

```bash
git clone --jobs=5 https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--reference-if-able`

Activa reference if able durante crear un repositorio local a partir de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `reference repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --reference-if-able=valor https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--revision`

Comprueba revision antes de aceptar el resultado de `git clone`.

```bash
git clone --revision=valor https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--depth`

Establece un límite numérico para la selección o el recorrido.

```bash
git clone --depth=2 https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `2` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow-since`

Crea historial shallow desde una fecha como parte de crear un repositorio local a partir de otro repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `create a shallow clone since a specific time`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --shallow-since=2026-01-15T10:00:00Z https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `2026-01-15T10:00:00Z` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow-exclude`

Excluye elementos que cumplan la condición indicada.

```bash
git clone --shallow-exclude=refs/heads/main https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `refs/heads/main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--single-branch`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git clone --single-branch https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--tags`

Incluye o selecciona etiquetas según la operación.

```bash
git clone --tags https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--shallow-submodules`

Activa historial shallow submódulos durante crear un repositorio local a partir de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `any cloned submodules will be shallow`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --shallow-submodules https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--ref-format`

Selecciona el formato de almacenamiento de referencias que usará el repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `specify the reference format to use`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --ref-format=reftable https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `reftable` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-c` y `--config`

Define config para esta ejecución de `git clone`. En Git 2.51.1, la ayuda corta expresa el contrato como `set config inside the new repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--config`

```bash
git clone --config=user.name https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--server-option`

Activa server option durante crear un repositorio local a partir de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `option to transmit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --server-option=valor https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `-4` y `--ipv4`

Limita crear un repositorio local a partir de otro repositorio al alcance identificado por ipv4. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv4 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--ipv4`

```bash
git clone --ipv4 https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `-6` y `--ipv6`

Limita crear un repositorio local a partir de otro repositorio al alcance identificado por ipv6. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv6 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--ipv6`

```bash
git clone --ipv6 https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--filter`

Limita los objetos transferidos mediante una especificación de filtro de clon parcial. En Git 2.51.1, la ayuda corta expresa el contrato como `object filtering`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --filter=valor https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--also-filter-submodules`

Activa also filtro submódulos durante crear un repositorio local a partir de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `apply partial clone filters to submodules`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --also-filter-submodules https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--remote-submodules`

Define remote submódulos para esta ejecución de `git clone`. En Git 2.51.1, la ayuda corta expresa el contrato como `any cloned submodules will use their remote-tracking branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --remote-submodules https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--sparse`

Permite operar sobre entradas que quedan fuera de la selección sparse activa.

```bash
git clone --sparse https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--bundle-uri`

Activa bundle uri durante crear un repositorio local a partir de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `a URI for downloading bundles before fetching from origin remote`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git clone --bundle-uri=valor https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--no-reject-shallow`

Desactiva para esta invocación el comportamiento que habilita `--reject-shallow`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git clone --no-reject-shallow https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--no-local`

Desactiva para esta invocación el comportamiento que habilita `--local`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git clone --no-local https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--no-single-branch`

Desactiva para esta invocación el comportamiento que habilita `--single-branch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git clone --no-single-branch https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--no-tags`

Desactiva para esta invocación el comportamiento que habilita `--tags`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git clone --no-tags https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--no-shallow-submodules`

Desactiva para esta invocación el comportamiento que habilita `--shallow-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git clone --no-shallow-submodules https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

### `--no-remote-submodules`

Desactiva para esta invocación el comportamiento que habilita `--remote-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git clone --no-remote-submodules https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git sparse-checkout`](../getting-and-creating-projects/sparse-checkout.md)
- [`git init`](../getting-and-creating-projects/init.md)

## Fuente

- [git-clone - Clone a repository into a new directory](https://git-scm.com/docs/git-clone)
