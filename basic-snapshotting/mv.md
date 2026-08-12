---
title: "git mv"
source: "https://git-scm.com/docs/git-mv"
section: "basic-snapshotting"
status: "source-audited"
version: "2.55.0"
---

# `git mv`

Este caso usa `git mv` para mover o renombrar una ruta seguida por Git.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Ejemplo mínimo

```bash
git mv borrador.md capitulos/introduccion.md
git status --short
```

La invocación `git mv borrador.md capitulos/introduccion.md` ejecuta esta operación: mover o renombrar una ruta seguida por Git. Después, `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Sintaxis y formas de invocación

```text
git mv [-v] [-f] [-n] [-k] <source> <destination>
git mv [-v] [-f] [-n] [-k] <source>... <destination-directory>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git mv [-v] [-f] [-n] [-k] <source> <destination>
   or: git mv [-v] [-f] [-n] [-k] <source>... <destination-directory>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git mv -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git mv --verbose borrador.md capitulos/introduccion.md
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git mv --force borrador.md capitulos/introduccion.md
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-n` y `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

#### Ejemplo con `--dry-run`

```bash
git mv --dry-run borrador.md capitulos/introduccion.md
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-k`

Activa k durante mover o renombrar una ruta seguida por Git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `skip move/rename errors`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git mv` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque k actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git mv -k borrador.md capitulos/introduccion.md
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sparse`

Permite operar sobre entradas que quedan fuera de la selección sparse activa.

```bash
git mv --sparse borrador.md capitulos/introduccion.md
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git notes`](../basic-snapshotting/notes.md)
- [`git commit`](../basic-snapshotting/commit.md)
- [`git reset`](../basic-snapshotting/reset.md)

## Fuente

- [git-mv - Move or rename a file, a directory, or a symlink](https://git-scm.com/docs/git-mv)
