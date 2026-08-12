---
title: "git config"
source: "https://git-scm.com/docs/git-config"
section: "setup-and-config"
status: "source-audited"
version: "2.55.0"
---

# `git config`

Este caso usa `git config` para leer y cambiar opciones de configuración por ámbito.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

## Ejemplo mínimo

```bash
git config --global user.name "Ana Torres"
git config --global user.email user@example.com
git config --get user.name
```

La invocación `git config --global user.name "Ana Torres"` ejecuta esta operación: leer y cambiar opciones de configuración por ámbito. Después, una consulta posterior muestra el valor efectivo o la información generada.

## Sintaxis y formas de invocación

```text
git config list [<file-option>] [<display-option>] [--includes]
git config get [<file-option>] [<display-option>] [--includes] [--all] [--regexp] [--value=<pattern>] [--fixed-value] [--default=<default>] [--url=<url>] <name>
git config set [<file-option>] [--type=<type>] [--all] [--value=<pattern>] [--fixed-value] <name> <value>
git config unset [<file-option>] [--all] [--value=<pattern>] [--fixed-value] <name>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git config list [<file-option>] [<display-option>] [--includes]
   or: git config get [<file-option>] [<display-option>] [--includes] [--all] [--regexp] [--value=<pattern>] [--fixed-value] [--default=<default>] [--url=<url>] <name>
   or: git config set [<file-option>] [--type=<type>] [--all] [--value=<pattern>] [--fixed-value] <name> <value>
   or: git config unset [<file-option>] [--all] [--value=<pattern>] [--fixed-value] <name>
   or: git config rename-section [<file-option>] <old-name> <new-name>
   or: git config remove-section [<file-option>] <name>
   or: git config edit [<file-option>]
   or: git config [<file-option>] --get-colorbool <name> [<stdout-is-tty>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git config -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--includes`

Activa includes durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git config --includes --global user.name "Ana Torres"
git config --show-origin --list
```

 La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git config --all --global user.name "Ana Torres"
git config --show-origin --list
```

 La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--regexp`

Activa regexp durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git config --regexp --global user.name "Ana Torres"
git config --show-origin --list
```

 La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--value`

Activa value durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git config --value --global user.name "Ana Torres"
git config --show-origin --list
```

 La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--fixed-value`

Activa fixed value durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git config --fixed-value --global user.name "Ana Torres"
git config --show-origin --list
```

 La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--default`

Activa default durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git config --default --global user.name "Ana Torres"
git config --show-origin --list
```

 La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--url`

Activa url durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git config --url --global user.name "Ana Torres"
git config --show-origin --list
```

 La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--type`

Activa type durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git config --type --global user.name "Ana Torres"
git config --show-origin --list
```

 La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--get-colorbool`

Activa get colorbool durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git config --get-colorbool --global user.name "Ana Torres"
git config --show-origin --list
```

 La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--value` y `--no-value`

Con `get`, `set` y `unset`, `--value=<patrón>` limita las entradas cuyo valor coincide con una expresión regular extendida; `--fixed-value` cambia esa comparación por igualdad literal. `--no-value` retira el filtro establecido por una opción anterior.

```bash
git config get --all --value='^main$' init.defaultBranch
git config get --all --fixed-value --value=main init.defaultBranch
```

### `--show-names` y `--no-show-names`

Con `get`, la forma positiva imprime cada clave además de su valor. La forma negativa conserva solo los valores y es la predeterminada, salvo el caso especial de `--url` sin subsecciones que define el manual.

```bash
git config get --all --show-names user.name
git config get --all --no-show-names user.name
```

Mantén el formato fijo en scripts porque ambas salidas tienen distinto número de campos.

## Páginas relacionadas

- [`git bugreport`](../setup-and-config/bugreport.md)
- [`git`](../setup-and-config/git.md)
- [`git diagnose`](../setup-and-config/diagnose.md)

## Fuente

- [git-config - Get and set repository or global options](https://git-scm.com/docs/git-config)
