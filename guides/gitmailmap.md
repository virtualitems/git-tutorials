---
title: "gitmailmap"
source: "https://git-scm.com/docs/gitmailmap"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitmailmap`

Este caso usa `gitmailmap` para unificar nombres y correos que representan a una misma persona.

La guía cubre **formatos de entrada**, **correo canónico**, **nombre canónico**, **precedencia**, **consultas y logs**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
Ana Torres <user@example.com> <user-old@example.com>
```

La invocación `gitmailmap` ejecuta esta operación: unificar nombres y correos que representan a una misma persona. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
Ana Torres <user@example.com> <user-old@example.com>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Identidad

Una entrada asocia nombre o correo observado con una identidad canónica.

```bash
git check-mailmap
```

Ejecuta `git check-mailmap` con la identidad original. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Formas

El formato permite corregir nombre, correo o ambos según los campos presentes.

Prueba cada forma sobre datos de laboratorio. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Archivos

Git puede leer `.mailmap` y ubicaciones configuradas.

Consulta la configuración y ejecuta desde otra ruta. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Historial

La mailmap cambia presentación, no reescribe commits.

```bash
git cat-file -p
```

Compara `git cat-file -p` con `git log --use-mailmap`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Automatización

Los formatos de log pueden aplicar mailmap a campos concretos.

Declara el placeholder y valida el correo emitido. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitmodules`](../guides/gitmodules.md)
- [`gitignore`](../guides/gitignore.md)
- [`gitrepository-layout`](../guides/gitrepository-layout.md)

## Fuente

- [gitmailmap - Map author/committer names and/or E-Mail addresses](https://git-scm.com/docs/gitmailmap)
