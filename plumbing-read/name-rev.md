---
title: "git name-rev"
source: "https://git-scm.com/docs/git-name-rev"
section: "plumbing-read"
---

# `git name-rev`

## Ejemplo de partida

```bash
git name-rev --name-only HEAD~3
```

Este caso usa `git name-rev` para expresar identificadores mediante nombres relativos a referencias. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: expresar identificadores mediante nombres relativos a referencias.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git name-rev [--tags] [--refs=<pattern>]
	       ( --all | --annotate-stdin | <commit-ish>… )
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git pack-redundant`](../plumbing-read/pack-redundant.md)
- [`git merge-base`](../plumbing-read/merge-base.md)
- [`git repo`](../plumbing-read/repo.md)

## Fuente

- [git-name-rev - Find symbolic names for given revs](https://git-scm.com/docs/git-name-rev)
