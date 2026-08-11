---
title: "git repo"
source: "https://git-scm.com/docs/git-repo"
section: "plumbing-read"
---

# `git repo`

## Ejemplo de partida

```bash
git repo info --all
git repo structure
```

Este caso usa `git repo` para consultar propiedades y estructura del repositorio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: consultar propiedades y estructura del repositorio.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git repo info [--format=(lines|nul) | -z] [--all | <key>…]
git repo info --keys [--format=(lines|nul) | -z]
git repo structure [--format=(table|lines|nul) | -z]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Condición que debes comprobar

Comprueba la disponibilidad de este comando en la versión instalada antes de incorporarlo a un script.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git rev-list`](../plumbing-read/rev-list.md)
- [`git pack-redundant`](../plumbing-read/pack-redundant.md)
- [`git rev-parse`](../plumbing-read/rev-parse.md)

## Fuente

- [git-repo - Retrieve information about the repository](https://git-scm.com/docs/git-repo)
