---
title: "git fetch-pack"
source: "https://git-scm.com/docs/git-fetch-pack"
section: "server-and-transport"
status: "option-expanded"
---

# `git fetch-pack`

Este caso usa `git fetch-pack` para solicitar a otro repositorio los objetos que faltan. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Responsabilidad y efecto

git fetch-pack expone repositorios o participa en negociación y transferencia de objetos. Recibe como entrada la ruta del repositorio, el servicio y los parámetros de transporte. La operación consiste en solicitar a otro repositorio los objetos que faltan.

Puede persistir el estado implicado por esta operación: solicitar a otro repositorio los objetos que faltan. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git fetch-pack https://example.test/equipo/biblioteca.git refs/heads/main
```

La invocación `git fetch-pack https://example.test/equipo/biblioteca.git refs/heads/main` ejecuta esta operación: solicitar a otro repositorio los objetos que faltan. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git fetch-pack [--all] [--quiet|-q] [--keep|-k] [--thin] [--include-tag]
	[--upload-pack=<git-upload-pack>]
	[--depth=<n>] [--no-progress]
	[-v] <repository> [<refs>…]
```

### Uso verificado con `git version 2.51.1`

```text
git fetch-pack [--all] [--stdin] [--quiet | -q] [--keep | -k] [--thin] [--include-tag] [--upload-pack=<git-upload-pack>] [--depth=<n>] [--no-progress] [--diag-url] [-v] [<host>:]<directory> [<refs>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git fetch-pack -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

solicitar a otro repositorio los objetos que faltan. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git fetch-pack a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git fetch-pack con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

La opción limita o amplía el conjunto sobre el que se ejecuta solicitar a otro repositorio los objetos que faltan. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch-pack --all https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quiet`

Reduce mensajes que no representan errores.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git fetch-pack --quiet https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q`

Activa q durante solicitar a otro repositorio los objetos que faltan. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git fetch-pack`, q modifica la forma en que se ejecuta solicitar a otro repositorio los objetos que faltan. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch-pack -q https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep`

Conserva el asunto del mensaje recibido según la forma que define el comando.

En `git fetch-pack`, conservar modifica la forma en que se ejecuta solicitar a otro repositorio los objetos que faltan. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch-pack --keep https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-k`

Activa k durante solicitar a otro repositorio los objetos que faltan. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git fetch-pack`, k modifica la forma en que se ejecuta solicitar a otro repositorio los objetos que faltan. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch-pack -k https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--thin`

Activa thin durante solicitar a otro repositorio los objetos que faltan. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git fetch-pack`, thin modifica la forma en que se ejecuta solicitar a otro repositorio los objetos que faltan. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch-pack --thin https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include-tag`

Selecciona o modifica referencias dentro del alcance de la orden.

La opción limita o amplía el conjunto sobre el que se ejecuta solicitar a otro repositorio los objetos que faltan. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch-pack --include-tag https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--upload-pack`

Activa upload pack durante solicitar a otro repositorio los objetos que faltan. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git fetch-pack`, upload pack modifica la forma en que se ejecuta solicitar a otro repositorio los objetos que faltan. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch-pack --upload-pack https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--depth`

Establece un límite numérico para la selección o el recorrido.

En `git fetch-pack`, profundidad modifica la forma en que se ejecuta solicitar a otro repositorio los objetos que faltan. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch-pack --depth https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva la presentación de progreso.

En `git fetch-pack`, desactivar progreso modifica la forma en que se ejecuta solicitar a otro repositorio los objetos que faltan. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch-pack --no-progress https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v`

Activa v durante solicitar a otro repositorio los objetos que faltan. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta solicitar a otro repositorio los objetos que faltan. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git fetch-pack -v https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git fetch-pack` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fetch-pack --stdin https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--diag-url`

Activa diag url durante solicitar a otro repositorio los objetos que faltan. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git fetch-pack`, diag url modifica la forma en que se ejecuta solicitar a otro repositorio los objetos que faltan. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git fetch-pack --diag-url https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git fetch-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El repositorio no se anuncia

Comprueba esta causa: La ruta, exportación o política no lo permite. Comprueba la raíz del servicio y los marcadores de exportación.

### La negociación se corta

Comprueba esta causa: Cliente y servidor no acuerdan capacidad o protocolo. Registra trazas sin incluir credenciales y compara versiones.

### La recepción se rechaza

Comprueba esta causa: Los permisos o hooks bloquean la referencia. Revisa la política del repositorio y el mensaje del hook.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: solicitar a otro repositorio los objetos que faltan. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git http-backend`](../server-and-transport/http-backend.md)
- [`git daemon`](../server-and-transport/daemon.md)
- [`git http-fetch`](../server-and-transport/http-fetch.md)

## Fuente

- [git-fetch-pack - Receive missing objects from another repository](https://git-scm.com/docs/git-fetch-pack)
