---
title: "git rerere"
source: "https://git-scm.com/docs/git-rerere"
section: "branching-and-merging"
status: "source-audited"
version: "2.55.0"
---

# `git rerere`

Este caso usa `git rerere` para recordar resoluciones de conflictos y reutilizarlas.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git config rerere.enabled true
git rerere status
```

La invocación `git rerere status` ejecuta esta operación: recordar resoluciones de conflictos y reutilizarlas. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Sintaxis y formas de invocación

```text
git rerere [clear | forget <pathspec>… | diff | status | remaining | gc]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git rerere [clear | forget <pathspec>... | diff | status | remaining | gc]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git rerere -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--rerere-autoupdate`

Activa rerere autoupdate durante recordar resoluciones de conflictos y reutilizarlas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `register clean resolutions in index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rerere --rerere-autoupdate status
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git stash`](../branching-and-merging/stash.md)
- [`git refs`](../branching-and-merging/refs.md)
- [`git switch`](../branching-and-merging/switch.md)

## Fuente

- [git-rerere - Reuse recorded resolution of conflicted merges](https://git-scm.com/docs/git-rerere)
