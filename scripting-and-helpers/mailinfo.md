---
title: "git mailinfo"
source: "https://git-scm.com/docs/git-mailinfo"
section: "scripting-and-helpers"
status: "option-expanded"
---

# `git mailinfo`

Este caso usa `git mailinfo` para separar metadatos, mensaje y parche de un correo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git mailinfo ofrece contratos de entrada y salida para scripts, hooks y procesos auxiliares. Recibe como entrada datos controlados por entrada estándar, argumentos o configuración. La operación consiste en separar metadatos, mensaje y parche de un correo.

El helper usa stdout, archivos auxiliares o un proceso llamado; su contrato define si persiste datos.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git mailinfo mensaje.txt cambio.patch < correo.eml
```

La invocación `git mailinfo mensaje.txt cambio.patch < correo.eml` ejecuta esta operación: separar metadatos, mensaje y parche de un correo. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git mailinfo [-k|-b] [-u | --encoding=<encoding> | -n]
	       [--[no-]scissors] [--quoted-cr=<action>]
	       <msg> <patch>
```

### Uso verificado con `git version 2.51.1`

```text
git mailinfo [<options>] <msg> <patch> < mail >info
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git mailinfo -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

separar metadatos, mensaje y parche de un correo. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git mailinfo a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git mailinfo con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-k`

Activa k durante separar metadatos, mensaje y parche de un correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `keep subject`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git mailinfo`, k modifica la forma en que se ejecuta separar metadatos, mensaje y parche de un correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailinfo -k mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mailinfo` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-b`

Activa b durante separar metadatos, mensaje y parche de un correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `keep non patch brackets in subject`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git mailinfo`, b modifica la forma en que se ejecuta separar metadatos, mensaje y parche de un correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailinfo -b mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mailinfo` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-u`

Activa u durante separar metadatos, mensaje y parche de un correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `re-code metadata to i18n.commitEncoding`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git mailinfo`, u modifica la forma en que se ejecuta separar metadatos, mensaje y parche de un correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailinfo -u mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mailinfo` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--encoding`

Activa encoding durante separar metadatos, mensaje y parche de un correo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.  La misma línea de ayuda también acepta `-code`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

En `git mailinfo`, encoding modifica la forma en que se ejecuta separar metadatos, mensaje y parche de un correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailinfo --encoding=valor mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-n`

Impide n durante esta invocación de `git mailinfo`. En Git 2.51.1, la ayuda corta expresa el contrato como `disable charset re-coding of metadata`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git mailinfo`, n modifica la forma en que se ejecuta separar metadatos, mensaje y parche de un correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailinfo -n mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mailinfo` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--scissors`

Reconoce la línea scissors y descarta el contenido anterior según el formato de correo. En Git 2.51.1, la ayuda corta expresa el contrato como `use scissors`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git mailinfo`, línea scissors modifica la forma en que se ejecuta separar metadatos, mensaje y parche de un correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailinfo --scissors mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mailinfo` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--quoted-cr`

Define cómo se tratan los caracteres CR que aparecen al final de líneas citadas. En Git 2.51.1, la ayuda corta expresa el contrato como `action when quoted CR is found`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git mailinfo`, contenido citado retornos CR modifica la forma en que se ejecuta separar metadatos, mensaje y parche de un correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailinfo --quoted-cr=warn mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

El ejemplo usa `warn` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--message-id`

Añade el identificador del mensaje de correo al mensaje de commit.  La misma línea de ayuda también acepta `-m` y `-ID`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git mailinfo`, mensaje id modifica la forma en que se ejecuta separar metadatos, mensaje y parche de un correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-m`

```bash
git mailinfo -m mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git mailinfo` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

#### Ejemplo con `--message-id`

```bash
git mailinfo --message-id mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git mailinfo` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--no-scissors`

Desactiva para esta invocación el comportamiento que habilita `--scissors`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git mailinfo`, desactivar línea scissors modifica la forma en que se ejecuta separar metadatos, mensaje y parche de un correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailinfo --no-scissors mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mailinfo` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-message-id`

Desactiva para esta invocación el comportamiento que habilita `--message-id`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git mailinfo`, desactivar mensaje id modifica la forma en que se ejecuta separar metadatos, mensaje y parche de un correo. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailinfo --no-message-id mensaje.txt cambio.patch < correo.eml
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mailinfo` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un nombre se divide

Comprueba esta causa: El script usa espacios como separador para rutas. Usa NUL o el formato estructurado que admita la orden.

### Un predicado detiene el script

Comprueba esta causa: El código 1 representa una respuesta negativa. Evalúa el código de forma explícita.

### El helper espera más datos

Comprueba esta causa: El protocolo de stdin requiere una línea vacía o longitud. Escribe el terminador definido y conserva el orden de campos.

## Automatización y recuperación

Persistencia: El helper usa stdout, archivos auxiliares o un proceso llamado; su contrato define si persiste datos. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git mailsplit`](../scripting-and-helpers/mailsplit.md)
- [`git interpret-trailers`](../scripting-and-helpers/interpret-trailers.md)
- [`git merge-one-file`](../scripting-and-helpers/merge-one-file.md)

## Fuente

- [git-mailinfo - Extracts patch and authorship from a single e-mail message](https://git-scm.com/docs/git-mailinfo)
