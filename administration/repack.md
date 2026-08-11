---
title: "git repack"
source: "https://git-scm.com/docs/git-repack"
section: "administration"
---

# `git repack`

## Ejemplo de partida

```bash
git count-objects -v
git repack -ad
git count-objects -v
```

Este caso usa `git repack` para reorganizar objetos dentro de archivos pack. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: reorganizar objetos dentro de archivos pack.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
git repack [-a] [-A] [-d] [-f] [-F] [-l] [-n] [-q] [-b] [-m]
	[--window=<n>] [--depth=<n>] [--threads=<n>] [--keep-pack=<pack-name>]
	[--write-midx[=<mode>]] [--name-hash-version=<n>] [--path-walk]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`git replace`](../administration/replace.md)
- [`git reflog`](../administration/reflog.md)
- [`scalar`](../administration/scalar.md)

## Fuente

- [git-repack - Pack unpacked objects in a repository](https://git-scm.com/docs/git-repack)
