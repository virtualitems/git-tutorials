---
title: "git stripspace"
source: "https://git-scm.com/docs/git-stripspace"
section: "scripting-and-helpers"
status: "option-expanded"
---

# `git stripspace`

Este caso usa `git stripspace` para normalizar espacios, líneas vacías y comentarios de un mensaje. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git stripspace ofrece contratos de entrada y salida para scripts, hooks y procesos auxiliares. Recibe como entrada datos controlados por entrada estándar, argumentos o configuración. La operación consiste en normalizar espacios, líneas vacías y comentarios de un mensaje.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
printf 'Título  \n\n\nCuerpo\n' | git stripspace
```

La invocación `git stripspace` ejecuta esta operación: normalizar espacios, líneas vacías y comentarios de un mensaje. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git stripspace [-s | --strip-comments]
git stripspace [-c | --comment-lines]
```

### Uso verificado con `git version 2.51.1`

```text
git stripspace [-s | --strip-comments]
   or: git stripspace [-c | --comment-lines]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git stripspace -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

normalizar espacios, líneas vacías y comentarios de un mensaje. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git stripspace a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git stripspace con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-s` y `--strip-comments`

Retira strip comments del alcance que procesa `git stripspace`. En Git 2.51.1, la ayuda corta expresa el contrato como `skip and remove all lines starting with comment character`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-s`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

Esta forma se usa cuando `git stripspace` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque strip comments actúa sobre el estado que Git registró al iniciar la secuencia.

#### Ejemplo con `-s`

```bash
git stripspace -s
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git stripspace` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--strip-comments`

```bash
git stripspace --strip-comments
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git stripspace` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-c` y `--comment-lines`

Antepone comment lines al valor que produce `git stripspace`. En Git 2.51.1, la ayuda corta expresa el contrato como `prepend comment character and space to each line`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-c`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git stripspace`, comment lines modifica la forma en que se ejecuta normalizar espacios, líneas vacías y comentarios de un mensaje. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-c`

```bash
git stripspace -c
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git stripspace` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--comment-lines`

```bash
git stripspace --comment-lines
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git stripspace` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

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

- [`git url-parse`](../scripting-and-helpers/url-parse.md)
- [`git sh-setup`](../scripting-and-helpers/sh-setup.md)
- [`git sh-i18n`](../scripting-and-helpers/sh-i18n.md)

## Fuente

- [git-stripspace - Remove unnecessary whitespace](https://git-scm.com/docs/git-stripspace)
