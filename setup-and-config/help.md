---
title: "git help"
source: "https://git-scm.com/docs/git-help"
section: "setup-and-config"
status: "source-audited"
version: "2.55.0"
---

# `git help`

Este caso usa `git help` para abrir la ayuda de un comando o concepto.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

## Ejemplo mínimo

```bash
git help rebase
git help revisions
```

La invocación `git help rebase` ejecuta esta operación: abrir la ayuda de un comando o concepto. Después, una consulta posterior muestra el valor efectivo o la información generada.

## Sintaxis y formas de invocación

```text
git help [-a|--all] [--[no-]verbose] [--[no-]external-commands] [--[no-]aliases]
git help [[-i|--info] [-m|--man] [-w|--web]] [<command>|<doc>]
git help [-g|--guides]
git help [-c|--config]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git help [-a|--all] [--[no-]verbose] [--[no-]external-commands] [--[no-]aliases]
   or: git help [[-i|--info] [-m|--man] [-w|--web]] [<command>|<doc>]
   or: git help [-g|--guides]
   or: git help [-c|--config]
   or: git help [--user-interfaces]
   or: git help [--developer-interfaces]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git help -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-a` y `--all`

Amplía la selección a todos los elementos del alcance definido.

#### Ejemplo con `--all`

```bash
git help --all rebase
printf 'exit=%s\n' "$?"
```

### `--verbose` y `-v`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git help --verbose rebase
printf 'exit=%s\n' "$?"
```

### `--external-commands`

Incluye external commands en la salida o cambia cómo `git help` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show external commands in --all`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git help --external-commands rebase
printf 'exit=%s\n' "$?"
```

### `--aliases`

Incluye aliases en la salida o cambia cómo `git help` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show aliases in --all`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git help --aliases rebase
printf 'exit=%s\n' "$?"
```

### `-i` y `--info`

Incluye info en la salida o cambia cómo `git help` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show info page`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--info`

```bash
git help --info rebase
printf 'exit=%s\n' "$?"
```

### `-m` y `--man`

Incluye man en la salida o cambia cómo `git help` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show man page`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--man`

```bash
git help --man rebase
printf 'exit=%s\n' "$?"
```

### `-w` y `--web`

Incluye web en la salida o cambia cómo `git help` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show manual in web browser`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--web`

```bash
git help --web rebase
printf 'exit=%s\n' "$?"
```

### `-g` y `--guides`

Incluye guides en la salida o cambia cómo `git help` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print list of useful guides`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--guides`

```bash
git help --guides rebase
printf 'exit=%s\n' "$?"
```

### `-c` y `--config`

Incluye config en la salida o cambia cómo `git help` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print all configuration variable names`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--config`

```bash
git help --config rebase
printf 'exit=%s\n' "$?"
```

### `--user-interfaces`

Incluye user interfaces en la salida o cambia cómo `git help` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print list of user-facing repository, command and file interfaces`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git help --user-interfaces rebase
printf 'exit=%s\n' "$?"
```

### `--developer-interfaces`

Incluye developer interfaces en la salida o cambia cómo `git help` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print list of file formats, protocols and other developer interfaces`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git help --developer-interfaces rebase
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git version`](../setup-and-config/version.md)
- [`git diagnose`](../setup-and-config/diagnose.md)
- [`git bugreport`](../setup-and-config/bugreport.md)

## Fuente

- [git-help - Display help information about Git](https://git-scm.com/docs/git-help)
