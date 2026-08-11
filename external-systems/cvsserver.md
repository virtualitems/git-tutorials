---
title: "git cvsserver"
source: "https://git-scm.com/docs/git-cvsserver"
section: "external-systems"
---

# `git cvsserver`

## Ejemplo de partida

```bash
git config cvsserver.enabled true
CVS_SERVER='git cvsserver' cvs -d :ext:servidor/repo co modulo
```

Este caso usa `git cvsserver` para permitir que clientes CVS accedan a un repositorio Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: la ubicación y los nombres que deben traducirse desde el sistema de origen.
- Operación: permitir que clientes CVS accedan a un repositorio Git.
- Comprobación: el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Modelo mental

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Forma de referencia

```text
export CVS_SERVER="git cvsserver"
cvs -d :ext:user@server/path/repo.git co <HEAD_name>
```

Los elementos entre `<` y `>` se sustituyen por valores.

## Práctica

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

## Páginas relacionadas

- [`git fast-export`](../external-systems/fast-export.md)
- [`git cvsimport`](../external-systems/cvsimport.md)
- [`git fast-import`](../external-systems/fast-import.md)

## Fuente

- [git-cvsserver - A CVS server emulator for Git](https://git-scm.com/docs/git-cvsserver)
