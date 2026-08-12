---
title: "git show-index"
source: "https://git-scm.com/docs/git-show-index"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git show-index`

Este caso usa `git show-index` para leer la tabla de objetos de un índice de pack.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git show-index < .git/objects/pack/pack-ejemplo.idx
```

La invocación `git show-index < .git/objects/pack/pack-ejemplo.idx` ejecuta esta operación: leer la tabla de objetos de un índice de pack. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git show-index [--object-format=<hash-algorithm>] < <pack-idx-file>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git show-index [--object-format=<hash-algorithm>] < <pack-idx-file>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git show-index -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--object-format`

Selecciona el algoritmo de hash con el que el repositorio identifica objetos nuevos. En Git 2.51.1, la ayuda corta expresa el contrato como `specify the hash algorithm to use`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git show-index --object-format=sha256 < .git/objects/pack/pack-ejemplo.idx
printf 'exit=%s\n' "$?"
```

El ejemplo usa `sha256` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git show-ref`](../plumbing-read/show-ref.md)
- [`git rev-parse`](../plumbing-read/rev-parse.md)
- [`git unpack-file`](../plumbing-read/unpack-file.md)

## Fuente

- [git-show-index - Show packed archive index](https://git-scm.com/docs/git-show-index)
