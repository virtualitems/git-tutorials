---
title: "git interpret-trailers"
source: "https://git-scm.com/docs/git-interpret-trailers"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git interpret-trailers`

Este caso usa `git interpret-trailers` para analizar y añadir campos al final de mensajes de commit.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
printf '%s\n' 'Corrige el índice' | git interpret-trailers --trailer 'Reviewed-by: Ana <user@example.com>'
```

La invocación `git interpret-trailers` ejecuta esta operación: analizar y añadir campos al final de mensajes de commit. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git interpret-trailers [--in-place] [--trim-empty]
			[(--trailer (<key>|<key-alias>)[(=|:)<value>])…]
			[--parse] [<file>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git interpret-trailers [--in-place] [--trim-empty]
                              [(--trailer (<key>|<key-alias>)[(=|:)<value>])...]
                              [--parse] [<file>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git interpret-trailers -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--in-place`

Activa in place durante analizar y añadir campos al final de mensajes de commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `edit files in place`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git interpret-trailers` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git interpret-trailers --in-place
printf 'exit=%s\n' "$?"
```

### `--trim-empty`

Activa trim vacío durante analizar y añadir campos al final de mensajes de commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `trim empty trailers`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git interpret-trailers --trim-empty
printf 'exit=%s\n' "$?"
```

### `--trailer`

Incluye trailer en la entrada, el resultado o el registro que construye `git interpret-trailers`. En Git 2.51.1, la ayuda corta expresa el contrato como `trailer(s) to add`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git interpret-trailers --trailer=valor
printf 'exit=%s\n' "$?"
```

### `--parse`

Limita analizar y añadir campos al final de mensajes de commit al alcance identificado por parse. En Git 2.51.1, la ayuda corta expresa el contrato como `alias for --only-trailers --only-input --unfold`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git interpret-trailers` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git interpret-trailers --parse
printf 'exit=%s\n' "$?"
```

### `--where`

Activa where durante analizar y añadir campos al final de mensajes de commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `where to place the new trailer`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git interpret-trailers --where=valor
printf 'exit=%s\n' "$?"
```

### `--if-exists`

Activa if exists durante analizar y añadir campos al final de mensajes de commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `action if trailer already exists`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git interpret-trailers --if-exists=warn
printf 'exit=%s\n' "$?"
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--if-missing`

Activa if missing durante analizar y añadir campos al final de mensajes de commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `action if trailer is missing`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git interpret-trailers --if-missing=warn
printf 'exit=%s\n' "$?"
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--only-trailers`

Limita analizar y añadir campos al final de mensajes de commit al alcance identificado por only trailers. En Git 2.51.1, la ayuda corta expresa el contrato como `output only the trailers`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git interpret-trailers --only-trailers
printf 'exit=%s\n' "$?"
```

### `--only-input`

Impide only entrada durante esta invocación de `git interpret-trailers`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not apply trailer.* configuration variables`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git interpret-trailers` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git interpret-trailers --only-input
printf 'exit=%s\n' "$?"
```

### `--unfold`

Activa unfold durante analizar y añadir campos al final de mensajes de commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `reformat multiline trailer values as single-line values`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git interpret-trailers --unfold
printf 'exit=%s\n' "$?"
```

### `--no-divider`

Desactiva el comportamiento `divider` para esta invocación.

```bash
git interpret-trailers --no-divider
printf 'exit=%s\n' "$?"
```

### `--divider`

Selecciona la relación indicada por divider; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-divider`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git interpret-trailers --divider
printf 'exit=%s\n' "$?"
```

### `--no-in-place`

Desactiva para esta invocación el comportamiento que habilita `--in-place`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git interpret-trailers` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git interpret-trailers --no-in-place
printf 'exit=%s\n' "$?"
```

### `--no-trim-empty`

Desactiva para esta invocación el comportamiento que habilita `--trim-empty`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git interpret-trailers --no-trim-empty
printf 'exit=%s\n' "$?"
```

### `--no-trailer`

Desactiva para esta invocación el comportamiento que habilita `--trailer`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git interpret-trailers --no-trailer
printf 'exit=%s\n' "$?"
```

### `--no-where`

Desactiva para esta invocación el comportamiento que habilita `--where`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git interpret-trailers --no-where
printf 'exit=%s\n' "$?"
```

### `--no-if-exists`

Desactiva para esta invocación el comportamiento que habilita `--if-exists`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git interpret-trailers --no-if-exists
printf 'exit=%s\n' "$?"
```

### `--no-if-missing`

Desactiva para esta invocación el comportamiento que habilita `--if-missing`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git interpret-trailers --no-if-missing
printf 'exit=%s\n' "$?"
```

### `--no-only-trailers`

Desactiva para esta invocación el comportamiento que habilita `--only-trailers`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git interpret-trailers --no-only-trailers
printf 'exit=%s\n' "$?"
```

### `--no-only-input`

Desactiva para esta invocación el comportamiento que habilita `--only-input`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git interpret-trailers` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git interpret-trailers --no-only-input
printf 'exit=%s\n' "$?"
```

### `--no-unfold`

Desactiva para esta invocación el comportamiento que habilita `--unfold`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git interpret-trailers --no-unfold
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git mailinfo`](../scripting-and-helpers/mailinfo.md)
- [`git hook`](../scripting-and-helpers/hook.md)
- [`git mailsplit`](../scripting-and-helpers/mailsplit.md)

## Fuente

- [git-interpret-trailers - Add or parse structured information in commit messages](https://git-scm.com/docs/git-interpret-trailers)
