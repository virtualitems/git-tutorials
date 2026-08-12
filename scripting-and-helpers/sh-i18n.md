---
title: "git sh-i18n"
source: "https://git-scm.com/docs/git-sh-i18n"
section: "scripting-and-helpers"
status: "option-expanded"
---

# `git sh-i18n`

Este caso usa `git sh-i18n` para cargar funciones de internacionalización en scripts de shell. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git sh-i18n ofrece contratos de entrada y salida para scripts, hooks y procesos auxiliares. Recibe como entrada datos controlados por entrada estándar, argumentos o configuración. La operación consiste en cargar funciones de internacionalización en scripts de shell.

El helper usa stdout, archivos auxiliares o un proceso llamado; su contrato define si persiste datos.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Ejemplo mínimo

```bash
. "$(git --exec-path)/git-sh-i18n"
eval_gettext 'Procesando $archivo'
```

La invocación `git sh-i18n` ejecuta esta operación: cargar funciones de internacionalización en scripts de shell. Después, la salida y el código de retorno distinguen el caso aceptado del rechazado. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
. "$(git --exec-path)/git-sh-i18n"
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git sh-i18n -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

cargar funciones de internacionalización en scripts de shell. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git sh-i18n a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git sh-i18n con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--exec-path`

Activa exec ruta durante cargar funciones de internacionalización en scripts de shell. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git sh-i18n`, exec ruta modifica la forma en que se ejecuta cargar funciones de internacionalización en scripts de shell. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git sh-i18n --exec-path
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git sh-i18n` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--help`

Muestra la ayuda correspondiente a la versión instalada.

En `git sh-i18n`, ayuda modifica la forma en que se ejecuta cargar funciones de internacionalización en scripts de shell. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git sh-i18n --help
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git sh-i18n` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

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

- [`git sh-setup`](../scripting-and-helpers/sh-setup.md)
- [`git patch-id`](../scripting-and-helpers/patch-id.md)
- [`git stripspace`](../scripting-and-helpers/stripspace.md)

## Fuente

- [git-sh-i18n - Git’s i18n setup code for shell scripts](https://git-scm.com/docs/git-sh-i18n)
