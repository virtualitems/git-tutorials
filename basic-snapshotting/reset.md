---
title: "git reset"
source: "https://git-scm.com/docs/git-reset"
section: "basic-snapshotting"
status: "source-audited"
version: "2.55.0"
---

# `git reset`

Este caso usa `git reset` para mover HEAD o restablecer el índice y, según el modo, el área de trabajo.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Ejemplo mínimo

```bash
git add guia.txt
git reset HEAD -- guia.txt
git status --short
```

La invocación `git reset HEAD -- guia.txt` ejecuta esta operación: mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Después, `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Sintaxis y formas de invocación

```text
git reset [--soft | --mixed [-N] | --hard | --merge | --keep] [-q] [<commit>]
git reset [-q] [<tree-ish>] [--] <pathspec>…
git reset [-q] [--pathspec-from-file=<file> [--pathspec-file-nul]] [<tree-ish>]
git reset (--patch | -p) [<tree-ish>] [--] [<pathspec>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git reset [--mixed | --soft | --hard | --merge | --keep] [-q] [<commit>]
   or: git reset [-q] [<tree-ish>] [--] <pathspec>...
   or: git reset [-q] [--pathspec-from-file [--pathspec-file-nul]] [<tree-ish>]
   or: git reset --patch [<tree-ish>] [--] [<pathspec>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git reset -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--soft`

Restablece soft como parte de mover HEAD o restablecer el índice y, según el modo, el área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `reset only HEAD`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git reset --soft HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mixed`

Restablece mixed como parte de mover HEAD o restablecer el índice y, según el modo, el área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `reset HEAD and index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git reset --mixed HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-N` y `--intent-to-add`

Registra una entrada sin preparar todavía su contenido.

#### Ejemplo con `--intent-to-add`

```bash
git reset --intent-to-add HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--hard`

Restablece hard como parte de mover HEAD o restablecer el índice y, según el modo, el área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `reset HEAD, index and working tree`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git reset --hard HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--merge`

Restablece merge como parte de mover HEAD o restablecer el índice y, según el modo, el área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `reset HEAD, index and working tree`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git reset --merge HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep`

Conserva el asunto del mensaje recibido según la forma que define el comando. En Git 2.51.1, la ayuda corta expresa el contrato como `reset HEAD but keep local changes`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git reset --keep HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git reset --quiet HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--pathspec-from-file`

Lee pathspecs desde un archivo o desde stdin.

La opción cambia cómo `git reset` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git reset --pathspec-from-file=rutas.txt HEAD -- guia.txt
git status --short
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pathspec-file-nul`

Interpreta los pathspecs de archivo como registros terminados en NUL.

La opción cambia cómo `git reset` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git reset --pathspec-file-nul HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--patch` y `-p`

Permite elegir hunks en vez de operar sobre el archivo completo.

#### Ejemplo con `--patch`

```bash
git reset --patch HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--no-refresh`

Desactiva el comportamiento `refresh` para esta invocación.

```bash
git reset --no-refresh HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--refresh`

Actualiza metadatos de comprobación sin copiar contenido nuevo al índice.

```bash
git reset --refresh HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

```bash
git reset --recurse-submodules HEAD -- guia.txt
git status --short
```

### `-U` y `--unified`

Define cuántas líneas de contexto rodean cada hunk.

#### Ejemplo con `--unified`

```bash
git reset --unified=5 HEAD -- guia.txt
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--inter-hunk-context`

Fusiona hunks cercanos cuando la distancia no supera el límite indicado.

```bash
git reset --inter-hunk-context=5 HEAD -- guia.txt
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git reset --no-recurse-submodules HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git restore`](../basic-snapshotting/restore.md)
- [`git notes`](../basic-snapshotting/notes.md)
- [`git rm`](../basic-snapshotting/rm.md)

## Fuente

- [git-reset - Set HEAD or the index to a known state](https://git-scm.com/docs/git-reset)
