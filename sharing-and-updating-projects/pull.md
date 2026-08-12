---
title: "git pull"
source: "https://git-scm.com/docs/git-pull"
section: "sharing-and-updating-projects"
status: "source-audited"
version: "2.55.0"
---

# `git pull`

Este caso usa `git pull` para descargar cambios e integrarlos en la rama actual.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git pull --ff-only origin main
```

La invocación `git pull --ff-only origin main` ejecuta esta operación: descargar cambios e integrarlos en la rama actual. Después, las referencias locales y remotas permiten separar descarga, integración y publicación.

## Sintaxis y formas de invocación

```text
git pull [<options>] [<repository> [<refspec>…]]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git pull [<options>] [<repository> [<refspec>...]]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git pull -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git pull --verbose --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git pull --quiet --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git pull --progress --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

```bash
git pull --recurse-submodules=valor --ff-only origin main
git branch -vv
```

### `-r` y `--rebase`

Activa rebase durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `incorporate changes by rebasing rather than merging`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--rebase`

```bash
git pull --rebase=valor --ff-only origin main
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

### `-n`

Impide n durante esta invocación de `git pull`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not show a diffstat at the end of the merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull -n --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stat`

Resume cambios mediante conteos por ruta.

Esta forma se usa cuando `git pull` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque estadísticas actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git pull --stat --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--compact-summary`

Incluye compact summary en la salida o cambia cómo `git pull` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show a compact-summary at the end of the merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --compact-summary --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--log`

Incluye log en la entrada, el resultado o el registro que construye `git pull`. En Git 2.51.1, la ayuda corta expresa el contrato como `add (at most <n>) entries from shortlog to merge commit message`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --log=5 --ff-only origin main
git branch -vv
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signoff`

Añade una línea `Signed-off-by` al mensaje con la identidad del committer. En Git 2.51.1, la ayuda corta expresa el contrato como `add a Signed-off-by trailer`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --signoff --ff-only origin main
git branch -vv
```

### `--squash`

Crea un commit marcado para fusionar cambios y mensajes durante rebase autosquash. En Git 2.51.1, la ayuda corta expresa el contrato como `create a single commit instead of doing a merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --squash --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--commit`

Ejecuta commit durante descargar cambios e integrarlos en la rama actual. En Git 2.51.1, la ayuda corta expresa el contrato como `perform a commit if the merge succeeds (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --commit --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--edit`

Abre la representación editable que define la orden antes de aplicarla.

```bash
git pull --edit --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--cleanup`

Selecciona cómo Git retira comentarios y espacios del mensaje antes de crear el commit.

```bash
git pull --cleanup=all --ff-only origin main
git branch -vv
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ff`

Permite ff cuando la forma predeterminada de `git pull` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow fast-forward`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --ff --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ff-only`

Limita descargar cambios e integrarlos en la rama actual al alcance identificado por ff only. En Git 2.51.1, la ayuda corta expresa el contrato como `abort if fast-forward is not possible`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git pull` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque ff only actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git pull --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify`

Exige que el nombre o estructura cumpla el contrato antes de continuar.

```bash
git pull --verify --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verify-signatures`

Valida el dato o estado antes de producir el resultado.

```bash
git pull --verify-signatures --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--autostash`

Activa autostash durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `automatically stash/stash pop before and after`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --autostash --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-s` y `--strategy`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git pull` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `--strategy`

```bash
git pull --strategy=ort --ff-only origin main
git branch -vv
```

En esta forma, `ort` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

### `-X` y `--strategy-option`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git pull` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

#### Ejemplo con `--strategy-option`

```bash
git pull --strategy-option=Ana --ff-only origin main
git branch -vv
```

En esta forma, `Ana` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

### `-S` y `--gpg-sign`

Activa gpg sign durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--gpg-sign`

```bash
git pull --gpg-sign=user.name --ff-only origin main
git branch -vv
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

### `--allow-unrelated-histories`

Permite permitir unrelated histories cuando la forma predeterminada de `git pull` lo rechazaría o lo omitiría. En Git 2.51.1, la ayuda corta expresa el contrato como `allow merging unrelated histories`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --allow-unrelated-histories --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git pull --all --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a` y `--append`

Activa append durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `append to .git/FETCH_HEAD instead of overwriting`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--append`

```bash
git pull --append --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--upload-pack`

Define upload pack con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `path to upload pack on remote end`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --upload-pack=archivo.txt --ff-only origin main
git branch -vv
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git pull --force --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-t` y `--tags`

Incluye o selecciona etiquetas según la operación.

#### Ejemplo con `--tags`

```bash
git pull --tags --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-p` y `--prune`

Retira entradas que ya no cumplen la condición documentada.

#### Ejemplo con `--prune`

```bash
git pull --prune --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-j` y `--jobs`

Define cuántas tareas puede ejecutar Git en paralelo para la operación.

#### Ejemplo con `--jobs`

```bash
git pull --jobs=5 --ff-only origin main
git branch -vv
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

```bash
git pull --dry-run --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-k` y `--keep`

Conserva el asunto del mensaje recibido según la forma que define el comando. En Git 2.51.1, la ayuda corta expresa el contrato como `keep downloaded pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--keep`

```bash
git pull --keep --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--depth`

Establece un límite numérico para la selección o el recorrido.

```bash
git pull --depth=2 --ff-only origin main
git branch -vv
```

El ejemplo usa `2` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow-since`

Activa historial shallow desde una fecha durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `deepen history of shallow repository based on time`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --shallow-since=2026-01-15T10:00:00Z --ff-only origin main
git branch -vv
```

El ejemplo usa `2026-01-15T10:00:00Z` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow-exclude`

Excluye elementos que cumplan la condición indicada.

```bash
git pull --shallow-exclude=refs/heads/main --ff-only origin main
git branch -vv
```

El ejemplo usa `refs/heads/main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--deepen`

Activa deepen durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `deepen history of shallow clone`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --deepen=5 --ff-only origin main
git branch -vv
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unshallow`

Activa unshallow durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `convert to a complete repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --unshallow --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--update-shallow`

Actualiza actualizar historial shallow como parte de descargar cambios e integrarlos en la rama actual.

```bash
git pull --update-shallow --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--refmap`

Define refmap para esta ejecución de `git pull`. En Git 2.51.1, la ayuda corta expresa el contrato como `specify fetch refmap`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --refmap=main --ff-only origin main
git branch -vv
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-o` y `--server-option`

Activa server option durante descargar cambios e integrarlos en la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `option to transmit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--server-option`

```bash
git pull --server-option=valor --ff-only origin main
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

### `-4` y `--ipv4`

Limita descargar cambios e integrarlos en la rama actual al alcance identificado por ipv4. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv4 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--ipv4`

```bash
git pull --ipv4 --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-6` y `--ipv6`

Limita descargar cambios e integrarlos en la rama actual al alcance identificado por ipv6. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv6 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--ipv6`

```bash
git pull --ipv6 --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--negotiation-tip`

Limita descargar cambios e integrarlos en la rama actual al alcance identificado por negotiation tip. En Git 2.51.1, la ayuda corta expresa el contrato como `report that we have only objects reachable from this object`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --negotiation-tip=valor --ff-only origin main
git branch -vv
```

### `--show-forced-updates`

Incluye información adicional en la salida.

```bash
git pull --show-forced-updates --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--set-upstream`

Configura la asociación upstream después de actualizar la referencia remota. En Git 2.51.1, la ayuda corta expresa el contrato como `set upstream for git pull/fetch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git pull --set-upstream --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-progress --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-recurse-submodules --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-rebase`

Desactiva para esta invocación el comportamiento que habilita `--rebase`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-rebase --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stat`

Desactiva para esta invocación el comportamiento que habilita `--stat`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-stat --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-log`

Desactiva para esta invocación el comportamiento que habilita `--log`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-log --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signoff`

Desactiva para esta invocación el comportamiento que habilita `--signoff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-signoff --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-squash`

Desactiva para esta invocación el comportamiento que habilita `--squash`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-squash --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-commit`

Desactiva para esta invocación el comportamiento que habilita `--commit`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-commit --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-edit`

Conserva el mensaje existente sin abrir el editor.

```bash
git pull --no-edit --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ff`

Desactiva para esta invocación el comportamiento que habilita `--ff`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-ff --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verify`

Desactiva para esta invocación el comportamiento que habilita `--verify`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-verify --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verify-signatures`

Desactiva para esta invocación el comportamiento que habilita `--verify-signatures`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-verify-signatures --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-autostash`

Desactiva para esta invocación el comportamiento que habilita `--autostash`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-autostash --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-gpg-sign`

Desactiva para esta invocación el comportamiento que habilita `--gpg-sign`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-gpg-sign --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-all`

Desactiva para esta invocación el comportamiento que habilita `--all`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-all --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tags`

Desactiva para esta invocación el comportamiento que habilita `--tags`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-tags --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-show-forced-updates`

Desactiva para esta invocación el comportamiento que habilita `--show-forced-updates`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git pull --no-show-forced-updates --ff-only origin main
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git push`](../sharing-and-updating-projects/push.md)
- [`git ls-remote`](../sharing-and-updating-projects/ls-remote.md)
- [`git remote`](../sharing-and-updating-projects/remote.md)

## Fuente

- [git-pull - Fetch from and integrate with another repository or a local branch](https://git-scm.com/docs/git-pull)
