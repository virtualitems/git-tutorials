---
title: "git whatchanged"
source: "https://git-scm.com/docs/git-whatchanged"
section: "inspection-and-comparison"
status: "source-audited"
version: "2.55.0"
---

# `git whatchanged`

Este caso usa `git whatchanged` para mostrar commits junto con diferencias en formato sin procesar.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Ejemplo mínimo

```bash
git whatchanged --oneline -- README.md
```

La invocación `git whatchanged --oneline -- README.md` ejecuta esta operación: mostrar commits junto con diferencias en formato sin procesar. Después, la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Sintaxis y formas de invocación

```text
git whatchanged <option>…
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git log [<options>] [<revision-range>] [[--] <path>...]
   or: git show [<options>] <object>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git whatchanged -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git whatchanged --quiet --oneline -- README.md
printf 'exit=%s\n' "$?"
```

### `--source`

Incluye source en la salida o cambia cómo `git whatchanged` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show source`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git whatchanged --source --oneline -- README.md
printf 'exit=%s\n' "$?"
```

### `--use-mailmap`

Define use mailmap para esta ejecución de `git whatchanged`. En Git 2.51.1, la ayuda corta expresa el contrato como `use mail map file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git whatchanged` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git whatchanged --use-mailmap --oneline -- README.md
printf 'exit=%s\n' "$?"
```

### `--mailmap`

Define mailmap para esta ejecución de `git whatchanged`. En Git 2.51.1, la ayuda corta expresa el contrato como `alias of --use-mailmap`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git whatchanged --mailmap --oneline -- README.md
printf 'exit=%s\n' "$?"
```

### `--clear-decorations`

Activa clear decorations durante mostrar commits junto con diferencias en formato sin procesar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `clear all previously-defined decoration filters`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git whatchanged --clear-decorations --oneline -- README.md
printf 'exit=%s\n' "$?"
```

### `--decorate-refs`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git whatchanged --decorate-refs=TODO --oneline -- README.md
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--decorate-refs-exclude`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git whatchanged --decorate-refs-exclude=TODO --oneline -- README.md
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--decorate`

Activa decorate durante mostrar commits junto con diferencias en formato sin procesar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git whatchanged --decorate=valor --oneline -- README.md
printf 'exit=%s\n' "$?"
```

### `-L`

Activa L durante mostrar commits junto con diferencias en formato sin procesar. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `trace the evolution of line range <start>,<end> or function :<funcname> in <file>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git whatchanged` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git whatchanged -L rutas.txt --oneline -- README.md
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git verify-tag`](../inspection-and-comparison/verify-tag.md)
- [`git verify-commit`](../inspection-and-comparison/verify-commit.md)

## Fuente

- [git-whatchanged - Show logs with differences each commit introduces](https://git-scm.com/docs/git-whatchanged)
