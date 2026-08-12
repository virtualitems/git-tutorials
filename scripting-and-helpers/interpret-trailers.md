---
title: "git interpret-trailers"
source: "https://git-scm.com/docs/git-interpret-trailers"
section: "scripting-and-helpers"
status: "option-expanded"
---

# `git interpret-trailers`

Este caso usa `git interpret-trailers` para analizar y añadir campos al final de mensajes de commit. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git interpret-trailers ofrece contratos de entrada y salida para scripts, hooks y procesos auxiliares. Recibe como entrada datos controlados por entrada estándar, argumentos o configuración. La operación consiste en analizar y añadir campos al final de mensajes de commit.

El helper usa stdout, archivos auxiliares o un proceso llamado; su contrato define si persiste datos.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
printf '%s\n' 'Corrige el índice' | git interpret-trailers --trailer 'Reviewed-by: Ana <user@example.com>'
```

La invocación `git interpret-trailers` ejecuta esta operación: analizar y añadir campos al final de mensajes de commit. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git interpret-trailers [--in-place] [--trim-empty]
			[(--trailer (<key>|<key-alias>)[(=|:)<value>])…]
			[--parse] [<file>…]
```

### Uso verificado con `git version 2.51.1`

```text
git interpret-trailers [--in-place] [--trim-empty]
                              [(--trailer (<key>|<key-alias>)[(=|:)<value>])...]
                              [--parse] [<file>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git interpret-trailers -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

analizar y añadir campos al final de mensajes de commit. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git interpret-trailers a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git interpret-trailers con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--in-place`

Activa in place durante analizar y añadir campos al final de mensajes de commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `edit files in place`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git interpret-trailers` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git interpret-trailers --in-place
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--trim-empty`

Activa trim vacío durante analizar y añadir campos al final de mensajes de commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `trim empty trailers`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git interpret-trailers`, trim vacío modifica la forma en que se ejecuta analizar y añadir campos al final de mensajes de commit. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git interpret-trailers --trim-empty
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--trailer`

Incluye trailer en la entrada, el resultado o el registro que construye `git interpret-trailers`. En Git 2.51.1, la ayuda corta expresa el contrato como `trailer(s) to add`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git interpret-trailers`, trailer modifica la forma en que se ejecuta analizar y añadir campos al final de mensajes de commit. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git interpret-trailers --trailer=valor
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--parse`

Limita analizar y añadir campos al final de mensajes de commit al alcance identificado por parse. En Git 2.51.1, la ayuda corta expresa el contrato como `alias for --only-trailers --only-input --unfold`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git interpret-trailers` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git interpret-trailers --parse
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--where`

Activa where durante analizar y añadir campos al final de mensajes de commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `where to place the new trailer`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git interpret-trailers`, where modifica la forma en que se ejecuta analizar y añadir campos al final de mensajes de commit. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git interpret-trailers --where=valor
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--if-exists`

Activa if exists durante analizar y añadir campos al final de mensajes de commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `action if trailer already exists`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git interpret-trailers`, if exists modifica la forma en que se ejecuta analizar y añadir campos al final de mensajes de commit. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git interpret-trailers --if-exists=warn
printf 'exit=%s\n' "$?"
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--if-missing`

Activa if missing durante analizar y añadir campos al final de mensajes de commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `action if trailer is missing`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git interpret-trailers`, if missing modifica la forma en que se ejecuta analizar y añadir campos al final de mensajes de commit. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git interpret-trailers --if-missing=warn
printf 'exit=%s\n' "$?"
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--only-trailers`

Limita analizar y añadir campos al final de mensajes de commit al alcance identificado por only trailers. En Git 2.51.1, la ayuda corta expresa el contrato como `output only the trailers`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git interpret-trailers --only-trailers
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--only-input`

Impide only entrada durante esta invocación de `git interpret-trailers`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not apply trailer.* configuration variables`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git interpret-trailers` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git interpret-trailers --only-input
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--unfold`

Activa unfold durante analizar y añadir campos al final de mensajes de commit. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `reformat multiline trailer values as single-line values`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git interpret-trailers --unfold
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-divider`

Desactiva el comportamiento `divider` para esta invocación.

En `git interpret-trailers`, desactivar divider modifica la forma en que se ejecuta analizar y añadir campos al final de mensajes de commit. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git interpret-trailers --no-divider
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--divider`

Selecciona la relación indicada por divider; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-divider`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git interpret-trailers`, divider modifica la forma en que se ejecuta analizar y añadir campos al final de mensajes de commit. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git interpret-trailers --divider
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-in-place`

Desactiva para esta invocación el comportamiento que habilita `--in-place`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git interpret-trailers` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git interpret-trailers --no-in-place
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-trim-empty`

Desactiva para esta invocación el comportamiento que habilita `--trim-empty`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git interpret-trailers`, desactivar trim vacío modifica la forma en que se ejecuta analizar y añadir campos al final de mensajes de commit. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git interpret-trailers --no-trim-empty
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-trailer`

Desactiva para esta invocación el comportamiento que habilita `--trailer`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git interpret-trailers`, desactivar trailer modifica la forma en que se ejecuta analizar y añadir campos al final de mensajes de commit. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git interpret-trailers --no-trailer
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-where`

Desactiva para esta invocación el comportamiento que habilita `--where`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git interpret-trailers`, desactivar where modifica la forma en que se ejecuta analizar y añadir campos al final de mensajes de commit. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git interpret-trailers --no-where
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-if-exists`

Desactiva para esta invocación el comportamiento que habilita `--if-exists`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git interpret-trailers`, desactivar if exists modifica la forma en que se ejecuta analizar y añadir campos al final de mensajes de commit. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git interpret-trailers --no-if-exists
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-if-missing`

Desactiva para esta invocación el comportamiento que habilita `--if-missing`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git interpret-trailers`, desactivar if missing modifica la forma en que se ejecuta analizar y añadir campos al final de mensajes de commit. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git interpret-trailers --no-if-missing
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-only-trailers`

Desactiva para esta invocación el comportamiento que habilita `--only-trailers`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git interpret-trailers --no-only-trailers
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-only-input`

Desactiva para esta invocación el comportamiento que habilita `--only-input`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git interpret-trailers` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git interpret-trailers --no-only-input
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-unfold`

Desactiva para esta invocación el comportamiento que habilita `--unfold`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git interpret-trailers --no-unfold
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git interpret-trailers` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un nombre se divide

Comprueba esta causa: El script usa espacios como separador para rutas. Usa NUL o el formato estructurado que admita la orden.

### Un predicado detiene el script

Comprueba esta causa: El código 1 representa una respuesta negativa. Evalúa el código de forma explícita.

### El helper espera más datos

Comprueba esta causa: El protocolo de stdin requiere una línea vacía o longitud. Escribe el terminador definido y conserva el orden de campos.

## Automatización y recuperación

Persistencia: El helper usa stdout, archivos auxiliares o un proceso llamado; su contrato define si persiste datos. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git mailinfo`](../scripting-and-helpers/mailinfo.md)
- [`git hook`](../scripting-and-helpers/hook.md)
- [`git mailsplit`](../scripting-and-helpers/mailsplit.md)

## Fuente

- [git-interpret-trailers - Add or parse structured information in commit messages](https://git-scm.com/docs/git-interpret-trailers)
