---
title: "git receive-pack"
source: "https://git-scm.com/docs/git-receive-pack"
section: "server-and-transport"
status: "source-audited"
version: "2.55.0"
---

# `git receive-pack`

Este caso usa `git receive-pack` para recibir objetos y solicitudes de actualización de referencias. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git receive-pack /srv/git/biblioteca.git
```

La invocación `git receive-pack /srv/git/biblioteca.git` ejecuta esta operación: recibir objetos y solicitudes de actualización de referencias. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Sintaxis y formas de invocación

```text
git receive-pack <git-dir>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git receive-pack <git-dir>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git receive-pack -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git receive-pack --quiet /srv/git/biblioteca.git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió.

## Páginas relacionadas

- [`git send-pack`](../server-and-transport/send-pack.md)
- [`git http-push`](../server-and-transport/http-push.md)
- [`git shell`](../server-and-transport/shell.md)

## Fuente

- [git-receive-pack - Receive what is pushed into the repository](https://git-scm.com/docs/git-receive-pack)
