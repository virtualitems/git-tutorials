---
title: "githooks"
source: "https://git-scm.com/docs/githooks"
section: "guides"
status: "option-expanded"
---

# `githooks`

Este caso usa `githooks` para ejecutar programas en puntos definidos del flujo de Git. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **ubicación y descubrimiento**, **entrada por argumentos o stdin**, **entorno**, **códigos de salida**, **despliegue y pruebas**.

## Responsabilidad y efecto

githooks define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en ejecutar programas en puntos definidos del flujo de Git.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```ini
# .git/hooks/pre-commit
#!/bin/sh
exec ./scripts/verificar-formato.sh
```

La invocación `githooks` ejecuta esta operación: ejecutar programas en puntos definidos del flujo de Git. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
# .git/hooks/pre-commit
#!/bin/sh
exec ./scripts/verificar-formato.sh
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

ejecutar programas en puntos definidos del flujo de Git. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### ubicación y descubrimiento

Aplicar las reglas de ubicación y descubrimiento. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### entrada por argumentos o stdin

Aplicar las reglas de entrada por argumentos o stdin. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### entorno

Aplicar las reglas de entorno. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### códigos de salida

Aplicar las reglas de códigos de salida. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### despliegue y pruebas

Aplicar las reglas de despliegue y pruebas. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

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

- [`gitignore`](../guides/gitignore.md)
- [`gitcli`](../guides/gitcli.md)
- [`gitmailmap`](../guides/gitmailmap.md)

## Fuente

- [githooks - Hooks used by Git](https://git-scm.com/docs/githooks)
