---
title: "git fetch"
source: "https://git-scm.com/docs/git-fetch"
section: "sharing-and-updating-projects"
status: "source-audited"
version: "2.55.0"
---

# `git fetch`

Este caso usa `git fetch` para descargar objetos y referencias sin integrar la rama actual.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git fetch origin
git log --oneline main..origin/main
```

La invocación `git fetch origin` ejecuta esta operación: descargar objetos y referencias sin integrar la rama actual. Después, las referencias locales y remotas permiten separar descarga, integración y publicación.

## Sintaxis y formas de invocación

```text
git fetch [<options>] [<repository> [<refspec>…]]
git fetch [<options>] <group>
git fetch --multiple [<options>] [(<repository>|<group>)…]
git fetch --all [<options>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git fetch [<options>] [<repository> [<refspec>...]]
   or: git fetch [<options>] <group>
   or: git fetch --multiple [<options>] [(<repository> | <group>)...]
   or: git fetch --all [<options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git fetch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--multiple` y `-m`

Activa multiple durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `fetch from multiple remotes`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--multiple`

```bash
git fetch --multiple origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git fetch --all origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git fetch --verbose origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git fetch --quiet origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--set-upstream`

Configura la asociación upstream después de actualizar la referencia remota. En Git 2.51.1, la ayuda corta expresa el contrato como `set upstream for git pull/fetch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fetch --set-upstream origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a` y `--append`

Activa append durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `append to .git/FETCH_HEAD instead of overwriting`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--append`

```bash
git fetch --append origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--atomic`

Exige que el conjunto se aplique completo o no se aplique.

```bash
git fetch --atomic origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--upload-pack`

Define upload pack con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `path to upload pack on remote end`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fetch --upload-pack=archivo.txt origin
git branch -vv
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git fetch --force origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-t` y `--tags`

Incluye o selecciona etiquetas según la operación.

#### Ejemplo con `--tags`

```bash
git fetch --tags origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-n`

Impide n durante esta invocación de `git fetch`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not fetch all tags (--no-tags)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fetch -n origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tags`

Desactiva el comportamiento `tags` para esta invocación.

```bash
git fetch --no-tags origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-j` y `--jobs`

Define cuántas tareas puede ejecutar Git en paralelo para la operación. En Git 2.51.1, la ayuda corta expresa el contrato como `number of submodules fetched in parallel`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--jobs`

```bash
git fetch --jobs=5 origin
git branch -vv
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

### `--prefetch`

Activa prefetch durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `modify the refspec to place all refs within refs/prefetch/`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fetch --prefetch origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p` y `--prune`

Retira entradas que ya no cumplen la condición documentada.

#### Ejemplo con `--prune`

```bash
git fetch --prune origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-P` y `--prune-tags`

Selecciona o modifica referencias dentro del alcance de la orden.

#### Ejemplo con `--prune-tags`

```bash
git fetch --prune-tags origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

```bash
git fetch --recurse-submodules=valor origin
git branch -vv
```

### `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

```bash
git fetch --dry-run origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--porcelain`

Produce un contrato de salida destinado a scripts.

```bash
git fetch --porcelain origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--write-fetch-head`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción cambia cómo `git fetch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fetch --write-fetch-head origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-k` y `--keep`

Conserva el asunto del mensaje recibido según la forma que define el comando. En Git 2.51.1, la ayuda corta expresa el contrato como `keep downloaded pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--keep`

```bash
git fetch --keep origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-u` y `--update-head-ok`

Selecciona o modifica referencias dentro del alcance de la orden.

#### Ejemplo con `--update-head-ok`

```bash
git fetch --update-head-ok origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git fetch --progress origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--depth`

Establece un límite numérico para la selección o el recorrido.

```bash
git fetch --depth=2 origin
git branch -vv
```

El ejemplo usa `2` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow-since`

Activa historial shallow desde una fecha durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `deepen history of shallow repository based on time`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fetch --shallow-since=2026-01-15T10:00:00Z origin
git branch -vv
```

El ejemplo usa `2026-01-15T10:00:00Z` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow-exclude`

Excluye elementos que cumplan la condición indicada.

```bash
git fetch --shallow-exclude=refs/heads/main origin
git branch -vv
```

El ejemplo usa `refs/heads/main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--deepen`

Activa deepen durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `deepen history of shallow clone`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fetch --deepen=5 origin
git branch -vv
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unshallow`

Activa unshallow durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `convert to a complete repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fetch --unshallow origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--refetch`

Activa refetch durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `re-fetch without negotiating common commits`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fetch --refetch origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--update-shallow`

Actualiza actualizar historial shallow como parte de descargar objetos y referencias sin integrar la rama actual.

```bash
git fetch --update-shallow origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--refmap`

Define refmap para esta ejecución de `git fetch`. En Git 2.51.1, la ayuda corta expresa el contrato como `specify fetch refmap`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fetch --refmap=main origin
git branch -vv
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-o` y `--server-option`

Activa server option durante descargar objetos y referencias sin integrar la rama actual. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `option to transmit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--server-option`

```bash
git fetch --server-option=valor origin
git branch -vv
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comparar la rama local con su upstream.

### `-4` y `--ipv4`

Limita descargar objetos y referencias sin integrar la rama actual al alcance identificado por ipv4. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv4 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--ipv4`

```bash
git fetch --ipv4 origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `-6` y `--ipv6`

Limita descargar objetos y referencias sin integrar la rama actual al alcance identificado por ipv6. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv6 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--ipv6`

```bash
git fetch --ipv6 origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--negotiation-tip`

Limita descargar objetos y referencias sin integrar la rama actual al alcance identificado por negotiation tip. En Git 2.51.1, la ayuda corta expresa el contrato como `report that we have only objects reachable from this object`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fetch --negotiation-tip=valor origin
git branch -vv
```

### `--negotiate-only`

Ejecuta la negociación de objetos sin descargar el pack resultante.

```bash
git fetch --negotiate-only origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--filter`

Limita los objetos transferidos mediante una especificación de filtro de clon parcial. En Git 2.51.1, la ayuda corta expresa el contrato como `object filtering`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fetch --filter=valor origin
git branch -vv
```

### `--auto-maintenance`

Ejecuta auto maintenance durante descargar objetos y referencias sin integrar la rama actual. En Git 2.51.1, la ayuda corta expresa el contrato como `run 'maintenance --auto' after fetching`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git fetch --auto-maintenance origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--auto` y `--auto-gc`

Ejecuta auto gc durante descargar objetos y referencias sin integrar la rama actual. En Git 2.51.1, la ayuda corta expresa el contrato como `run 'maintenance --auto' after fetching`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--auto`

```bash
git fetch --auto origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

#### Ejemplo con `--auto-gc`

```bash
git fetch --auto-gc origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream.

### `--show-forced-updates`

Incluye información adicional en la salida.

```bash
git fetch --show-forced-updates origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--write-commit-graph`

Permite crear o escribir el elemento seleccionado.

```bash
git fetch --write-commit-graph origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git fetch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fetch --stdin origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-all`

Desactiva para esta invocación el comportamiento que habilita `--all`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git fetch --no-all origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git fetch --no-recurse-submodules origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-write-fetch-head`

Desactiva para esta invocación el comportamiento que habilita `--write-fetch-head`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git fetch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fetch --no-write-fetch-head origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-auto-maintenance`

Desactiva para esta invocación el comportamiento que habilita `--auto-maintenance`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git fetch --no-auto-maintenance origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-auto`

Desactiva para esta invocación el comportamiento que habilita `--auto`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git fetch --no-auto origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-auto-gc`

Desactiva para esta invocación el comportamiento que habilita `--auto-gc`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git fetch --no-auto-gc origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-show-forced-updates`

Desactiva para esta invocación el comportamiento que habilita `--show-forced-updates`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git fetch --no-show-forced-updates origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-write-commit-graph`

Desactiva para esta invocación el comportamiento que habilita `--write-commit-graph`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git fetch --no-write-commit-graph origin
git branch -vv
```

 La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--negotiation-restrict` y `--negotiation-include`

Git normalmente comunica al servidor commits alcanzables desde todas las referencias locales. `--negotiation-restrict=<commit|glob>` limita las puntas consideradas; su alias heredado es `--negotiation-tip`. `--negotiation-include=<commit|glob>` fuerza puntas adicionales como líneas `have`, incluso si el algoritmo no las seleccionaría. Ambas opciones se pueden repetir.

```bash
git fetch --negotiation-restrict=refs/heads/main \
  --negotiation-include='refs/heads/release-*' origin
```

Una restricción incorrecta puede aumentar el pack recibido porque el servidor descubre menos historia común; no cambia qué referencias se solicitan.

### `--submodule-prefix` y `--recurse-submodules-default`

Son opciones internas del recorrido de submódulos. `--submodule-prefix=<ruta>` antepone una ruta a mensajes como `Fetching submodule ...`. `--recurse-submodules-default=(yes|on-demand)` aporta un valor predeterminado temporal; `.gitmodules`, la configuración y `--[no-]recurse-submodules` tienen precedencia.

```bash
git fetch --recurse-submodules-default=on-demand \
  --submodule-prefix=vendor/ origin
```

Los scripts ordinarios deben preferir `--recurse-submodules=<modo>`; estas dos formas se documentan porque `--help-all` las expone y Git las usa en llamadas internas.

## Páginas relacionadas

- [`git ls-remote`](../sharing-and-updating-projects/ls-remote.md)
- [`git bundle`](../sharing-and-updating-projects/bundle.md)
- [`git pull`](../sharing-and-updating-projects/pull.md)

## Fuente

- [git-fetch - Download objects and refs from another repository](https://git-scm.com/docs/git-fetch)
