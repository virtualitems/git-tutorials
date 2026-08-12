---
title: "gitrevisions"
source: "https://git-scm.com/docs/gitrevisions"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitrevisions`

Este caso usa `gitrevisions` para seleccionar commits y rangos mediante la sintaxis de revisiones.

La guía cubre **objetos nombrados**, **sufijos de alcance**, **ancestros**, **rangos de dos y tres puntos**, **exclusiones**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Revisiones y rangos

Una revisión resuelve un objeto. `HEAD` nombra el commit actual. `main` resuelve la referencia de esa rama. `HEAD^` selecciona el primer padre y `HEAD~2` sigue dos veces el primer padre. Comprueba cada expresión antes de usarla en una orden que escriba estado.

```bash
git rev-parse --verify HEAD
git rev-parse --verify HEAD^
```

`A..B` selecciona commits alcanzables desde `B` que no son alcanzables desde `A`. `A...B` selecciona la diferencia simétrica respecto de las bases de fusión. La guía explica esas expresiones junto a ancestros, reflogs, tags anotados y exclusiones.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
git show HEAD~2
git log main..tema-portada
git diff v1.0...main
```

La invocación `gitrevisions` ejecuta esta operación: seleccionar commits y rangos mediante la sintaxis de revisiones. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
git show HEAD~2
git log main..tema-portada
git diff v1.0...main
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Nombre

Ramas, etiquetas, reflogs y hashes pueden resolver un objeto.

```bash
git rev-parse --verify
```

Usa `git rev-parse --verify`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Ancestros

`^` selecciona padres y `~n` sigue el primer padre n veces.

Dibuja el grafo y resuelve cada expresión. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Peeled

`^{tipo}` exige desreferenciar hasta un tipo de objeto.

Prueba una etiqueta anotada. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Dos puntos

`A..B` selecciona commits alcanzables desde B y no desde A.

Compara con `rev-list B ^A`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Tres puntos

`A...B` selecciona la diferencia simétrica respecto a bases de fusión.

Calcula antes las bases con `merge-base --all`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitrepository-layout`](../guides/gitrepository-layout.md)
- [`gitmodules`](../guides/gitmodules.md)

## Fuente

- [gitrevisions - Specifying revisions and ranges for Git](https://git-scm.com/docs/gitrevisions)
