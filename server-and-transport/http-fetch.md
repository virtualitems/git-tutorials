---
title: "git http-fetch"
source: "https://git-scm.com/docs/git-http-fetch"
section: "server-and-transport"
status: "source-audited"
version: "2.55.0"
---

# `git http-fetch`

Este caso usa `git http-fetch` para descargar objetos mediante el transporte HTTP heredado. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git http-fetch HEAD https://example.com/equipo/biblioteca.git
```

La invocación `git http-fetch HEAD https://example.com/equipo/biblioteca.git` ejecuta esta operación: descargar objetos mediante el transporte HTTP heredado. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Sintaxis y formas de invocación

```text
git http-fetch [-c] [-t] [-a] [-d] [-v] [-w <filename>] [--recover] [--stdin | --packfile=<hash> | <commit>] <URL>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git http-fetch [-c] [-t] [-a] [-v] [--recover] [-w ref] [--stdin | --packfile=hash | commit-id] url
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git http-fetch -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-c`

Aplica una clave de configuración solo a esta invocación.

```bash
git http-fetch -c HEAD https://example.com/equipo/biblioteca.git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-t`

Activa t durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git http-fetch -t HEAD https://example.com/equipo/biblioteca.git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a`

Activa a durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git http-fetch -a HEAD https://example.com/equipo/biblioteca.git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d`

Activa d durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git http-fetch -d HEAD https://example.com/equipo/biblioteca.git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v`

Activa v durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git http-fetch -v HEAD https://example.com/equipo/biblioteca.git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-w`

Activa w durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git http-fetch -w HEAD https://example.com/equipo/biblioteca.git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recover`

Activa recover durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git http-fetch --recover HEAD https://example.com/equipo/biblioteca.git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git http-fetch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git http-fetch --stdin HEAD https://example.com/equipo/biblioteca.git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--packfile`

Activa packfile durante descargar objetos mediante el transporte HTTP heredado. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia cómo `git http-fetch` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git http-fetch --packfile HEAD https://example.com/equipo/biblioteca.git
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git http-push`](../server-and-transport/http-push.md)
- [`git http-backend`](../server-and-transport/http-backend.md)
- [`git receive-pack`](../server-and-transport/receive-pack.md)

## Fuente

- [git-http-fetch - Download from a remote Git repository via HTTP](https://git-scm.com/docs/git-http-fetch)
