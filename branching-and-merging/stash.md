---
title: "git stash"
source: "https://git-scm.com/docs/git-stash"
section: "branching-and-merging"
status: "source-audited"
version: "2.55.0"
---

# `git stash`

Este caso usa `git stash` para guardar cambios sin commit y recuperar un área de trabajo limpia.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git stash push -m "portada incompleta"
git switch main
git stash pop
```

La invocación `git stash push -m "portada incompleta"` ejecuta esta operación: guardar cambios sin commit y recuperar un área de trabajo limpia. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Sintaxis y formas de invocación

```text
git stash list [<log-options>]
git stash show [-u | --include-untracked | --only-untracked] [<diff-options>] [<stash>]
git stash drop [-q | --quiet] [<stash>]
git stash pop [--index] [-q | --quiet] [<stash>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git stash list [<log-options>]
   or: git stash show [-u | --include-untracked | --only-untracked] [<diff-options>] [<stash>]
   or: git stash drop [-q | --quiet] [<stash>]
   or: git stash pop [--index] [-q | --quiet] [<stash>]
   or: git stash apply [--index] [-q | --quiet] [<stash>]
   or: git stash branch <branchname> [<stash>]
   or: git stash [push [-p | --patch] [-S | --staged] [-k | --[no-]keep-index] [-q | --quiet]
                 [-u | --include-untracked] [-a | --all] [(-m | --message) <message>]
                 [--pathspec-from-file=<file> [--pathspec-file-nul]]
                 [--] [<pathspec>...]]
   or: git stash save [-p | --patch] [-S | --staged] [-k | --[no-]keep-index] [-q | --quiet]
                 [-u | --include-untracked] [-a | --all] [<message>]
   or: git stash clear
   or: git stash create [<message>]
   or: git stash store [(-m | --message) <message>] [-q | --quiet] <commit>
   or: git stash export (--print | --to-ref <ref>) [<stash>...]
   or: git stash import <commit>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git stash -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-u`

Activa u durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git stash -u push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include-untracked`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git stash --include-untracked push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--only-untracked`

Activa only untracked durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git stash --only-untracked push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q`

Activa q durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git stash -q push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quiet`

Reduce mensajes que no representan errores.

```bash
git stash --quiet push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index`

Incluye el índice en la operación.

```bash
git stash --index push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p`

Activa p durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git stash -p push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--patch`

Permite elegir hunks en vez de operar sobre el archivo completo.

```bash
git stash --patch push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-S`

Activa S durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git stash -S push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--staged`

Selecciona el contenido preparado en el índice.

```bash
git stash --staged push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-k`

Activa k durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git stash -k push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-index`

Activa conservar índice durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git stash --keep-index push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a`

Activa a durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git stash -a push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git stash --all push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m`

Activa m durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git stash -m push "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--message`

Activa mensaje durante guardar cambios sin commit y recuperar un área de trabajo limpia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git stash --message push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pathspec-from-file`

Lee pathspecs desde un archivo o desde stdin.

La opción cambia cómo `git stash` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git stash --pathspec-from-file push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pathspec-file-nul`

Interpreta los pathspecs de archivo como registros terminados en NUL.

La opción cambia cómo `git stash` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git stash --pathspec-file-nul push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--print`

Incluye información adicional en la salida.

```bash
git stash --print push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--to-ref`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git stash --to-ref push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-keep-index`

Desactiva para esta invocación el comportamiento que habilita `--keep-index`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git stash --no-keep-index push -m "portada incompleta"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include-untracked` y `--no-include-untracked`

Con `push` o `save`, la forma positiva guarda también archivos no seguidos y después los retira del área de trabajo. Con `show`, controla si esos archivos aparecen en el diff. La forma negativa revierte una configuración o una opción positiva anterior.

```bash
git stash push --include-untracked -m "incluye borrador"
git stash show --include-untracked --stat stash@{0}
```

### `--label-ours`, `--label-theirs` y `--label-base`

Estas opciones solo se aceptan con `stash apply`. Sustituyen las etiquetas predeterminadas de los marcadores de conflicto; `--label-base` solo produce efecto cuando `merge.conflictStyle=diff3`.

```bash
git -c merge.conflictStyle=diff3 stash apply \
  --label-ours='cambios actuales' \
  --label-theirs='cambios guardados' \
  --label-base='base común' stash@{0}
```

Si la aplicación genera un conflicto, abre el archivo afectado y comprueba las tres etiquetas en sus marcadores.

## Páginas relacionadas

- [`git switch`](../branching-and-merging/switch.md)
- [`git rerere`](../branching-and-merging/rerere.md)
- [`git tag`](../branching-and-merging/tag.md)

## Fuente

- [git-stash - Stash the changes in a dirty working directory away](https://git-scm.com/docs/git-stash)
