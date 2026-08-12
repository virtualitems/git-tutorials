---
title: "gitcredentials"
source: "https://git-scm.com/docs/gitcredentials"
section: "guides"
status: "option-expanded"
---

# `gitcredentials`

Este caso usa `gitcredentials` para configurar la obtención y el almacenamiento de credenciales. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

La guía cubre **contexto de credencial**, **acciones `fill`, `approve` y `reject`**, **cascada de helpers**, **entrada y salida por pares clave-valor**, **protección del secreto**.

## Responsabilidad y efecto

gitcredentials define reglas compartidas por comandos, archivos y flujos de trabajo. Recibe como entrada el estado de repositorio representado por el caso. La operación consiste en configurar la obtención y el almacenamiento de credenciales.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
git config --global credential.helper 'cache --timeout=900'
git config --show-origin --get-all credential.helper
```

La invocación `gitcredentials` ejecuta esta operación: configurar la obtención y el almacenamiento de credenciales. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git config credential.https://example.com.username myusername
git config credential.helper "$helper $options"
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

configurar la obtención y el almacenamiento de credenciales. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### contexto de credencial

Aplicar las reglas de contexto de credencial. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### acciones `fill`, `approve` y `reject`

Aplicar las reglas de acciones `fill`, `approve` y `reject`. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### cascada de helpers

Aplicar las reglas de cascada de helpers. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### entrada y salida por pares clave-valor

Aplicar las reglas de entrada y salida por pares clave-valor. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

### protección del secreto

Aplicar las reglas de protección del secreto. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Cambia una entrada y comprueba el efecto que define la guía.

## Funciones y reglas

### Contexto

El protocolo describe URL mediante campos como protocol, host, path y username.

```bash
git credential fill
```

Envía el contexto a `git credential fill` sin registrar el secreto. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Fill

`fill` consulta configuración y helpers hasta completar una credencial o fallar.

Captura los campos devueltos y elimina el password del registro. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Approve

`approve` notifica a los helpers que una credencial funcionó.

Usa un helper de laboratorio y comprueba su almacenamiento. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Reject

`reject` solicita retirar una credencial que falló.

Consulta de nuevo el helper y confirma que no devuelve la entrada. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Terminación

Cada solicitud termina con una línea vacía.

```bash
printf
```

Prueba el protocolo con `printf` y confirma que el proceso no queda esperando. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

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

- [`gitcvs-migration`](../guides/gitcvs-migration.md)
- [`gitcore-tutorial`](../guides/gitcore-tutorial.md)
- [`gitdiffcore`](../guides/gitdiffcore.md)

## Fuente

- [gitcredentials - Providing usernames and passwords to Git](https://git-scm.com/docs/gitcredentials)
