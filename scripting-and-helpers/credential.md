---
title: "git credential"
source: "https://git-scm.com/docs/git-credential"
section: "scripting-and-helpers"
---

# `git credential`

## Ejemplo de partida

```bash
printf 'protocol=https\nhost=example.test\n\n' | git credential fill
```

Este caso usa `git credential` para intercambiar credenciales con los ayudantes configurados. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: intercambiar credenciales con los ayudantes configurados.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
'git credential' (fill|approve|reject|capability)
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git credential-cache`](../scripting-and-helpers/credential-cache.md)
- [`git column`](../scripting-and-helpers/column.md)
- [`git credential-store`](../scripting-and-helpers/credential-store.md)

## Fuente

- [git-credential - Retrieve and store user credentials](https://git-scm.com/docs/git-credential)
