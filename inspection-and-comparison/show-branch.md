---
title: "git show-branch"
source: "https://git-scm.com/docs/git-show-branch"
section: "inspection-and-comparison"
status: "expanded"
---

# `git show-branch`

Este caso usa `git show-branch` para comparar el desarrollo representado por varias ramas. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git show-branch selecciona objetos o rangos y produce una vista sin cambiar el repositorio. Recibe como entrada los estados u objetos que la consulta debe mostrar o comparar. La operación consiste en comparar el desarrollo representado por varias ramas.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | los estados u objetos que la consulta debe mostrar o comparar. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | comparar el desarrollo representado por varias ramas. | Comprueba el resultado con una orden de lectura. |
| Persistencia | No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa el hash, el rango y el pathspec impresos junto al resultado. |

## Requisitos y laboratorio

Crea dos commits y una rama. Compara cada par de estados con una ruta explícita y después sin limitar la ruta.

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

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

Para comprobar el resultado: la salida cambia cuando se modifica una sola revisión, ruta u opción de formato. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git show-branch main tema-portada
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: los estados u objetos que la consulta debe mostrar o comparar.
- La operación observable es: comparar el desarrollo representado por varias ramas.
- La comprobación se realiza mediante: la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git show-branch [-a | --all] [-r | --remotes] [--topo-order | --date-order]
		[--current] [--color[=<when>] | --no-color] [--sparse]
		[--more=<n> | --list | --independent | --merge-base]
		[--no-name | --sha1-name] [--topics]
```

### Uso verificado con `git version 2.51.1`

```text
git show-branch [-a | --all] [-r | --remotes] [--topo-order | --date-order]
                       [--current] [--color[=<when>] | --no-color] [--sparse]
                       [--more=<n> | --list | --independent | --merge-base]
                       [--no-name | --sha1-name] [--topics]
                       [(<rev> | <glob>)...]
   or: git show-branch (-g | --reflog)[=<n>[,<base>]] [--list] [<ref>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git show-branch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | comparar el desarrollo representado por varias ramas | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git show-branch a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git show-branch con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-a` | Activa la forma corta de selección total o una opción propia de la orden. |
| `--all` | Amplía la selección a todos los elementos del alcance definido. |
| `-r` | Activa el modo `-r`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--remotes` | Activa el modo `--remotes`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--topo-order` | Activa el modo `--topo-order`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--date-order` | Aplica una fecha, duración o política de vencimiento. |
| `--current` | Activa el modo `--current`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--color` | Controla el uso de secuencias de color en la salida. |
| `--no-color` | Desactiva secuencias de color. |
| `--sparse` | Permite operar sobre entradas que quedan fuera de la selección sparse activa. |
| `--more` | Activa el modo `--more`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--list` | Incluye información adicional en la salida. |
| `--independent` | Activa el modo `--independent`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--merge-base` | Activa el modo `--merge-base`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-name` | Desactiva el comportamiento `name` para esta invocación. |
| `--sha1-name` | Activa el modo `--sha1-name`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--topics` | Activa el modo `--topics`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-g` | Activa el modo `-g`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reflog` | Activa el modo `--reflog`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--name` | Activa el modo `--name`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| La salida está vacía | El rango o el pathspec no contiene cambios | Resuelve cada revisión con `git rev-parse --verify`. |
| El orden no coincide con el esperado | La función usa un recorrido o criterio de orden | Declara el criterio con opciones de fecha, topología o formato. |
| Un script interpreta colores | La salida está destinada a terminal | Usa una forma de formato y desactiva color para datos de máquina. |

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

Ejecuta la consulta sobre dos revisiones conocidas. Cambia un solo argumento y explica qué conjunto de objetos o rutas cambió.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git verify-commit`](../inspection-and-comparison/verify-commit.md)
- [`git show`](../inspection-and-comparison/show.md)
- [`git verify-tag`](../inspection-and-comparison/verify-tag.md)

## Fuente

- [git-show-branch - Show branches and their commits](https://git-scm.com/docs/git-show-branch)
