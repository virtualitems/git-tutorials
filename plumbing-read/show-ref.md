---
title: "git show-ref"
source: "https://git-scm.com/docs/git-show-ref"
section: "plumbing-read"
---

# `git show-ref`

## Ejemplo de partida

```bash
git show-ref --heads --tags
git show-ref --verify refs/heads/main
```

Este caso usa `git show-ref` para enumerar o comprobar referencias del repositorio local. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: enumerar o comprobar referencias del repositorio local.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git show-ref [--head] [-d | --dereference]
	     [-s | --hash[=<n>]] [--abbrev[=<n>]] [--branches] [--tags]
	     [--] [<pattern>…]
git show-ref --verify [-q | --quiet] [-d | --dereference]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git unpack-file`](../plumbing-read/unpack-file.md)
- [`git show-index`](../plumbing-read/show-index.md)
- [`git var`](../plumbing-read/var.md)

## Fuente

- [git-show-ref - List references in a local repository](https://git-scm.com/docs/git-show-ref)
