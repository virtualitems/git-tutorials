---
title: "git clone"
source: "https://git-scm.com/docs/git-clone"
section: "getting-and-creating-projects"
status: "option-expanded"
---

# `git clone`

Este caso usa `git clone` para crear un repositorio local a partir de otro repositorio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git clone crea la base de datos local de objetos y prepara el área de trabajo. Recibe como entrada un directorio, una URL o una selección de rutas. La operación consiste en crear un repositorio local a partir de otro repositorio.

Puede persistir el estado implicado por esta operación: crear un repositorio local a partir de otro repositorio. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Un repositorio contiene objetos y referencias. Un área de trabajo materializa un commit para que los archivos puedan editarse.

Separa los datos del repositorio de los archivos materializados. Un repositorio bare conserva objetos y referencias sin área de trabajo.

## Ejemplo mínimo

```bash
git clone https://example.com/equipo/biblioteca.git
cd biblioteca
git status
```

La invocación `git clone https://example.com/equipo/biblioteca.git` ejecuta esta operación: crear un repositorio local a partir de otro repositorio. Después, el directorio resultante contiene el repositorio y, cuando corresponde, un área de trabajo. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

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

## Flujos de uso

### Caso base

crear un repositorio local a partir de otro repositorio. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git clone a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git clone con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--template`

Usa el directorio indicado como fuente de plantillas para crear archivos iniciales dentro del nuevo repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `directory from which templates will be used`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git clone`, template modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --template=../plantillas https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `../plantillas` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-l` y `--local`

Opera sobre la configuración del repositorio.  La misma línea de ayuda también acepta `-l`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git clone`, alcance local modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-l`

```bash
git clone -l https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--local`

```bash
git clone --local https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-s` y `--shared`

Ajusta permisos y configuración para que varios usuarios del sistema operativo puedan escribir el repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `setup as shared repository`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-s`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git clone`, shared modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-s`

```bash
git clone -s https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--shared`

```bash
git clone --shared https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-hardlinks`

Desactiva el comportamiento `hardlinks` para esta invocación.

En `git clone`, desactivar hardlinks modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-hardlinks https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git clone -q https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--quiet`

```bash
git clone --quiet https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-n`

Crea n como parte de crear un repositorio local a partir de otro repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `don't create a checkout`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `--no-checkout`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git clone -n https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--bare`

Opera sin un área de trabajo asociada.

En `git clone`, repositorio bare modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --bare https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mirror`

Crea espejo como parte de crear un repositorio local a partir de otro repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `create a mirror repository (implies --bare)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git clone`, espejo modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --mirror https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-o` y `--origin`

Define origin para esta ejecución de `git clone`. En Git 2.51.1, la ayuda corta expresa el contrato como `use <name> instead of 'origin' to track upstream`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-o`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git clone`, origin modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-o`

```bash
git clone -o tema https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `tema` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--origin`

```bash
git clone --origin=tema https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `tema` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-b` y `--branch`

Selecciona o modifica referencias dentro del alcance de la orden.  La misma línea de ayuda también acepta `-b`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-b`

```bash
git clone -b main https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `main` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--branch`

```bash
git clone --branch=main https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `main` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-u` y `--upload-pack`

Define upload pack con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `path to git-upload-pack on the remote`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-u`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git clone`, upload pack modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-u`

```bash
git clone -u archivo.txt https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `archivo.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--upload-pack`

```bash
git clone --upload-pack=archivo.txt https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `archivo.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--reference`

Activa reference durante crear un repositorio local a partir de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `reference repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git clone`, reference modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --reference=valor https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dissociate`

Limita crear un repositorio local a partir de otro repositorio al alcance identificado por dissociate. En Git 2.51.1, la ayuda corta expresa el contrato como `use --reference only while cloning`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git clone`, dissociate modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --dissociate https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--separate-git-dir`

Guarda los datos del repositorio en otra ruta y deja en el área de trabajo un archivo que apunta a esa ubicación. En Git 2.51.1, la ayuda corta expresa el contrato como `separate git dir from working tree`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git clone`, separate git dir modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --separate-git-dir=../datos-git https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `../datos-git` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-v`

```bash
git clone -v https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--verbose`

```bash
git clone --verbose https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

La opción controla progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque crear un repositorio local a partir de otro repositorio puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git clone --progress https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reject-shallow`

Impide rechazos historial shallow durante esta invocación de `git clone`.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --reject-shallow https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-checkout`

Desactiva el comportamiento `checkout` para esta invocación.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git clone --no-checkout https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--checkout`

Selecciona la relación indicada por checkout; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-checkout`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git clone --checkout https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--hardlinks`

Selecciona la relación indicada por hardlinks; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-hardlinks`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git clone`, hardlinks modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --hardlinks https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

En `git clone`, recorrer submódulos modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --recurse-submodules=archivo.txt https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recursive`

Extiende la operación de forma recursiva al ámbito documentado.

En `git clone`, recursión modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --recursive=archivo.txt https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-j` y `--jobs`

Define cuántas tareas puede ejecutar Git en paralelo para la operación. En Git 2.51.1, la ayuda corta expresa el contrato como `number of submodules cloned in parallel`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-j`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-j`

```bash
git clone -j 5 https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--jobs`

```bash
git clone --jobs=5 https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--reference-if-able`

Activa reference if able durante crear un repositorio local a partir de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `reference repository`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git clone`, reference if able modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --reference-if-able=valor https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--revision`

Comprueba revision antes de aceptar el resultado de `git clone`.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git clone --revision=valor https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--depth`

Establece un límite numérico para la selección o el recorrido.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --depth=2 https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `2` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow-since`

Crea historial shallow desde una fecha como parte de crear un repositorio local a partir de otro repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `create a shallow clone since a specific time`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --shallow-since=2026-01-15T10:00:00Z https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `2026-01-15T10:00:00Z` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow-exclude`

Excluye elementos que cumplan la condición indicada.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --shallow-exclude=refs/heads/main https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `refs/heads/main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--single-branch`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --single-branch https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tags`

Incluye o selecciona etiquetas según la operación.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --tags https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--shallow-submodules`

Activa historial shallow submódulos durante crear un repositorio local a partir de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `any cloned submodules will be shallow`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --shallow-submodules https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ref-format`

Selecciona el formato de almacenamiento de referencias que usará el repositorio. En Git 2.51.1, la ayuda corta expresa el contrato como `specify the reference format to use`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git clone --ref-format=reftable https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `reftable` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-c` y `--config`

Define config para esta ejecución de `git clone`. En Git 2.51.1, la ayuda corta expresa el contrato como `set config inside the new repository`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-c`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git clone`, config modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-c`

```bash
git clone -c user.name https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--config`

```bash
git clone --config=user.name https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

En esta forma, `user.name` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--server-option`

Activa server option durante crear un repositorio local a partir de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `option to transmit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git clone`, server option modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --server-option=valor https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-4` y `--ipv4`

Limita crear un repositorio local a partir de otro repositorio al alcance identificado por ipv4. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv4 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-4`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git clone`, ipv4 modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-4`

```bash
git clone -4 https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--ipv4`

```bash
git clone --ipv4 https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-6` y `--ipv6`

Limita crear un repositorio local a partir de otro repositorio al alcance identificado por ipv6. En Git 2.51.1, la ayuda corta expresa el contrato como `use IPv6 addresses only`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-6`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git clone`, ipv6 modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-6`

```bash
git clone -6 https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--ipv6`

```bash
git clone --ipv6 https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--filter`

Limita los objetos transferidos mediante una especificación de filtro de clon parcial. En Git 2.51.1, la ayuda corta expresa el contrato como `object filtering`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --filter=valor https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--also-filter-submodules`

Activa also filtro submódulos durante crear un repositorio local a partir de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `apply partial clone filters to submodules`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --also-filter-submodules https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--remote-submodules`

Define remote submódulos para esta ejecución de `git clone`. En Git 2.51.1, la ayuda corta expresa el contrato como `any cloned submodules will use their remote-tracking branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --remote-submodules https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sparse`

Permite operar sobre entradas que quedan fuera de la selección sparse activa.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --sparse https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--bundle-uri`

Activa bundle uri durante crear un repositorio local a partir de otro repositorio. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `a URI for downloading bundles before fetching from origin remote`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git clone`, bundle uri modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --bundle-uri=valor https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-template`

Desactiva para esta invocación el comportamiento que habilita `--template`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar template modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-template https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-bare`

Desactiva para esta invocación el comportamiento que habilita `--bare`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar repositorio bare modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-bare https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-mirror`

Desactiva para esta invocación el comportamiento que habilita `--mirror`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar espejo modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-mirror https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reference`

Desactiva para esta invocación el comportamiento que habilita `--reference`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar reference modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-reference https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-dissociate`

Desactiva para esta invocación el comportamiento que habilita `--dissociate`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar dissociate modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-dissociate https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-separate-git-dir`

Desactiva para esta invocación el comportamiento que habilita `--separate-git-dir`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar separate git dir modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-separate-git-dir https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git clone --no-verbose https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git clone --no-quiet https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque crear un repositorio local a partir de otro repositorio puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git clone --no-progress https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reject-shallow`

Desactiva para esta invocación el comportamiento que habilita `--reject-shallow`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --no-reject-shallow https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-local`

Desactiva para esta invocación el comportamiento que habilita `--local`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar alcance local modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-local https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-shared`

Desactiva para esta invocación el comportamiento que habilita `--shared`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar shared modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-shared https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar recorrer submódulos modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-recurse-submodules https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recursive`

Desactiva para esta invocación el comportamiento que habilita `--recursive`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar recursión modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-recursive https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-jobs`

Desactiva para esta invocación el comportamiento que habilita `--jobs`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --no-jobs https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reference-if-able`

Desactiva para esta invocación el comportamiento que habilita `--reference-if-able`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar reference if able modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-reference-if-able https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-origin`

Desactiva para esta invocación el comportamiento que habilita `--origin`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar origin modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-origin https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-branch`

Desactiva para esta invocación el comportamiento que habilita `--branch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --no-branch https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-revision`

Desactiva para esta invocación el comportamiento que habilita `--revision`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git clone --no-revision https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-upload-pack`

Desactiva para esta invocación el comportamiento que habilita `--upload-pack`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar upload pack modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-upload-pack https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-depth`

Desactiva para esta invocación el comportamiento que habilita `--depth`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --no-depth https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-shallow-since`

Desactiva para esta invocación el comportamiento que habilita `--shallow-since`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --no-shallow-since https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-shallow-exclude`

Desactiva para esta invocación el comportamiento que habilita `--shallow-exclude`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --no-shallow-exclude https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-single-branch`

Desactiva para esta invocación el comportamiento que habilita `--single-branch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --no-single-branch https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tags`

Desactiva para esta invocación el comportamiento que habilita `--tags`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --no-tags https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-shallow-submodules`

Desactiva para esta invocación el comportamiento que habilita `--shallow-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --no-shallow-submodules https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ref-format`

Desactiva para esta invocación el comportamiento que habilita `--ref-format`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git clone --no-ref-format https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-config`

Desactiva para esta invocación el comportamiento que habilita `--config`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar config modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-config https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-server-option`

Desactiva para esta invocación el comportamiento que habilita `--server-option`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar server option modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-server-option https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-filter`

Desactiva para esta invocación el comportamiento que habilita `--filter`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --no-filter https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-also-filter-submodules`

Desactiva para esta invocación el comportamiento que habilita `--also-filter-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --no-also-filter-submodules https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-remote-submodules`

Desactiva para esta invocación el comportamiento que habilita `--remote-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --no-remote-submodules https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-sparse`

Desactiva para esta invocación el comportamiento que habilita `--sparse`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta crear un repositorio local a partir de otro repositorio. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git clone --no-sparse https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-bundle-uri`

Desactiva para esta invocación el comportamiento que habilita `--bundle-uri`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git clone`, desactivar bundle uri modifica la forma en que se ejecuta crear un repositorio local a partir de otro repositorio. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git clone --no-bundle-uri https://example.com/equipo/biblioteca.git
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git clone` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El destino ya contiene archivos

Comprueba esta causa: La creación o clonación requiere una ruta compatible. Elige un directorio vacío o inicializa la ruta de forma explícita.

### No se recibe una referencia

Comprueba esta causa: El remoto no la anuncia o el filtro la excluye. Ejecuta `git ls-remote <url>` y revisa los filtros.

### Falla la autenticación

Comprueba esta causa: La URL o el helper de credenciales no entrega acceso. Comprueba la URL sin registrar credenciales en el historial del shell.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: crear un repositorio local a partir de otro repositorio. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa un directorio temporal. Compara el contenido antes y después, incluidos `.git`, HEAD y las ramas disponibles.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git sparse-checkout`](../getting-and-creating-projects/sparse-checkout.md)
- [`git init`](../getting-and-creating-projects/init.md)

## Fuente

- [git-clone - Clone a repository into a new directory](https://git-scm.com/docs/git-clone)
