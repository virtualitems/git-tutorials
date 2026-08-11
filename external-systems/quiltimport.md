---
title: "git quiltimport"
source: "https://git-scm.com/docs/git-quiltimport"
section: "external-systems"
---

# `git quiltimport`

## Ejemplo de partida

```bash
git quiltimport --patches parches
```

Este caso usa `git quiltimport` para importar una serie de parches administrada por quilt. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: la ubicación y los nombres que deben traducirse desde el sistema de origen.
- Operación: importar una serie de parches administrada por quilt.
- Comprobación: el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Modelo mental

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Forma de referencia

```text
git quiltimport [--dry-run | -n] [--author <author>] [--patches <dir>]
		[--series <file>] [--keep-non-patch]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

## Páginas relacionadas

- [`git svn`](../external-systems/svn.md)
- [`git p4`](../external-systems/p4.md)
- [`git fast-import`](../external-systems/fast-import.md)

## Fuente

- [git-quiltimport - Applies a quilt patchset onto the current branch](https://git-scm.com/docs/git-quiltimport)
