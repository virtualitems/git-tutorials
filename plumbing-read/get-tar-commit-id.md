---
title: "git get-tar-commit-id"
source: "https://git-scm.com/docs/git-get-tar-commit-id"
section: "plumbing-read"
---

# `git get-tar-commit-id`

## Ejemplo de partida

```bash
git archive HEAD | git get-tar-commit-id
```

Este caso usa `git get-tar-commit-id` para extraer el identificador incluido por git archive en un tar. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: extraer el identificador incluido por git archive en un tar.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git get-tar-commit-id
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git ls-files`](../plumbing-read/ls-files.md)
- [`git format-rev`](../plumbing-read/format-rev.md)
- [`git ls-tree`](../plumbing-read/ls-tree.md)

## Fuente

- [git-get-tar-commit-id - Extract commit ID from an archive created using git-archive](https://git-scm.com/docs/git-get-tar-commit-id)
