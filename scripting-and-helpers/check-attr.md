---
title: "git check-attr"
source: "https://git-scm.com/docs/git-check-attr"
section: "scripting-and-helpers"
---

# `git check-attr`

## Ejemplo de partida

```bash
git check-attr diff text -- informe.bin
```

Este caso usa `git check-attr` para consultar los atributos que se aplican a una ruta. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: consultar los atributos que se aplican a una ruta.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git check-attr [--source <tree-ish>] [-a | --all | <attr>…] [--] <pathname>…
git check-attr --stdin [-z] [--source <tree-ish>] [-a | --all | <attr>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git check-ignore`](../scripting-and-helpers/check-ignore.md)
- [`git check-mailmap`](../scripting-and-helpers/check-mailmap.md)

## Fuente

- [git-check-attr - Display gitattributes information](https://git-scm.com/docs/git-check-attr)
