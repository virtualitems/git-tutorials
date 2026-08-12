---
title: "git format-patch"
source: "https://git-scm.com/docs/git-format-patch"
section: "email-and-patches"
status: "source-audited"
version: "2.55.0"
---

# `git format-patch`

Este caso usa `git format-patch` para representar commits como archivos de parche para correo.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Cada parche puede transportar autoría, mensaje y diferencias. El receptor valida, aplica y registra la serie en su propio historial.

Conserva el orden de la serie y separa autor de quien aplica el parche. Los conflictos se resuelven antes de continuar con el siguiente mensaje.

## Ejemplo mínimo

```bash
git format-patch origin/main..HEAD --output-directory parches/
```

La invocación `git format-patch origin/main..HEAD --output-directory parches/` ejecuta esta operación: representar commits como archivos de parche para correo. Después, el receptor obtiene parches o commits con el orden, autoría y mensaje esperados.

## Sintaxis y formas de invocación

```text
git format-patch [-k] [(-o|--output-directory) <dir> | --stdout]
		   [--no-thread | --thread[=<style>]]
		   [(--attach|--inline)[=<boundary>] | --no-attach]
		   [-s | --signoff]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git format-patch [<options>] [<since> | <revision-range>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git format-patch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-k` y `--keep-subject`

Incluye conservar subject en la entrada, el resultado o el registro que construye `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `don't strip/add [PATCH]`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--keep-subject`

```bash
git format-patch --keep-subject origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `-o` y `--output-directory`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

#### Ejemplo con `--output-directory`

```bash
git format-patch --output-directory=docs origin/main..HEAD
printf 'exit=%s\n' "$?"
```

En esta forma, `docs` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--stdout`

Incluye salida estándar en la salida o cambia cómo `git format-patch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print patches to standard out`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --stdout origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--no-thread`

Desactiva el comportamiento `thread` para esta invocación.

```bash
git format-patch --no-thread origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--thread`

Activa thread durante representar commits como archivos de parche para correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `enable message threading, styles: shallow, deep`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --thread=short origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--attach`

Activa attach durante representar commits como archivos de parche para correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `attach the patch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --attach=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--inline`

Activa inline durante representar commits como archivos de parche para correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git format-patch --inline=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--no-attach`

Desactiva el comportamiento `attach` para esta invocación.

```bash
git format-patch --no-attach origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `-s` y `--signoff`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--signoff`

```bash
git format-patch --signoff origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `-n` y `--numbered`

Define numbered para esta ejecución de `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `use [PATCH n/m] even with a single patch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--numbered`

```bash
git format-patch --numbered origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `-N`

Define N para esta ejecución de `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `use [PATCH] even with multiple patches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch -N origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--no-numbered`

Desactiva el comportamiento `numbered` para esta invocación.

```bash
git format-patch --no-numbered origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--cover-letter`

Genera cover letter como parte del resultado de `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate a cover letter`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --cover-letter origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--numbered-files`

Incluye numbered files en la salida o cambia cómo `git format-patch` la representa.

```bash
git format-patch --numbered-files origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--suffix`

Define suffix para esta ejecución de `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `use <sfx> instead of '.patch'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --suffix=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--start-number`

Activa start number durante representar commits como archivos de parche para correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `start numbering patches at <n> instead of 1`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --start-number=5 origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--reroll-count`

Establece un límite numérico para la selección o el recorrido.

#### Ejemplo con `--reroll-count`

```bash
git format-patch --reroll-count=5 origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--filename-max-length`

Establece un límite numérico para la selección o el recorrido.

```bash
git format-patch --filename-max-length=5 origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--rfc`

Incluye rfc en la entrada, el resultado o el registro que construye `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `add <rfc> (default 'RFC') before 'PATCH'`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --rfc=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--cover-from-description`

Genera cover from description como parte del resultado de `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `generate parts of a cover letter based on a branch's description`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --cover-from-description=all origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--description-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

```bash
git format-patch --description-file=rutas.txt origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--subject-prefix`

Define subject prefix para esta ejecución de `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `use [<prefix>] instead of [PATCH]`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --subject-prefix=refs/heads/ origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `refs/heads/` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--binary`

Selecciona la relación indicada por contenido binario; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-binary`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --binary origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--zero-commit`

Incluye zero commit en la salida o cambia cómo `git format-patch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output all-zero hash in From header`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --zero-commit origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--ignore-if-in-upstream`

Excluye elementos que cumplan la condición indicada.

```bash
git format-patch --ignore-if-in-upstream origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `-p`

Incluye p en la salida o cambia cómo `git format-patch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show patch format instead of default (patch + stat)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch -p origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--add-header`

Permite crear o escribir el elemento seleccionado.

```bash
git format-patch --add-header=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--to`

Incluye to en la entrada, el resultado o el registro que construye `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `add To: header`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --to=user@example.com origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `user@example.com` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cc`

Incluye cc en la entrada, el resultado o el registro que construye `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `add Cc: header`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --cc=user@example.com origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `user@example.com` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--from`

Define from para esta ejecución de `git format-patch`.

```bash
git format-patch --from=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--in-reply-to`

Activa in reply to durante representar commits como archivos de parche para correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `make first mail a reply to <message-id>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --in-reply-to='mensaje de ejemplo' origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `mensaje de ejemplo` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signature`

Incluye firma en la entrada, el resultado o el registro que construye `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `add a signature`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --signature=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--base`

Incluye base en la entrada, el resultado o el registro que construye `git format-patch`. En Git 2.51.1, la ayuda corta expresa el contrato como `add prerequisite tree info to the patch series`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --base=HEAD origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `HEAD` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signature-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia cómo `git format-patch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git format-patch --signature-file=rutas.txt origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git format-patch --quiet origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git format-patch --progress origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--interdiff`

Incluye interdiff en la salida o cambia cómo `git format-patch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show changes against <rev> in cover letter or single patch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --interdiff=valor origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--range-diff`

Incluye range diff en la salida o cambia cómo `git format-patch` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show changes against <refspec> in cover letter or single patch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --range-diff=main origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--creation-factor`

Activa creation factor durante representar commits como archivos de parche para correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `percentage by which creation is weighted`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git format-patch --creation-factor=5 origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-in-body-from`

Omite una protección concreta de la orden; requiere verificar origen y destino.

```bash
git format-patch --force-in-body-from origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--no-cover-letter`

Desactiva para esta invocación el comportamiento que habilita `--cover-letter`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git format-patch --no-cover-letter origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--no-add-header`

Desactiva para esta invocación el comportamiento que habilita `--add-header`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git format-patch --no-add-header origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--no-to`

Desactiva para esta invocación el comportamiento que habilita `--to`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git format-patch --no-to origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--no-cc`

Desactiva para esta invocación el comportamiento que habilita `--cc`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git format-patch --no-cc origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--no-signature`

Desactiva para esta invocación el comportamiento que habilita `--signature`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git format-patch --no-signature origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

### `--no-base`

Desactiva para esta invocación el comportamiento que habilita `--base`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git format-patch --no-base origin/main..HEAD --output-directory parches/
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git imap-send`](../email-and-patches/imap-send.md)
- [`git am`](../email-and-patches/am.md)
- [`git send-email`](../email-and-patches/send-email.md)

## Fuente

- [git-format-patch - Prepare patches for e-mail submission](https://git-scm.com/docs/git-format-patch)
