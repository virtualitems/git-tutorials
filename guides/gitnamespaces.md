---
title: "gitnamespaces"
source: "https://git-scm.com/docs/gitnamespaces"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitnamespaces`

Este caso usa `gitnamespaces` para aislar conjuntos de referencias dentro de un repositorio servidor.

La guía cubre **aislamiento de referencias**, **selección de namespace**, **servicios de transporte**, **alcance de objetos**, **operación en servidor**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
GIT_NAMESPACE=curso-a git upload-pack /srv/git/biblioteca.git
GIT_NAMESPACE=curso-b git upload-pack /srv/git/biblioteca.git
```

La invocación `gitnamespaces` ejecuta esta operación: aislar conjuntos de referencias dentro de un repositorio servidor. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
GIT_NAMESPACE=<namespace> git upload-pack
GIT_NAMESPACE=<namespace> git receive-pack
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Prefijo

Un namespace inserta un prefijo interno en las referencias visibles.

```bash
git show-ref
```

Compara `git show-ref` con y sin `GIT_NAMESPACE`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Objetos

Los objetos se comparten aunque las referencias queden separadas.

Resuelve un hash conocido bajo dos namespaces. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Transporte

Los procesos de servidor pueden seleccionar namespace por solicitud o configuración.

Clona dos vistas desde un servidor de prueba. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### HEAD

Cada namespace puede exponer referencias distintas y requiere un HEAD coherente.

Consulta el anuncio de referencias. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Administración

Eliminar un namespace afecta sus referencias, no implica borrar de inmediato objetos compartidos.

Ejecuta fsck antes de mantenimiento. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitremote-helpers`](../guides/gitremote-helpers.md)
- [`gitglossary`](../guides/gitglossary.md)
- [`gitsubmodules`](../guides/gitsubmodules.md)

## Fuente

- [gitnamespaces - Git namespaces](https://git-scm.com/docs/gitnamespaces)
