---
title: "git init"
source: "https://git-scm.com/docs/git-init"
section: "getting-and-creating-projects"
status: "option-expanded"
---

# `git init`

Este caso usa `git init` para crear un repositorio vacío o reinicializar uno existente. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git init crea la base de datos local de objetos y prepara el área de trabajo. Recibe como entrada un directorio, una URL o una selección de rutas. La operación consiste en crear un repositorio vacío o reinicializar uno existente.

Puede persistir el estado implicado por esta operación: crear un repositorio vacío o reinicializar uno existente. Las opciones pueden limitar o ampliar ese efecto.

## Laboratorio base

Crea este repositorio una vez. Las demás guías enlazan este apartado y continúan desde el commit `base`.

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

`mktemp -d` crea una ruta que puedes eliminar cuando termines. `git init` crea el directorio Git. Las dos órdenes `git config` guardan nombre y correo solo dentro de este repositorio. `git add` copia `archivo.txt` al índice y `git commit` registra el estado que usarán los ejemplos posteriores. Comprueba el punto de partida con `git status --short`; una salida vacía indica que el área de trabajo y el índice coinciden con `HEAD`.

## Cómo funciona

Un repositorio contiene objetos y referencias. Un área de trabajo materializa un commit para que los archivos puedan editarse.

Separa los datos del repositorio de los archivos materializados. Un repositorio bare conserva objetos y referencias sin área de trabajo.

## Ejemplo mínimo

```bash
mkdir biblioteca
cd biblioteca
git init -b main
git status
```

La invocación `git init -b main` ejecuta esta operación: crear un repositorio vacío o reinicializar uno existente. Después, el directorio resultante contiene el repositorio y, cuando corresponde, un área de trabajo. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git init [-q | --quiet] [--bare] [--template=<template-directory>]
	 [--separate-git-dir <git-dir>] [--object-format=<format>]
	 [--ref-format=<format>]
	 [-b <branch-name> | --initial-branch=<branch-name>]
```

### Uso verificado con `git version 2.51.1`

```text
git init [-q | --quiet] [--bare] [--template=<template-directory>]
                [--separate-git-dir <git-dir>] [--object-format=<format>]
                [--ref-format=<format>]
                [-b <branch-name> | --initial-branch=<branch-name>]
                [--shared[=<permissions>]] [<directory>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git init -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

crear un repositorio vacío o reinicializar uno existente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git init a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git init con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git init -q "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git init` o a otra opción. La salida identifica el directorio que almacena el repositorio recién creado.

#### Ejemplo con `--quiet`

```bash
git init --quiet "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git init` o a otra opción. La salida identifica el directorio que almacena el repositorio recién creado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--bare`

Opera sin un área de trabajo asociada.

En `git init`, repositorio bare modifica la forma en que se ejecuta crear un repositorio vacío o reinicializar uno existente. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git init --bare "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git init` o a otra opción. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--template`

Usa el directorio indicado como fuente de plantillas para crear archivos iniciales dentro del nuevo repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `directory from which templates will be used`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git init`, template modifica la forma en que se ejecuta crear un repositorio vacío o reinicializar uno existente. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
mkdir -p "$lab_dir/plantillas"
printf 'plantilla del laboratorio\n' > "$lab_dir/plantillas/description"
git init --template="$lab_dir/plantillas" "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

El ejemplo usa `../plantillas` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--separate-git-dir`

Guarda los datos del repositorio en otra ruta y deja en el área de trabajo un archivo que apunta a esa ubicación. En Git 2.51.1, la ayuda corta expresa el contrato como `separate git dir from working tree`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git init`, separate git dir modifica la forma en que se ejecuta crear un repositorio vacío o reinicializar uno existente. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git init --separate-git-dir="$lab_dir/datos-git" "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

El ejemplo usa `../datos-git` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--object-format`

Selecciona el algoritmo de hash con el que el repositorio identifica objetos nuevos. En Git 2.51.1, la ayuda corta expresa el contrato como `specify the hash algorithm to use`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git init --object-format=sha256 "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

El ejemplo usa `sha256` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ref-format`

Selecciona el formato de almacenamiento de referencias que usará el repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `specify the reference format to use`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git init --ref-format=reftable "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

El ejemplo usa `reftable` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-b` y `--initial-branch`

Selecciona o modifica referencias dentro del alcance de la orden.  La misma línea de ayuda también acepta `-b`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio vacío o reinicializar uno existente. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-b`

```bash
git init -b main "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

En esta forma, `main` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida identifica el directorio que almacena el repositorio recién creado.

#### Ejemplo con `--initial-branch`

```bash
git init --initial-branch=main "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

En esta forma, `main` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida identifica el directorio que almacena el repositorio recién creado.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--shared`

Ajusta permisos y configuración para que varios usuarios del sistema operativo puedan escribir el repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `specify that the git repository is to be shared amongst several users`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git init`, shared modifica la forma en que se ejecuta crear un repositorio vacío o reinicializar uno existente. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git init --shared=group "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

El ejemplo usa `group` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git init --no-quiet "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git init` o a otra opción. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-bare`

Desactiva para esta invocación el comportamiento que habilita `--bare`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git init`, desactivar repositorio bare modifica la forma en que se ejecuta crear un repositorio vacío o reinicializar uno existente. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git init --no-bare "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git init` o a otra opción. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-template`

Desactiva para esta invocación el comportamiento que habilita `--template`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git init`, desactivar template modifica la forma en que se ejecuta crear un repositorio vacío o reinicializar uno existente. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git init --no-template "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git init` o a otra opción. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-separate-git-dir`

Desactiva para esta invocación el comportamiento que habilita `--separate-git-dir`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git init`, desactivar separate git dir modifica la forma en que se ejecuta crear un repositorio vacío o reinicializar uno existente. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git init --no-separate-git-dir "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git init` o a otra opción. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-object-format`

Desactiva para esta invocación el comportamiento que habilita `--object-format`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git init --no-object-format "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git init` o a otra opción. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ref-format`

Desactiva para esta invocación el comportamiento que habilita `--ref-format`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git init --no-ref-format "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git init` o a otra opción. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-initial-branch`

Desactiva para esta invocación el comportamiento que habilita `--initial-branch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio vacío o reinicializar uno existente. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git init --no-initial-branch "$lab_dir/init-opcion"
git -C "$lab_dir/init-opcion" rev-parse --git-dir
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git init` o a otra opción. La salida identifica el directorio que almacena el repositorio recién creado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El destino ya contiene archivos

Comprueba esta causa: La creación o clonación requiere una ruta compatible. Elige un directorio vacío o inicializa la ruta de forma explícita.

### No se recibe una referencia

Comprueba esta causa: El remoto no la anuncia o el filtro la excluye. Ejecuta `git ls-remote <url>` y revisa los filtros.

### Falla la autenticación

Comprueba esta causa: La URL o el helper de credenciales no entrega acceso. Comprueba la URL sin registrar credenciales en el historial del shell.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: crear un repositorio vacío o reinicializar uno existente. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa un directorio temporal. Compara el contenido antes y después, incluidos `.git`, HEAD y las ramas disponibles.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git clone`](../getting-and-creating-projects/clone.md)
- [`git sparse-checkout`](../getting-and-creating-projects/sparse-checkout.md)

## Fuente

- [git-init - Create an empty Git repository or reinitialize an existing one](https://git-scm.com/docs/git-init)
