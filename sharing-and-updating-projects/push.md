---
title: "git push"
source: "https://git-scm.com/docs/git-push"
section: "sharing-and-updating-projects"
---

# `git push`

## Ejemplo de partida

```bash
git push -u origin tema-portada
```

Este caso usa `git push` para actualizar referencias de un repositorio remoto y enviar sus objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el repositorio, las referencias y el sentido de la transferencia.
- Operación: actualizar referencias de un repositorio remoto y enviar sus objetos.
- Comprobación: las referencias locales y remotas permiten separar descarga, integración y publicación.

## Modelo mental

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Forma de referencia

```text
git push [--all | --branches | --mirror | --tags] [--follow-tags] [--atomic] [-n | --dry-run] [--receive-pack=<git-receive-pack>]
	 [--repo=<repository>] [-f | --force] [-d | --delete] [--prune] [-q | --quiet] [-v | --verbose]
	 [-u | --set-upstream] [-o <string> | --push-option=<string>]
	 [--[no-]signed | --signed=(true|false|if-asked)]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

## Páginas relacionadas

- [`git remote`](../sharing-and-updating-projects/remote.md)
- [`git pull`](../sharing-and-updating-projects/pull.md)
- [`git request-pull`](../sharing-and-updating-projects/request-pull.md)

## Fuente

- [git-push - Update remote refs along with associated objects](https://git-scm.com/docs/git-push)
