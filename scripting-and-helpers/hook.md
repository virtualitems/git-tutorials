---
title: "git hook"
source: "https://git-scm.com/docs/git-hook"
section: "scripting-and-helpers"
status: "option-expanded"
---

# `git hook`

Este caso usa `git hook` para enumerar o ejecutar hooks mediante Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git hook ofrece contratos de entrada y salida para scripts, hooks y procesos auxiliares. Recibe como entrada datos controlados por entrada estándar, argumentos o configuración. La operación consiste en enumerar o ejecutar hooks mediante Git.

El helper usa stdout, archivos auxiliares o un proceso llamado; su contrato define si persiste datos.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git hook list pre-commit
git hook run pre-commit
```

La invocación `git hook list pre-commit` ejecuta esta operación: enumerar o ejecutar hooks mediante Git. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git hook run [--allow-unknown-hook-name] [--ignore-missing] [--to-stdin=<path>] [(-j|--jobs) <n>]
	<hook-name> [-- <hook-args>]
git hook list [--allow-unknown-hook-name] [-z] [--show-scope] <hook-name>
```

### Uso verificado con `git version 2.51.1`

```text
git hook run [--ignore-missing] [--to-stdin=<path>] <hook-name> [-- <hook-args>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git hook -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

enumerar o ejecutar hooks mediante Git. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git hook a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git hook con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--allow-unknown-hook-name`

Activa permitir unknown hook nombre durante enumerar o ejecutar hooks mediante Git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta enumerar o ejecutar hooks mediante Git. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git hook --allow-unknown-hook-name list pre-commit
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git hook` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-missing`

Permite comprobar rutas ausentes bajo las condiciones que define la orden.

En `git hook`, ignorar missing modifica la forma en que se ejecuta enumerar o ejecutar hooks mediante Git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git hook --ignore-missing list pre-commit
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git hook` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--to-stdin`

Activa to entrada estándar durante enumerar o ejecutar hooks mediante Git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git hook` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git hook --to-stdin list pre-commit
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git hook` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-j`

Activa j durante enumerar o ejecutar hooks mediante Git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git hook`, j modifica la forma en que se ejecuta enumerar o ejecutar hooks mediante Git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git hook -j list pre-commit
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git hook` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--jobs`

Define cuántas tareas puede ejecutar Git en paralelo para la operación.

En `git hook`, jobs modifica la forma en que se ejecuta enumerar o ejecutar hooks mediante Git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git hook --jobs list pre-commit
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git hook` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

En `git hook`, z modifica la forma en que se ejecuta enumerar o ejecutar hooks mediante Git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git hook -z list pre-commit
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git hook` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--show-scope`

Muestra el alcance de cada valor de configuración.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git hook --show-scope list pre-commit
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git hook` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

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

- [`git interpret-trailers`](../scripting-and-helpers/interpret-trailers.md)
- [`git fmt-merge-msg`](../scripting-and-helpers/fmt-merge-msg.md)
- [`git mailinfo`](../scripting-and-helpers/mailinfo.md)

## Fuente

- [git-hook - Run Git hooks](https://git-scm.com/docs/git-hook)
