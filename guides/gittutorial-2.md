---
title: "gittutorial-2"
source: "https://git-scm.com/docs/gittutorial-2"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gittutorial-2`

Este caso usa `gittutorial-2` para relacionar el índice, los objetos y las referencias detrás de los comandos.

La guía cubre **objetos internos**, **árboles**, **commits**, **referencias**, **operaciones de bajo nivel**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
git cat-file -p HEAD
git cat-file -p HEAD^{tree}
git ls-files --stage
```

La invocación `gittutorial-2` ejecuta esta operación: relacionar el índice, los objetos y las referencias detrás de los comandos. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
git *
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Contenido

`hash-object` muestra cómo los bytes determinan un blob.

Cambia un byte y compara OID. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Índice

`update-index` prepara entradas con modo, OID y ruta.

Consulta etapas con `ls-files --stage`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Tree

`write-tree` serializa el estado resuelto del índice.

Inspecciona con `ls-tree`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Commit

`commit-tree` enlaza tree, padres y mensaje.

Consulta el objeto antes de crear una referencia. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Referencia

`update-ref` publica el commit bajo un nombre con control del valor anterior.

Verifica con `show-ref`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitworkflows`](../guides/gitworkflows.md)
- [`gittutorial`](../guides/gittutorial.md)
- [`gitattributes`](../guides/gitattributes.md)

## Fuente

- [gittutorial-2 - A tutorial introduction to Git: part two](https://git-scm.com/docs/gittutorial-2)
