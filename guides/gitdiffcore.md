---
title: "gitdiffcore"
source: "https://git-scm.com/docs/gitdiffcore"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitdiffcore`

Este caso usa `gitdiffcore` para entender las transformaciones que producen la salida de diff.

La guía cubre **pares de archivos**, **detección de ruptura**, **renombres y copias**, **selección por contenido**, **orden de salida**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
git diff -M -C --find-copies-harder HEAD~1 HEAD
```

La invocación `gitdiffcore` ejecuta esta operación: entender las transformaciones que producen la salida de diff. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
git diff *
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Pares

El motor recibe pares de archivos antes y después y transforma esa lista.

Observa `--raw` para identificar modos y hashes. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Ruptura

La detección de ruptura puede convertir una modificación extensa en borrado y creación.

Varía el umbral de `-B` sobre el mismo cambio. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Renombres

La detección relaciona un origen borrado con un destino creado por similitud.

Compara salida con y sin `-M`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Copias

La detección de copia busca un origen cuyo contenido explique el destino.

Compara salida con `-C` y un origen sin cambios. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Pickaxe

`-S` y `-G` seleccionan cambios por variación de texto o coincidencia en el parche.

Prueba ambos criterios sobre el mismo commit. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`giteveryday`](../guides/giteveryday.md)
- [`gitcvs-migration`](../guides/gitcvs-migration.md)
- [`gitfaq`](../guides/gitfaq.md)

## Fuente

- [gitdiffcore - Tweaking diff output](https://git-scm.com/docs/gitdiffcore)
