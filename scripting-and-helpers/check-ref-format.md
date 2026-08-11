---
title: "git check-ref-format"
source: "https://git-scm.com/docs/git-check-ref-format"
section: "scripting-and-helpers"
---

# `git check-ref-format`

## Ejemplo de partida

```bash
git check-ref-format 'refs/heads/tema-portada'
```

Este caso usa `git check-ref-format` para validar la sintaxis de un nombre de referencia. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: validar la sintaxis de un nombre de referencia.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git check-ref-format [--normalize]
       [--[no-]allow-onelevel] [--refspec-pattern]
       <refname>
git check-ref-format --branch <branchname-shorthand>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git column`](../scripting-and-helpers/column.md)
- [`git check-mailmap`](../scripting-and-helpers/check-mailmap.md)
- [`git credential`](../scripting-and-helpers/credential.md)

## Fuente

- [git-check-ref-format - Ensures that a reference name is well formed](https://git-scm.com/docs/git-check-ref-format)
