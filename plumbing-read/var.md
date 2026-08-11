---
title: "git var"
source: "https://git-scm.com/docs/git-var"
section: "plumbing-read"
---

# `git var`

## Ejemplo de partida

```bash
git var GIT_AUTHOR_IDENT
git var -l
```

Este caso usa `git var` para mostrar variables lógicas calculadas por Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: mostrar variables lógicas calculadas por Git.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git var (-l | <variable>)
```

Los elementos entre `<` y `>` se sustituyen por valores.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git verify-pack`](../plumbing-read/verify-pack.md)
- [`git unpack-file`](../plumbing-read/unpack-file.md)
- [`git show-ref`](../plumbing-read/show-ref.md)

## Fuente

- [git-var - Show a Git logical variable](https://git-scm.com/docs/git-var)
