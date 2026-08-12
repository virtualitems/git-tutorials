---
title: "git bisect"
source: "https://git-scm.com/docs/git-bisect"
section: "debugging"
status: "source-audited"
version: "2.55.0"
---

# `git bisect`

Este caso usa `git bisect` para localizar por búsqueda binaria el commit que introdujo un cambio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La búsqueda combina revisiones, rutas y contenido. Primero delimita el conjunto de commits o archivos; después interpreta la evidencia que devuelve Git.

Reduce primero el rango y las rutas. Después interpreta cada coincidencia dentro de ese conjunto, sin atribuir significado a elementos que quedaron fuera.

## Ejemplo mínimo

```bash
git bisect start
git bisect bad
git bisect good v1.0
git bisect run ./prueba.sh
git bisect reset
```

La invocación `git bisect start` ejecuta esta operación: localizar por búsqueda binaria el commit que introdujo un cambio. Después, la salida identifica líneas, archivos o commits que cumplen el criterio.

## Sintaxis y formas de invocación

```text
git bisect start [--term-(bad|new)=<term-new> --term-(good|old)=<term-old>]
		 [--no-checkout] [--first-parent] [<bad> [<good>…]] [--] [<pathspec>…]
git bisect (bad|new|<term-new>) [<rev>]
git bisect (good|old|<term-old>) [<rev>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git bisect start [--term-(new|bad)=<term> --term-(old|good)=<term>]    [--no-checkout] [--first-parent] [<bad> [<good>...]] [--]    [<pathspec>...]
   or: git bisect (good|bad) [<rev>...]
   or: git bisect terms [--term-good | --term-bad]
   or: git bisect skip [(<rev>|<range>)...]
   or: git bisect next
   or: git bisect reset [<commit>]
   or: git bisect visualize
   or: git bisect replay <logfile>
   or: git bisect log
   or: git bisect run <cmd> [<arg>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git bisect -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--term-`

Activa term durante localizar por búsqueda binaria el commit que introdujo un cambio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git bisect --term- start
printf 'exit=%s\n' "$?"
```

### `--no-checkout`

Desactiva el comportamiento `checkout` para esta invocación.

```bash
git bisect --no-checkout start
printf 'exit=%s\n' "$?"
```

### `--first-parent`

Activa first parent durante localizar por búsqueda binaria el commit que introdujo un cambio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git bisect --first-parent start
printf 'exit=%s\n' "$?"
```

### `--term-good`

Activa term good durante localizar por búsqueda binaria el commit que introdujo un cambio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git bisect --term-good start
printf 'exit=%s\n' "$?"
```

### `--term-bad`

Activa term bad durante localizar por búsqueda binaria el commit que introdujo un cambio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git bisect --term-bad start
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git blame`](../debugging/blame.md)
- [`git annotate`](../debugging/annotate.md)
- [`git grep`](../debugging/grep.md)

## Fuente

- [git-bisect - Use binary search to find the commit that introduced a bug](https://git-scm.com/docs/git-bisect)
