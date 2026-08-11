---
title: "git check-ignore"
source: "https://git-scm.com/docs/git-check-ignore"
section: "scripting-and-helpers"
---

# `git check-ignore`

## Ejemplo de partida

```bash
git check-ignore -v build/salida.log
```

Este caso usa `git check-ignore` para explicar qué regla de exclusión afecta a una ruta. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: explicar qué regla de exclusión afecta a una ruta.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git check-ignore [<options>] <pathname>…
git check-ignore [<options>] --stdin
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git check-mailmap`](../scripting-and-helpers/check-mailmap.md)
- [`git check-attr`](../scripting-and-helpers/check-attr.md)
- [`git check-ref-format`](../scripting-and-helpers/check-ref-format.md)

## Fuente

- [git-check-ignore - Debug gitignore / exclude files](https://git-scm.com/docs/git-check-ignore)
