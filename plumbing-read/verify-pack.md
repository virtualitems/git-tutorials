---
title: "git verify-pack"
source: "https://git-scm.com/docs/git-verify-pack"
section: "plumbing-read"
---

# `git verify-pack`

## Ejemplo de partida

```bash
git verify-pack -v .git/objects/pack/pack-ejemplo.idx
```

Este caso usa `git verify-pack` para comprobar un pack mediante su archivo de índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: comprobar un pack mediante su archivo de índice.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git verify-pack [-v | --verbose] [-s | --stat-only] [--] <pack>.idx...
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git var`](../plumbing-read/var.md)
- [`git unpack-file`](../plumbing-read/unpack-file.md)

## Fuente

- [git-verify-pack - Validate packed Git archive files](https://git-scm.com/docs/git-verify-pack)
