---
title: "git diff-pairs"
source: "https://git-scm.com/docs/git-diff-pairs"
section: "plumbing-read"
---

# `git diff-pairs`

## Ejemplo de partida

```bash
printf '%s\0%s\0' "$blob_a" "$blob_b" | git diff-pairs -z
```

Este caso usa `git diff-pairs` para comparar pares de blobs recibidos por la entrada estándar. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: comparar pares de blobs recibidos por la entrada estándar.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git diff-pairs -z [<diff-options>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git diff-tree`](../plumbing-read/diff-tree.md)
- [`git diff-index`](../plumbing-read/diff-index.md)
- [`git for-each-ref`](../plumbing-read/for-each-ref.md)

## Fuente

- [git-diff-pairs - Compare the content and mode of provided blob pairs](https://git-scm.com/docs/git-diff-pairs)
