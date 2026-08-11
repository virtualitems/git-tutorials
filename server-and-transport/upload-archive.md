---
title: "git upload-archive"
source: "https://git-scm.com/docs/git-upload-archive"
section: "server-and-transport"
---

# `git upload-archive`

## Ejemplo de partida

```bash
git upload-archive /srv/git/biblioteca.git
```

Este caso usa `git upload-archive` para responder a una solicitud remota de git archive. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Qué se deriva del ejemplo

- Entrada: la ruta del repositorio, el servicio y los parámetros de transporte.
- Operación: responder a una solicitud remota de git archive.
- Comprobación: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Modelo mental

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Forma de referencia

```text
git upload-archive <repository>
```

Los elementos entre `<` y `>` se sustituyen por valores.

## Práctica

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

## Páginas relacionadas

- [`git upload-pack`](../server-and-transport/upload-pack.md)
- [`git update-server-info`](../server-and-transport/update-server-info.md)
- [`git shell`](../server-and-transport/shell.md)

## Fuente

- [git-upload-archive - Send archive back to git-archive](https://git-scm.com/docs/git-upload-archive)
