---
title: "git imap-send"
source: "https://git-scm.com/docs/git-imap-send"
section: "email-and-patches"
status: "source-audited"
version: "2.55.0"
---

# `git imap-send`

Este caso usa `git imap-send` para enviar una colección de parches a una carpeta IMAP.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Cada parche puede transportar autoría, mensaje y diferencias. El receptor valida, aplica y registra la serie en su propio historial.

Conserva el orden de la serie y separa autor de quien aplica el parche. Los conflictos se resuelven antes de continuar con el siguiente mensaje.

## Ejemplo mínimo

```bash
git format-patch --stdout origin/main..HEAD | git imap-send
```

La invocación `git imap-send` ejecuta esta operación: enviar una colección de parches a una carpeta IMAP. Después, el receptor obtiene parches o commits con el orden, autoría y mensaje esperados.

## Sintaxis y formas de invocación

```text
git imap-send [-v] [-q] [--[no-]curl] [(--folder|-f) <folder>]
git imap-send --list
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git imap-send [-v] [-q] [--[no-]curl] [(--folder|-f) <folder>] < <mbox>
   or: git imap-send --list
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git imap-send -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git imap-send --verbose
printf 'exit=%s\n' "$?"
```

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git imap-send --quiet
printf 'exit=%s\n' "$?"
```

### `--curl`

Define curl para esta ejecución de `git imap-send`. En Git 2.51.1, la ayuda corta expresa el contrato como `use libcurl to communicate with the IMAP server`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git imap-send --curl
printf 'exit=%s\n' "$?"
```

### `--folder` y `-f`

Define folder para esta ejecución de `git imap-send`. En Git 2.51.1, la ayuda corta expresa el contrato como `specify the IMAP folder`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--folder`

```bash
git imap-send --folder=valor
printf 'exit=%s\n' "$?"
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--list`

Incluye información adicional en la salida.

```bash
git imap-send --list
printf 'exit=%s\n' "$?"
```

### `--no-curl`

Desactiva para esta invocación el comportamiento que habilita `--curl`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git imap-send --no-curl
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git send-email`](../email-and-patches/send-email.md)
- [`git format-patch`](../email-and-patches/format-patch.md)
- [`git am`](../email-and-patches/am.md)

## Fuente

- [git-imap-send - Send a collection of patches from stdin to an IMAP folder](https://git-scm.com/docs/git-imap-send)
