---
title: "git merge-tree"
source: "https://git-scm.com/docs/git-merge-tree"
section: "branching-and-merging"
status: "expanded"
---

# `git merge-tree`

Este caso usa `git merge-tree` para calcular una fusión y exponer su resultado sin cambiar el índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git merge-tree consulta o cambia referencias, `HEAD`, worktrees y estados de integración. Recibe como entrada las ramas, commits o rutas que participan en la operación. La operación consiste en calcular una fusión y exponer su resultado sin cambiar el índice.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | las ramas, commits o rutas que participan en la operación. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | calcular una fusión y exponer su resultado sin cambiar el índice. | Comprueba el resultado con una orden de lectura. |
| Persistencia | No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. | Compara el estado antes y después. |
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
git merge-tree --write-tree main tema-portada
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: las ramas, commits o rutas que participan en la operación.
- La operación observable es: calcular una fusión y exponer su resultado sin cambiar el índice.
- La comprobación se realiza mediante: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git merge-tree [--write-tree] [<options>] <branch1> <branch2>
git merge-tree [--trivial-merge] <base-tree> <branch1> <branch2> (deprecated)
```

### Uso verificado con `git version 2.51.1`

```text
git merge-tree [--write-tree] [<options>] <branch1> <branch2>
   or: git merge-tree [--trivial-merge] <base-tree> <branch1> <branch2>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git merge-tree -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | calcular una fusión y exponer su resultado sin cambiar el índice | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git merge-tree a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Salida para scripts | Producir registros con campos y separadores definidos. | Prueba nombres con espacios y saltos de línea. |
| Validación | Comprobar el resultado de git merge-tree con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--write-tree` | Permite crear o escribir el elemento seleccionado. |
| `--trivial-merge` | Activa el modo `--trivial-merge`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--messages` | Activa el modo `--messages`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `-z` | Termina registros con NUL para evitar división por espacios o saltos de línea. |
| `--name-only` | Muestra nombres de ruta sin el contenido del diff. |
| `--allow-unrelated-histories` | Activa el modo `--allow-unrelated-histories`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--stdin` | Lee registros o nombres desde la entrada estándar. |
| `--merge-base` | Activa el modo `--merge-base`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-X` | Activa el modo `-X`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--strategy-option` | Selecciona el algoritmo o estrategia que procesa la entrada. |

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

Persistencia: No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git refs`](../branching-and-merging/refs.md)
- [`git mergetool`](../branching-and-merging/mergetool.md)
- [`git rerere`](../branching-and-merging/rerere.md)

## Fuente

- [git-merge-tree - Perform merge without touching index or working tree](https://git-scm.com/docs/git-merge-tree)
