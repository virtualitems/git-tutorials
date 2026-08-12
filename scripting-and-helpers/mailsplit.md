---
title: "git mailsplit"
source: "https://git-scm.com/docs/git-mailsplit"
section: "scripting-and-helpers"
status: "option-expanded"
---

# `git mailsplit`

Este caso usa `git mailsplit` para dividir un buzón mbox o Maildir en mensajes. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git mailsplit ofrece contratos de entrada y salida para scripts, hooks y procesos auxiliares. Recibe como entrada datos controlados por entrada estándar, argumentos o configuración. La operación consiste en dividir un buzón mbox o Maildir en mensajes.

El helper usa stdout, archivos auxiliares o un proceso llamado; su contrato define si persiste datos.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
mkdir mensajes
git mailsplit -o mensajes serie.mbox
```

La invocación `git mailsplit -o mensajes serie.mbox` ejecuta esta operación: dividir un buzón mbox o Maildir en mensajes. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git mailsplit [-b] [-f<nn>] [-d<prec>] [--keep-cr] [--mboxrd]
		-o<directory> [--] [(<mbox>|<Maildir>)…]
```

### Uso verificado con `git version 2.51.1`

```text
git mailsplit [-d<prec>] [-f<n>] [-b] [--keep-cr] -o<directory> [(<mbox>|<Maildir>)...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git mailsplit -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

dividir un buzón mbox o Maildir en mensajes. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git mailsplit a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git mailsplit con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-b`

Activa b durante dividir un buzón mbox o Maildir en mensajes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git mailsplit`, b modifica la forma en que se ejecuta dividir un buzón mbox o Maildir en mensajes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailsplit -b -o mensajes serie.mbox
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mailsplit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f`

Activa f durante dividir un buzón mbox o Maildir en mensajes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git mailsplit`, f modifica la forma en que se ejecuta dividir un buzón mbox o Maildir en mensajes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailsplit -f -o mensajes serie.mbox
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mailsplit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d`

Activa d durante dividir un buzón mbox o Maildir en mensajes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git mailsplit`, d modifica la forma en que se ejecuta dividir un buzón mbox o Maildir en mensajes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailsplit -d -o mensajes serie.mbox
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mailsplit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--keep-cr`

Conserva caracteres CR al procesar mensajes de correo.

En `git mailsplit`, conservar retornos CR modifica la forma en que se ejecuta dividir un buzón mbox o Maildir en mensajes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailsplit --keep-cr -o mensajes serie.mbox
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mailsplit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--mboxrd`

Activa mboxrd durante dividir un buzón mbox o Maildir en mensajes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git mailsplit`, mboxrd modifica la forma en que se ejecuta dividir un buzón mbox o Maildir en mensajes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailsplit --mboxrd -o mensajes serie.mbox
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mailsplit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-o`

Activa o durante dividir un buzón mbox o Maildir en mensajes. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git mailsplit`, o modifica la forma en que se ejecuta dividir un buzón mbox o Maildir en mensajes. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git mailsplit -o mensajes serie.mbox
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git mailsplit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

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

- [`git merge-one-file`](../scripting-and-helpers/merge-one-file.md)
- [`git mailinfo`](../scripting-and-helpers/mailinfo.md)
- [`git patch-id`](../scripting-and-helpers/patch-id.md)

## Fuente

- [git-mailsplit - Simple UNIX mbox splitter program](https://git-scm.com/docs/git-mailsplit)
