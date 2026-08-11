---
title: "git svn"
source: "https://git-scm.com/docs/git-svn"
section: "external-systems"
---

# `git svn`

## Ejemplo de partida

```bash
git svn clone https://example.test/svn/biblioteca/trunk biblioteca
```

Este caso usa `git svn` para usar un repositorio Subversion desde un repositorio Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: la ubicación y los nombres que deben traducirse desde el sistema de origen.
- Operación: usar un repositorio Subversion desde un repositorio Git.
- Comprobación: el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Modelo mental

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Forma de referencia

```text
git svn <command> [<options>] [<arguments>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

## Páginas relacionadas

- [`git quiltimport`](../external-systems/quiltimport.md)
- [`git p4`](../external-systems/p4.md)

## Fuente

- [git-svn - Bidirectional operation between a Subversion repository and Git](https://git-scm.com/docs/git-svn)
