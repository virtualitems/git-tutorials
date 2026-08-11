---
title: "git sparse-checkout"
source: "https://git-scm.com/docs/git-sparse-checkout"
section: "getting-and-creating-projects"
---

# `git sparse-checkout`

## Ejemplo de partida

```bash
git sparse-checkout init --cone
git sparse-checkout set app docs
```

Este caso usa `git sparse-checkout` para materializar solo una parte de los archivos seguidos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: un directorio, una URL o una selección de rutas.
- Operación: materializar solo una parte de los archivos seguidos.
- Comprobación: el directorio resultante contiene el repositorio y, cuando corresponde, un área de trabajo.

## Modelo mental

Un repositorio contiene objetos y referencias. Un área de trabajo materializa un commit para que los archivos puedan editarse.

Separa los datos del repositorio de los archivos materializados. Un repositorio bare conserva objetos y referencias sin área de trabajo.

## Forma de referencia

```text
git sparse-checkout (init | list | set | add | reapply | disable | check-rules | clean) [<options>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Usa un directorio temporal. Compara el contenido antes y después, incluidos `.git`, HEAD y las ramas disponibles.

## Páginas relacionadas

- [`git clone`](../getting-and-creating-projects/clone.md)
- [`git init`](../getting-and-creating-projects/init.md)

## Fuente

- [git-sparse-checkout - Reduce your working tree to a subset of tracked files](https://git-scm.com/docs/git-sparse-checkout)
