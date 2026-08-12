---
title: "git notes"
source: "https://git-scm.com/docs/git-notes"
section: "basic-snapshotting"
status: "source-audited"
version: "2.55.0"
---

# `git notes`

Este caso usa `git notes` para asociar anotaciones a objetos sin cambiar los objetos.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Ejemplo mínimo

```bash
git notes add -m "Revisado en clase" HEAD
git notes show HEAD
```

La invocación `git notes add -m "Revisado en clase" HEAD` ejecuta esta operación: asociar anotaciones a objetos sin cambiar los objetos. Después, `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Sintaxis y formas de invocación

```text
git notes [list [<object>]]
git notes add [-f] [--allow-empty] [--[no-]separator | --separator=<paragraph-break>] [--[no-]stripspace] [-F <file> | -m <msg> | (-c | -C) <object>] [-e] [<object>]
git notes copy [-f] ( --stdin | <from-object> [<to-object>] )
git notes append [--allow-empty] [--[no-]separator | --separator=<paragraph-break>] [--[no-]stripspace] [-F <file> | -m <msg> | (-c | -C) <object>] [-e] [<object>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git notes [--ref <notes-ref>] [list [<object>]]
   or: git notes [--ref <notes-ref>] add [-f] [--allow-empty] [--[no-]separator|--separator=<paragraph-break>] [--[no-]stripspace] [-m <msg> | -F <file> | (-c | -C) <object>] [<object>] [-e]
   or: git notes [--ref <notes-ref>] copy [-f] <from-object> <to-object>
   or: git notes [--ref <notes-ref>] append [--allow-empty] [--[no-]separator|--separator=<paragraph-break>] [--[no-]stripspace] [-m <msg> | -F <file> | (-c | -C) <object>] [<object>] [-e]
   or: git notes [--ref <notes-ref>] edit [--allow-empty] [<object>]
   or: git notes [--ref <notes-ref>] show [<object>]
   or: git notes [--ref <notes-ref>] merge [-v | -q] [-s <strategy>] <notes-ref>
   or: git notes merge --commit [-v | -q]
   or: git notes merge --abort [-v | -q]
   or: git notes [--ref <notes-ref>] remove [<object>...]
   or: git notes [--ref <notes-ref>] prune [-n] [-v]
   or: git notes [--ref <notes-ref>] get-ref
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git notes -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-f`

Activa f durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git notes -f add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--allow-empty`

Permite continuar cuando el cambio produce un commit sin diferencias.

```bash
git notes --allow-empty add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--separator`

Activa separator durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git notes --separator add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stripspace`

Activa stripspace durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git notes --stripspace add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-F`

Activa F durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git notes -F add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m`

Activa m durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git notes -m add "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-c`

Aplica una clave de configuración solo a esta invocación.

```bash
git notes -c add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

```bash
git notes -C add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-e`

Activa e durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git notes -e add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git notes` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git notes --stdin add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ref`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git notes --ref=refs/heads/main add -m "Revisado en clase" HEAD
git status --short
```

El ejemplo usa `refs/heads/main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v`

Activa v durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git notes -v add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q`

Activa q durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git notes -q add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-s`

Activa s durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git notes -s add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--commit`

Activa commit durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git notes --commit add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--abort`

Cancela la secuencia y restaura el punto que la orden registró al comenzar.

Esta forma se usa cuando `git notes` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque abortar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git notes --abort
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-n`

Activa n durante asociar anotaciones a objetos sin cambiar los objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git notes -n add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-separator`

Desactiva para esta invocación el comportamiento que habilita `--separator`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git notes --no-separator add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stripspace`

Desactiva para esta invocación el comportamiento que habilita `--stripspace`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git notes --no-stripspace add -m "Revisado en clase" HEAD
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--message`, `--file`, `--reuse-message` y `--reedit-message`

Estas opciones proporcionan el texto de una nota sin partir de un editor vacío. `--message=<texto>` usa el argumento y concatena varios usos como párrafos; `--file=<archivo>` lee un archivo o stdin si el valor es `-`; `--reuse-message=<objeto>` copia literalmente el blob indicado; `--reedit-message=<objeto>` carga ese blob y abre el editor.

```bash
git notes add --message='Revisado por QA' HEAD
printf 'Nota desde stdin\n' | git notes add --file=- HEAD~1
git notes show HEAD
```

### `--force`

Sobrescribe la nota cuando el objeto ya tiene una. Sin esta opción, `git notes add` termina con error para evitar una sustitución accidental.

```bash
git notes add --force --message='Texto corregido' HEAD
git notes show HEAD
```

### `--ignore-missing` y `--dry-run`

`--ignore-missing` permite que `notes remove` reciba objetos sin nota. `--dry-run` muestra los objetos cuyas notas retiraría sin modificar la referencia de notas.

```bash
git notes remove --dry-run --ignore-missing HEAD HEAD~1
```

### `--strategy`

Selecciona cómo `notes merge` resuelve conflictos: `manual` (predeterminado), `ours`, `theirs`, `union` o `cat_sort_uniq`. La opción sustituye `notes.mergeStrategy` para esa invocación.

```bash
git notes merge --strategy=union refs/notes/revision
git notes list
```

### `--quiet` y `--verbose`

Durante `notes merge`, `--quiet` reduce mensajes y `--verbose` los amplía. Con `notes prune`, `--verbose` muestra los objetos cuyas notas elimina.

```bash
git notes prune --dry-run --verbose
```

El ejemplo combina `--verbose` con la simulación para enumerar candidatos sin borrarlos.

## Páginas relacionadas

- [`git reset`](../basic-snapshotting/reset.md)
- [`git mv`](../basic-snapshotting/mv.md)
- [`git restore`](../basic-snapshotting/restore.md)

## Fuente

- [git-notes - Add or inspect object notes](https://git-scm.com/docs/git-notes)
