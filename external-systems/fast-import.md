---
title: "git fast-import"
source: "https://git-scm.com/docs/git-fast-import"
section: "external-systems"
---

# `git fast-import`

## Ejemplo de partida

```bash
git init destino
cd destino
git fast-import < ../historial.fi
```

Este caso usa `git fast-import` para crear historial y referencias a partir de un flujo de importación. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: la ubicación y los nombres que deben traducirse desde el sistema de origen.
- Operación: crear historial y referencias a partir de un flujo de importación.
- Comprobación: el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Modelo mental

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Forma de referencia

```text
frontend | git fast-import [<options>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

## Páginas relacionadas

- [`git p4`](../external-systems/p4.md)
- [`git fast-export`](../external-systems/fast-export.md)
- [`git quiltimport`](../external-systems/quiltimport.md)

## Fuente

- [git-fast-import - Backend for fast Git data importers](https://git-scm.com/docs/git-fast-import)
