---
title: "git http-fetch"
source: "https://git-scm.com/docs/git-http-fetch"
section: "server-and-transport"
---

# `git http-fetch`

## Ejemplo de partida

```bash
git http-fetch HEAD https://example.test/equipo/biblioteca.git
```

Este caso usa `git http-fetch` para descargar objetos mediante el transporte HTTP heredado. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Qué se deriva del ejemplo

- Entrada: la ruta del repositorio, el servicio y los parámetros de transporte.
- Operación: descargar objetos mediante el transporte HTTP heredado.
- Comprobación: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Modelo mental

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Forma de referencia

```text
git http-fetch [-c] [-t] [-a] [-d] [-v] [-w <filename>] [--recover] [--stdin | --packfile=<hash> | <commit>] <URL>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

## Páginas relacionadas

- [`git http-push`](../server-and-transport/http-push.md)
- [`git http-backend`](../server-and-transport/http-backend.md)
- [`git receive-pack`](../server-and-transport/receive-pack.md)

## Fuente

- [git-http-fetch - Download from a remote Git repository via HTTP](https://git-scm.com/docs/git-http-fetch)
