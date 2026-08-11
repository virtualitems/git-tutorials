---
title: "git http-push"
source: "https://git-scm.com/docs/git-http-push"
section: "server-and-transport"
---

# `git http-push`

## Ejemplo de partida

```bash
git http-push --dry-run https://example.test/equipo/biblioteca.git refs/heads/main
```

Este caso usa `git http-push` para enviar objetos mediante HTTP con WebDAV. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Qué se deriva del ejemplo

- Entrada: la ruta del repositorio, el servicio y los parámetros de transporte.
- Operación: enviar objetos mediante HTTP con WebDAV.
- Comprobación: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Modelo mental

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Forma de referencia

```text
git http-push [--all] [--dry-run] [--force] [--verbose] <URL> <ref> [<ref>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Condición que debes comprobar

Este transporte usa HTTP con WebDAV y pertenece al flujo heredado. La guía explica su papel para interpretar sistemas existentes.

## Práctica

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

## Páginas relacionadas

- [`git receive-pack`](../server-and-transport/receive-pack.md)
- [`git http-fetch`](../server-and-transport/http-fetch.md)
- [`git send-pack`](../server-and-transport/send-pack.md)

## Fuente

- [git-http-push - Push objects over HTTP/DAV to another repository](https://git-scm.com/docs/git-http-push)
