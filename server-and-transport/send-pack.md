---
title: "git send-pack"
source: "https://git-scm.com/docs/git-send-pack"
section: "server-and-transport"
status: "source-audited"
version: "2.55.0"
---

# `git send-pack`

Este caso usa `git send-pack` para enviar objetos y actualizaciones de referencias al receptor. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git send-pack https://example.com/equipo/biblioteca.git refs/heads/main
```

La invocación `git send-pack https://example.com/equipo/biblioteca.git refs/heads/main` ejecuta esta operación: enviar objetos y actualizaciones de referencias al receptor. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron.

## Sintaxis y formas de invocación

```text
git send-pack [--mirror] [--dry-run] [--force]
		[--receive-pack=<git-receive-pack>]
		[--verbose] [--thin] [--atomic]
		[--[no-]signed | --signed=(true|false|if-asked)]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git send-pack [--mirror] [--dry-run] [--force]
                     [--receive-pack=<git-receive-pack>]
                     [--verbose] [--thin] [--atomic]
                     [--[no-]signed | --signed=(true|false|if-asked)]
                     [<host>:]<directory> (--all | <ref>...)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git send-pack -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--mirror`

Activa espejo durante enviar objetos y actualizaciones de referencias al receptor. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `mirror all refs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-pack --mirror https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dry-run` y `-n`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

#### Ejemplo con `--dry-run`

```bash
git send-pack --dry-run https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió.

### `--force` y `-f`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git send-pack --force https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió.

### `--receive-pack`

Activa receive pack durante enviar objetos y actualizaciones de referencias al receptor. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `receive pack program`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-pack --receive-pack=valor https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

### `--verbose` y `-v`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git send-pack --verbose https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió.

### `--thin`

Define thin para esta ejecución de `git send-pack`. En Git 2.51.1, la ayuda corta expresa el contrato como `use thin pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-pack --thin https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--atomic`

Exige que el conjunto se aplique completo o no se aplique.

```bash
git send-pack --atomic https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signed`

Activa firmado durante enviar objetos y actualizaciones de referencias al receptor. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign the push`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-pack --signed=valor https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

### `--all`

Amplía la selección a todos los elementos del alcance definido.

```bash
git send-pack --all https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git send-pack --quiet https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió.

### `--exec`

Activa exec durante enviar objetos y actualizaciones de referencias al receptor. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `receive pack program`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-pack --exec=valor https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

### `--remote`

Activa remote durante enviar objetos y actualizaciones de referencias al receptor. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `remote name`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-pack --remote=origin https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

El ejemplo usa `origin` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--push-option`

Activa push option durante enviar objetos y actualizaciones de referencias al receptor. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `option to transmit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-pack --push-option=valor https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git send-pack --progress https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stateless-rpc`

Define stateless rpc para esta ejecución de `git send-pack`. En Git 2.51.1, la ayuda corta expresa el contrato como `use stateless RPC protocol`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-pack --stateless-rpc https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git send-pack` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git send-pack --stdin https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--helper-status`

Incluye helper estado en la salida o cambia cómo `git send-pack` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print status from remote helper`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git send-pack --helper-status https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-with-lease`

Omite una protección concreta de la orden; requiere verificar origen y destino.

```bash
git send-pack --force-with-lease=main https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-if-includes`

Omite una protección concreta de la orden; requiere verificar origen y destino.

```bash
git send-pack --force-if-includes https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signed`

Desactiva para esta invocación el comportamiento que habilita `--signed`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git send-pack --no-signed https://example.com/equipo/biblioteca.git refs/heads/main
git show-ref
```

 La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git shell`](../server-and-transport/shell.md)
- [`git receive-pack`](../server-and-transport/receive-pack.md)
- [`git update-server-info`](../server-and-transport/update-server-info.md)

## Fuente

- [git-send-pack - Push objects over Git protocol to another repository](https://git-scm.com/docs/git-send-pack)
