---
title: "git cvsexportcommit"
source: "https://git-scm.com/docs/git-cvsexportcommit"
section: "external-systems"
status: "source-audited"
version: "2.55.0"
---

# `git cvsexportcommit`

Este caso usa `git cvsexportcommit` para aplicar un commit de Git sobre un checkout de CVS.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Ejemplo mínimo

```bash
git cvsexportcommit -w /tmp/checkout-cvs HEAD
```

La invocación `git cvsexportcommit -w /tmp/checkout-cvs HEAD` ejecuta esta operación: aplicar un commit de Git sobre un checkout de CVS. Después, el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Sintaxis y formas de invocación

```text
git cvsexportcommit [-h] [-u] [-v] [-c] [-P] [-p] [-a] [-d <cvsroot>]
	[-w <cvs-workdir>] [-W] [-f] [-m <msgprefix>] [<parent-commit>] <commit-id>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
GIT_DIR=/path/to/.git git cvsexportcommit [-h] [-p] [-v] [-c] [-f] [-u] [-k] [-w cvsworkdir] [-m msgprefix] [ parent ] commit
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git cvsexportcommit -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-h`

Muestra ayuda corta cuando la orden admite esta convención.

```bash
git cvsexportcommit -h
printf 'exit=%s\n' "$?"
```

### `-u`

Activa u durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsexportcommit -u -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

### `-v`

Activa v durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsexportcommit -v -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

### `-c`

Aplica una clave de configuración solo a esta invocación.

```bash
git cvsexportcommit -c -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

### `-P`

Activa P durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsexportcommit -P -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

### `-p`

Activa p durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsexportcommit -p -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

### `-a`

Activa a durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsexportcommit -a -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

### `-d`

Activa d durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsexportcommit -d -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

### `-w`

Activa w durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsexportcommit -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

### `-W`

Activa W durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsexportcommit -W -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

### `-f`

Activa f durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsexportcommit -f -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

### `-m`

Activa m durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsexportcommit -m -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

### `-k`

Activa k durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsexportcommit -k -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git cvsimport`](../external-systems/cvsimport.md)
- [`git archimport`](../external-systems/archimport.md)
- [`git cvsserver`](../external-systems/cvsserver.md)

## Fuente

- [git-cvsexportcommit - Export a single commit to a CVS checkout](https://git-scm.com/docs/git-cvsexportcommit)
