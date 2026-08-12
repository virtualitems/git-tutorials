---
title: "git check-ref-format"
source: "https://git-scm.com/docs/git-check-ref-format"
section: "scripting-and-helpers"
status: "option-expanded"
---

# `git check-ref-format`

Este caso usa `git check-ref-format` para validar la sintaxis de un nombre de referencia. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git check-ref-format ofrece contratos de entrada y salida para scripts, hooks y procesos auxiliares. Recibe como entrada datos controlados por entrada estándar, argumentos o configuración. La operación consiste en validar la sintaxis de un nombre de referencia.

No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git check-ref-format 'refs/heads/tema-portada'
```

La invocación `git check-ref-format 'refs/heads/tema-portada'` ejecuta esta operación: validar la sintaxis de un nombre de referencia. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git check-ref-format [--normalize]
       [--[no-]allow-onelevel] [--refspec-pattern]
       <refname>
git check-ref-format --branch <branchname-shorthand>
```

### Uso verificado con `git version 2.51.1`

```text
git check-ref-format [--normalize] [<options>] <refname>
   or: git check-ref-format --branch <branchname-shorthand>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git check-ref-format -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

validar la sintaxis de un nombre de referencia. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git check-ref-format a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git check-ref-format con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--normalize`

Activa normalize durante validar la sintaxis de un nombre de referencia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git check-ref-format`, normalize modifica la forma en que se ejecuta validar la sintaxis de un nombre de referencia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git check-ref-format --normalize 'refs/heads/tema-portada'
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git check-ref-format` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--allow-onelevel`

Activa permitir onelevel durante validar la sintaxis de un nombre de referencia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta validar la sintaxis de un nombre de referencia. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git check-ref-format --allow-onelevel 'refs/heads/tema-portada'
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git check-ref-format` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--refspec-pattern`

Activa refspec pattern durante validar la sintaxis de un nombre de referencia. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git check-ref-format`, refspec pattern modifica la forma en que se ejecuta validar la sintaxis de un nombre de referencia. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git check-ref-format --refspec-pattern 'refs/heads/tema-portada'
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git check-ref-format` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--branch`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta validar la sintaxis de un nombre de referencia. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git check-ref-format --branch 'refs/heads/tema-portada'
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git check-ref-format` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

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

- [`git column`](../scripting-and-helpers/column.md)
- [`git check-mailmap`](../scripting-and-helpers/check-mailmap.md)
- [`git credential`](../scripting-and-helpers/credential.md)

## Fuente

- [git-check-ref-format - Ensures that a reference name is well formed](https://git-scm.com/docs/git-check-ref-format)
