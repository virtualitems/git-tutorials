---
title: "githooks"
source: "https://git-scm.com/docs/githooks"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `githooks`

Este caso usa `githooks` para ejecutar programas en puntos definidos del flujo de Git.

La guía cubre **ubicación y descubrimiento**, **entrada por argumentos o stdin**, **entorno**, **códigos de salida**, **despliegue y pruebas**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```ini
# .git/hooks/pre-commit
#!/bin/sh
exec git diff --cached --check
```

La invocación `githooks` ejecuta esta operación: ejecutar programas en puntos definidos del flujo de Git. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
# .git/hooks/pre-commit
#!/bin/sh
exec git diff --cached --check
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Descubrimiento

Git busca hooks en `core.hooksPath` o en la ruta de hooks del repositorio.

```bash
git config --show-origin core.hooksPath
```

Consulta `git config --show-origin core.hooksPath`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Ejecución

El archivo debe poder ejecutarse y usar un intérprete disponible.

Invócalo con el mismo usuario que ejecuta Git. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Entrada

Cada hook define argumentos, stdin y variables; no comparten un contrato único.

Registra entradas en un repositorio de prueba. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Salida

Un código distinto de cero puede rechazar la operación cuando el hook lo define.

Prueba códigos 0 y 1 y observa la orden que lo llama. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Distribución

Los hooks no viajan con un clone por defecto.

Versiona una fuente y configura su instalación de forma explícita. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitignore`](../guides/gitignore.md)
- [`gitcli`](../guides/gitcli.md)
- [`gitmailmap`](../guides/gitmailmap.md)

## Fuente

- [githooks - Hooks used by Git](https://git-scm.com/docs/githooks)
