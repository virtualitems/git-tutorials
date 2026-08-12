---
title: "git daemon"
source: "https://git-scm.com/docs/git-daemon"
section: "server-and-transport"
status: "source-audited"
version: "2.55.0"
---

# `git daemon`

Este caso usa `git daemon` para servir repositorios mediante el protocolo git. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git daemon --reuseaddr --base-path=/srv/git /srv/git
```

La invocación `git daemon --reuseaddr --base-path=/srv/git /srv/git` ejecuta esta operación: servir repositorios mediante el protocolo git. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Sintaxis y formas de invocación

```text
git daemon [--verbose] [--syslog] [--export-all]
	   [--timeout=<n>] [--init-timeout=<n>] [--max-connections=<n>]
	   [--strict-paths] [--base-path=<path>] [--base-path-relaxed]
	   [--user-path | --user-path=<path>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

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

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--verbose`

Aumenta el detalle enviado a la salida.

```bash
git daemon --verbose --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--syslog`

Activa syslog durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --syslog --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--export-all`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git daemon --export-all --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--timeout`

Activa timeout durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --timeout --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--init-timeout`

Activa init timeout durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --init-timeout --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--max-connections`

Establece un límite numérico para la selección o el recorrido.

```bash
git daemon --max-connections --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--strict-paths`

Activa strict paths durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --strict-paths --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--base-path`

Activa base ruta durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --base-path --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--base-path-relaxed`

Activa base ruta relaxed durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --base-path-relaxed --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--user-path`

Activa user ruta durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --user-path --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--interpolated-path`

Activa interpolated ruta durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --interpolated-path --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reuseaddr`

Activa reuseaddr durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pid-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia cómo `git daemon` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git daemon --pid-file --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--access-hook`

Activa access hook durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --access-hook --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--inetd`

Activa inetd durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --inetd --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--listen`

Activa listen durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --listen --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--port`

Activa port durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --port --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--detach`

Hace que `HEAD` apunte directamente a un commit.

```bash
git daemon --detach --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--user`

Activa user durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --user --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--group`

Activa group durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --group --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--log-destination`

Activa log destination durante servir repositorios mediante el protocolo git. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git daemon --log-destination --reuseaddr --base-path=/srv/git /srv/git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--enable` y `--disable`

Activan o desactivan por defecto un servicio para todas las rutas atendidas, por ejemplo `upload-pack`, `upload-archive` o `receive-pack`. Un repositorio puede cambiar el valor si el servicio permite sobrescritura.

```bash
git daemon --verbose --export-all \
  --enable=upload-pack --disable=receive-pack /srv/git
```

### `--allow-override` y `--forbid-override`

Permiten o impiden que la configuración de cada repositorio sustituya el valor global del servicio. De forma predeterminada todos los servicios permiten esa sustitución.

```bash
git daemon --export-all \
  --disable=upload-archive \
  --allow-override=upload-archive /srv/git
```

Un repositorio servido por esa instancia puede activar el archivo con `daemon.uploadarch=true`.

### `--informative-errors` y `--no-informative-errors`

La forma positiva distingue errores como repositorio inexistente y repositorio no exportado. Esa precisión revela información sobre rutas no publicadas. La forma negativa, que es la predeterminada, responde `access denied` en todos esos casos.

```bash
git daemon --no-informative-errors --export-all /srv/git
```

## Páginas relacionadas

- [`git fetch-pack`](../server-and-transport/fetch-pack.md)
- [`git http-backend`](../server-and-transport/http-backend.md)

## Fuente

- [git-daemon - A really simple server for Git repositories](https://git-scm.com/docs/git-daemon)
