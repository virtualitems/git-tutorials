---
title: "git check-attr"
source: "https://git-scm.com/docs/git-check-attr"
section: "scripting-and-helpers"
status: "source-audited"
version: "2.55.0"
---

# `git check-attr`

Este caso usa `git check-attr` para consultar los atributos que se aplican a una ruta.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git check-attr diff text -- informe.bin
```

La invocación `git check-attr diff text -- informe.bin` ejecuta esta operación: consultar los atributos que se aplican a una ruta. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Sintaxis y formas de invocación

```text
git check-attr [--source <tree-ish>] [-a | --all | <attr>…] [--] <pathname>…
git check-attr --stdin [-z] [--source <tree-ish>] [-a | --all | <attr>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git check-attr [--source <tree-ish>] [-a | --all | <attr>...] [--] <pathname>...
   or: git check-attr --stdin [-z] [--source <tree-ish>] [-a | --all | <attr>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git check-attr -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--source`

Comprueba source antes de aceptar el resultado de `git check-attr`. En Git 2.51.1, la ayuda corta expresa el contrato como `which tree-ish to check attributes at`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git check-attr --source=HEAD^{tree} diff text -- informe.bin
printf 'exit=%s\n' "$?"
```

El ejemplo usa `HEAD^{tree}` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a` y `--all`

Amplía la selección a todos los elementos del alcance definido.

#### Ejemplo con `--all`

```bash
git check-attr --all diff text -- informe.bin
printf 'exit=%s\n' "$?"
```

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git check-attr` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git check-attr --stdin diff text -- informe.bin
printf 'exit=%s\n' "$?"
```

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git check-attr -z diff text -- informe.bin
printf 'exit=%s\n' "$?"
```

### `--cached`

Usa el índice como origen o destino, sin tratar el área de trabajo de la misma forma.

```bash
git check-attr --cached diff text -- informe.bin
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git check-ignore`](../scripting-and-helpers/check-ignore.md)
- [`git check-mailmap`](../scripting-and-helpers/check-mailmap.md)

## Fuente

- [git-check-attr - Display gitattributes information](https://git-scm.com/docs/git-check-attr)
