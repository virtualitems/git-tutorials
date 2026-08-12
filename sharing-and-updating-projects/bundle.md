---
title: "git bundle"
source: "https://git-scm.com/docs/git-bundle"
section: "sharing-and-updating-projects"
status: "source-audited"
version: "2.55.0"
---

# `git bundle`

Este caso usa `git bundle` para transportar objetos y referencias dentro de un solo archivo.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git bundle create entrega.bundle main
git bundle verify entrega.bundle
git clone entrega.bundle copia
```

La invocación `git bundle create entrega.bundle main` ejecuta esta operación: transportar objetos y referencias dentro de un solo archivo. Después, las referencias locales y remotas permiten separar descarga, integración y publicación.

## Sintaxis y formas de invocación

```text
git bundle create [-q | --quiet | --progress]
		    [--version=<version>] <file> <git-rev-list-args>
git bundle verify [-q | --quiet] <file>
git bundle list-heads <file> [<refname>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git bundle create [-q | --quiet | --progress]
                         [--version=<version>] <file> <git-rev-list-args>
   or: git bundle verify [-q | --quiet] <file>
   or: git bundle list-heads <file> [<refname>...]
   or: git bundle unbundle [--progress] <file> [<refname>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git bundle -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-q`

Activa q durante transportar objetos y referencias dentro de un solo archivo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git bundle -q create entrega.bundle main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quiet`

Reduce mensajes que no representan errores.

```bash
git bundle --quiet create entrega.bundle main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git bundle --progress create entrega.bundle main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--version`

Muestra la versión y termina.

```bash
git bundle --version
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git fetch`](../sharing-and-updating-projects/fetch.md)
- [`git ls-remote`](../sharing-and-updating-projects/ls-remote.md)

## Fuente

- [git-bundle - Move objects and refs by archive](https://git-scm.com/docs/git-bundle)
