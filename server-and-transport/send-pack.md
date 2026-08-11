---
title: "git send-pack"
source: "https://git-scm.com/docs/git-send-pack"
section: "server-and-transport"
---

# `git send-pack`

## Ejemplo de partida

```bash
git send-pack https://example.test/equipo/biblioteca.git refs/heads/main
```

Este caso usa `git send-pack` para enviar objetos y actualizaciones de referencias al receptor. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Qué se deriva del ejemplo

- Entrada: la ruta del repositorio, el servicio y los parámetros de transporte.
- Operación: enviar objetos y actualizaciones de referencias al receptor.
- Comprobación: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Modelo mental

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Forma de referencia

```text
git send-pack [--mirror] [--dry-run] [--force]
		[--receive-pack=<git-receive-pack>]
		[--verbose] [--thin] [--atomic]
		[--[no-]signed | --signed=(true|false|if-asked)]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

## Páginas relacionadas

- [`git shell`](../server-and-transport/shell.md)
- [`git receive-pack`](../server-and-transport/receive-pack.md)
- [`git update-server-info`](../server-and-transport/update-server-info.md)

## Fuente

- [git-send-pack - Push objects over Git protocol to another repository](https://git-scm.com/docs/git-send-pack)
