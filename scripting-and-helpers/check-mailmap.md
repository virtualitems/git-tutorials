---
title: "git check-mailmap"
source: "https://git-scm.com/docs/git-check-mailmap"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git check-mailmap`

Este caso usa `git check-mailmap` para convertir identidades mediante las reglas de mailmap.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git check-mailmap 'Ana <ana@correo-antiguo.test>'
```

La invocación `git check-mailmap 'Ana <ana@correo-antiguo.test>'` ejecuta esta operación: convertir identidades mediante las reglas de mailmap. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git check-mailmap [<options>] <contact>…
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git check-mailmap [<options>] <contact>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git check-mailmap -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git check-mailmap` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git check-mailmap --stdin 'Ana <ana@correo-antiguo.test>'
printf 'exit=%s\n' "$?"
```

### `--mailmap-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia cómo `git check-mailmap` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git check-mailmap --mailmap-file=rutas.txt 'Ana <ana@correo-antiguo.test>'
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mailmap-blob`

Lee mailmap blob como parte de la entrada de `git check-mailmap`. En Git 2.51.1, la ayuda corta expresa el contrato como `read additional mailmap entries from blob`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git check-mailmap --mailmap-blob=:archivo.txt 'Ana <ana@correo-antiguo.test>'
printf 'exit=%s\n' "$?"
```

El ejemplo usa `:archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git check-ref-format`](../scripting-and-helpers/check-ref-format.md)
- [`git check-ignore`](../scripting-and-helpers/check-ignore.md)
- [`git column`](../scripting-and-helpers/column.md)

## Fuente

- [git-check-mailmap - Show canonical names and email addresses of contacts](https://git-scm.com/docs/git-check-mailmap)
