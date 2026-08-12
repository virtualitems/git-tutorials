---
title: "git rev-parse"
source: "https://git-scm.com/docs/git-rev-parse"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git rev-parse`

Este caso usa `git rev-parse` para resolver revisiones y separar opciones para scripts.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git rev-parse --show-toplevel
git rev-parse HEAD^{tree}
```

La invocación `git rev-parse --show-toplevel` ejecuta esta operación: resolver revisiones y separar opciones para scripts. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git rev-parse [<options>] <arg>…
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git rev-parse --parseopt [<options>] -- [<args>...]
   or: git rev-parse --sq-quote [<arg>...]
   or: git rev-parse [<options>] [<arg>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git rev-parse -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--parseopt`

Activa parseopt durante resolver revisiones y separar opciones para scripts. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git rev-parse --parseopt --show-toplevel
printf 'exit=%s\n' "$?"
```

### `--sq-quote`

Activa sq quote durante resolver revisiones y separar opciones para scripts. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git rev-parse --sq-quote --show-toplevel
printf 'exit=%s\n' "$?"
```

### `-h`

Muestra ayuda corta cuando la orden admite esta convención.

```bash
git rev-parse -h
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git show-index`](../plumbing-read/show-index.md)
- [`git rev-list`](../plumbing-read/rev-list.md)
- [`git show-ref`](../plumbing-read/show-ref.md)

## Fuente

- [git-rev-parse - Pick out and massage parameters](https://git-scm.com/docs/git-rev-parse)
