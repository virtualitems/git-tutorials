---
title: "scalar"
source: "https://git-scm.com/docs/scalar"
section: "administration"
---

# `scalar`

## Ejemplo de partida

```bash
scalar clone https://example.test/equipo/biblioteca.git biblioteca
scalar list
```

Este caso usa `scalar` para administrar repositorios con funciones orientadas a conjuntos de archivos extensos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: administrar repositorios con funciones orientadas a conjuntos de archivos extensos.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
scalar clone [--single-branch] [--branch <main-branch>] [--full-clone]
	[--[no-]src] [--[no-]tags] [--[no-]maintenance] <url> [<enlistment>]
scalar list
scalar register [--[no-]maintenance] [<enlistment>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`git replace`](../administration/replace.md)
- [`git repack`](../administration/repack.md)

## Fuente

- [scalar - A tool for managing large Git repositories](https://git-scm.com/docs/scalar)
