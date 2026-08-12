---
title: "git patch-id"
source: "https://git-scm.com/docs/git-patch-id"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git patch-id`

Este caso usa `git patch-id` para calcular una identidad estable para el contenido de un parche.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git show HEAD | git patch-id --stable
```

La invocación `git patch-id` ejecuta esta operación: calcular una identidad estable para el contenido de un parche. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git patch-id [--stable | --unstable | --verbatim]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git patch-id [--stable | --unstable | --verbatim]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git patch-id -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--stable`

Define stable para esta ejecución de `git patch-id`. En Git 2.51.1, la ayuda corta expresa el contrato como `use the stable patch-id algorithm`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción selecciona el procedimiento que `git patch-id` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git patch-id --stable
printf 'exit=%s\n' "$?"
```

### `--unstable`

Define unstable para esta ejecución de `git patch-id`. En Git 2.51.1, la ayuda corta expresa el contrato como `use the unstable patch-id algorithm`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción selecciona el procedimiento que `git patch-id` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git patch-id --unstable
printf 'exit=%s\n' "$?"
```

### `--verbatim`

Impide verbatim durante esta invocación de `git patch-id`. En Git 2.51.1, la ayuda corta expresa el contrato como `don't strip whitespace from the patch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git patch-id --verbatim
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git sh-i18n`](../scripting-and-helpers/sh-i18n.md)
- [`git merge-one-file`](../scripting-and-helpers/merge-one-file.md)
- [`git sh-setup`](../scripting-and-helpers/sh-setup.md)

## Fuente

- [git-patch-id - Compute unique IDs for patches](https://git-scm.com/docs/git-patch-id)
