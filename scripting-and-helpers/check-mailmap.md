---
title: "git check-mailmap"
source: "https://git-scm.com/docs/git-check-mailmap"
section: "scripting-and-helpers"
---

# `git check-mailmap`

## Ejemplo de partida

```bash
git check-mailmap 'Ana <ana@correo-antiguo.test>'
```

Este caso usa `git check-mailmap` para convertir identidades mediante las reglas de mailmap. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: convertir identidades mediante las reglas de mailmap.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git check-mailmap [<options>] <contact>…
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git check-ref-format`](../scripting-and-helpers/check-ref-format.md)
- [`git check-ignore`](../scripting-and-helpers/check-ignore.md)
- [`git column`](../scripting-and-helpers/column.md)

## Fuente

- [git-check-mailmap - Show canonical names and email addresses of contacts](https://git-scm.com/docs/git-check-mailmap)
