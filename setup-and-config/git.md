---
title: "git"
source: "https://git-scm.com/docs/git"
section: "setup-and-config"
status: "source-audited"
version: "2.55.0"
---

# `git`

Este caso usa `git` para invocar Git, elegir el repositorio y aplicar opciones globales.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

## Ejemplo mínimo

```bash
git -C ../biblioteca status
git -c color.ui=false log --oneline -3
```

La invocación `git -C ../biblioteca status` ejecuta esta operación: invocar Git, elegir el repositorio y aplicar opciones globales. Después, una consulta posterior muestra el valor efectivo o la información generada.

## Sintaxis y formas de invocación

```text
git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
    [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
    [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--no-lazy-fetch]
    [--no-optional-locks] [--no-advice] [--bare] [--git-dir=<path>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--no-lazy-fetch]
           [--no-optional-locks] [--no-advice] [--bare] [--git-dir=<path>]
           [--work-tree=<path>] [--namespace=<name>] [--config-env=<name>=<envvar>]
           <command> [<args>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-v`

Activa v durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git -v -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--version`

Muestra la versión y termina.

```bash
git --version
printf 'exit=%s\n' "$?"
```

### `-h`

Muestra ayuda corta cuando la orden admite esta convención.

```bash
git -h
printf 'exit=%s\n' "$?"
```

### `--help`

Muestra la ayuda correspondiente a la versión instalada.

```bash
git --help
printf 'exit=%s\n' "$?"
```

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

```bash
git -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `-c`

Aplica una clave de configuración solo a esta invocación.

```bash
git -c -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--exec-path`

Activa exec ruta durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git --exec-path -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--html-path`

Activa html ruta durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git --html-path -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--man-path`

Activa man ruta durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git --man-path -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--info-path`

Activa info ruta durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git --info-path -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `-p`

Activa p durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git -p -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--paginate`

Envía la salida por el paginador configurado.

```bash
git --paginate -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `-P`

Activa P durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git -P -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--no-pager`

Escribe la salida sin paginador.

```bash
git --no-pager -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--no-replace-objects`

Ignora referencias de reemplazo durante la lectura de objetos.

```bash
git --no-replace-objects -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--no-lazy-fetch`

Desactiva el comportamiento `lazy-fetch` para esta invocación.

```bash
git --no-lazy-fetch -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--no-optional-locks`

Desactiva el comportamiento `optional-locks` para esta invocación.

```bash
git --no-optional-locks -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--no-advice`

Desactiva el comportamiento `advice` para esta invocación.

```bash
git --no-advice -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--bare`

Opera sin un área de trabajo asociada.

```bash
git --bare -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--git-dir`

Define de forma explícita la ruta del directorio Git.

```bash
git --git-dir -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--work-tree`

Define de forma explícita la raíz del área de trabajo.

```bash
git --work-tree -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--namespace`

Selecciona el namespace de referencias para la invocación.

```bash
git --namespace -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `--config-env`

Toma un valor de configuración desde una variable de entorno.

```bash
git --config-env -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `-a`

Activa a durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git -a -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

### `-g`

Activa g durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git -g -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git config`](../setup-and-config/config.md)
- [`git bugreport`](../setup-and-config/bugreport.md)

## Fuente

- [git - the stupid content tracker](https://git-scm.com/docs/git)
