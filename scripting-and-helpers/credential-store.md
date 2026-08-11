---
title: "git credential-store"
source: "https://git-scm.com/docs/git-credential-store"
section: "scripting-and-helpers"
---

# `git credential-store`

## Ejemplo de partida

```bash
git config --global credential.helper store
```

Este caso usa `git credential-store` para guardar credenciales sin cifrado en un archivo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: guardar credenciales sin cifrado en un archivo.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git config credential.helper 'store [<options>]'
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Condición que debes comprobar

Este ayudante guarda credenciales sin cifrado. Restringe los permisos del archivo y úsalo solo cuando ese riesgo sea aceptable.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git fmt-merge-msg`](../scripting-and-helpers/fmt-merge-msg.md)
- [`git credential-cache`](../scripting-and-helpers/credential-cache.md)
- [`git hook`](../scripting-and-helpers/hook.md)

## Fuente

- [git-credential-store - Helper to store credentials on disk](https://git-scm.com/docs/git-credential-store)
