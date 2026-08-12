---
title: "git config"
source: "https://git-scm.com/docs/git-config"
section: "setup-and-config"
status: "option-expanded"
---

# `git config`

Este caso usa `git config` para leer y cambiar opciones de configuración por ámbito. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git config define cómo Git localiza configuración, ejecutables, repositorios y diagnósticos. Recibe como entrada el ámbito, la clave o el dato del entorno indicado por la orden. La operación consiste en leer y cambiar opciones de configuración por ámbito.

Las formas de escritura modifican el archivo del alcance seleccionado; las formas get y list solo consultan.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

## Ejemplo mínimo

```bash
git config --global user.name "Ana Torres"
git config --global user.email ana@example.test
git config --get user.name
```

La invocación `git config --global user.name "Ana Torres"` ejecuta esta operación: leer y cambiar opciones de configuración por ámbito. Después, una consulta posterior muestra el valor efectivo o la información generada. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git config list [<file-option>] [<display-option>] [--includes]
git config get [<file-option>] [<display-option>] [--includes] [--all] [--regexp] [--value=<pattern>] [--fixed-value] [--default=<default>] [--url=<url>] <name>
git config set [<file-option>] [--type=<type>] [--all] [--value=<pattern>] [--fixed-value] <name> <value>
git config unset [<file-option>] [--all] [--value=<pattern>] [--fixed-value] <name>
```

### Uso verificado con `git version 2.51.1`

```text
git config list [<file-option>] [<display-option>] [--includes]
   or: git config get [<file-option>] [<display-option>] [--includes] [--all] [--regexp] [--value=<pattern>] [--fixed-value] [--default=<default>] [--url=<url>] <name>
   or: git config set [<file-option>] [--type=<type>] [--all] [--value=<pattern>] [--fixed-value] <name> <value>
   or: git config unset [<file-option>] [--all] [--value=<pattern>] [--fixed-value] <name>
   or: git config rename-section [<file-option>] <old-name> <new-name>
   or: git config remove-section [<file-option>] <name>
   or: git config edit [<file-option>]
   or: git config [<file-option>] --get-colorbool <name> [<stdout-is-tty>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git config -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

leer y cambiar opciones de configuración por ámbito. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git config a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git config con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `--includes`

Activa includes durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción limita o amplía el conjunto sobre el que se ejecuta leer y cambiar opciones de configuración por ámbito. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git config --includes --global user.name "Ana Torres"
git config --show-origin --list
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git config` o a otra opción. La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--all`

Amplía la selección a todos los elementos del alcance definido.

La opción limita o amplía el conjunto sobre el que se ejecuta leer y cambiar opciones de configuración por ámbito. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git config --all --global user.name "Ana Torres"
git config --show-origin --list
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git config` o a otra opción. La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--regexp`

Activa regexp durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git config`, regexp modifica la forma en que se ejecuta leer y cambiar opciones de configuración por ámbito. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git config --regexp --global user.name "Ana Torres"
git config --show-origin --list
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git config` o a otra opción. La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--value`

Activa value durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git config`, value modifica la forma en que se ejecuta leer y cambiar opciones de configuración por ámbito. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git config --value --global user.name "Ana Torres"
git config --show-origin --list
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git config` o a otra opción. La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--fixed-value`

Activa fixed value durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git config`, fixed value modifica la forma en que se ejecuta leer y cambiar opciones de configuración por ámbito. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git config --fixed-value --global user.name "Ana Torres"
git config --show-origin --list
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git config` o a otra opción. La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--default`

Activa default durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git config`, default modifica la forma en que se ejecuta leer y cambiar opciones de configuración por ámbito. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git config --default --global user.name "Ana Torres"
git config --show-origin --list
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git config` o a otra opción. La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--url`

Activa url durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git config`, url modifica la forma en que se ejecuta leer y cambiar opciones de configuración por ámbito. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git config --url --global user.name "Ana Torres"
git config --show-origin --list
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git config` o a otra opción. La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--type`

Activa type durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

En `git config`, type modifica la forma en que se ejecuta leer y cambiar opciones de configuración por ámbito. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git config --type --global user.name "Ana Torres"
git config --show-origin --list
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git config` o a otra opción. La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--get-colorbool`

Activa get colorbool durante leer y cambiar opciones de configuración por ámbito. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git config --get-colorbool --global user.name "Ana Torres"
git config --show-origin --list
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git config` o a otra opción. La salida identifica el archivo que aporta cada valor. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### El valor aplicado no coincide

Comprueba esta causa: Otra capa de configuración tiene precedencia. Ejecuta `git config --show-origin --get-all <clave>`.

### Git no localiza el repositorio

Comprueba esta causa: `--git-dir`, `--work-tree` o el directorio actual apuntan a otra ruta. Ejecuta `git rev-parse --show-toplevel`.

### La orden no existe

Comprueba esta causa: La versión instalada no incluye la función. Comprueba `git --version` y `git help -a`.

## Automatización y recuperación

Persistencia: Las formas de escritura modifican el archivo del alcance seleccionado; las formas get y list solo consultan. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Ejecuta el ejemplo en un repositorio temporal y usa `git config --show-origin --list` o el comando de consulta correspondiente para identificar el origen del resultado.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git bugreport`](../setup-and-config/bugreport.md)
- [`git`](../setup-and-config/git.md)
- [`git diagnose`](../setup-and-config/diagnose.md)

## Fuente

- [git-config - Get and set repository or global options](https://git-scm.com/docs/git-config)
