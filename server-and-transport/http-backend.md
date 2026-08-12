---
title: "git http-backend"
source: "https://git-scm.com/docs/git-http-backend"
section: "server-and-transport"
status: "source-audited"
version: "2.55.0"
---

# `git http-backend`

Este caso usa `git http-backend` para atender operaciones Git del lado servidor sobre HTTP. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
GIT_PROJECT_ROOT=/srv/git GIT_HTTP_EXPORT_ALL=1 git http-backend
```

La invocación `git http-backend` ejecuta esta operación: atender operaciones Git del lado servidor sobre HTTP. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Sintaxis y formas de invocación

```text
git http-backend
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git http-backend -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-h`

Activa h durante atender operaciones Git del lado servidor sobre HTTP. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git http-backend -h
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git http-fetch`](../server-and-transport/http-fetch.md)
- [`git fetch-pack`](../server-and-transport/fetch-pack.md)
- [`git http-push`](../server-and-transport/http-push.md)

## Fuente

- [git-http-backend - Server side implementation of Git over HTTP](https://git-scm.com/docs/git-http-backend)
