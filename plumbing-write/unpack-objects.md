---
title: "git unpack-objects"
source: "https://git-scm.com/docs/git-unpack-objects"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git unpack-objects`

Este caso usa `git unpack-objects` para extraer objetos de un flujo pack.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git unpack-objects < paquete.pack
```

La invocación `git unpack-objects < paquete.pack` ejecuta esta operación: extraer objetos de un flujo pack. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git unpack-objects [-n] [-q] [-r] [--strict]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git unpack-objects [-n] [-q] [-r] [--strict]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git unpack-objects -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-n`

Activa n durante extraer objetos de un flujo pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git unpack-objects -n < paquete.pack
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q`

Activa q durante extraer objetos de un flujo pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git unpack-objects -q < paquete.pack
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-r`

Activa r durante extraer objetos de un flujo pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git unpack-objects -r < paquete.pack
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--strict`

Activa strict durante extraer objetos de un flujo pack. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git unpack-objects --strict < paquete.pack
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git update-index`](../plumbing-write/update-index.md)
- [`git symbolic-ref`](../plumbing-write/symbolic-ref.md)
- [`git update-ref`](../plumbing-write/update-ref.md)

## Fuente

- [git-unpack-objects - Unpack objects from a packed archive](https://git-scm.com/docs/git-unpack-objects)
