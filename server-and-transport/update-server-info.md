---
title: "git update-server-info"
source: "https://git-scm.com/docs/git-update-server-info"
section: "server-and-transport"
---

# `git update-server-info`

## Ejemplo de partida

```bash
git update-server-info
```

Este caso usa `git update-server-info` para generar archivos auxiliares para clientes HTTP sin negociación. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Qué se deriva del ejemplo

- Entrada: la ruta del repositorio, el servicio y los parámetros de transporte.
- Operación: generar archivos auxiliares para clientes HTTP sin negociación.
- Comprobación: los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Modelo mental

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Forma de referencia

```text
git update-server-info [-f | --force]
```

Los corchetes delimitan partes opcionales.

## Práctica

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

## Páginas relacionadas

- [`git upload-archive`](../server-and-transport/upload-archive.md)
- [`git shell`](../server-and-transport/shell.md)
- [`git upload-pack`](../server-and-transport/upload-pack.md)

## Fuente

- [git-update-server-info - Update auxiliary info file to help dumb servers](https://git-scm.com/docs/git-update-server-info)
