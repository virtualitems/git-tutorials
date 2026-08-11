---
title: "git upload-pack"
source: "https://git-scm.com/docs/git-upload-pack"
section: "server-and-transport"
---

# `git upload-pack`

## Ejemplo de partida

```bash
git upload-pack /srv/git/biblioteca.git
```

Este caso usa `git upload-pack` para negociar y enviar objetos a un cliente de fetch. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Qué se deriva del ejemplo

- Entrada: la ruta del repositorio, el servicio y los parámetros de transporte.
- Operación: negociar y enviar objetos a un cliente de fetch.
- Comprobación: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Modelo mental

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Forma de referencia

```text
git-upload-pack [--[no-]strict] [--timeout=<n>] [--stateless-rpc]
		  [--advertise-refs] <directory>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

## Páginas relacionadas

- [`git upload-archive`](../server-and-transport/upload-archive.md)
- [`git update-server-info`](../server-and-transport/update-server-info.md)

## Fuente

- [git-upload-pack - Send objects packed back to git-fetch-pack](https://git-scm.com/docs/git-upload-pack)
