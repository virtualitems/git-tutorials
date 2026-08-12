---
title: "git citool"
source: "https://git-scm.com/docs/git-citool"
section: "graphical-tools"
status: "option-expanded"
---

# `git citool`

Este caso usa `git citool` para preparar y crear commits desde una interfaz gráfica. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git citool presenta commits, cambios o acciones mediante una interfaz de escritorio o HTTP. Recibe como entrada el repositorio y la vista u operación elegida en la interfaz. La operación consiste en preparar y crear commits desde una interfaz gráfica.

Puede persistir el estado implicado por esta operación: preparar y crear commits desde una interfaz gráfica. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La interfaz presenta operaciones que también existen en el modelo de objetos, índice, referencias y commits. La vista cambia; el repositorio conserva el mismo estado.

Relaciona cada acción de la interfaz con índice, commit o referencia. Usa una consulta de Git para comprobar el cambio de estado.

## Ejemplo mínimo

```bash
git citool
```

La invocación `git citool` ejecuta esta operación: preparar y crear commits desde una interfaz gráfica. Después, los comandos de consulta confirman el mismo estado que presenta la interfaz. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git citool
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git citool -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

preparar y crear commits desde una interfaz gráfica. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git citool a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git citool con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-h`

Activa h durante preparar y crear commits desde una interfaz gráfica. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git citool`, h modifica la forma en que se ejecuta preparar y crear commits desde una interfaz gráfica. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git citool -h
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git citool` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La interfaz no inicia

Comprueba esta causa: Falta el entorno gráfico, un intérprete o un puerto. Comprueba dependencias y ejecuta desde el repositorio.

### No aparecen cambios

Comprueba esta causa: La herramienta abrió otra ruta o referencia. Confirma la raíz y la referencia mostradas.

### El servicio queda activo

Comprueba esta causa: El proceso web se ejecuta en segundo plano. Usa la orden de parada de la herramienta y verifica el puerto.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: preparar y crear commits desde una interfaz gráfica. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Realiza una operación en la interfaz y verifica el resultado con `git status`, `git log` o `git show`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git gui`](../graphical-tools/gui.md)
- [`git instaweb`](../graphical-tools/instaweb.md)

## Fuente

- [git-citool - Graphical alternative to git-commit](https://git-scm.com/docs/git-citool)
