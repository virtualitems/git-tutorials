---
title: "git cherry"
source: "https://git-scm.com/docs/git-cherry"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git cherry`

Este caso usa `git cherry` para detectar commits cuyo parche todavía no aparece en una rama base.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git cherry -v origin/main tema-portada
```

La invocación `git cherry -v origin/main tema-portada` ejecuta esta operación: detectar commits cuyo parche todavía no aparece en una rama base. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git cherry [-v] [<upstream> [<head> [<limit>]]]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git cherry [-v] [<upstream> [<head> [<limit>]]]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git cherry -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git cherry --verbose origin/main tema-portada
printf 'exit=%s\n' "$?"
```

### `--abbrev`

Reduce la representación visible del identificador sin cambiar el objeto.

```bash
git cherry --abbrev=5 -v origin/main tema-portada
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git diff-files`](../plumbing-read/diff-files.md)
- [`git cat-file`](../plumbing-read/cat-file.md)
- [`git diff-index`](../plumbing-read/diff-index.md)

## Fuente

- [git-cherry - Find commits yet to be applied to upstream](https://git-scm.com/docs/git-cherry)
