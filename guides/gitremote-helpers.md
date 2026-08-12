---
title: "gitremote-helpers"
source: "https://git-scm.com/docs/gitremote-helpers"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitremote-helpers`

Este caso usa `gitremote-helpers` para implementar transportes mediante procesos auxiliares.

La guía cubre **descubrimiento del helper**, **capacidades**, **comandos y respuestas**, **flujo de importación o exportación**, **errores de protocolo**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
git remote add datos transporte::direccion
git fetch datos
# Git busca un ejecutable llamado git-remote-transporte
```

La invocación `gitremote-helpers` ejecuta esta operación: implementar transportes mediante procesos auxiliares. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
git remote-<transport> <repository> [<URL>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Descubrimiento

Una URL con transporte no integrado puede activar `git-remote-<transporte>`.

Comprueba el ejecutable en PATH. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Capacidades

El helper anuncia funciones antes de recibir comandos que dependan de ellas.

Registra el intercambio hasta la línea vacía. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Lista

La respuesta list comunica referencias y atributos del remoto.

Valida nombres y OID antes de importar. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Importar o exportar

El helper intercambia fast-import, fast-export o conecta transporte según capacidades.

Prueba un repositorio con una referencia. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Errores

Un protocolo incompleto puede dejar al proceso esperando terminación.

Valida líneas vacías, flushing y cierre de canales. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitsubmodules`](../guides/gitsubmodules.md)
- [`gitnamespaces`](../guides/gitnamespaces.md)
- [`gittutorial`](../guides/gittutorial.md)

## Fuente

- [gitremote-helpers - Helper programs to interact with remote repositories](https://git-scm.com/docs/gitremote-helpers)
