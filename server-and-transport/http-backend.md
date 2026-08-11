---
title: "git http-backend"
source: "https://git-scm.com/docs/git-http-backend"
section: "server-and-transport"
---

# `git http-backend`

## Ejemplo de partida

```bash
GIT_PROJECT_ROOT=/srv/git GIT_HTTP_EXPORT_ALL=1 git http-backend
```

Este caso usa `git http-backend` para atender operaciones Git del lado servidor sobre HTTP. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Qué se deriva del ejemplo

- Entrada: la ruta del repositorio, el servicio y los parámetros de transporte.
- Operación: atender operaciones Git del lado servidor sobre HTTP.
- Comprobación: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Modelo mental

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Forma de referencia

```text
git http-backend
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

## Páginas relacionadas

- [`git http-fetch`](../server-and-transport/http-fetch.md)
- [`git fetch-pack`](../server-and-transport/fetch-pack.md)
- [`git http-push`](../server-and-transport/http-push.md)

## Fuente

- [git-http-backend - Server side implementation of Git over HTTP](https://git-scm.com/docs/git-http-backend)
