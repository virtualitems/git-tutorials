---
title: "git send-pack"
source: "https://git-scm.com/docs/git-send-pack"
section: "server-and-transport"
status: "option-expanded"
---

# `git send-pack`

Este caso usa `git send-pack` para enviar objetos y actualizaciones de referencias al receptor. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Responsabilidad y efecto

git send-pack expone repositorios o participa en negociación y transferencia de objetos. Recibe como entrada la ruta del repositorio, el servicio y los parámetros de transporte. La operación consiste en enviar objetos y actualizaciones de referencias al receptor.

Puede persistir el estado implicado por esta operación: enviar objetos y actualizaciones de referencias al receptor. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git send-pack https://example.test/equipo/biblioteca.git refs/heads/main
```

La invocación `git send-pack https://example.test/equipo/biblioteca.git refs/heads/main` ejecuta esta operación: enviar objetos y actualizaciones de referencias al receptor. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git send-pack [--mirror] [--dry-run] [--force]
		[--receive-pack=<git-receive-pack>]
		[--verbose] [--thin] [--atomic]
		[--[no-]signed | --signed=(true|false|if-asked)]
```

### Uso verificado con `git version 2.51.1`

```text
git send-pack [--mirror] [--dry-run] [--force]
                     [--receive-pack=<git-receive-pack>]
                     [--verbose] [--thin] [--atomic]
                     [--[no-]signed | --signed=(true|false|if-asked)]
                     [<host>:]<directory> (--all | <ref>...)
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git send-pack -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

enviar objetos y actualizaciones de referencias al receptor. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git send-pack a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Simulación

Calcular el efecto sin escribir el estado principal. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Compara la simulación con la selección prevista.

### Validación

Comprobar el resultado de git send-pack con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--mirror`

Activa espejo durante enviar objetos y actualizaciones de referencias al receptor. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `mirror all refs`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git send-pack --mirror https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--dry-run` y `-n`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.  La misma línea de ayuda también acepta `-n`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

#### Ejemplo con `--dry-run`

```bash
git send-pack --dry-run https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió.

#### Ejemplo con `-n`

```bash
git send-pack -n https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--force` y `-f`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.  La misma línea de ayuda también acepta `-f`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque enviar objetos y actualizaciones de referencias al receptor puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `--force`

```bash
git send-pack --force https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió.

#### Ejemplo con `-f`

```bash
git send-pack -f https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--receive-pack`

Activa receive pack durante enviar objetos y actualizaciones de referencias al receptor. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `receive pack program`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-pack`, receive pack modifica la forma en que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-pack --receive-pack=valor https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--verbose` y `-v`

Aumenta el detalle enviado a la salida.  La misma línea de ayuda también acepta `-v`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `--verbose`

```bash
git send-pack --verbose https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió.

#### Ejemplo con `-v`

```bash
git send-pack -v https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--thin`

Define thin para esta ejecución de `git send-pack`. En Git 2.51.1, la ayuda corta expresa el contrato como `use thin pack`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-pack`, thin modifica la forma en que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-pack --thin https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--atomic`

Exige que el conjunto se aplique completo o no se aplique.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git send-pack --atomic https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--signed`

Activa firmado durante enviar objetos y actualizaciones de referencias al receptor. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `GPG sign the push`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-pack`, firmado modifica la forma en que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-pack --signed=valor https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

La opción limita o amplía el conjunto sobre el que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git send-pack --all https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git send-pack -q https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió.

#### Ejemplo con `--quiet`

```bash
git send-pack --quiet https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--exec`

Activa exec durante enviar objetos y actualizaciones de referencias al receptor. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `receive pack program`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-pack`, exec modifica la forma en que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-pack --exec=valor https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--remote`

Activa remote durante enviar objetos y actualizaciones de referencias al receptor. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `remote name`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-pack`, remote modifica la forma en que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-pack --remote=origin https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

El ejemplo usa `origin` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--push-option`

Activa push option durante enviar objetos y actualizaciones de referencias al receptor. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `option to transmit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git send-pack`, push option modifica la forma en que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-pack --push-option=valor https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

La opción controla progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque enviar objetos y actualizaciones de referencias al receptor puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git send-pack --progress https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stateless-rpc`

Define stateless rpc para esta ejecución de `git send-pack`. En Git 2.51.1, la ayuda corta expresa el contrato como `use stateless RPC protocol`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git send-pack --stateless-rpc https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git send-pack` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git send-pack --stdin https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--helper-status`

Incluye helper estado en la salida o cambia cómo `git send-pack` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `print status from remote helper`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git send-pack --helper-status https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-with-lease`

Omite una protección concreta de la orden; requiere verificar origen y destino.

La opción controla omitir la protección with lease. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque enviar objetos y actualizaciones de referencias al receptor puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git send-pack --force-with-lease=main https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--force-if-includes`

Omite una protección concreta de la orden; requiere verificar origen y destino.

La opción controla omitir la protección if includes. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque enviar objetos y actualizaciones de referencias al receptor puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git send-pack --force-if-includes https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-mirror`

Desactiva para esta invocación el comportamiento que habilita `--mirror`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git send-pack --no-mirror https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-dry-run`

Desactiva para esta invocación el comportamiento que habilita `--dry-run`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git send-pack --no-dry-run https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force`

Desactiva para esta invocación el comportamiento que habilita `--force`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque enviar objetos y actualizaciones de referencias al receptor puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git send-pack --no-force https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-receive-pack`

Desactiva para esta invocación el comportamiento que habilita `--receive-pack`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-pack`, desactivar receive pack modifica la forma en que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-pack --no-receive-pack https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-verbose`

Desactiva para esta invocación el comportamiento que habilita `--verbose`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git send-pack --no-verbose https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-thin`

Desactiva para esta invocación el comportamiento que habilita `--thin`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-pack`, desactivar thin modifica la forma en que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-pack --no-thin https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-atomic`

Desactiva para esta invocación el comportamiento que habilita `--atomic`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git send-pack --no-atomic https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-signed`

Desactiva para esta invocación el comportamiento que habilita `--signed`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-pack`, desactivar firmado modifica la forma en que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-pack --no-signed https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-all`

Desactiva para esta invocación el comportamiento que habilita `--all`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git send-pack --no-all https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git send-pack --no-quiet https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-exec`

Desactiva para esta invocación el comportamiento que habilita `--exec`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-pack`, desactivar exec modifica la forma en que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-pack --no-exec https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-remote`

Desactiva para esta invocación el comportamiento que habilita `--remote`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-pack`, desactivar remote modifica la forma en que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-pack --no-remote https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-push-option`

Desactiva para esta invocación el comportamiento que habilita `--push-option`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git send-pack`, desactivar push option modifica la forma en que se ejecuta enviar objetos y actualizaciones de referencias al receptor. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git send-pack --no-push-option https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque enviar objetos y actualizaciones de referencias al receptor puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git send-pack --no-progress https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stateless-rpc`

Desactiva para esta invocación el comportamiento que habilita `--stateless-rpc`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git send-pack --no-stateless-rpc https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stdin`

Desactiva para esta invocación el comportamiento que habilita `--stdin`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git send-pack` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git send-pack --no-stdin https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-helper-status`

Desactiva para esta invocación el comportamiento que habilita `--helper-status`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git send-pack --no-helper-status https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force-with-lease`

Desactiva para esta invocación el comportamiento que habilita `--force-with-lease`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección with lease. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque enviar objetos y actualizaciones de referencias al receptor puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git send-pack --no-force-with-lease https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force-if-includes`

Desactiva para esta invocación el comportamiento que habilita `--force-if-includes`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección if includes. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque enviar objetos y actualizaciones de referencias al receptor puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git send-pack --no-force-if-includes https://example.test/equipo/biblioteca.git refs/heads/main
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git send-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El repositorio no se anuncia

Comprueba esta causa: La ruta, exportación o política no lo permite. Comprueba la raíz del servicio y los marcadores de exportación.

### La negociación se corta

Comprueba esta causa: Cliente y servidor no acuerdan capacidad o protocolo. Registra trazas sin incluir credenciales y compara versiones.

### La recepción se rechaza

Comprueba esta causa: Los permisos o hooks bloquean la referencia. Revisa la política del repositorio y el mensaje del hook.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: enviar objetos y actualizaciones de referencias al receptor. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git shell`](../server-and-transport/shell.md)
- [`git receive-pack`](../server-and-transport/receive-pack.md)
- [`git update-server-info`](../server-and-transport/update-server-info.md)

## Fuente

- [git-send-pack - Push objects over Git protocol to another repository](https://git-scm.com/docs/git-send-pack)
