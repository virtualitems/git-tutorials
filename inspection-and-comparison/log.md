---
title: "git log"
source: "https://git-scm.com/docs/git-log"
section: "inspection-and-comparison"
status: "source-audited"
version: "2.55.0"
---

# `git log`

Este caso usa `git log` para consultar commits con filtros y formatos de salida.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Ejemplo mínimo

```bash
git log --oneline --decorate --graph --all
```

La invocación `git log --oneline --decorate --graph --all` ejecuta esta operación: consultar commits con filtros y formatos de salida. Después, la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Sintaxis y formas de invocación

```text
git log [<options>] [<revision-range>] [[--] <path>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git log [<options>] [<revision-range>] [[--] <path>...]
   or: git show [<options>] <object>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git log -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git log --quiet --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

### `--source`

Incluye source en la salida o cambia cómo `git log` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show source`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git log --source --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

### `--use-mailmap`

Define use mailmap para esta ejecución de `git log`. En Git 2.51.1, la ayuda corta expresa el contrato como `use mail map file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git log` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git log --use-mailmap --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

### `--mailmap`

Define mailmap para esta ejecución de `git log`. En Git 2.51.1, la ayuda corta expresa el contrato como `alias of --use-mailmap`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git log --mailmap --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

### `--clear-decorations`

Activa clear decorations durante consultar commits con filtros y formatos de salida. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `clear all previously-defined decoration filters`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git log --clear-decorations --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

### `--decorate-refs`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git log --decorate-refs=TODO --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--decorate-refs-exclude`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git log --decorate-refs-exclude=TODO --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--decorate`

Activa decorate durante consultar commits con filtros y formatos de salida. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git log --decorate=valor --oneline --all
printf 'exit=%s\n' "$?"
```

### `-L`

Activa L durante consultar commits con filtros y formatos de salida. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `trace the evolution of line range <start>,<end> or function :<funcname> in <file>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git log` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git log -L rutas.txt --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-use-mailmap`

Desactiva para esta invocación el comportamiento que habilita `--use-mailmap`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git log` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git log --no-use-mailmap --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

### `--no-mailmap`

Desactiva para esta invocación el comportamiento que habilita `--mailmap`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git log --no-mailmap --oneline --decorate --graph --all
printf 'exit=%s\n' "$?"
```

### `--no-decorate`

Desactiva para esta invocación el comportamiento que habilita `--decorate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git log --no-decorate --oneline --all
printf 'exit=%s\n' "$?"
```

### `--follow`

Continúa el historial de un archivo más allá de sus renombrados. Solo admite una ruta.

```bash
git log --follow --oneline -- README.md
```

### `--full-diff`

Con `git log -p -- <ruta>`, el pathspec limita tanto los commits como cada diff. `--full-diff` mantiene el filtro de commits, pero muestra el diff completo de cada commit seleccionado.

```bash
git log -p --full-diff -- README.md
```

### `--log-size`

Añade antes de cada commit una línea `log size <n>`, donde `<n>` es la cantidad de bytes del mensaje. Un consumidor puede reservar el búfer antes de leerlo.

```bash
git log --log-size --format='%H%n%B' -1
```

### Opciones compartidas

Los filtros y recorridos del grafo se explican en [`git rev-list`](../plumbing-read/rev-list.md#opciones). Los formatos de parche y comparación se explican en [opciones comunes de diff](../plumbing-read/diff-pairs.md#opciones).

## Páginas relacionadas

- [`git range-diff`](../inspection-and-comparison/range-diff.md)
- [`git last-modified`](../inspection-and-comparison/last-modified.md)
- [`git shortlog`](../inspection-and-comparison/shortlog.md)

## Fuente

- [git-log - Show commit logs](https://git-scm.com/docs/git-log)
