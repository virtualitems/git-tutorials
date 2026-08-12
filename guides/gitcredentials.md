---
title: "gitcredentials"
source: "https://git-scm.com/docs/gitcredentials"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitcredentials`

Este caso usa `gitcredentials` para configurar la obtención y el almacenamiento de credenciales.

La guía cubre **contexto de credencial**, **acciones `fill`, `approve` y `reject`**, **cascada de helpers**, **entrada y salida por pares clave-valor**, **protección del secreto**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
git config --global credential.helper 'cache --timeout=900'
git config --show-origin --get-all credential.helper
```

La invocación `gitcredentials` ejecuta esta operación: configurar la obtención y el almacenamiento de credenciales. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
git config credential.https://example.com.username myusername
git config credential.helper "$helper $options"
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

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

## Páginas relacionadas

- [`gitcvs-migration`](../guides/gitcvs-migration.md)
- [`gitcore-tutorial`](../guides/gitcore-tutorial.md)
- [`gitdiffcore`](../guides/gitdiffcore.md)

## Fuente

- [gitcredentials - Providing usernames and passwords to Git](https://git-scm.com/docs/gitcredentials)
