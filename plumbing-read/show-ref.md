---
title: "git show-ref"
source: "https://git-scm.com/docs/git-show-ref"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git show-ref`

Este caso usa `git show-ref` para enumerar o comprobar referencias del repositorio local.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git show-ref --heads --tags
git show-ref --verify refs/heads/main
```

La invocación `git show-ref --heads --tags` ejecuta esta operación: enumerar o comprobar referencias del repositorio local. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git show-ref [--head] [-d | --dereference]
	     [-s | --hash[=<n>]] [--abbrev[=<n>]] [--branches] [--tags]
	     [--] [<pattern>…]
git show-ref --verify [-q | --quiet] [-d | --dereference]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git show-ref [--head] [-d | --dereference]
                    [-s | --hash[=<n>]] [--abbrev[=<n>]] [--branches] [--tags]
                    [--] [<pattern>...]
   or: git show-ref --verify [-q | --quiet] [-d | --dereference]
                    [-s | --hash[=<n>]] [--abbrev[=<n>]]
                    [--] [<ref>...]
   or: git show-ref --exclude-existing[=<pattern>]
   or: git show-ref --exists <ref>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git show-ref -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--head`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git show-ref --head --heads --tags
printf 'exit=%s\n' "$?"
```

### `-d` y `--dereference`

Activa dereference durante enumerar o comprobar referencias del repositorio local. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `dereference tags into object IDs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--dereference`

```bash
git show-ref --dereference --heads --tags
printf 'exit=%s\n' "$?"
```

### `-s` y `--hash`

Selecciona la representación o tratamiento de identificadores de objeto.

#### Ejemplo con `--hash`

```bash
git show-ref --hash=5 --heads --tags
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--abbrev`

Reduce la representación visible del identificador sin cambiar el objeto.

```bash
git show-ref --abbrev=5 --heads --tags
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--branches` y `--tags`

Incluye o selecciona etiquetas según la operación.

#### Ejemplo con `--branches`

```bash
git show-ref --branches --heads
printf 'exit=%s\n' "$?"
```

#### Ejemplo con `--tags`

```bash
git show-ref --tags --heads
printf 'exit=%s\n' "$?"
```

### `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

```bash
git show-ref --verify --heads --tags
printf 'exit=%s\n' "$?"
```

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git show-ref --quiet --heads --tags
printf 'exit=%s\n' "$?"
```

### `--exclude-existing`

Excluye elementos que cumplan la condición indicada.

```bash
git show-ref --exclude-existing=TODO --heads --tags
printf 'exit=%s\n' "$?"
```

El ejemplo usa `TODO` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exists`

Comprueba exists antes de aceptar el resultado de `git show-ref`. En Git 2.51.1, la ayuda corta expresa el contrato como `check for reference existence without resolving`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git show-ref --exists --heads --tags
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git unpack-file`](../plumbing-read/unpack-file.md)
- [`git show-index`](../plumbing-read/show-index.md)
- [`git var`](../plumbing-read/var.md)

## Fuente

- [git-show-ref - List references in a local repository](https://git-scm.com/docs/git-show-ref)
