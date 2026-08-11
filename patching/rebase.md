---
title: "git rebase"
source: "https://git-scm.com/docs/git-rebase"
section: "patching"
status: "expanded"
---

# `git rebase`

Este caso usa `git rebase` para reaplicar commits sobre una base distinta. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git rebase aplica diffs o commits y mantiene un estado que puede continuar o abortarse. Recibe como entrada un parche, un commit o un rango que representa cambios. La operación consiste en reaplicar commits sobre una base distinta.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | un parche, un commit o un rango que representa cambios. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | reaplicar commits sobre una base distinta. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: reaplicar commits sobre una base distinta. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git status`, `git diff --check` y `git log --oneline --decorate -n 10`. |

## Requisitos y laboratorio

Trabaja sobre una rama de prueba y crea una etiqueta o rama de respaldo antes de aplicar una serie.

```bash
lab_dir="$(mktemp -d)"
git init "$lab_dir/proyecto"
git -C "$lab_dir/proyecto" config user.name "Persona de prueba"
git -C "$lab_dir/proyecto" config user.email "prueba@example.test"
printf 'línea base\n' > "$lab_dir/proyecto/archivo.txt"
git -C "$lab_dir/proyecto" add archivo.txt
git -C "$lab_dir/proyecto" commit -m "base"
cd "$lab_dir/proyecto"
```

Antes de ejecutar el ejemplo, confirma la raíz con `git rev-parse --show-toplevel` cuando exista un repositorio. Registra `git status --short` y las referencias que puedan cambiar.

## Modelo de funcionamiento

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

Para comprobar el resultado: el diff y el historial muestran si cambiaron archivos, índice o commits. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git switch tema-portada
git rebase main
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: un parche, un commit o un rango que representa cambios.
- La operación observable es: reaplicar commits sobre una base distinta.
- La comprobación se realiza mediante: el diff y el historial muestran si cambiaron archivos, índice o commits.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git rebase [-i | --interactive] [<options>] [--exec <cmd>]
	[--onto <newbase> | --keep-base] [<upstream> [<branch>]]
git rebase [-i | --interactive] [<options>] [--exec <cmd>] [--onto <newbase>]
	--root [<branch>]
```

### Uso verificado con `git version 2.51.1`

```text
git rebase [-i] [options] [--exec <cmd>] [--onto <newbase> | --keep-base] [<upstream> [<branch>]]
   or: git rebase [-i] [options] [--exec <cmd>] [--onto <newbase>] --root [<branch>]
   or: git rebase --continue | --abort | --skip | --edit-todo
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git rebase -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | reaplicar commits sobre una base distinta | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git rebase a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Sesión interrumpida | Continuar o cancelar una secuencia después de revisar el estado. | Consulta `git status` antes de elegir la acción. |
| Validación | Comprobar el resultado de git rebase con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-i` | Activa la forma corta del modo interactivo o una opción propia de la orden. |
| `--interactive` | Abre una selección interactiva antes de aplicar la operación. |
| `--exec` | Activa el modo `--exec`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--onto` | Activa el modo `--onto`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--keep-base` | Activa el modo `--keep-base`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--root` | Activa el modo `--root`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--continue` | Reanuda una secuencia pausada después de resolver su estado. |
| `--abort` | Cancela la secuencia y restaura el punto que la orden registró al comenzar. |
| `--skip` | Omite el elemento actual y continúa la secuencia. |
| `--edit-todo` | Activa el modo `--edit-todo`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-verify` | Desactiva el comportamiento `verify` para esta invocación. |
| `--verify` | Exige que el nombre o estructura cumpla el contrato antes de continuar. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--no-stat` | Desactiva el comportamiento `stat` para esta invocación. |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `--verbose` | Aumenta el detalle enviado a la salida. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `--stat` | Resume cambios mediante conteos por ruta. |
| `--signoff` | Activa el modo `--signoff`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--committer-date-is-author-date` | Aplica una fecha, duración o política de vencimiento. |
| `--reset-author-date` | Aplica una fecha, duración o política de vencimiento. |
| `-C` | Ejecuta Git como si se hubiera iniciado en el directorio indicado. |
| `--ignore-whitespace` | Excluye elementos que cumplan la condición indicada. |
| `--whitespace` | Activa el modo `--whitespace`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-f` | Activa la forma corta de la operación forzada. |
| `--force-rebase` | Omite una protección concreta de la orden; requiere verificar origen y destino. |
| `--no-ff` | Desactiva el comportamiento `ff` para esta invocación. |
| `--ff` | Activa el modo `--ff`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--quit` | Sale de la secuencia y conserva el estado que la documentación define. |
| `--show-current-patch` | Incluye información adicional en la salida. |
| `--apply` | Activa el modo `--apply`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-m` | Activa el modo `-m`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--merge` | Activa el modo `--merge`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--rerere-autoupdate` | Activa el modo `--rerere-autoupdate`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--empty` | Activa el modo `--empty`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--autosquash` | Activa el modo `--autosquash`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--update-refs` | Selecciona o modifica referencias dentro del alcance de la orden. |
| `-S` | Activa el modo `-S`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--gpg-sign` | Activa el modo `--gpg-sign`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--autostash` | Activa el modo `--autostash`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-x` | Activa el modo `-x`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-r` | Activa el modo `-r`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--rebase-merges` | Activa el modo `--rebase-merges`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--fork-point` | Activa el modo `--fork-point`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-s` | Activa el modo `-s`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--strategy` | Selecciona el algoritmo o estrategia que procesa la entrada. |
| `-X` | Activa el modo `-X`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--strategy-option` | Selecciona el algoritmo o estrategia que procesa la entrada. |
| `--reschedule-failed-exec` | Activa el modo `--reschedule-failed-exec`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reapply-cherry-picks` | Activa el modo `--reapply-cherry-picks`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| Un parche no aplica | El contexto no coincide con el contenido actual | Inspecciona los rechazos o resuelve el conflicto antes de continuar. |
| La secuencia queda en pausa | Git espera una resolución o una decisión | Consulta `git status` y usa `--continue`, `--skip` o `--abort`. |
| El resultado contiene commits vacíos | Los cambios ya existen o se resolvieron sin diferencias | Revisa el diff y aplica la política de commits vacíos de la orden. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: reaplicar commits sobre una base distinta. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Trabaja en una rama de prueba. Compara `git diff`, `git diff --staged` y `git log --oneline --graph` antes y después.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git replay`](../patching/replay.md)
- [`git cherry-pick`](../patching/cherry-pick.md)
- [`git revert`](../patching/revert.md)

## Fuente

- [git-rebase - Reapply commits on top of another base tip](https://git-scm.com/docs/git-rebase)
