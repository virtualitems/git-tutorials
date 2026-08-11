---
title: "git shell"
source: "https://git-scm.com/docs/git-shell"
section: "server-and-transport"
---

# `git shell`

## Ejemplo de partida

```bash
chsh -s "$(command -v git-shell)" usuario-git
```

Este caso usa `git shell` para restringir una cuenta SSH a operaciones de Git. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Qué se deriva del ejemplo

- Entrada: la ruta del repositorio, el servicio y los parámetros de transporte.
- Operación: restringir una cuenta SSH a operaciones de Git.
- Comprobación: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Modelo mental

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Forma de referencia

```text
chsh -s $(command -v git-shell) <user>
git clone <user>@localhost:/path/to/repo.git
ssh <user>@localhost
```

Los elementos entre `<` y `>` se sustituyen por valores.

## Práctica

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

## Páginas relacionadas

- [`git update-server-info`](../server-and-transport/update-server-info.md)
- [`git send-pack`](../server-and-transport/send-pack.md)
- [`git upload-archive`](../server-and-transport/upload-archive.md)

## Fuente

- [git-shell - Restricted login shell for Git-only SSH access](https://git-scm.com/docs/git-shell)
