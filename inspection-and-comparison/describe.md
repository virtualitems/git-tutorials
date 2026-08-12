---
title: "git describe"
source: "https://git-scm.com/docs/git-describe"
section: "inspection-and-comparison"
status: "source-audited"
version: "2.55.0"
---

# `git describe`

Este caso usa `git describe` para nombrar un commit con la referencia cercana que lo alcanza.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Ejemplo mínimo

```bash
git tag v1.0
git describe --tags --always HEAD
```

La invocación `git describe --tags --always HEAD` ejecuta esta operación: nombrar un commit con la referencia cercana que lo alcanza. Después, la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Sintaxis y formas de invocación

```text
git describe [--all] [--tags] [--contains] [--abbrev=<n>] [<commit-ish>…]
git describe [--all] [--tags] [--contains] [--abbrev=<n>] --dirty[=<mark>]
git describe <blob>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git describe [--all] [--tags] [--contains] [--abbrev=<n>] [<commit-ish>...]
   or: git describe [--all] [--tags] [--contains] [--abbrev=<n>] --dirty[=<mark>]
   or: git describe <blob>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git describe -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git describe --all --tags --always HEAD
printf 'exit=%s\n' "$?"
```

### `--tags`

Incluye o selecciona etiquetas según la operación.

```bash
git describe --tags --always HEAD
printf 'exit=%s\n' "$?"
```

### `--contains`

Filtra referencias cuyo historial contiene el commit indicado.

```bash
git describe --contains --tags --always HEAD
printf 'exit=%s\n' "$?"
```

### `--abbrev`

Reduce la representación visible del identificador sin cambiar el objeto.

```bash
git describe --abbrev=5 --tags --always HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dirty`

Activa dirty durante nombrar un commit con la referencia cercana que lo alcanza. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git describe --dirty=valor --tags --always HEAD
printf 'exit=%s\n' "$?"
```

### `--debug`

Activa debug durante nombrar un commit con la referencia cercana que lo alcanza. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `debug search strategy on stderr`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción selecciona el procedimiento que `git describe` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git describe --debug --tags --always HEAD
printf 'exit=%s\n' "$?"
```

### `--long`

Define long para esta ejecución de `git describe`. En Git 2.51.1, la ayuda corta expresa el contrato como `always use long format`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git describe --long --tags --always HEAD
printf 'exit=%s\n' "$?"
```

### `--first-parent`

Limita nombrar un commit con la referencia cercana que lo alcanza al alcance identificado por first parent. En Git 2.51.1, la ayuda corta expresa el contrato como `only follow first parent`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git describe --first-parent --tags --always HEAD
printf 'exit=%s\n' "$?"
```

### `--exact-match`

Limita nombrar un commit con la referencia cercana que lo alcanza al alcance identificado por exact match. En Git 2.51.1, la ayuda corta expresa el contrato como `only output exact matches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git describe --exact-match --tags --always HEAD
printf 'exit=%s\n' "$?"
```

### `--candidates`

Activa candidates durante nombrar un commit con la referencia cercana que lo alcanza. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git describe --candidates=5 --tags --always HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--match`

Limita nombrar un commit con la referencia cercana que lo alcanza al alcance identificado por match. En Git 2.51.1, la ayuda corta expresa el contrato como `only consider tags matching <pattern>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git describe --match=TODO --tags --always HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude`

Excluye elementos que cumplan la condición indicada.

```bash
git describe --exclude=TODO --tags --always HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--always`

Incluye always en la salida o cambia cómo `git describe` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show abbreviated commit object as fallback`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git describe --always --tags HEAD
printf 'exit=%s\n' "$?"
```

### `--broken`

Activa broken durante nombrar un commit con la referencia cercana que lo alcanza. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `append <mark> on broken working tree (default: "-broken")`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git describe --broken=valor --tags --always HEAD
printf 'exit=%s\n' "$?"
```

### `--no-match`

Desactiva para esta invocación el comportamiento que habilita `--match`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git describe --no-match --tags --always HEAD
printf 'exit=%s\n' "$?"
```

### `--no-exclude`

Desactiva para esta invocación el comportamiento que habilita `--exclude`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git describe --no-exclude --tags --always HEAD
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git diff`](../inspection-and-comparison/diff.md)
- [`git difftool`](../inspection-and-comparison/difftool.md)

## Fuente

- [git-describe - Give an object a human readable name based on an available ref](https://git-scm.com/docs/git-describe)
