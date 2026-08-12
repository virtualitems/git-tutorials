---
title: "git sparse-checkout"
source: "https://git-scm.com/docs/git-sparse-checkout"
section: "getting-and-creating-projects"
status: "option-expanded"
---

# `git sparse-checkout`

Este caso usa `git sparse-checkout` para materializar solo una parte de los archivos seguidos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git sparse-checkout crea la base de datos local de objetos y prepara el área de trabajo. Recibe como entrada un directorio, una URL o una selección de rutas. La operación consiste en materializar solo una parte de los archivos seguidos.

Puede persistir el estado implicado por esta operación: materializar solo una parte de los archivos seguidos. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Un repositorio contiene objetos y referencias. Un área de trabajo materializa un commit para que los archivos puedan editarse.

Separa los datos del repositorio de los archivos materializados. Un repositorio bare conserva objetos y referencias sin área de trabajo.

## Ejemplo mínimo

```bash
git sparse-checkout init --cone
git sparse-checkout set app docs
```

La invocación `git sparse-checkout init --cone` ejecuta esta operación: materializar solo una parte de los archivos seguidos. Después, el directorio resultante contiene el repositorio y, cuando corresponde, un área de trabajo. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git sparse-checkout (init | list | set | add | reapply | disable | check-rules | clean) [<options>]
```

### Uso verificado con `git version 2.51.1`

```text
git sparse-checkout (init | list | set | add | reapply | disable | check-rules) [<options>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git sparse-checkout -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

materializar solo una parte de los archivos seguidos. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git sparse-checkout a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git sparse-checkout con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-h`

Activa h durante materializar solo una parte de los archivos seguidos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git sparse-checkout`, h modifica la forma en que se ejecuta materializar solo una parte de los archivos seguidos. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git sparse-checkout -h
printf 'exit=%s\n' "$?"
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git sparse-checkout` o a otra opción. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El destino ya contiene archivos

Comprueba esta causa: La creación o clonación requiere una ruta compatible. Elige un directorio vacío o inicializa la ruta de forma explícita.

### No se recibe una referencia

Comprueba esta causa: El remoto no la anuncia o el filtro la excluye. Ejecuta `git ls-remote <url>` y revisa los filtros.

### Falla la autenticación

Comprueba esta causa: La URL o el helper de credenciales no entrega acceso. Comprueba la URL sin registrar credenciales en el historial del shell.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: materializar solo una parte de los archivos seguidos. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa un directorio temporal. Compara el contenido antes y después, incluidos `.git`, HEAD y las ramas disponibles.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git clone`](../getting-and-creating-projects/clone.md)
- [`git init`](../getting-and-creating-projects/init.md)

## Fuente

- [git-sparse-checkout - Reduce your working tree to a subset of tracked files](https://git-scm.com/docs/git-sparse-checkout)
