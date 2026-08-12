---
title: "git shell"
source: "https://git-scm.com/docs/git-shell"
section: "server-and-transport"
status: "source-audited"
version: "2.55.0"
---

# `git shell`

Este caso usa `git shell` para restringir una cuenta SSH a operaciones de Git. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
chsh -s "$(command -v git-shell)" usuario-git
```

La invocación `git shell` ejecuta esta operación: restringir una cuenta SSH a operaciones de Git. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Sintaxis y formas de invocación

```text
chsh -s $(command -v git-shell) <user>
git clone <user>@localhost:/path/to/repo.git
ssh <user>@localhost
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git shell -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-s`

Activa s durante restringir una cuenta SSH a operaciones de Git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git shell -s
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v`

Activa v durante restringir una cuenta SSH a operaciones de Git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git shell -v
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-c`

Aplica una clave de configuración solo a esta invocación.

```bash
git shell -c
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git update-server-info`](../server-and-transport/update-server-info.md)
- [`git send-pack`](../server-and-transport/send-pack.md)
- [`git upload-archive`](../server-and-transport/upload-archive.md)

## Fuente

- [git-shell - Restricted login shell for Git-only SSH access](https://git-scm.com/docs/git-shell)
