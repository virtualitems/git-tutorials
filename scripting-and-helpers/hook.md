---
title: "git hook"
source: "https://git-scm.com/docs/git-hook"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git hook`

Este caso usa `git hook` para enumerar o ejecutar hooks mediante Git.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git hook list pre-commit
git hook run pre-commit
```

La invocación `git hook list pre-commit` ejecuta esta operación: enumerar o ejecutar hooks mediante Git. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git hook run [--allow-unknown-hook-name] [--ignore-missing] [--to-stdin=<path>] [(-j|--jobs) <n>]
	<hook-name> [-- <hook-args>]
git hook list [--allow-unknown-hook-name] [-z] [--show-scope] <hook-name>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git hook run [--ignore-missing] [--to-stdin=<path>] <hook-name> [-- <hook-args>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git hook -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--allow-unknown-hook-name`

Activa permitir unknown hook nombre durante enumerar o ejecutar hooks mediante Git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git hook --allow-unknown-hook-name list pre-commit
printf 'exit=%s\n' "$?"
```

### `--ignore-missing`

Permite comprobar rutas ausentes bajo las condiciones que define la orden.

```bash
git hook --ignore-missing list pre-commit
printf 'exit=%s\n' "$?"
```

### `--to-stdin`

Activa to entrada estándar durante enumerar o ejecutar hooks mediante Git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git hook` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git hook --to-stdin list pre-commit
printf 'exit=%s\n' "$?"
```

### `-j`

Activa j durante enumerar o ejecutar hooks mediante Git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git hook -j list pre-commit
printf 'exit=%s\n' "$?"
```

### `--jobs`

Define cuántas tareas puede ejecutar Git en paralelo para la operación.

```bash
git hook --jobs list pre-commit
printf 'exit=%s\n' "$?"
```

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git hook -z list pre-commit
printf 'exit=%s\n' "$?"
```

### `--show-scope`

Muestra el alcance de cada valor de configuración.

```bash
git hook --show-scope list pre-commit
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git interpret-trailers`](../scripting-and-helpers/interpret-trailers.md)
- [`git fmt-merge-msg`](../scripting-and-helpers/fmt-merge-msg.md)
- [`git mailinfo`](../scripting-and-helpers/mailinfo.md)

## Fuente

- [git-hook - Run Git hooks](https://git-scm.com/docs/git-hook)
