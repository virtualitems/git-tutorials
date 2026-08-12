---
title: "git apply"
source: "https://git-scm.com/docs/git-apply"
section: "patching"
status: "source-audited"
version: "2.55.0"
---

# `git apply`

Este caso usa `git apply` para aplicar un parche sobre archivos o sobre el índice.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Ejemplo mínimo

```bash
git apply --check cambio.patch
git apply cambio.patch
```

La invocación `git apply --check cambio.patch` ejecuta esta operación: aplicar un parche sobre archivos o sobre el índice. Después, el diff y el historial muestran si cambiaron archivos, índice o commits.

## Sintaxis y formas de invocación

```text
git apply [--stat] [--numstat] [--summary] [--check]
	  [--index | --intent-to-add] [--3way] [--ours | --theirs | --union]
	  [--apply] [--no-add] [--build-fake-ancestor=<file>] [-R | --reverse]
	  [--allow-binary-replacement | --binary] [--reject] [-z]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git apply [<options>] [<patch>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git apply -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--stat`

Resume cambios mediante conteos por ruta.

Esta forma se usa cuando `git apply` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque estadísticas actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git apply --stat --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--numstat`

Incluye numstat en la salida o cambia cómo `git apply` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show number of added and deleted lines in decimal notation`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --numstat --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--summary`

Incluye summary en la salida o cambia cómo `git apply` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `instead of applying the patch, output a summary for the input`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --summary --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--check`

Valida sin producir el efecto principal de la orden.

```bash
git apply --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index`

Incluye el índice en la operación.

```bash
git apply --index --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--intent-to-add` y `-N`

Registra una entrada sin preparar todavía su contenido.

La opción cambia cómo `git apply` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `--intent-to-add`

```bash
git apply --intent-to-add --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--3way` y `-3`

Intenta una fusión de tres vías cuando el parche no se aplica directamente y existen los blobs necesarios. En Git 2.51.1, la ayuda corta expresa el contrato como `attempt three-way merge, fall back on normal patch if that fails`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--3way`

```bash
git apply --3way --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--ours`

Selecciona la versión de la etapa ours para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use our version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --ours --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--theirs`

Selecciona la versión de la etapa theirs para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use their version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --theirs --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--union`

Define union para esta ejecución de `git apply`. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use a union version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --union --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--apply`

Comprueba apply antes de aceptar el resultado de `git apply`. En Git 2.51.1, la ayuda corta expresa el contrato como `also apply the patch (use with --stat/--summary/--check)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --apply --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-add`

Desactiva el comportamiento `add` para esta invocación.

```bash
git apply --no-add --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--build-fake-ancestor`

Activa build fake ancestor durante aplicar un parche sobre archivos o sobre el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `build a temporary index based on embedded index information`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --build-fake-ancestor=rutas.txt --check cambio.patch
git status --short
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-R` y `--reverse`

Invierte el orden del recorrido o resultado.

#### Ejemplo con `--reverse`

```bash
git apply --reverse --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--allow-binary-replacement`

Activa permitir contenido binario replacement durante aplicar un parche sobre archivos o sobre el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git apply --allow-binary-replacement --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--binary`

Activa contenido binario durante aplicar un parche sobre archivos o sobre el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git apply --binary --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reject`

Conserva hunks que no pudieron aplicarse en archivos de rechazo para inspección manual. En Git 2.51.1, la ayuda corta expresa el contrato como `leave the rejected hunks in corresponding *.rej files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git apply` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git apply --reject --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git apply -z --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude`

Excluye elementos que cumplan la condición indicada.

```bash
git apply --exclude=archivo.txt --check cambio.patch
git status --short
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git apply --include=archivo.txt --check cambio.patch
git status --short
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p`

Retira p del alcance que procesa `git apply`. En Git 2.51.1, la ayuda corta expresa el contrato como `remove <num> leading slashes from traditional diff paths`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply -p 5 --check cambio.patch
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--add`

Permite crear o escribir el elemento seleccionado.

```bash
git apply --add --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cached`

Usa el índice como origen o destino, sin tratar el área de trabajo de la misma forma.

```bash
git apply --cached --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unsafe-paths`

Activa unsafe paths durante aplicar un parche sobre archivos o sobre el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `accept a patch that touches outside the working area`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --unsafe-paths --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

```bash
git apply -C 5 --check cambio.patch
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--whitespace`

Selecciona la acción que Git ejecuta cuando detecta errores de espacios en un parche. En Git 2.51.1, la ayuda corta expresa el contrato como `detect new or modified lines that have whitespace errors`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --whitespace=warn --check cambio.patch
git status --short
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-space-change`

Excluye elementos que cumplan la condición indicada.

```bash
git apply --ignore-space-change --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-whitespace`

Excluye elementos que cumplan la condición indicada.

```bash
git apply --ignore-whitespace --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unidiff-zero`

Impide unidiff zero durante esta invocación de `git apply`. En Git 2.51.1, la ayuda corta expresa el contrato como `don't expect at least one line of context`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --unidiff-zero --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--allow-overlap`

Permite permitir overlap cuando la forma predeterminada de `git apply` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow overlapping hunks`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --allow-overlap --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git apply --verbose --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git apply --quiet --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--inaccurate-eof`

Activa inaccurate eof durante aplicar un parche sobre archivos o sobre el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git apply` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git apply --inaccurate-eof --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recount`

Impide recount durante esta invocación de `git apply`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not trust the line counts in the hunk headers`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --recount --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--directory`

Añade el prefijo indicado a las rutas afectadas antes de procesarlas. En Git 2.51.1, la ayuda corta expresa el contrato como `prepend <root> to all filenames`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --directory=valor --check cambio.patch
git status --short
```

### `--allow-empty`

Permite continuar cuando el cambio produce un commit sin diferencias. En Git 2.51.1, la ayuda corta expresa el contrato como `don't return error for empty patches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git apply --allow-empty --check cambio.patch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git cherry-pick`](../patching/cherry-pick.md)
- [`git rebase`](../patching/rebase.md)

## Fuente

- [git-apply - Apply a patch to files and/or to the index](https://git-scm.com/docs/git-apply)
