---
title: "git upload-pack"
source: "https://git-scm.com/docs/git-upload-pack"
section: "server-and-transport"
status: "source-audited"
version: "2.55.0"
---

# `git upload-pack`

Este caso usa `git upload-pack` para negociar y enviar objetos a un cliente de fetch. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git upload-pack /srv/git/biblioteca.git
```

La invocación `git upload-pack /srv/git/biblioteca.git` ejecuta esta operación: negociar y enviar objetos a un cliente de fetch. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Sintaxis y formas de invocación

```text
git-upload-pack [--[no-]strict] [--timeout=<n>] [--stateless-rpc]
		  [--advertise-refs] <directory>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git-upload-pack [--[no-]strict] [--timeout=<n>] [--stateless-rpc]
                       [--advertise-refs] <directory>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git upload-pack -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--strict`

Impide strict durante esta invocación de `git upload-pack`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not try <directory>/.git/ if <directory> is no Git directory`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git upload-pack --strict /srv/git/biblioteca.git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--timeout`

Activa timeout durante negociar y enviar objetos a un cliente de fetch. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `interrupt transfer after <n> seconds of inactivity`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git upload-pack --timeout=5 /srv/git/biblioteca.git
git show-ref
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stateless-rpc`

Activa stateless rpc durante negociar y enviar objetos a un cliente de fetch. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `quit after a single request/response exchange`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git upload-pack` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque stateless rpc actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git upload-pack --stateless-rpc /srv/git/biblioteca.git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--advertise-refs`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git upload-pack --advertise-refs /srv/git/biblioteca.git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git upload-archive`](../server-and-transport/upload-archive.md)
- [`git update-server-info`](../server-and-transport/update-server-info.md)

## Fuente

- [git-upload-pack - Send objects packed back to git-fetch-pack](https://git-scm.com/docs/git-upload-pack)
