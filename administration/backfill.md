---
title: "git backfill"
source: "https://git-scm.com/docs/git-backfill"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `git backfill`

Este caso usa `git backfill` para descargar en lotes los objetos que faltan en un clon parcial.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git clone --filter=blob:none https://example.com/biblioteca.git
cd biblioteca
git backfill main~50..main
```

La invocación `git backfill main~50..main` ejecuta esta operación: descargar en lotes los objetos que faltan en un clon parcial. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
git backfill [--min-batch-size=<n>] [--[no-]sparse] [--[no-]include-edges] [<revision-range>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git backfill [--min-batch-size=<n>] [--[no-]sparse]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git backfill -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--min-batch-size`

Establece un límite numérico para la selección o el recorrido.

La opción cambia cómo `git backfill` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git backfill --min-batch-size=5 main~50..main
git count-objects -vH
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--sparse`

Permite operar sobre entradas que quedan fuera de la selección sparse activa.

```bash
git backfill --sparse main~50..main
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include-edges`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git backfill --include-edges main~50..main
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-sparse`

Desactiva para esta invocación el comportamiento que habilita `--sparse`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git backfill --no-sparse main~50..main
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--include-edges` y `--no-include-edges`

Incluye o excluye los blobs de los commits que forman el límite del rango. La inclusión es el valor predeterminado y permite que operaciones posteriores como `git log -p A..B` dispongan también de los blobs de `A`.

```bash
git backfill --no-include-edges HEAD~10..HEAD
git fsck --connectivity-only
```

La segunda orden comprueba que los objetos necesarios para la conectividad sigan disponibles.

## Páginas relacionadas

- [`git clean`](../administration/clean.md)
- [`git archive`](../administration/archive.md)
- [`git count-objects`](../administration/count-objects.md)

## Fuente

- [git-backfill - Download missing objects in a partial clone](https://git-scm.com/docs/git-backfill)
