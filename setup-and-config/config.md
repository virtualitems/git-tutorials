---
title: "git config"
source: "https://git-scm.com/docs/git-config"
section: "setup-and-config"
---

# `git config`

## Ejemplo de partida

```bash
git config --global user.name "Ana Torres"
git config --global user.email ana@example.test
git config --get user.name
```

Este caso usa `git config` para leer y cambiar opciones de configuración por ámbito. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el ámbito, la clave o el dato del entorno indicado por la orden.
- Operación: leer y cambiar opciones de configuración por ámbito.
- Comprobación: una consulta posterior muestra el valor efectivo o la información generada.

## Modelo mental

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

## Forma de referencia

```text
git config list [<file-option>] [<display-option>] [--includes]
git config get [<file-option>] [<display-option>] [--includes] [--all] [--regexp] [--value=<pattern>] [--fixed-value] [--default=<default>] [--url=<url>] <name>
git config set [<file-option>] [--type=<type>] [--all] [--value=<pattern>] [--fixed-value] <name> <value>
git config unset [<file-option>] [--all] [--value=<pattern>] [--fixed-value] <name>
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Ejecuta el ejemplo en un repositorio temporal y usa `git config --show-origin --list` o el comando de consulta correspondiente para identificar el origen del resultado.

## Páginas relacionadas

- [`git bugreport`](../setup-and-config/bugreport.md)
- [`git`](../setup-and-config/git.md)
- [`git diagnose`](../setup-and-config/diagnose.md)

## Fuente

- [git-config - Get and set repository or global options](https://git-scm.com/docs/git-config)
