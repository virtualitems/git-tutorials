---
title: "git instaweb"
source: "https://git-scm.com/docs/git-instaweb"
section: "graphical-tools"
status: "option-expanded"
---

# `git instaweb`

Este caso usa `git instaweb` para iniciar una instancia temporal de gitweb. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git instaweb presenta commits, cambios o acciones mediante una interfaz de escritorio o HTTP. Recibe como entrada el repositorio y la vista u operación elegida en la interfaz. La operación consiste en iniciar una instancia temporal de gitweb.

Inicia o atiende un servicio. El repositorio cambia solo si el servicio y la política admiten una operación de escritura.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La interfaz presenta operaciones que también existen en el modelo de objetos, índice, referencias y commits. La vista cambia; el repositorio conserva el mismo estado.

Relaciona cada acción de la interfaz con índice, commit o referencia. Usa una consulta de Git para comprobar el cambio de estado.

## Ejemplo mínimo

```bash
git instaweb --start
git instaweb --stop
```

La invocación `git instaweb --start` ejecuta esta operación: iniciar una instancia temporal de gitweb. Después, los comandos de consulta confirman el mismo estado que presenta la interfaz. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git instaweb [--local] [--httpd=<httpd>] [--port=<port>]
               [--browser=<browser>]
git instaweb [--start] [--stop] [--restart]
```

### Uso verificado con `git version 2.51.1`

```text
git instaweb [options] (--start | --stop | --restart)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git instaweb -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

iniciar una instancia temporal de gitweb. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git instaweb a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git instaweb con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--local` y `-l`

Opera sobre la configuración del repositorio.  La misma línea de ayuda también acepta `-l`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git instaweb`, alcance local modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--local`

```bash
git instaweb --local --start
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `-l`

```bash
git instaweb -l --start
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--httpd` y `-d`

Activa httpd durante iniciar una instancia temporal de gitweb. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `the command to launch`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-d`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git instaweb`, httpd modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--httpd`

```bash
git instaweb --httpd --start
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `-d`

```bash
git instaweb -d --start
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--port` y `-p`

Activa port durante iniciar una instancia temporal de gitweb. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `the port to bind to`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-p`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git instaweb`, port modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--port`

```bash
git instaweb --port --start
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `-p`

```bash
git instaweb -p --start
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--browser` y `-b`

Activa browser durante iniciar una instancia temporal de gitweb. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `the browser to launch`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-b`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git instaweb`, browser modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--browser`

```bash
git instaweb --browser --start
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `-b`

```bash
git instaweb -b --start
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--start`

Activa start durante iniciar una instancia temporal de gitweb. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `start the web server`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git instaweb`, start modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git instaweb --start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stop`

Activa stop durante iniciar una instancia temporal de gitweb. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `stop the web server`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git instaweb`, stop modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git instaweb --stop --start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--restart`

Activa restart durante iniciar una instancia temporal de gitweb. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `restart the web server`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git instaweb`, restart modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git instaweb --restart --start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--module-path`

Limita iniciar una instancia temporal de gitweb al alcance identificado por module ruta. En Git 2.51.1, la ayuda corta expresa el contrato como `the module path (only needed for apache2)`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-m`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git instaweb`, module ruta modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-m`

```bash
git instaweb -m --start
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--module-path`

```bash
git instaweb --module-path --start
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-local`

Desactiva para esta invocación el comportamiento que habilita `--local`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git instaweb`, desactivar alcance local modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git instaweb --no-local --start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-httpd`

Desactiva para esta invocación el comportamiento que habilita `--httpd`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git instaweb`, desactivar httpd modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git instaweb --no-httpd --start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-port`

Desactiva para esta invocación el comportamiento que habilita `--port`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git instaweb`, desactivar port modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git instaweb --no-port --start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-browser`

Desactiva para esta invocación el comportamiento que habilita `--browser`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git instaweb`, desactivar browser modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git instaweb --no-browser --start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-start`

Desactiva para esta invocación el comportamiento que habilita `--start`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git instaweb`, desactivar start modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git instaweb --no-start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stop`

Desactiva para esta invocación el comportamiento que habilita `--stop`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git instaweb`, desactivar stop modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git instaweb --no-stop --start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-restart`

Desactiva para esta invocación el comportamiento que habilita `--restart`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git instaweb`, desactivar restart modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git instaweb --no-restart --start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-module-path`

Desactiva para esta invocación el comportamiento que habilita `--module-path`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git instaweb`, desactivar module ruta modifica la forma en que se ejecuta iniciar una instancia temporal de gitweb. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git instaweb --no-module-path --start
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git instaweb` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La interfaz no inicia

Comprueba esta causa: Falta el entorno gráfico, un intérprete o un puerto. Comprueba dependencias y ejecuta desde el repositorio.

### No aparecen cambios

Comprueba esta causa: La herramienta abrió otra ruta o referencia. Confirma la raíz y la referencia mostradas.

### El servicio queda activo

Comprueba esta causa: El proceso web se ejecuta en segundo plano. Usa la orden de parada de la herramienta y verifica el puerto.

## Automatización y recuperación

Persistencia: Inicia o atiende un servicio. El repositorio cambia solo si el servicio y la política admiten una operación de escritura. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Realiza una operación en la interfaz y verifica el resultado con `git status`, `git log` o `git show`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`gitk`](../graphical-tools/gitk.md)
- [`git gui`](../graphical-tools/gui.md)
- [`gitweb`](../graphical-tools/gitweb.md)

## Fuente

- [git-instaweb - Instantly browse your working repository in gitweb](https://git-scm.com/docs/git-instaweb)
