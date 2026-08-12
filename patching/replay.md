---
title: "git replay"
source: "https://git-scm.com/docs/git-replay"
section: "patching"
status: "option-expanded"
---

# `git replay`

Este caso usa `git replay` para reproducir commits sobre una base y comunicar el cambio de referencias. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git replay aplica diffs o commits y mantiene un estado que puede continuar o abortarse. Recibe como entrada un parche, un commit o un rango que representa cambios. La operación consiste en reproducir commits sobre una base y comunicar el cambio de referencias.

Puede persistir el estado implicado por esta operación: reproducir commits sobre una base y comunicar el cambio de referencias. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Ejemplo mínimo

```bash
git replay --onto=main main..tema-portada
```

La invocación `git replay --onto=main main..tema-portada` ejecuta esta operación: reproducir commits sobre una base y comunicar el cambio de referencias. Después, el diff y el historial muestran si cambiaron archivos, índice o commits. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
(EXPERIMENTAL!) git replay ([--contained] --onto=<newbase> | --advance=<branch> | --revert=<branch>)
			     [--ref=<ref>] [--ref-action=<mode>] <revision-range>
```

### Uso verificado con `git version 2.51.1`

```text
(EXPERIMENTAL!) git replay ([--contained] --onto <newbase> | --advance <branch>) <revision-range>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git replay -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

reproducir commits sobre una base y comunicar el cambio de referencias. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git replay a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git replay con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--contained`

Activa contained durante reproducir commits sobre una base y comunicar el cambio de referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `advance all branches contained in revision-range`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta reproducir commits sobre una base y comunicar el cambio de referencias. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git replay --contained --onto=main main..tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git replay` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--onto`

Activa onto durante reproducir commits sobre una base y comunicar el cambio de referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `replay onto given commit`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git replay`, onto modifica la forma en que se ejecuta reproducir commits sobre una base y comunicar el cambio de referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git replay --onto=valor main..tema-portada
git status --short
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--advance`

Activa advance durante reproducir commits sobre una base y comunicar el cambio de referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `make replay advance given branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta reproducir commits sobre una base y comunicar el cambio de referencias. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git replay --advance=main --onto=main main..tema-portada
git status --short
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--revert`

Activa revert durante reproducir commits sobre una base y comunicar el cambio de referencias. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git replay`, revert modifica la forma en que se ejecuta reproducir commits sobre una base y comunicar el cambio de referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git replay --revert --onto=main main..tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git replay` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ref`

Selecciona o modifica referencias dentro del alcance de la orden.

En `git replay`, referencia modifica la forma en que se ejecuta reproducir commits sobre una base y comunicar el cambio de referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git replay --ref --onto=main main..tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git replay` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ref-action`

Selecciona o modifica referencias dentro del alcance de la orden.

En `git replay`, referencia action modifica la forma en que se ejecuta reproducir commits sobre una base y comunicar el cambio de referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git replay --ref-action --onto=main main..tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git replay` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-contained`

Desactiva para esta invocación el comportamiento que habilita `--contained`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta reproducir commits sobre una base y comunicar el cambio de referencias. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git replay --no-contained --onto=main main..tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git replay` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-onto`

Desactiva para esta invocación el comportamiento que habilita `--onto`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git replay`, desactivar onto modifica la forma en que se ejecuta reproducir commits sobre una base y comunicar el cambio de referencias. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git replay --no-onto main..tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git replay` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-advance`

Desactiva para esta invocación el comportamiento que habilita `--advance`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta reproducir commits sobre una base y comunicar el cambio de referencias. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git replay --no-advance --onto=main main..tema-portada
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git replay` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### Un parche no aplica

Comprueba esta causa: El contexto no coincide con el contenido actual. Inspecciona los rechazos o resuelve el conflicto antes de continuar.

### La secuencia queda en pausa

Comprueba esta causa: Git espera una resolución o una decisión. Consulta `git status` y usa `--continue`, `--skip` o `--abort`.

### El resultado contiene commits vacíos

Comprueba esta causa: Los cambios ya existen o se resolvieron sin diferencias. Revisa el diff y aplica la política de commits vacíos de la orden.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: reproducir commits sobre una base y comunicar el cambio de referencias. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Trabaja en una rama de prueba. Compara `git diff`, `git diff --staged` y `git log --oneline --graph` antes y después.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git revert`](../patching/revert.md)
- [`git rebase`](../patching/rebase.md)
- [`git cherry-pick`](../patching/cherry-pick.md)

## Fuente

- [git-replay - EXPERIMENTAL: Replay commits on a new base, works with bare repos too](https://git-scm.com/docs/git-replay)
