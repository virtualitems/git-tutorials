---
title: "git archimport"
source: "https://git-scm.com/docs/git-archimport"
section: "external-systems"
status: "source-audited"
version: "2.55.0"
---

# `git archimport`

Este caso usa `git archimport` para importar un repositorio de GNU Arch.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Ejemplo mínimo

```bash
git archimport archivo/linea:main
```

La invocación `git archimport archivo/linea:main` ejecuta esta operación: importar un repositorio de GNU Arch. Después, el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Sintaxis y formas de invocación

```text
git archimport [-h] [-v] [-o] [-a] [-f] [-T] [-D <depth>] [-t <tempdir>]
	       <archive>/<branch>[:<git-branch>]…
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git archimport     # fetch/update GIT from Arch
       [ -h ] [ -v ] [ -o ] [ -a ] [ -f ] [ -T ] [ -D depth ] [ -t tempdir ]
       repository/arch-branch [ repository/arch-branch] ...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git archimport -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-h`

Muestra ayuda corta cuando la orden admite esta convención.

```bash
git archimport -h
printf 'exit=%s\n' "$?"
```

### `-v`

Activa v durante importar un repositorio de GNU Arch. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git archimport -v archivo/linea:main
printf 'exit=%s\n' "$?"
```

### `-o`

Activa o durante importar un repositorio de GNU Arch. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git archimport -o archivo/linea:main
printf 'exit=%s\n' "$?"
```

### `-a`

Activa a durante importar un repositorio de GNU Arch. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git archimport -a archivo/linea:main
printf 'exit=%s\n' "$?"
```

### `-f`

Activa f durante importar un repositorio de GNU Arch. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git archimport -f archivo/linea:main
printf 'exit=%s\n' "$?"
```

### `-T`

Activa T durante importar un repositorio de GNU Arch. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git archimport -T archivo/linea:main
printf 'exit=%s\n' "$?"
```

### `-D`

Activa D durante importar un repositorio de GNU Arch. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git archimport -D archivo/linea:main
printf 'exit=%s\n' "$?"
```

### `-t`

Activa t durante importar un repositorio de GNU Arch. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git archimport -t archivo/linea:main
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git cvsexportcommit`](../external-systems/cvsexportcommit.md)
- [`git cvsimport`](../external-systems/cvsimport.md)

## Fuente

- [git-archimport - Import a GNU Arch repository into Git](https://git-scm.com/docs/git-archimport)
