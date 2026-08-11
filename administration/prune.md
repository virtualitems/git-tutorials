---
title: "git prune"
source: "https://git-scm.com/docs/git-prune"
section: "administration"
status: "expanded"
---

# `git prune`

Este caso usa `git prune` para eliminar objetos sueltos que ningún objeto alcanzable necesita. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Alcance y responsabilidad

git prune comprueba integridad, administra reflogs y reorganiza o elimina datos del almacén. Recibe como entrada los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. La operación consiste en eliminar objetos sueltos que ningún objeto alcanzable necesita.

La página distingue lectura, escritura y resultado:

| Elemento | Relación con la función | Comprobación |
| --- | --- | --- |
| Entrada | los objetos, referencias o archivos de almacenamiento que se van a inspeccionar. | Registra los argumentos y resuelve revisiones antes de ejecutar. |
| Efecto principal | eliminar objetos sueltos que ningún objeto alcanzable necesita. | Comprueba el resultado con una orden de lectura. |
| Persistencia | Puede persistir el estado implicado por esta operación: eliminar objetos sueltos que ningún objeto alcanzable necesita. Las opciones pueden limitar o ampliar ese efecto. | Compara el estado antes y después. |
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
git prune --dry-run
```

Ejecuta el bloque en orden. Conserva los nombres del laboratorio hasta confirmar el resultado. Sustituye rutas, revisiones o URL solo después de identificar su tipo y alcance.

### Resultado esperado

- La entrada queda limitada a: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- La operación observable es: eliminar objetos sueltos que ningún objeto alcanzable necesita.
- La comprobación se realiza mediante: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.
- stdout contiene datos o confirmaciones; stderr contiene diagnósticos. Captura ambos canales cuando automatices.

## Sintaxis

```text
git prune [-n] [-v] [--progress] [--expire <time>] [--] [<head>…]
```

### Uso verificado con `git version 2.51.1`

```text
git prune [-n] [-v] [--progress] [--expire <time>] [--] [<head>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git prune -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Casos de uso

| Caso | Objetivo | Criterio de verificación |
| --- | --- | --- |
| Caso base | eliminar objetos sueltos que ningún objeto alcanzable necesita | Ejecuta el ejemplo mínimo y registra el estado antes y después. |
| Alcance explícito | Aplicar git prune a una referencia, rango o ruta identificada. | Resuelve cada argumento antes de ejecutar y usa `--` para rutas. |
| Simulación | Calcular el efecto sin escribir el estado principal. | Compara la simulación con la selección prevista. |
| Validación | Comprobar el resultado de git prune con una orden de lectura independiente. | No uses la misma salida como única prueba del cambio. |


## Opciones y variaciones

La tabla agrupa las opciones visibles en la sintaxis y en la ayuda corta. Una opción puede tener un significado propio cuando la página lo define; ejecuta la ayuda de tu versión antes de usarla en automatización.

| Opción | Efecto que debes controlar |
| --- | --- |
| `-n` | Activa la forma corta documentada por la sintaxis; en muchas órdenes corresponde a simulación o límite numérico. |
| `-v` | Activa la forma corta de salida con detalle o muestra versión según la orden. |
| `--progress` | Muestra progreso aunque la salida no sea un terminal. |
| `--expire` | Aplica una fecha, duración o política de vencimiento. |
| `--dry-run` | Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio. |
| `--verbose` | Aumenta el detalle enviado a la salida. |
| `--exclude-promisor-objects` | Selecciona la representación o tratamiento de identificadores de objeto. |

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

Persistencia: Puede persistir el estado implicado por esta operación: eliminar objetos sueltos que ningún objeto alcanzable necesita. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

## Práctica guiada

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git reflog`](../administration/reflog.md)
- [`git pack-refs`](../administration/pack-refs.md)
- [`git repack`](../administration/repack.md)

## Fuente

- [git-prune - Prune all unreachable objects from the object database](https://git-scm.com/docs/git-prune)
