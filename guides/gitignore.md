---
title: "gitignore"
source: "https://git-scm.com/docs/gitignore"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitignore`

Este caso usa `gitignore` para declarar patrones de archivos que Git debe dejar sin seguimiento.

La guía cubre **fuentes de patrones**, **precedencia**, **negación**, **directorios**, **diagnóstico con `check-ignore`**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```ini
# .gitignore
.env
node_modules/
build/*.log
!build/.gitkeep
```

La invocación `gitignore` ejecuta esta operación: declarar patrones de archivos que Git debe dejar sin seguimiento. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
# .gitignore
.env
node_modules/
build/*.log
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Fuentes

Las reglas pueden venir de argumentos, archivos del repositorio, exclusiones locales y configuración global.

```bash
git check-ignore -v
```

Usa `git check-ignore -v`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Precedencia

Dentro del mismo nivel gana la última regla que coincide.

Invierte dos reglas y repite la consulta. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Negación

`!` vuelve a incluir una ruta solo si Git puede recorrer sus directorios padre.

Prueba una exclusión de directorio y una excepción interna. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Rutas registradas

Una regla ignore no deja de seguir un archivo que ya está en el índice.

```bash
git ls-files --error-unmatch
```

Comprueba `git ls-files --error-unmatch`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Globos

Slash, doble asterisco y posición del patrón cambian el alcance.

Crea coincidencias en raíz y subdirectorios. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitmailmap`](../guides/gitmailmap.md)
- [`githooks`](../guides/githooks.md)
- [`gitmodules`](../guides/gitmodules.md)

## Fuente

- [gitignore - Specifies intentionally untracked files to ignore](https://git-scm.com/docs/gitignore)
