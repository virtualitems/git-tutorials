---
title: "git tag"
source: "https://git-scm.com/docs/git-tag"
section: "branching-and-merging"
status: "source-audited"
version: "2.55.0"
---

# `git tag`

Este caso usa `git tag` para crear, listar, verificar y eliminar etiquetas.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git tag -a v1.0 -m "Primera entrega"
git show v1.0
```

La invocación `git tag -a v1.0 -m "Primera entrega"` ejecuta esta operación: crear, listar, verificar y eliminar etiquetas. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Sintaxis y formas de invocación

```text
git tag [-a | -s | -u <key-id>] [-f] [-m <msg> | -F <file>] [-e]
	[(--trailer <token>[(=|:)<value>])…]
	<tagname> [<commit> | <object>]
git tag -d <tagname>…
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git tag [-a | -s | -u <key-id>] [-f] [-m <msg> | -F <file>] [-e]
               [(--trailer <token>[(=|:)<value>])...]
               <tagname> [<commit> | <object>]
   or: git tag -d <tagname>...
   or: git tag [-n[<num>]] -l [--contains <commit>] [--no-contains <commit>]
               [--points-at <object>] [--column[=<options>] | --no-column]
               [--create-reflog] [--sort=<key>] [--format=<format>]
               [--merged <commit>] [--no-merged <commit>] [<pattern>...]
   or: git tag -v [--format=<format>] <tagname>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git tag -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-a` y `--annotate`

Activa annotate durante crear, listar, verificar y eliminar etiquetas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `annotated tag, needs a message`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--annotate`

```bash
git tag --annotate v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-s` y `--sign`

Activa sign durante crear, listar, verificar y eliminar etiquetas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `annotated and GPG-signed tag`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--sign`

```bash
git tag --sign -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-u` y `--local-user`

Define alcance local user para esta ejecución de `git tag`. En Git 2.51.1, la ayuda corta expresa el contrato como `use another key to sign the tag`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--local-user`

```bash
git tag --local-user=user.name -a v1.0 -m "Primera entrega"
git status --short
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git tag --force -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-m` y `--message`

Activa mensaje durante crear, listar, verificar y eliminar etiquetas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `tag message`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--message`

```bash
git tag --message='mensaje de ejemplo' -a v1.0
git status --short
```

En esta forma, `mensaje de ejemplo` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-F` y `--file`

Usa el archivo indicado en vez de la ubicación por defecto.

La opción cambia cómo `git tag` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `--file`

```bash
git tag --file=rutas.txt -a v1.0 -m "Primera entrega"
git status --short
```

En esta forma, `rutas.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-e` y `--edit`

Abre la representación editable que define la orden antes de aplicarla.

#### Ejemplo con `--edit`

```bash
git tag --edit -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--trailer`

Incluye trailer en la entrada, el resultado o el registro que construye `git tag`. En Git 2.51.1, la ayuda corta expresa el contrato como `add custom trailer(s)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git tag --trailer=valor -a v1.0 -m "Primera entrega"
git status --short
```

### `-d` y `--delete`

Elimina el elemento seleccionado.

#### Ejemplo con `--delete`

```bash
git tag --delete -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-n`

Incluye n en la salida o cambia cómo `git tag` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print <n> lines of each tag message`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git tag -n 5 -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-l` y `--list`

Incluye información adicional en la salida.

#### Ejemplo con `--list`

```bash
git tag --list -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--contains`

Filtra referencias cuyo historial contiene el commit indicado.

```bash
git tag --contains=HEAD -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-contains`

Filtra referencias cuyo historial no contiene el commit indicado.

```bash
git tag --no-contains -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--points-at`

Limita crear, listar, verificar y eliminar etiquetas al alcance identificado por points at. En Git 2.51.1, la ayuda corta expresa el contrato como `print only tags of the object`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git tag --points-at=HEAD -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--column`

Incluye column en la salida o cambia cómo `git tag` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show tag list in columns`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git tag --column=short -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-column`

Desactiva el comportamiento `column` para esta invocación.

```bash
git tag --no-column -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--create-reflog`

Permite crear o escribir el elemento seleccionado.

```bash
git tag --create-reflog -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sort`

Ordena registros por el campo indicado.

```bash
git tag --sort=user.name -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `user.name` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--format`

Define los campos y separadores de la salida.

```bash
git tag --format=oneline -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--merged`

Filtra elementos ya alcanzables desde la revisión indicada.

```bash
git tag --merged=HEAD -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-merged`

Filtra elementos no alcanzables desde la revisión indicada.

```bash
git tag --no-merged -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

#### Ejemplo con `--verify`

```bash
git tag --verify -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--cleanup`

Selecciona cómo Git retira comentarios y espacios del mensaje antes de crear el commit.

```bash
git tag --cleanup=all -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--omit-empty`

Impide omit vacío durante esta invocación de `git tag`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not output a newline after empty formatted refs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git tag --omit-empty -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--color`

Controla el uso de secuencias de color en la salida.

```bash
git tag --color=always -a v1.0 -m "Primera entrega"
git status --short
```

El ejemplo usa `always` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-i` y `--ignore-case`

Excluye elementos que cumplan la condición indicada.

#### Ejemplo con `--ignore-case`

```bash
git tag --ignore-case -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--no-create-reflog`

Desactiva para esta invocación el comportamiento que habilita `--create-reflog`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git tag --no-create-reflog -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-sign`

Desactiva para esta invocación el comportamiento que habilita `--sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git tag --no-sign -a v1.0 -m "Primera entrega"
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git worktree`](../branching-and-merging/worktree.md)
- [`git switch`](../branching-and-merging/switch.md)
- [`git stash`](../branching-and-merging/stash.md)

## Fuente

- [git-tag - Create, list, delete or verify tags](https://git-scm.com/docs/git-tag)
