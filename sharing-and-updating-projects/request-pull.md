---
title: "git request-pull"
source: "https://git-scm.com/docs/git-request-pull"
section: "sharing-and-updating-projects"
status: "source-audited"
version: "2.55.0"
---

# `git request-pull`

Este caso usa `git request-pull` para generar un resumen para solicitar que otra persona integre cambios.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git request-pull v1.0 https://example.com/equipo/biblioteca.git main
```

La invocación `git request-pull v1.0 https://example.com/equipo/biblioteca.git main` ejecuta esta operación: generar un resumen para solicitar que otra persona integre cambios. Después, las referencias locales y remotas permiten separar descarga, integración y publicación.

## Sintaxis y formas de invocación

```text
git request-pull [-p] <start> <URL> [<end>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git request-pull [options] start url [end]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git request-pull -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-p`

Incluye p en la salida o cambia cómo `git request-pull` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show patch text as well`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git request-pull -p v1.0 https://example.com/equipo/biblioteca.git main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git submodule`](../sharing-and-updating-projects/submodule.md)
- [`git remote`](../sharing-and-updating-projects/remote.md)
- [`git push`](../sharing-and-updating-projects/push.md)

## Fuente

- [git-request-pull - Generates a summary of pending changes](https://git-scm.com/docs/git-request-pull)
