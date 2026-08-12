---
title: "git verify-tag"
source: "https://git-scm.com/docs/git-verify-tag"
section: "inspection-and-comparison"
status: "source-audited"
version: "2.55.0"
---

# `git verify-tag`

Este caso usa `git verify-tag` para verificar la firma criptográfica de etiquetas.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Ejemplo mínimo

```bash
git verify-tag v1.0
```

La invocación `git verify-tag v1.0` ejecuta esta operación: verificar la firma criptográfica de etiquetas. Después, la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Sintaxis y formas de invocación

```text
git verify-tag [-v | --verbose] [--format=<format>] [--raw] <tag>…
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git verify-tag [-v | --verbose] [--format=<format>] [--raw] <tag>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git verify-tag -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git verify-tag --verbose v1.0
printf 'exit=%s\n' "$?"
```

### `--format`

Define los campos y separadores de la salida.

```bash
git verify-tag --format=oneline v1.0
printf 'exit=%s\n' "$?"
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--raw`

Incluye raw en la salida o cambia cómo `git verify-tag` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print raw gpg status output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git verify-tag --raw v1.0
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git whatchanged`](../inspection-and-comparison/whatchanged.md)
- [`git verify-commit`](../inspection-and-comparison/verify-commit.md)
- [`git show-branch`](../inspection-and-comparison/show-branch.md)

## Fuente

- [git-verify-tag - Check the GPG signature of tags](https://git-scm.com/docs/git-verify-tag)
