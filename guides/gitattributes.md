---
title: "gitattributes"
source: "https://git-scm.com/docs/gitattributes"
section: "guides"
status: "source-audited"
version: "2.55.0"
---

# `gitattributes`

Este caso usa `gitattributes` para asignar atributos a rutas para diff, merge, exportación y filtros.

La guía cubre **patrones y alcance**, **atributos `text` y `eol`**, **drivers de diff y merge**, **filtros `clean` y `smudge`**, **`export-ignore` y `export-subst`**.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Ejemplo mínimo

```ini
# .gitattributes
*.txt text eol=lf
*.bin binary
docs/*.md diff=markdown
```

La invocación `gitattributes` ejecuta esta operación: asignar atributos a rutas para diff, merge, exportación y filtros. Después, los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Sintaxis y formas de invocación

```text
# .gitattributes
*.txt text eol=lf
*.bin binary
docs/*.md diff=markdown
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Funciones y reglas

### Patrones

Un patrón selecciona rutas; un patrón de directorio no recorre su contenido por sí solo.

```bash
git check-attr -a -- ruta
```

Ejecuta `git check-attr -a -- ruta`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Texto

`text` controla normalización y `eol` fija el final de línea en checkout.

```bash
git show :ruta
```

Añade el archivo y compara el blob con `git show :ruta`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Diff y merge

`diff=<driver>` y `merge=<driver>` asignan drivers configurados por nombre.

Consulta el atributo y provoca un diff o merge en el laboratorio. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Filtros

`filter=<driver>` conecta las acciones clean y smudge; clean afecta el contenido que entra al índice.

Compara archivo, índice y blob después de añadir. Usa el [ejemplo mínimo](#ejemplo-mínimo) y cambia solo la regla descrita en este apartado. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

### Exportación

`export-ignore` excluye rutas y `export-subst` sustituye marcadores durante `git archive`.

```bash
git archive --format=tar HEAD > salida.tar
```

Lista el archivo generado por `git archive`. Repite la comprobación después de cambiar una sola entrada para identificar qué regla produjo la diferencia.

## Páginas relacionadas

- [`gitcli`](../guides/gitcli.md)
- [`gitworkflows`](../guides/gitworkflows.md)
- [`githooks`](../guides/githooks.md)

## Fuente

- [gitattributes - Defining attributes per path](https://git-scm.com/docs/gitattributes)
