---
title: "git history"
source: "https://git-scm.com/docs/git-history"
section: "branching-and-merging"
---

# `git history`

## Ejemplo de partida

```bash
git history reword HEAD~2 --dry-run
```

Este caso usa `git history` para reescribir commits con operaciones de corrección, mensaje o división. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las ramas, commits o rutas que participan en la operación.
- Operación: reescribir commits con operaciones de corrección, mensaje o división.
- Comprobación: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Modelo mental

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Forma de referencia

```text
git history fixup <commit> [--dry-run] [--update-refs=(branches|head)] [--reedit-message] [--empty=(drop|keep|abort)]
git history reword <commit> [--dry-run] [--update-refs=(branches|head)]
git history split <commit> [--dry-run] [--update-refs=(branches|head)] [--] [<pathspec>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Condición que debes comprobar

La documentación marca este comando como experimental. Usa `--dry-run` y conserva una referencia al historial anterior.

## Práctica

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

## Páginas relacionadas

- [`git merge`](../branching-and-merging/merge.md)
- [`git checkout`](../branching-and-merging/checkout.md)
- [`git mergetool`](../branching-and-merging/mergetool.md)

## Fuente

- [git-history - EXPERIMENTAL: Rewrite history](https://git-scm.com/docs/git-history)
