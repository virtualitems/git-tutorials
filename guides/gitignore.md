---
title: "gitignore"
source: "https://git-scm.com/docs/gitignore"
section: "guides"
status: "option-expanded"
---

# `gitignore`

Este caso usa `gitignore` para declarar patrones de archivos que Git debe dejar sin seguimiento. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **fuentes de patrones**, **precedencia**, **negación**, **directorios**, **diagnóstico con `check-ignore`**.

## Responsabilidad y efecto

gitignore define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en declarar patrones de archivos que Git debe dejar sin seguimiento.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

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

La invocación `gitignore` ejecuta esta operación: declarar patrones de archivos que Git debe dejar sin seguimiento. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
# .gitignore
.env
node_modules/
build/*.log
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

declarar patrones de archivos que Git debe dejar sin seguimiento. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### fuentes de patrones

Aplicar las reglas de fuentes de patrones. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### precedencia

Aplicar las reglas de precedencia. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### negación

Aplicar las reglas de negación. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### directorios

Aplicar las reglas de directorios. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### diagnóstico con `check-ignore`

Aplicar las reglas de diagnóstico con `check-ignore`. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

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

- [`gitmailmap`](../guides/gitmailmap.md)
- [`githooks`](../guides/githooks.md)
- [`gitmodules`](../guides/gitmodules.md)

## Fuente

- [gitignore - Specifies intentionally untracked files to ignore](https://git-scm.com/docs/gitignore)
