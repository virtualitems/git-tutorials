---
title: "git verify-commit"
source: "https://git-scm.com/docs/git-verify-commit"
section: "inspection-and-comparison"
status: "source-audited"
version: "2.55.0"
---

# `git verify-commit`

Este caso usa `git verify-commit` para verificar la firma criptográfica de commits.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Ejemplo mínimo

```bash
git verify-commit HEAD
```

La invocación `git verify-commit HEAD` ejecuta esta operación: verificar la firma criptográfica de commits. Después, la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Sintaxis y formas de invocación

```text
git verify-commit [-v | --verbose] [--raw] <commit>…
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git verify-commit [-v | --verbose] [--raw] <commit>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git verify-commit -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git verify-commit --verbose HEAD
printf 'exit=%s\n' "$?"
```

### `--raw`

Incluye raw en la salida o cambia cómo `git verify-commit` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print raw gpg status output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git verify-commit --raw HEAD
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git verify-tag`](../inspection-and-comparison/verify-tag.md)
- [`git show-branch`](../inspection-and-comparison/show-branch.md)
- [`git whatchanged`](../inspection-and-comparison/whatchanged.md)

## Fuente

- [git-verify-commit - Check the GPG signature of commits](https://git-scm.com/docs/git-verify-commit)
