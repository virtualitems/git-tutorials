---
title: "git merge-one-file"
source: "https://git-scm.com/docs/git-merge-one-file"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git merge-one-file`

Este caso usa `git merge-one-file` para resolver una ruta durante una fusión de tres vías.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git merge-index git-merge-one-file -a
```

La invocación `git merge-one-file` ejecuta esta operación: resolver una ruta durante una fusión de tres vías. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git merge-one-file
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git merge-one-file <orig blob> <our blob> <their blob> <path> <orig mode> <our mode> <their mode>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git merge-one-file -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-h`

Activa h durante resolver una ruta durante una fusión de tres vías. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git merge-one-file -h
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git patch-id`](../scripting-and-helpers/patch-id.md)
- [`git mailsplit`](../scripting-and-helpers/mailsplit.md)
- [`git sh-i18n`](../scripting-and-helpers/sh-i18n.md)

## Fuente

- [git-merge-one-file - The standard helper program to use with git-merge-index](https://git-scm.com/docs/git-merge-one-file)
