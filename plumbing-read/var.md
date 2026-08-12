---
title: "git var"
source: "https://git-scm.com/docs/git-var"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git var`

Este caso usa `git var` para mostrar variables lógicas calculadas por Git.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git var GIT_AUTHOR_IDENT
git var -l
```

La invocación `git var GIT_AUTHOR_IDENT` ejecuta esta operación: mostrar variables lógicas calculadas por Git. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git var (-l | <variable>)
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git var (-l | <variable>)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git var -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-l`

Activa l durante mostrar variables lógicas calculadas por Git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git var -l GIT_AUTHOR_IDENT
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git verify-pack`](../plumbing-read/verify-pack.md)
- [`git unpack-file`](../plumbing-read/unpack-file.md)
- [`git show-ref`](../plumbing-read/show-ref.md)

## Fuente

- [git-var - Show a Git logical variable](https://git-scm.com/docs/git-var)
