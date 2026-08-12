---
title: "gitcvs-migration"
source: "https://git-scm.com/docs/gitcvs-migration"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitcvs-migration`

Este caso usa `gitcvs-migration` para trasladar prácticas y datos de CVS a Git.

La guía cubre **inventario del repositorio CVS**, **conversión de ramas y etiquetas**, **mapeo de autores**, **validación de contenido**, **corte de migración**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```bash
git cvsimport -C biblioteca modulo
cd biblioteca
git log --oneline --all
```

La invocación `gitcvs-migration` ejecuta esta operación: trasladar prácticas y datos de CVS a Git. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
git cvsimport *
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Inventario

La migración identifica módulos, ramas, etiquetas, autores y archivos binarios antes de convertir.

Registra conteos del origen. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Autores

Un mapa estable convierte identidades de CVS a nombres y correos de Git.

Busca autores sin correspondencia en el historial convertido. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Ramas

Las ramas y etiquetas se validan por nombre, punto de creación y contenido.

Compara el tip de cada línea con el origen. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Contenido

La validación compara snapshots y no solo cantidad de commits.

Exporta revisiones equivalentes y calcula checksums. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Corte

El cambio de sistema requiere un último punto de importación y un periodo sin escrituras.

Documenta el identificador final de CVS y el commit resultante. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitdiffcore`](../guides/gitdiffcore.md)
- [`gitcredentials`](../guides/gitcredentials.md)
- [`giteveryday`](../guides/giteveryday.md)

## Fuente

- [gitcvs-migration - Git for CVS users](https://git-scm.com/docs/gitcvs-migration)
