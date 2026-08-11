---
title: "git unpack-file"
source: "https://git-scm.com/docs/git-unpack-file"
section: "plumbing-read"
---

# `git unpack-file`

## Ejemplo de partida

```bash
blob=$(git rev-parse HEAD:README.md)
temporal=$(git unpack-file "$blob")
printf '%s\n' "$temporal"
```

Este caso usa `git unpack-file` para crear un archivo temporal con el contenido de un blob. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: crear un archivo temporal con el contenido de un blob.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git unpack-file <blob>
```

Los elementos entre `<` y `>` se sustituyen por valores.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git var`](../plumbing-read/var.md)
- [`git show-ref`](../plumbing-read/show-ref.md)
- [`git verify-pack`](../plumbing-read/verify-pack.md)

## Fuente

- [git-unpack-file - Creates a temporary file with a blob’s contents](https://git-scm.com/docs/git-unpack-file)
