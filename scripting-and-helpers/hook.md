---
title: "git hook"
source: "https://git-scm.com/docs/git-hook"
section: "scripting-and-helpers"
status: "expanded"
---

# `git hook`

Este caso usa `git hook` para enumerar o ejecutar hooks mediante Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git hook ofrece contratos de entrada y salida para scripts, hooks y procesos auxiliares. Recibe como entrada datos controlados por entrada estándar, argumentos o configuración. La operación consiste en enumerar o ejecutar hooks mediante Git.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | datos controlados por entrada estándar, argumentos o configuración. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | enumerar o ejecutar hooks mediante Git. | Comprueba el resultado con una orden de lectura. |
| Persistencia | El helper usa stdout, archivos auxiliares o un proceso llamado; su contrato define si persiste datos. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa stdout, stderr y el código de terminación con casos positivos y negativos. |

## Requisitos y laboratorio

Ejecuta los ejemplos en un script con `set -u`. Captura la salida y el código antes de activar `set -e`.

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

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

Para comprobar el resultado: la salida y el código de retorno distinguen el caso aceptado del rechazado. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git hook list pre-commit
git hook run pre-commit
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: datos controlados por entrada estándar, argumentos o configuración.
- La operación observable es: enumerar o ejecutar hooks mediante Git.
- La comprobación se realiza mediante: la salida y el código de retorno distinguen el caso aceptado del rechazado.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git hook run [--allow-unknown-hook-name] [--ignore-missing] [--to-stdin=<path>] [(-j|--jobs) <n>]
	<hook-name> [-- <hook-args>]
git hook list [--allow-unknown-hook-name] [-z] [--show-scope] <hook-name>
```

### Uso verificado con `git version 2.51.1`

```text
git hook run [--ignore-missing] [--to-stdin=<path>] <hook-name> [-- <hook-args>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git hook -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | enumerar o ejecutar hooks mediante Git | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git hook a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Salida para scripts | Producir registros con campos y separadores definidos. | Prueba nombres con espacios y saltos de línea. |
| Validación | Comprobar el resultado de git hook con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--allow-unknown-hook-name` | Activa el modo `--allow-unknown-hook-name`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--ignore-missing` | Permite comprobar rutas ausentes bajo las condiciones que define la orden. |
| `--to-stdin` | Activa el modo `--to-stdin`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-j` | Activa el modo `-j`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--jobs` | Activa el modo `--jobs`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-z` | Termina registros con NUL para evitar división por espacios o saltos de línea. |
| `--show-scope` | Muestra el alcance de cada valor de configuración. |

## Selección de entradas

Las revisiones se resuelven antes que los pathspecs cuando la sintaxis las espera. Usa `--` para separar opciones y rutas. Cita los globos para decidir si los expande el shell o Git.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| Un nombre se divide | El script usa espacios como separador para rutas | Usa NUL o el formato estructurado que admita la orden. |
| Un predicado detiene el script | El código 1 representa una respuesta negativa | Evalúa el código de forma explícita. |
| El helper espera más datos | El protocolo de stdin requiere una línea vacía o longitud | Escribe el terminador definido y conserva el orden de campos. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: El helper usa stdout, archivos auxiliares o un proceso llamado; su contrato define si persiste datos. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git interpret-trailers`](../scripting-and-helpers/interpret-trailers.md)
- [`git fmt-merge-msg`](../scripting-and-helpers/fmt-merge-msg.md)
- [`git mailinfo`](../scripting-and-helpers/mailinfo.md)

## Fuente

- [git-hook - Run Git hooks](https://git-scm.com/docs/git-hook)
