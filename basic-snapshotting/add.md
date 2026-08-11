---
title: "git add"
source: "https://git-scm.com/docs/git-add"
section: "basic-snapshotting"
status: "expanded"
---

# `git add`

Este caso usa `git add` para copiar cambios del área de trabajo al índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git add mueve contenido entre el área de trabajo, el índice y el commit señalado por `HEAD`. Recibe como entrada las rutas y el estado de origen seleccionados por los argumentos. La operación consiste en copiar cambios del área de trabajo al índice.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | las rutas y el estado de origen seleccionados por los argumentos. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | copiar cambios del área de trabajo al índice. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: copiar cambios del área de trabajo al índice. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git status --short`, `git diff` y `git diff --cached`. |

## Requisitos y laboratorio

Crea un repositorio con un commit base. Observa `HEAD`, el índice y el archivo antes y después de cada orden.

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

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

Para comprobar el resultado: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
printf 'capítulo 1\n' > guia.txt
git add guia.txt
git status --short
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: las rutas y el estado de origen seleccionados por los argumentos.
- La operación observable es: copiar cambios del área de trabajo al índice.
- La comprobación se realiza mediante: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git add [--verbose | -v] [--dry-run | -n] [--force | -f] [--interactive | -i] [--patch | -p]
	[--edit | -e] [--[no-]all | -A | --[no-]ignore-removal | [--update | -u]] [--sparse]
	[--intent-to-add | -N] [--refresh] [--ignore-errors] [--ignore-missing] [--renormalize]
	[--chmod=(+|-)x] [--pathspec-from-file=<file> [--pathspec-file-nul]]
```

### Uso verificado con `git version 2.51.1`

```text
git add [<options>] [--] <pathspec>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git add -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | copiar cambios del área de trabajo al índice | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git add a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Simulación | Calcular el efecto sin escribir el estado principal. | Compara la simulación con la selección prevista. |
| Validación | Comprobar el resultado de git add con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--verbose` | Aumenta el detalle enviado a la salida. |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `--dry-run` | Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `--force` | Omite una protección concreta; úsala solo después de verificar el estado objetivo. |
| `-f` | Activa la forma corta de la operación forzada. |
| `--interactive` | Abre una selección interactiva antes de aplicar la operación. |
| `-i` | Activa la forma corta del modo interactivo o una opción propia de la orden. |
| `--patch` | Permite elegir hunks en vez de operar sobre el archivo completo. |
| `-p` | Activa la forma corta del modo patch o de una opción propia de la orden. |
| `--edit` | Abre la representación editable que define la orden antes de aplicarla. |
| `-e` | Activa el modo `-e`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--all` | Amplía la selección a todos los elementos del alcance definido. |
| `-A` | Activa el modo `-A`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ignore-removal` | Excluye elementos que cumplan la condición indicada. |
| `--update` | Limita la actualización a elementos que ya existen en el estado de destino. |
| `-u` | Activa el modo `-u`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--sparse` | Permite operar sobre entradas que quedan fuera de la selección sparse activa. |
| `--intent-to-add` | Registra una entrada sin preparar todavía su contenido. |
| `-N` | Activa el modo `-N`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--refresh` | Actualiza metadatos de comprobación sin copiar contenido nuevo al índice. |
| `--ignore-errors` | Continúa con otras entradas después de un error y conserva un código de fallo. |
| `--ignore-missing` | Permite comprobar rutas ausentes bajo las condiciones que define la orden. |
| `--renormalize` | Vuelve a aplicar reglas de normalización al contenido seleccionado. |
| `--chmod` | Cambia el bit ejecutable registrado en el índice, no el permiso del archivo en disco. |
| `--pathspec-from-file` | Lee pathspecs desde un archivo o desde stdin. |
| `--pathspec-file-nul` | Interpreta los pathspecs de archivo como registros terminados en NUL. |
| `-U` | Activa el modo `-U`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--unified` | Define cuántas líneas de contexto rodean cada hunk. |
| `--inter-hunk-context` | Fusiona hunks cercanos cuando la distancia no supera el límite indicado. |
| `--no-all` | Desactiva el comportamiento `all` para esta invocación. |

## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El cambio no entra al commit | El índice no contiene la versión esperada | Compara `git diff` con `git diff --cached`. |
| Un pathspec no coincide | La ruta se evalúa desde otro directorio o está ignorada | Usa `git status --short --untracked-files=all` y separa opciones con `--`. |
| Se reemplaza contenido local | La orden escribe el área de trabajo | Guarda el diff o crea un stash antes de repetir la operación. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: copiar cambios del área de trabajo al índice. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git commit`](../basic-snapshotting/commit.md)
- [`git mv`](../basic-snapshotting/mv.md)

## Fuente

- [git-add - Add file contents to the index](https://git-scm.com/docs/git-add)
