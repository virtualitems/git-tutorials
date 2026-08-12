---
title: "Referencia de Git"
source: "https://git-scm.com/docs"
section: "overview"
status: "option-expanded"
---

# `Referencia de Git`

Este caso usa `Referencia de Git` para localizar comandos y guías dentro de la referencia de Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

Referencia de Git organiza las páginas por estado, tipo de entrada y efecto observable. Recibe como entrada el nombre del comando o concepto que quieres consultar. La operación consiste en localizar comandos y guías dentro de la referencia de Git.

La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina.

## Preparación

 Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La referencia organiza comandos de usuario, comandos de plomería, guías y formatos. El nombre de una página identifica una operación o un modelo que otras páginas reutilizan.

Usa el nombre de la operación como punto de entrada. Sigue los enlaces conceptuales cuando la sintaxis dependa de revisiones, rutas, atributos o protocolos.

## Ejemplo mínimo

```bash
git help --all
git help revisions
git help gitignore
```

La invocación `Referencia de Git` ejecuta esta operación: localizar comandos y guías dentro de la referencia de Git. Después, la página elegida enlaza su sintaxis, su modelo y sus referencias relacionadas. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git help --all
git help revisions
git help gitignore
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

localizar comandos y guías dentro de la referencia de Git. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar Referencia de Git a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de Referencia de Git con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

La opción limita o amplía el conjunto sobre el que se ejecuta localizar comandos y guías dentro de la referencia de Git. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git help --all
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `Referencia de Git` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Una página no aparece

Comprueba esta causa: La versión instalada no contiene ese comando. Consulta `git --version` y la fuente enlazada.

### Un nombre no se reconoce

Comprueba esta causa: Se confundió una orden con una guía o un formato. Comprueba si se invoca como `git <orden>` o se consulta como documento.

### La ruta lleva a otra sección

Comprueba esta causa: Una función participa en más de un flujo. Usa la página canónica indicada por el índice.

## Automatización y recuperación

Persistencia: La guía no ejecuta cambios. Un productor que implemente el formato o regla puede escribir la salida que su contrato defina. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Abre la página de referencia, elige un comando y sigue sus enlaces hacia una guía conceptual y un formato relacionado.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- Consulta el índice de la sección.

## Fuente

- [Referencia de Git](https://git-scm.com/docs)
