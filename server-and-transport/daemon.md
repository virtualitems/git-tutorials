---
title: "git daemon"
source: "https://git-scm.com/docs/git-daemon"
section: "server-and-transport"
status: "option-expanded"
---

# `git daemon`

Este caso usa `git daemon` para servir repositorios mediante el protocolo git. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Responsabilidad y efecto

git daemon expone repositorios o participa en negociación y transferencia de objetos. Recibe como entrada la ruta del repositorio, el servicio y los parámetros de transporte. La operación consiste en servir repositorios mediante el protocolo git.

Inicia o atiende un servicio. El repositorio cambia solo si el servicio y la política admiten una operación de escritura.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git daemon --reuseaddr --base-path=/srv/git /srv/git
```

La invocación `git daemon --reuseaddr --base-path=/srv/git /srv/git` ejecuta esta operación: servir repositorios mediante el protocolo git. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git daemon [--verbose] [--syslog] [--export-all]
	   [--timeout=<n>] [--init-timeout=<n>] [--max-connections=<n>]
	   [--strict-paths] [--base-path=<path>] [--base-path-relaxed]
	   [--user-path | --user-path=<path>]
```

### Uso verificado con `git version 2.51.1`

```text
git daemon [--verbose] [--syslog] [--export-all]
           [--timeout=<n>] [--init-timeout=<n>] [--max-connections=<n>]
           [--strict-paths] [--base-path=<path>] [--base-path-relaxed]
           [--user-path | --user-path=<path>]
           [--interpolated-path=<path>]
           [--reuseaddr] [--pid-file=<file>]
           [--(enable|disable|allow-override|forbid-override)=<service>]
           [--access-hook=<path>]
           [--inetd | [--listen=<host_or_ipaddr>] [--port=<n>]
                      [--detach] [--user=<user> [--group=<group>]]
           [--log-destination=(stderr|syslog|none)]
           [<directory>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git daemon -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

servir repositorios mediante el protocolo git. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git daemon a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git daemon con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--verbose`

Aumenta el detalle enviado a la salida.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git daemon --verbose --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--syslog`

Activa syslog durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, syslog modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --syslog --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--export-all`

Incluye elementos adicionales dentro del alcance indicado.

La opción limita o amplía el conjunto sobre el que se ejecuta servir repositorios mediante el protocolo git. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git daemon --export-all --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--timeout`

Activa timeout durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, timeout modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --timeout --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--init-timeout`

Activa init timeout durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, init timeout modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --init-timeout --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-connections`

Establece un límite numérico para la selección o el recorrido.

En `git daemon`, máximo connections modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --max-connections --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--strict-paths`

Activa strict paths durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, strict paths modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --strict-paths --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--base-path`

Activa base ruta durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, base ruta modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --base-path --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--base-path-relaxed`

Activa base ruta relaxed durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, base ruta relaxed modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --base-path-relaxed --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--user-path`

Activa user ruta durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, user ruta modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --user-path --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--interpolated-path`

Activa interpolated ruta durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, interpolated ruta modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --interpolated-path --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reuseaddr`

Activa reuseaddr durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, reuseaddr modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pid-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia cómo `git daemon` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git daemon --pid-file --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--access-hook`

Activa access hook durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, access hook modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --access-hook --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--inetd`

Activa inetd durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, inetd modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --inetd --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--listen`

Activa listen durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, listen modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --listen --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--port`

Activa port durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, port modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --port --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--detach`

Hace que `HEAD` apunte directamente a un commit.

En `git daemon`, HEAD separado modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --detach --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--user`

Activa user durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, user modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --user --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--group`

Activa group durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, group modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --group --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--log-destination`

Activa log destination durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git daemon`, log destination modifica la forma en que se ejecuta servir repositorios mediante el protocolo git. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git daemon --log-destination --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git daemon` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El repositorio no se anuncia

Comprueba esta causa: La ruta, exportación o política no lo permite. Comprueba la raíz del servicio y los marcadores de exportación.

### La negociación se corta

Comprueba esta causa: Cliente y servidor no acuerdan capacidad o protocolo. Registra trazas sin incluir credenciales y compara versiones.

### La recepción se rechaza

Comprueba esta causa: Los permisos o hooks bloquean la referencia. Revisa la política del repositorio y el mensaje del hook.

## Automatización y recuperación

Persistencia: Inicia o atiende un servicio. El repositorio cambia solo si el servicio y la política admiten una operación de escritura. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git fetch-pack`](../server-and-transport/fetch-pack.md)
- [`git http-backend`](../server-and-transport/http-backend.md)

## Fuente

- [git-daemon - A really simple server for Git repositories](https://git-scm.com/docs/git-daemon)
