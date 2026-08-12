---
title: "git am"
source: "https://git-scm.com/docs/git-am"
section: "email-and-patches"
status: "source-audited"
version: "2.55.0"
---

# `git am`

Este caso usa `git am` para convertir una serie de parches de correo en commits.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Cada parche puede transportar autoría, mensaje y diferencias. El receptor valida, aplica y registra la serie en su propio historial.

Conserva el orden de la serie y separa autor de quien aplica el parche. Los conflictos se resuelven antes de continuar con el siguiente mensaje.

## Ejemplo mínimo

```bash
git am 0001-corrige-indice.patch
# Si aparece un conflicto:
git am --continue
```

La invocación `git am 0001-corrige-indice.patch` ejecuta esta operación: convertir una serie de parches de correo en commits. Después, el receptor obtiene parches o commits con el orden, autoría y mensaje esperados.

## Sintaxis y formas de invocación

```text
git am [--signoff] [--keep] [--[no-]keep-cr] [--[no-]utf8] [--[no-]verify]
	 [--[no-]3way] [--interactive] [--committer-date-is-author-date]
	 [--ignore-date] [--ignore-space-change | --ignore-whitespace]
	 [--whitespace=<action>] [-C<n>] [-p<n>] [--directory=<dir>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git am [<options>] [(<mbox> | <Maildir>)...]
   or: git am [<options>] (--continue | --skip | --abort)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git am -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--signoff` y `-s`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer to the commit message`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--signoff`

```bash
git am --signoff 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--keep` y `-k`

Conserva el asunto del mensaje recibido según la forma que define el comando. En Git 2.51.1, la ayuda corta expresa el contrato como `pass -k flag to git-mailinfo`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--keep`

```bash
git am --keep 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--keep-cr`

Conserva caracteres CR al procesar mensajes de correo. En Git 2.51.1, la ayuda corta expresa el contrato como `pass --keep-cr flag to git-mailsplit for mbox format`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git am --keep-cr 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--utf8` y `-u`

Controla la recodificación del mensaje de commit a UTF-8. En Git 2.51.1, la ayuda corta expresa el contrato como `recode into utf8 (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--utf8`

```bash
git am --utf8 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

```bash
git am --verify 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--3way` y `-3`

Intenta una fusión de tres vías cuando el parche no se aplica directamente y existen los blobs necesarios. En Git 2.51.1, la ayuda corta expresa el contrato como `allow fall back on 3way merging if needed`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--3way`

```bash
git am --3way 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--interactive` y `-i`

Abre una selección interactiva antes de aplicar la operación.

#### Ejemplo con `--interactive`

```bash
git am --interactive 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--committer-date-is-author-date`

Aplica una fecha, duración o política de vencimiento.

```bash
git am --committer-date-is-author-date 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--ignore-date`

Aplica una fecha, duración o política de vencimiento.

```bash
git am --ignore-date 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--ignore-space-change`

Excluye elementos que cumplan la condición indicada.

```bash
git am --ignore-space-change 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--ignore-whitespace`

Excluye elementos que cumplan la condición indicada.

```bash
git am --ignore-whitespace 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--whitespace`

Selecciona la acción que Git ejecuta cuando detecta errores de espacios en un parche. En Git 2.51.1, la ayuda corta expresa el contrato como `pass it through git-apply`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git am --whitespace=warn 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

```bash
git am -C 5 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p`

Activa p durante convertir una serie de parches de correo en commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pass it through git-apply`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git am -p 5 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--directory`

Añade el prefijo indicado a las rutas afectadas antes de procesarlas. En Git 2.51.1, la ayuda corta expresa el contrato como `pass it through git-apply`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git am --directory=valor 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--continue`

Reanuda una secuencia pausada después de resolver su estado.

Esta forma se usa cuando `git am` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque continuar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git am --continue
printf 'exit=%s\n' "$?"
```

### `--skip`

Omite el elemento actual y continúa la secuencia.

Esta forma se usa cuando `git am` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque omitir el elemento actual actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git am --skip
printf 'exit=%s\n' "$?"
```

### `--abort`

Cancela la secuencia y restaura el punto que la orden registró al comenzar.

Esta forma se usa cuando `git am` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque abortar actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git am --abort
printf 'exit=%s\n' "$?"
```

### `-n`

Comprueba n antes de aceptar el resultado de `git am`. En Git 2.51.1, la ayuda corta expresa el contrato como `bypass pre-applypatch and applypatch-msg hooks`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git am -n 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--no-verify`

Desactiva el comportamiento `verify` para esta invocación.

```bash
git am --no-verify 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git am --quiet 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--keep-non-patch` y `-b`

Activa conservar non parche durante convertir una serie de parches de correo en commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.  La misma línea de ayuda también acepta `-b` y `-mailinfo`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

#### Ejemplo con `--keep-non-patch`

```bash
git am --keep-non-patch 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `-m` y `--message-id`

Añade el identificador del mensaje de correo al mensaje de commit.  La misma línea de ayuda también acepta `-m` y `-m` y `-mailinfo`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

#### Ejemplo con `--message-id`

```bash
git am --message-id 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `-c` y `--scissors`

Reconoce la línea scissors y descarta el contenido anterior según el formato de correo. En Git 2.51.1, la ayuda corta expresa el contrato como `strip everything before a scissors line`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--scissors`

```bash
git am --scissors 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--quoted-cr`

Define cómo se tratan los caracteres CR que aparecen al final de líneas citadas. En Git 2.51.1, la ayuda corta expresa el contrato como `pass it through git-mailinfo`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git am --quoted-cr=warn 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude`

Excluye elementos que cumplan la condición indicada.

```bash
git am --exclude=archivo.txt 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git am --include=archivo.txt 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--patch-format`

Declara el formato de parche que debe interpretar la entrada. En Git 2.51.1, la ayuda corta expresa el contrato como `format the patch(es) are in`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git am --patch-format=oneline 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reject`

Conserva hunks que no pudieron aplicarse en archivos de rechazo para inspección manual. En Git 2.51.1, la ayuda corta expresa el contrato como `pass it through git-apply`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git am --reject 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--resolvemsg`

Sustituye el mensaje que se muestra cuando la aplicación necesita resolución manual.

```bash
git am --resolvemsg 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `-r` y `--resolved`

Activa resuelto durante convertir una serie de parches de correo en commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `synonyms for --continue`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git am` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque resuelto actúa sobre el estado que Git registró al iniciar la secuencia.

#### Ejemplo con `--resolved`

```bash
git am --resolved 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--quit`

Sale de la secuencia y conserva el estado que la documentación define.

Esta forma se usa cuando `git am` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque salir actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git am --quit
printf 'exit=%s\n' "$?"
```

### `--show-current-patch`

Incluye información adicional en la salida.

```bash
git am --show-current-patch=valor 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--retry`

Activa retry durante convertir una serie de parches de correo en commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `try to apply current patch again`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git am --retry 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--allow-empty`

Permite continuar cuando el cambio produce un commit sin diferencias. En Git 2.51.1, la ayuda corta expresa el contrato como `record the empty patch as an empty commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git am --allow-empty 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--rerere-autoupdate`

Actualiza rerere autoupdate como parte de convertir una serie de parches de correo en commits. En Git 2.51.1, la ayuda corta expresa el contrato como `update the index with reused conflict resolution if possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git am --rerere-autoupdate 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `-S` y `--gpg-sign`

Activa gpg sign durante convertir una serie de parches de correo en commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG-sign commits`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--gpg-sign`

```bash
git am --gpg-sign=user.name 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--empty`

Activa vacío durante convertir una serie de parches de correo en commits. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `how to handle empty patches`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git am --empty=valor 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--no-keep`

Desactiva para esta invocación el comportamiento que habilita `--keep`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git am --no-keep 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--no-keep-cr`

Desactiva para esta invocación el comportamiento que habilita `--keep-cr`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git am --no-keep-cr 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--no-utf8`

Desactiva para esta invocación el comportamiento que habilita `--utf8`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git am --no-utf8 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--no-3way`

Desactiva para esta invocación el comportamiento que habilita `--3way`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git am --no-3way 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--no-message-id`

Desactiva para esta invocación el comportamiento que habilita `--message-id`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git am --no-message-id 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--no-scissors`

Desactiva para esta invocación el comportamiento que habilita `--scissors`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git am --no-scissors 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--no-rerere-autoupdate`

Desactiva para esta invocación el comportamiento que habilita `--rerere-autoupdate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git am --no-rerere-autoupdate 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

### `--no-gpg-sign`

Desactiva para esta invocación el comportamiento que habilita `--gpg-sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git am --no-gpg-sign 0001-corrige-indice.patch
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git format-patch`](../email-and-patches/format-patch.md)
- [`git imap-send`](../email-and-patches/imap-send.md)

## Fuente

- [git-am - Apply a series of patches from a mailbox](https://git-scm.com/docs/git-am)
