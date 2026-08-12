---
title: "git fast-export"
source: "https://git-scm.com/docs/git-fast-export"
section: "external-systems"
status: "option-expanded"
---

# `git fast-export`

Este caso usa `git fast-export` para emitir historial y referencias en un flujo para migración. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git fast-export traduce historial, referencias e identidades entre Git y otro sistema. Recibe como entrada la ubicación y los nombres que deben traducirse desde el sistema de origen. La operación consiste en emitir historial y referencias en un flujo para migración.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Ejemplo mínimo

```bash
git fast-export --all > historial.fi
```

La invocación `git fast-export --all > historial.fi` ejecuta esta operación: emitir historial y referencias en un flujo para migración. Después, el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git fast-export [<options>] | git fast-import
```

### Uso verificado con `git version 2.51.1`

```text
git fast-export [<rev-list-opts>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git fast-export -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

emitir historial y referencias en un flujo para migración. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git fast-export a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git fast-export con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fast-export --progress=5 --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signed-tags`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta emitir historial y referencias en un flujo para migración. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fast-export --signed-tags=all --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signed-commits`

Define firmado commits para esta ejecución de `git fast-export`. En Git 2.51.1, la ayuda corta expresa el contrato como `select handling of signed commits`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fast-export`, firmado commits modifica la forma en que se ejecuta emitir historial y referencias en un flujo para migración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fast-export --signed-commits=all --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--tag-of-filtered-object`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta emitir historial y referencias en un flujo para migración. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fast-export --tag-of-filtered-object=all --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reencode`

Define reencode para esta ejecución de `git fast-export`. En Git 2.51.1, la ayuda corta expresa el contrato como `select handling of commit messages in an alternate encoding`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fast-export`, reencode modifica la forma en que se ejecuta emitir historial y referencias en un flujo para migración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fast-export --reencode=all --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--export-marks`

Activa export marks durante emitir historial y referencias en un flujo para migración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `dump marks to this file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git fast-export` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fast-export --export-marks=rutas.txt --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--import-marks`

Activa import marks durante emitir historial y referencias en un flujo para migración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `import marks from this file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git fast-export` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fast-export --import-marks=rutas.txt --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--import-marks-if-exists`

Activa import marks if exists durante emitir historial y referencias en un flujo para migración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `import marks from this file if it exists`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git fast-export` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fast-export --import-marks-if-exists=rutas.txt --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--fake-missing-tagger`

Activa fake missing tagger durante emitir historial y referencias en un flujo para migración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `fake a tagger when tags lack one`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta emitir historial y referencias en un flujo para migración. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fast-export --fake-missing-tagger --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--full-tree`

Incluye full tree en la salida o cambia cómo `git fast-export` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output full tree for each commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fast-export --full-tree --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--use-done-feature`

Define use done feature para esta ejecución de `git fast-export`. En Git 2.51.1, la ayuda corta expresa el contrato como `use the done feature to terminate the stream`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fast-export`, use done feature modifica la forma en que se ejecuta emitir historial y referencias en un flujo para migración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fast-export --use-done-feature --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-data`

Desactiva el comportamiento `data` para esta invocación.

En `git fast-export`, desactivar data modifica la forma en que se ejecuta emitir historial y referencias en un flujo para migración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fast-export --no-data --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--data`

Selecciona la relación indicada por data; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-data`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fast-export`, data modifica la forma en que se ejecuta emitir historial y referencias en un flujo para migración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fast-export --data --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--refspec`

Activa refspec durante emitir historial y referencias en un flujo para migración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `apply refspec to exported refs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git fast-export`, refspec modifica la forma en que se ejecuta emitir historial y referencias en un flujo para migración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fast-export --refspec=main --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--anonymize`

Incluye anonymize en la salida o cambia cómo `git fast-export` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `anonymize output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fast-export --anonymize --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--anonymize-map`

Incluye anonymize map en la salida o cambia cómo `git fast-export` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `convert <from> to <to> in anonymized output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fast-export --anonymize-map=valor --all > historial.fi
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reference-excluded-parents`

Activa reference excluded parents durante emitir historial y referencias en un flujo para migración. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `reference parents which are not in fast-export stream by object id`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta emitir historial y referencias en un flujo para migración. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fast-export --reference-excluded-parents --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--show-original-ids`

Incluye información adicional en la salida.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fast-export --show-original-ids --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mark-tags`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta emitir historial y referencias en un flujo para migración. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fast-export --mark-tags --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fast-export --no-progress --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signed-tags`

Desactiva para esta invocación el comportamiento que habilita `--signed-tags`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta emitir historial y referencias en un flujo para migración. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fast-export --no-signed-tags --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signed-commits`

Desactiva para esta invocación el comportamiento que habilita `--signed-commits`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fast-export`, desactivar firmado commits modifica la forma en que se ejecuta emitir historial y referencias en un flujo para migración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fast-export --no-signed-commits --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-tag-of-filtered-object`

Desactiva para esta invocación el comportamiento que habilita `--tag-of-filtered-object`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta emitir historial y referencias en un flujo para migración. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fast-export --no-tag-of-filtered-object --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reencode`

Desactiva para esta invocación el comportamiento que habilita `--reencode`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fast-export`, desactivar reencode modifica la forma en que se ejecuta emitir historial y referencias en un flujo para migración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fast-export --no-reencode --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-export-marks`

Desactiva para esta invocación el comportamiento que habilita `--export-marks`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git fast-export` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fast-export --no-export-marks --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-import-marks`

Desactiva para esta invocación el comportamiento que habilita `--import-marks`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git fast-export` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fast-export --no-import-marks --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-import-marks-if-exists`

Desactiva para esta invocación el comportamiento que habilita `--import-marks-if-exists`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git fast-export` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fast-export --no-import-marks-if-exists --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-fake-missing-tagger`

Desactiva para esta invocación el comportamiento que habilita `--fake-missing-tagger`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta emitir historial y referencias en un flujo para migración. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fast-export --no-fake-missing-tagger --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-full-tree`

Desactiva para esta invocación el comportamiento que habilita `--full-tree`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fast-export --no-full-tree --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-use-done-feature`

Desactiva para esta invocación el comportamiento que habilita `--use-done-feature`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fast-export`, desactivar use done feature modifica la forma en que se ejecuta emitir historial y referencias en un flujo para migración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fast-export --no-use-done-feature --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-refspec`

Desactiva para esta invocación el comportamiento que habilita `--refspec`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git fast-export`, desactivar refspec modifica la forma en que se ejecuta emitir historial y referencias en un flujo para migración. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fast-export --no-refspec --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-anonymize`

Desactiva para esta invocación el comportamiento que habilita `--anonymize`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fast-export --no-anonymize --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-reference-excluded-parents`

Desactiva para esta invocación el comportamiento que habilita `--reference-excluded-parents`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta emitir historial y referencias en un flujo para migración. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fast-export --no-reference-excluded-parents --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-show-original-ids`

Desactiva para esta invocación el comportamiento que habilita `--show-original-ids`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fast-export --no-show-original-ids --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-mark-tags`

Desactiva para esta invocación el comportamiento que habilita `--mark-tags`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta emitir historial y referencias en un flujo para migración. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fast-export --no-mark-tags --all > historial.fi
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fast-export` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Faltan revisiones

Comprueba esta causa: El rango, rama o marcador de importación las excluye. Compara conteos y el último identificador importado.

### La identidad cambia

Comprueba esta causa: No existe una regla de mapeo estable. Define el mapa antes de repetir la importación.

### La sincronización duplica cambios

Comprueba esta causa: Se perdió el marcador entre sistemas. Restaura el punto de control y prueba sobre una copia.

## Automatización y recuperación

Persistencia: No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git fast-import`](../external-systems/fast-import.md)
- [`git cvsserver`](../external-systems/cvsserver.md)
- [`git p4`](../external-systems/p4.md)

## Fuente

- [git-fast-export - Git data exporter](https://git-scm.com/docs/git-fast-export)
