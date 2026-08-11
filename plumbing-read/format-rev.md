---
title: "git format-rev"
source: "https://git-scm.com/docs/git-format-rev"
section: "plumbing-read"
---

# `git format-rev`

## Ejemplo de partida

```bash
printf '%s\n' HEAD~2 HEAD~1 HEAD | git format-rev --stdin-mode=single --format='%h %s'
```

Este caso usa `git format-rev` para formatear revisiones recibidas por la entrada estándar. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: formatear revisiones recibidas por la entrada estándar.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
(EXPERIMENTAL!) git format-rev --stdin-mode=<mode> --format=<pretty> [--[no-]notes=<ref>] [-z] [--[no-]null-output] [--[no-]null-input]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Condición que debes comprobar

La documentación marca este comando como experimental. No bases un formato persistente en su salida sin fijar la versión de Git.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git get-tar-commit-id`](../plumbing-read/get-tar-commit-id.md)
- [`git for-each-repo`](../plumbing-read/for-each-repo.md)
- [`git ls-files`](../plumbing-read/ls-files.md)

## Fuente

- [git-format-rev - EXPERIMENTAL: Pretty format revisions on demand](https://git-scm.com/docs/git-format-rev)
