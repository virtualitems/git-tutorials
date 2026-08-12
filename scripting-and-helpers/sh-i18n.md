---
title: "git sh-i18n"
source: "https://git-scm.com/docs/git-sh-i18n"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git sh-i18n`

Este caso usa `git sh-i18n` para cargar funciones de internacionalización en scripts de shell.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
. "$(git --exec-path)/git-sh-i18n"
eval_gettext 'Procesando $archivo'
```

La invocación `git sh-i18n` ejecuta esta operación: cargar funciones de internacionalización en scripts de shell. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
. "$(git --exec-path)/git-sh-i18n"
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git sh-i18n -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--exec-path`

Activa exec ruta durante cargar funciones de internacionalización en scripts de shell. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git sh-i18n --exec-path
printf 'exit=%s\n' "$?"
```

### `--help`

Muestra la ayuda correspondiente a la versión instalada.

```bash
git sh-i18n --help
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git sh-setup`](../scripting-and-helpers/sh-setup.md)
- [`git patch-id`](../scripting-and-helpers/patch-id.md)
- [`git stripspace`](../scripting-and-helpers/stripspace.md)

## Fuente

- [git-sh-i18n - Git’s i18n setup code for shell scripts](https://git-scm.com/docs/git-sh-i18n)
