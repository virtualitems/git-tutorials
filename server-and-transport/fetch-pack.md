---
title: "git fetch-pack"
source: "https://git-scm.com/docs/git-fetch-pack"
section: "server-and-transport"
status: "source-audited"
version: "2.55.0"
---

# `git fetch-pack`

Este caso usa `git fetch-pack` para solicitar a otro repositorio los objetos que faltan. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git fetch-pack https://example.com/equipo/biblioteca.git refs/heads/main
```

La invocación `git fetch-pack https://example.com/equipo/biblioteca.git refs/heads/main` ejecuta esta operación: solicitar a otro repositorio los objetos que faltan. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Sintaxis y formas de invocación

```text
git fetch-pack [--all] [--quiet|-q] [--keep|-k] [--thin] [--include-tag]
	[--upload-pack=<git-upload-pack>]
	[--depth=<n>] [--no-progress]
	[-v] <repository> [<refs>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git fetch-pack [--all] [--stdin] [--quiet | -q] [--keep | -k] [--thin] [--include-tag] [--upload-pack=<git-upload-pack>] [--depth=<n>] [--no-progress] [--diag-url] [-v] [<host>:]<directory> [<refs>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git fetch-pack -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git fetch-pack --all https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quiet`

Reduce mensajes que no representan errores.

```bash
git fetch-pack --quiet https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q`

Activa q durante solicitar a otro repositorio los objetos que faltan. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git fetch-pack -q https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep`

Conserva el asunto del mensaje recibido según la forma que define el comando.

```bash
git fetch-pack --keep https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-k`

Activa k durante solicitar a otro repositorio los objetos que faltan. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git fetch-pack -k https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--thin`

Activa thin durante solicitar a otro repositorio los objetos que faltan. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git fetch-pack --thin https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include-tag`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git fetch-pack --include-tag https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--upload-pack`

Activa upload pack durante solicitar a otro repositorio los objetos que faltan. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git fetch-pack --upload-pack https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--depth`

Establece un límite numérico para la selección o el recorrido.

```bash
git fetch-pack --depth https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva la presentación de progreso.

```bash
git fetch-pack --no-progress https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v`

Activa v durante solicitar a otro repositorio los objetos que faltan. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git fetch-pack -v https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git fetch-pack` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fetch-pack --stdin https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--diag-url`

Activa diag url durante solicitar a otro repositorio los objetos que faltan. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git fetch-pack --diag-url https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git http-backend`](../server-and-transport/http-backend.md)
- [`git daemon`](../server-and-transport/daemon.md)
- [`git http-fetch`](../server-and-transport/http-fetch.md)

## Fuente

- [git-fetch-pack - Receive missing objects from another repository](https://git-scm.com/docs/git-fetch-pack)
