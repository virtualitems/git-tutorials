---
title: "git sparse-checkout"
source: "https://git-scm.com/docs/git-sparse-checkout"
section: "getting-and-creating-projects"
status: "source-audited"
version: "2.55.0"
---

# `git sparse-checkout`

Este caso usa `git sparse-checkout` para materializar solo una parte de los archivos seguidos.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un repositorio contiene objetos y referencias. Un área de trabajo materializa un commit para que los archivos puedan editarse.

Separa los datos del repositorio de los archivos materializados. Un repositorio bare conserva objetos y referencias sin área de trabajo.

## Ejemplo mínimo

```bash
git sparse-checkout init --cone
git sparse-checkout set app docs
```

La invocación `git sparse-checkout init --cone` ejecuta esta operación: materializar solo una parte de los archivos seguidos. Después, el directorio resultante contiene el repositorio y, cuando corresponde, un área de trabajo.

## Sintaxis y formas de invocación

```text
git sparse-checkout (init | list | set | add | reapply | disable | check-rules | clean) [<options>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git sparse-checkout (init | list | set | add | reapply | disable | check-rules) [<options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git sparse-checkout -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-h`

Activa h durante materializar solo una parte de los archivos seguidos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git sparse-checkout -h
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git clone`](../getting-and-creating-projects/clone.md)
- [`git init`](../getting-and-creating-projects/init.md)

## Fuente

- [git-sparse-checkout - Reduce your working tree to a subset of tracked files](https://git-scm.com/docs/git-sparse-checkout)
