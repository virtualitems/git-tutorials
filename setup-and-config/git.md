---
title: "git"
source: "https://git-scm.com/docs/git"
section: "setup-and-config"
status: "option-expanded"
---

# `git`

Este caso usa `git` para invocar Git, elegir el repositorio y aplicar opciones globales. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git define cómo Git localiza configuración, ejecutables, repositorios y diagnósticos. Recibe como entrada el ámbito, la clave o el dato del entorno indicado por la orden. La operación consiste en invocar Git, elegir el repositorio y aplicar opciones globales.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

## Ejemplo mínimo

```bash
git -C ../biblioteca status
git -c color.ui=false log --oneline -3
```

La invocación `git -C ../biblioteca status` ejecuta esta operación: invocar Git, elegir el repositorio y aplicar opciones globales. Después, una consulta posterior muestra el valor efectivo o la información generada. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
    [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
    [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--no-lazy-fetch]
    [--no-optional-locks] [--no-advice] [--bare] [--git-dir=<path>]
```

### Uso verificado con `git version 2.51.1`

```text
git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--no-lazy-fetch]
           [--no-optional-locks] [--no-advice] [--bare] [--git-dir=<path>]
           [--work-tree=<path>] [--namespace=<name>] [--config-env=<name>=<envvar>]
           <command> [<args>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

invocar Git, elegir el repositorio y aplicar opciones globales. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-v`

Activa v durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git -v -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--version`

Muestra la versión y termina.

En `git`, versión modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --version
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-h`

Muestra ayuda corta cuando la orden admite esta convención.

En `git`, h modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git -h
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--help`

Muestra la ayuda correspondiente a la versión instalada.

En `git`, ayuda modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --help
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

En `git`, C modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-c`

Aplica una clave de configuración solo a esta invocación.

En `git`, c modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git -c -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exec-path`

Activa exec ruta durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git`, exec ruta modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --exec-path -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--html-path`

Activa html ruta durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git`, html ruta modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --html-path -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--man-path`

Activa man ruta durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git`, man ruta modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --man-path -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--info-path`

Activa info ruta durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git`, info ruta modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --info-path -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p`

Activa p durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git`, p modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git -p -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--paginate`

Envía la salida por el paginador configurado.

En `git`, paginate modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --paginate -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-P`

Activa P durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git`, P modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git -P -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-pager`

Escribe la salida sin paginador.

En `git`, desactivar pager modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --no-pager -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-replace-objects`

Ignora referencias de reemplazo durante la lectura de objetos.

En `git`, desactivar replace objetos modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --no-replace-objects -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-lazy-fetch`

Desactiva el comportamiento `lazy-fetch` para esta invocación.

En `git`, desactivar lazy fetch modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --no-lazy-fetch -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-optional-locks`

Desactiva el comportamiento `optional-locks` para esta invocación.

En `git`, desactivar optional locks modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --no-optional-locks -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-advice`

Desactiva el comportamiento `advice` para esta invocación.

En `git`, desactivar advice modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --no-advice -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--bare`

Opera sin un área de trabajo asociada.

En `git`, repositorio bare modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --bare -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--git-dir`

Define de forma explícita la ruta del directorio Git.

En `git`, git dir modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --git-dir -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--work-tree`

Define de forma explícita la raíz del área de trabajo.

En `git`, work tree modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --work-tree -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--namespace`

Selecciona el namespace de referencias para la invocación.

En `git`, namespace modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --namespace -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--config-env`

Toma un valor de configuración desde una variable de entorno.

En `git`, config env modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git --config-env -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a`

Activa a durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git`, a modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git -a -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-g`

Activa g durante invocar Git, elegir el repositorio y aplicar opciones globales. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git`, g modifica la forma en que se ejecuta invocar Git, elegir el repositorio y aplicar opciones globales. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git -g -C ../biblioteca status
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El valor aplicado no coincide

Comprueba esta causa: Otra capa de configuración tiene precedencia. Ejecuta `git config --show-origin --get-all <clave>`.

### Git no localiza el repositorio

Comprueba esta causa: `--git-dir`, `--work-tree` o el directorio actual apuntan a otra ruta. Ejecuta `git rev-parse --show-toplevel`.

### La orden no existe

Comprueba esta causa: La versión instalada no incluye la función. Comprueba `git --version` y `git help -a`.

## Automatización y recuperación

Persistencia: No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Ejecuta el ejemplo en un repositorio temporal y usa `git config --show-origin --list` o el comando de consulta correspondiente para identificar el origen del resultado.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git config`](../setup-and-config/config.md)
- [`git bugreport`](../setup-and-config/bugreport.md)

## Fuente

- [git - the stupid content tracker](https://git-scm.com/docs/git)
