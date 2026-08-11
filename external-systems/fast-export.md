---
title: "git fast-export"
source: "https://git-scm.com/docs/git-fast-export"
section: "external-systems"
---

# `git fast-export`

## Ejemplo de partida

```bash
git fast-export --all > historial.fi
```

Este caso usa `git fast-export` para emitir historial y referencias en un flujo para migración. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: la ubicación y los nombres que deben traducirse desde el sistema de origen.
- Operación: emitir historial y referencias en un flujo para migración.
- Comprobación: el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Modelo mental

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Forma de referencia

```text
git fast-export [<options>] | git fast-import
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

## Páginas relacionadas

- [`git fast-import`](../external-systems/fast-import.md)
- [`git cvsserver`](../external-systems/cvsserver.md)
- [`git p4`](../external-systems/p4.md)

## Fuente

- [git-fast-export - Git data exporter](https://git-scm.com/docs/git-fast-export)
