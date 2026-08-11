---
title: "git url-parse"
source: "https://git-scm.com/docs/git-url-parse"
section: "scripting-and-helpers"
---

# `git url-parse`

## Ejemplo de partida

```bash
git url-parse -c host https://example.test/equipo/biblioteca.git
```

Este caso usa `git url-parse` para extraer componentes de una URL aceptada por Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: extraer componentes de una URL aceptada por Git.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git url-parse [-c <component>] [--] <url>…
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Condición que debes comprobar

Comprueba la disponibilidad de este comando en la versión instalada antes de incorporarlo a un script.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git stripspace`](../scripting-and-helpers/stripspace.md)
- [`git sh-setup`](../scripting-and-helpers/sh-setup.md)

## Fuente

- [git-url-parse - Parse and extract git URL components](https://git-scm.com/docs/git-url-parse)
