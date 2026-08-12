---
title: "git cvsimport"
source: "https://git-scm.com/docs/git-cvsimport"
section: "external-systems"
status: "source-audited"
version: "2.55.0"
---

# `git cvsimport`

Este caso usa `git cvsimport` para importar historial desde CVS.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Ejemplo mínimo

```bash
git cvsimport -C biblioteca -r cvs modulo
```

La invocación `git cvsimport -C biblioteca -r cvs modulo` ejecuta esta operación: importar historial desde CVS. Después, el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Sintaxis y formas de invocación

```text
git cvsimport [-o <branch-for-HEAD>] [-h] [-v] [-d <CVSROOT>]
	      [-A <author-conv-file>] [-p <options-for-cvsps>] [-P <file>]
	      [-C <git-repository>] [-z <fuzz>] [-i] [-k] [-u] [-s <subst>]
	      [-a] [-m] [-M <regex>] [-S <regex>] [-L <commit-limit>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git cvsimport     # fetch/update GIT from CVS
       [-o branch-for-HEAD] [-h] [-v] [-d CVSROOT] [-A author-conv-file]
       [-p opts-for-cvsps] [-P file] [-C GIT_repository] [-z fuzz] [-i] [-k]
       [-u] [-s subst] [-a] [-m] [-M regex] [-S regex] [-L commitlimit]
       [-r remote] [-R] [CVS_module]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git cvsimport -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-o`

Activa o durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -o -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-h`

Muestra ayuda corta cuando la orden admite esta convención.

```bash
git cvsimport -h
printf 'exit=%s\n' "$?"
```

### `-v`

Activa v durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -v -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-d`

Activa d durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -d -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-A`

Activa A durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -A -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-p`

Activa p durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -p -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-P`

Activa P durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -P -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

```bash
git cvsimport -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git cvsimport -z -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-i`

Activa i durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -i -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-k`

Activa k durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -k -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-u`

Activa u durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -u -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-s`

Activa s durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -s -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-a`

Activa a durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -a -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-m`

Activa m durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -m -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-M`

Activa M durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -M -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-S`

Activa S durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -S -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-L`

Activa L durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -L -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

### `-r`

Activa r durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -r -C biblioteca cvs modulo
printf 'exit=%s\n' "$?"
```

### `-R`

Activa R durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git cvsimport -R -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git cvsserver`](../external-systems/cvsserver.md)
- [`git cvsexportcommit`](../external-systems/cvsexportcommit.md)
- [`git fast-export`](../external-systems/fast-export.md)

## Fuente

- [git-cvsimport - Salvage your data out of another SCM people love to hate](https://git-scm.com/docs/git-cvsimport)
