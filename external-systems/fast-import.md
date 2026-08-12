---
title: "git fast-import"
source: "https://git-scm.com/docs/git-fast-import"
section: "external-systems"
status: "source-audited"
version: "2.55.0"
---

# `git fast-import`

Este caso usa `git fast-import` para crear historial y referencias a partir de un flujo de importación.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La integración traduce identidades, ramas y cambios entre dos modelos de control de versiones. Una migración se valida comparando historial, contenido y referencias en el destino.

Define una regla para autores, ramas, etiquetas y finales de línea antes de importar. Valida cada regla con un conjunto que contenga ese caso.

## Ejemplo mínimo

```bash
git init destino
cd destino
git fast-import < ../historial.fi
```

La invocación `git fast-import < ../historial.fi` ejecuta esta operación: crear historial y referencias a partir de un flujo de importación. Después, el destino conserva el contenido, autores, ramas y etiquetas que admita la conversión.

## Sintaxis y formas de invocación

```text
frontend | git fast-import [<options>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git fast-import [--date-format=<f>] [--max-pack-size=<n>] [--big-file-threshold=<n>] [--depth=<n>] [--active-branches=<n>] [--export-marks=<marks.file>]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git fast-import -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--date-format`

Activa fecha formato durante crear historial y referencias a partir de un flujo de importación. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git fast-import --date-format < ../historial.fi
printf 'exit=%s\n' "$?"
```

### `--max-pack-size`

Establece un límite numérico para la selección o el recorrido.

```bash
git fast-import --max-pack-size < ../historial.fi
printf 'exit=%s\n' "$?"
```

### `--big-file-threshold`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia cómo `git fast-import` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git fast-import --big-file-threshold < ../historial.fi
printf 'exit=%s\n' "$?"
```

### `--depth`

Establece un límite numérico para la selección o el recorrido.

```bash
git fast-import --depth < ../historial.fi
printf 'exit=%s\n' "$?"
```

### `--active-branches`

Selecciona o modifica referencias dentro del alcance de la orden.

```bash
git fast-import --active-branches < ../historial.fi
printf 'exit=%s\n' "$?"
```

### `--export-marks`

Activa export marks durante crear historial y referencias a partir de un flujo de importación. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git fast-import --export-marks < ../historial.fi
printf 'exit=%s\n' "$?"
```

### `--signed-commits` y `--signed-tags`

Definen cómo importar firmas incluidas en commits o tags. Los modos son `verbatim` (predeterminado), `warn-verbatim`, `abort`, `strip`, `warn-strip`, `strip-if-invalid`, `sign-if-invalid[=<keyid>]` y `abort-if-invalid`. Los modos `strip*` retiran firmas; `sign-if-invalid` sustituye una firma inválida; los modos `abort*` detienen la importación.

```bash
git fast-import --signed-commits=abort-if-invalid \
  --signed-tags=warn-verbatim < export.fi
git fsck --strict
```

La comprobación posterior valida la estructura importada. Usa `verbatim` solo cuando el flujo de confianza permite conservar firmas sin verificarlas durante la importación.

## Páginas relacionadas

- [`git p4`](../external-systems/p4.md)
- [`git fast-export`](../external-systems/fast-export.md)
- [`git quiltimport`](../external-systems/quiltimport.md)

## Fuente

- [git-fast-import - Backend for fast Git data importers](https://git-scm.com/docs/git-fast-import)
