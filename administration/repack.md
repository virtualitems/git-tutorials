---
title: "git repack"
source: "https://git-scm.com/docs/git-repack"
section: "administration"
status: "expanded"
---

# `git repack`

Este caso usa `git repack` para reorganizar objetos dentro de archivos pack. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git repack comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Recibe como entrada los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. La operación consiste en reorganizar objetos dentro de archivos pack.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | reorganizar objetos dentro de archivos pack. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: reorganizar objetos dentro de archivos pack. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
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
git count-objects -v
git repack -ad
git count-objects -v
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- La operación observable es: reorganizar objetos dentro de archivos pack.
- La comprobación se realiza mediante: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git repack [-a] [-A] [-d] [-f] [-F] [-l] [-n] [-q] [-b] [-m]
	[--window=<n>] [--depth=<n>] [--threads=<n>] [--keep-pack=<pack-name>]
	[--write-midx[=<mode>]] [--name-hash-version=<n>] [--path-walk]
```

### Uso verificado con `git version 2.51.1`

```text
git repack [-a] [-A] [-d] [-f] [-F] [-l] [-n] [-q] [-b] [-m]
       [--window=<n>] [--depth=<n>] [--threads=<n>] [--keep-pack=<pack-name>]
       [--write-midx] [--name-hash-version=<n>] [--path-walk]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git repack -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | reorganizar objetos dentro de archivos pack | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git repack a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Validación | Comprobar el resultado de git repack con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-a` | Activa la forma corta de selección total o una opción propia de la orden. |
| `-A` | Activa el modo `-A`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-d` | Activa la forma corta de eliminación o una opción propia de la orden. |
| `-f` | Activa la forma corta de la operación forzada. |
| `-F` | Activa el modo `-F`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-l` | Activa el modo `-l`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `-q` | Activa la forma corta del modo sin mensajes. |
| `-b` | Activa el modo `-b`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-m` | Activa el modo `-m`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--window` | Activa el modo `--window`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--depth` | Establece un límite numérico para la selección o el recorrido. |
| `--threads` | Activa el modo `--threads`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--keep-pack` | Activa el modo `--keep-pack`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--write-midx` | Permite crear o escribir el elemento seleccionado. |
| `--name-hash-version` | Selecciona la representación o tratamiento de identificadores de objeto. |
| `--path-walk` | Activa el modo `--path-walk`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--cruft` | Activa el modo `--cruft`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--cruft-expiration` | Activa el modo `--cruft-expiration`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--combine-cruft-below-size` | Activa el modo `--combine-cruft-below-size`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--max-cruft-size` | Establece un límite numérico para la selección o el recorrido. |
| `--no-reuse-delta` | Desactiva el comportamiento `reuse-delta` para esta invocación. |
| `--no-reuse-object` | Desactiva el comportamiento `reuse-object` para esta invocación. |
| `--quiet` | Reduce mensajes que no representan errores. |
| `--local` | Opera sobre la configuración del repositorio. |
| `--write-bitmap-index` | Permite crear o escribir el elemento seleccionado. |
| `-i` | Activa la forma corta del modo interactivo o una opción propia de la orden. |
| `--delta-islands` | Activa el modo `--delta-islands`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--unpack-unreachable` | Activa el modo `--unpack-unreachable`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `-k` | Activa el modo `-k`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--keep-unreachable` | Activa el modo `--keep-unreachable`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--window-memory` | Activa el modo `--window-memory`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--max-pack-size` | Establece un límite numérico para la selección o el recorrido. |
| `--filter` | Activa el modo `--filter`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--pack-kept-objects` | Selecciona la representación o tratamiento de identificadores de objeto. |
| `-g` | Activa el modo `-g`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--geometric` | Activa el modo `--geometric`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |
| `--expire-to` | Aplica una fecha, duración o política de vencimiento. |
| `--filter-to` | Activa el modo `--filter-to`; los argumentos y restricciones aparecen en la sintaxis y en la fuente oficial. |

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

Persistencia: Puede persistir el estado implicado por esta operación: reorganizar objetos dentro de archivos pack. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git replace`](../administration/replace.md)
- [`git reflog`](../administration/reflog.md)
- [`scalar`](../administration/scalar.md)

## Fuente

- [git-repack - Pack unpacked objects in a repository](https://git-scm.com/docs/git-repack)
