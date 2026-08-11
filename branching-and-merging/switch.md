---
title: "git switch"
source: "https://git-scm.com/docs/git-switch"
section: "branching-and-merging"
status: "expanded"
---

# `git switch`

Este caso usa `git switch` para cambiar de rama o crear una rama antes de cambiar. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git switch consulta o cambia referencias, `HEAD`, worktrees y estados de integración. Recibe como entrada las ramas, commits o rutas que participan en la operación. La operación consiste en cambiar de rama o crear una rama antes de cambiar.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | las ramas, commits o rutas que participan en la operación. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | cambiar de rama o crear una rama antes de cambiar. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: cambiar de rama o crear una rama antes de cambiar. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git status`, `git branch -vv`, `git log --graph --oneline --decorate --all`. |

## Requisitos y laboratorio

Crea un commit base y dos ramas con un cambio distinto. Ejecuta la operación desde la rama indicada en el ejemplo.

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

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

Para comprobar el resultado: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git switch -c tema-portada
git switch main
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: las ramas, commits o rutas que participan en la operación.
- La operación observable es: cambiar de rama o crear una rama antes de cambiar.
- La comprobación se realiza mediante: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git switch [<options>] [--no-guess] <branch>
git switch [<options>] --detach [<start-point>]
git switch [<options>] (-c|-C) <new-branch> [<start-point>]
git switch [<options>] --orphan <new-branch>
```

### Uso verificado con `git version 2.51.1`

```text
git switch [<options>] [<branch>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git switch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | cambiar de rama o crear una rama antes de cambiar | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git switch a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git switch con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--no-guess` | Desactiva el comportamiento `guess` para esta invocación. |
| `--detach` | Hace que `HEAD` apunte directamente a un commit. |
| `-c` | Aplica una clave de configuración solo a esta invocación. |
| `-C` | Ejecuta Git como si se hubiera iniciado en el directorio indicado. |
| `--orphan` | Activa el modo `--orphan`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--create` | Permite crear o escribir el elemento seleccionado. |
| `--force-create` | Permite crear o escribir el elemento seleccionado. |
| `--guess` | Activa el modo `--guess`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--discard-changes` | Activa el modo `--discard-changes`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--recurse-submodules` | Propaga la operación a submódulos dentro del alcance. |
| `--progress` | Muestra progreso aunque la salida no sea un terminal. |
| `-m` | Activa el modo `-m`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--merge` | Activa el modo `--merge`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--conflict` | Activa el modo `--conflict`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-d` | Activa la forma corta de eliminación o una opción propia de la orden. |
| `-t` | Activa el modo `-t`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--track` | Crea o ajusta la asociación de seguimiento solicitada. |
| `-f` | Activa la forma corta de la operación forzada. |
| `--force` | Omite una protección concreta; úsala solo después de verificar el estado objetivo. |
| `--overwrite-ignore` | Excluye elementos que cumplan la condición indicada. |
| `--ignore-other-worktrees` | Excluye elementos que cumplan la condición indicada. |

## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| La referencia es ambigua | Un nombre coincide con más de un objeto o una ruta | Usa `--` para separar rutas y una revisión completa para el objeto. |
| El cambio de rama se rechaza | Hay modificaciones que serían sobrescritas | Confirma el estado y decide entre commit, stash o descarte. |
| La integración se detiene | Dos cambios afectan la misma región o ruta | Resuelve, añade los archivos y usa la orden `--continue` o `--abort` que corresponda. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: cambiar de rama o crear una rama antes de cambiar. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git tag`](../branching-and-merging/tag.md)
- [`git stash`](../branching-and-merging/stash.md)
- [`git worktree`](../branching-and-merging/worktree.md)

## Fuente

- [git-switch - Switch branches](https://git-scm.com/docs/git-switch)
