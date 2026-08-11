---
title: "git count-objects"
source: "https://git-scm.com/docs/git-count-objects"
section: "plumbing-commands"
canonical_file: "administration/count-objects.md"
status: "expanded"
---

# `git count-objects`

> Esta ruta conserva la clasificación `plumbing-commands`. La guía canónica está en [`administration/count-objects.md`](../administration/count-objects.md). Ambas documentan la misma URL del sitemap.

Este caso usa `git count-objects` para medir objetos sueltos, packs y espacio ocupado. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git count-objects comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Recibe como entrada los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. La operación consiste en medir objetos sueltos, packs y espacio ocupado.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | medir objetos sueltos, packs y espacio ocupado. | Comprueba el resultado con una orden de lectura. |
| Persistencia | No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. | Compara el estado antes y después. |
| Resultado | La orden comunica datos por stdout y diagnósticos por stderr. | Captura también el código de terminación. |
| Fuente de verdad | El repositorio y la configuración efectiva determinan el resultado. | Usa `git fsck`, `git count-objects -vH` y una lista de referencias antes y después. |

## Requisitos y laboratorio

Clona o copia un repositorio de prueba. Registra referencias y tamaño antes de una operación que elimine datos.

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

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

Para comprobar el resultado: los modos de simulación y las consultas de tamaño muestran el efecto antes y después. La verificación debe observar un estado distinto del canal que produjo el cambio.

## Ejemplo mínimo

```bash
git count-objects -v -H
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- La operación observable es: medir objetos sueltos, packs y espacio ocupado.
- La comprobación se realiza mediante: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git count-objects [-v] [-H | --human-readable]
```

### Uso verificado con `git version 2.51.1`

```text
git count-objects [-v] [-H | --human-readable]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git count-objects -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | medir objetos sueltos, packs y espacio ocupado | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git count-objects a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git count-objects con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `-H` | Activa el modo `-H`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--human-readable` | Activa el modo `--human-readable`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--verbose` | Aumenta el detalle enviado a la salida. |

## Selección de entradas

Distingue identificadores de objeto, referencias y rutas. Resuelve revisiones con `git rev-parse --verify`; inspecciona tipo y tamaño con `git cat-file`; usa actualización condicional al escribir referencias.

Comprueba cada entrada con una orden de lectura antes de una escritura. Para listas de rutas generadas por otro proceso, prefiere una interfaz terminada en NUL cuando esté disponible.

## Salida y códigos de terminación

Un código 0 indica que la operación terminó bajo el contrato solicitado. Trata cualquier código distinto de cero según la función; no deduzcas el estado solo a partir de que stdout esté vacío.

No analices mensajes destinados a personas si existe un formato de máquina. Declara los campos, desactiva color y conserva stderr para diagnóstico.

## Errores y diagnóstico

| Señal | Causa que debes comprobar | Acción |
| --- | --- | --- |
| Un objeto aparece como inalcanzable | Ninguna referencia o reflog lo conserva | Determina si debe recuperarse antes de podar. |
| El tamaño no disminuye | Los objetos siguen alcanzables o aún están protegidos por reflogs | Inspecciona alcanzabilidad y vencimientos. |
| La operación se interrumpe | Otro proceso mantiene un lock | Comprueba procesos activos antes de retirar un lock obsoleto. |

Si una operación deja archivos de estado dentro de `.git`, usa `git status` y la acción de continuar, omitir o abortar definida por esa operación. No borres esos archivos para simular una cancelación.

## Automatización

1. Declara la versión mínima de Git que necesita el script.
2. Resuelve la raíz del repositorio y evita depender del directorio actual.
3. Separa opciones y rutas con `--`.
4. Captura stdout, stderr y el código de terminación.
5. Usa formatos de máquina o terminación NUL para nombres de archivo.
6. Ejecuta primero sobre el laboratorio y añade un caso sin coincidencias.

## Seguridad y recuperación

Persistencia: No modifica el repositorio en su forma de consulta. Puede iniciar un visor o escribir un archivo si se solicita de forma explícita. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git filter-branch`](../administration/filter-branch.md)
- [`git clean`](../administration/clean.md)
- [`git fsck`](../administration/fsck.md)

## Fuente

- [git-count-objects - Count unpacked number of objects and their disk consumption](https://git-scm.com/docs/git-count-objects)
