---
title: "git commit-graph"
source: "https://git-scm.com/docs/git-commit-graph"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git commit-graph`

Este caso usa `git commit-graph` para escribir y verificar el archivo que acelera recorridos de commits.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git commit-graph write --reachable
git commit-graph verify
```

La invocación `git commit-graph write --reachable` ejecuta esta operación: escribir y verificar el archivo que acelera recorridos de commits. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git commit-graph verify [--object-dir <dir>] [--shallow] [--[no-]progress]
git commit-graph write [--object-dir <dir>] [--append]
			[--split[=<strategy>]] [--reachable | --stdin-packs | --stdin-commits]
			[--changed-paths] [--[no-]max-new-filters <n>] [--[no-]progress]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git commit-graph verify [--object-dir <dir>] [--shallow] [--[no-]progress]
   or: git commit-graph write [--object-dir <dir>] [--append]
                              [--split[=<strategy>]] [--reachable | --stdin-packs | --stdin-commits]
                              [--changed-paths] [--[no-]max-new-filters <n>] [--[no-]progress]
                              <split-options>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git commit-graph -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--object-dir`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git commit-graph --object-dir=docs write --reachable
git fsck --no-progress
```

El ejemplo usa `docs` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow`

Activa historial shallow durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git commit-graph --shallow write --reachable
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git commit-graph --progress write --reachable
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--append`

Activa append durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git commit-graph --append write --reachable
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--split`

Activa split durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git commit-graph --split write --reachable
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reachable`

Activa reachable durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git commit-graph --reachable write
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin-packs`

Activa entrada estándar packs durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git commit-graph` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit-graph --stdin-packs write --reachable
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin-commits`

Activa entrada estándar commits durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git commit-graph` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git commit-graph --stdin-commits write --reachable
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--changed-paths`

Activa changed paths durante escribir y verificar el archivo que acelera recorridos de commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git commit-graph --changed-paths write --reachable
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-new-filters`

Establece un límite numérico para la selección o el recorrido.

```bash
git commit-graph --max-new-filters write --reachable
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git commit-tree`](../plumbing-write/commit-tree.md)
- [`git checkout-index`](../plumbing-write/checkout-index.md)
- [`git hash-object`](../plumbing-write/hash-object.md)

## Fuente

- [git-commit-graph - Write and verify Git commit-graph files](https://git-scm.com/docs/git-commit-graph)
