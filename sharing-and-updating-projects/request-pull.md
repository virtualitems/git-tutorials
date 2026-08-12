---
title: "git request-pull"
source: "https://git-scm.com/docs/git-request-pull"
section: "sharing-and-updating-projects"
status: "option-expanded"
---

# `git request-pull`

Este caso usa `git request-pull` para generar un resumen para solicitar que otra persona integre cambios. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git request-pull anuncia, descarga o actualiza objetos y referencias entre repositorios. Recibe como entrada el repositorio, las referencias y el sentido de la transferencia. La operación consiste en generar un resumen para solicitar que otra persona integre cambios.

Genera un archivo o flujo de salida; no mueve referencias por sí mismo.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). La relación entre URL, remoto y refspec se desarrolla en [`git remote`](../sharing-and-updating-projects/remote.md#remotos-y-refspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Ejemplo mínimo

```bash
git request-pull v1.0 https://example.test/equipo/biblioteca.git main
```

La invocación `git request-pull v1.0 https://example.test/equipo/biblioteca.git main` ejecuta esta operación: generar un resumen para solicitar que otra persona integre cambios. Después, las referencias locales y remotas permiten separar descarga, integración y publicación. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git request-pull [-p] <start> <URL> [<end>]
```

### Uso verificado con `git version 2.51.1`

```text
git request-pull [options] start url [end]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git request-pull -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

generar un resumen para solicitar que otra persona integre cambios. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git request-pull a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git request-pull con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-p`

Incluye p en la salida o cambia cómo `git request-pull` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show patch text as well`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git request-pull -p v1.0 https://example.test/equipo/biblioteca.git main
git branch -vv
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git request-pull` o a otra opción. La salida permite comparar la rama local con su upstream. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El refspec no coincide

Comprueba esta causa: La parte de origen no resuelve una referencia. Comprueba la referencia local y escribe el refspec completo.

### La actualización se rechaza

Comprueba esta causa: El destino perdería commits o una política lo impide. Integra primero o usa una protección con lease tras verificar el remoto.

### La rama no tiene upstream

Comprueba esta causa: No existe asociación entre rama local y remota. Configura el upstream y confirma con `git branch -vv`.

## Automatización y recuperación

Persistencia: Genera un archivo o flujo de salida; no mueve referencias por sí mismo. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git submodule`](../sharing-and-updating-projects/submodule.md)
- [`git remote`](../sharing-and-updating-projects/remote.md)
- [`git push`](../sharing-and-updating-projects/push.md)

## Fuente

- [git-request-pull - Generates a summary of pending changes](https://git-scm.com/docs/git-request-pull)
