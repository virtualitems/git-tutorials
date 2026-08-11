---
title: "git init"
source: "https://git-scm.com/docs/git-init"
section: "getting-and-creating-projects"
---

# `git init`

## Ejemplo de partida

```bash
mkdir biblioteca
cd biblioteca
git init -b main
git status
```

Este caso usa `git init` para crear un repositorio vacío o reinicializar uno existente. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: un directorio, una URL o una selección de rutas.
- Operación: crear un repositorio vacío o reinicializar uno existente.
- Comprobación: el directorio resultante contiene el repositorio y, cuando corresponde, un área de trabajo.

## Modelo mental

Un repositorio contiene objetos y referencias. Un área de trabajo materializa un commit para que los archivos puedan editarse.

Separa los datos del repositorio de los archivos materializados. Un repositorio bare conserva objetos y referencias sin área de trabajo.

## Forma de referencia

```text
git init [-q | --quiet] [--bare] [--template=<template-directory>]
	 [--separate-git-dir <git-dir>] [--object-format=<format>]
	 [--ref-format=<format>]
	 [-b <branch-name> | --initial-branch=<branch-name>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa un directorio temporal. Compara el contenido antes y después, incluidos `.git`, HEAD y las ramas disponibles.

## Páginas relacionadas

- [`git clone`](../getting-and-creating-projects/clone.md)
- [`git sparse-checkout`](../getting-and-creating-projects/sparse-checkout.md)

## Fuente

- [git-init - Create an empty Git repository or reinitialize an existing one](https://git-scm.com/docs/git-init)
