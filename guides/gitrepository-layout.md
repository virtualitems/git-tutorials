---
title: "gitrepository-layout"
source: "https://git-scm.com/docs/gitrepository-layout"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitrepository-layout`

Este caso usa `gitrepository-layout` para identificar los archivos y directorios internos de un repositorio.

La guía cubre **directorio Git**, **objetos y packs**, **referencias y reflogs**, **índice**, **archivos de estado transitorio**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
biblioteca/
├── .git/
│   ├── HEAD
│   ├── config
│   ├── index
│   ├── objects/
│   └── refs/
└── README.md
```

La invocación `gitrepository-layout` ejecuta esta operación: identificar los archivos y directorios internos de un repositorio. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
biblioteca/
├── .git/
│   ├── HEAD
│   ├── config
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Objetos

`objects` guarda objetos sueltos, packs y alternates.

Usa comandos de plomería; no edites los archivos. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Referencias

`refs` y `packed-refs` representan nombres; reflogs registran movimientos cuando están activos.

Compara `show-ref` y `reflog`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Índice

`index` representa el próximo tree y puede contener etapas de conflicto.

Ejecuta `ls-files --stage`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Estado transitorio

Archivos como `MERGE_HEAD` o directorios de rebase describen una operación pausada.

```bash
git status
```

Usa `git status` para elegir continuación o aborto. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Worktrees

Repositorios con worktrees separan datos comunes de datos por worktree.

```bash
git rev-parse --git-common-dir --git-path HEAD
```

Consulta `git rev-parse --git-common-dir --git-path HEAD`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitrevisions`](../guides/gitrevisions.md)
- [`gitmodules`](../guides/gitmodules.md)
- [`gitmailmap`](../guides/gitmailmap.md)

## Fuente

- [gitrepository-layout - Git Repository Layout](https://git-scm.com/docs/gitrepository-layout)
