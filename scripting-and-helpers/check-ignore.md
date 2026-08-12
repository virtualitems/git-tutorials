---
title: "git check-ignore"
source: "https://git-scm.com/docs/git-check-ignore"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git check-ignore`

Este caso usa `git check-ignore` para explicar qué regla de exclusión afecta a una ruta.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git check-ignore -v build/salida.log
```

La invocación `git check-ignore -v build/salida.log` ejecuta esta operación: explicar qué regla de exclusión afecta a una ruta. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git check-ignore [<options>] <pathname>…
git check-ignore [<options>] --stdin
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git check-ignore [<options>] <pathname>...
   or: git check-ignore [<options>] --stdin
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git check-ignore -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git check-ignore` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git check-ignore --stdin -v build/salida.log
printf 'exit=%s\n' "$?"
```

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git check-ignore --quiet -v build/salida.log
printf 'exit=%s\n' "$?"
```

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git check-ignore --verbose build/salida.log
printf 'exit=%s\n' "$?"
```

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git check-ignore -z -v build/salida.log
printf 'exit=%s\n' "$?"
```

### `-n` y `--non-matching`

Incluye non matching en la salida o cambia cómo `git check-ignore` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show non-matching input paths`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--non-matching`

```bash
git check-ignore --non-matching -v build/salida.log
printf 'exit=%s\n' "$?"
```

### `--no-index`

Desactiva el comportamiento `index` para esta invocación.

```bash
git check-ignore --no-index -v build/salida.log
printf 'exit=%s\n' "$?"
```

### `--index`

Incluye el índice en la operación.

```bash
git check-ignore --index -v build/salida.log
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git check-mailmap`](../scripting-and-helpers/check-mailmap.md)
- [`git check-attr`](../scripting-and-helpers/check-attr.md)
- [`git check-ref-format`](../scripting-and-helpers/check-ref-format.md)

## Fuente

- [git-check-ignore - Debug gitignore / exclude files](https://git-scm.com/docs/git-check-ignore)
