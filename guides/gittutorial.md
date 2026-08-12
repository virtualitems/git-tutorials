---
title: "gittutorial"
source: "https://git-scm.com/docs/gittutorial"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gittutorial`

Este caso usa `gittutorial` para recorrer el ciclo de crear, registrar, inspeccionar y compartir cambios.

La guía cubre **creación del repositorio**, **snapshots**, **historial**, **ramas**, **intercambio**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
git init -b main
printf 'Biblioteca\n' > README.md
git add README.md
git commit -m "Inicia el proyecto"
```

La invocación `gittutorial` ejecuta esta operación: recorrer el ciclo de crear, registrar, inspeccionar y compartir cambios. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
git *
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Inicio

`git init` crea la base del repositorio en una ruta.

Confirma la raíz y el directorio Git. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Snapshot

Add copia contenido al índice y commit registra el tree resultante.

Compara diff de trabajo y diff cached. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Historial

Log recorre commits desde una revisión.

Dibuja el grafo con decoraciones. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Rama

Una rama mueve una referencia; cambiar de rama cambia HEAD y puede cambiar archivos.

Comprueba status antes y después. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Intercambio

Fetch descarga y actualiza referencias remotas; la integración es un paso separado.

Compara referencias locales y remotas. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gittutorial-2`](../guides/gittutorial-2.md)
- [`gitsubmodules`](../guides/gitsubmodules.md)
- [`gitworkflows`](../guides/gitworkflows.md)

## Fuente

- [gittutorial - A tutorial introduction to Git](https://git-scm.com/docs/gittutorial)
