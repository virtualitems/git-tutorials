---
title: "git bugreport"
source: "https://git-scm.com/docs/git-bugreport"
section: "setup-and-config"
---

# `git bugreport`

## Ejemplo de partida

```bash
mkdir diagnostico
git bugreport --output-directory diagnostico
```

Este caso usa `git bugreport` para reunir información para informar un problema de Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el ámbito, la clave o el dato del entorno indicado por la orden.
- Operación: reunir información para informar un problema de Git.
- Comprobación: una consulta posterior muestra el valor efectivo o la información generada.

## Modelo mental

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

## Forma de referencia

```text
git bugreport [(-o | --output-directory) <path>]
		[(-s | --suffix) <format> | --no-suffix]
		[--diagnose[=<mode>]]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Ejecuta el ejemplo en un repositorio temporal y usa `git config --show-origin --list` o el comando de consulta correspondiente para identificar el origen del resultado.

## Páginas relacionadas

- [`git diagnose`](../setup-and-config/diagnose.md)
- [`git config`](../setup-and-config/config.md)
- [`git help`](../setup-and-config/help.md)

## Fuente

- [git-bugreport - Collect information for user to file a bug report](https://git-scm.com/docs/git-bugreport)
