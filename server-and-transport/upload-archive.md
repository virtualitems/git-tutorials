---
title: "git upload-archive"
source: "https://git-scm.com/docs/git-upload-archive"
section: "server-and-transport"
status: "source-audited"
version: "2.55.0"
---

# `git upload-archive`

Este caso usa `git upload-archive` para responder a una solicitud remota de git archive. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git upload-archive /srv/git/biblioteca.git
```

La invocación `git upload-archive /srv/git/biblioteca.git` ejecuta esta operación: responder a una solicitud remota de git archive. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Sintaxis y formas de invocación

```text
git upload-archive <repository>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git upload-archive <repository>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git upload-archive -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-h`

Activa h durante responder a una solicitud remota de git archive. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git upload-archive -h
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git upload-pack`](../server-and-transport/upload-pack.md)
- [`git update-server-info`](../server-and-transport/update-server-info.md)
- [`git shell`](../server-and-transport/shell.md)

## Fuente

- [git-upload-archive - Send archive back to git-archive](https://git-scm.com/docs/git-upload-archive)
