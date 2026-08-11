---
title: "git clone"
source: "https://git-scm.com/docs/git-clone"
section: "getting-and-creating-projects"
status: "expanded"
---

# `git clone`

Este caso usa `git clone` para crear un repositorio local a partir de otro repositorio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git clone crea la base de datos local de objetos y prepara el área de trabajo. Recibe como entrada un directorio, una URL o una selección de rutas. La operación consiste en crear un repositorio local a partir de otro repositorio.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | un directorio, una URL o una selección de rutas. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | crear un repositorio local a partir de otro repositorio. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: crear un repositorio local a partir de otro repositorio. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git status`, `git remote -v` y `git rev-parse --show-toplevel`. |

## Requisitos y laboratorio

Usa dos directorios bajo una ruta creada con `mktemp -d`: uno como origen y otro como destino.

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

Un repositorio contiene objetos y referencias. Un área de trabajo materializa un commit para que los archivos puedan editarse.

Separa los datos del repositorio de los archivos materializados. Un repositorio bare conserva objetos y referencias sin área de trabajo.

Para comprobar el resultado: el directorio resultante contiene el repositorio y, cuando corresponde, un área de trabajo. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git clone https://example.test/equipo/biblioteca.git
cd biblioteca
git status
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: un directorio, una URL o una selección de rutas.
- La operación observable es: crear un repositorio local a partir de otro repositorio.
- La comprobación se realiza mediante: el directorio resultante contiene el repositorio y, cuando corresponde, un área de trabajo.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git clone [--template=<template-directory>]
	  [-l] [-s] [--no-hardlinks] [-q] [-n] [--bare] [--mirror]
	  [-o <name>] [-b <name>] [-u <upload-pack>] [--reference <repository>]
	  [--dissociate] [--separate-git-dir <git-dir>]
```

### Uso verificado con `git version 2.51.1`

```text
git clone [<options>] [--] <repo> [<dir>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git clone -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | crear un repositorio local a partir de otro repositorio | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git clone a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git clone con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--template` | Controla campos, orden o representación del resultado. |
| `-l` | Activa el modo `-l`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-s` | Activa el modo `-s`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-hardlinks` | Desactiva el comportamiento `hardlinks` para esta invocación. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `--bare` | Opera sin un área de trabajo asociada. |
| `--mirror` | Activa el modo `--mirror`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-o` | Activa la forma corta de salida o una opción propia de la orden. |
| `-b` | Activa el modo `-b`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-u` | Activa el modo `-u`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reference` | Activa el modo `--reference`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--dissociate` | Activa el modo `--dissociate`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--separate-git-dir` | Activa el modo `--separate-git-dir`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `--verbose` | Aumenta el detalle enviado a la salida. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--progress` | Muestra progreso aunque la salida no sea un terminal. |
| `--reject-shallow` | Activa el modo `--reject-shallow`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--no-checkout` | Desactiva el comportamiento `checkout` para esta invocación. |
| `--checkout` | Activa el modo `--checkout`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--local` | Opera sobre la configuración del repositorio. |
| `--hardlinks` | Activa el modo `--hardlinks`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--shared` | Activa el modo `--shared`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--recurse-submodules` | Propaga la operación a submódulos dentro del alcance. |
| `--recursive` | Extiende la operación de forma recursiva al ámbito documentado. |
| `-j` | Activa el modo `-j`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--jobs` | Activa el modo `--jobs`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--reference-if-able` | Activa el modo `--reference-if-able`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--origin` | Activa el modo `--origin`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--branch` | Selecciona o modifica referencias dentro del alcance de la orden. |
| `--revision` | Activa el modo `--revision`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--upload-pack` | Activa el modo `--upload-pack`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--depth` | Establece un límite numérico para la selección o el recorrido. |
| `--shallow-since` | Activa el modo `--shallow-since`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--shallow-exclude` | Excluye elementos que cumplan la condición indicada. |
| `--single-branch` | Selecciona o modifica referencias dentro del alcance de la orden. |
| `--tags` | Incluye o selecciona etiquetas según la operación. |
| `--shallow-submodules` | Activa el modo `--shallow-submodules`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ref-format` | Controla campos, orden o representación del resultado. |
| `-c` | Aplica una clave de configuración solo a esta invocación. |
| `--config` | Activa el modo `--config`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--server-option` | Activa el modo `--server-option`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-4` | Activa el modo `-4`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ipv4` | Activa el modo `--ipv4`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-6` | Activa el modo `-6`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ipv6` | Activa el modo `--ipv6`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--filter` | Activa el modo `--filter`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--also-filter-submodules` | Activa el modo `--also-filter-submodules`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--remote-submodules` | Activa el modo `--remote-submodules`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--sparse` | Permite operar sobre entradas que quedan fuera de la selección sparse activa. |
| `--bundle-uri` | Activa el modo `--bundle-uri`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El destino ya contiene archivos | La creación o clonación requiere una ruta compatible | Elige un directorio vacío o inicializa la ruta de forma explícita. |
| No se recibe una referencia | El remoto no la anuncia o el filtro la excluye | Ejecuta `git ls-remote <url>` y revisa los filtros. |
| Falla la autenticación | La URL o el helper de credenciales no entrega acceso | Comprueba la URL sin registrar credenciales en el historial del shell. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: crear un repositorio local a partir de otro repositorio. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Usa un directorio temporal. Compara el contenido antes y después, incluidos `.git`, HEAD y las ramas disponibles.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git sparse-checkout`](../getting-and-creating-projects/sparse-checkout.md)
- [`git init`](../getting-and-creating-projects/init.md)

## Fuente

- [git-clone - Clone a repository into a new directory](https://git-scm.com/docs/git-clone)
