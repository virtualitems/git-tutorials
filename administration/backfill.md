---
title: "git backfill"
source: "https://git-scm.com/docs/git-backfill"
section: "administration"
status: "expanded"
---

# `git backfill`

Este caso usa `git backfill` para descargar en lotes los objetos que faltan en un clon parcial. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git backfill comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Recibe como entrada los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. La operación consiste en descargar en lotes los objetos que faltan en un clon parcial.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | descargar en lotes los objetos que faltan en un clon parcial. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: descargar en lotes los objetos que faltan en un clon parcial. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
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
git clone --filter=blob:none https://example.test/biblioteca.git
cd biblioteca
git backfill main~50..main
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- La operación observable es: descargar en lotes los objetos que faltan en un clon parcial.
- La comprobación se realiza mediante: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git backfill [--min-batch-size=<n>] [--[no-]sparse] [--[no-]include-edges] [<revision-range>]
```

### Uso verificado con `git version 2.51.1`

```text
git backfill [--min-batch-size=<n>] [--[no-]sparse]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git backfill -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | descargar en lotes los objetos que faltan en un clon parcial | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git backfill a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git backfill con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `--min-batch-size` | Establece un límite numérico para la selección o el recorrido. |
| `--sparse` | Permite operar sobre entradas que quedan fuera de la selección sparse activa. |
| `--include-edges` | Incluye elementos adicionales dentro del alcance indicado. |

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

Persistencia: Puede persistir el estado implicado por esta operación: descargar en lotes los objetos que faltan en un clon parcial. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git clean`](../administration/clean.md)
- [`git archive`](../administration/archive.md)
- [`git count-objects`](../administration/count-objects.md)

## Fuente

- [git-backfill - Download missing objects in a partial clone](https://git-scm.com/docs/git-backfill)
