---
title: "git stripspace"
source: "https://git-scm.com/docs/git-stripspace"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git stripspace`

Este caso usa `git stripspace` para normalizar espacios, líneas vacías y comentarios de un mensaje.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
printf 'Título  \n\n\nCuerpo\n' | git stripspace
```

La invocación `git stripspace` ejecuta esta operación: normalizar espacios, líneas vacías y comentarios de un mensaje. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git stripspace [-s | --strip-comments]
git stripspace [-c | --comment-lines]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git stripspace [-s | --strip-comments]
   or: git stripspace [-c | --comment-lines]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git stripspace -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-s` y `--strip-comments`

Retira strip comments del alcance que procesa `git stripspace`. En Git 2.51.1, la ayuda corta expresa el contrato como `skip and remove all lines starting with comment character`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git stripspace` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque strip comments actúa sobre el estado que Git registró al iniciar la secuencia.

#### Ejemplo con `--strip-comments`

```bash
git stripspace --strip-comments
printf 'exit=%s\n' "$?"
```

### `-c` y `--comment-lines`

Antepone comment lines al valor que produce `git stripspace`. En Git 2.51.1, la ayuda corta expresa el contrato como `prepend comment character and space to each line`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--comment-lines`

```bash
git stripspace --comment-lines
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git url-parse`](../scripting-and-helpers/url-parse.md)
- [`git sh-setup`](../scripting-and-helpers/sh-setup.md)
- [`git sh-i18n`](../scripting-and-helpers/sh-i18n.md)

## Fuente

- [git-stripspace - Remove unnecessary whitespace](https://git-scm.com/docs/git-stripspace)
