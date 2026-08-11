---
title: "git diagnose"
source: "https://git-scm.com/docs/git-diagnose"
section: "setup-and-config"
---

# `git diagnose`

## Ejemplo de partida

```bash
mkdir diagnostico
git diagnose --mode=stats --output-directory=diagnostico
```

Este caso usa `git diagnose` para generar un archivo con datos de diagnóstico del repositorio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el ámbito, la clave o el dato del entorno indicado por la orden.
- Operación: generar un archivo con datos de diagnóstico del repositorio.
- Comprobación: una consulta posterior muestra el valor efectivo o la información generada.

## Modelo mental

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

## Forma de referencia

```text
git diagnose [(-o | --output-directory) <path>] [(-s | --suffix) <format>]
	       [--mode=<mode>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Ejecuta el ejemplo en un repositorio temporal y usa `git config --show-origin --list` o el comando de consulta correspondiente para identificar el origen del resultado.

## Páginas relacionadas

- [`git help`](../setup-and-config/help.md)
- [`git bugreport`](../setup-and-config/bugreport.md)
- [`git version`](../setup-and-config/version.md)

## Fuente

- [git-diagnose - Generate a zip archive of diagnostic information](https://git-scm.com/docs/git-diagnose)
