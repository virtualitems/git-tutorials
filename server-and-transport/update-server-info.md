---
title: "git update-server-info"
source: "https://git-scm.com/docs/git-update-server-info"
section: "server-and-transport"
status: "source-audited"
version: "2.55.0"
---

# `git update-server-info`

Este caso usa `git update-server-info` para generar archivos auxiliares para clientes HTTP sin negociación. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git update-server-info
```

La invocación `git update-server-info` ejecuta esta operación: generar archivos auxiliares para clientes HTTP sin negociación. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Sintaxis y formas de invocación

```text
git update-server-info [-f | --force]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git update-server-info [-f | --force]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git update-server-info -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git update-server-info --force
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió.

## Páginas relacionadas

- [`git upload-archive`](../server-and-transport/upload-archive.md)
- [`git shell`](../server-and-transport/shell.md)
- [`git upload-pack`](../server-and-transport/upload-pack.md)

## Fuente

- [git-update-server-info - Update auxiliary info file to help dumb servers](https://git-scm.com/docs/git-update-server-info)
