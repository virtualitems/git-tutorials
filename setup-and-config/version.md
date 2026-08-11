---
title: "git version"
source: "https://git-scm.com/docs/git-version"
section: "setup-and-config"
---

# `git version`

## Ejemplo de partida

```bash
git version
git version --build-options
```

Este caso usa `git version` para mostrar la versión de Git y datos del proceso de compilación. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el ámbito, la clave o el dato del entorno indicado por la orden.
- Operación: mostrar la versión de Git y datos del proceso de compilación.
- Comprobación: una consulta posterior muestra el valor efectivo o la información generada.

## Modelo mental

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

## Forma de referencia

```text
git version [--build-options]
```

Los corchetes delimitan partes opcionales.

## Práctica

Ejecuta el ejemplo en un repositorio temporal y usa `git config --show-origin --list` o el comando de consulta correspondiente para identificar el origen del resultado.

## Páginas relacionadas

- [`git help`](../setup-and-config/help.md)
- [`git diagnose`](../setup-and-config/diagnose.md)

## Fuente

- [git-version - Display version information about Git](https://git-scm.com/docs/git-version)
