---
title: "git credential-store"
source: "https://git-scm.com/docs/git-credential-store"
section: "scripting-and-helpers"
status: "option-expanded"
---

# `git credential-store`

Este caso usa `git credential-store` para guardar credenciales sin cifrado en un archivo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git credential-store ofrece contratos de entrada y salida para scripts, hooks y procesos auxiliares. Recibe como entrada datos controlados por entrada estándar, argumentos o configuración. La operación consiste en guardar credenciales sin cifrado en un archivo.

El helper usa stdout, archivos auxiliares o un proceso llamado; su contrato define si persiste datos.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
git config --global credential.helper store
```

La invocación `git credential-store` ejecuta esta operación: guardar credenciales sin cifrado en un archivo. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git config credential.helper 'store [<options>]'
```

### Uso verificado con `git version 2.51.1`

```text
git credential-store [<options>] <action>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git credential-store -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

guardar credenciales sin cifrado en un archivo. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git credential-store a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git credential-store con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--file`

Usa el archivo indicado en vez de la ubicación por defecto.

La opción cambia cómo `git credential-store` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git credential-store --file=archivo.txt
printf 'exit=%s\n' "$?"
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-file`

Desactiva para esta invocación el comportamiento que habilita `--file`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git credential-store` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git credential-store --no-file
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git credential-store` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

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

- [`git fmt-merge-msg`](../scripting-and-helpers/fmt-merge-msg.md)
- [`git credential-cache`](../scripting-and-helpers/credential-cache.md)
- [`git hook`](../scripting-and-helpers/hook.md)

## Fuente

- [git-credential-store - Helper to store credentials on disk](https://git-scm.com/docs/git-credential-store)
