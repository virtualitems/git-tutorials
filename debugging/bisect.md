---
title: "git bisect"
source: "https://git-scm.com/docs/git-bisect"
section: "debugging"
status: "expanded"
---

# `git bisect`

Este caso usa `git bisect` para localizar por búsqueda binaria el commit que introdujo un cambio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git bisect localiza texto, autores, líneas o el commit que introdujo un comportamiento. Recibe como entrada un patrón, una ruta y el rango de historial que limita la búsqueda. La operación consiste en localizar por búsqueda binaria el commit que introdujo un cambio.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | un patrón, una ruta y el rango de historial que limita la búsqueda. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | localizar por búsqueda binaria el commit que introdujo un cambio. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Escribe el estado de la sesión de bisección y cambia el commit materializado hasta ejecutar reset. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa la salida, el código de terminación y una revisión manual del commit hallado. |

## Requisitos y laboratorio

Crea tres commits que cambien la misma línea. Usa un patrón que exista y otro que no exista para observar los códigos de salida.

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

La búsqueda combina revisiones, rutas y contenido. Primero delimita el conjunto de commits o archivos; después interpreta la evidencia que devuelve Git.

Reduce primero el rango y las rutas. Después interpreta cada coincidencia dentro de ese conjunto, sin atribuir significado a elementos que quedaron fuera.

Para comprobar el resultado: la salida identifica líneas, archivos o commits que cumplen el criterio. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git bisect start
git bisect bad
git bisect good v1.0
git bisect run ./prueba.sh
git bisect reset
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: un patrón, una ruta y el rango de historial que limita la búsqueda.
- La operación observable es: localizar por búsqueda binaria el commit que introdujo un cambio.
- La comprobación se realiza mediante: la salida identifica líneas, archivos o commits que cumplen el criterio.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git bisect start [--term-(bad|new)=<term-new> --term-(good|old)=<term-old>]
		 [--no-checkout] [--first-parent] [<bad> [<good>…]] [--] [<pathspec>…]
git bisect (bad|new|<term-new>) [<rev>]
git bisect (good|old|<term-old>) [<rev>…]
```

### Uso verificado con `git version 2.51.1`

```text
git bisect start [--term-(new|bad)=<term> --term-(old|good)=<term>]    [--no-checkout] [--first-parent] [<bad> [<good>...]] [--]    [<pathspec>...]
   or: git bisect (good|bad) [<rev>...]
   or: git bisect terms [--term-good | --term-bad]
   or: git bisect skip [(<rev>|<range>)...]
   or: git bisect next
   or: git bisect reset [<commit>]
   or: git bisect visualize
   or: git bisect replay <logfile>
   or: git bisect log
   or: git bisect run <cmd> [<arg>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git bisect -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | localizar por búsqueda binaria el commit que introdujo un cambio | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git bisect a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git bisect con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--term-` | Activa el modo `--term-`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-checkout` | Desactiva el comportamiento `checkout` para esta invocación. |
| `--first-parent` | Activa el modo `--first-parent`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--term-good` | Activa el modo `--term-good`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--term-bad` | Activa el modo `--term-bad`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

El comando de prueba usado por `git bisect run` debe devolver 0 para bueno, 1–127 salvo 125 para malo y 125 para omitir.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| No hay coincidencias | El patrón, la revisión o la ruta no abarca el dato | Prueba el patrón sobre `HEAD` y separa la ruta con `--`. |
| La atribución parece incorrecta | El archivo se movió o el bloque se reformateó | Activa detección de movimiento o copia y compara el commit. |
| La búsqueda binaria no avanza | La prueba no clasifica el commit | Marca el commit como `skip` o corrige el comando de prueba. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Escribe el estado de la sesión de bisección y cambia el commit materializado hasta ejecutar reset. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Prepara un historial corto con un cambio por commit. Delimita una ruta o un rango para comprobar qué evidencia incluye y cuál excluye el comando.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git blame`](../debugging/blame.md)
- [`git annotate`](../debugging/annotate.md)
- [`git grep`](../debugging/grep.md)

## Fuente

- [git-bisect - Use binary search to find the commit that introduced a bug](https://git-scm.com/docs/git-bisect)
