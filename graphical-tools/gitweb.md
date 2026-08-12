---
title: "gitweb"
source: "https://git-scm.com/docs/gitweb"
section: "graphical-tools"
status: "option-expanded"
---

# `gitweb`

Este caso usa `gitweb` para publicar repositorios mediante una interfaz web. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

gitweb presenta commits, cambios o acciones mediante una interfaz de escritorio o HTTP. Recibe como entrada el repositorio y la vista u operación elegida en la interfaz. La operación consiste en publicar repositorios mediante una interfaz web.

Inicia o atiende un servicio. El repositorio cambia solo si el servicio y la política admiten una operación de escritura.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

La interfaz presenta operaciones que también existen en el modelo de objetos, índice, referencias y commits. La vista cambia; el repositorio conserva el mismo estado.

Relaciona cada acción de la interfaz con índice, commit o referencia. Usa una consulta de Git para comprobar el cambio de estado.

## Ejemplo mínimo

```bash
GITWEB_CONFIG=/etc/gitweb.conf gitweb.cgi
```

La invocación `gitweb` ejecuta esta operación: publicar repositorios mediante una interfaz web. Después, los comandos de consulta confirman el mismo estado que presenta la interfaz. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
GITWEB_CONFIG=/etc/gitweb.conf gitweb.cgi
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa la fuente oficial enlazada para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

publicar repositorios mediante una interfaz web. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar gitweb a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de gitweb con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Errores y diagnóstico

### La interfaz no inicia

Comprueba esta causa: Falta el entorno gráfico, un intérprete o un puerto. Comprueba dependencias y ejecuta desde el repositorio.

### No aparecen cambios

Comprueba esta causa: La herramienta abrió otra ruta o referencia. Confirma la raíz y la referencia mostradas.

### El servicio queda activo

Comprueba esta causa: El proceso web se ejecuta en segundo plano. Usa la orden de parada de la herramienta y verifica el puerto.

## Automatización y recuperación

Persistencia: Inicia o atiende un servicio. El repositorio cambia solo si el servicio y la política admiten una operación de escritura. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Realiza una operación en la interfaz y verifica el resultado con `git status`, `git log` o `git show`.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`gitk`](../graphical-tools/gitk.md)
- [`git instaweb`](../graphical-tools/instaweb.md)

## Fuente

- [gitweb - Git web interface (web frontend to Git repositories)](https://git-scm.com/docs/gitweb)
