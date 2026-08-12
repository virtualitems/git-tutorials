---
title: "git column"
source: "https://git-scm.com/docs/git-column"
section: "scripting-and-helpers"
status: "option-expanded"
---

# `git column`

Este caso usa `git column` para organizar líneas de entrada en columnas. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git column ofrece contratos de entrada y salida para scripts, hooks y procesos auxiliares. Recibe como entrada datos controlados por entrada estándar, argumentos o configuración. La operación consiste en organizar líneas de entrada en columnas.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
printf '%s\n' main develop release | git column --mode=column
```

La invocación `git column` ejecuta esta operación: organizar líneas de entrada en columnas. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git column [--command=<name>] [--[raw-]mode=<mode>] [--width=<width>]
	     [--indent=<string>] [--nl=<string>] [--padding=<n>]
```

### Uso verificado con `git version 2.51.1`

```text
git column [<options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git column -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

organizar líneas de entrada en columnas. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git column a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git column con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--command`

Activa command durante organizar líneas de entrada en columnas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git column`, command modifica la forma en que se ejecuta organizar líneas de entrada en columnas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git column --command=tema
printf 'exit=%s\n' "$?"
```

El ejemplo usa `tema` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--width`

Define el límite representado por width para esta ejecución. En Git 2.51.1, la ayuda corta expresa el contrato como `maximum width`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git column`, width modifica la forma en que se ejecuta organizar líneas de entrada en columnas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git column --width=5
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--indent`

Activa indent durante organizar líneas de entrada en columnas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `padding space on left border`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git column`, indent modifica la forma en que se ejecuta organizar líneas de entrada en columnas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git column --indent=valor
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--nl`

Activa nl durante organizar líneas de entrada en columnas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `padding space on right border`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git column`, nl modifica la forma en que se ejecuta organizar líneas de entrada en columnas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git column --nl=valor
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--padding`

Activa padding durante organizar líneas de entrada en columnas. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `padding space between columns`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git column`, padding modifica la forma en que se ejecuta organizar líneas de entrada en columnas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git column --padding=5
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mode`

Define mode para esta ejecución de `git column`.

En `git column`, mode modifica la forma en que se ejecuta organizar líneas de entrada en columnas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git column --mode=short
printf 'exit=%s\n' "$?"
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--raw-mode`

Define raw mode para esta ejecución de `git column`. En Git 2.51.1, la ayuda corta expresa el contrato como `layout to use`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git column`, raw mode modifica la forma en que se ejecuta organizar líneas de entrada en columnas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git column --raw-mode=5
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-command`

Desactiva para esta invocación el comportamiento que habilita `--command`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git column`, desactivar command modifica la forma en que se ejecuta organizar líneas de entrada en columnas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git column --no-command
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git column` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-width`

Desactiva para esta invocación el comportamiento que habilita `--width`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git column`, desactivar width modifica la forma en que se ejecuta organizar líneas de entrada en columnas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git column --no-width
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git column` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-indent`

Desactiva para esta invocación el comportamiento que habilita `--indent`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git column`, desactivar indent modifica la forma en que se ejecuta organizar líneas de entrada en columnas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git column --no-indent
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git column` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-nl`

Desactiva para esta invocación el comportamiento que habilita `--nl`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git column`, desactivar nl modifica la forma en que se ejecuta organizar líneas de entrada en columnas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git column --no-nl
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git column` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-padding`

Desactiva para esta invocación el comportamiento que habilita `--padding`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git column`, desactivar padding modifica la forma en que se ejecuta organizar líneas de entrada en columnas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git column --no-padding
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git column` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-mode`

Desactiva para esta invocación el comportamiento que habilita `--mode`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git column`, desactivar mode modifica la forma en que se ejecuta organizar líneas de entrada en columnas. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git column --no-mode
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git column` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un nombre se divide

Comprueba esta causa: El script usa espacios como separador para rutas. Usa NUL o el formato estructurado que admita la orden.

### Un predicado detiene el script

Comprueba esta causa: El código 1 representa una respuesta negativa. Evalúa el código de forma explícita.

### El helper espera más datos

Comprueba esta causa: El protocolo de stdin requiere una línea vacía o longitud. Escribe el terminador definido y conserva el orden de campos.

## Automatización y recuperación

Persistencia: No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git credential`](../scripting-and-helpers/credential.md)
- [`git check-ref-format`](../scripting-and-helpers/check-ref-format.md)
- [`git credential-cache`](../scripting-and-helpers/credential-cache.md)

## Fuente

- [git-column - Display data in columns](https://git-scm.com/docs/git-column)
