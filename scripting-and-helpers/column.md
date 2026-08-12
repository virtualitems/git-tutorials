---
title: "git column"
source: "https://git-scm.com/docs/git-column"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git column`

Este caso usa `git column` para organizar líneas de entrada en columnas.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
printf '%s\n' main develop release | git column --mode=column
```

La invocación `git column` ejecuta esta operación: organizar líneas de entrada en columnas. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git column [--command=<name>] [--[raw-]mode=<mode>] [--width=<width>]
	     [--indent=<string>] [--nl=<string>] [--padding=<n>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git column [<options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git column -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--command`

Activa command durante organizar líneas de entrada en columnas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git column --command=tema
printf 'exit=%s\n' "$?"
```

El ejemplo usa `tema` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--width`

Define el límite representado por width para esta ejecución. En Git 2.51.1, la ayuda corta expresa el contrato como `maximum width`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git column --width=5
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--indent`

Activa indent durante organizar líneas de entrada en columnas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `padding space on left border`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git column --indent=valor
printf 'exit=%s\n' "$?"
```

### `--nl`

Activa nl durante organizar líneas de entrada en columnas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `padding space on right border`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git column --nl=valor
printf 'exit=%s\n' "$?"
```

### `--padding`

Activa padding durante organizar líneas de entrada en columnas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `padding space between columns`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git column --padding=5
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mode`

Define mode para esta ejecución de `git column`.

```bash
git column --mode=short
printf 'exit=%s\n' "$?"
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--raw-mode`

Define raw mode para esta ejecución de `git column`. En Git 2.51.1, la ayuda corta expresa el contrato como `layout to use`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git column --raw-mode=5
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git credential`](../scripting-and-helpers/credential.md)
- [`git check-ref-format`](../scripting-and-helpers/check-ref-format.md)
- [`git credential-cache`](../scripting-and-helpers/credential-cache.md)

## Fuente

- [git-column - Display data in columns](https://git-scm.com/docs/git-column)
