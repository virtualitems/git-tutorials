---
title: "git add"
source: "https://git-scm.com/docs/git-add"
section: "basic-snapshotting"
status: "source-audited"
version: "2.55.0"
---

# `git add`

Este caso usa `git add` para copiar cambios del área de trabajo al índice.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Ejemplo mínimo

```bash
printf 'capítulo 1\n' > guia.txt
git add guia.txt
git status --short
```

La invocación `git add guia.txt` ejecuta esta operación: copiar cambios del área de trabajo al índice. Después, `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Sintaxis y formas de invocación

```text
git add [--verbose | -v] [--dry-run | -n] [--force | -f] [--interactive | -i] [--patch | -p]
	[--edit | -e] [--[no-]all | -A | --[no-]ignore-removal | [--update | -u]] [--sparse]
	[--intent-to-add | -N] [--refresh] [--ignore-errors] [--ignore-missing] [--renormalize]
	[--chmod=(+|-)x] [--pathspec-from-file=<file> [--pathspec-file-nul]]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git add [<options>] [--] <pathspec>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git add -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--verbose` y `-v`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git add --verbose guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--dry-run` y `-n`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

#### Ejemplo con `--dry-run`

```bash
git add --dry-run guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--force` y `-f`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git add --force guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--interactive` y `-i`

Abre una selección interactiva antes de aplicar la operación.

#### Ejemplo con `--interactive`

```bash
git add --interactive guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--patch` y `-p`

Permite elegir hunks en vez de operar sobre el archivo completo.

#### Ejemplo con `--patch`

```bash
git add --patch guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--edit` y `-e`

Abre la representación editable que define la orden antes de aplicarla.

#### Ejemplo con `--edit`

```bash
git add --edit guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--all` y `-A`

Amplía la selección a todos los elementos del alcance definido.

#### Ejemplo con `--all`

```bash
git add --all guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--ignore-removal`

Excluye elementos que cumplan la condición indicada.

```bash
git add --ignore-removal guia.txt
git status --short
```

### `--update` y `-u`

Limita la actualización a elementos que ya existen en el estado de destino.

La opción cambia cómo `git add` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `--update`

```bash
git add --update guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--sparse`

Permite operar sobre entradas que quedan fuera de la selección sparse activa.

```bash
git add --sparse guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--intent-to-add` y `-N`

Registra una entrada sin preparar todavía su contenido.

#### Ejemplo con `--intent-to-add`

```bash
git add --intent-to-add guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--refresh`

Actualiza metadatos de comprobación sin copiar contenido nuevo al índice.

```bash
git add --refresh guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-errors`

Continúa con otras entradas después de un error y conserva un código de fallo.

Esta forma se usa cuando `git add` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque ignorar errors actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git add --ignore-errors guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-missing`

Permite comprobar rutas ausentes bajo las condiciones que define la orden.

La opción cambia cómo `git add` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git add --ignore-missing guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--renormalize`

Vuelve a aplicar reglas de normalización al contenido seleccionado.

La opción cambia cómo `git add` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git add --renormalize guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--chmod`

Cambia el bit ejecutable registrado en el índice, no el permiso del archivo en disco.

La opción cambia cómo `git add` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git add --chmod=valor guia.txt
git status --short
```

### `--pathspec-from-file`

Lee pathspecs desde un archivo o desde stdin.

La opción cambia cómo `git add` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git add --pathspec-from-file=rutas.txt guia.txt
git status --short
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pathspec-file-nul`

Interpreta los pathspecs de archivo como registros terminados en NUL.

La opción cambia cómo `git add` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git add --pathspec-file-nul guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-U` y `--unified`

Define cuántas líneas de contexto rodean cada hunk.

#### Ejemplo con `--unified`

```bash
git add --unified=5 guia.txt
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--inter-hunk-context`

Fusiona hunks cercanos cuando la distancia no supera el límite indicado.

```bash
git add --inter-hunk-context=5 guia.txt
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-all`

Desactiva el comportamiento `all` para esta invocación.

```bash
git add --no-all guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-removal`

Desactiva para esta invocación el comportamiento que habilita `--ignore-removal`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git add --no-ignore-removal guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-warn-embedded-repo`

Suprime el aviso que aparece al añadir un repositorio Git embebido sin registrarlo mediante `git submodule add`. La opción no crea `.gitmodules` ni convierte la ruta en un submódulo.

```bash
git add --no-warn-embedded-repo vendor/proyecto
git ls-files --stage -- vendor/proyecto
```

La salida del índice permite comprobar que la ruta se registró como gitlink. Usa esta opción solo si administrarás manualmente el repositorio embebido.

## Páginas relacionadas

- [`git commit`](../basic-snapshotting/commit.md)
- [`git mv`](../basic-snapshotting/mv.md)

## Fuente

- [git-add - Add file contents to the index](https://git-scm.com/docs/git-add)
