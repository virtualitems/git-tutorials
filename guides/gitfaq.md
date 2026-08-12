---
title: "gitfaq"
source: "https://git-scm.com/docs/gitfaq"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitfaq`

Este caso usa `gitfaq` para resolver preguntas sobre configuración, historial y archivos.

La guía cubre **recuperación**, **configuración**, **rutas y nombres**, **credenciales**, **interoperabilidad**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
git add README.md
git restore --staged README.md
git status --short
```

La invocación `gitfaq` ejecuta esta operación: resolver preguntas sobre configuración, historial y archivos. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
git add README.md
git restore --staged README.md
git status --short
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Recuperación

El reflog permite localizar valores anteriores de referencias mientras no hayan vencido.

Busca el hash y crea una rama antes de mantenimiento. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Configuración

`--show-origin` identifica qué archivo aportó un valor.

Consulta todas las apariciones de la clave. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Rutas

Git registra rutas y el shell decide la expansión inicial de argumentos.

Usa `--` y una ruta con espacios. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Credenciales

Los helpers reciben contexto y secreto por un protocolo separado de la URL.

Evita secretos en argumentos y remotos. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Historial

Cambiar un commit cambia sus descendientes porque el identificador incluye el padre.

Compara hashes antes y después de un rebase. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--staged`

Selecciona el contenido preparado en el índice.

```bash
git restore --staged README.md
printf 'exit=%s\n' "$?"
```

El ejemplo usa `README.md` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--short`

Activa short durante resolver preguntas sobre configuración, historial y archivos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git status --short
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`gitglossary`](../guides/gitglossary.md)
- [`giteveryday`](../guides/giteveryday.md)
- [`gitnamespaces`](../guides/gitnamespaces.md)

## Fuente

- [gitfaq - Frequently asked questions about using Git](https://git-scm.com/docs/gitfaq)
