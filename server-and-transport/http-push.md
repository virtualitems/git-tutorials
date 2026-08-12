---
title: "git http-push"
source: "https://git-scm.com/docs/git-http-push"
section: "server-and-transport"
status: "source-audited"
version: "2.55.0"
---

# `git http-push`

Este caso usa `git http-push` para enviar objetos mediante HTTP con WebDAV. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git http-push --dry-run https://example.com/equipo/biblioteca.git refs/heads/main
```

La invocación `git http-push --dry-run https://example.com/equipo/biblioteca.git refs/heads/main` ejecuta esta operación: enviar objetos mediante HTTP con WebDAV. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Sintaxis y formas de invocación

```text
git http-push [--all] [--dry-run] [--force] [--verbose] <URL> <ref> [<ref>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git http-push [--all] [--dry-run] [--force] [--verbose] <remote> [<head>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git http-push -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git http-push --all --dry-run https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

```bash
git http-push --dry-run https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

```bash
git http-push --force --dry-run https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verbose`

Aumenta el detalle enviado a la salida.

```bash
git http-push --verbose --dry-run https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git receive-pack`](../server-and-transport/receive-pack.md)
- [`git http-fetch`](../server-and-transport/http-fetch.md)
- [`git send-pack`](../server-and-transport/send-pack.md)

## Fuente

- [git-http-push - Push objects over HTTP/DAV to another repository](https://git-scm.com/docs/git-http-push)
