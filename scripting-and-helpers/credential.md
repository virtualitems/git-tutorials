---
title: "git credential"
source: "https://git-scm.com/docs/git-credential"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git credential`

Este caso usa `git credential` para intercambiar credenciales con los ayudantes configurados.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
printf 'protocol=https\nhost=example.com\n\n' | git credential fill
```

La invocación `git credential` ejecuta esta operación: intercambiar credenciales con los ayudantes configurados. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
'git credential' (fill|approve|reject|capability)
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git credential (fill|approve|reject)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git credential -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-h`

Activa h durante intercambiar credenciales con los ayudantes configurados. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git credential -h
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git credential-cache`](../scripting-and-helpers/credential-cache.md)
- [`git column`](../scripting-and-helpers/column.md)
- [`git credential-store`](../scripting-and-helpers/credential-store.md)

## Fuente

- [git-credential - Retrieve and store user credentials](https://git-scm.com/docs/git-credential)
