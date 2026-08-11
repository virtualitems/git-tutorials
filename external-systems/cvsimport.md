---
title: "git cvsimport"
source: "https://git-scm.com/docs/git-cvsimport"
section: "external-systems"
---

# `git cvsimport`

## Ejemplo de partida

```bash
git cvsimport -C biblioteca -r cvs modulo
```

Este caso usa `git cvsimport` para importar historial desde CVS. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: la ubicación y los nombres que deben traducirse desde el sistema de origen.
- Operación: importar historial desde CVS.
- Comprobación: el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Modelo mental

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Forma de referencia

```text
git cvsimport [-o <branch-for-HEAD>] [-h] [-v] [-d <CVSROOT>]
	      [-A <author-conv-file>] [-p <options-for-cvsps>] [-P <file>]
	      [-C <git-repository>] [-z <fuzz>] [-i] [-k] [-u] [-s <subst>]
	      [-a] [-m] [-M <regex>] [-S <regex>] [-L <commit-limit>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

## Páginas relacionadas

- [`git cvsserver`](../external-systems/cvsserver.md)
- [`git cvsexportcommit`](../external-systems/cvsexportcommit.md)
- [`git fast-export`](../external-systems/fast-export.md)

## Fuente

- [git-cvsimport - Salvage your data out of another SCM people love to hate](https://git-scm.com/docs/git-cvsimport)
