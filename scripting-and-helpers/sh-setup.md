---
title: "git sh-setup"
source: "https://git-scm.com/docs/git-sh-setup"
section: "scripting-and-helpers"
status: "expanded"
---

# `git sh-setup`

Este caso usa `git sh-setup` para cargar funciones comunes para scripts de shell de Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git sh-setup ofrece contratos de entrada y salida para scripts, hooks y procesos auxiliares. Recibe como entrada datos controlados por entrada estándar, argumentos o configuración. La operación consiste en cargar funciones comunes para scripts de shell de Git.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | datos controlados por entrada estándar, argumentos o configuración. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | cargar funciones comunes para scripts de shell de Git. | Comprueba el resultado con una orden de lectura. |
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
. "$(git --exec-path)/git-sh-setup"
require_work_tree
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: datos controlados por entrada estándar, argumentos o configuración.
- La operación observable es: cargar funciones comunes para scripts de shell de Git.
- La comprobación se realiza mediante: la salida y el código de retorno distinguen el caso aceptado del rechazado.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
. "$(git --exec-path)/git-sh-setup"
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git sh-setup -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | cargar funciones comunes para scripts de shell de Git | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git sh-setup a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git sh-setup con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--exec-path` | Activa el modo `--exec-path`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--help` | Muestra la ayuda correspondiente a la versión instalada. |

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

- [`git stripspace`](../scripting-and-helpers/stripspace.md)
- [`git sh-i18n`](../scripting-and-helpers/sh-i18n.md)
- [`git url-parse`](../scripting-and-helpers/url-parse.md)

## Fuente

- [git-sh-setup - Common Git shell script setup code](https://git-scm.com/docs/git-sh-setup)
