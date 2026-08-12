---
title: "git cvsimport"
source: "https://git-scm.com/docs/git-cvsimport"
section: "external-systems"
status: "option-expanded"
---

# `git cvsimport`

Este caso usa `git cvsimport` para importar historial desde CVS. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git cvsimport traduce historial, referencias e identidades entre Git y otro sistema. Recibe como entrada la ubicación y los nombres que deben traducirse desde el sistema de origen. La operación consiste en importar historial desde CVS.

Puede persistir el estado implicado por esta operación: importar historial desde CVS. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Ejemplo mínimo

```bash
git cvsimport -C biblioteca -r cvs modulo
```

La invocación `git cvsimport -C biblioteca -r cvs modulo` ejecuta esta operación: importar historial desde CVS. Después, el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git cvsimport [-o <branch-for-HEAD>] [-h] [-v] [-d <CVSROOT>]
	      [-A <author-conv-file>] [-p <options-for-cvsps>] [-P <file>]
	      [-C <git-repository>] [-z <fuzz>] [-i] [-k] [-u] [-s <subst>]
	      [-a] [-m] [-M <regex>] [-S <regex>] [-L <commit-limit>]
```

### Uso verificado con `git version 2.51.1`

```text
git cvsimport     # fetch/update GIT from CVS
       [-o branch-for-HEAD] [-h] [-v] [-d CVSROOT] [-A author-conv-file]
       [-p opts-for-cvsps] [-P file] [-C GIT_repository] [-z fuzz] [-i] [-k]
       [-u] [-s subst] [-a] [-m] [-M regex] [-S regex] [-L commitlimit]
       [-r remote] [-R] [CVS_module]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git cvsimport -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

importar historial desde CVS. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git cvsimport a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Salida para scripts

Producir registros con campos y separadores definidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Prueba nombres con espacios y saltos de línea.

### Validación

Comprobar el resultado de git cvsimport con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-o`

Activa o durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, o modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -o -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-h`

Muestra ayuda corta cuando la orden admite esta convención.

En `git cvsimport`, h modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -h
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v`

Activa v durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta importar historial desde CVS. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git cvsimport -v -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d`

Activa d durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, d modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -d -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-A`

Activa A durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, A modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -A -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p`

Activa p durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, p modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -p -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-P`

Activa P durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, P modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -P -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

En `git cvsimport`, C modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

En `git cvsimport`, z modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -z -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-i`

Activa i durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, i modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -i -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-k`

Activa k durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, k modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -k -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-u`

Activa u durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, u modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -u -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-s`

Activa s durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, s modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -s -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a`

Activa a durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, a modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -a -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m`

Activa m durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, m modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -m -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-M`

Activa M durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, M modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -M -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-S`

Activa S durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, S modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -S -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-L`

Activa L durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, L modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -L -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-r`

Activa r durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, r modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -r -C biblioteca cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-R`

Activa R durante importar historial desde CVS. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git cvsimport`, R modifica la forma en que se ejecuta importar historial desde CVS. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git cvsimport -R -C biblioteca -r cvs modulo
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git cvsimport` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Faltan revisiones

Comprueba esta causa: El rango, rama o marcador de importación las excluye. Compara conteos y el último identificador importado.

### La identidad cambia

Comprueba esta causa: No existe una regla de mapeo estable. Define el mapa antes de repetir la importación.

### La sincronización duplica cambios

Comprueba esta causa: Se perdió el marcador entre sistemas. Restaura el punto de control y prueba sobre una copia.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: importar historial desde CVS. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Importa un conjunto de prueba con dos autores, dos ramas y una etiqueta. Compara cantidades, nombres y contenido en el destino.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git cvsserver`](../external-systems/cvsserver.md)
- [`git cvsexportcommit`](../external-systems/cvsexportcommit.md)
- [`git fast-export`](../external-systems/fast-export.md)

## Fuente

- [git-cvsimport - Salvage your data out of another SCM people love to hate](https://git-scm.com/docs/git-cvsimport)
