---
title: "git cherry"
source: "https://git-scm.com/docs/git-cherry"
section: "plumbing-read"
---

# `git cherry`

## Ejemplo de partida

```bash
git cherry -v origin/main tema-portada
```

Este caso usa `git cherry` para detectar commits cuyo parche todavía no aparece en una rama base. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: detectar commits cuyo parche todavía no aparece en una rama base.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git cherry [-v] [<upstream> [<head> [<limit>]]]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git diff-files`](../plumbing-read/diff-files.md)
- [`git cat-file`](../plumbing-read/cat-file.md)
- [`git diff-index`](../plumbing-read/diff-index.md)

## Fuente

- [git-cherry - Find commits yet to be applied to upstream](https://git-scm.com/docs/git-cherry)
