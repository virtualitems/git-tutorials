---
title: "git http-fetch"
source: "https://git-scm.com/docs/git-http-fetch"
section: "server-and-transport"
status: "option-expanded"
---

# `git http-fetch`

Este caso usa `git http-fetch` para descargar objetos mediante el transporte HTTP heredado. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Responsabilidad y efecto

git http-fetch expone repositorios o participa en negociación y transferencia de objetos. Recibe como entrada la ruta del repositorio, el servicio y los parámetros de transporte. La operación consiste en descargar objetos mediante el transporte HTTP heredado.

Puede persistir el estado implicado por esta operación: descargar objetos mediante el transporte HTTP heredado. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git http-fetch HEAD https://example.test/equipo/biblioteca.git
```

La invocación `git http-fetch HEAD https://example.test/equipo/biblioteca.git` ejecuta esta operación: descargar objetos mediante el transporte HTTP heredado. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git http-fetch [-c] [-t] [-a] [-d] [-v] [-w <filename>] [--recover] [--stdin | --packfile=<hash> | <commit>] <URL>
```

### Uso verificado con `git version 2.51.1`

```text
git http-fetch [-c] [-t] [-a] [-v] [--recover] [-w ref] [--stdin | --packfile=hash | commit-id] url
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git http-fetch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

descargar objetos mediante el transporte HTTP heredado. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git http-fetch a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git http-fetch con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-c`

Aplica una clave de configuración solo a esta invocación.

En `git http-fetch`, c modifica la forma en que se ejecuta descargar objetos mediante el transporte HTTP heredado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git http-fetch -c HEAD https://example.test/equipo/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git http-fetch` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-t`

Activa t durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git http-fetch`, t modifica la forma en que se ejecuta descargar objetos mediante el transporte HTTP heredado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git http-fetch -t HEAD https://example.test/equipo/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git http-fetch` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a`

Activa a durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git http-fetch`, a modifica la forma en que se ejecuta descargar objetos mediante el transporte HTTP heredado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git http-fetch -a HEAD https://example.test/equipo/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git http-fetch` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d`

Activa d durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git http-fetch`, d modifica la forma en que se ejecuta descargar objetos mediante el transporte HTTP heredado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git http-fetch -d HEAD https://example.test/equipo/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git http-fetch` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v`

Activa v durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta descargar objetos mediante el transporte HTTP heredado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git http-fetch -v HEAD https://example.test/equipo/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git http-fetch` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-w`

Activa w durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git http-fetch`, w modifica la forma en que se ejecuta descargar objetos mediante el transporte HTTP heredado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git http-fetch -w HEAD https://example.test/equipo/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git http-fetch` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recover`

Activa recover durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git http-fetch`, recover modifica la forma en que se ejecuta descargar objetos mediante el transporte HTTP heredado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git http-fetch --recover HEAD https://example.test/equipo/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git http-fetch` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git http-fetch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git http-fetch --stdin HEAD https://example.test/equipo/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git http-fetch` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--packfile`

Activa packfile durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git http-fetch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git http-fetch --packfile HEAD https://example.test/equipo/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git http-fetch` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El repositorio no se anuncia

Comprueba esta causa: La ruta, exportación o política no lo permite. Comprueba la raíz del servicio y los marcadores de exportación.

### La negociación se corta

Comprueba esta causa: Cliente y servidor no acuerdan capacidad o protocolo. Registra trazas sin incluir credenciales y compara versiones.

### La recepción se rechaza

Comprueba esta causa: Los permisos o hooks bloquean la referencia. Revisa la política del repositorio y el mensaje del hook.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: descargar objetos mediante el transporte HTTP heredado. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git http-push`](../server-and-transport/http-push.md)
- [`git http-backend`](../server-and-transport/http-backend.md)
- [`git receive-pack`](../server-and-transport/receive-pack.md)

## Fuente

- [git-http-fetch - Download from a remote Git repository via HTTP](https://git-scm.com/docs/git-http-fetch)
