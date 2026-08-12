---
title: "gitworkflows"
source: "https://git-scm.com/docs/gitworkflows"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitworkflows`

Este caso usa `gitworkflows` para organizar ramas, integración y publicación en un equipo.

La guía cubre **ramas de integración**, **ramas temáticas**, **graduación de cambios**, **mantenimiento**, **publicación**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
main:          A---B-------M
                         /
tema-portada:     C---D
```

La invocación `gitworkflows` ejecuta esta operación: organizar ramas, integración y publicación en un equipo. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
git *
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Rama temática

Una rama temática contiene un cambio con base identificable.

Publica el punto base y el rango. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Integración

La rama de integración reúne cambios que ya pasaron la revisión definida.

Verifica ancestros antes de fusionar. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Graduación

Mover un tema entre ramas requiere conservar qué commits se probaron.

Compara rangos con `range-diff`. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Mantenimiento

Un mantenedor aplica, revierte o reemplaza temas bajo una política de publicación.

Registra referencias antes de reescribir. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Publicación

Las ramas publicadas establecen expectativas sobre reescritura y estabilidad.

Documenta cuáles aceptan force push. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitattributes`](../guides/gitattributes.md)
- [`gittutorial-2`](../guides/gittutorial-2.md)
- [`gitcli`](../guides/gitcli.md)

## Fuente

- [gitworkflows - An overview of recommended workflows with Git](https://git-scm.com/docs/gitworkflows)
