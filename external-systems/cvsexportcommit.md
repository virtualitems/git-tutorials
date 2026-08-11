---
title: "git cvsexportcommit"
source: "https://git-scm.com/docs/git-cvsexportcommit"
section: "external-systems"
---

# `git cvsexportcommit`

## Ejemplo de partida

```bash
git cvsexportcommit -w /tmp/checkout-cvs HEAD
```

Este caso usa `git cvsexportcommit` para aplicar un commit de Git sobre un checkout de CVS. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: la ubicación y los nombres que deben traducirse desde el sistema de origen.
- Operación: aplicar un commit de Git sobre un checkout de CVS.
- Comprobación: el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Modelo mental

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Forma de referencia

```text
git cvsexportcommit [-h] [-u] [-v] [-c] [-P] [-p] [-a] [-d <cvsroot>]
	[-w <cvs-workdir>] [-W] [-f] [-m <msgprefix>] [<parent-commit>] <commit-id>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

## Páginas relacionadas

- [`git cvsimport`](../external-systems/cvsimport.md)
- [`git archimport`](../external-systems/archimport.md)
- [`git cvsserver`](../external-systems/cvsserver.md)

## Fuente

- [git-cvsexportcommit - Export a single commit to a CVS checkout](https://git-scm.com/docs/git-cvsexportcommit)
