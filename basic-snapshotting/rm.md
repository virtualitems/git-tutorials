---
title: "git rm"
source: "https://git-scm.com/docs/git-rm"
section: "basic-snapshotting"
status: "source-audited"
version: "2.55.0"
---

# `git rm`

Este caso usa `git rm` para retirar rutas del índice y, por defecto, del área de trabajo.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Ejemplo mínimo

```bash
git rm notas-temporales.txt
git commit -m "Retira notas temporales"
```

La invocación `git rm notas-temporales.txt` ejecuta esta operación: retirar rutas del índice y, por defecto, del área de trabajo. Después, `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Sintaxis y formas de invocación

```text
git rm [-f | --force] [-n] [-r] [--cached] [--ignore-unmatch]
       [--quiet] [--pathspec-from-file=<file> [--pathspec-file-nul]]
       [--] [<pathspec>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git rm [-f | --force] [-n] [-r] [--cached] [--ignore-unmatch]
              [--quiet] [--pathspec-from-file=<file> [--pathspec-file-nul]]
              [--] [<pathspec>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git rm -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git rm --force notas-temporales.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-n` y `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

#### Ejemplo con `--dry-run`

```bash
git rm --dry-run notas-temporales.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-r`

Permite r cuando la forma predeterminada de `git rm` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow recursive removal`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git rm -r notas-temporales.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cached`

Usa el índice como origen o destino, sin tratar el área de trabajo de la misma forma.

```bash
git rm --cached notas-temporales.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-unmatch`

Excluye elementos que cumplan la condición indicada.

```bash
git rm --ignore-unmatch notas-temporales.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quiet` y `-q`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git rm --quiet notas-temporales.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--pathspec-from-file`

Lee pathspecs desde un archivo o desde stdin.

La opción cambia cómo `git rm` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git rm --pathspec-from-file=rutas.txt notas-temporales.txt
git status --short
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pathspec-file-nul`

Interpreta los pathspecs de archivo como registros terminados en NUL.

La opción cambia cómo `git rm` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git rm --pathspec-file-nul notas-temporales.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sparse`

Permite operar sobre entradas que quedan fuera de la selección sparse activa.

```bash
git rm --sparse notas-temporales.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git status`](../basic-snapshotting/status.md)
- [`git restore`](../basic-snapshotting/restore.md)
- [`git reset`](../basic-snapshotting/reset.md)

## Fuente

- [git-rm - Remove files from the working tree and from the index](https://git-scm.com/docs/git-rm)
