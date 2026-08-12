---
title: "git rev-list"
source: "https://git-scm.com/docs/git-rev-list"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git rev-list`

Este caso usa `git rev-list` para enumerar commits alcanzables según límites y filtros.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git rev-list --count main
git rev-list main --not origin/main
```

La invocación `git rev-list --count main` ejecuta esta operación: enumerar commits alcanzables según límites y filtros. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git rev-list [<options>] <commit>… [--] [<path>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git rev-list [<options>] <commit>... [--] [<path>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git rev-list -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--max-count`

Limita el número de registros producidos.

```bash
git rev-list --max-count=5 --count main
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-age`

Aplica una fecha, duración o política de vencimiento.

```bash
git rev-list --max-age=valor --count main
printf 'exit=%s\n' "$?"
```

### `--min-age`

Aplica una fecha, duración o política de vencimiento.

```bash
git rev-list --min-age=valor --count main
printf 'exit=%s\n' "$?"
```

### `--sparse`

Permite operar sobre entradas que quedan fuera de la selección sparse activa.

```bash
git rev-list --sparse --count main
printf 'exit=%s\n' "$?"
```

### `--no-merges`

Desactiva el comportamiento `merges` para esta invocación.

```bash
git rev-list --no-merges --count main
printf 'exit=%s\n' "$?"
```

### `--min-parents`

Establece un límite numérico para la selección o el recorrido.

```bash
git rev-list --min-parents=5 --count main
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-min-parents`

Desactiva el comportamiento `min-parents` para esta invocación.

```bash
git rev-list --no-min-parents --count main
printf 'exit=%s\n' "$?"
```

### `--max-parents`

Establece un límite numérico para la selección o el recorrido.

```bash
git rev-list --max-parents=5 --count main
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-max-parents`

Desactiva el comportamiento `max-parents` para esta invocación.

```bash
git rev-list --no-max-parents --count main
printf 'exit=%s\n' "$?"
```

### `--remove-empty`

Retira elementos según las condiciones de la orden.

```bash
git rev-list --remove-empty --count main
printf 'exit=%s\n' "$?"
```

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git rev-list --all --count main
printf 'exit=%s\n' "$?"
```

### `--branches`

Incluye o selecciona ramas según la operación.

```bash
git rev-list --branches --count main
printf 'exit=%s\n' "$?"
```

### `--tags`

Incluye o selecciona etiquetas según la operación.

```bash
git rev-list --tags --count main
printf 'exit=%s\n' "$?"
```

### `--remotes`

Activa remotes durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git rev-list --remotes --count main
printf 'exit=%s\n' "$?"
```

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git rev-list` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git rev-list --stdin --count main
printf 'exit=%s\n' "$?"
```

### `--exclude-hidden`

Excluye elementos que cumplan la condición indicada.

```bash
git rev-list --exclude-hidden=valor --count main
printf 'exit=%s\n' "$?"
```

### `--quiet`

Reduce mensajes que no representan errores.

```bash
git rev-list --quiet --count main
printf 'exit=%s\n' "$?"
```

### `--topo-order`

Activa topo order durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git rev-list --topo-order --count main
printf 'exit=%s\n' "$?"
```

### `--date-order`

Aplica una fecha, duración o política de vencimiento.

```bash
git rev-list --date-order --count main
printf 'exit=%s\n' "$?"
```

### `--reverse`

Invierte el orden del recorrido o resultado.

```bash
git rev-list --reverse --count main
printf 'exit=%s\n' "$?"
```

### `--parents`

Activa parents durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git rev-list --parents --count main
printf 'exit=%s\n' "$?"
```

### `--children`

Activa children durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git rev-list --children --count main
printf 'exit=%s\n' "$?"
```

### `--objects` y `--objects-edge`

Selecciona la representación o tratamiento de identificadores de objeto.

#### Ejemplo con `--objects`

```bash
git rev-list --objects --count main
printf 'exit=%s\n' "$?"
```

#### Ejemplo con `--objects-edge`

```bash
git rev-list --objects-edge --count main
printf 'exit=%s\n' "$?"
```

### `--disk-usage`

Activa disk usage durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git rev-list --disk-usage=valor --count main
printf 'exit=%s\n' "$?"
```

### `--unpacked`

Activa unpacked durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git rev-list --unpacked --count main
printf 'exit=%s\n' "$?"
```

### `--header` y `--pretty`

Selecciona un formato para representar commits.

#### Ejemplo con `--header`

```bash
git rev-list --header --count main
printf 'exit=%s\n' "$?"
```

#### Ejemplo con `--pretty`

```bash
git rev-list --pretty --count main
printf 'exit=%s\n' "$?"
```

### `--object-names`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git rev-list --object-names --count main
printf 'exit=%s\n' "$?"
```

### `--abbrev`

Reduce la representación visible del identificador sin cambiar el objeto.

```bash
git rev-list --abbrev=5 --count main
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-abbrev`

Desactiva el comportamiento `abbrev` para esta invocación.

```bash
git rev-list --no-abbrev --count main
printf 'exit=%s\n' "$?"
```

### `--abbrev-commit`

Activa abbrev commit durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git rev-list --abbrev-commit --count main
printf 'exit=%s\n' "$?"
```

### `--left-right`

Activa left right durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git rev-list --left-right --count main
printf 'exit=%s\n' "$?"
```

### `--count`

Establece un límite numérico para la selección o el recorrido.

```bash
git rev-list --count main
printf 'exit=%s\n' "$?"
```

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git rev-list -z --count main
printf 'exit=%s\n' "$?"
```

### `--bisect`

Activa bisect durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git rev-list --bisect --count main
printf 'exit=%s\n' "$?"
```

### `--bisect-vars`

Activa bisect vars durante enumerar commits alcanzables según límites y filtros. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git rev-list --bisect-vars --count main
printf 'exit=%s\n' "$?"
```

### `--bisect-all`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git rev-list --bisect-all --count main
printf 'exit=%s\n' "$?"
```

### `--no-object-names`

Desactiva para esta invocación el comportamiento que habilita `--object-names`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git rev-list --no-object-names --count main
printf 'exit=%s\n' "$?"
```

### `--after`, `--before`, `--until`, `--since-as-filter` y `--max-count-oldest`

`--after=<fecha>` es sinónimo de `--since`; `--before=<fecha>` es sinónimo de `--until`. El filtro normal detiene el recorrido cuando alcanza commits suficientemente antiguos; `--since-as-filter` recorre todos los commits y filtra la salida al final. `--max-count-oldest=<n>` conserva los últimos `<n>` commits del resultado, mientras `--max-count=<n>` conserva los primeros.

```bash
git rev-list --after='2026-01-01' --before='2026-02-01' main
git rev-list --since-as-filter='2026-01-01' main
git rev-list --max-count-oldest=3 main
```

### `--author-date-order`, `--in-commit-order` y `--timestamp`

`--author-date-order` evita mostrar un padre antes que sus hijos y, dentro de esa restricción, usa la fecha de autor. `--in-commit-order` ordena la salida de `--objects` por el commit que alcanzó cada objeto. `--timestamp` antepone el timestamp bruto del commit.

```bash
git rev-list --author-date-order --timestamp --max-count=5 main
git rev-list --objects --in-commit-order --max-count=2 main
```

### `--ancestry-path`, `--full-history`, `--simplify-merges`, `--simplify-by-decoration`, `--dense`, `--show-pulls` y `--exclude-first-parent-only`

Estas opciones cambian la simplificación del grafo. `--ancestry-path` conserva commits que son ancestros o descendientes dentro del rango; `--full-history` evita la poda predeterminada; `--simplify-merges` retira fusiones que quedan redundantes después del recorrido; `--simplify-by-decoration` conserva commits señalados por referencias; `--dense` omite commits TREESAME; `--show-pulls` añade fusiones que incorporaron por primera vez un cambio; `--exclude-first-parent-only` sigue solo el primer padre al calcular el lado excluido de un rango.

```bash
git rev-list --ancestry-path --full-history main..tema
git rev-list --simplify-merges --show-pulls main -- README.md
git rev-list --exclude-first-parent-only origin/main..tema
```

### `--merges`, `--grep`, `--grep-reflog`, `--invert-grep`, `--regexp-ignore-case` y `--walk-reflogs`

`--merges` limita la salida a commits con al menos dos padres. `--grep=<patrón>` filtra mensajes; `--invert-grep` invierte la coincidencia y `--regexp-ignore-case` ignora mayúsculas. `--grep-reflog` busca en mensajes de reflog y requiere `--walk-reflogs`.

```bash
git rev-list --merges --grep='integración' --regexp-ignore-case main
git rev-list --walk-reflogs --grep-reflog='rebase' --invert-grep HEAD
```

### `--alternate-refs`, `--glob` y `--maximal-only`

`--alternate-refs` incluye las puntas de repositorios alternativos; `--glob=<patrón>` incluye referencias que coinciden con el glob bajo `refs/`; `--maximal-only` conserva commits que no son alcanzables desde otro commit del rango.

```bash
git rev-list --glob='refs/heads/release-*' --maximal-only
git rev-list --alternate-refs --objects
```

### `--boundary`, `--cherry`, `--cherry-mark` y `--cherry-pick`

`--boundary` añade commits límite excluidos con el prefijo `-`. En una diferencia simétrica, `--cherry-mark` marca pares equivalentes con `=` y los demás con `+`; `--cherry-pick` omite los pares equivalentes; `--cherry` equivale a `--right-only --cherry-mark --no-merges`.

```bash
git rev-list --boundary main..tema
git rev-list --left-right --cherry-mark main...tema
git rev-list --cherry-pick main...tema
```

### `--filter-provided-objects`, `--filter-print-omitted`, `--no-filter`, `--objects-edge-aggressive` y `--maximal-only`

Con `--filter`, `--filter-provided-objects` aplica el filtro también a objetos nombrados explícitamente y `--filter-print-omitted` escribe los OID omitidos con el prefijo `~`. `--no-filter` cancela filtros anteriores. `--objects-edge-aggressive` añade objetos límite con una búsqueda más costosa para construir packs delgados.

```bash
git rev-list --objects --filter=blob:none \
  --filter-provided-objects --filter-print-omitted main
git rev-list --objects-edge-aggressive --boundary main..tema
```

### `--do-walk` y `--no-walk`

`--no-walk[=(sorted|unsorted)]` muestra solo los commits indicados, sin recorrer ancestros. `--do-walk` restaura el recorrido después de una opción que lo haya desactivado.

```bash
git rev-list --no-walk=unsorted HEAD~2 HEAD HEAD~1
git rev-list --no-walk HEAD --do-walk HEAD~2
```

### `--commit-header`, `--no-commit-header`, `--no-abbrev-commit`, `--timestamp` y `--relative-date`

`--no-commit-header` suprime la cabecera `commit <OID>` en formatos que la generan; `--commit-header` la restaura. `--no-abbrev-commit` usa OID completos. `--timestamp` muestra el tiempo Unix bruto y `--relative-date` solicita fechas relativas en los formatos que muestran fechas.

```bash
git rev-list --header --no-abbrev-commit --timestamp -1 HEAD
git rev-list --pretty=medium --relative-date -1 HEAD
```

### `--expand-tabs`, `--no-expand-tabs`, `--graph`, `--graph-lane-limit` y `--show-linear-break`

`--expand-tabs[=<n>]` expande tabuladores de mensajes; `--no-expand-tabs` los conserva. `--graph` dibuja el grafo; `--graph-lane-limit=<n>` reemplaza carriles que superan el límite por `~`, y cero desactiva el límite. `--show-linear-break[=<texto>]` separa ramas lineales cuando no se usa `--graph`.

```bash
git rev-list --graph --graph-lane-limit=4 --oneline --all
git rev-list --pretty=medium --expand-tabs=4 --show-linear-break='---' main
```

### `--show-notes`, `--show-notes-by-default`, `--standard-notes`, `--no-standard-notes` y `--show-signature`

`--show-notes[=<ref>]` añade notas de la referencia indicada; `--show-notes-by-default` usa las notas predeterminadas salvo que se seleccione otra referencia. `--standard-notes` restaura las referencias estándar y `--no-standard-notes` las excluye. `--show-signature` comprueba una firma GPG válida en cada commit mostrado.

```bash
git rev-list --pretty=medium --show-notes-by-default --show-signature -1 HEAD
git rev-list --pretty=medium --show-notes=refs/notes/revision -1 HEAD
```

## Páginas relacionadas

- [`git rev-parse`](../plumbing-read/rev-parse.md)
- [`git repo`](../plumbing-read/repo.md)
- [`git show-index`](../plumbing-read/show-index.md)

## Fuente

- [git-rev-list - Lists commit objects in reverse chronological order](https://git-scm.com/docs/git-rev-list)
