---
title: "git history"
source: "https://git-scm.com/docs/git-history"
section: "branching-and-merging"
status: "source-audited"
version: "2.55.0"
---

# `git history`

Este caso usa `git history` para reescribir commits con operaciones de corrección, mensaje o división.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git history reword HEAD~2 --dry-run
```

La invocación `git history reword HEAD~2 --dry-run` ejecuta esta operación: reescribir commits con operaciones de corrección, mensaje o división. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Sintaxis y formas de invocación

```text
git history fixup <commit> [--dry-run] [--update-refs=(branches|head)] [--reedit-message] [--empty=(drop|keep|abort)]
git history reword <commit> [--dry-run] [--update-refs=(branches|head)]
git history split <commit> [--dry-run] [--update-refs=(branches|head)] [--] [<pathspec>…]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git history -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

```bash
git history --dry-run reword HEAD~2
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--update-refs`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git history --update-refs reword HEAD~2 --dry-run
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reedit-message`

Reutiliza un mensaje existente y abre el editor antes de confirmar.

```bash
git history --reedit-message reword HEAD~2 --dry-run
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--empty`

Activa vacío durante reescribir commits con operaciones de corrección, mensaje o división. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git history --empty reword HEAD~2 --dry-run
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--help`

Muestra la ayuda correspondiente a la versión instalada.

```bash
git history --help
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git merge`](../branching-and-merging/merge.md)
- [`git checkout`](../branching-and-merging/checkout.md)
- [`git mergetool`](../branching-and-merging/mergetool.md)

## Fuente

- [git-history - EXPERIMENTAL: Rewrite history](https://git-scm.com/docs/git-history)
