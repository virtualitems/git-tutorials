---
title: "git daemon"
source: "https://git-scm.com/docs/git-daemon"
section: "server-and-transport"
---

# `git daemon`

## Ejemplo de partida

```bash
git daemon --reuseaddr --base-path=/srv/git /srv/git
```

Este caso usa `git daemon` para servir repositorios mediante el protocolo git. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Qué se deriva del ejemplo

- Entrada: la ruta del repositorio, el servicio y los parámetros de transporte.
- Operación: servir repositorios mediante el protocolo git.
- Comprobación: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Modelo mental

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Forma de referencia

```text
git daemon [--verbose] [--syslog] [--export-all]
	   [--timeout=<n>] [--init-timeout=<n>] [--max-connections=<n>]
	   [--strict-paths] [--base-path=<path>] [--base-path-relaxed]
	   [--user-path | --user-path=<path>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

## Páginas relacionadas

- [`git fetch-pack`](../server-and-transport/fetch-pack.md)
- [`git http-backend`](../server-and-transport/http-backend.md)

## Fuente

- [git-daemon - A really simple server for Git repositories](https://git-scm.com/docs/git-daemon)
