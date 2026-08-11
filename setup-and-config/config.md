---
title: "git config"
source: "https://git-scm.com/docs/git-config"
section: "setup-and-config"
status: "expanded"
---

# `git config`

Este caso usa `git config` para leer y cambiar opciones de configuración por ámbito. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git config define cómo Git localiza configuración, ejecutables, repositorios y diagnósticos. Recibe como entrada el ámbito, la clave o el dato del entorno indicado por la orden. La operación consiste en leer y cambiar opciones de configuración por ámbito.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | el ámbito, la clave o el dato del entorno indicado por la orden. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | leer y cambiar opciones de configuración por ámbito. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Las formas de escritura modifican el archivo del alcance seleccionado; las formas get y list solo consultan. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git config --show-origin --list`, `git version` o el archivo generado. |

## Requisitos y laboratorio

Crea un repositorio de prueba y aplica cambios de configuración con `--local`. Así evitas modificar la configuración global.

```bash
lab_dir="$(mktemp -d)"
git init "$lab_dir/proyecto"
git -C "$lab_dir/proyecto" config user.name "Persona de prueba"
git -C "$lab_dir/proyecto" config user.email "prueba@example.test"
printf 'línea base\n' > "$lab_dir/proyecto/archivo.txt"
git -C "$lab_dir/proyecto" add archivo.txt
git -C "$lab_dir/proyecto" commit -m "base"
cd "$lab_dir/proyecto"
```

Antes de ejecutar el ejemplo, confirma la raíz con `git rev-parse --show-toplevel` cuando exista un repositorio. Registra `git status --short` y las referencias que puedan cambiar.

## Modelo de funcionamiento

Git combina opciones de sistema, usuario, repositorio, área de trabajo y línea de comandos. La opción con mayor precedencia determina el valor que usa la operación.

Separa el valor solicitado del ámbito donde Git lo busca. Una misma clave puede producir otro resultado en un repositorio o con una opción de línea de comandos.

Para comprobar el resultado: una consulta posterior muestra el valor efectivo o la información generada. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git config --global user.name "Ana Torres"
git config --global user.email ana@example.test
git config --get user.name
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: el ámbito, la clave o el dato del entorno indicado por la orden.
- La operación observable es: leer y cambiar opciones de configuración por ámbito.
- La comprobación se realiza mediante: una consulta posterior muestra el valor efectivo o la información generada.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

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

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | leer y cambiar opciones de configuración por ámbito | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git config a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git config con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--includes` | Activa el modo `--includes`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--all` | Amplía la selección a todos los elementos del alcance definido. |
| `--regexp` | Activa el modo `--regexp`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--value` | Activa el modo `--value`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--fixed-value` | Activa el modo `--fixed-value`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--default` | Activa el modo `--default`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--url` | Activa el modo `--url`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--type` | Activa el modo `--type`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--get-colorbool` | Activa el modo `--get-colorbool`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| El valor aplicado no coincide | Otra capa de configuración tiene precedencia | Ejecuta `git config --show-origin --get-all <clave>`. |
| Git no localiza el repositorio | `--git-dir`, `--work-tree` o el directorio actual apuntan a otra ruta | Ejecuta `git rev-parse --show-toplevel`. |
| La orden no existe | La versión instalada no incluye la función | Comprueba `git --version` y `git help -a`. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: Las formas de escritura modifican el archivo del alcance seleccionado; las formas get y list solo consultan. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Ejecuta el ejemplo en un repositorio temporal y usa `git config --show-origin --list` o el comando de consulta correspondiente para identificar el origen del resultado.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git bugreport`](../setup-and-config/bugreport.md)
- [`git`](../setup-and-config/git.md)
- [`git diagnose`](../setup-and-config/diagnose.md)

## Fuente

- [git-config - Get and set repository or global options](https://git-scm.com/docs/git-config)
