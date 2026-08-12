---
title: "gitrepository-layout"
source: "https://git-scm.com/docs/gitrepository-layout"
section: "guides"
status: "option-expanded"
---

# `gitrepository-layout`

Este caso usa `gitrepository-layout` para identificar los archivos y directorios internos de un repositorio. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **directorio Git**, **objetos y packs**, **referencias y reflogs**, **índice**, **archivos de estado transitorio**.

## Responsabilidad y efecto

gitrepository-layout define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en identificar los archivos y directorios internos de un repositorio.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

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

La invocación `gitrepository-layout` ejecuta esta operación: identificar los archivos y directorios internos de un repositorio. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
biblioteca/
├── .git/
│   ├── HEAD
│   ├── config
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

identificar los archivos y directorios internos de un repositorio. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### directorio Git

Aplicar las reglas de directorio Git. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### objetos y packs

Aplicar las reglas de objetos y packs. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### referencias y reflogs

Aplicar las reglas de referencias y reflogs. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### índice

Aplicar las reglas de índice. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### archivos de estado transitorio

Aplicar las reglas de archivos de estado transitorio. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

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

## Errores y diagnóstico

### La regla no se aplica

Comprueba esta causa: El patrón, alcance o precedencia no coincide. Consulta la regla efectiva y el archivo que la definió.

### Una revisión se interpreta como ruta

Comprueba esta causa: El nombre es ambiguo. Separa revisiones y rutas con `--`.

### El resultado cambia entre equipos

Comprueba esta causa: La regla vive en configuración no compartida. Decide qué parte debe versionarse en el repositorio.

## Automatización y recuperación

Persistencia: La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`gitrevisions`](../guides/gitrevisions.md)
- [`gitmodules`](../guides/gitmodules.md)
- [`gitmailmap`](../guides/gitmailmap.md)

## Fuente

- [gitrepository-layout - Git Repository Layout](https://git-scm.com/docs/gitrepository-layout)
