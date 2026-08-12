---
title: "gitglossary"
source: "https://git-scm.com/docs/gitglossary"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitglossary`

Este caso usa `gitglossary` para relacionar los términos usados por la documentación de Git.

La guía cubre **objetos**, **referencias**, **índice y worktree**, **revisiones**, **pathspecs**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```text
HEAD -> refs/heads/main -> commit -> tree -> blob
```

La invocación `gitglossary` ejecuta esta operación: relacionar los términos usados por la documentación de Git. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
HEAD -> refs/heads/main -> commit -> tree -> blob
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Objeto

Blob, tree, commit y tag son objetos dirigidos por contenido.

```bash
git cat-file
```

Consulta tipo y tamaño con `git cat-file`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Referencia

Una referencia asigna un nombre a un identificador y puede tener reflog.

```bash
git show-ref
```

Inspecciona `git show-ref` y `git reflog`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Índice

El índice mantiene la propuesta de tree y etapas de conflicto.

```bash
git ls-files --stage
```

Ejecuta `git ls-files --stage`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Revisión

Una revisión es una expresión que Git resuelve a uno o varios objetos.

```bash
git rev-parse
```

Prueba la expresión con `git rev-parse`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Pathspec

Un pathspec limita rutas mediante prefijos, globos y firmas mágicas.

```bash
git ls-files --
```

Observa la selección con `git ls-files --`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitnamespaces`](../guides/gitnamespaces.md)
- [`gitfaq`](../guides/gitfaq.md)
- [`gitremote-helpers`](../guides/gitremote-helpers.md)

## Fuente

- [gitglossary - A Git Glossary](https://git-scm.com/docs/gitglossary)
