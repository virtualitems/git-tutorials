---
title: "git maintenance"
source: "https://git-scm.com/docs/git-maintenance"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `git maintenance`

Este caso usa `git maintenance` para ejecutar o programar tareas de mantenimiento del repositorio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git maintenance run --task=commit-graph
git maintenance run --task=gc
```

La invocación `git maintenance run --task=commit-graph` ejecuta esta operación: ejecutar o programar tareas de mantenimiento del repositorio. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
git maintenance run [<options>]
git maintenance start [--scheduler=<scheduler>]
git maintenance (stop|register|unregister) [<options>]
git maintenance is-needed [<options>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git maintenance <subcommand> [<options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git maintenance -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--scheduler`

Activa scheduler durante ejecutar o programar tareas de mantenimiento del repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git maintenance --scheduler run --task=commit-graph
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git pack-refs`](../administration/pack-refs.md)
- [`git gc`](../administration/gc.md)
- [`git prune`](../administration/prune.md)

## Fuente

- [git-maintenance - Run tasks to optimize Git repository data](https://git-scm.com/docs/git-maintenance)
