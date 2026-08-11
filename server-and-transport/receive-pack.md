---
title: "git receive-pack"
source: "https://git-scm.com/docs/git-receive-pack"
section: "server-and-transport"
---

# `git receive-pack`

## Ejemplo de partida

```bash
git receive-pack /srv/git/biblioteca.git
```

Este caso usa `git receive-pack` para recibir objetos y solicitudes de actualización de referencias. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Qué se deriva del ejemplo

- Entrada: la ruta del repositorio, el servicio y los parámetros de transporte.
- Operación: recibir objetos y solicitudes de actualización de referencias.
- Comprobación: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Modelo mental

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Forma de referencia

```text
git receive-pack <git-dir>
```

Los elementos entre `<` y `>` se sustituyen por valores.

## Práctica

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

## Páginas relacionadas

- [`git send-pack`](../server-and-transport/send-pack.md)
- [`git http-push`](../server-and-transport/http-push.md)
- [`git shell`](../server-and-transport/shell.md)

## Fuente

- [git-receive-pack - Receive what is pushed into the repository](https://git-scm.com/docs/git-receive-pack)
