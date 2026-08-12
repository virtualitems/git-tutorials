---
title: "git cvsexportcommit"
source: "https://git-scm.com/docs/git-cvsexportcommit"
section: "external-systems"
status: "option-expanded"
---

# `git cvsexportcommit`

Este caso usa `git cvsexportcommit` para aplicar un commit de Git sobre un checkout de CVS. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git cvsexportcommit traduce historial, referencias e identidades entre Git y otro sistema. Recibe como entrada la ubicación y los nombres que deben traducirse desde el sistema de origen. La operación consiste en aplicar un commit de Git sobre un checkout de CVS.

Puede persistir el estado implicado por esta operación: aplicar un commit de Git sobre un checkout de CVS. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Ejemplo mínimo

```bash
git cvsexportcommit -w /tmp/checkout-cvs HEAD
```

La invocación `git cvsexportcommit -w /tmp/checkout-cvs HEAD` ejecuta esta operación: aplicar un commit de Git sobre un checkout de CVS. Después, el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git cvsexportcommit [-h] [-u] [-v] [-c] [-P] [-p] [-a] [-d <cvsroot>]
	[-w <cvs-workdir>] [-W] [-f] [-m <msgprefix>] [<parent-commit>] <commit-id>
```

### Uso verificado con `git version 2.51.1`

```text
GIT_DIR=/path/to/.git git cvsexportcommit [-h] [-p] [-v] [-c] [-f] [-u] [-k] [-w cvsworkdir] [-m msgprefix] [ parent ] commit
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git cvsexportcommit -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

aplicar un commit de Git sobre un checkout de CVS. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git cvsexportcommit a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git cvsexportcommit con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-h`

Muestra ayuda corta cuando la orden admite esta convención.

En `git cvsexportcommit`, h modifica la forma en que se ejecuta aplicar un commit de Git sobre un checkout de CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsexportcommit -h
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsexportcommit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-u`

Activa u durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsexportcommit`, u modifica la forma en que se ejecuta aplicar un commit de Git sobre un checkout de CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsexportcommit -u -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsexportcommit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v`

Activa v durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta aplicar un commit de Git sobre un checkout de CVS. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git cvsexportcommit -v -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsexportcommit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-c`

Aplica una clave de configuración solo a esta invocación.

En `git cvsexportcommit`, c modifica la forma en que se ejecuta aplicar un commit de Git sobre un checkout de CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsexportcommit -c -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsexportcommit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-P`

Activa P durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsexportcommit`, P modifica la forma en que se ejecuta aplicar un commit de Git sobre un checkout de CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsexportcommit -P -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsexportcommit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p`

Activa p durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsexportcommit`, p modifica la forma en que se ejecuta aplicar un commit de Git sobre un checkout de CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsexportcommit -p -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsexportcommit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a`

Activa a durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsexportcommit`, a modifica la forma en que se ejecuta aplicar un commit de Git sobre un checkout de CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsexportcommit -a -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsexportcommit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d`

Activa d durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsexportcommit`, d modifica la forma en que se ejecuta aplicar un commit de Git sobre un checkout de CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsexportcommit -d -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsexportcommit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-w`

Activa w durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsexportcommit`, w modifica la forma en que se ejecuta aplicar un commit de Git sobre un checkout de CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsexportcommit -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsexportcommit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-W`

Activa W durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsexportcommit`, W modifica la forma en que se ejecuta aplicar un commit de Git sobre un checkout de CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsexportcommit -W -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsexportcommit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-f`

Activa f durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsexportcommit`, f modifica la forma en que se ejecuta aplicar un commit de Git sobre un checkout de CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsexportcommit -f -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsexportcommit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m`

Activa m durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsexportcommit`, m modifica la forma en que se ejecuta aplicar un commit de Git sobre un checkout de CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsexportcommit -m -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsexportcommit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-k`

Activa k durante aplicar un commit de Git sobre un checkout de CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsexportcommit`, k modifica la forma en que se ejecuta aplicar un commit de Git sobre un checkout de CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsexportcommit -k -w /tmp/checkout-cvs HEAD
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsexportcommit` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Faltan revisiones

Comprueba esta causa: El rango, rama o marcador de importación las excluye. Compara conteos y el último identificador importado.

### La identidad cambia

Comprueba esta causa: No existe una regla de mapeo estable. Define el mapa antes de repetir la importación.

### La sincronización duplica cambios

Comprueba esta causa: Se perdió el marcador entre sistemas. Restaura el punto de control y prueba sobre una copia.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: aplicar un commit de Git sobre un checkout de CVS. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git cvsimport`](../external-systems/cvsimport.md)
- [`git archimport`](../external-systems/archimport.md)
- [`git cvsserver`](../external-systems/cvsserver.md)

## Fuente

- [git-cvsexportcommit - Export a single commit to a CVS checkout](https://git-scm.com/docs/git-cvsexportcommit)
