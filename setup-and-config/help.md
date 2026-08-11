---
title: "git help"
source: "https://git-scm.com/docs/git-help"
section: "setup-and-config"
---

# `git help`

## Ejemplo de partida

```bash
git help rebase
git help revisions
```

Este caso usa `git help` para abrir la ayuda de un comando o concepto. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el ámbito, la clave o el dato del entorno indicado por la orden.
- Operación: abrir la ayuda de un comando o concepto.
- Comprobación: una consulta posterior muestra el valor efectivo o la información generada.

## Modelo mental

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

## Forma de referencia

```text
git help [-a|--all] [--[no-]verbose] [--[no-]external-commands] [--[no-]aliases]
git help [[-i|--info] [-m|--man] [-w|--web]] [<command>|<doc>]
git help [-g|--guides]
git help [-c|--config]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Ejecuta el ejemplo en un repositorio temporal y usa `git config --show-origin --list` o el comando de consulta correspondiente para identificar el origen del resultado.

## Páginas relacionadas

- [`git version`](../setup-and-config/version.md)
- [`git diagnose`](../setup-and-config/diagnose.md)
- [`git bugreport`](../setup-and-config/bugreport.md)

## Fuente

- [git-help - Display help information about Git](https://git-scm.com/docs/git-help)
