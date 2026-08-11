---
title: "git clone"
source: "https://git-scm.com/docs/git-clone"
section: "getting-and-creating-projects"
---

# `git clone`

## Ejemplo de partida

```bash
git clone https://example.test/equipo/biblioteca.git
cd biblioteca
git status
```

Este caso usa `git clone` para crear un repositorio local a partir de otro repositorio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: un directorio, una URL o una selección de rutas.
- Operación: crear un repositorio local a partir de otro repositorio.
- Comprobación: el directorio resultante contiene el repositorio y, cuando corresponde, un área de trabajo.

## Modelo mental

Un repositorio contiene objetos y referencias. Un área de trabajo materializa un commit para que los archivos puedan editarse.

Separa los datos del repositorio de los archivos materializados. Un repositorio bare conserva objetos y referencias sin área de trabajo.

## Forma de referencia

```text
git clone [--template=<template-directory>]
	  [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror]
	  [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>]
	  [--dissociate] [--separate-git-dir <git-dir>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa un directorio temporal. Compara el contenido antes y después, incluidos `.git`, HEAD y las ramas disponibles.

## Páginas relacionadas

- [`git sparse-checkout`](../getting-and-creating-projects/sparse-checkout.md)
- [`git init`](../getting-and-creating-projects/init.md)

## Fuente

- [git-clone - Clone a repository into a new directory](https://git-scm.com/docs/git-clone)
