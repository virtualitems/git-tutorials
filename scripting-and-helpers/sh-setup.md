---
title: "git sh-setup"
source: "https://git-scm.com/docs/git-sh-setup"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git sh-setup`

Este caso usa `git sh-setup` para cargar funciones comunes para scripts de shell de Git.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
. "$(git --exec-path)/git-sh-setup"
require_work_tree
```

La invocación `git sh-setup` ejecuta esta operación: cargar funciones comunes para scripts de shell de Git. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
. "$(git --exec-path)/git-sh-setup"
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git sh-setup -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--exec-path`

Activa exec ruta durante cargar funciones comunes para scripts de shell de Git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git sh-setup --exec-path
printf 'exit=%s\n' "$?"
```

### `--help`

Muestra la ayuda correspondiente a la versión instalada.

```bash
git sh-setup --help
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git stripspace`](../scripting-and-helpers/stripspace.md)
- [`git sh-i18n`](../scripting-and-helpers/sh-i18n.md)
- [`git url-parse`](../scripting-and-helpers/url-parse.md)

## Fuente

- [git-sh-setup - Common Git shell script setup code](https://git-scm.com/docs/git-sh-setup)
