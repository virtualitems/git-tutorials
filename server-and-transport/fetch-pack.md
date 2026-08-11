---
title: "git fetch-pack"
source: "https://git-scm.com/docs/git-fetch-pack"
section: "server-and-transport"
---

# `git fetch-pack`

## Ejemplo de partida

```bash
git fetch-pack https://example.test/equipo/biblioteca.git refs/heads/main
```

Este caso usa `git fetch-pack` para solicitar a otro repositorio los objetos que faltan. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Qué se deriva del ejemplo

- Entrada: la ruta del repositorio, el servicio y los parámetros de transporte.
- Operación: solicitar a otro repositorio los objetos que faltan.
- Comprobación: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Modelo mental

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Forma de referencia

```text
git fetch-pack [--all] [--quiet|-q] [--keep|-k] [--thin] [--include-tag]
	[--upload-pack=<git-upload-pack>]
	[--depth=<n>] [--no-progress]
	[-v] <repository> [<refs>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

## Páginas relacionadas

- [`git http-backend`](../server-and-transport/http-backend.md)
- [`git daemon`](../server-and-transport/daemon.md)
- [`git http-fetch`](../server-and-transport/http-fetch.md)

## Fuente

- [git-fetch-pack - Receive missing objects from another repository](https://git-scm.com/docs/git-fetch-pack)
