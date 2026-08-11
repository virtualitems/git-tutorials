---
title: "git"
source: "https://git-scm.com/docs/git"
section: "setup-and-config"
---

# `git`

## Ejemplo de partida

```bash
git -C ../biblioteca status
git -c color.ui=false log --oneline -3
```

Este caso usa `git` para invocar Git, elegir el repositorio y aplicar opciones globales. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el ámbito, la clave o el dato del entorno indicado por la orden.
- Operación: invocar Git, elegir el repositorio y aplicar opciones globales.
- Comprobación: una consulta posterior muestra el valor efectivo o la información generada.

## Modelo mental

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

## Forma de referencia

```text
git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
    [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
    [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--no-lazy-fetch]
    [--no-optional-locks] [--no-advice] [--bare] [--git-dir=<path>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Ejecuta el ejemplo en un repositorio temporal y usa `git config --show-origin --list` o el comando de consulta correspondiente para identificar el origen del resultado.

## Páginas relacionadas

- [`git config`](../setup-and-config/config.md)
- [`git bugreport`](../setup-and-config/bugreport.md)

## Fuente

- [git - the stupid content tracker](https://git-scm.com/docs/git)
