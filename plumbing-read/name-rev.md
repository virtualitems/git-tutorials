---
title: "git name-rev"
source: "https://git-scm.com/docs/git-name-rev"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git name-rev`

Este caso usa `git name-rev` para expresar identificadores mediante nombres relativos a referencias.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git name-rev --name-only HEAD~3
```

La invocación `git name-rev --name-only HEAD~3` ejecuta esta operación: expresar identificadores mediante nombres relativos a referencias. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git name-rev [--tags] [--refs=<pattern>]
	       ( --all | --annotate-stdin | <commit-ish>… )
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git name-rev [<options>] <commit>...
   or: git name-rev [<options>] --all
   or: git name-rev [<options>] --annotate-stdin
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git name-rev -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--tags`

Incluye o selecciona etiquetas según la operación.

```bash
git name-rev --tags --name-only HEAD~3
printf 'exit=%s\n' "$?"
```

### `--refs`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git name-rev --refs=TODO --name-only HEAD~3
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git name-rev --all --name-only HEAD~3
printf 'exit=%s\n' "$?"
```

### `--annotate-stdin`

Lee annotate entrada estándar como parte de la entrada de `git name-rev`.

La opción cambia cómo `git name-rev` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git name-rev --annotate-stdin --name-only HEAD~3
printf 'exit=%s\n' "$?"
```

### `--name-only`

Muestra nombres de ruta sin el contenido del diff.

```bash
git name-rev --name-only HEAD~3
printf 'exit=%s\n' "$?"
```

### `--exclude`

Excluye elementos que cumplan la condición indicada.

```bash
git name-rev --exclude=TODO --name-only HEAD~3
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--undefined`

Permite undefined cuando la forma predeterminada de `git name-rev` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow to print `undefined` names (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git name-rev --undefined --name-only HEAD~3
printf 'exit=%s\n' "$?"
```

### `--always`

Incluye always en la salida o cambia cómo `git name-rev` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show abbreviated commit object as fallback`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git name-rev --always --name-only HEAD~3
printf 'exit=%s\n' "$?"
```

### `--no-refs`

Desactiva para esta invocación el comportamiento que habilita `--refs`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git name-rev --no-refs --name-only HEAD~3
printf 'exit=%s\n' "$?"
```

### `--no-exclude`

Desactiva para esta invocación el comportamiento que habilita `--exclude`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git name-rev --no-exclude --name-only HEAD~3
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git pack-redundant`](../plumbing-read/pack-redundant.md)
- [`git merge-base`](../plumbing-read/merge-base.md)
- [`git repo`](../plumbing-read/repo.md)

## Fuente

- [git-name-rev - Find symbolic names for given revs](https://git-scm.com/docs/git-name-rev)
