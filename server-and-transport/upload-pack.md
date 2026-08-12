---
title: "git upload-pack"
source: "https://git-scm.com/docs/git-upload-pack"
section: "server-and-transport"
status: "option-expanded"
---

# `git upload-pack`

Este caso usa `git upload-pack` para negociar y enviar objetos a un cliente de fetch. Las rutas, cuentas y direcciones del ejemplo pertenecen a un entorno de prueba. Define autenticación y permisos antes de adaptar el servicio.

## Responsabilidad y efecto

git upload-pack expone repositorios o participa en negociación y transferencia de objetos. Recibe como entrada la ruta del repositorio, el servicio y los parámetros de transporte. La operación consiste en negociar y enviar objetos a un cliente de fetch.

Inicia o atiende un servicio. El repositorio cambia solo si el servicio y la política admiten una operación de escritura.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

El cliente anuncia lo que tiene y solicita lo que necesita. El servidor negocia, empaqueta objetos y acepta o rechaza cambios de referencias según su configuración.

Separa negociación de objetos, transferencia y actualización de referencias. Los permisos del servicio pueden aceptar una fase y rechazar otra.

## Ejemplo mínimo

```bash
git upload-pack /srv/git/biblioteca.git
```

La invocación `git upload-pack /srv/git/biblioteca.git` ejecuta esta operación: negociar y enviar objetos a un cliente de fetch. Después, los registros y referencias confirman qué objetos se transfirieron y qué actualizaciones se aceptaron. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git-upload-pack [--[no-]strict] [--timeout=<n>] [--stateless-rpc]
		  [--advertise-refs] <directory>
```

### Uso verificado con `git version 2.51.1`

```text
git-upload-pack [--[no-]strict] [--timeout=<n>] [--stateless-rpc]
                       [--advertise-refs] <directory>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git upload-pack -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

negociar y enviar objetos a un cliente de fetch. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git upload-pack a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git upload-pack con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--strict`

Impide strict durante esta invocación de `git upload-pack`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not try <directory>/.git/ if <directory> is no Git directory`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git upload-pack`, strict modifica la forma en que se ejecuta negociar y enviar objetos a un cliente de fetch. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git upload-pack --strict /srv/git/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git upload-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--timeout`

Activa timeout durante negociar y enviar objetos a un cliente de fetch. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `interrupt transfer after <n> seconds of inactivity`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git upload-pack`, timeout modifica la forma en que se ejecuta negociar y enviar objetos a un cliente de fetch. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git upload-pack --timeout=5 /srv/git/biblioteca.git
git show-ref
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stateless-rpc`

Activa stateless rpc durante negociar y enviar objetos a un cliente de fetch. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `quit after a single request/response exchange`. Conserva esa formulación al comparar el efecto entre versiones de Git.

Esta forma se usa cuando `git upload-pack` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque stateless rpc actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git upload-pack --stateless-rpc /srv/git/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git upload-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--advertise-refs`

Selecciona o modifica referencias dentro del alcance de la orden.

En `git upload-pack`, advertise referencias modifica la forma en que se ejecuta negociar y enviar objetos a un cliente de fetch. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git upload-pack --advertise-refs /srv/git/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git upload-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-strict`

Desactiva para esta invocación el comportamiento que habilita `--strict`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git upload-pack`, desactivar strict modifica la forma en que se ejecuta negociar y enviar objetos a un cliente de fetch. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git upload-pack --no-strict /srv/git/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git upload-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-timeout`

Desactiva para esta invocación el comportamiento que habilita `--timeout`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git upload-pack`, desactivar timeout modifica la forma en que se ejecuta negociar y enviar objetos a un cliente de fetch. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git upload-pack --no-timeout /srv/git/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git upload-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-stateless-rpc`

Desactiva para esta invocación el comportamiento que habilita `--stateless-rpc`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

Esta forma se usa cuando `git upload-pack` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque desactivar stateless rpc actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git upload-pack --no-stateless-rpc /srv/git/biblioteca.git
git show-ref
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git upload-pack` o a otra opción. La lista de referencias permite identificar qué valor permaneció o cambió. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

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

- [`git upload-archive`](../server-and-transport/upload-archive.md)
- [`git update-server-info`](../server-and-transport/update-server-info.md)

## Fuente

- [git-upload-pack - Send objects packed back to git-fetch-pack](https://git-scm.com/docs/git-upload-pack)
