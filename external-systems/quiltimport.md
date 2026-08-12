---
title: "git quiltimport"
source: "https://git-scm.com/docs/git-quiltimport"
section: "external-systems"
status: "source-audited"
version: "2.55.0"
---

# `git quiltimport`

Este caso usa `git quiltimport` para importar una serie de parches administrada por quilt.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Ejemplo mínimo

```bash
git quiltimport --patches parches
```

La invocación `git quiltimport --patches parches` ejecuta esta operación: importar una serie de parches administrada por quilt. Después, el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Sintaxis y formas de invocación

```text
git quiltimport [--dry-run | -n] [--author <author>] [--patches <dir>]
		[--series <file>] [--keep-non-patch]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git quiltimport [options]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git quiltimport -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--dry-run` y `-n`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

#### Ejemplo con `--dry-run`

```bash
git quiltimport --dry-run --patches parches
printf 'exit=%s\n' "$?"
```

### `--author`

Limita el resultado a autores que coinciden con el patrón indicado. En Git 2.51.1, la ayuda corta expresa el contrato como `author name and email address for patches without any`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git quiltimport --author --patches parches
printf 'exit=%s\n' "$?"
```

### `--patches`

Define patches con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `path to the quilt patches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git quiltimport --patches parches
printf 'exit=%s\n' "$?"
```

### `--series`

Define series con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `path to the quilt series file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git quiltimport` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git quiltimport --series --patches parches
printf 'exit=%s\n' "$?"
```

### `--keep-non-patch` y `-b`

Activa conservar non parche durante importar una serie de parches administrada por quilt. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

#### Ejemplo con `--keep-non-patch`

```bash
git quiltimport --keep-non-patch --patches parches
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git svn`](../external-systems/svn.md)
- [`git p4`](../external-systems/p4.md)
- [`git fast-import`](../external-systems/fast-import.md)

## Fuente

- [git-quiltimport - Applies a quilt patchset onto the current branch](https://git-scm.com/docs/git-quiltimport)
