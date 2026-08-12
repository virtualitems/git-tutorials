---
title: "git count-objects"
source: "https://git-scm.com/docs/git-count-objects"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `git count-objects`

Este caso usa `git count-objects` para medir objetos sueltos, packs y espacio ocupado.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git count-objects -v -H
```

La invocación `git count-objects -v -H` ejecuta esta operación: medir objetos sueltos, packs y espacio ocupado. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
git count-objects [-v] [-H | --human-readable]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git count-objects [-v] [-H | --human-readable]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git count-objects -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git count-objects --verbose -H
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `-H` y `--human-readable`

Incluye human readable en la salida o cambia cómo `git count-objects` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print sizes in human readable format`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--human-readable`

```bash
git count-objects --human-readable -v
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

## Páginas relacionadas

- [`git filter-branch`](../administration/filter-branch.md)
- [`git clean`](../administration/clean.md)
- [`git fsck`](../administration/fsck.md)

## Fuente

- [git-count-objects - Count unpacked number of objects and their disk consumption](https://git-scm.com/docs/git-count-objects)
