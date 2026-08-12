---
title: "git svn"
source: "https://git-scm.com/docs/git-svn"
section: "external-systems"
status: "source-audited"
version: "2.55.0"
---

# `git svn`

Este caso usa `git svn` para usar un repositorio Subversion desde un repositorio Git.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Ejemplo mínimo

```bash
git svn clone https://example.com/svn/biblioteca/trunk biblioteca
```

La invocación `git svn clone https://example.com/svn/biblioteca/trunk biblioteca` ejecuta esta operación: usar un repositorio Subversion desde un repositorio Git. Después, el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Sintaxis y formas de invocación

```text
git svn <command> [<options>] [<arguments>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git svn -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-h`

Activa h durante usar un repositorio Subversion desde un repositorio Git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git svn -h
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git quiltimport`](../external-systems/quiltimport.md)
- [`git p4`](../external-systems/p4.md)

## Fuente

- [git-svn - Bidirectional operation between a Subversion repository and Git](https://git-scm.com/docs/git-svn)
