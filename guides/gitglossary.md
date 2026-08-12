---
title: "gitglossary"
source: "https://git-scm.com/docs/gitglossary"
section: "guides"
status: "option-expanded"
---

# `gitglossary`

Este caso usa `gitglossary` para relacionar los términos usados por la documentación de Git. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **objetos**, **referencias**, **índice y worktree**, **revisiones**, **pathspecs**.

## Responsabilidad y efecto

gitglossary define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en relacionar los términos usados por la documentación de Git.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```text
HEAD -> refs/heads/main -> commit -> tree -> blob
```

La invocación `gitglossary` ejecuta esta operación: relacionar los términos usados por la documentación de Git. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
HEAD -> refs/heads/main -> commit -> tree -> blob
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

relacionar los términos usados por la documentación de Git. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### objetos

Aplicar las reglas de objetos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### referencias

Aplicar las reglas de referencias. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### índice y worktree

Aplicar las reglas de índice y worktree. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### revisiones

Aplicar las reglas de revisiones. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### pathspecs

Aplicar las reglas de pathspecs. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

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

- [`gitnamespaces`](../guides/gitnamespaces.md)
- [`gitfaq`](../guides/gitfaq.md)
- [`gitremote-helpers`](../guides/gitremote-helpers.md)

## Fuente

- [gitglossary - A Git Glossary](https://git-scm.com/docs/gitglossary)
