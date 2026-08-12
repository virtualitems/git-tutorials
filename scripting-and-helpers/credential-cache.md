---
title: "git credential-cache"
source: "https://git-scm.com/docs/git-credential-cache"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git credential-cache`

Este caso usa `git credential-cache` para mantener credenciales durante un tiempo en memoria.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git config --global credential.helper 'cache --timeout=900'
```

La invocación `git credential-cache` ejecuta esta operación: mantener credenciales durante un tiempo en memoria. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git config credential.helper 'cache [<options>]'
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git credential-cache [<options>] <action>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git credential-cache -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--timeout`

Activa timeout durante mantener credenciales durante un tiempo en memoria. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `number of seconds to cache credentials`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git credential-cache --timeout=5
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--socket`

Activa socket durante mantener credenciales durante un tiempo en memoria. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `path of cache-daemon socket`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git credential-cache --socket=archivo.txt
printf 'exit=%s\n' "$?"
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git credential-store`](../scripting-and-helpers/credential-store.md)
- [`git credential`](../scripting-and-helpers/credential.md)
- [`git fmt-merge-msg`](../scripting-and-helpers/fmt-merge-msg.md)

## Fuente

- [git-credential-cache - Helper to temporarily store passwords in memory](https://git-scm.com/docs/git-credential-cache)
