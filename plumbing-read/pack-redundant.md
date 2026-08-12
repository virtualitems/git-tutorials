---
title: "git pack-redundant"
source: "https://git-scm.com/docs/git-pack-redundant"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git pack-redundant`

Este caso usa `git pack-redundant` para detectar packs cuyo contenido ya está cubierto por otros packs.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git pack-redundant --all
```

La invocación `git pack-redundant --all` ejecuta esta operación: detectar packs cuyo contenido ya está cubierto por otros packs. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git pack-redundant [--verbose] [--alt-odb] (--all | <pack-filename>…)
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git pack-redundant [--verbose] [--alt-odb] (--all | <pack-filename>...)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git pack-redundant -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--verbose`

Aumenta el detalle enviado a la salida.

```bash
git pack-redundant --verbose --all
printf 'exit=%s\n' "$?"
```

### `--alt-odb`

Activa alt odb durante detectar packs cuyo contenido ya está cubierto por otros packs. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git pack-redundant --alt-odb --all
printf 'exit=%s\n' "$?"
```

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git pack-redundant --all
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git repo`](../plumbing-read/repo.md)
- [`git name-rev`](../plumbing-read/name-rev.md)
- [`git rev-list`](../plumbing-read/rev-list.md)

## Fuente

- [git-pack-redundant - Find redundant pack files](https://git-scm.com/docs/git-pack-redundant)
