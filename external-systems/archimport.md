---
title: "git archimport"
source: "https://git-scm.com/docs/git-archimport"
section: "external-systems"
---

# `git archimport`

## Ejemplo de partida

```bash
git archimport archivo/linea:main
```

Este caso usa `git archimport` para importar un repositorio de GNU Arch. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: la ubicación y los nombres que deben traducirse desde el sistema de origen.
- Operación: importar un repositorio de GNU Arch.
- Comprobación: el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Modelo mental

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Forma de referencia

```text
git archimport [-h] [-v] [-o] [-a] [-f] [-T] [-D <depth>] [-t <tempdir>]
	       <archive>/<branch>[:<git-branch>]…
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

## Páginas relacionadas

- [`git cvsexportcommit`](../external-systems/cvsexportcommit.md)
- [`git cvsimport`](../external-systems/cvsimport.md)

## Fuente

- [git-archimport - Import a GNU Arch repository into Git](https://git-scm.com/docs/git-archimport)
