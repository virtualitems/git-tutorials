---
title: "gitmailmap"
source: "https://git-scm.com/docs/gitmailmap"
section: "guides"
status: "option-expanded"
---

# `gitmailmap`

Este caso usa `gitmailmap` para unificar nombres y correos que representan a una misma persona. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **formatos de entrada**, **correo canónico**, **nombre canónico**, **precedencia**, **consultas y logs**.

## Responsabilidad y efecto

gitmailmap define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en unificar nombres y correos que representan a una misma persona.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
Ana Torres <ana@example.test> <ana@correo-antiguo.test>
```

La invocación `gitmailmap` ejecuta esta operación: unificar nombres y correos que representan a una misma persona. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
Ana Torres <ana@example.test> <ana@correo-antiguo.test>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

unificar nombres y correos que representan a una misma persona. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### formatos de entrada

Aplicar las reglas de formatos de entrada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### correo canónico

Aplicar las reglas de correo canónico. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### nombre canónico

Aplicar las reglas de nombre canónico. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### precedencia

Aplicar las reglas de precedencia. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### consultas y logs

Aplicar las reglas de consultas y logs. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

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

- [`gitmodules`](../guides/gitmodules.md)
- [`gitignore`](../guides/gitignore.md)
- [`gitrepository-layout`](../guides/gitrepository-layout.md)

## Fuente

- [gitmailmap - Map author/committer names and/or E-Mail addresses](https://git-scm.com/docs/gitmailmap)
