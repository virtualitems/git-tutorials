---
title: "git fmt-merge-msg"
source: "https://git-scm.com/docs/git-fmt-merge-msg"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git fmt-merge-msg`

Este caso usa `git fmt-merge-msg` para generar el mensaje de un commit de fusión.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git fetch origin main
git fmt-merge-msg --log < .git/FETCH_HEAD
```

La invocación `git fmt-merge-msg --log < .git/FETCH_HEAD` ejecuta esta operación: generar el mensaje de un commit de fusión. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git fmt-merge-msg [-m <message>] [--into-name <branch>] [--log[=<n>] | --no-log]
git fmt-merge-msg [-m <message>] [--log[=<n>] | --no-log] -F <file>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git fmt-merge-msg [-m <message>] [--log[=<n>] | --no-log] [--file <file>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git fmt-merge-msg -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-m` y `--message`

Define mensaje para esta ejecución de `git fmt-merge-msg`. En Git 2.51.1, la ayuda corta expresa el contrato como `use <text> as start of message`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--message`

```bash
git fmt-merge-msg --message=valor --log < .git/FETCH_HEAD
printf 'exit=%s\n' "$?"
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--into-name`

Define into nombre para esta ejecución de `git fmt-merge-msg`. En Git 2.51.1, la ayuda corta expresa el contrato como `use <name> instead of the real target branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fmt-merge-msg --into-name=tema --log < .git/FETCH_HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `tema` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--log`

Activa log durante generar el mensaje de un commit de fusión. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `populate log with at most <n> entries from shortlog`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fmt-merge-msg --log=5 .git/FETCH_HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-log`

Desactiva el comportamiento `log` para esta invocación.

```bash
git fmt-merge-msg --no-log .git/FETCH_HEAD
printf 'exit=%s\n' "$?"
```

### `-F` y `--file`

Usa el archivo indicado en vez de la ubicación por defecto.

La opción cambia cómo `git fmt-merge-msg` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `--file`

```bash
git fmt-merge-msg --file=rutas.txt --log < .git/FETCH_HEAD
printf 'exit=%s\n' "$?"
```

En esta forma, `rutas.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

## Páginas relacionadas

- [`git hook`](../scripting-and-helpers/hook.md)
- [`git credential-store`](../scripting-and-helpers/credential-store.md)
- [`git interpret-trailers`](../scripting-and-helpers/interpret-trailers.md)

## Fuente

- [git-fmt-merge-msg - Produce a merge commit message](https://git-scm.com/docs/git-fmt-merge-msg)
