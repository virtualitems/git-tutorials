---
title: "git multi-pack-index"
source: "https://git-scm.com/docs/git-multi-pack-index"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git multi-pack-index`

Este caso usa `git multi-pack-index` para administrar un índice que cubre varios archivos pack.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git multi-pack-index write
git multi-pack-index verify
```

La invocación `git multi-pack-index write` ejecuta esta operación: administrar un índice que cubre varios archivos pack. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git multi-pack-index [<options>] write [--preferred-pack=<pack>]
		         [--[no-]bitmap] [--[no-]incremental] [--[no-]stdin-packs]
		         [--refs-snapshot=<path>] [--[no-]write-chain-file]
			 [--base=<checksum>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git multi-pack-index [<options>] write [--preferred-pack=<pack>][--refs-snapshot=<path>]
   or: git multi-pack-index [<options>] verify
   or: git multi-pack-index [<options>] expire
   or: git multi-pack-index [<options>] repack [--batch-size=<size>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git multi-pack-index -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--preferred-pack`

Activa preferred pack durante administrar un índice que cubre varios archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git multi-pack-index --preferred-pack write
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--bitmap`

Activa bitmap durante administrar un índice que cubre varios archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git multi-pack-index --bitmap write
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--incremental`

Activa incremental durante administrar un índice que cubre varios archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git multi-pack-index --incremental write
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin-packs`

Activa entrada estándar packs durante administrar un índice que cubre varios archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git multi-pack-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git multi-pack-index --stdin-packs write
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--refs-snapshot`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git multi-pack-index --refs-snapshot write
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--write-chain-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia cómo `git multi-pack-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git multi-pack-index --write-chain-file write
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--base`

Activa base durante administrar un índice que cubre varios archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git multi-pack-index --base write
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--batch-size`

Activa batch size durante administrar un índice que cubre varios archivos pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git multi-pack-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git multi-pack-index --batch-size write
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--object-dir`

Selecciona la representación o tratamiento de identificadores de objeto.

La opción cambia cómo `git multi-pack-index` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git multi-pack-index --object-dir=docs write
git fsck --no-progress
```

El ejemplo usa `docs` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git pack-objects`](../plumbing-write/pack-objects.md)
- [`git mktree`](../plumbing-write/mktree.md)
- [`git prune-packed`](../plumbing-write/prune-packed.md)

## Fuente

- [git-multi-pack-index - Write and verify multi-pack-indexes](https://git-scm.com/docs/git-multi-pack-index)
