---
title: "git receive-pack"
source: "https://git-scm.com/docs/git-receive-pack"
section: "server-and-transport"
status: "option-expanded"
---

# `git receive-pack`

Este caso usa `git receive-pack` para recibir objetos y solicitudes de actualización de referencias. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Responsabilidad y efecto

git receive-pack expone repositorios o participa en negociación y transferencia de objetos. Recibe como entrada la ruta del repositorio, el servicio y los parámetros de transporte. La operación consiste en recibir objetos y solicitudes de actualización de referencias.

Puede persistir el estado implicado por esta operación: recibir objetos y solicitudes de actualización de referencias. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git receive-pack /srv/git/biblioteca.git
```

La invocación `git receive-pack /srv/git/biblioteca.git` ejecuta esta operación: recibir objetos y solicitudes de actualización de referencias. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git receive-pack <git-dir>
```

### Uso verificado con `git version 2.51.1`

```text
git receive-pack <git-dir>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git receive-pack -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

recibir objetos y solicitudes de actualización de referencias. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git receive-pack a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git receive-pack con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git receive-pack -q /srv/git/biblioteca.git
git show-ref
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git receive-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió.

#### Ejemplo con `--quiet`

```bash
git receive-pack --quiet /srv/git/biblioteca.git
git show-ref
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git receive-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git receive-pack --no-quiet /srv/git/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git receive-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El repositorio no se anuncia

Comprueba esta causa: La ruta, exportación o política no lo permite. Comprueba la raíz del servicio y los marcadores de exportación.

### La negociación se corta

Comprueba esta causa: Cliente y servidor no acuerdan capacidad o protocolo. Registra trazas sin incluir credenciales y compara versiones.

### La recepción se rechaza

Comprueba esta causa: Los permisos o hooks bloquean la referencia. Revisa la política del repositorio y el mensaje del hook.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: recibir objetos y solicitudes de actualización de referencias. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa repositorios locales o un contenedor de prueba. Registra solicitudes, capacidades anunciadas y cambios de referencias sin exponer el servicio a una red pública.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git send-pack`](../server-and-transport/send-pack.md)
- [`git http-push`](../server-and-transport/http-push.md)
- [`git shell`](../server-and-transport/shell.md)

## Fuente

- [git-receive-pack - Receive what is pushed into the repository](https://git-scm.com/docs/git-receive-pack)
